---
title: Bibliotheken zu Azure-Datenbank für PostgreSQL für Java
description: Referenzdokumentation für die Java-Clientbibliotheken für Azure-Datenbank für PostgreSQL
keywords: Azure, Java, SDK, API, SQL, Datenbank, PostGres, PostgreSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: postgresql
ms.openlocfilehash: d6fa2acb9a2f44b157ae52ba6e41f6777a43b574
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930976"
---
# <a name="azure-database-for-postgresql-libraries-for-java"></a><span data-ttu-id="a31de-104">Bibliotheken zu Azure-Datenbank für PostgreSQL für Java</span><span class="sxs-lookup"><span data-stu-id="a31de-104">Azure Database for PostgreSQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a31de-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="a31de-105">Overview</span></span>

<span data-ttu-id="a31de-106">[Azure-Datenbank für PostgreSQL](/azure/sql-database/sql-database-technical-overview) ist ein relationaler Datenbankdienst in Azure für Entwickler, der auf der Communityversion des Open Source-Datenbankmoduls für [PostgreSQL](https://www.postgresql.org/) basiert.</span><span class="sxs-lookup"><span data-stu-id="a31de-106">[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview) is a relational database service in Azure built for developers based on the community version of open source [PostgreSQL](https://www.postgresql.org/) database engine.</span></span>

<span data-ttu-id="a31de-107">Informationen zu den ersten Schritten mit Azure-Datenbank für PostgreSQL finden Sie unter [Verwenden von Java zum Verbinden und Abfragen von Daten](/azure/postgresql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="a31de-107">To get started with Azure Database for PostgreSQL, see [Use Java to connect and query data](/azure/postgresql/connect-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="a31de-108">Client-JDBC-Treiber</span><span class="sxs-lookup"><span data-stu-id="a31de-108">Client JDBC driver</span></span>

<span data-ttu-id="a31de-109">Stellen Sie in Ihren Anwendungen mit dem Open Source-[PostgreSQL-JDBC-Treiber](https://jdbc.postgresql.org/) eine Verbindung mit Azure-Datenbank für PostgreSQL her.</span><span class="sxs-lookup"><span data-stu-id="a31de-109">Connect to Azure Database for PostgreSQL from your applications using the open-source [PostgreSQL JDBC driver](https://jdbc.postgresql.org/).</span></span> <span data-ttu-id="a31de-110">Sie können mit der [Java-JDBC-API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) eine direkte Verbindung mit der Datenbank herstellen oder Datenzugriffsframeworks verwenden, die mit der Datenbank über JDBC (etwa [Hibernate](http://hibernate.org/)) interagieren.</span><span class="sxs-lookup"><span data-stu-id="a31de-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="a31de-111">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um den JDBC-Clienttreiber in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a31de-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="a31de-112">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a31de-112">Example</span></span>

<span data-ttu-id="a31de-113">Stellen Sie mit JDBC eine Verbindung mit Azure-Datenbank für PostgreSQL her, und wählen Sie alle Datensätze in der Vertriebstabelle aus.</span><span class="sxs-lookup"><span data-stu-id="a31de-113">Connect to Azure Database for PostgreSQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="a31de-114">Sie können die JDBC-Verbindungszeichenfolge für die Datenbank aus dem Azure-Portal abrufen.</span><span class="sxs-lookup"><span data-stu-id="a31de-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:postgresql://mypostgresdb.postgres.database.azure.com:5432/mydb?user=frank@mypostgresdb&password=AbCdEfGhIjK&ssl=true");
Connection connection = null;
try {
    connection = DriverManager.getConnection(url);
    String selectSql = "SELECT * FROM SALES";
    Statement statement = connection.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="a31de-115">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a31de-115">Samples</span></span>

[<span data-ttu-id="a31de-116">Entwerfen Ihrer ersten Azure-Datenbank für PostgreSQL mithilfe der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a31de-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

<span data-ttu-id="a31de-117">Sehen Sie sich weitere [Java-Codebeispiele für Azure-Datenbank für PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="a31de-117">Explore more [sample Java code for Azure Database for PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) you can use in your apps.</span></span>
