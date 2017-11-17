---
title: "Azure Traffic Manager-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Verwaltungsbibliotheken für Azure Traffic Manager"
keywords: Azure, Java, SDK, API, Lastenausgleich, Lastverteilung, Netzwerk, Traffic Manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: 9e13f97c6ddb763fb162b3de0c8d09c77eae1ccb
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="04d0f-104">Azure Traffic Manager-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="04d0f-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="04d0f-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="04d0f-105">Overview</span></span>

<span data-ttu-id="04d0f-106">Mit [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) können Sie die Verteilung von Benutzerdatenverkehr für Dienstendpunkte in verschiedenen Datencentern steuern.</span><span class="sxs-lookup"><span data-stu-id="04d0f-106">Control the distribution of user traffic for service endpoints in different datacenters with [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>

<span data-ttu-id="04d0f-107">Informationen zu den ersten Schritten mit Azure Traffic Manager finden Sie unter [Erstellen eines Traffic Manager-Profils](/azure/traffic-manager/traffic-manager-create-profile).</span><span class="sxs-lookup"><span data-stu-id="04d0f-107">To get started with Azure Traffic Manager, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).</span></span>

## <a name="management-api"></a><span data-ttu-id="04d0f-108">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="04d0f-108">Management API</span></span>

<span data-ttu-id="04d0f-109">Erstellen Sie Traffic Manager-Profile, definieren Sie Endpunkte, und ändern Sie die Routingmethode mit der Verwaltungs-API.</span><span class="sxs-lookup"><span data-stu-id="04d0f-109">Create Traffic Manager profiles, define endpoints, and change the routing method with the management API.</span></span> 

<span data-ttu-id="04d0f-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="04d0f-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.3.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="04d0f-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="04d0f-111">Example</span></span>

<span data-ttu-id="04d0f-112">Erstellen eines Traffic Manager-Profils und Zuweisen zu einem Endpunkt</span><span class="sxs-lookup"><span data-stu-id="04d0f-112">Create a Traffic Manager profile and assign a single endpoint.</span></span>

```java
TrafficManagerProfile tmProfile = azure.trafficManagerProfiles().define("testTMProfile")
        .withNewResourceGroup(Region.US_EAST)
        .withLeafDomainLabel("testTMProfile")
        .withPriorityBasedRouting()
        .defineAzureTargetEndpoint("endpoint")
        .toResourceId(webAppId)
        .withRoutingPriority(1)
        .attach()
        .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="04d0f-113">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="04d0f-113">Explore the Management APIs</span></span>](/java/api/overview/azure/trafficmanager/managementapi)

## <a name="samples"></a><span data-ttu-id="04d0f-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="04d0f-114">Samples</span></span>

[<span data-ttu-id="04d0f-115">Ausgleich des Web-App-Datenverkehrs über mehrere Regionen hinweg</span><span class="sxs-lookup"><span data-stu-id="04d0f-115">Balance web app traffic across multiple regions</span></span>](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

<span data-ttu-id="04d0f-116">Sehen Sie sich weitere [Java-Codebeispiele für Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="04d0f-116">Explore more [sample Java code for Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) you can use in your apps.</span></span>
