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
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a><span data-ttu-id="5323f-103">Erstellen virtueller Computer in mehreren Regionen über Ihre Java-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="5323f-103">Create virtual machines across multiple regions from your Java applications</span></span>

<span data-ttu-id="5323f-104">[Dieses Beispiel](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) erstellt virtuelle Computer parallel in verschiedenen Azure-Regionen unter Verwendung der [Azure-Verwaltungsbibliotheken für Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="5323f-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) creates virtual machines in parallel across different Azure regions using the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5323f-105">In dem Beispiel werden insgesamt 48 virtuelle Computer mit Ubuntu 16.04 LTS und der Größe [STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) in vier Regionen erstellt.</span><span class="sxs-lookup"><span data-stu-id="5323f-105">The sample creates a total of 48 VMs running Ubuntu 16.04 LTS of [size STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) across four regions.</span></span> <span data-ttu-id="5323f-106">Die virtuellen Computer werden durch den Beispielcode vor dem Beenden wieder gelöscht.</span><span class="sxs-lookup"><span data-stu-id="5323f-106">The sample code deletes these virtual machines before exiting.</span></span> <span data-ttu-id="5323f-107">[Überprüfen Sie Ihre Diensteinschränkungen und Kontingente](http://docs.microsoft.com/azure/azure-subscription-service-limits), bevor Sie dieses Beispiel mit der Standardanzahl von virtuellen Computern ausführen.</span><span class="sxs-lookup"><span data-stu-id="5323f-107">Make sure to [check your service limits and quota](http://docs.microsoft.com/azure/azure-subscription-service-limits) before running this sample with the default number of VMs.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="5323f-108">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="5323f-108">Run the sample</span></span>

<span data-ttu-id="5323f-109">Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest.</span><span class="sxs-lookup"><span data-stu-id="5323f-109">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="5323f-110">Führen Sie anschließend Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="5323f-110">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

<span data-ttu-id="5323f-111">Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java) an.</span><span class="sxs-lookup"><span data-stu-id="5323f-111">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="5323f-112">Authentifizieren über Azure</span><span class="sxs-lookup"><span data-stu-id="5323f-112">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a><span data-ttu-id="5323f-113">Festlegen der Standorte und der Anzahl für die virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="5323f-113">Set locations and counts for the virtual machines</span></span>

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

<span data-ttu-id="5323f-114">Dieser `Map`-Code wird im weiteren Verlauf des Beispiels zum Festlegen der weltweiten Verteilung der virtuellen Computer verwendet.</span><span class="sxs-lookup"><span data-stu-id="5323f-114">This `Map` is used later in the sample to set the distrubtion of the VMs worldwide.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="5323f-115">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="5323f-115">Create a resource group</span></span> 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

<span data-ttu-id="5323f-116">Die einzelnen Ressourcen in dem Beispiel werden von dieser Ressourcengruppe verwaltet.</span><span class="sxs-lookup"><span data-stu-id="5323f-116">Each resource in the sample is managed by this resource group.</span></span> <span data-ttu-id="5323f-117">Dadurch können Sie später die Ressourcengruppe löschen und die Ressourcen komfortabel bereinigen.</span><span class="sxs-lookup"><span data-stu-id="5323f-117">This makes the resources easy to clean up later by deleting the resource group.</span></span>

## <a name="define-the-virtual-machines"></a><span data-ttu-id="5323f-118">Definieren der virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="5323f-118">Define the virtual machines</span></span>
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

<span data-ttu-id="5323f-119">Die äußere `for`-Schleife durchläuft die einzelnen Regionen und definiert ein Creatable-Objekt für ein virtuelles Netzwerk sowie ein Creatable-Objekt für ein Speicherkonto zur Verwendung durch alle virtuellen Computer in der entsprechenden Region.</span><span class="sxs-lookup"><span data-stu-id="5323f-119">The outer `for` loop above iterates through each region, defining a virtual network Creatable and storage account Creatable for use by all virtual machines in that region.</span></span> <span data-ttu-id="5323f-120">Weitere Informationen zur Verwendung von Creatable-Objekten für die bedarfsbasierte Ressourcenerstellung bei Verwendung der Verwaltungsbibliotheken finden Sie [hier](java-sdk-azure-concepts.md#Creatables).</span><span class="sxs-lookup"><span data-stu-id="5323f-120">Learn more about using [Creatables](java-sdk-azure-concepts.md#Creatables) to create resources only as needed when using the management libraries.</span></span>

<span data-ttu-id="5323f-121">Die innere `for`-Schleife ruft ein Creatable-Objekt für die öffentliche IP-Adresse für den virtuellen Computer ab und definiert dann ein Creatable-Objekt für den virtuellen Computer unter Verwendung der Creatable-Objekte für das virtuelle Netzwerk, das Speicherkonto und die öffentliche IP-Adresse, die zuvor definiert wurden.</span><span class="sxs-lookup"><span data-stu-id="5323f-121">The inner `for` loop gets a public IP address Creatable for the virtual machine and then defines a virtual machine Creatable using the Creatables for the virtual network, storage account, and public IP address defined previously.</span></span>  <span data-ttu-id="5323f-122">Anschließend wird das Creatable-Objekt „VirtualMachine“ der Liste `creatableVirtualMachines` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="5323f-122">This VirtualMachine Creatable is then added to the `creatableVirtualMachines` list.</span></span>

## <a name="create-the-virtual-machines"></a><span data-ttu-id="5323f-123">Erstellen der virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="5323f-123">Create the virtual machines</span></span>

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

<span data-ttu-id="5323f-124">Der Aufruf `azure.virtualMachines().create(creatableVirtualMachines)` erstellt alle in der Liste `creatableVirtualMachines` definierten virtuellen Computer parallel in allen Regionen.</span><span class="sxs-lookup"><span data-stu-id="5323f-124">The `azure.virtualMachines().create(creatableVirtualMachines)` call creates all of the virtual machines defined in the `creatableVirtualMachines` List in parallel across the regions.</span></span>

<span data-ttu-id="5323f-125">Verwenden Sie das zurückgegebene Objekt `CreatedResources<VirtualMachine>`, um auf Ressourcen zuzugreifen, die im Rahmen der Methode `create()` im Azure-Abonnement erstellt wurden (nicht nur den zurückgegebenen Typ `VirtualMachine`).</span><span class="sxs-lookup"><span data-stu-id="5323f-125">Use the returned `CreatedResources<VirtualMachine>` object to access any resources created in the Azure subscription during the the `create()` method, not just the returned `VirtualMachine` type.</span></span> <span data-ttu-id="5323f-126">Wandeln Sie den zurückgegebenen Wert von `createdRelatedResources()` in den korrekten Typ um.</span><span class="sxs-lookup"><span data-stu-id="5323f-126">Cast the returned value from `createdRelatedResources()` to the correct type.</span></span> 

<span data-ttu-id="5323f-127">Weitere Informationen zur Verwendung von `Creatable<T>` und `CreatedResources` finden Sie in unserem [Artikel zu Bibliothekkonzepten](java-sdk-azure-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="5323f-127">Learn more about working with `Creatable<T>` and `CreatedResources` in our [library concepts article](java-sdk-azure-concepts.md).</span></span>

## <a name="delete-the-resource-group"></a><span data-ttu-id="5323f-128">Löschen der Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="5323f-128">Delete the resource group</span></span> 

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

<span data-ttu-id="5323f-129">Dieser Block löscht Ressourcen aus dem Beispiel, bevor das Beispiel beendet wird.</span><span class="sxs-lookup"><span data-stu-id="5323f-129">This block deletes resources created in the sample before the sample exits.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="5323f-130">Erläuterung des Beispiels</span><span class="sxs-lookup"><span data-stu-id="5323f-130">Sample explanation</span></span>

<span data-ttu-id="5323f-131">Sehen Sie sich den vollständigen Beispielcode auf [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) an.</span><span class="sxs-lookup"><span data-stu-id="5323f-131">View the complete sample code on [Github](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span></span>

<span data-ttu-id="5323f-132">Das Beispiel verwendet Objekte vom Typ `Creatable`, um ein virtuelles Netzwerk und ein Speicherkonto für die einzelnen Hostregionen der virtuellen Computer zu definieren.</span><span class="sxs-lookup"><span data-stu-id="5323f-132">The sample uses `Creatable` objects to define a virtual network and storage account for each region hosting the virtual machines.</span></span> <span data-ttu-id="5323f-133">Danach werden Objekte vom Typ `Creatable` für die öffentliche IP-Adresse für die einzelnen virtuellen Computer definiert.</span><span class="sxs-lookup"><span data-stu-id="5323f-133">`Creatable` objects are then defined for the public IP address for each virtual machine.</span></span> <span data-ttu-id="5323f-134">Das Beispiel definiert die virtuellen Computer unter Verwendung dieser Objekte vom Typ `Creatable` und fügt die VM-Definition der Liste `virtualMachineCreatable` hinzu.</span><span class="sxs-lookup"><span data-stu-id="5323f-134">The sample defines the virtual machines using these `Creatable` objects, and sample adds the VM definition to the `virtualMachineCreatable` list.</span></span>

<span data-ttu-id="5323f-135">Nachdem die einzelnen VM-Definitionen der Liste hinzugefügt wurden, erstellt `azure.virtualMachines().create(creatableVirtualMachines)` die einzelnen virtuellen Computer parallel in Azure.</span><span class="sxs-lookup"><span data-stu-id="5323f-135">After the code adds every virtual machine definition to the list, `azure.virtualMachines().create(creatableVirtualMachines)` creates each virtual machine in parallel in Azure.</span></span>

<span data-ttu-id="5323f-136">Danach ruft der Beispielcode die IP-Adressen für alle erstellten virtuellen Computer aus dem zurückgegebenen CreatedResources-Objekt ab, um einen [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) für die Verteilung der Last auf die virtuellen Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5323f-136">The sample code then gets the IP addresses for all of the created virtual machines from the returned CreatedResources object to create a [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) to distribute load across the virtual machines.</span></span> 

<span data-ttu-id="5323f-137">Der Block `finally` löscht die Ressourcen aus Ihrem Azure-Abonnement (auch im Falle eines Fehlers).</span><span class="sxs-lookup"><span data-stu-id="5323f-137">The `finally` block deletes the resources from your Azure subscription even in the case of an error.</span></span>

| <span data-ttu-id="5323f-138">Im Beispiel verwendete Klasse</span><span class="sxs-lookup"><span data-stu-id="5323f-138">Class used in sample</span></span> | <span data-ttu-id="5323f-139">Hinweise</span><span class="sxs-lookup"><span data-stu-id="5323f-139">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="5323f-140">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="5323f-140">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="5323f-141">Dient zum Abfragen der Eigenschaften sowie zum Verwalten des Zustands virtueller Computer.</span><span class="sxs-lookup"><span data-stu-id="5323f-141">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="5323f-142">Wird in Listenform (`azure.virtualMachines().list()`) oder nach Name oder ID (`azure.virtualMachines().getByResourceGroup()`) abgerufen.</span><span class="sxs-lookup"><span data-stu-id="5323f-142">Retrieved in list form from `azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="5323f-143">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="5323f-143">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="5323f-144">Statische Werte, die [Größenoptionen für virtuelle Computer](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) entsprechen und beim Definieren eines virtuellen Computers als Parameter für `withSize()` angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="5323f-144">Static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) for use as a parameter to `withSize()` when defining a virtual machine.</span></span>
| [<span data-ttu-id="5323f-145">PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5323f-145">PublicIpAddress</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | <span data-ttu-id="5323f-146">Wird für die einzelnen virtuellen Computer über `azure.publicIpAddresses().define()` definiert, aber nicht sofort erstellt.</span><span class="sxs-lookup"><span data-stu-id="5323f-146">Defined, but not immediately created, for each virtual machine through `azure.publicIpAddresses().define()`.</span></span> <span data-ttu-id="5323f-147">Speichern Sie den Schlüssel für die einzelnen Objekte vom Typ `Creatable`, und rufen Sie sie später über `createdRelatedResource()` ab.</span><span class="sxs-lookup"><span data-stu-id="5323f-147">Store the key for each `Creatable` and retrieve later through `createdRelatedResource()`</span></span>
| [<span data-ttu-id="5323f-148">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="5323f-148">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="5323f-149">Satz von Optionen für virtuelle Linux-Computer, die beim Definieren eines virtuellen Computers als Parameter für die Methode `withPopularLinuxImage()` angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="5323f-149">Set of Linux virtual machine options used as a parameter to `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="5323f-150">Network</span><span class="sxs-lookup"><span data-stu-id="5323f-150">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="5323f-151">Das Beispiel definiert ein virtuelles Netzwerk für die einzelnen Regionen über `azure.networks().define()`.</span><span class="sxs-lookup"><span data-stu-id="5323f-151">The sample defines one virtual network for each region through  `azure.networks().define()` .</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5323f-152">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="5323f-152">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]