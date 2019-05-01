---
title: Azure CDN-Bibliotheken für Java
description: Referenzdokumentation für die Java-CDN-Bibliotheken
keywords: Azure, Java, SDK, API, Inhalt, Verteilung, Netzwerk, CDN
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: 88013a1d82d11d97bf99cb5acf0dee4bc8b5704d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592885"
---
# <a name="azure-cdn-libraries-for-java"></a>Azure CDN-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Speichern Sie mit [Azure Content Delivery Network (CDN)](/azure/cdn/cdn-overview) statische Webinhalte an strategisch platzierten Standorten zwischen, um für Benutzer einen maximalen Durchsatz zu ermöglichen

Informationen zu den ersten Schritten mit Azure CDN finden Sie unter [Erste Schritte mit Azure CDN](/azure/cdn/cdn-create-new-endpoint).

## <a name="management-api"></a>Verwaltungs-API

Mit der Verwaltungs-API können Sie CDN-Profile erstellen, Endpunkte definieren und dem CDN Inhalte hinzufügen.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Erstellen Sie ein CDN-Profil, weisen Sie Endpunkte zu, und laden Sie Inhalte ins CDN:

```java
CdnProfile profile = azure.cdnProfiles().define("testCDN")
        .withRegion(Region.US_EAST)
        .withNewResourceGroup()
        .withStandardVerizonSku()
        .withNewEndpoint("webAppHostname1")
        .withNewEndpoint("webAppHostname2")
        .create();

List<String> contentList = new ArrayList<String>();
contentList.add("/client.js");
contentList.add("/media/fabrikam_logo.png");

for (CdnEndpoint endpoint : profile.endpoints().values()) {
    endpoint.loadContent(contentList);
}
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/cdn/management)

## <a name="samples"></a>Beispiele

[Verwalten von CDNs mit Java](https://github.com/Azure-Samples/cdn-java-manage-cdn)

Sehen Sie sich weitere [Java-Codebeispiele für Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) an, die Sie in Ihren Apps verwenden können.