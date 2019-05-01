---
title: Verwalten von virtuellen Azure-Netzwerken mit Java | Microsoft-Dokumentation
description: Beispielcode zum Verwalten von virtuellen Azure-Netzwerken in Ihrem Java-Code
author: rloutlaw
manager: douge
ms.assetid: 92736911-3df6-46e7-b751-25bb36bf89b9
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 6989c5184d09ac011cb39eb21ad8d96db3f0c107
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592555"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a><span data-ttu-id="647f0-103">Erstellen und Verwalten von virtuellen Azure-Netzwerken über Ihre Java-Apps</span><span class="sxs-lookup"><span data-stu-id="647f0-103">Create and manage Azure virtual networks from your Java apps</span></span>

<span data-ttu-id="647f0-104">In [diesem Beispiel](https://github.com/Azure-Samples/network-java-manage-virtual-network) wird ein [virtuelles Netzwerk](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) erstellt, um Ihre Azure-Ressourcen in dem von Ihnen gesteuerten Netzwerksegment zu isolieren.</span><span class="sxs-lookup"><span data-stu-id="647f0-104">[This sample](https://github.com/Azure-Samples/network-java-manage-virtual-network) creates a [virtual network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) to isolate your Azure resources on network segment you control.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="647f0-105">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="647f0-105">Run the sample</span></span>

<span data-ttu-id="647f0-106">Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest.</span><span class="sxs-lookup"><span data-stu-id="647f0-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="647f0-107">Führen Sie anschließend Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="647f0-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

<span data-ttu-id="647f0-108">Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java) an.</span><span class="sxs-lookup"><span data-stu-id="647f0-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="647f0-109">Authentifizieren über Azure</span><span class="sxs-lookup"><span data-stu-id="647f0-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a><span data-ttu-id="647f0-110">Erstellen einer Netzwerksicherheitsgruppe zum Blockieren von Internetdatenverkehr</span><span class="sxs-lookup"><span data-stu-id="647f0-110">Create a network security group to block Internet traffic</span></span>

```java
// this NSG definition block traffic to and from the public Internet
NetworkSecurityGroup backEndSubnetNsg = azure.networkSecurityGroups()
              .define(vnet1BackEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .defineRule("DenyInternetInComing")
                        .denyInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="647f0-111">Mit dieser [Netzwerksicherheitsregel](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) wird sowohl eingehender als auch ausgehender öffentlicher Internetdatenverkehr blockiert.</span><span class="sxs-lookup"><span data-stu-id="647f0-111">This [network security rule](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) blocks both inbound and outbound public Internet traffic.</span></span> <span data-ttu-id="647f0-112">Diese Netzwerksicherheitsgruppe hat erst dann eine Auswirkung, wenn sie auf ein Subnetz im virtuellen Netzwerk angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="647f0-112">This network security group will not have an effect until applied to a subnet in your virtual network.</span></span>

## <a name="create-a-virtual-network-with-two-subnets"></a><span data-ttu-id="647f0-113">Erstellen eines virtuellen Netzwerks mit zwei Subnetzen</span><span class="sxs-lookup"><span data-stu-id="647f0-113">Create a virtual network with two subnets</span></span>

```java
// create the a virtual network with two subnets
// assign the backend subnet a rule blocking public internet traffic
Network virtualNetwork1 = azure.networks().define(vnetName1)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withAddressSpace("192.168.0.0/16")
                    .withSubnet(vnet1FrontEndSubnetName, "192.168.1.0/24")
                    .defineSubnet(vnet1BackEndSubnetName)
                        .withAddressPrefix("192.168.2.0/24")
                        .withExistingNetworkSecurityGroup(backEndSubnetNsg)
                        .attach()
                    .create();
