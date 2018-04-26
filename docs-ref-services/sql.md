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
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="azure-sql-database-libraries-for-java"></a>Azure SQL-Datenbank-Bibliotheken für Java

## <a name="overview"></a>Übersicht

[Azure SQL-Datenbank](/azure/sql-database/sql-database-technical-overview) ist ein relationaler Datenbankdienst und verwendet die Microsoft SQL Server-Engine, das sowohl Tabellen-, JSON- und XML-Daten als auch räumliche Daten unterstützt. 

Informationen zu den ersten Schritten mit Azure SQL-Datenbank finden Sie unter [Abfragen einer Azure SQL-Datenbank mithilfe von Java](/azure/sql-database/sql-database-connect-query-java).

## <a name="client-jdbc-driver"></a>Client-JDBC-Treiber

Stellen Sie in Ihren Anwendungen mithilfe des [SQL-Datenbank-JDBC-Treibers](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) eine Verbindung mit Azure SQL-Datenbank her. Sie können mit der [Java-JDBC-API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) eine direkte Verbindung mit der Datenbank herstellen oder Datenzugriffsframeworks verwenden, die mit der Datenbank über JDBC interagieren (beispielsweise [Hibernate](http://hibernate.org/)).

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um den JDBC-Clienttreiber in Ihrem Projekt zu verwenden.


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Stellen Sie mithilfe von JDBC eine Verbindung mit SQL-Datenbank her, und wählen Sie alle Datensätze in einer Tabelle aus.

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a>Verwaltungs-API

Über die Verwaltungs-API können Sie Azure SQL-Datenbank-Ressourcen in Ihrem Abonnement erstellen und verwalten.   

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/sql/management)

### <a name="example"></a>Beispiel

Erstellen Sie eine SQL-Datenbank-Ressource, und schränken Sie den Zugriff mithilfe einer Firewallregel auf einen bestimmten IP-Adressbereich ein.

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a>Beispiele

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

Sehen Sie sich weitere [Java-Codebeispiele für Azure SQL-Datenbank](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) an, die Sie in Ihren Apps verwenden können.