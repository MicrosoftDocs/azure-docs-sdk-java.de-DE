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
# <a name="azure-database-for-postgresql-libraries-for-java"></a>Bibliotheken zu Azure-Datenbank für PostgreSQL für Java

## <a name="overview"></a>Übersicht

[Azure-Datenbank für PostgreSQL](/azure/sql-database/sql-database-technical-overview) ist ein relationaler Datenbankdienst in Azure für Entwickler, der auf der Communityversion des Open Source-Datenbankmoduls für [PostgreSQL](https://www.postgresql.org/) basiert.

Informationen zu den ersten Schritten mit Azure-Datenbank für PostgreSQL finden Sie unter [Verwenden von Java zum Verbinden und Abfragen von Daten](/azure/postgresql/connect-java).

## <a name="client-jdbc-driver"></a>Client-JDBC-Treiber

Stellen Sie in Ihren Anwendungen mit dem Open Source-[PostgreSQL-JDBC-Treiber](https://jdbc.postgresql.org/) eine Verbindung mit Azure-Datenbank für PostgreSQL her. Sie können mit der [Java-JDBC-API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) eine direkte Verbindung mit der Datenbank herstellen oder Datenzugriffsframeworks verwenden, die mit der Datenbank über JDBC (etwa [Hibernate](http://hibernate.org/)) interagieren.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um den JDBC-Clienttreiber in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a>Beispiel

Stellen Sie mit JDBC eine Verbindung mit Azure-Datenbank für PostgreSQL her, und wählen Sie alle Datensätze in der Vertriebstabelle aus. Sie können die JDBC-Verbindungszeichenfolge für die Datenbank aus dem Azure-Portal abrufen.

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

## <a name="samples"></a>Beispiele

[Entwerfen Ihrer ersten Azure-Datenbank für PostgreSQL mithilfe der Azure CLI](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

Sehen Sie sich weitere [Java-Codebeispiele für Azure-Datenbank für PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) an, die Sie in Ihren Apps verwenden können.
