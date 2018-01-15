---
title: "Azure-Netzwerkbibliotheken für Java"
description: "Referenzdokumentation für die Java-Verwaltungsbibliotheken für Azure-Netzwerke"
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
ms.openlocfilehash: 6eed6f45ee239db1286e94f210341febb189378d
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2017
---
# <a name="azure-network-libraries-for-java"></a>Azure-Netzwerkbibliotheken für Java

## <a name="overview"></a>Übersicht

Mit [Azure-Netzwerken](/azure/networking/networking-overview) können Sie Azure-Ressourcen verbinden, Datenverkehr filtern und ausgleichen und das Routing verwalten.

Informationen zu den ersten Schritten mit Azure-Netzwerken finden Sie unter [Erstellen Ihres ersten virtuellen Netzwerks](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-api"></a>Verwaltungs-API

Erstellen und verwalten Sie mithilfe der Verwaltungs-API [virtuelle Azure-Netzwerke](/azure/virtual-network/virtual-networks-overview), [ExpressRoute](/azure/expressroute/)-Verbindungen und [Anwendungsgateways](/azure/application-gateway/).

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Erstellen Sie ein virtuelles Netzwerk mit einem einzelnen Subnetz:

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
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/networking/managementapi)

## <a name="samples"></a>Beispiele

[Verwalten virtueller Netzwerke](https://github.com/Azure-Samples/network-java-manage-virtual-network)   
[Verwalten von Netzwerkschnittstellen](https://github.com/Azure-Samples/network-java-manage-network-interface)   
[Verwalten von Anwendungsgateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways)   
[Verwalten von Lastenausgleichsmodulen mit Internetzugriff](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

Sehen Sie sich weitere [Java-Codebeispiele für Azure-Netzwerke](https://azure.microsoft.com/resources/samples/?platform=java&term=network) an, die Sie in Ihren Apps verwenden können.