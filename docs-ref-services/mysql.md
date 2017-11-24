---
title: "Bibliotheken zu Azure-Datenbank für MySQL für Java"
description: "Referenzdokumentation für die Java-Clientbibliotheken für Azure-Datenbank für MySQL"
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
---
# <a name="azure-database-for-mysql-libraries-for-java"></a>Bibliotheken zu Azure-Datenbank für MySQL für Java

## <a name="overview"></a>Übersicht

[Azure-Datenbank für MySQL](/azure/sql-database/sql-database-technical-overview) ist ein relationaler Datenbankdienst, der auf dem Open Source-Modul für [MySQL](https://www.mysql.com/) Server basiert. 

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
