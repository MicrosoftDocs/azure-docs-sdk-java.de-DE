---
title: Azure Storage-Bibliotheken für Java
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: seguler
manager: dineshm
ms.date: 10/29/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 68a5fdbf8e2fbfe83f9ea09112d64488e0c11d08
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235232"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="a42bf-103">Azure Storage-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="a42bf-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a42bf-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="a42bf-104">Overview</span></span>

<span data-ttu-id="a42bf-105">Lesen und schreiben Sie mit [Azure Storage](/azure/storage/storage-introduction) Blob- bzw. Objektdaten, Dateien und Schlüssel-Wert-Paare und Nachrichten aus Ihren Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="a42bf-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="a42bf-106">Informationen zu den ersten Schritten mit Azure Storage finden Sie im Thema zum [Verwenden des Blob-Speichers mit dem Java SDK v7](/azure/storage/blobs/storage-quickstart-blobs-java).</span><span class="sxs-lookup"><span data-stu-id="a42bf-106">To get started with Azure Storage, see [How to use Blob storage from Java SDK v7](/azure/storage/blobs/storage-quickstart-blobs-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="a42bf-107">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="a42bf-107">Client library</span></span>

<span data-ttu-id="a42bf-108">Verwenden Sie einen gemeinsam verwendeten Schlüssel, ein SAS-Token oder ein OAuth-Token aus Azure Active Directory für die Autorisierung bei Azure Storage-Diensten.</span><span class="sxs-lookup"><span data-stu-id="a42bf-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="a42bf-109">Verwenden Sie dann Klassen und Methoden von Clientbibliotheken, um mit Blob-, Datei- oder Warteschlangenspeicher zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="a42bf-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="a42bf-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a42bf-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="a42bf-111">**Abhängigkeit für das ältere Azure Storage SDK v7**:</span><span class="sxs-lookup"><span data-stu-id="a42bf-111">**Dependency for the legacy Azure Storage SDK v7**:</span></span>
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="a42bf-112">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a42bf-112">Example</span></span>

<span data-ttu-id="a42bf-113">Schreiben Sie eine Imagedatei aus dem lokalen Dateisystem in ein neues Blob in einem vorhandenen Azure Storage-Blobcontainer.</span><span class="sxs-lookup"><span data-stu-id="a42bf-113">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a42bf-114">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="a42bf-114">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="a42bf-115">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="a42bf-115">Management API</span></span>

<span data-ttu-id="a42bf-116">Erstellen und Verwalten Sie Azure Storage-Konten und -Verbindungsschlüssel mit der Verwaltungs-API.</span><span class="sxs-lookup"><span data-stu-id="a42bf-116">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="a42bf-117">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a42bf-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="a42bf-118">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a42bf-118">Example</span></span>

<span data-ttu-id="a42bf-119">Erstellen Sie in Ihrem Abonnement ein neues Azure Storage-Konto, und rufen Sie dessen Zugriffsschlüssel ab.</span><span class="sxs-lookup"><span data-stu-id="a42bf-119">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="a42bf-120">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="a42bf-120">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="a42bf-121">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a42bf-121">Samples</span></span>

<span data-ttu-id="a42bf-122">[Azure Storage-SDK für Java](https://github.com/azure/azure-storage-java)
[Lesen und Schreiben von Objekten aus dem bzw. in den Blobspeicher](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="a42bf-122">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="a42bf-123">Lesen und Schreiben von Nachrichten mit Warteschlangen</span><span class="sxs-lookup"><span data-stu-id="a42bf-123">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
