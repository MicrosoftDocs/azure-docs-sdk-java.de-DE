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
ms.openlocfilehash: 393f57df0ea2076c6ee7045b56883ee088716fad
ms.sourcegitcommit: 93107ca9ed76a29573a5faf8f39737c85e6bbaff
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2017
---
# <a name="azure-cosmos-db-libraries-for-java"></a>Azure DB Cosmos-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Mit [Cosmos DB](/azure/cosmos-db/introduction) können Sie Schlüsselwerte, JSON-Dokumente, Diagramme und Spaltendaten in einer global verteilten Datenbank speichern und abfragen.

Informationen zu den ersten Schritten mit Cosmos DB finden Sie unter [Azure Cosmos DB: Erstellen einer Dokumentdatenbank mit Java und dem Azure-Portal](/azure/cosmos-db/create-documentdb-java).

## <a name="client-library"></a>Clientbibliothek

Stellen Sie mit der [DocumentDB](/azure/cosmos-db/documentdb-introduction)-Clientbibliothek eine Verbindung mit Cosmos DB her, um mit der [SQL-Abfragesyntax](/azure/cosmos-db/documentdb-sql-query) JSON-Daten zu arbeiten.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Cosmos DB-Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a>Beispiel

Wählen Sie übereinstimmende JSON-Dokumente in Cosmos DB mit der SQL-Abfragesyntax aus:

```java
DocumentClient client = new DocumentClient("https://contoso.documents.azure.com:443",
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
> [Informationen zu den Client-APIs](/java/api/overview/azure/cosmosdb/clientlibrary)


## <a name="samples"></a>Beispiele

[Entwickeln einer Java-App mit der MongoDB-API von Azure Cosmos DB][2]   
[Entwickeln einer Java-App mit der Graph-API von Azure Cosmos DB][3]   
[Entwickeln einer Java-App mit der DocumentDB-API von Azure Cosmos DB][4]        

Sehen Sie sich weitere [Java-Codebeispiele für Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) an, die Sie in Ihren Apps verwenden können.

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started