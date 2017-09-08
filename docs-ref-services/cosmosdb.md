---
title: "Azure DB Cosmos-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Clientbibliotheken für Azure Cosmos DB"
keywords: Azure, Java, SDK, API, SQL, Datenbank, MongoDB, Cosmos DB, NoSQL, DocumentDB
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 249907528c24395b0da5d64e4dc06e3422894cfe
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cosmos-db-libraries-for-java"></a><span data-ttu-id="29fb5-104">Azure DB Cosmos-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="29fb5-104">Azure Cosmos DB libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="29fb5-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="29fb5-105">Overview</span></span>

<span data-ttu-id="29fb5-106">Mit [Cosmos DB](/azure/cosmos-db/introduction) können Sie Schlüsselwerte, JSON-Dokumente, Diagramme und Spaltendaten in einer global verteilten Datenbank speichern und abfragen.</span><span class="sxs-lookup"><span data-stu-id="29fb5-106">Store and query key-value, JSON document, graph, and columnar data in a globally distributed database with [Cosmos DB](/azure/cosmos-db/introduction).</span></span>

<span data-ttu-id="29fb5-107">Informationen zu den ersten Schritten mit Cosmos DB finden Sie unter [Azure Cosmos DB: Erstellen einer Dokumentdatenbank mit Java und dem Azure-Portal](/azure/cosmos-db/create-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="29fb5-107">To get started with Cosmos DB, see [Azure Cosmos DB: Build an API app with Java and the Azure portal](/azure/cosmos-db/create-documentdb-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="29fb5-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="29fb5-108">Client library</span></span>

<span data-ttu-id="29fb5-109">Stellen Sie mit der [DocumentDB](/azure/cosmos-db/documentdb-introduction)-Clientbibliothek eine Verbindung mit Cosmos DB her, um mit der [SQL-Abfragesyntax](/azure/cosmos-db/documentdb-sql-query) JSON-Daten zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="29fb5-109">Connect to Cosmos DB using the [DocumentDB](/azure/cosmos-db/documentdb-introduction) client library to work with JSON data with [SQL query syntax](/azure/cosmos-db/documentdb-sql-query).</span></span>

<span data-ttu-id="29fb5-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Cosmos DB-Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="29fb5-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the Cosmos DB client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="29fb5-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="29fb5-111">Example</span></span>

<span data-ttu-id="29fb5-112">Wählen Sie übereinstimmende JSON-Dokumente in Cosmos DB mit der SQL-Abfragesyntax aus:</span><span class="sxs-lookup"><span data-stu-id="29fb5-112">Select matching JSON documents in Cosmos DB using SQL query syntax.</span></span>

```java
DocumentClient client = new DocumentClient(new DocumentClient("https://contoso.documents.azure.com:443",
                "contosoCosmosDBKey", 
                new ConnectionPolicy(),
                ConsistencyLevel.Session);

List<Document> results = client.queryDocuments("dbs/" + DATABASE_ID + "/colls/" + COLLECTION_ID,
        "SELECT * FROM myCollection WHERE myCollection.email = 'allen [at] contoso.com'",
        null)
    .getQueryIterable()
    .toList();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="29fb5-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="29fb5-113">Explore the Client APIs</span></span>](/java/api/overview/azure/cosmosdb/clientlibrary)


## <a name="samples"></a><span data-ttu-id="29fb5-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="29fb5-114">Samples</span></span>

<span data-ttu-id="29fb5-115">[Entwickeln einer Java-App mit der MongoDB-API von Azure Cosmos DB][2] </span><span class="sxs-lookup"><span data-stu-id="29fb5-115">[Develop a Java app using Azure Cosmos DB MongoDB API][2] </span></span>  
<span data-ttu-id="29fb5-116">[Entwickeln einer Java-App mit der Graph-API von Azure Cosmos DB][3] </span><span class="sxs-lookup"><span data-stu-id="29fb5-116">[Develop a Java app using Azure Cosmos DB Graph API][3] </span></span>  
<span data-ttu-id="29fb5-117">[Entwickeln einer Java-App mit der DocumentDB-API von Azure Cosmos DB][4]</span><span class="sxs-lookup"><span data-stu-id="29fb5-117">[Develop a Java app using Azure Cosmos DB DocumentDB API][4]</span></span>        

<span data-ttu-id="29fb5-118">Sehen Sie sich weitere [Java-Codebeispiele für Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="29fb5-118">Explore more [sample Java code for Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) you can use in your apps.</span></span>

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started