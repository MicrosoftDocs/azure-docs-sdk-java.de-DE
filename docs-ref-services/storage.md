---
title: Azure Storage-Bibliotheken für Java
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: douge
manager: douge
ms.date: 02/07/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: ec06e79374176b5a4795d27c5fbbb2260e65cd8c
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="553c8-103">Azure Storage-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="553c8-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="553c8-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="553c8-104">Overview</span></span>

<span data-ttu-id="553c8-105">Lesen und schreiben Sie mit [Azure Storage](/azure/storage/storage-introduction) Dateien, Blob- bzw. Objektdaten, Schlüssel-Wert-Paare und Nachrichten aus Ihren Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="553c8-105">Read and write files, blob (object) data, key-value pairs, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="553c8-106">Informationen zu den ersten Schritten mit Azure Storage finden Sie unter [Verwenden des Blob-Speichers mit Java](/azure/storage/storage-java-how-to-use-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="553c8-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/storage-java-how-to-use-blob-storage).</span></span>

## <a name="client-library"></a><span data-ttu-id="553c8-107">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="553c8-107">Client library</span></span>

<span data-ttu-id="553c8-108">Verwenden Sie [Verbindungszeichenfolgen](/azure/storage/storage-create-storage-account#manage-your-storage-account), um eine Verbindung mit einem Azure Storage-Konto herzustellen. Nutzen Sie anschließend die Klassen und Methoden der Clientbibliotheken, um mit Blob-, Tabellen-, Datei- oder Warteschlangenspeicher zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="553c8-108">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span> 

<span data-ttu-id="553c8-109">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="553c8-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="553c8-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="553c8-110">Example</span></span>

<span data-ttu-id="553c8-111">Schreiben Sie eine Bilddatei aus dem lokalen Dateisystem in ein neues Blob in einem vorhandenen Azure Storage-Blobcontainer.</span><span class="sxs-lookup"><span data-stu-id="553c8-111">Write a image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
String storageConnectionString = "DefaultEndpointsProtocol=https;" + 
"AccountName=fabrikamblobstorage;" + 
"AccountKey=keyvalue;EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient serviceClient = account.createCloudBlobClient();
CloudBlobContainer container = serviceClient.getContainerReference(blobContainer);

// write a blob from a local filesystem path to the container as logo.png
CloudBlockBlob blob = container.getBlockBlobReference("logo.png");
blob.uploadFromFile("/Users/raisa/fabrikam.png");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="553c8-112">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="553c8-112">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="553c8-113">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="553c8-113">Management API</span></span>

<span data-ttu-id="553c8-114">Erstellen und Verwalten Sie Azure Storage-Konten und -Verbindungsschlüssel mit der Verwaltungs-API.</span><span class="sxs-lookup"><span data-stu-id="553c8-114">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="553c8-115">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="553c8-115">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="553c8-116">Beispiel</span><span class="sxs-lookup"><span data-stu-id="553c8-116">Example</span></span>

<span data-ttu-id="553c8-117">Erstellen Sie in Ihrem Abonnement ein neues Azure Storage-Konto, und rufen Sie dessen Zugriffsschlüssel ab.</span><span class="sxs-lookup"><span data-stu-id="553c8-117">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

```java
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
        .withRegion(Region.US_EAST)
        .withNewResourceGroup(rgName)
        .create();

// get a list of storage account keys related to the account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="553c8-118">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="553c8-118">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="553c8-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="553c8-119">Samples</span></span>

<span data-ttu-id="553c8-120">[Verwalten von Azure Storage-Konten](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span><span class="sxs-lookup"><span data-stu-id="553c8-120">[Manage Azure Storage accounts](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span></span>  
<span data-ttu-id="553c8-121">[Lesen und Schreiben von Objekten aus dem bzw. in den Blobspeicher](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="553c8-121">[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span></span>  
<span data-ttu-id="553c8-122">[Lesen und Schreiben von Nachrichten mit Warteschlangen](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="553c8-122">[Read and write messages with queues](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span></span>  
[<span data-ttu-id="553c8-123">Lesen von Dateien aus dem Blobspeicher in einer Web-App</span><span class="sxs-lookup"><span data-stu-id="553c8-123">Read files from blob storage in a web app</span></span>](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

<span data-ttu-id="553c8-124">Sehen Sie sich weitere [Java-Codebeispiele für Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="553c8-124">Explore more [sample Java code for Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) you can use in your apps.</span></span>
