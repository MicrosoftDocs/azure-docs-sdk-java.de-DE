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
# <a name="azure-storage-libraries-for-java"></a>Azure Storage-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Lesen und schreiben Sie mit [Azure Storage](/azure/storage/storage-introduction) Blob- bzw. Objektdaten, Dateien und Schlüssel-Wert-Paare und Nachrichten aus Ihren Java-Anwendungen.

Informationen zu den ersten Schritten mit Azure Storage finden Sie im Thema zum [Verwenden des Blob-Speichers mit dem Java SDK v7](/azure/storage/blobs/storage-quickstart-blobs-java).

## <a name="client-library"></a>Clientbibliothek

Verwenden Sie einen gemeinsam verwendeten Schlüssel, ein SAS-Token oder ein OAuth-Token aus Azure Active Directory für die Autorisierung bei Azure Storage-Diensten. Verwenden Sie dann Klassen und Methoden von Clientbibliotheken, um mit Blob-, Datei- oder Warteschlangenspeicher zu arbeiten. 

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.   

**Abhängigkeit für das ältere Azure Storage SDK v7**:
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a>Beispiel

Schreiben Sie eine Imagedatei aus dem lokalen Dateisystem in ein neues Blob in einem vorhandenen Azure Storage-Blobcontainer.


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/java/api/overview/azure/storage/client)

## <a name="management-api"></a>Verwaltungs-API

Erstellen und Verwalten Sie Azure Storage-Konten und -Verbindungsschlüssel mit der Verwaltungs-API.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a>Beispiel

Erstellen Sie in Ihrem Abonnement ein neues Azure Storage-Konto, und rufen Sie dessen Zugriffsschlüssel ab.

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
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/storage/management)


## <a name="samples"></a>Beispiele

[Azure Storage-SDK für Java](https://github.com/azure/azure-storage-java)
[Lesen und Schreiben von Objekten aus dem bzw. in den Blobspeicher](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart)   
[Lesen und Schreiben von Nachrichten mit Warteschlangen](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
