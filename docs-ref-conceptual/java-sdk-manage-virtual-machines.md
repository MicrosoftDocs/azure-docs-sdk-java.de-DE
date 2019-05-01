---
title: Verwalten von virtuellen Azure-Computern mit Java | Microsoft-Dokumentation
description: Beispielcode zum Verwalten virtueller Azure-Computer mit dem Azure SDK für Java
author: rloutlaw
manager: douge
ms.assetid: 88629aee-6279-433e-a08b-4f8e290446d0
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 388b68bfb0fdac70efed5ad5d0f7c957ce915449
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592565"
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a>Verwalten von virtuellen Azure-Computern über Ihre Java-Anwendungen

In [diesem Beispiel](https://github.com/Azure-Samples/compute-java-manage-vm/) werden zum Erstellen und Verwenden von virtuellen Azure-Computern die [Azure-Verwaltungsbibliotheken für Java](https://github.com/Azure/azure-sdk-for-java) verwendet.

## <a name="run-the-sample"></a>Ausführen des Beispiels

Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest. Führen Sie anschließend Folgendes aus:

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) an.

## <a name="authenticate-with-azure"></a>Authentifizierung über Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a>Erstellen eines virtuellen Windows-Computers

```java
// Prepare a data disk for VM
Disk dataDisk = azure.disks().define(SdkContext.randomResourceName("dsk", 30))
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withData()
            .withSizeInGB(50)
            .create();

// create the windows virtual machine with the data disk            
VirtualMachine windowsVM = azure.virtualMachines().define(windowsVmName)
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularWindowsImage(KnownWindowsVirtualMachineImage.WINDOWS_SERVER_2012_R2_DATACENTER)
            .withAdminUsername(userName)
            .withAdminPassword(password)
            .withNewDataDisk(10)
            .withNewDataDisk(dataDiskCreatable)
            .withExistingDataDisk(dataDisk)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

Dieser Code:   

0. definiert ein Creatable-Objekt vom Typ `Disk` mit einer Größe von 50 GB und einem zufälligen Namen zur Verwendung mit einem virtuellen Computer.
0. verwendet die Kette `azure.virtualMachines().define()..create()` zum Erstellen des virtuellen Windows Server 2012-Computers. Die API erstellt das im vorherigen Schritt definierte `Disk`-Element zum gleichen Zeitpunkt wie den virtuellen Computer. An den virtuellen Computer wird zudem über `withNewDataDisk(10)` ein 10-GB-Datenträger angefügt.

Erfahren Sie mehr darüber, wie Sie mit [Creatable<T>-Objekten](java-sdk-azure-concepts.md#Creatables) lokale Darstellungen von Ressourcen definieren und diese Objekte genau dann erstellen, wenn sie von anderen Azure-Ressourcen benötigt werden.

## <a name="stop-start-and-restart-a-virtual-machine"></a>Beenden, Starten und Neustarten eines virtuellen Computers

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

`powerOff()` beendet das Betriebssystem des virtuellen Computers, hebt jedoch die Zuordnung seiner Ressourcen nicht auf.

## <a name="add-a-virtual-machine-to-an-existing-network"></a>Hinzufügen eines virtuellen Computers zu einem vorhandenen Netzwerk

```java
// Get the virtual network the current virtual machine is using
Network network = windowsVM.getPrimaryNetworkInterface().primaryIPConfiguration().getNetwork();

// Create a Linux VM in the same subnet
VirtualMachine linuxVM = azure.virtualMachines().define(linuxVmName)
           .withRegion(region)
           .withExistingResourceGroup(rgName)
           .withExistingPrimaryNetwork(network)
           .withSubnet("subnet1") // default subnet name when no name specified at creation
           .withPrimaryPrivateIPAddressDynamic()
           .withoutPrimaryPublicIPAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withRootPassword(password)
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
```

Definieren Sie mithilfe von `withPopularLinuxImage` anstelle eines virtuellen Windows-Computers einen virtuellen Linux-Computer.


## <a name="list-virtual-machines"></a>Auflisten von virtuellen Computern

```java
// get a list of VMs in the same resource group as an existing VM
String resourceGroupName = windowsVM.resourceGroupName();
PagedList<VirtualMachine> resourceGroupVMs = azure.virtualMachines()
        .listByResourceGroup(resourceGroupName); 

// for each vitual machine in the resource group, log their name and plan
for (VirtualMachine virtualMachine : azure.virtualMachines().listByResourceGroup(resourceGroupName)) {
    System.out.println("VM " + virtualMachine.computerName() + 
        " has plan " + virtualMachine.plan());
}
```

Listen Sie alle virtuellen Computer für ein Abonnement mithilfe von `azure.virtualMachines().list()` auf, und durchlaufen Sie die von `tags()` zurückgegebene Zuordnung, um gekennzeichnete Sammlungen virtueller Computer in Ressourcengruppen zu verwalten.

## <a name="update-a-virtual-machine"></a>Aktualisieren eines virtuellen Computers

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

Aktualisieren Sie die Konfiguration der virtuellen Computer mit `update()...apply()` und denselben Methoden, die Sie zum Konfigurieren der virtuellen Computer bei der Erstellung über `define()...create()` verwendet haben.

## <a name="delete-a-virtual-machine"></a>Löschen eines virtuellen Computers

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a>Erläuterung des Beispiels

Der [Beispielcode](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) erstellt einen virtuellen Windows-Computer mit einem 50-GB-Datenträger. Anschließend wird im Beispiel ein zweiter 10-GB-Datenträger erstellt und an diesen virtuellen Windows-Computer angefügt.
Dann erstellt das Beispiel einen virtuellen Linux-Computer im gleichen virtuellen Netzwerk wie der virtuelle Windows-Computer.

Das Beispiel protokolliert Informationen zu beiden virtuellen Computern und löscht sie vor dem Abschluss.

| Im Beispiel verwendete Klasse | Notizen
|-------|-------|
| [VirtualMachine](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | Abfragen von Eigenschaften und Verwalten des Status virtueller Computer. Wird in Listenform (mit `azure.virtualMachines().list()`) oder nach Name oder ID (mit `azure.virtualMachines().getByResourceGroup()`) abgerufen.
| [VirtualMachineSizeTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | Klasse mit statischen Werten, die den [Optionen für die Größe virtueller Computer](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) entsprechen. Diese werden von der `withSize()`-Methode zum Definieren der dem virtuellen Computer zugeordneten Ressourcen verwendet.
| [Datenträger](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | Erstellen eines Datenträgers mit `withData()` zum Speichern von Daten oder eines Betriebssystemimages mit der entsprechenden `withLinux`- oder `withWindows`-Methode (beim Definieren des Datenträgers). Anfügen von Datenträgern an virtuelle Computer zum Zeitpunkt der Erstellung (`using withNewDataDisk` oder `withExistingDataDisk`) oder nach der Erstellung mit `update()..apply()` für das VirtualMachine-Objekt.
| [DiskSkuTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | Klasse mit statischen Werten zum Definieren eines Datenträgers mit dem Tarif Standard oder Storage [Premium](https://docs.microsoft.com/azure/storage/storage-premium-storage).
| [KnownLinuxVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | Klasse mit einem Satz von Optionen für virtuelle Linux-Computer zur Verwendung mit der `withPopularLinuxImage()`-Methode, wenn Sie einen virtuellen Computer definieren.
| [KnownWindowsVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | Klasse mit einem Satz von Optionen für Windows-VM-Images zur Verwendung mit der `withPopularWindowsImage()`-Methode, wenn Sie einen virtuellen Computer definieren.

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [next-steps](includes/java-next-steps.md)]