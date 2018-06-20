---
title: Bibliotheken zu Azure-Datenbank für MySQL für Java
description: Referenzdokumentation für die Java-Clientbibliotheken für Azure-Datenbank für MySQL
keywords: Azure, Java, SDK, API, SQL, Datenbank, PostGres, MySQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: mysql
ms.openlocfilehash: 72c94ef4bdad7adeae63da2efda93b52a9afef53
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931016"
---
# <a name="azure-database-for-mysql-libraries-for-java"></a><span data-ttu-id="58cf7-104">Bibliotheken zu Azure-Datenbank für MySQL für Java</span><span class="sxs-lookup"><span data-stu-id="58cf7-104">Azure Database for MySQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="58cf7-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="58cf7-105">Overview</span></span>

<span data-ttu-id="58cf7-106">[Azure-Datenbank für MySQL](/azure/sql-database/sql-database-technical-overview) ist ein relationaler Datenbankdienst, der auf dem Open Source-Modul für [MySQL](https://www.mysql.com/) Server basiert.</span><span class="sxs-lookup"><span data-stu-id="58cf7-106">[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview) is a relational database service based on the open source [MySQL](https://www.mysql.com/) Server engine.</span></span> 

<span data-ttu-id="58cf7-107">Informationen zu den ersten Schritten mit Azure-Datenbank für MySQL finden Sie unter [Azure-Datenbank für MySQL: Verwenden von Java zum Verbinden und Abfragen von Daten](/azure/mysql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="58cf7-107">To get started with Azure Database for MySQL, see [Use Java to connect and query data](/azure/mysql/connect-java).</span></span>

## <a name="client-jbdc-driver"></a><span data-ttu-id="58cf7-108">JBDC-Clienttreiber</span><span class="sxs-lookup"><span data-stu-id="58cf7-108">Client JBDC driver</span></span>

<span data-ttu-id="58cf7-109">Stellen Sie in Ihren Anwendungen mit dem Open Source-[MySQL-JDBC-Treiber](https://dev.mysql.com/downloads/connector/j/) eine Verbindung mit Azure-Datenbank für MySQL her.</span><span class="sxs-lookup"><span data-stu-id="58cf7-109">Connect to Azure Database for MySQL from your applications using the open-source [MySQL JDBC driver](https://dev.mysql.com/downloads/connector/j/).</span></span> <span data-ttu-id="58cf7-110">Sie können mit der [Java-JDBC-API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) eine direkte Verbindung mit der Datenbank herstellen oder Datenzugriffsframeworks verwenden, die mit der Datenbank über JDBC (etwa [Hibernate](http://hibernate.org/)) interagieren.</span><span class="sxs-lookup"><span data-stu-id="58cf7-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="58cf7-111">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um den JDBC-Clienttreiber in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="58cf7-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="58cf7-112">Beispiel</span><span class="sxs-lookup"><span data-stu-id="58cf7-112">Example</span></span>

<span data-ttu-id="58cf7-113">Stellen Sie mithilfe von JDBC eine Verbindung mit Azure-Datenbank für MySQL her, und wählen Sie alle Datensätze in der Vertriebstabelle aus.</span><span class="sxs-lookup"><span data-stu-id="58cf7-113">Connect to Azure Database for MySQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="58cf7-114">Sie können die JDBC-Verbindungszeichenfolge für die Datenbank aus dem Azure-Portal abrufen.</span><span class="sxs-lookup"><span data-stu-id="58cf7-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="58cf7-115">Beispiele</span><span class="sxs-lookup"><span data-stu-id="58cf7-115">Samples</span></span>

<span data-ttu-id="58cf7-116">[Erstellen einer Java- und MySQL-Web-App](/azure/app-service-web/app-service-web-tutorial-java-mysql) </span><span class="sxs-lookup"><span data-stu-id="58cf7-116">[Build a Java and MySQL web app](/azure/app-service-web/app-service-web-tutorial-java-mysql) </span></span>  
[<span data-ttu-id="58cf7-117">Entwerfen Ihrer ersten Azure-Datenbank für MySQL</span><span class="sxs-lookup"><span data-stu-id="58cf7-117">Design a MySQL database using the Azure CLI</span></span>](/azure/mysql/tutorial-design-database-using-cli)   

<span data-ttu-id="58cf7-118">Sehen Sie sich weitere [Java-Codebeispiele für Azure-Datenbank für MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="58cf7-118">Explore more [sample Java code for Azure Database for MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) you can use in your apps.</span></span>
