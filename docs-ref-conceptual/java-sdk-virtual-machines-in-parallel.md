---
title: Paralleles regionsübergreifendes Erstellen von virtuellen Computern | Microsoft-Dokumentation
description: Beispielcode zum parallelen Erstellen virtueller Computer in verschiedenen Azure-Regionen mithilfe des Azure SDKs für Java
author: rloutlaw
manager: douge
ms.assetid: e5a36699-2d96-4571-84f9-a6af13f3c067
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e20feb555c3a360eceae60c1569af9a00a5cd027
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931196"
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a>Erstellen virtueller Computer in mehreren Regionen über Ihre Java-Anwendungen

[Dieses Beispiel](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) erstellt virtuelle Computer parallel in verschiedenen Azure-Regionen unter Verwendung der [Azure-Verwaltungsbibliotheken für Java](https://github.com/Azure/azure-sdk-for-java).

> [!IMPORTANT]
> In dem Beispiel werden insgesamt 48 virtuelle Computer mit Ubuntu 16.04 LTS und der Größe [STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) in vier Regionen erstellt. Die virtuellen Computer werden durch den Beispielcode vor dem Beenden wieder gelöscht. [Überprüfen Sie Ihre Diensteinschränkungen und Kontingente](http://docs.microsoft.com/azure/azure-subscription-service-limits), bevor Sie dieses Beispiel mit der Standardanzahl von virtuellen Computern ausführen.

## <a name="run-the-sample"></a>Ausführen des Beispiels

Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest. Führen Sie anschließend Folgendes aus:

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java) an.

## <a name="authenticate-with-azure"></a>Authentifizieren über Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a>Festlegen der Standorte und der Anzahl für die virtuellen Computer

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

Dieser `Map`-Code wird im weiteren Verlauf des Beispiels zum Festlegen der weltweiten Verteilung der virtuellen Computer verwendet.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

Die einzelnen Ressourcen in dem Beispiel werden von dieser Ressourcengruppe verwaltet. Dadurch können Sie später die Ressourcengruppe löschen und die Ressourcen komfortabel bereinigen.

## <a name="define-the-virtual-machines"></a>Definieren der virtuellen Computer
```java
// list to store the VirtualMachine definitions
List<Creatable<VirtualMachine>> creatableVirtualMachines = new ArrayList<>();
    
// outer loop: iterate through each region included in the map
for (Map.Entry<Region, Integer> entry : virtualMachinesByLocation.entrySet()) {
    Region region = entry.getKey();
    Integer vmCount = entry.getValue();

    // Define one virtual network Creatable per region for the VMs to share
    String networkName = SdkContext.randomResourceName("vnetCOPD-", 20);
    Creatable<Network> networkCreatable = azure.networks().define(networkName)
           .withRegion(region)
           .withExistingResourceGroup(resourceGroup)
           .withAddressSpace("172.16.0.0/16");

    // Define one storage account Creatable per region for storing VM disks
    String storageAccountName = SdkContext.randomResourceName("stgcopd", 20);
    Creatable<StorageAccount> storageAccountCreatable = azure.storageAccounts()
        .define(storageAccountName)
              .withRegion(region)
              .withExistingResourceGroup(resourceGroup);

    // generate a common prefix for every VM name
    String linuxVMNamePrefix = SdkContext.randomResourceName("vm-", 15);

    // inner loop: iterate once for every VM instance in the region
    for (int i = 1; i <= vmCount; i++) {

        // Create one public IP address Creatable for each VM
        Creatable<PublicIpAddress> publicIpAddressCreatable = azure.publicIpAddresses()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withLeafDomainLabel(SdkContext.randomResourceName("pip", 10));

        publicIpCreatableKeys.add(publicIpAddressCreatable.key());

        // Create one virtual machine Creatable 
        Creatable<VirtualMachine> virtualMachineCreatable = azure.virtualMachines()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withNewPrimaryNetwork(networkCreatable)
             .withPrimaryPrivateIpAddressDynamic()
             .withNewPrimaryPublicIpAddress(publicIpAddressCreatable)
             .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
             .withRootUsername(userName)
             .withSsh(sshKey)
             .withSize(VirtualMachineSizeTypes.STANDARD_DS3_V2)
             .withNewStorageAccount(storageAccountCreatable);
        // add the virtual machine Creatable to the list     
        creatableVirtualMachines.add(virtualMachineCreatable); 
     }
}
```

Die äußere `for`-Schleife durchläuft die einzelnen Regionen und definiert ein Creatable-Objekt für ein virtuelles Netzwerk sowie ein Creatable-Objekt für ein Speicherkonto zur Verwendung durch alle virtuellen Computer in der entsprechenden Region. Weitere Informationen zur Verwendung von Creatable-Objekten für die bedarfsbasierte Ressourcenerstellung bei Verwendung der Verwaltungsbibliotheken finden Sie [hier](java-sdk-azure-concepts.md#Creatables).

Die innere `for`-Schleife ruft ein Creatable-Objekt für die öffentliche IP-Adresse für den virtuellen Computer ab und definiert dann ein Creatable-Objekt für den virtuellen Computer unter Verwendung der Creatable-Objekte für das virtuelle Netzwerk, das Speicherkonto und die öffentliche IP-Adresse, die zuvor definiert wurden.  Anschließend wird das Creatable-Objekt „VirtualMachine“ der Liste `creatableVirtualMachines` hinzugefügt.

## <a name="create-the-virtual-machines"></a>Erstellen der virtuellen Computer

```java
// create all virtual machines defined in the list, return all Creatable objects used
// including networks, public IP addresses, and storage accounts
CreatedResources<VirtualMachine> virtualMachines = azure.virtualMachines().create(creatableVirtualMachines);

// list the IDs of each virtual machine created 
for (VirtualMachine virtualMachine : virtualMachines.values()) {
    System.out.println(virtualMachine.id());
}

// call createdRelatedResource(key) to get the resources used to define the virtual machines. 
// Save the key at the time you define the Creatable to use CreatedResources like this
for (String publicIpCreatableKey : publicIpCreatableKeys) {
    PublicIPAddress pip = 
         (PublicIPAddress) virtualMachines.createdRelatedResource(publicIpCreatableKey);
}
```

Der Aufruf `azure.virtualMachines().create(creatableVirtualMachines)` erstellt alle in der Liste `creatableVirtualMachines` definierten virtuellen Computer parallel in allen Regionen.

Verwenden Sie das zurückgegebene Objekt `CreatedResources<VirtualMachine>`, um auf Ressourcen zuzugreifen, die im Rahmen der Methode `create()` im Azure-Abonnement erstellt wurden (nicht nur den zurückgegebenen Typ `VirtualMachine`). Wandeln Sie den zurückgegebenen Wert von `createdRelatedResources()` in den korrekten Typ um. 

Weitere Informationen zur Verwendung von `Creatable<T>` und `CreatedResources` finden Sie in unserem [Artikel zu Bibliothekkonzepten](java-sdk-azure-concepts.md).

## <a name="delete-the-resource-group"></a>Löschen der Ressourcengruppe 

```java
// finally block deletes the resource group before the code exits
// deleting a resource group deletes all resources created in it
finally {
    try {
        System.out.println("Deleting Resource Group: " + rgName);
        azure.resourceGroups().deleteByName(rgName);
        System.out.println("Deleted Resource Group: " + rgName);
    } catch (NullPointerException npe) {
        System.out.println("Did not create any resources in Azure. No clean up is necessary");
    } catch (Exception g) {
        g.printStackTrace();
    }
}
```

Dieser Block löscht Ressourcen aus dem Beispiel, bevor das Beispiel beendet wird.

## <a name="sample-explanation"></a>Erläuterung des Beispiels

Sehen Sie sich den vollständigen Beispielcode auf [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) an.

Das Beispiel verwendet Objekte vom Typ `Creatable`, um ein virtuelles Netzwerk und ein Speicherkonto für die einzelnen Hostregionen der virtuellen Computer zu definieren. Danach werden Objekte vom Typ `Creatable` für die öffentliche IP-Adresse für die einzelnen virtuellen Computer definiert. Das Beispiel definiert die virtuellen Computer unter Verwendung dieser Objekte vom Typ `Creatable` und fügt die VM-Definition der Liste `virtualMachineCreatable` hinzu.

Nachdem die einzelnen VM-Definitionen der Liste hinzugefügt wurden, erstellt `azure.virtualMachines().create(creatableVirtualMachines)` die einzelnen virtuellen Computer parallel in Azure.

Danach ruft der Beispielcode die IP-Adressen für alle erstellten virtuellen Computer aus dem zurückgegebenen CreatedResources-Objekt ab, um einen [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) für die Verteilung der Last auf die virtuellen Computer zu erstellen. 

Der Block `finally` löscht die Ressourcen aus Ihrem Azure-Abonnement (auch im Falle eines Fehlers).

| Im Beispiel verwendete Klasse | Hinweise
|-------|-------|
| [VirtualMachine](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | Dient zum Abfragen der Eigenschaften sowie zum Verwalten des Zustands virtueller Computer. Wird in Listenform (`azure.virtualMachines().list()`) oder nach Name oder ID (`azure.virtualMachines().getByResourceGroup()`) abgerufen.
| [VirtualMachineSizeTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | Statische Werte, die [Größenoptionen für virtuelle Computer](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) entsprechen und beim Definieren eines virtuellen Computers als Parameter für `withSize()` angegeben werden können.
| [PublicIpAddress](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | Wird für die einzelnen virtuellen Computer über `azure.publicIpAddresses().define()` definiert, aber nicht sofort erstellt. Speichern Sie den Schlüssel für die einzelnen Objekte vom Typ `Creatable`, und rufen Sie sie später über `createdRelatedResource()` ab.
| [KnownLinuxVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | Satz von Optionen für virtuelle Linux-Computer, die beim Definieren eines virtuellen Computers als Parameter für die Methode `withPopularLinuxImage()` angegeben werden können.
| [Network](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | Das Beispiel definiert ein virtuelles Netzwerk für die einzelnen Regionen über `azure.networks().define()`. 

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [next-steps](includes/java-next-steps.md)]