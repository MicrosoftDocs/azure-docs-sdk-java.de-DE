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
ms.openlocfilehash: b414f4dc9289958c2562ddc6d41133279f47a45e
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="fc793-103">Azure Virtual Machines-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="fc793-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="fc793-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="fc793-104">Overview</span></span>

<span data-ttu-id="fc793-105">Bedarfsgesteuerte, skalierbare Computeressourcen unter Linux oder Windows</span><span class="sxs-lookup"><span data-stu-id="fc793-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="fc793-106">Informationen zu den ersten Schritten mit virtuellen Azure-Computern finden Sie unter [Erstellen einer Linux-VM mit dem Azure-Portal](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="fc793-106">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="fc793-107">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="fc793-107">Management API</span></span>

<span data-ttu-id="fc793-108">Mit der Verwaltungs-API können Sie virtuelle Windows- und Linux-Computer in Azure über Ihren Code erstellen, konfigurieren und horizontal hochskalieren.</span><span class="sxs-lookup"><span data-stu-id="fc793-108">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="fc793-109">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="fc793-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.2.1</version>
</dependency>
```   


## <a name="example"></a><span data-ttu-id="fc793-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="fc793-110">Example</span></span>

<span data-ttu-id="fc793-111">Erstellen eines neuen virtuellen Linux-Computers in einer neuen Azure-Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="fc793-111">Create a new Linux virtual machine in a new Azure resource group.</span></span>

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
> [<span data-ttu-id="fc793-112">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="fc793-112">Explore the Management APIs</span></span>](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a><span data-ttu-id="fc793-113">Beispiele</span><span class="sxs-lookup"><span data-stu-id="fc793-113">Samples</span></span>

<span data-ttu-id="fc793-114">[Verwalten virtueller Computer][1] </span><span class="sxs-lookup"><span data-stu-id="fc793-114">[Manage virtual machines][1] </span></span>  
<span data-ttu-id="fc793-115">[Verwalten virtueller Netzwerke][6] </span><span class="sxs-lookup"><span data-stu-id="fc793-115">[Manage virtual networks][6] </span></span>  
<span data-ttu-id="fc793-116">[Erstellen eines virtuellen Computers aus einem benutzerdefinierten Image][2] </span><span class="sxs-lookup"><span data-stu-id="fc793-116">[Create a virtual machine from a custom image][2] </span></span>  
<span data-ttu-id="fc793-117">[Paralleles Erstellen von virtuellen Computern in mehreren Regionen][5]  </span><span class="sxs-lookup"><span data-stu-id="fc793-117">[Create virtual machines across regions in parallel][5]  </span></span>  
<span data-ttu-id="fc793-118">[Erstellen einer VM-Skalierungsgruppe mit einem Lastenausgleich][7]</span><span class="sxs-lookup"><span data-stu-id="fc793-118">[Create a virtual machine scale set with a load balancer][7]</span></span>    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

<span data-ttu-id="fc793-119">Sehen Sie sich weitere [Java-Codebeispiele für virtuelle Azure-Computer](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="fc793-119">Explore more [sample Java code for Azure virtual machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) you can use in your apps.</span></span>