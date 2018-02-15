---
title: "Azure Storage-Bibliotheken für Java"
description: 
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
ms.openlocfilehash: 3c7a3a1fcf2e97202e7f38f8df5acb6637fb4b47
ms.sourcegitcommit: 2ae0d99c02f4ad7efa9e3d3fbd1db7e9de20c6e7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="azure-storage-libraries-for-java"></a>Azure Storage-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Lesen und schreiben Sie mit [Azure Storage](/azure/storage/storage-introduction) Dateien, Blob- bzw. Objektdaten, Schlüssel-Wert-Paare und Nachrichten aus Ihren Java-Anwendungen.

Informationen zu den ersten Schritten mit Azure Storage finden Sie unter [Verwenden des Blob-Speichers mit Java](/azure/storage/storage-java-how-to-use-blob-storage).

## <a name="client-library"></a>Clientbibliothek

Verwenden Sie [Verbindungszeichenfolgen](/azure/storage/storage-create-storage-account#manage-your-storage-account), um eine Verbindung mit einem Azure Storage-Konto herzustellen. Nutzen Sie anschließend die Klassen und Methoden der Clientbibliotheken, um mit Blob-, Tabellen-, Datei- oder Warteschlangenspeicher zu arbeiten. 

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Schreiben Sie eine Bilddatei aus dem lokalen Dateisystem in ein neues Blob in einem vorhandenen Azure Storage-Blobcontainer.


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
> [Informationen zu den Client-APIs](/java/api/overview/azure/storage/clientlibrary)

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
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/storage/managementapi)


## <a name="samples"></a>Beispiele

[Verwalten von Azure Storage-Konten](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)    
[Lesen und Schreiben von Objekten aus dem bzw. in den Blobspeicher](https://github.com/Azure-Samples/storage-blob-java-getting-started)   
[Lesen und Schreiben von Nachrichten mit Warteschlangen](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
[Lesen von Dateien aus dem Blobspeicher in einer Web-App](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

Sehen Sie sich weitere [Java-Codebeispiele für Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) an, die Sie in Ihren Apps verwenden können.
