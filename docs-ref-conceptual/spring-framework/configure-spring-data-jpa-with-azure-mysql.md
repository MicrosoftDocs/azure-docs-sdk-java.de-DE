---
title: Verwenden der Spring Data-JPA mit Azure MySQL
description: Erfahren Sie, wie Sie die Spring Data-JPA (Java-Persistenz-API) mit einer Azure MySQL-Datenbank verwenden.
services: mysql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: mysql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 95dfc292d8f6d7e03d396afd7da4cfff0bd05b1b
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992412"
---
# <a name="how-to-use-spring-data-jpa-with-azure-mysql"></a>Verwenden der Spring Data-JPA mit Azure MySQL

## <a name="overview"></a>Übersicht

In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen in einer Azure [MySQL](https://www.mysql.com/)-Datenbank mithilfe der [Java-Persistenz-API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm) zu speichern und abzurufen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher
* [cURL](https://curl.haxx.se/) oder ein ähnliches HTTP-Hilfsprogramm zum Testen der Funktionalität
* Das Befehlszeilenprogramm [mysql](https://dev.mysql.com/downloads/)
* Einen [Git-Client](https://git-scm.com/downloads)

## <a name="create-a-mysql-database-for-azure"></a>Erstellen einer MySQL-Datenbank für Azure

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a>Erstellen eines MySQL-Datenbankservers im Azure-Portal

> [!NOTE]
> 
> Ausführlichere Informationen zum Erstellen von MySQL-Datenbanken finden Sie unter [Erstellen eines Azure Database for MySQL-Servers im Azure-Portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **Azure Database for MySQL**.

   ![Erstellen einer MySQL-Datenbank][MYSQL01]

1. Geben Sie Folgendes ein:

   - **Servername**: Wählen Sie einen eindeutigen Namen für Ihren MySQL-Server aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoysmysql.mysql.database.azure.com*) verwendet.
   - **Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.
   - **Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.
   - **Quelle auswählen**: Wählen Sie für dieses Tutorial `Blank` aus, um eine neue Datenbank zu erstellen.
   - **Serveradministratoranmeldung**: Geben Sie den Namen des Datenbankadministrators an.
   - **Kennwort** und **Kennwort bestätigen**: Geben Sie das Kennwort für den Datenbankadministrator an.
   - **Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.
   - **Version**: Geben Sie aktuelle Datenbankversion an.
   - **Tarif**: Geben Sie für dieses Tutorial den kostengünstigsten Tarif an.

   ![Festlegen der Eigenschaften der MySQL-Datenbank][MYSQL02]

1. Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Erstellen**.

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a>Konfigurieren einer Firewallregel für den MySQL-Datenbankserver im Azure-Portal

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **Alle Ressourcen** und anschließend auf die MySQL-Datenbank, die Sie gerade erstellt haben.

   ![Auswählen der MySQL-Datenbank][MYSQL03]

1. Klicken Sie auf **Verbindungssicherheit**, und erstellen Sie im Abschnitt **Firewallregeln** eine neue Regel, indem Sie einen eindeutigen Namen für die Regel angeben, den Bereich der IP-Adressen eingeben, die Zugriff auf Ihre Datenbank benötigen, und anschließend auf **Speichern** klicken.

   ![Konfigurieren der Verbindungssicherheit][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a>Abrufen der Verbindungszeichenfolge für den MySQL-Server im Azure-Portal

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **Alle Ressourcen** und anschließend auf die MySQL-Datenbank, die Sie gerade erstellt haben.

   ![Auswählen der MySQL-Datenbank][MYSQL03]

1. Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie den Wert im Textfeld **JDBC**.

   ![Abrufen der JDBC-Verbindungszeichenfolge][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a>Erstellen der MySQL-Datenbank mit dem Befehlszeilenprogramm `mysql`

1. Öffnen Sie eine Befehlsshell, und stellen Sie wie im folgenden Beispiel gezeigt eine Verbindung mit Ihrem MySQL-Server her, indem Sie einen `mysql`-Befehl eingeben:

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `host` | Der vollqualifizierte MySQL-Servername, den Sie weiter oben in diesem Artikel festgelegt haben |
   | `user` | Der MySQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen |
   | `p` | Gibt an, dass auf eine Aufforderung zur Kennworteingabe gewartet werden soll |


   Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:

   ```shell
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 64552
   Server version: 5.6.39.0 MySQL Community Server (GPL)
   
   Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   
   mysql>
   ```

1. Erstellen Sie eine Datenbank mit dem Namen *mysqldb*, indem Sie wie im folgenden Beispiel gezeigt einen `mysql`-Befehl eingeben:

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. OPTIONAL: Sie können überprüfen, ob Ihre Datenbank erstellt wurde, indem Sie wie im folgenden Beispiel gezeigt einen `mysql`-Befehl eingeben:

   ```SQL
   SHOW DATABASES;
   ```

   Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:

   ```shell
   +--------------------+
   | Database           |
   +--------------------+
   | information_schema |
   | mysql              |
   | mysqldb            |
   | performance_schema |
   | sys                |
   +--------------------+
   ```

1. Geben Sie `\q` ein, um das Befehlszeilenprogramm `mysql` zu beenden.

## <a name="configure-the-sample-application"></a>Konfigurieren der Beispielanwendung

1. Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. Suchen Sie im Verzeichnis *resources* des Beispielprojekts nach der Datei *application.properties*, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.

1. Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu, bzw. konfigurieren Sie diese Zeilen. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:

   ```yaml
   spring.jpa.database-platform=org.hibernate.dialect.MySQL5InnoDBDialect
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `spring.jpa.database-platform` | Die JPA-Datenbankplattform |
   | `spring.datasource.url` | Die MySQL-JDBC-Zeichenfolge, die Sie weiter oben in diesem Artikel kopiert haben |
   | `spring.datasource.username` | Der MySQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen |
   | `spring.datasource.password` | Das MySQL-Administratorkennwort, das Sie weiter oben in diesem Artikel festgelegt haben |

1. Speichern und schließen Sie die Datei *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Verpacken und Testen der Beispielanwendung 

1. Erstellen Sie die Beispielanwendung mit Maven. Beispiel:

   ```shell
   mvn clean package -P mysql
   ```

1. Starten Sie die Beispielanwendung. Beispiel:

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. Erstellen Sie wie in den folgenden Beispielen dargestellt über eine Eingabeaufforderung mit `curl` neue Datensätze:

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. Rufen Sie wie im folgenden Beispiel dargestellt über eine Eingabeaufforderung mit `curl` alle vorhandenen Datensätze ab:

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen in einer Azure MySQL-Datenbank mithilfe der Java-Persistenz-API (JPA) zu speichern und abzurufen.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.

> [!div class="nextstepaction"]
> [Spring Framework in Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Weitere Ressourcen

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).

<!-- URL List -->

[Azure für Java-Entwickler]: /java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Arbeiten mit Azure DevOps und Java)
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[MYSQL01]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-05.png
