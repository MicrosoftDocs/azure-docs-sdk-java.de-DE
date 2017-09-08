---
title: "Azure Data Lake Analytics-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Data Lake Analytics-Bibliotheken"
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
ms.openlocfilehash: 19d580a8700aad36897b473ff96f1b05bb3f83c7
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a><span data-ttu-id="37490-104">Azure Data Lake Analytics-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="37490-104">Azure Data Lake Analytics libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="37490-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="37490-105">Overview</span></span>

<span data-ttu-id="37490-106">Ausführen von Big Data-Analyseaufträgen, die sich mit [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview) auf besonders umfangreiche Datasets skalieren lassen.</span><span class="sxs-lookup"><span data-stu-id="37490-106">Run big data analysis jobs that scale to massive data sets with [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

<span data-ttu-id="37490-107">Informationen zu den ersten Schritten mit Azure Data Lake Analytics finden Sie unter [Erste Schritte mit Azure Data Lake Analytics mithilfe des Java SDK](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).</span><span class="sxs-lookup"><span data-stu-id="37490-107">To get started with Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics using Java SDK](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).</span></span>

## <a name="management-api"></a><span data-ttu-id="37490-108">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="37490-108">Management API</span></span>

<span data-ttu-id="37490-109">Verwenden Sie die Verwaltungs-API zum Verwalten von Data Lake Analytics-Konten, -Aufträgen, -Richtlinien und -Katalogen.</span><span class="sxs-lookup"><span data-stu-id="37490-109">Use the management API to manage Data Lake Analytics accounts, jobs, policies, and catalogs.</span></span>

<span data-ttu-id="37490-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="37490-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="37490-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="37490-111">Example</span></span>

<span data-ttu-id="37490-112">Übermitteln eines neuen U-SQL-Auftrags an Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="37490-112">Submit a new U-SQL job to Data Lake Analytics.</span></span>

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
> [<span data-ttu-id="37490-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="37490-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakeanalytics/managementapi)

## <a name="samples"></a><span data-ttu-id="37490-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="37490-114">Samples</span></span>

<span data-ttu-id="37490-115">[Erste Schritte mit Azure Data Lake Analytics mithilfe des Java SDK][1]</span><span class="sxs-lookup"><span data-stu-id="37490-115">[Azure Data Lake Analytics using Java SDK][1]</span></span> 

[1]: https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

<span data-ttu-id="37490-116">Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) von Azure Data Lake Analytics-Beispielen an.</span><span class="sxs-lookup"><span data-stu-id="37490-116">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) of Azure Data Lake Analytics samples.</span></span>
