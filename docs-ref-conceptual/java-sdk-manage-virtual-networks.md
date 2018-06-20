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
ms.openlocfilehash: 3d21cdd890912c1fc58fc65a79ba972b8327edeb
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931086"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a>Erstellen und Verwalten von virtuellen Azure-Netzwerken über Ihre Java-Apps

In [diesem Beispiel](https://github.com/Azure-Samples/network-java-manage-virtual-network) wird ein [virtuelles Netzwerk](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) erstellt, um Ihre Azure-Ressourcen in dem von Ihnen gesteuerten Netzwerksegment zu isolieren.

## <a name="run-the-sample"></a>Ausführen des Beispiels

Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest. Führen Sie anschließend Folgendes aus:

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java) an.

## <a name="authenticate-with-azure"></a>Authentifizierung über Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a>Erstellen einer Netzwerksicherheitsgruppe zum Blockieren von Internetdatenverkehr

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

Mit dieser [Netzwerksicherheitsregel](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) wird sowohl eingehender als auch ausgehender öffentlicher Internetdatenverkehr blockiert. Diese Netzwerksicherheitsgruppe hat erst dann eine Auswirkung, wenn sie auf ein Subnetz im virtuellen Netzwerk angewendet wird.

## <a name="create-a-virtual-network-with-two-subnets"></a>Erstellen eines virtuellen Netzwerks mit zwei Subnetzen

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

Das Back-End-Subnetz verweigert den Internetzugriff gemäß den Regeln, die in der Netzwerksicherheitsgruppe festgelegt sind. Das Front-End-Subnetz verwendet die [Standardregeln](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), die ausgehenden Datenverkehr an das Internet ermöglichen.

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a>Erstellen einer Netzwerksicherheitsgruppe zum Zulassen von eingehendem HTTP-Datenverkehr
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

Diese Netzwerksicherheitsgruppe lässt eingehenden Datenverkehr an Port 80 aus dem öffentlichen Internet zu und blockiert den gesamten ausgehenden Datenverkehr vom Netzwerk an das öffentliche Internet. 

## <a name="update-a-virtual-network"></a>Erstellen eines virtuellen Netzwerks
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

Aktualisieren Sie das Front-End-Subnetz, um mithilfe der im vorherigen Schritt erstellten Netzwerksicherheitsregel eingehenden HTTP-Datenverkehr zuzulassen.

## <a name="create-a-virtual-machine-on-a-subnet"></a>Erstellen eines virtuellen Computers in einem Subnetz
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

Mit `withExistingPrimaryNetwork()` und `withSubnet()` wird der virtuelle Computer zur Verwendung des Front-End-Subnetzes im virtuellen Netzwerk konfiguriert, das im vorherigen Schritt erstellt wurde.

## <a name="list-virtual-networks-in-a-resource-group"></a>Auflisten virtueller Netzwerke in einer Ressourcengruppe
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

Sie können `Network`-Objekte mit der äußeren Abfrage auflisten und untersuchen oder mit der geschachtelten For-Each-Schleife alle untergeordneten Ressourcen für jedes Netzwerk wie in diesem Beispiel gezeigt durchlaufen.

## <a name="delete-a-virtual-network"></a>Löschen eines virtuellen Netzwerks
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

Wenn Sie ein virtuelles Netzwerk entfernen, werden die Subnetze im Netzwerk, aber nicht die auf die Subnetze angewendeten Regeln der Netzwerksicherheitsgruppe gelöscht. Diese Definitionen können wieder auf andere Subnetze angewendet werden.

## <a name="sample-explanation"></a>Erläuterung des Beispiels

In diesem Beispiel wird ein virtuelles Netzwerk mit zwei Subnetzen und einem virtuellen Computer in jedem Subnetz erstellt. Das Back-End-Subnetz ist nicht mit dem öffentlichen Internet verbunden. Das Front-End-Subnetz akzeptiert eingehenden HTTP-Datenverkehr vom Internet. Beide virtuellen Computer im virtuellen Netzwerk kommunizieren über die Netzwerksicherheitsgruppen-Standardregeln miteinander.

| Im Beispiel verwendete Klasse | Hinweise
|-------|-------|
| [Netzwerk](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | Lokale Objektdarstellung des über `azure.networks().define()...create()` erstellten virtuellen Netzwerks. Aktualisieren Sie mit der `update()...apply()`-Fluent-Kette ein vorhandenes virtuelles Netzwerk.
| [Subnetz](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | Erstellen Sie Subnetze im virtuellen Netzwerk, wenn Sie das Netzwerk mit `withSubnet()` definieren oder aktualisieren. Rufen Sie Objektdarstellungen eines Subnetzes über `Network.subnets().get()` oder `Network.subnets().entrySet()` ab. Diese Objekte enthalten Methoden zum Abfragen der Subnetzeigenschaften.
| [NetworkSecurityGroup](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | Wird mit der `azure.networkSecurityGroups().define()...create()`-Fluent-Kette erstellt und dann durch Aktualisieren oder Erstellen von Subnetzen in einem virtuellen Netzwerk auf Subnetze angewendet. 

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [next-steps](includes/java-next-steps.md)]