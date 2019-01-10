---
title: Verwenden der Spring Data-JPA mit Azure PostgreSQL
description: Erfahren Sie, wie Sie die Spring Data-JPA (Java-Persistenz-API) mit einer Azure PostgreSQL-Datenbank verwenden.
services: postgresql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: postgresql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 1849e03674534882a579f85b2654a628bd867487
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992341"
---
# <a name="how-to-use-spring-data-jpa-with-azure-postgresql"></a>Verwenden der Spring Data-JPA mit Azure PostgreSQL

## <a name="overview"></a>Übersicht

In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen in einer Azure [PostgreSQL]https://www.postgresql.org/-Datenbank mithilfe der [Java-Persistenz-API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm) zu speichern und abzurufen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher
* [cURL](https://curl.haxx.se/) oder ein ähnliches HTTP-Hilfsprogramm zum Testen der Funktionalität
* Das Befehlszeilenprogramm [psql](https://www.postgresql.org/docs/current/app-psql.html)
* Einen [Git-Client](https://git-scm.com/downloads)

## <a name="create-a-postgresql-database-for-azure"></a>Erstellen einer PostgreSQL-Datenbank für Azure

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a>Erstellen eines PostgreSQL-Datenbankservers im Azure-Portal

> [!NOTE]
> 
> Ausführlichere Informationen zum Erstellen von PostgreSQL-Datenbanken finden Sie unter [Erstellen eines Azure Database for PostgreSQL-Servers im Azure-Portal](/azure/postgresql/quickstart-create-server-database-portal).

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **Azure Database for PostgreSQL**.

   ![Erstellen einer PostgreSQL-Datenbank][POSTGRESQL01]

1. Geben Sie Folgendes ein:

   - **Servername**: Wählen Sie einen eindeutigen Namen für Ihren PostgreSQL-Server aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoyspostgresql.postgres.database.azure.com*) verwendet.
   - **Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.
   - **Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.
   - **Quelle auswählen**: Wählen Sie für dieses Tutorial `Blank` aus, um eine neue Datenbank zu erstellen.
   - **Serveradministratoranmeldung**: Geben Sie den Namen des Datenbankadministrators an.
   - **Kennwort** und **Kennwort bestätigen**: Geben Sie das Kennwort für den Datenbankadministrator an.
   - **Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.
   - **Version**: Geben Sie aktuelle Datenbankversion an.
   - **Tarif**: Geben Sie für dieses Tutorial den kostengünstigsten Tarif an.

   ![Festlegen der Eigenschaften der PostgreSQL-Datenbank][POSTGRESQL02]

1. Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Erstellen**.

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a>Konfigurieren einer Firewallregel für den PostgreSQL-Datenbankserver im Azure-Portal

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **Alle Ressourcen** und anschließend auf die PostgreSQL-Datenbank, die Sie gerade erstellt haben.

   ![Auswählen der PostgreSQL-Datenbank][POSTGRESQL03]

1. Klicken Sie auf **Verbindungssicherheit**, und erstellen Sie im Abschnitt **Firewallregeln** eine neue Regel, indem Sie einen eindeutigen Namen für die Regel angeben, den Bereich der IP-Adressen eingeben, die Zugriff auf Ihre Datenbank benötigen, und anschließend auf **Speichern** klicken.

   ![Konfigurieren der Verbindungssicherheit][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a>Abrufen der Verbindungszeichenfolge für den PostgreSQL-Server im Azure-Portal

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **Alle Ressourcen** und anschließend auf die PostgreSQL-Datenbank, die Sie gerade erstellt haben.

   ![Auswählen der PostgreSQL-Datenbank][POSTGRESQL03]

1. Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie den Wert im Textfeld **JDBC**.

   ![Abrufen der JDBC-Verbindungszeichenfolge][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a>Erstellen der PostgreSQL-Datenbank mit dem Befehlszeilenprogramm `psql`

1. Öffnen Sie eine Befehlsshell, und stellen Sie wie im folgenden Beispiel gezeigt eine Verbindung mit Ihrem PostgreSQL-Server her, indem Sie einen `psql`-Befehl eingeben:

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `host` | Der vollqualifizierte PostgreSQL-Servername, den Sie weiter oben in diesem Artikel festgelegt haben |
   | `host` | Der PostgreSQL-Serverport (Standardwert: `5432`) |
   | `username` | Der PostgreSQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen |
   | `dbname` | Gibt an, dass Sie vorerst die `postgres`-Standarddatenbank verwenden möchten |

   Ihr PostgreSQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. Erstellen Sie eine Datenbank mit dem Namen *mypgsqldb*, indem Sie wie im folgenden Beispiel gezeigt einen `psql`-Befehl eingeben:

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   Ihr PostgreSQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:

   ```shell
   CREATE DATABASE
   ```

1. OPTIONAL: Sie können überprüfen, ob die Datenbank erstellt wurde, indem Sie `\l` im Befehlszeilenprogramm `psql` eingeben. Ihr PostgreSQL-Server sollte mit einer Ausgabe antworten, die dem folgenden Beispiel ähnelt:

   ```shell
                   List of databases
          Name        |      Owner      | Encoding
   -------------------+-----------------+----------
    azure_maintenance | azure_superuser | UTF8
    azure_sys         | azure_superuser | UTF8
    mypgsqldb         | wingtiptoysuser | UTF8
    postgres          | azure_superuser | UTF8
    template0         | azure_superuser | UTF8
    template1         | azure_superuser | UTF8
   (6 rows)
   ```

1. Geben Sie `\q` ein, um das Befehlszeilenprogramm `psql` zu beenden.

## <a name="configure-the-sample-application"></a>Konfigurieren der Beispielanwendung

1. Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. Suchen Sie im Verzeichnis *resources* des Beispielprojekts nach der Datei *application.properties*, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.

1. Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu, bzw. konfigurieren Sie diese Zeilen. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `spring.datasource.url` | Die PostgreSQL-JDBC-Zeichenfolge, die Sie weiter oben in diesem Artikel kopiert haben |
   | `spring.datasource.username` | Der PostgreSQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen |
   | `spring.datasource.password` | Das PostgreSQL-Administratorkennwort, das Sie weiter oben in diesem Artikel festgelegt haben |

1. Speichern und schließen Sie die Datei *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Verpacken und Testen der Beispielanwendung 

1. Erstellen Sie die Beispielanwendung mit Maven. Beispiel:

   ```shell
   mvn clean package -P postgresql
   ```

1. Starten Sie die Beispielanwendung. Beispiel:

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
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

In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen in einer Azure PostgreSQL-Datenbank mithilfe der Java-Persistenz-API (JPA) zu speichern und abzurufen.

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

[POSTGRESQL01]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-05.png
