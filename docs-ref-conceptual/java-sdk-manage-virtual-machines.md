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
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a><span data-ttu-id="6e088-103">Verwalten von virtuellen Azure-Computern über Ihre Java-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="6e088-103">Manage Azure virtual machines from your Java applications</span></span>

<span data-ttu-id="6e088-104">In [diesem Beispiel](https://github.com/Azure-Samples/compute-java-manage-vm/) werden zum Erstellen und Verwenden von virtuellen Azure-Computern die [Azure-Verwaltungsbibliotheken für Java](https://github.com/Azure/azure-sdk-for-java) verwendet.</span><span class="sxs-lookup"><span data-stu-id="6e088-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-vm/) uses the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java) to create and work with Azure virtual machines.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="6e088-105">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="6e088-105">Run the sample</span></span>

<span data-ttu-id="6e088-106">Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest.</span><span class="sxs-lookup"><span data-stu-id="6e088-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="6e088-107">Führen Sie anschließend Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="6e088-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

<span data-ttu-id="6e088-108">Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) an.</span><span class="sxs-lookup"><span data-stu-id="6e088-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="6e088-109">Authentifizierung über Azure</span><span class="sxs-lookup"><span data-stu-id="6e088-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a><span data-ttu-id="6e088-110">Erstellen eines virtuellen Windows-Computers</span><span class="sxs-lookup"><span data-stu-id="6e088-110">Create a Windows virtual machine</span></span>

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

<span data-ttu-id="6e088-111">Dieser Code:</span><span class="sxs-lookup"><span data-stu-id="6e088-111">This code:</span></span>   

0. <span data-ttu-id="6e088-112">definiert ein Creatable-Objekt vom Typ `Disk` mit einer Größe von 50 GB und einem zufälligen Namen zur Verwendung mit einem virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="6e088-112">Defines a `Disk` Creatable with a 50GB size and random name for use with a virtual machine.</span></span>
0. <span data-ttu-id="6e088-113">verwendet die Kette `azure.virtualMachines().define()..create()` zum Erstellen des virtuellen Windows Server 2012-Computers.</span><span class="sxs-lookup"><span data-stu-id="6e088-113">Uses the `azure.virtualMachines().define()..create()` chain to create the Windows Server 2012 virtual machine.</span></span> <span data-ttu-id="6e088-114">Die API erstellt das im vorherigen Schritt definierte `Disk`-Element zum gleichen Zeitpunkt wie den virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="6e088-114">The API creates the `Disk` defined in the previous step the same time as the virtual machine.</span></span> <span data-ttu-id="6e088-115">An den virtuellen Computer wird zudem über `withNewDataDisk(10)` ein 10-GB-Datenträger angefügt.</span><span class="sxs-lookup"><span data-stu-id="6e088-115">A 10GB data disk is also attached to the virtual machine through `withNewDataDisk(10)`.</span></span>

