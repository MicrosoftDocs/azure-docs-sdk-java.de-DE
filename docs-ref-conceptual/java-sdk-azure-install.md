---
title: "Azure für Java-Entwickler | Microsoft-Dokumentation"
description: "Java SDK- und API-Referenz für Azure"
keywords: Azure Java, Azure Java-API-Referenz, Azure-Java-Klassenbibliothek, Azure SDK
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 570f820e1349e1dfd01a6c7f323b5312c14c40c6
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/14/2017
---
# <a name="azure-libraries-for-java"></a>Azure-Bibliotheken für Java

Azure-Bibliotheken unterstützen Sie bei der Nutzung von Azure-Diensten in Ihren Java-Apps unter Verwendung nativer Schnittstellen. Jede Bibliothek ist unabhängig und kann getrennt von den anderen verwendet werden.

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [Azure Storage (in englischer Sprache)](#azure-storage) | [SQL-Datenbank](#sql-database)  | [Redis Cache](#redis-cache)   | [DocumentDB](#documentdb) |
| [Service Bus](#servicebus)  | [Azure Active Directory](#azuread) | [Schlüsseltresor](#keyvault)  | [Event Hub](#eventhub)
| [IoT-Dienst](#iotservice) | [IoT-Gerät](#iotdevice) | [Data Lake](#datalake)  | [AppInsights](#appinsights) | 
| [Batch](#batch) | [Manage Azure resources (Verwalten von Azure-Ressourcen)](#management) |

## <a name="install-with-maven"></a>Installieren mit Maven

Fügen Sie in `pom.xml` einen Abhängigkeitseintrag hinzu, um eine Bibliothek in Ihr [Maven](https://maven.apache.org)-Projekt zu importieren.

Verwenden Sie beispielsweise Folgendes, um die neueste Version der [Azure-Verwaltungsbibliotheken für Java](#management) einzuschließen:

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

Andere Java-Erstellungstools (beispielsweise Gradle) werden zwar ebenfalls unterstützt, die entsprechenden Installationsschritte sind in diesem Artikel jedoch nicht enthalten. Informationen zur Nutzung von Maven-Importen finden Sie in der Dokumentation Ihres Erstellungstools.

## <a name="azure-service-libraries"></a>Azure-Dienstbibliotheken

Integrieren Sie Azure-Dienste, um den Funktionsumfang Ihrer Apps mithilfe dieser Bibliotheken zu erweitern. Weitere Informationen zum Erstellen von Apps mit Azure-Diensten finden Sie im [Java Developer Center](https://azure.microsoft.com/develop/java).

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[Azure Storage (in englischer Sprache)](/azure/storage/storage-introduction)  

Datenspeicher und Messaging für Ihre Anwendungen.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

[Beispiele](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Referenz](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Versionshinweise](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[SQL-Datenbank](/azure/sql-database/sql-database-technical-overview)

JDBC-Treiber für Azure SQL-Datenbank.

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

[Beispiele](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Referenz](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Versionshinweise](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[Redis Cache](https://azure.microsoft.com/services/cache/)

Schlüssel-Wert-Speicher mit geringer Wartezeit und hoher Leistung.

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

[Beispiele](/azure/redis-cache/cache-java-get-started) | [Referenz](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Versionshinweise](https://github.com/xetorthio/jedis/releases)  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[Cosmos DB](/azure/documentdb/documentdb-introduction)

Skalierbare NoSQL-Datenbank mit JSON-Dokumenten und SQL- oder JavaScript-Abfragesyntax.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

[Beispiele](/azure/documentdb/documentdb-java-application) | [Referenz](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Versionshinweise](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[ServiceBus](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 Service Bus ist ein professioneller Plattformdienst für transaktionales Messaging.
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 [Beispiele](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referenz](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Versionshinweise](https://github.com/Azure/azure-service-bus-java)   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[Azure Active Directory](/azure/active-directory/active-directory-whatis)   

Identitätsverwaltung und sichere Anmeldung für Ihre Anwendungen.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
[Beispiele](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Referenz](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Versionshinweise](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[Schlüsseltresor](/azure/key-vault) 

Sicherer Zugriff auf Schlüssel und Geheimnisse über Ihre Anwendungen. 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

[Beispiele](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Referenz](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Versionshinweise](https://github.com/Azure/azure-keyvault-java) 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[Event Hub](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
Ereignis- und Telemetrieverarbeitung mit hohem Durchsatz für Ihre Instrumentations- oder IoT-Szenarien.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

[Beispiele](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Referenz](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Versionshinweise](https://github.com/Azure/azure-event-hubs-java)

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[IoT-Dienst](/azure/iot-hub/)

Verwalten von Identitäten, Senden von Nachrichten und Erhalten von Feedback von Geräten, die bei Ihrem IoT Hub registriert sind.

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
[Beispiele](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Referenz](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Versionshinweise](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[IoT-Gerät](/azure/iot-hub/iot-hub-devguide)

Senden einer Nachricht an einen IoT Hub über Ihr Gerät.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

[Beispiele](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Referenz](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Versionshinweise](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[Data Lake Store](/azure/data-lake-store/data-lake-store-overview)   
   
Erfassen von Daten beliebiger Größe und in beliebigem Format an einem zentralen Ort zu Analysezwecken.    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

[Beispiele](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Referenz](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Versionshinweise](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[AppInsights](/azure/application-insights/app-insights-overview)

Nachverfolgen der Verwendung, Hinzufügen von Telemetriedaten und Überwachen Ihrer Web-Apps.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

[Beispiele](/azure/application-insights/app-insights-java-get-started) | [Referenz](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Versionshinweise](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)

<a name="batch"></a>

### <a name="batchazurebatch"></a>[Batch](/azure/batch)

Effizientes Ausführen umfangreicher paralleler HPC-Anwendungen in der Cloud.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

[Beispiele](https://github.com/azure/azure-batch-samples) | [Referenz](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Versionshinweise](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)

<a name="management"></a> 

## <a name="manage-azure-resources"></a>Verwalten von Azure-Ressourcen

Erstellen, Aktualisieren und Löschen von Azure-Ressourcen über Ihren Anwendungscode.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

[Beispiele](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Referenz](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Versionshinweise](java-sdk-azure-release-notes.md)

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[ServiceBus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
Service Bus ist ein professioneller Plattformdienst für transaktionales Messaging.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

[Beispiele](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referenz](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Versionshinweise](https://github.com/Azure/azure-service-bus-java)

