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
# <a name="azure-data-lake-store-libraries-for-java"></a>Azure Data Lake Store-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Erfassen Sie für die Analyse mit [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview) Daten von beliebiger Größe, Art und Erfassungsgeschwindigkeit an einer zentralen Stelle.

Informationen zu den ersten Schritten mit Data Lake Store finden Sie unter [Erste Schritte mit Azure Data Lake Store mit Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).


## <a name="client-library"></a>Clientbibliothek

Mit der Clientbibliothek können Sie in Data Lake Store Dateien lesen und schreiben, Berechtigungen und Metadaten festlegen sowie Dateien und Verzeichnisse verwalten.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a>Beispiel

Erstellen eines Data Lake-Clients auf der Grundlage eines vollqualifizierten Domänennamens und eines OAuth2-Zugriffstokens und anschließendes Erstellen einer Datei in Data Lake und Schreiben in diese Datei

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
> [Informationen zu den Client-APIs](/java/api/overview/azure/datalakestore/clientlibrary)


## <a name="management-api"></a>Verwaltungs-API

Verwenden Sie die Verwaltungs-API zum Verwalten von Data Lake Store-Konten, Firewallregeln und vertrauenswürdigen Identitätsanbietern.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/datalakestore/managementapi)

## <a name="samples"></a>Beispiele

[Erste Schritte mit Azure Data Lake][1] 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

Sehen Sie sich weitere [Java-Codebeispiele für Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) an, die Sie in Ihren Apps verwenden können.
