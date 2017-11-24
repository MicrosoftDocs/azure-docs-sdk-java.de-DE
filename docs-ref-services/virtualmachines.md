---
title: "Azure Virtual Machines-Bibliotheken für Java"
description: 
keywords: Azure, Java, SDK, API, Compute, Virtual Machines
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: f9a816d5787e41a4ee4643b1bc66bf21192ea298
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2017
---
# <a name="azure-virtual-machine-libraries"></a>Azure Virtual Machines-Bibliotheken

## <a name="overview"></a>Übersicht

Bedarfsgesteuerte, skalierbare Computeressourcen unter Linux oder Windows

Informationen zu den ersten Schritten mit virtuellen Azure-Computern finden Sie unter [Erstellen einer Linux-VM mit dem Azure-Portal](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>Verwaltungs-API

Mit der Verwaltungs-API können Sie virtuelle Windows- und Linux-Computer in Azure über Ihren Code erstellen, konfigurieren und horizontal hochskalieren.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.3.0</version>
</dependency>
```   


## <a name="example"></a>Beispiel

Erstellen eines neuen virtuellen Linux-Computers in einer neuen Azure-Ressourcengruppe

```java
VirtualMachine newLinuxVm = azure.virtualMachines().define(linuxVmName)
            .withRegion(Region.US_EAST)
            .withNewResourceGroup("myResourceGroup")
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
            .withRootUsername(userName)
            .withSshKey(key)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a>Beispiele

[Verwalten virtueller Computer][1]   
[Verwalten virtueller Netzwerke][6]   
[Erstellen eines virtuellen Computers aus einem benutzerdefinierten Image][2]   
[Paralleles Erstellen von virtuellen Computern in mehreren Regionen][5]    
[Erstellen einer VM-Skalierungsgruppe mit einem Lastenausgleich][7]    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

Sehen Sie sich weitere [Java-Codebeispiele für virtuelle Azure-Computer](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) an, die Sie in Ihren Apps verwenden können.