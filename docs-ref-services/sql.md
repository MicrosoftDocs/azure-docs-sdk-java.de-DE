---
title: Azure SQL-Datenbank-Bibliotheken für Java
description: Stellen Sie über den JDBC-Treiber eine Verbindung mit Azure SQL-Datenbank her, oder verwalten Sie Instanzen von Azure SQL-Datenbank über die Verwaltungs-API.
keywords: Azure, Java, SDK, API, SQL, Datenbank, JDBC
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/05/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: sql-database
ms.openlocfilehash: 37f7d3caf10e6b709cee2452c63a543d49e0ead8
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893311"
---
# <a name="azure-sql-database-libraries-for-java"></a><span data-ttu-id="8fcad-104">Azure SQL-Datenbank-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="8fcad-104">Azure SQL Database libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="8fcad-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="8fcad-105">Overview</span></span>

<span data-ttu-id="8fcad-106">[Azure SQL-Datenbank](/azure/sql-database/sql-database-technical-overview) ist ein relationaler Datenbankdienst und verwendet die Microsoft SQL Server-Engine, das sowohl Tabellen-, JSON- und XML-Daten als auch räumliche Daten unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8fcad-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) is a relational database service using the Microsoft SQL Server engine that supports table, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="8fcad-107">Informationen zu den ersten Schritten mit Azure SQL-Datenbank finden Sie unter [Abfragen einer Azure SQL-Datenbank mithilfe von Java](/azure/sql-database/sql-database-connect-query-java).</span><span class="sxs-lookup"><span data-stu-id="8fcad-107">To get started with Azure SQL Database, see [Azure SQL Database: Use Java to connect and query data](/azure/sql-database/sql-database-connect-query-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="8fcad-108">Client-JDBC-Treiber</span><span class="sxs-lookup"><span data-stu-id="8fcad-108">Client JDBC driver</span></span>

<span data-ttu-id="8fcad-109">Stellen Sie in Ihren Anwendungen mithilfe des [SQL-Datenbank-JDBC-Treibers](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) eine Verbindung mit Azure SQL-Datenbank her.</span><span class="sxs-lookup"><span data-stu-id="8fcad-109">Connect to Azure SQL Database from your applications using the [SQL Database JDBC driver](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span></span> <span data-ttu-id="8fcad-110">Sie können mit der [Java-JDBC-API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) eine direkte Verbindung mit der Datenbank herstellen oder Datenzugriffsframeworks verwenden, die mit der Datenbank über JDBC interagieren (beispielsweise [Hibernate](http://hibernate.org/)).</span><span class="sxs-lookup"><span data-stu-id="8fcad-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect with the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="8fcad-111">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um den JDBC-Clienttreiber in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="8fcad-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="8fcad-112">Beispiel</span><span class="sxs-lookup"><span data-stu-id="8fcad-112">Example</span></span>

<span data-ttu-id="8fcad-113">Stellen Sie mithilfe von JDBC eine Verbindung mit SQL-Datenbank her, und wählen Sie alle Datensätze in einer Tabelle aus.</span><span class="sxs-lookup"><span data-stu-id="8fcad-113">Connect to SQL database and select all records in a table using JDBC.</span></span>

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a><span data-ttu-id="8fcad-114">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="8fcad-114">Management API</span></span>

<span data-ttu-id="8fcad-115">Über die Verwaltungs-API können Sie Azure SQL-Datenbank-Ressourcen in Ihrem Abonnement erstellen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="8fcad-115">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span>   

<span data-ttu-id="8fcad-116">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="8fcad-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8fcad-117">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="8fcad-117">Explore the Management APIs</span></span>](/java/api/overview/azure/sql/management)

### <a name="example"></a><span data-ttu-id="8fcad-118">Beispiel</span><span class="sxs-lookup"><span data-stu-id="8fcad-118">Example</span></span>

<span data-ttu-id="8fcad-119">Erstellen Sie eine SQL-Datenbank-Ressource, und schränken Sie den Zugriff mithilfe einer Firewallregel auf einen bestimmten IP-Adressbereich ein.</span><span class="sxs-lookup"><span data-stu-id="8fcad-119">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a><span data-ttu-id="8fcad-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="8fcad-120">Samples</span></span>

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

<span data-ttu-id="8fcad-121">Sehen Sie sich weitere [Java-Codebeispiele für Azure SQL-Datenbank](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="8fcad-121">Explore more [sample Java code for Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) you can use in your apps.</span></span>