<span data-ttu-id="6e088-116">Erfahren Sie mehr darüber, wie Sie mit [Creatable<T>-Objekten](java-sdk-azure-concepts.md#Creatables) lokale Darstellungen von Ressourcen definieren und diese Objekte genau dann erstellen, wenn sie von anderen Azure-Ressourcen benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="6e088-116">Learn more about using [Creatable<T> objects](java-sdk-azure-concepts.md#Creatables) to define local representations of resources and create them just as other Azure resources need them.</span></span>

## <a name="stop-start-and-restart-a-virtual-machine"></a><span data-ttu-id="6e088-117">Beenden, Starten und Neustarten eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="6e088-117">Stop, start, and restart a virtual machine</span></span>

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

<span data-ttu-id="6e088-118">`powerOff()` beendet das Betriebssystem des virtuellen Computers, hebt jedoch die Zuordnung seiner Ressourcen nicht auf.</span><span class="sxs-lookup"><span data-stu-id="6e088-118">`powerOff()` stops the virtual machine operating system but does not deallocate its resources.</span></span>

## <a name="add-a-virtual-machine-to-an-existing-network"></a><span data-ttu-id="6e088-119">Hinzufügen eines virtuellen Computers zu einem vorhandenen Netzwerk</span><span class="sxs-lookup"><span data-stu-id="6e088-119">Add a virtual machine to an existing network</span></span>

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

<span data-ttu-id="6e088-120">Definieren Sie mithilfe von `withPopularLinuxImage` anstelle eines virtuellen Windows-Computers einen virtuellen Linux-Computer.</span><span class="sxs-lookup"><span data-stu-id="6e088-120">Use `withPopularLinuxImage` to define a Linux VM instead of a Windows one.</span></span>


## <a name="list-virtual-machines"></a><span data-ttu-id="6e088-121">Auflisten von virtuellen Computern</span><span class="sxs-lookup"><span data-stu-id="6e088-121">List virtual machines</span></span>

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

<span data-ttu-id="6e088-122">Listen Sie alle virtuellen Computer für ein Abonnement mithilfe von `azure.virtualMachines().list()` auf, und durchlaufen Sie die von `tags()` zurückgegebene Zuordnung, um gekennzeichnete Sammlungen virtueller Computer in Ressourcengruppen zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="6e088-122">List all virtual machines for a subscription using `azure.virtualMachines().list()` and iterate through the Map returned by `tags()` to manage tagged collections of virtual machines across resource groups.</span></span>

## <a name="update-a-virtual-machine"></a><span data-ttu-id="6e088-123">Aktualisieren eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="6e088-123">Update a virtual machine</span></span>

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

<span data-ttu-id="6e088-124">Aktualisieren Sie die Konfiguration der virtuellen Computer mit `update()...apply()` und denselben Methoden, die Sie zum Konfigurieren der virtuellen Computer bei der Erstellung über `define()...create()` verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="6e088-124">Update the virtual machine configuration using `update()...apply()` and the same methods used to configure the virtual machine when created through `define()...create()`.</span></span>

## <a name="delete-a-virtual-machine"></a><span data-ttu-id="6e088-125">Löschen eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="6e088-125">Delete a virtual machine</span></span>

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a><span data-ttu-id="6e088-126">Erläuterung des Beispiels</span><span class="sxs-lookup"><span data-stu-id="6e088-126">Sample explanation</span></span>

<span data-ttu-id="6e088-127">Der [Beispielcode](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) erstellt einen virtuellen Windows-Computer mit einem 50-GB-Datenträger.</span><span class="sxs-lookup"><span data-stu-id="6e088-127">[The sample code](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) creates a Windows virtual machine with a 50GB data disk.</span></span> <span data-ttu-id="6e088-128">Anschließend wird im Beispiel ein zweiter 10-GB-Datenträger erstellt und an diesen virtuellen Windows-Computer angefügt.</span><span class="sxs-lookup"><span data-stu-id="6e088-128">The sample then creates a second 10GB data disk and attaches it to this Windows virtual machine.</span></span>
<span data-ttu-id="6e088-129">Dann erstellt das Beispiel einen virtuellen Linux-Computer im gleichen virtuellen Netzwerk wie der virtuelle Windows-Computer.</span><span class="sxs-lookup"><span data-stu-id="6e088-129">Then the sample creates a Linux virtual machine in the same virtual network as the Windows virtual machine.</span></span>

<span data-ttu-id="6e088-130">Das Beispiel protokolliert Informationen zu beiden virtuellen Computern und löscht sie vor dem Abschluss.</span><span class="sxs-lookup"><span data-stu-id="6e088-130">The sample logs information about both virtual machines and deletes them both before completing.</span></span>

| <span data-ttu-id="6e088-131">Im Beispiel verwendete Klasse</span><span class="sxs-lookup"><span data-stu-id="6e088-131">Class used in sample</span></span> | <span data-ttu-id="6e088-132">Notizen</span><span class="sxs-lookup"><span data-stu-id="6e088-132">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="6e088-133">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="6e088-133">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="6e088-134">Abfragen von Eigenschaften und Verwalten des Status virtueller Computer.</span><span class="sxs-lookup"><span data-stu-id="6e088-134">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="6e088-135">Wird in Listenform (mit `azure.virtualMachines().list()`) oder nach Name oder ID (mit `azure.virtualMachines().getByResourceGroup()`) abgerufen.</span><span class="sxs-lookup"><span data-stu-id="6e088-135">Retrieved in list form  with`azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="6e088-136">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="6e088-136">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="6e088-137">Klasse mit statischen Werten, die den [Optionen für die Größe virtueller Computer](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) entsprechen. Diese werden von der `withSize()`-Methode zum Definieren der dem virtuellen Computer zugeordneten Ressourcen verwendet.</span><span class="sxs-lookup"><span data-stu-id="6e088-137">Class with static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), used by the `withSize()` method to define the resources allocated to the VM.</span></span>
| [<span data-ttu-id="6e088-138">Datenträger</span><span class="sxs-lookup"><span data-stu-id="6e088-138">Disk</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | <span data-ttu-id="6e088-139">Erstellen eines Datenträgers mit `withData()` zum Speichern von Daten oder eines Betriebssystemimages mit der entsprechenden `withLinux`- oder `withWindows`-Methode (beim Definieren des Datenträgers).</span><span class="sxs-lookup"><span data-stu-id="6e088-139">Create a disk to store data using `withData()` or operating system image using the appropriate `withLinux` or `withWindows` method when defining the disk.</span></span> <span data-ttu-id="6e088-140">Anfügen von Datenträgern an virtuelle Computer zum Zeitpunkt der Erstellung (`using withNewDataDisk` oder `withExistingDataDisk`) oder nach der Erstellung mit `update()..apply()` für das VirtualMachine-Objekt.</span><span class="sxs-lookup"><span data-stu-id="6e088-140">Attach disks to virtual machines either at the time of creation (`using withNewDataDisk` or `withExistingDataDisk`) or after creation by `update()..apply()` on the VirtualMachine object.</span></span>
| [<span data-ttu-id="6e088-141">DiskSkuTypes</span><span class="sxs-lookup"><span data-stu-id="6e088-141">DiskSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | <span data-ttu-id="6e088-142">Klasse mit statischen Werten zum Definieren eines Datenträgers mit dem Tarif Standard oder Storage [Premium](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="6e088-142">Class with static values to define a disk with a standard or [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) storage plan.</span></span>
| [<span data-ttu-id="6e088-143">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="6e088-143">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="6e088-144">Klasse mit einem Satz von Optionen für virtuelle Linux-Computer zur Verwendung mit der `withPopularLinuxImage()`-Methode, wenn Sie einen virtuellen Computer definieren.</span><span class="sxs-lookup"><span data-stu-id="6e088-144">Class with a set of Linux virtual machine options for use with the `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="6e088-145">KnownWindowsVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="6e088-145">KnownWindowsVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | <span data-ttu-id="6e088-146">Klasse mit einem Satz von Optionen für Windows-VM-Images zur Verwendung mit der `withPopularWindowsImage()`-Methode, wenn Sie einen virtuellen Computer definieren.</span><span class="sxs-lookup"><span data-stu-id="6e088-146">Class with a set of Windows virtual machine image options for use with the `withPopularWindowsImage()` method when defining a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e088-147">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6e088-147">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]