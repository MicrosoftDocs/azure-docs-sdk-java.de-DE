---
title: Azure-Netzwerkbibliotheken für Java
description: Referenzdokumentation für die Java-Verwaltungsbibliotheken für Azure-Netzwerke
keywords: Azure, Java, SDK, API, Netzwerke, Lastenausgleich, VNET, Subnetz
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: networking
ms.openlocfilehash: bb74ccd8826df7b627e0b5f4e4ffd2da44b2642d
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893381"
---
# <a name="azure-network-libraries-for-java"></a><span data-ttu-id="81760-104">Azure-Netzwerkbibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="81760-104">Azure Network libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="81760-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="81760-105">Overview</span></span>

<span data-ttu-id="81760-106">Mit [Azure-Netzwerken](/azure/networking/networking-overview) können Sie Azure-Ressourcen verbinden, Datenverkehr filtern und ausgleichen und das Routing verwalten.</span><span class="sxs-lookup"><span data-stu-id="81760-106">Connect Azure resources, filter and balance traffic, and manage routing with [Azure Networking](/azure/networking/networking-overview).</span></span>

<span data-ttu-id="81760-107">Informationen zu den ersten Schritten mit Azure-Netzwerken finden Sie unter [Erstellen Ihres ersten virtuellen Netzwerks](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="81760-107">To get started with Azure Networking, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-api"></a><span data-ttu-id="81760-108">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="81760-108">Management API</span></span>

<span data-ttu-id="81760-109">Erstellen und verwalten Sie mithilfe der Verwaltungs-API [virtuelle Azure-Netzwerke](/azure/virtual-network/virtual-networks-overview), [ExpressRoute](/azure/expressroute/)-Verbindungen und [Anwendungsgateways](/azure/application-gateway/).</span><span class="sxs-lookup"><span data-stu-id="81760-109">Create and manage Azure [virtual networks](/azure/virtual-network/virtual-networks-overview) , [ExpressRoutes](/azure/expressroute/) , and [Application Gateways](/azure/application-gateway/) with the management API.</span></span>

<span data-ttu-id="81760-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="81760-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="81760-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="81760-111">Example</span></span>

<span data-ttu-id="81760-112">Erstellen Sie ein virtuelles Netzwerk mit einem einzelnen Subnetz:</span><span class="sxs-lookup"><span data-stu-id="81760-112">Create a new virtual network with a single subnet.</span></span>

```java
Network virtualNetwork1 = azure.networks().define(vnetName1)
        .withRegion(Region.US_EAST)
        .withExistingResourceGroup("myResourceGroup")
        .withAddressSpace("192.168.0.0/16")
        .defineSubnet("myVirtualNetwork")
            .withAddressPrefix("192.168.2.0/24")
            .attach()
        .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="81760-113">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="81760-113">Explore the Management APIs</span></span>](/java/api/overview/azure/networking/management)

## <a name="samples"></a><span data-ttu-id="81760-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="81760-114">Samples</span></span>

<span data-ttu-id="81760-115">[Verwalten virtueller Netzwerke](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span><span class="sxs-lookup"><span data-stu-id="81760-115">[Manage virtual networks](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span></span>  
<span data-ttu-id="81760-116">[Verwalten von Netzwerkschnittstellen](https://github.com/Azure-Samples/network-java-manage-network-interface) </span><span class="sxs-lookup"><span data-stu-id="81760-116">[Manage network interfaces](https://github.com/Azure-Samples/network-java-manage-network-interface) </span></span>  
<span data-ttu-id="81760-117">[Verwalten von Anwendungsgateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span><span class="sxs-lookup"><span data-stu-id="81760-117">[Manage Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span></span>  
[<span data-ttu-id="81760-118">Verwalten von Lastenausgleichsmodulen mit Internetzugriff</span><span class="sxs-lookup"><span data-stu-id="81760-118">Manage internet facing load balancers</span></span>](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

<span data-ttu-id="81760-119">Sehen Sie sich weitere [Java-Codebeispiele für Azure-Netzwerke](https://azure.microsoft.com/resources/samples/?platform=java&term=network) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="81760-119">Explore more [sample Java code for Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) you can use in your apps.</span></span>
