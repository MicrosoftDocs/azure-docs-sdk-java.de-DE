---
title: Azure DB Cosmos-Bibliotheken für Java
description: Referenzdokumentation für die Java-Clientbibliotheken für Azure Cosmos DB
keywords: Azure, Java, SDK, API, SQL, Datenbank, MongoDB, Cosmos DB, NoSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 6fc9f90cb3c8130aa82b20554a94a8b5ab78c083
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823843"
---
# <a name="azure-cosmos-db-libraries-for-java"></a>Azure DB Cosmos-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Mit [Azure Cosmos DB](/azure/cosmos-db/introduction) können Sie Schlüsselwerte, JSON-Dokumente, Diagramme und Spaltendaten in einer global verteilten Datenbank speichern und abfragen.

Informationen zu den ersten Schritten mit Azure Cosmos DB finden Sie unter [Azure Cosmos DB: Erstellen einer Dokumentdatenbank mit Java und dem Azure-Portal](/azure/cosmos-db/create-sql-api-java).

## <a name="client-library"></a>Clientbibliothek

Stellen Sie mithilfe der [SQL-API](/azure/cosmos-db/sql-api-introduction)-Clientbibliothek eine Verbindung mit Azure Cosmos DB her, um mit JSON-Daten mit [SQL-Abfragesyntax](/azure/cosmos-db/sql-api-sql-query) zu arbeiten.

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
> [Informationen zu den Client-APIs](/java/api/overview/azure/cosmosdb/client)


## <a name="samples"></a>Beispiele

[Entwickeln einer Java-App mit der MongoDB-API von Azure Cosmos DB][2]   
[Entwickeln einer Java-App mit der Graph-API von Azure Cosmos DB][3]   
[Entwickeln einer Java-App mit der SQL-API von Azure Cosmos DB][4]        

Sehen Sie sich weitere [Java-Codebeispiele für Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) an, die Sie in Ihren Apps verwenden können.

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
