---
title: "Azure Data Lake Store-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Data Lake Store-Bibliotheken"
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
ms.openlocfilehash: 66ff566e74203d3b5a8e9bcc170f4c21cf310645
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-store-libraries-for-java"></a><span data-ttu-id="17c1b-104">Azure Data Lake Store-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="17c1b-104">Azure Data Lake Store libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="17c1b-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="17c1b-105">Overview</span></span>

<span data-ttu-id="17c1b-106">Erfassen Sie für die Analyse mit [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview) Daten von beliebiger Größe, Art und Erfassungsgeschwindigkeit an einer zentralen Stelle.</span><span class="sxs-lookup"><span data-stu-id="17c1b-106">Capture data of any size, type, and ingestion speed in a single place for analytics with [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

<span data-ttu-id="17c1b-107">Informationen zu den ersten Schritten mit Data Lake Store finden Sie unter [Erste Schritte mit Azure Data Lake Store mit Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span><span class="sxs-lookup"><span data-stu-id="17c1b-107">To get started with Data Lake Store, see [Get started with Azure Data Lake Store using Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span></span>


## <a name="client-library"></a><span data-ttu-id="17c1b-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="17c1b-108">Client library</span></span>

<span data-ttu-id="17c1b-109">Mit der Clientbibliothek können Sie in Data Lake Store Dateien lesen und schreiben, Berechtigungen und Metadaten festlegen sowie Dateien und Verzeichnisse verwalten.</span><span class="sxs-lookup"><span data-stu-id="17c1b-109">Read and write files, set permissions and metadata, and manage files and directories in Data Lake Store with the client library.</span></span>

<span data-ttu-id="17c1b-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="17c1b-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="17c1b-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="17c1b-111">Example</span></span>

<span data-ttu-id="17c1b-112">Erstellen eines Data Lake-Clients auf der Grundlage eines vollqualifizierten Domänennamens und eines OAuth2-Zugriffstokens und anschließendes Erstellen einer Datei in Data Lake und Schreiben in diese Datei</span><span class="sxs-lookup"><span data-stu-id="17c1b-112">Create a Data Lake client from a fully qualified domain name and OAuth2 access token, then create a file in Data Lake and write to it.</span></span>

```java
// AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);
ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

// create directory
client.createDirectory("/a/b/w");
        
// create file and write some content
String filename = "/a/b/c.txt";
OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
PrintStream out = new PrintStream(stream);
for (int i = 1; i <= 10; i++) {
    out.println("This is line #" + i);
    out.format("This is the same line (%d), but using formatted output. %n", i);
}
out.close();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="17c1b-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="17c1b-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakestore/clientlibrary)


## <a name="management-api"></a><span data-ttu-id="17c1b-114">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="17c1b-114">Management API</span></span>

<span data-ttu-id="17c1b-115">Verwenden Sie die Verwaltungs-API zum Verwalten von Data Lake Store-Konten, Firewallregeln und vertrauenswürdigen Identitätsanbietern.</span><span class="sxs-lookup"><span data-stu-id="17c1b-115">Use the management API to manage Data Lake Store accounts, firewall rules, and trusted identity providers.</span></span>

<span data-ttu-id="17c1b-116">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="17c1b-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="17c1b-117">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="17c1b-117">Explore the Management APIs</span></span>](/java/api/overview/azure/datalakestore/managementapi)

## <a name="samples"></a><span data-ttu-id="17c1b-118">Beispiele</span><span class="sxs-lookup"><span data-stu-id="17c1b-118">Samples</span></span>

<span data-ttu-id="17c1b-119">[Erste Schritte mit Azure Data Lake][1]</span><span class="sxs-lookup"><span data-stu-id="17c1b-119">[Azure Data Lake Get Started][1]</span></span> 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

<span data-ttu-id="17c1b-120">Sehen Sie sich weitere [Java-Codebeispiele für Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="17c1b-120">Explore more [sample Java code for Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) you can use in your apps.</span></span>
