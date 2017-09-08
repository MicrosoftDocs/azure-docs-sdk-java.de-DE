---
title: "Azure Application Insights-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Verwaltungs-API für Azure Application Insights"
keywords: Azure, Java, SDK, API, AppInsights, Telemetrie, Diagnose, Ablaufverfolgung, Protokolle, Leistung
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appinsights
ms.openlocfilehash: 9f943dc87d9e9b3e015407eea4dfd2900040da37
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-application-insights-libraries-for-java"></a>Azure Application Insights-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Erkennen, selektieren und diagnostizieren Sie mit [Application Insights](/azure/application-insights/app-insights-overview) Probleme in Ihren Web-Apps und Diensten.

Informationen zu den ersten Schritten mit Application Insights finden Sie unter [Erste Schritte mit Application Insights in einem Java-Webprojekt](/azure/application-insights/app-insights-java-get-started).

## <a name="client-library"></a>Clientbibliothek

Fügen Sie Telemetrie hinzu, um mit der Application Insights-Clientbibliothek Ereignisse, Ausnahmen und Benutzermetriken in Ihren Apps nachzuverfolgen.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Erstellen eines neuen Metrikeintrags und Aufzeichnen eines Werts dafür

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/java/api/overview/azure/appinsights/clientlibrary)

## <a name="samples"></a>Beispiele

Sehen Sie sich weitere [Java-Codebeispiele für Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) an, die Sie in Ihren Apps verwenden können.