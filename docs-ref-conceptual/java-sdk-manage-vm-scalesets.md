---
title: Verwalten von VM-Skalierungsgruppen mit Java | Microsoft-Dokumentation
description: Beispielcode zum Verwalten von Azure-VM-Skalierungsgruppen mithilfe des Azure SDKs für Java
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 4653726b387369c18942b6c11392f15b9f0351f3
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893491"
---
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a>Verwalten von Azure-VM-Skalierungsgruppen über Ihre Java-Anwendungen

[Dieses Beispiel](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) erstellt eine [VM-Skalierungsgruppe](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) unter Verwendung der [Java-Verwaltungsbibliotheken](https://github.com/Azure/azure-sdk-for-java). 

## <a name="run-the-sample"></a>Ausführen des Beispiels

Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest. Führen Sie anschließend Folgendes aus:

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) an.

## <a name="authenticate-with-azure"></a>Authentifizieren über Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a>Erstellen eines virtuellen Netzwerks für die Skalierungsgruppe

```java
Network network = azure.networks().define(vnetName)
                    .withRegion(region)
                    .withNewResourceGroup(rgName)
                    .withAddressSpace("172.16.0.0/16")
                    .defineSubnet("Front-end")
                    .withAddressPrefix("172.16.1.0/24")
                    .attach()
                    .create();
```

Richten Sie vor dem Erstellen der Skalierungsgruppendefinition zunächst ein virtuelles Netzwerk und einen Lastenausgleich ein. Die Skalierungsgruppe verwendet diese Ressourcen bei der Erstkonfiguration.

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a>Erstellen eines Lastenausgleichs zum Verteilen der Last auf die Skalierungsgruppe

```java
LoadBalancer loadBalancer1 = azure.loadBalancers().define(loadBalancerName1)
                    .withRegion(region)
                    .withExistingResourceGroup(rgName)
                    // assign a public IP address to the load balancer
                    .definePublicFrontend(frontendName)
                        .withExistingPublicIPAddress(publicIPAddress)
                        .attach()
                    // Add two backend address pools
                    .defineBackend(backendPoolName1)
                        .attach()
                    .defineBackend(backendPoolName2)
                        .attach()
                    // Add two health probes on 80 and 443
                    .defineHttpProbe(httpProbe)
                        .withRequestPath("/")
                        .withPort(80)
                        .attach()
                    .defineHttpProbe(httpsProbe)
                        .withRequestPath("/")
                        .withPort(443)
                        .attach()

                    // balance HTTP and HTTPs traffic
                    .defineLoadBalancingRule(httpLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(80)
                        .withProbe(httpProbe)
                        .withBackend(backendPoolName1)
                        .attach()
                    .defineLoadBalancingRule(httpsLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(443)
                        .withProbe(httpsProbe)
                        .withBackend(backendPoolName2)
                        .attach()

                    // Add NAT definitions to enable SSH and telnet to the VMs 
                    .defineInboundNatPool(natPool50XXto22)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(5000, 5099)
                        .withBackendPort(22)
                        .attach()
                    .defineInboundNatPool(natPool60XXto23)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(6000, 6099)
                        .withBackendPort(23)
                        .attach()
                    .create();
```

 Der Lastenausgleich definiert zwei Back-End-Netzwerkadresspools: einen für den Lastenausgleich über HTTP (`backendPoolName1`) und einen für den Lastenausgleich über HTTPS (`backendPoolName2`).  Die Methoden vom Typ `defineHttpProbe()` richten [Integritätstest-Endpunkte](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) für die Lastenausgleichsmodule ein. NAT-Regeln machen die Ports 22 und 23 für die virtuellen Computer der Skalierungsgruppe verfügbar, um telnet- und SSH-Zugriff zu ermöglichen.

## <a name="create-a-scale-set"></a>Erstellen einer Skalierungsgruppe
 
```java
 // Create a virtual machine scale set with three virtual machines
 // And, install Apache Web servers on them
VirtualMachineScaleSet virtualMachineScaleSet = azure.virtualMachineScaleSets()
       .define(vmssName)
                .withRegion(region)
                .withExistingResourceGroup(rgName)
                .withSku(VirtualMachineScaleSetSkuTypes.STANDARD_D3_V2)
                .withExistingPrimaryNetworkSubnet(network, "Front-end")
                .withExistingPrimaryInternetFacingLoadBalancer(loadBalancer1)
                .withPrimaryInternetFacingLoadBalancerBackends(backendPoolName1, backendPoolName2)
                .withPrimaryInternetFacingLoadBalancerInboundNatPools(natPool50XXto22, natPool60XXto23)
                .withoutPrimaryInternalLoadBalancer()
                .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                .withRootUsername(userName)
                .withSsh(sshKey)
                .withNewDataDisk(100)
                .withNewDataDisk(100, 1, CachingTypes.READ_WRITE)
                .withNewDataDisk(100, 2, 
                     CachingTypes.READ_WRITE, StorageAccountTypes.STANDARD_LRS)
                .withCapacity(3)
                // Use a VM extension to install Apache Web servers
                .defineNewExtension("CustomScriptForLinux")
                    .withPublisher("Microsoft.OSTCExtensions")
                    .withType("CustomScriptForLinux")
                    .withVersion("1.4")
                    .withMinorVersionAutoUpgrade()
                    .withPublicSetting("fileUris", fileUris)
                    .withPublicSetting("commandToExecute", installCommand)
                    .attach()
                .create();
```

