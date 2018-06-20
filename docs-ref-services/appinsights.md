---
title: Azure Application Insights-Bibliotheken für Java
description: Referenzdokumentation für die Java-Verwaltungs-API für Azure Application Insights
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
ms.openlocfilehash: d881ff66ad806e13f7d2cbafff6ce85c23240304
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823763"
---
# <a name="azure-application-insights-libraries-for-java"></a><span data-ttu-id="ec9fd-104">Azure Application Insights-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="ec9fd-104">Azure Application Insights libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="ec9fd-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="ec9fd-105">Overview</span></span>

<span data-ttu-id="ec9fd-106">Erkennen, selektieren und diagnostizieren Sie mit [Application Insights](/azure/application-insights/app-insights-overview) Probleme in Ihren Web-Apps und Diensten.</span><span class="sxs-lookup"><span data-stu-id="ec9fd-106">Detect, triage, and diagnose issues in your web apps and services with [Application Insights](/azure/application-insights/app-insights-overview).</span></span>

<span data-ttu-id="ec9fd-107">Informationen zu den ersten Schritten mit Application Insights finden Sie unter [Erste Schritte mit Application Insights in einem Java-Webprojekt](/azure/application-insights/app-insights-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="ec9fd-107">To get started with Application Insights, see [Get started with Application Insights in a Java web project](/azure/application-insights/app-insights-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="ec9fd-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="ec9fd-108">Client library</span></span>

<span data-ttu-id="ec9fd-109">Fügen Sie Telemetrie hinzu, um mit der Application Insights-Clientbibliothek Ereignisse, Ausnahmen und Benutzermetriken in Ihren Apps nachzuverfolgen.</span><span class="sxs-lookup"><span data-stu-id="ec9fd-109">Add telemetry to track events, exceptions, and user metrics in your apps with the Application Insights client library.</span></span>

<span data-ttu-id="ec9fd-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ec9fd-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="ec9fd-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ec9fd-111">Example</span></span>

<span data-ttu-id="ec9fd-112">Erstellen eines neuen Metrikeintrags und Aufzeichnen eines Werts dafür</span><span class="sxs-lookup"><span data-stu-id="ec9fd-112">Create a new metric entry and record a value for it.</span></span>

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec9fd-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="ec9fd-113">Explore the Client APIs</span></span>](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a><span data-ttu-id="ec9fd-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ec9fd-114">Samples</span></span>

<span data-ttu-id="ec9fd-115">Sehen Sie sich weitere [Java-Codebeispiele für Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ec9fd-115">Explore more [sample Java code for Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) you can use in your apps.</span></span>
