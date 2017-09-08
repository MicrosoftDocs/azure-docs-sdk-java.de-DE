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
ms.openlocfilehash: 3b9c8f0e3bd5e8feb5a819a7c2583ffbbcf53e38
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Azure Traffic Manager-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Mit [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) können Sie die Verteilung von Benutzerdatenverkehr für Dienstendpunkte in verschiedenen Datencentern steuern.

Informationen zu den ersten Schritten mit Azure Traffic Manager finden Sie unter [Erstellen eines Traffic Manager-Profils](/azure/traffic-manager/traffic-manager-create-profile).

## <a name="management-api"></a>Verwaltungs-API

Erstellen Sie Traffic Manager-Profile, definieren Sie Endpunkte, und ändern Sie die Routingmethode mit der Verwaltungs-API. 

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.1.2</version>
</dependency>
```   

## <a name="example"></a>Beispiel

Erstellen eines Traffic Manager-Profils und Zuweisen zu einem Endpunkt

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
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/trafficmanager/managementapi)

## <a name="samples"></a>Beispiele

[Ausgleich des Web-App-Datenverkehrs über mehrere Regionen hinweg](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

Sehen Sie sich weitere [Java-Codebeispiele für Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) an, die Sie in Ihren Apps verwenden können.
