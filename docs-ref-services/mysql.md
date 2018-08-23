---
title: Bibliotheken zu Azure-Datenbank für MySQL für Java
description: Referenzdokumentation für die Java-Clientbibliotheken für Azure-Datenbank für MySQL
keywords: Azure, Java, SDK, API, SQL, Datenbank, PostGres, MySQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.devlang: java
ms.service: mysql
ms.openlocfilehash: f3c0b84a8c6577e5a844c4084b3d9cfaf3a52323
ms.sourcegitcommit: 1b22376e4ceb3d2f2734c8fc80823a44cc5fe8fb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2018
ms.locfileid: "42703365"
---
# <a name="azure-database-for-mysql-libraries-for-java"></a>Bibliotheken zu Azure-Datenbank für MySQL für Java

## <a name="overview"></a>Übersicht

[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview) ist ein relationaler Datenbankdienst, der auf der Open Source-Engine für [MySQL](https://www.mysql.com/) Server basiert. 

Informationen zu den ersten Schritten mit Azure-Datenbank für MySQL finden Sie unter [Azure-Datenbank für MySQL: Verwenden von Java zum Verbinden und Abfragen von Daten](/azure/mysql/connect-java).

## <a name="client-jbdc-driver"></a>JBDC-Clienttreiber

Stellen Sie in Ihren Anwendungen mit dem Open Source-[MySQL-JDBC-Treiber](https://dev.mysql.com/downloads/connector/j/) eine Verbindung mit Azure-Datenbank für MySQL her. Sie können mit der [Java-JDBC-API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) eine direkte Verbindung mit der Datenbank herstellen oder Datenzugriffsframeworks verwenden, die mit der Datenbank über JDBC (etwa [Hibernate](http://hibernate.org/)) interagieren.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um den JDBC-Clienttreiber in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a>Beispiel

Stellen Sie mithilfe von JDBC eine Verbindung mit Azure-Datenbank für MySQL her, und wählen Sie alle Datensätze in der Vertriebstabelle aus. Sie können die JDBC-Verbindungszeichenfolge für die Datenbank aus dem Azure-Portal abrufen.

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a>Beispiele

[Erstellen einer Java- und MySQL-Web-App](/azure/app-service-web/app-service-web-tutorial-java-mysql)   
[Entwerfen Ihrer ersten Azure-Datenbank für MySQL](/azure/mysql/tutorial-design-database-using-cli)   

Sehen Sie sich weitere [Java-Codebeispiele für Azure-Datenbank für MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) an, die Sie in Ihren Apps verwenden können.
