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
# <a name="how-to-use-spring-data-jpa-with-azure-postgresql"></a><span data-ttu-id="e51ed-103">Verwenden der Spring Data-JPA mit Azure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e51ed-103">How to use Spring Data JPA with Azure PostgreSQL</span></span>

## <a name="overview"></a><span data-ttu-id="e51ed-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="e51ed-104">Overview</span></span>

<span data-ttu-id="e51ed-105">In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen in einer Azure [PostgreSQL]https://www.postgresql.org/-Datenbank mithilfe der [Java-Persistenz-API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="e51ed-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [PostgreSQL]https://www.postgresql.org/ database using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e51ed-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="e51ed-106">Prerequisites</span></span>

<span data-ttu-id="e51ed-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="e51ed-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="e51ed-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="e51ed-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e51ed-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="e51ed-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="e51ed-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="e51ed-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="e51ed-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="e51ed-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="e51ed-112">[cURL](https://curl.haxx.se/) oder</span><span class="sxs-lookup"><span data-stu-id="e51ed-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span> <span data-ttu-id="e51ed-113">ein ähnliches HTTP-Hilfsprogramm zum Testen der Funktionalität</span><span class="sxs-lookup"><span data-stu-id="e51ed-113">or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="e51ed-114">Das Befehlszeilenprogramm [psql](https://www.postgresql.org/docs/current/app-psql.html)</span><span class="sxs-lookup"><span data-stu-id="e51ed-114">The [psql](https://www.postgresql.org/docs/current/app-psql.html) command-line utility.</span></span>
* <span data-ttu-id="e51ed-115">Einen [Git-Client](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="e51ed-115">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-postgresql-database-for-azure"></a><span data-ttu-id="e51ed-116">Erstellen einer PostgreSQL-Datenbank für Azure</span><span class="sxs-lookup"><span data-stu-id="e51ed-116">Create a PostgreSQL database for Azure</span></span>

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="e51ed-117">Erstellen eines PostgreSQL-Datenbankservers im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="e51ed-117">Create a PostgreSQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="e51ed-118">Ausführlichere Informationen zum Erstellen von PostgreSQL-Datenbanken finden Sie unter [Erstellen eines Azure Database for PostgreSQL-Servers im Azure-Portal](/azure/postgresql/quickstart-create-server-database-portal).</span><span class="sxs-lookup"><span data-stu-id="e51ed-118">You can read more detailed information about creating PostgreSQL databases in [Create an Azure Database for PostgreSQL server by using the Azure portal](/azure/postgresql/quickstart-create-server-database-portal).</span></span>

1. <span data-ttu-id="e51ed-119">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="e51ed-119">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="e51ed-120">Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **Azure Database for PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="e51ed-120">Click **+Create a resource**, then **Databases**, and then click **Azure Database for PostgreSQL**.</span></span>

   ![Erstellen einer PostgreSQL-Datenbank][POSTGRESQL01]

1. <span data-ttu-id="e51ed-122">Geben Sie Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="e51ed-122">Enter the following information:</span></span>

   - <span data-ttu-id="e51ed-123">**Servername**: Wählen Sie einen eindeutigen Namen für Ihren PostgreSQL-Server aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoyspostgresql.postgres.database.azure.com*) verwendet.</span><span class="sxs-lookup"><span data-stu-id="e51ed-123">**Server name**: Choose a unique name for your PostgreSQL server; this will be used to create a fully-qualified domain name like *wingtiptoyspostgresql.postgres.database.azure.com*.</span></span>
   - <span data-ttu-id="e51ed-124">**Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="e51ed-124">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="e51ed-125">**Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="e51ed-125">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="e51ed-126">**Quelle auswählen**: Wählen Sie für dieses Tutorial `Blank` aus, um eine neue Datenbank zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e51ed-126">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="e51ed-127">**Serveradministratoranmeldung**: Geben Sie den Namen des Datenbankadministrators an.</span><span class="sxs-lookup"><span data-stu-id="e51ed-127">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="e51ed-128">**Kennwort** und **Kennwort bestätigen**: Geben Sie das Kennwort für den Datenbankadministrator an.</span><span class="sxs-lookup"><span data-stu-id="e51ed-128">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="e51ed-129">**Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="e51ed-129">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="e51ed-130">**Version**: Geben Sie aktuelle Datenbankversion an.</span><span class="sxs-lookup"><span data-stu-id="e51ed-130">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="e51ed-131">**Tarif**: Geben Sie für dieses Tutorial den kostengünstigsten Tarif an.</span><span class="sxs-lookup"><span data-stu-id="e51ed-131">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Festlegen der Eigenschaften der PostgreSQL-Datenbank][POSTGRESQL02]

1. <span data-ttu-id="e51ed-133">Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e51ed-133">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="e51ed-134">Konfigurieren einer Firewallregel für den PostgreSQL-Datenbankserver im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="e51ed-134">Configure a firewall rule for your PostgreSQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="e51ed-135">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="e51ed-135">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="e51ed-136">Klicken Sie auf **Alle Ressourcen** und anschließend auf die PostgreSQL-Datenbank, die Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="e51ed-136">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Auswählen der PostgreSQL-Datenbank][POSTGRESQL03]

1. <span data-ttu-id="e51ed-138">Klicken Sie auf **Verbindungssicherheit**, und erstellen Sie im Abschnitt **Firewallregeln** eine neue Regel, indem Sie einen eindeutigen Namen für die Regel angeben, den Bereich der IP-Adressen eingeben, die Zugriff auf Ihre Datenbank benötigen, und anschließend auf **Speichern** klicken.</span><span class="sxs-lookup"><span data-stu-id="e51ed-138">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Konfigurieren der Verbindungssicherheit][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a><span data-ttu-id="e51ed-140">Abrufen der Verbindungszeichenfolge für den PostgreSQL-Server im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="e51ed-140">Retrieve the connection string for your PostgreSQL server using the Azure Portal</span></span>

1. <span data-ttu-id="e51ed-141">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="e51ed-141">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="e51ed-142">Klicken Sie auf **Alle Ressourcen** und anschließend auf die PostgreSQL-Datenbank, die Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="e51ed-142">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Auswählen der PostgreSQL-Datenbank][POSTGRESQL03]

