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
# <a name="how-to-use-spring-data-jpa-with-azure-mysql"></a><span data-ttu-id="322d8-103">Verwenden der Spring Data-JPA mit Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="322d8-103">How to use Spring Data JPA with Azure MySQL</span></span>

## <a name="overview"></a><span data-ttu-id="322d8-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="322d8-104">Overview</span></span>

<span data-ttu-id="322d8-105">In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen in einer Azure [MySQL](https://www.mysql.com/)-Datenbank mithilfe der [Java-Persistenz-API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="322d8-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [MySQL](https://www.mysql.com/) database using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="322d8-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="322d8-106">Prerequisites</span></span>

<span data-ttu-id="322d8-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="322d8-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="322d8-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="322d8-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="322d8-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="322d8-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="322d8-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="322d8-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="322d8-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="322d8-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="322d8-112">[cURL](https://curl.haxx.se/) oder ein ähnliches HTTP-Hilfsprogramm zum Testen der Funktionalität</span><span class="sxs-lookup"><span data-stu-id="322d8-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="322d8-113">Das Befehlszeilenprogramm [mysql](https://dev.mysql.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="322d8-113">The [mysql](https://dev.mysql.com/downloads/) command-line utility.</span></span>
* <span data-ttu-id="322d8-114">Einen [Git-Client](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="322d8-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-mysql-database-for-azure"></a><span data-ttu-id="322d8-115">Erstellen einer MySQL-Datenbank für Azure</span><span class="sxs-lookup"><span data-stu-id="322d8-115">Create a MySQL database for Azure</span></span>

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="322d8-116">Erstellen eines MySQL-Datenbankservers im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="322d8-116">Create a MySQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="322d8-117">Ausführlichere Informationen zum Erstellen von MySQL-Datenbanken finden Sie unter [Erstellen eines Azure Database for MySQL-Servers im Azure-Portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="322d8-117">You can read more detailed information about creating MySQL databases in [Create an Azure Database for MySQL server by using the Azure portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span></span>

1. <span data-ttu-id="322d8-118">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="322d8-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="322d8-119">Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **Azure Database for MySQL**.</span><span class="sxs-lookup"><span data-stu-id="322d8-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for MySQL**.</span></span>

   ![Erstellen einer MySQL-Datenbank][MYSQL01]

1. <span data-ttu-id="322d8-121">Geben Sie Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="322d8-121">Enter the following information:</span></span>

   - <span data-ttu-id="322d8-122">**Servername**: Wählen Sie einen eindeutigen Namen für Ihren MySQL-Server aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoysmysql.mysql.database.azure.com*) verwendet.</span><span class="sxs-lookup"><span data-stu-id="322d8-122">**Server name**: Choose a unique name for your MySQL server; this will be used to create a fully-qualified domain name like *wingtiptoysmysql.mysql.database.azure.com*.</span></span>
   - <span data-ttu-id="322d8-123">**Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="322d8-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="322d8-124">**Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="322d8-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="322d8-125">**Quelle auswählen**: Wählen Sie für dieses Tutorial `Blank` aus, um eine neue Datenbank zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="322d8-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="322d8-126">**Serveradministratoranmeldung**: Geben Sie den Namen des Datenbankadministrators an.</span><span class="sxs-lookup"><span data-stu-id="322d8-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="322d8-127">**Kennwort** und **Kennwort bestätigen**: Geben Sie das Kennwort für den Datenbankadministrator an.</span><span class="sxs-lookup"><span data-stu-id="322d8-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="322d8-128">**Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="322d8-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="322d8-129">**Version**: Geben Sie aktuelle Datenbankversion an.</span><span class="sxs-lookup"><span data-stu-id="322d8-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="322d8-130">**Tarif**: Geben Sie für dieses Tutorial den kostengünstigsten Tarif an.</span><span class="sxs-lookup"><span data-stu-id="322d8-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Festlegen der Eigenschaften der MySQL-Datenbank][MYSQL02]

1. <span data-ttu-id="322d8-132">Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="322d8-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="322d8-133">Konfigurieren einer Firewallregel für den MySQL-Datenbankserver im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="322d8-133">Configure a firewall rule for your MySQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="322d8-134">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="322d8-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="322d8-135">Klicken Sie auf **Alle Ressourcen** und anschließend auf die MySQL-Datenbank, die Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="322d8-135">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Auswählen der MySQL-Datenbank][MYSQL03]

1. <span data-ttu-id="322d8-137">Klicken Sie auf **Verbindungssicherheit**, und erstellen Sie im Abschnitt **Firewallregeln** eine neue Regel, indem Sie einen eindeutigen Namen für die Regel angeben, den Bereich der IP-Adressen eingeben, die Zugriff auf Ihre Datenbank benötigen, und anschließend auf **Speichern** klicken.</span><span class="sxs-lookup"><span data-stu-id="322d8-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Konfigurieren der Verbindungssicherheit][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a><span data-ttu-id="322d8-139">Abrufen der Verbindungszeichenfolge für den MySQL-Server im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="322d8-139">Retrieve the connection string for your MySQL server using the Azure Portal</span></span>

1. <span data-ttu-id="322d8-140">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="322d8-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="322d8-141">Klicken Sie auf **Alle Ressourcen** und anschließend auf die MySQL-Datenbank, die Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="322d8-141">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Auswählen der MySQL-Datenbank][MYSQL03]

1. <span data-ttu-id="322d8-143">Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie den Wert im Textfeld **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="322d8-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Abrufen der JDBC-Verbindungszeichenfolge][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a><span data-ttu-id="322d8-145">Erstellen der MySQL-Datenbank mit dem Befehlszeilenprogramm `mysql`</span><span class="sxs-lookup"><span data-stu-id="322d8-145">Create MySQL database using the `mysql` command-line utility</span></span>

1. <span data-ttu-id="322d8-146">Öffnen Sie eine Befehlsshell, und stellen Sie wie im folgenden Beispiel gezeigt eine Verbindung mit Ihrem MySQL-Server her, indem Sie einen `mysql`-Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="322d8-146">Open a command shell and connect to your MySQL server by entering a `mysql` command like the following example:</span></span>

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   <span data-ttu-id="322d8-147">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="322d8-147">Where:</span></span>

   | <span data-ttu-id="322d8-148">Parameter</span><span class="sxs-lookup"><span data-stu-id="322d8-148">Parameter</span></span> | <span data-ttu-id="322d8-149">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="322d8-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="322d8-150">Der vollqualifizierte MySQL-Servername, den Sie weiter oben in diesem Artikel festgelegt haben</span><span class="sxs-lookup"><span data-stu-id="322d8-150">Specifies your fully qualified MySQL server name from earlier in this article.</span></span> |
   | `user` | <span data-ttu-id="322d8-151">Der MySQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen</span><span class="sxs-lookup"><span data-stu-id="322d8-151">Specifies your MySQL administrator and shortened server name from earlier in this article.</span></span> |
   | `p` | <span data-ttu-id="322d8-152">Gibt an, dass auf eine Aufforderung zur Kennworteingabe gewartet werden soll</span><span class="sxs-lookup"><span data-stu-id="322d8-152">Specifies to wait until prompted for a password.</span></span> |


   <span data-ttu-id="322d8-153">Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="322d8-153">Your MySQL server should respond with a display like the following example:</span></span>

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

1. <span data-ttu-id="322d8-154">Erstellen Sie eine Datenbank mit dem Namen *mysqldb*, indem Sie wie im folgenden Beispiel gezeigt einen `mysql`-Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="322d8-154">Create a database named *mysqldb* by entering a `mysql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   <span data-ttu-id="322d8-155">Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="322d8-155">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. <span data-ttu-id="322d8-156">OPTIONAL: Sie können überprüfen, ob Ihre Datenbank erstellt wurde, indem Sie wie im folgenden Beispiel gezeigt einen `mysql`-Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="322d8-156">OPTIONAL: You can verify that your database was created by entering a `mysql` command like the following example:</span></span>

   ```SQL
   SHOW DATABASES;
   ```

   <span data-ttu-id="322d8-157">Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="322d8-157">Your MySQL server should respond with a display like the following example:</span></span>

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

1. <span data-ttu-id="322d8-158">Geben Sie `\q` ein, um das Befehlszeilenprogramm `mysql` zu beenden.</span><span class="sxs-lookup"><span data-stu-id="322d8-158">Enter `\q` to exit the `mysql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="322d8-159">Konfigurieren der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="322d8-159">Configure the sample application</span></span>

1. <span data-ttu-id="322d8-160">Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:</span><span class="sxs-lookup"><span data-stu-id="322d8-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. <span data-ttu-id="322d8-161">Suchen Sie im Verzeichnis *resources* des Beispielprojekts nach der Datei *application.properties*, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="322d8-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="322d8-162">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu, bzw. konfigurieren Sie diese Zeilen. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:</span><span class="sxs-lookup"><span data-stu-id="322d8-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.jpa.database-platform=org.hibernate.dialect.MySQL5InnoDBDialect
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   <span data-ttu-id="322d8-163">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="322d8-163">Where:</span></span>

   | <span data-ttu-id="322d8-164">Parameter</span><span class="sxs-lookup"><span data-stu-id="322d8-164">Parameter</span></span> | <span data-ttu-id="322d8-165">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="322d8-165">Description</span></span> |
   |---|---|
   | `spring.jpa.database-platform` | <span data-ttu-id="322d8-166">Die JPA-Datenbankplattform</span><span class="sxs-lookup"><span data-stu-id="322d8-166">Specifies the JPA database platform.</span></span> |
   | `spring.datasource.url` | <span data-ttu-id="322d8-167">Die MySQL-JDBC-Zeichenfolge, die Sie weiter oben in diesem Artikel kopiert haben</span><span class="sxs-lookup"><span data-stu-id="322d8-167">Specifies your MySQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="322d8-168">Der MySQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen</span><span class="sxs-lookup"><span data-stu-id="322d8-168">Specifies your MySQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="322d8-169">Das MySQL-Administratorkennwort, das Sie weiter oben in diesem Artikel festgelegt haben</span><span class="sxs-lookup"><span data-stu-id="322d8-169">Specifies your MySQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="322d8-170">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="322d8-170">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="322d8-171">Verpacken und Testen der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="322d8-171">Package and test the sample application</span></span> 

1. <span data-ttu-id="322d8-172">Erstellen Sie die Beispielanwendung mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="322d8-172">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P mysql
   ```

1. <span data-ttu-id="322d8-173">Starten Sie die Beispielanwendung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="322d8-173">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="322d8-174">Erstellen Sie wie in den folgenden Beispielen dargestellt über eine Eingabeaufforderung mit `curl` neue Datensätze:</span><span class="sxs-lookup"><span data-stu-id="322d8-174">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="322d8-175">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="322d8-175">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="322d8-176">Rufen Sie wie im folgenden Beispiel dargestellt über eine Eingabeaufforderung mit `curl` alle vorhandenen Datensätze ab:</span><span class="sxs-lookup"><span data-stu-id="322d8-176">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="322d8-177">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="322d8-177">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="322d8-178">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="322d8-178">Summary</span></span>

<span data-ttu-id="322d8-179">In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen in einer Azure MySQL-Datenbank mithilfe der Java-Persistenz-API (JPA) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="322d8-179">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure MySQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="322d8-180">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="322d8-180">Next steps</span></span>

<span data-ttu-id="322d8-181">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="322d8-181">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="322d8-182">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="322d8-182">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="322d8-183">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="322d8-183">Additional Resources</span></span>

<span data-ttu-id="322d8-184">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="322d8-184">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[MYSQL01]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-05.png