```

<span data-ttu-id="647f0-114">Das Back-End-Subnetz verweigert den Internetzugriff gemäß den Regeln, die in der Netzwerksicherheitsgruppe festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="647f0-114">The backend subnet denies Internet access usingfollowing the rules set in the network security group.</span></span> <span data-ttu-id="647f0-115">Das Front-End-Subnetz verwendet die [Standardregeln](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), die ausgehenden Datenverkehr an das Internet ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="647f0-115">The front end subnet uses the [default rules](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) which allow outbound traffic to the Internet.</span></span>

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a><span data-ttu-id="647f0-116">Erstellen einer Netzwerksicherheitsgruppe zum Zulassen von eingehendem HTTP-Datenverkehr</span><span class="sxs-lookup"><span data-stu-id="647f0-116">Create a network security group to allow inbound HTTP traffic</span></span>
```java
// create a rule that allows inbound HTTP and blocks outbound Internet traffic
NetworkSecurityGroup frontEndSubnetNsg = azure.networkSecurityGroups()
               .define(vnet1FrontEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .defineRule("AllowHttpInComing")
                        .allowInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toPort(80)
                        .withProtocol(SecurityRuleProtocol.TCP)
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="647f0-117">Diese Netzwerksicherheitsgruppe lässt eingehenden Datenverkehr an Port 80 aus dem öffentlichen Internet zu und blockiert den gesamten ausgehenden Datenverkehr vom Netzwerk an das öffentliche Internet.</span><span class="sxs-lookup"><span data-stu-id="647f0-117">This network security rule opens up inbound traffic on port 80 from the public Internet, and blocks all outbound traffic from inside the network to the public Internet.</span></span> 

## <a name="update-a-virtual-network"></a><span data-ttu-id="647f0-118">Erstellen eines virtuellen Netzwerks</span><span class="sxs-lookup"><span data-stu-id="647f0-118">Update a virtual network</span></span>
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

<span data-ttu-id="647f0-119">Aktualisieren Sie das Front-End-Subnetz, um mithilfe der im vorherigen Schritt erstellten Netzwerksicherheitsregel eingehenden HTTP-Datenverkehr zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="647f0-119">Update the front end subnet to allow inbound HTTP traffic using the network security rule created in the previous step.</span></span>

## <a name="create-a-virtual-machine-on-a-subnet"></a><span data-ttu-id="647f0-120">Erstellen eines virtuellen Computers in einem Subnetz</span><span class="sxs-lookup"><span data-stu-id="647f0-120">Create a virtual machine on a subnet</span></span>
```java
// attach the new VM to the front end subnet on the virtual network
VirtualMachine frontEndVM = azure.virtualMachines().define(frontEndVmName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withExistingPrimaryNetwork(virtualNetwork1) 
                    .withSubnet(vnet1FrontEndSubnetName)
                    .withPrimaryPrivateIpAddressDynamic()
                    .withNewPrimaryPublicIpAddress(publicIpAddressLeafDnsForFrontEndVm)
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();
```

<span data-ttu-id="647f0-121">Mit `withExistingPrimaryNetwork()` und `withSubnet()` wird der virtuelle Computer zur Verwendung des Front-End-Subnetzes im virtuellen Netzwerk konfiguriert, das im vorherigen Schritt erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="647f0-121">`withExistingPrimaryNetwork()` and `withSubnet()` configure the virtual machine to use the front-end subnet on the virtual network created in the previous steps.</span></span>

## <a name="list-virtual-networks-in-a-resource-group"></a><span data-ttu-id="647f0-122">Auflisten virtueller Netzwerke in einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="647f0-122">List virtual networks in a resource group</span></span>
```java
// iterate over every virtual network in the resource group 
for (Network virtualNetwork : azure.networks().listByResourceGroup(rgName)) {
    // for each subnet on the virtual network, log the network address prefix 
    for (Map.Entry<String, Subnet> entry : virtualNetwork.subnets().entrySet()) {
        String subnetName = entry.getKey();
        Subnet subnet = entry.getValue();
        System.out.println("Address prefix for subnet " + subnetName + 
             " is " + subnet.addressPrefix());
    }
}
```       

<span data-ttu-id="647f0-123">Sie können `Network`-Objekte mit der äußeren Abfrage auflisten und untersuchen oder mit der geschachtelten For-Each-Schleife alle untergeordneten Ressourcen für jedes Netzwerk wie in diesem Beispiel gezeigt durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="647f0-123">You can list and inspect `Network` object using the outer collection or iterate through each child resource for each network using the nested for-each loop as seen in this example.</span></span>

## <a name="delete-a-virtual-network"></a><span data-ttu-id="647f0-124">Löschen eines virtuellen Netzwerks</span><span class="sxs-lookup"><span data-stu-id="647f0-124">Delete a virtual network</span></span>
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

<span data-ttu-id="647f0-125">Wenn Sie ein virtuelles Netzwerk entfernen, werden die Subnetze im Netzwerk, aber nicht die auf die Subnetze angewendeten Regeln der Netzwerksicherheitsgruppe gelöscht.</span><span class="sxs-lookup"><span data-stu-id="647f0-125">Removing a virtual network deletes the subnets on the network but does not delete the network security group rules applied to the subnets.</span></span> <span data-ttu-id="647f0-126">Diese Definitionen können wieder auf andere Subnetze angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="647f0-126">Those definitions can be reapplied to other subnets.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="647f0-127">Erläuterung des Beispiels</span><span class="sxs-lookup"><span data-stu-id="647f0-127">Sample explanation</span></span>

<span data-ttu-id="647f0-128">In diesem Beispiel wird ein virtuelles Netzwerk mit zwei Subnetzen und einem virtuellen Computer in jedem Subnetz erstellt.</span><span class="sxs-lookup"><span data-stu-id="647f0-128">This sample creates a virtual network with two subnets and with one virtual machine on each subnet.</span></span> <span data-ttu-id="647f0-129">Das Back-End-Subnetz ist nicht mit dem öffentlichen Internet verbunden.</span><span class="sxs-lookup"><span data-stu-id="647f0-129">The back subnet is cut off from the public Internet.</span></span> <span data-ttu-id="647f0-130">Das Front-End-Subnetz akzeptiert eingehenden HTTP-Datenverkehr vom Internet.</span><span class="sxs-lookup"><span data-stu-id="647f0-130">The front-facing subnet accepts inbound HTTP traffic from the Internet.</span></span> <span data-ttu-id="647f0-131">Beide virtuellen Computer im virtuellen Netzwerk kommunizieren über die Netzwerksicherheitsgruppen-Standardregeln miteinander.</span><span class="sxs-lookup"><span data-stu-id="647f0-131">Both virtual machines in the virtual network communicate with each other through the default network security group rules.</span></span>

| <span data-ttu-id="647f0-132">Im Beispiel verwendete Klasse</span><span class="sxs-lookup"><span data-stu-id="647f0-132">Class used in sample</span></span> | <span data-ttu-id="647f0-133">Notizen</span><span class="sxs-lookup"><span data-stu-id="647f0-133">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="647f0-134">Netzwerk</span><span class="sxs-lookup"><span data-stu-id="647f0-134">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="647f0-135">Lokale Objektdarstellung des über `azure.networks().define()...create()` erstellten virtuellen Netzwerks.</span><span class="sxs-lookup"><span data-stu-id="647f0-135">Local object representation of the virtual network created from `azure.networks().define()...create()` .</span></span> <span data-ttu-id="647f0-136">Aktualisieren Sie mit der `update()...apply()`-Fluent-Kette ein vorhandenes virtuelles Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="647f0-136">Use the `update()...apply()` fluent chain to update an existing virtual network.</span></span>
| [<span data-ttu-id="647f0-137">Subnetz</span><span class="sxs-lookup"><span data-stu-id="647f0-137">Subnet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | <span data-ttu-id="647f0-138">Erstellen Sie Subnetze im virtuellen Netzwerk, wenn Sie das Netzwerk mit `withSubnet()` definieren oder aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="647f0-138">Create subnets on the virtual network when defining or updating the network using `withSubnet()`.</span></span> <span data-ttu-id="647f0-139">Rufen Sie Objektdarstellungen eines Subnetzes über `Network.subnets().get()` oder `Network.subnets().entrySet()` ab.</span><span class="sxs-lookup"><span data-stu-id="647f0-139">Get object representations of a subnet from `Network.subnets().get()` or `Network.subnets().entrySet()`.</span></span> <span data-ttu-id="647f0-140">Diese Objekte enthalten Methoden zum Abfragen der Subnetzeigenschaften.</span><span class="sxs-lookup"><span data-stu-id="647f0-140">These objects have methods to query subnet properties.</span></span>
| [<span data-ttu-id="647f0-141">NetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="647f0-141">NetworkSecurityGroup</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | <span data-ttu-id="647f0-142">Wird mit der `azure.networkSecurityGroups().define()...create()`-Fluent-Kette erstellt und dann durch Aktualisieren oder Erstellen von Subnetzen in einem virtuellen Netzwerk auf Subnetze angewendet.</span><span class="sxs-lookup"><span data-stu-id="647f0-142">Created using the `azure.networkSecurityGroups().define()...create()` fluent chain and then applied to subnets through the updating or creating subnets in a virtual network.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="647f0-143">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="647f0-143">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]