1. <span data-ttu-id="e51ed-144">Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie den Wert im Textfeld **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="e51ed-144">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Abrufen der JDBC-Verbindungszeichenfolge][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a><span data-ttu-id="e51ed-146">Erstellen der PostgreSQL-Datenbank mit dem Befehlszeilenprogramm `psql`</span><span class="sxs-lookup"><span data-stu-id="e51ed-146">Create PostgreSQL database using the `psql` command-line utility</span></span>

1. <span data-ttu-id="e51ed-147">Öffnen Sie eine Befehlsshell, und stellen Sie wie im folgenden Beispiel gezeigt eine Verbindung mit Ihrem PostgreSQL-Server her, indem Sie einen `psql`-Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="e51ed-147">Open a command shell and connect to your PostgreSQL server by entering a `psql` command like the following example:</span></span>

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   <span data-ttu-id="e51ed-148">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="e51ed-148">Where:</span></span>

   | <span data-ttu-id="e51ed-149">Parameter</span><span class="sxs-lookup"><span data-stu-id="e51ed-149">Parameter</span></span> | <span data-ttu-id="e51ed-150">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="e51ed-150">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="e51ed-151">Der vollqualifizierte PostgreSQL-Servername, den Sie weiter oben in diesem Artikel festgelegt haben</span><span class="sxs-lookup"><span data-stu-id="e51ed-151">Specifies your fully qualified PostgreSQL server name from earlier in this article.</span></span> |
   | `host` | <span data-ttu-id="e51ed-152">Der PostgreSQL-Serverport (Standardwert: `5432`)</span><span class="sxs-lookup"><span data-stu-id="e51ed-152">Specifies the PostgreSQL server port, which is `5432` by default.</span></span> |
   | `username` | <span data-ttu-id="e51ed-153">Der PostgreSQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen</span><span class="sxs-lookup"><span data-stu-id="e51ed-153">Specifies your PostgreSQL administrator and shortened server name from earlier in this article.</span></span> |
   | `dbname` | <span data-ttu-id="e51ed-154">Gibt an, dass Sie vorerst die `postgres`-Standarddatenbank verwenden möchten</span><span class="sxs-lookup"><span data-stu-id="e51ed-154">Specifies that you want to use the default `postgres` database for now.</span></span> |

   <span data-ttu-id="e51ed-155">Ihr PostgreSQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="e51ed-155">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. <span data-ttu-id="e51ed-156">Erstellen Sie eine Datenbank mit dem Namen *mypgsqldb*, indem Sie wie im folgenden Beispiel gezeigt einen `psql`-Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="e51ed-156">Create a database named *mypgsqldb* by entering a `psql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   <span data-ttu-id="e51ed-157">Ihr PostgreSQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="e51ed-157">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   CREATE DATABASE
   ```

1. <span data-ttu-id="e51ed-158">OPTIONAL: Sie können überprüfen, ob die Datenbank erstellt wurde, indem Sie `\l` im Befehlszeilenprogramm `psql` eingeben. Ihr PostgreSQL-Server sollte mit einer Ausgabe antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="e51ed-158">OPTIONAL: You can verify that your database was created by entering a `\l` at the `psql`; your PostgreSQL server should respond with something like the following example:</span></span>

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

1. <span data-ttu-id="e51ed-159">Geben Sie `\q` ein, um das Befehlszeilenprogramm `psql` zu beenden.</span><span class="sxs-lookup"><span data-stu-id="e51ed-159">Enter `\q` to exit the `psql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="e51ed-160">Konfigurieren der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="e51ed-160">Configure the sample application</span></span>

1. <span data-ttu-id="e51ed-161">Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:</span><span class="sxs-lookup"><span data-stu-id="e51ed-161">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. <span data-ttu-id="e51ed-162">Suchen Sie im Verzeichnis *resources* des Beispielprojekts nach der Datei *application.properties*, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="e51ed-162">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="e51ed-163">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu, bzw. konfigurieren Sie diese Zeilen. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:</span><span class="sxs-lookup"><span data-stu-id="e51ed-163">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   <span data-ttu-id="e51ed-164">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="e51ed-164">Where:</span></span>

   | <span data-ttu-id="e51ed-165">Parameter</span><span class="sxs-lookup"><span data-stu-id="e51ed-165">Parameter</span></span> | <span data-ttu-id="e51ed-166">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="e51ed-166">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="e51ed-167">Die PostgreSQL-JDBC-Zeichenfolge, die Sie weiter oben in diesem Artikel kopiert haben</span><span class="sxs-lookup"><span data-stu-id="e51ed-167">Specifies your PostgreSQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="e51ed-168">Der PostgreSQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen</span><span class="sxs-lookup"><span data-stu-id="e51ed-168">Specifies your PostgreSQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="e51ed-169">Das PostgreSQL-Administratorkennwort, das Sie weiter oben in diesem Artikel festgelegt haben</span><span class="sxs-lookup"><span data-stu-id="e51ed-169">Specifies your PostgreSQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="e51ed-170">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="e51ed-170">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="e51ed-171">Verpacken und Testen der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="e51ed-171">Package and test the sample application</span></span> 

1. <span data-ttu-id="e51ed-172">Erstellen Sie die Beispielanwendung mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="e51ed-172">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P postgresql
   ```

1. <span data-ttu-id="e51ed-173">Starten Sie die Beispielanwendung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="e51ed-173">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="e51ed-174">Erstellen Sie wie in den folgenden Beispielen dargestellt über eine Eingabeaufforderung mit `curl` neue Datensätze:</span><span class="sxs-lookup"><span data-stu-id="e51ed-174">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="e51ed-175">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="e51ed-175">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="e51ed-176">Rufen Sie wie im folgenden Beispiel dargestellt über eine Eingabeaufforderung mit `curl` alle vorhandenen Datensätze ab:</span><span class="sxs-lookup"><span data-stu-id="e51ed-176">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="e51ed-177">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="e51ed-177">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="e51ed-178">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="e51ed-178">Summary</span></span>

<span data-ttu-id="e51ed-179">In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen in einer Azure PostgreSQL-Datenbank mithilfe der Java-Persistenz-API (JPA) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="e51ed-179">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure PostgreSQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e51ed-180">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="e51ed-180">Next steps</span></span>

<span data-ttu-id="e51ed-181">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="e51ed-181">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e51ed-182">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="e51ed-182">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="e51ed-183">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="e51ed-183">Additional Resources</span></span>

<span data-ttu-id="e51ed-184">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="e51ed-184">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Azure für Java-Entwickler]: /java/azure/
[Azure for Java Developers]: /java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Arbeiten mit Azure DevOps und Java)
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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