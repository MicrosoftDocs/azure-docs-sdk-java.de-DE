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
# <a name="azure-libraries-for-java"></a><span data-ttu-id="a73d0-104">Azure-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="a73d0-104">Azure libraries for Java</span></span>

<span data-ttu-id="a73d0-105">Azure-Bibliotheken unterstützen Sie bei der Nutzung von Azure-Diensten in Ihren Java-Apps unter Verwendung nativer Schnittstellen.</span><span class="sxs-lookup"><span data-stu-id="a73d0-105">Azure libraries help you consume Azure services in your Java apps using native interfaces.</span></span> <span data-ttu-id="a73d0-106">Jede Bibliothek ist unabhängig und kann getrennt von den anderen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a73d0-106">Each library is independent and can be used separately from the others another.</span></span>

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [<span data-ttu-id="a73d0-107">Azure Storage (in englischer Sprache)</span><span class="sxs-lookup"><span data-stu-id="a73d0-107">Azure Storage</span></span>](#azure-storage) | [<span data-ttu-id="a73d0-108">SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="a73d0-108">SQL Database</span></span>](#sql-database)  | [<span data-ttu-id="a73d0-109">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="a73d0-109">Redis Cache</span></span>](#redis-cache)   | [<span data-ttu-id="a73d0-110">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a73d0-110">DocumentDB</span></span>](#documentdb) |
| [<span data-ttu-id="a73d0-111">Service Bus</span><span class="sxs-lookup"><span data-stu-id="a73d0-111">Service Bus</span></span>](#servicebus)  | [<span data-ttu-id="a73d0-112">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a73d0-112">Azure Active Directory</span></span>](#azuread) | [<span data-ttu-id="a73d0-113">Schlüsseltresor</span><span class="sxs-lookup"><span data-stu-id="a73d0-113">Key Vault</span></span>](#keyvault)  | [<span data-ttu-id="a73d0-114">Event Hub</span><span class="sxs-lookup"><span data-stu-id="a73d0-114">Event Hub</span></span>](#eventhub)
| [<span data-ttu-id="a73d0-115">IoT-Dienst</span><span class="sxs-lookup"><span data-stu-id="a73d0-115">IoT Service</span></span>](#iotservice) | [<span data-ttu-id="a73d0-116">IoT-Gerät</span><span class="sxs-lookup"><span data-stu-id="a73d0-116">IoT Device</span></span>](#iotdevice) | [<span data-ttu-id="a73d0-117">Data Lake</span><span class="sxs-lookup"><span data-stu-id="a73d0-117">Data Lake</span></span>](#datalake)  | [<span data-ttu-id="a73d0-118">AppInsights</span><span class="sxs-lookup"><span data-stu-id="a73d0-118">AppInsights</span></span>](#appinsights) | 
| [<span data-ttu-id="a73d0-119">Batch</span><span class="sxs-lookup"><span data-stu-id="a73d0-119">Batch</span></span>](#batch) | [<span data-ttu-id="a73d0-120">Manage Azure resources (Verwalten von Azure-Ressourcen)</span><span class="sxs-lookup"><span data-stu-id="a73d0-120">Manage Azure resources</span></span>](#management) |

## <a name="install-with-maven"></a><span data-ttu-id="a73d0-121">Installieren mit Maven</span><span class="sxs-lookup"><span data-stu-id="a73d0-121">Install with Maven</span></span>

<span data-ttu-id="a73d0-122">Fügen Sie in `pom.xml` einen Abhängigkeitseintrag hinzu, um eine Bibliothek in Ihr [Maven](https://maven.apache.org)-Projekt zu importieren.</span><span class="sxs-lookup"><span data-stu-id="a73d0-122">Add a dependency entry in your `pom.xml` to import a library into your [Maven](https://maven.apache.org) project.</span></span>

<span data-ttu-id="a73d0-123">Verwenden Sie beispielsweise Folgendes, um die neueste Version der [Azure-Verwaltungsbibliotheken für Java](#management) einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="a73d0-123">For example, to include the latest version of the [Azure management libraries for Java](#management):</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="a73d0-124">Andere Java-Erstellungstools (beispielsweise Gradle) werden zwar ebenfalls unterstützt, die entsprechenden Installationsschritte sind in diesem Artikel jedoch nicht enthalten.</span><span class="sxs-lookup"><span data-stu-id="a73d0-124">Other Java build tools like Gradle are supported but the install steps are not provided in this article.</span></span> <span data-ttu-id="a73d0-125">Informationen zur Nutzung von Maven-Importen finden Sie in der Dokumentation Ihres Erstellungstools.</span><span class="sxs-lookup"><span data-stu-id="a73d0-125">Review the documentation for your build tool on how to consume Maven imports.</span></span>

## <a name="azure-service-libraries"></a><span data-ttu-id="a73d0-126">Azure-Dienstbibliotheken</span><span class="sxs-lookup"><span data-stu-id="a73d0-126">Azure service libraries</span></span>

<span data-ttu-id="a73d0-127">Integrieren Sie Azure-Dienste, um den Funktionsumfang Ihrer Apps mithilfe dieser Bibliotheken zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="a73d0-127">Integrate Azure services to add functionality to your apps using these libraries.</span></span> <span data-ttu-id="a73d0-128">Weitere Informationen zum Erstellen von Apps mit Azure-Diensten finden Sie im [Java Developer Center](https://azure.microsoft.com/develop/java).</span><span class="sxs-lookup"><span data-stu-id="a73d0-128">Learn more about building apps with Azure services at the [Java developer center](https://azure.microsoft.com/develop/java).</span></span>

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[<span data-ttu-id="a73d0-129">Azure Storage (in englischer Sprache)</span><span class="sxs-lookup"><span data-stu-id="a73d0-129">Azure Storage</span></span>](/azure/storage/storage-introduction)  

<span data-ttu-id="a73d0-130">Datenspeicher und Messaging für Ihre Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="a73d0-130">Data storage and messaging for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

<span data-ttu-id="a73d0-131">[Beispiele](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Referenz](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Versionshinweise](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span><span class="sxs-lookup"><span data-stu-id="a73d0-131">[Samples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Reference](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Release Notes](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span></span>

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[<span data-ttu-id="a73d0-132">SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="a73d0-132">SQL Database</span></span>](/azure/sql-database/sql-database-technical-overview)

<span data-ttu-id="a73d0-133">JDBC-Treiber für Azure SQL-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="a73d0-133">JDBC driver for Azure SQL Database.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="a73d0-134">[Beispiele](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Referenz](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Versionshinweise](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span><span class="sxs-lookup"><span data-stu-id="a73d0-134">[Samples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Reference](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Release Notes](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span></span>

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[<span data-ttu-id="a73d0-135">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="a73d0-135">Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)

<span data-ttu-id="a73d0-136">Schlüssel-Wert-Speicher mit geringer Wartezeit und hoher Leistung.</span><span class="sxs-lookup"><span data-stu-id="a73d0-136">Low-latency, high-performance key-value store.</span></span>

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

<span data-ttu-id="a73d0-137">[Beispiele](/azure/redis-cache/cache-java-get-started) | [Referenz](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Versionshinweise](https://github.com/xetorthio/jedis/releases)</span><span class="sxs-lookup"><span data-stu-id="a73d0-137">[Samples](/azure/redis-cache/cache-java-get-started) | [Reference](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Release Notes](https://github.com/xetorthio/jedis/releases)</span></span>  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[<span data-ttu-id="a73d0-138">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a73d0-138">Cosmos DB</span></span>](/azure/documentdb/documentdb-introduction)

<span data-ttu-id="a73d0-139">Skalierbare NoSQL-Datenbank mit JSON-Dokumenten und SQL- oder JavaScript-Abfragesyntax.</span><span class="sxs-lookup"><span data-stu-id="a73d0-139">Scalable NoSQL database with JSON documents and a SQL or JavaScript query syntax.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

<span data-ttu-id="a73d0-140">[Beispiele](/azure/documentdb/documentdb-java-application) | [Referenz](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Versionshinweise](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span><span class="sxs-lookup"><span data-stu-id="a73d0-140">[Samples](/azure/documentdb/documentdb-java-application) | [Reference](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Release Notes](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span></span>

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="a73d0-141">ServiceBus</span><span class="sxs-lookup"><span data-stu-id="a73d0-141">ServiceBus</span></span>](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 <span data-ttu-id="a73d0-142">Service Bus ist ein professioneller Plattformdienst für transaktionales Messaging.</span><span class="sxs-lookup"><span data-stu-id="a73d0-142">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 <span data-ttu-id="a73d0-143">[Beispiele](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referenz](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Versionshinweise](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="a73d0-143">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[<span data-ttu-id="a73d0-144">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a73d0-144">Azure Active Directory</span></span>](/azure/active-directory/active-directory-whatis)   

<span data-ttu-id="a73d0-145">Identitätsverwaltung und sichere Anmeldung für Ihre Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="a73d0-145">Identity management and secure sign-in for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
<span data-ttu-id="a73d0-146">[Beispiele](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Referenz](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Versionshinweise](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span><span class="sxs-lookup"><span data-stu-id="a73d0-146">[Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Reference](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Release Notes](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span></span>
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[<span data-ttu-id="a73d0-147">Schlüsseltresor</span><span class="sxs-lookup"><span data-stu-id="a73d0-147">Key Vault</span></span>](/azure/key-vault) 

<span data-ttu-id="a73d0-148">Sicherer Zugriff auf Schlüssel und Geheimnisse über Ihre Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="a73d0-148">Safely access keys and secrets from your applications.</span></span> 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

<span data-ttu-id="a73d0-149">[Beispiele](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Referenz](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Versionshinweise](https://github.com/Azure/azure-keyvault-java)</span><span class="sxs-lookup"><span data-stu-id="a73d0-149">[Samples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Reference](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Release Notes](https://github.com/Azure/azure-keyvault-java)</span></span> 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[<span data-ttu-id="a73d0-150">Event Hub</span><span class="sxs-lookup"><span data-stu-id="a73d0-150">Event Hub</span></span>](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
<span data-ttu-id="a73d0-151">Ereignis- und Telemetrieverarbeitung mit hohem Durchsatz für Ihre Instrumentations- oder IoT-Szenarien.</span><span class="sxs-lookup"><span data-stu-id="a73d0-151">High-throughput event and telemetry handling for your instrumentation or IoT scenarios.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

<span data-ttu-id="a73d0-152">[Beispiele](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Referenz](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Versionshinweise](https://github.com/Azure/azure-event-hubs-java)</span><span class="sxs-lookup"><span data-stu-id="a73d0-152">[Samples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Reference](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Release Notes](https://github.com/Azure/azure-event-hubs-java)</span></span>

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[<span data-ttu-id="a73d0-153">IoT-Dienst</span><span class="sxs-lookup"><span data-stu-id="a73d0-153">IoT Service</span></span>](/azure/iot-hub/)

<span data-ttu-id="a73d0-154">Verwalten von Identitäten, Senden von Nachrichten und Erhalten von Feedback von Geräten, die bei Ihrem IoT Hub registriert sind.</span><span class="sxs-lookup"><span data-stu-id="a73d0-154">Manage identities, send messages, and get feedback from devices registered with your IoT hub.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
<span data-ttu-id="a73d0-155">[Beispiele](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Referenz](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Versionshinweise](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="a73d0-155">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[<span data-ttu-id="a73d0-156">IoT-Gerät</span><span class="sxs-lookup"><span data-stu-id="a73d0-156">IoT Device</span></span>](/azure/iot-hub/iot-hub-devguide)

<span data-ttu-id="a73d0-157">Senden einer Nachricht an einen IoT Hub über Ihr Gerät.</span><span class="sxs-lookup"><span data-stu-id="a73d0-157">Send a message to an IoT hub from your device.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

<span data-ttu-id="a73d0-158">[Beispiele](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Referenz](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Versionshinweise](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="a73d0-158">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[<span data-ttu-id="a73d0-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a73d0-159">Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)   
   
<span data-ttu-id="a73d0-160">Erfassen von Daten beliebiger Größe und in beliebigem Format an einem zentralen Ort zu Analysezwecken.</span><span class="sxs-lookup"><span data-stu-id="a73d0-160">Capture data of any size and shape into a single location for performing analytics.</span></span>    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

<span data-ttu-id="a73d0-161">[Beispiele](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Referenz](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Versionshinweise](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span><span class="sxs-lookup"><span data-stu-id="a73d0-161">[Samples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Reference](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Release Notes](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span></span>

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[<span data-ttu-id="a73d0-162">AppInsights</span><span class="sxs-lookup"><span data-stu-id="a73d0-162">AppInsights</span></span>](/azure/application-insights/app-insights-overview)

<span data-ttu-id="a73d0-163">Nachverfolgen der Verwendung, Hinzufügen von Telemetriedaten und Überwachen Ihrer Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="a73d0-163">Track usage, add telemetry, and monitor your web apps.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

<span data-ttu-id="a73d0-164">[Beispiele](/azure/application-insights/app-insights-java-get-started) | [Referenz](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Versionshinweise](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span><span class="sxs-lookup"><span data-stu-id="a73d0-164">[Samples](/azure/application-insights/app-insights-java-get-started) | [Reference](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Release Notes](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span></span>

<a name="batch"></a>

### <a name="batchazurebatch"></a>[<span data-ttu-id="a73d0-165">Batch</span><span class="sxs-lookup"><span data-stu-id="a73d0-165">Batch</span></span>](/azure/batch)

<span data-ttu-id="a73d0-166">Effizientes Ausführen umfangreicher paralleler HPC-Anwendungen in der Cloud.</span><span class="sxs-lookup"><span data-stu-id="a73d0-166">Run large-scale parallel and high-performance computing applications efficiently in the cloud.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

<span data-ttu-id="a73d0-167">[Beispiele](https://github.com/azure/azure-batch-samples) | [Referenz](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Versionshinweise](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="a73d0-167">[Samples](https://github.com/azure/azure-batch-samples) | [Reference](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Release Notes](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span></span>

<a name="management"></a> 

## <a name="manage-azure-resources"></a><span data-ttu-id="a73d0-168">Verwalten von Azure-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a73d0-168">Manage Azure resources</span></span>

<span data-ttu-id="a73d0-169">Erstellen, Aktualisieren und Löschen von Azure-Ressourcen über Ihren Anwendungscode.</span><span class="sxs-lookup"><span data-stu-id="a73d0-169">Create, update, and delete Azure resources from your application code.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="a73d0-170">[Beispiele](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Referenz](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Versionshinweise](java-sdk-azure-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="a73d0-170">[Samples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Reference](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Release Notes](java-sdk-azure-release-notes.md)</span></span>

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="a73d0-171">ServiceBus</span><span class="sxs-lookup"><span data-stu-id="a73d0-171">ServiceBus</span></span>](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
<span data-ttu-id="a73d0-172">Service Bus ist ein professioneller Plattformdienst für transaktionales Messaging.</span><span class="sxs-lookup"><span data-stu-id="a73d0-172">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

<span data-ttu-id="a73d0-173">[Beispiele](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referenz](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Versionshinweise](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="a73d0-173">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>