Verwenden Sie die Definition des virtuellen Netzwerks und die Lastenausgleichsdefinitionen aus dem vorherigen Schritt, um eine Skalierungsgruppe mit drei Linux-Instanzen (`withCapacity(3)`) und jeweils drei 100-GB-Datenträgern zu erstellen. Die Methode `defineNewExtension()` installiert den Apache-Webserver nacheinander auf den einzelnen virtuellen Computern.

## <a name="list-virtual-machine-scale-set-network-interfaces"></a>Auflisten der Netzwerkschnittstellen der VM-Skalierungsgruppe

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a>Abrufen von SSH-Verbindungszeichenfolgen für die einzelnen virtuellen Computer der Skalierungsgruppe

```java
for (VirtualMachineScaleSetVM instance : virtualMachineScaleSet.virtualMachines().list()) {
    System.out.println("Scale set virtual machine instance #" + instance.instanceId());
    System.out.println(instance.id());
    PagedList<VirtualMachineScaleSetNetworkInterface> networkInterfaces = 
         instance.listNetworkInterfaces();
    // Pick the first NIC on the instance and use its primary IP address
    VirtualMachineScaleSetNetworkInterface networkInterface = networkInterfaces.get(0);
    for (VirtualMachineScaleSetNicIPConfiguration ipConfig : networkInterface.ipConfigurations().values()) {
        if (ipConfig.isPrimary()) {
            List<LoadBalancerInboundNatRule> natRules = ipConfig.listAssociatedLoadBalancerInboundNatRules();
            for (LoadBalancerInboundNatRule natRule : natRules) {
                // find rule matching the inbound SSH port on the backend for the IP address
                // and return the SSH connection string to that port on the load balancer
                if (natRule.backendPort() == 22) {
                    System.out.println("SSH connection string: " + userName + 
                        "@" + publicIPAddress.fqdn() + ":" + natRule.frontendPort());
                break;
                }
            }
            break;
        }
    }
}
```

Durch den zuvor erstellten NAT-Pool wurden die SSH- und telnet-Ports (22 bzw. 23) auf den virtuellen Computern Lastenausgleichsports zugeordnet. Dieser Code erstellt die SSH-Verbindungszeichenfolge für die einzelnen virtuellen Computer.

## <a name="stop-the-virtual-machine-scale-set"></a>Beenden der VM-Skalierungsgruppe

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

Von beendeten virtuellen Computer werden weiterhin reservierte Ressourcen beansprucht. Verwenden Sie `deallocate()`, um das Betriebssystem auf den virtuellen Computern zu beenden und deren Computeressourcen freizugeben.

## <a name="deallocate-the-virtual-machine-scale-set"></a>Aufheben der Zuordnung der VM-Skalierungsgruppe

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

„Deallocate()“ fährt das Betriebssystem auf den virtuellen Computern herunter und gibt die von den Skalierungsgruppeninstanzen verwendeten Compute- und Netzwerkressourcen (beispielsweise IP-Adressen) frei. Für an die virtuellen Computer angefügte Datenträger fallen weiterhin Speichergebühren an (auch für den Betriebssystemdatenträger).

## <a name="start-a-virtual-machine-scale-set"></a>Starten einer VM-Skalierungsgruppe

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a>Aktualisieren der Anzahl von VM-Instanzen in der Skalierungsgruppe
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

Skalieren Sie die Anzahl virtueller Computer in der Skalierungsgruppe mit `withCapacity()` und die Kapazität der einzelnen virtuellen Computer mit `withSku()`.

## <a name="sample-explanation"></a>Erläuterung des Beispiels

Der [Beispielcode](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) erstellt zunächst ein virtuelles Netzwerk, über das die Skalierungsgruppe kommunizieren kann, und einen Lastenausgleich, um den Datenverkehr auf die virtuellen Computer zu verteilen. Die Methode `azure.virtualMachineScaleSets().define()...create()` erstellt die Skalierungsgruppe mit drei Linux-Instanzen, die den Apache-Webserver ausführen.    
   
| Im Beispiel verwendete Klasse | Notizen
|-------|-------|
| [VirtualMachineScaleSet](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | Dient zum Abfragen, Starten, Beenden, Aktualisieren und Löschen aller virtuellen Computer in der Skalierungsgruppe.
| [VirtualMachineScaleSetVM](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | Wird aus `virtualMachineScaleSet.virtualMachines().get()` oder `list()` abgerufen und ermöglicht das Abfragen, Starten, Beenden, Konfigurieren und Löschen virtueller Computer in der Skalierungsgruppe.
| [VirtualMachineScaleSetNetworkInterface](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | Von `virtualMachineScaleSet.listNetworkInterfaces()` zurückgegebene, schreibgeschützte Darstellung einer Netzwerkschnittstelle eines virtuellen Computers in einer Skalierungsgruppe.
| [VirtualMachineScaleSetSkuTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | Klasse von statischen Feldern zum Festlegen des [VM-Skalierungsgruppentarifs](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/), der die Menge an Ressourcen definiert, die Skalierungsgruppenmitglieder beanspruchen können.
| [VirtualMachineScaleSetNicIpConfiguration](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | Dient zum Abfragen der IP-Konfiguration, die einer Netzwerkschnittstelle eines virtuellen Computers in einer Skalierungsgruppe zugeordnet ist.

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [next-steps](includes/java-next-steps.md)]