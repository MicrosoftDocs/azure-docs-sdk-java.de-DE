---
title: Azure Data Lake Analytics-Bibliotheken für Java
description: Referenzdokumentation für die Java-Data Lake Analytics-Bibliotheken
keywords: Azure, Java, SDK, API, Big Data, Data Lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 0e97d2c53ca6b993a2240b37576e765009f81c51
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799856"
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a>Azure Data Lake Analytics-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Ausführen von Big Data-Analyseaufträgen, die sich mit [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview) auf besonders umfangreiche Datasets skalieren lassen.

Informationen zu den ersten Schritten mit Azure Data Lake Analytics finden Sie unter [Erste Schritte mit Azure Data Lake Analytics mithilfe des Java SDK](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).

## <a name="management-api"></a>Verwaltungs-API

Verwenden Sie die Verwaltungs-API zum Verwalten von Data Lake Analytics-Konten, -Aufträgen, -Richtlinien und -Katalogen.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a>Beispiel

Übermitteln eines neuen U-SQL-Auftrags an Data Lake Analytics

```java
// authenticate with service principal credentials
ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
DataLakeAnalyticsJobManagementClient adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);

// set up job parameters
UUID jobId = java.util.UUID.randomUUID();
USqlJobProperties properties = new USqlJobProperties();
properties.setScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();");
JobInformation parameters = new JobInformation();
parameters.setName("testJob");
parameters.setJobId(jobId);
parameters.setType(JobType.USQL);
parameters.setProperties(properties);

// create the job
JobInformation jobInfo = adlaJobClient.getJobOperations().create(accountName, jobId, parameters).getBody();
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Beispiele

[Erste Schritte mit Azure Data Lake Analytics mithilfe des Java SDK][1] 

[1]: https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) von Azure Data Lake Analytics-Beispielen an.
