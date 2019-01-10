---
title: Verwenden von Spring Data-JDBC mit Azure MySQL
description: Erfahren Sie, wie Sie Spring Data-JDBC (Java Database Connectivity) mit einer Azure MySQL-Datenbank verwenden.
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
ms.openlocfilehash: 5ec89194c72cef81c79d21382e41b33ebe91d3d0
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992332"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-mysql"></a><span data-ttu-id="f2f5e-103">Verwenden von Spring Data-JDBC mit Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="f2f5e-103">How to use Spring Data JDBC with Azure MySQL</span></span>

## <a name="overview"></a><span data-ttu-id="f2f5e-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="f2f5e-104">Overview</span></span>

<span data-ttu-id="f2f5e-105">In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen in einer Azure [MySQL](https://www.mysql.com/)-Datenbank mithilfe von [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [MySQL](https://www.mysql.com/) database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2f5e-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="f2f5e-106">Prerequisites</span></span>

<span data-ttu-id="f2f5e-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="f2f5e-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="f2f5e-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="f2f5e-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="f2f5e-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="f2f5e-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="f2f5e-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="f2f5e-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="f2f5e-112">[cURL](https://curl.haxx.se/) oder ein ähnliches HTTP-Hilfsprogramm zum Testen der Funktionalität</span><span class="sxs-lookup"><span data-stu-id="f2f5e-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="f2f5e-113">Das Befehlszeilenprogramm [mysql](https://dev.mysql.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="f2f5e-113">The [mysql](https://dev.mysql.com/downloads/) command-line utility.</span></span>
* <span data-ttu-id="f2f5e-114">Einen [Git-Client](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="f2f5e-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-mysql-database-for-azure"></a><span data-ttu-id="f2f5e-115">Erstellen einer MySQL-Datenbank für Azure</span><span class="sxs-lookup"><span data-stu-id="f2f5e-115">Create a MySQL database for Azure</span></span>

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="f2f5e-116">Erstellen eines MySQL-Datenbankservers im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="f2f5e-116">Create a MySQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="f2f5e-117">Ausführlichere Informationen zum Erstellen von MySQL-Datenbanken finden Sie unter [Erstellen eines Azure Database for MySQL-Servers im Azure-Portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f2f5e-117">You can read more detailed information about creating MySQL databases in [Create an Azure Database for MySQL server by using the Azure portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span></span>

1. <span data-ttu-id="f2f5e-118">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="f2f5e-119">Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **Azure Database for MySQL**.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for MySQL**.</span></span>

   ![Erstellen einer MySQL-Datenbank][MYSQL01]

1. <span data-ttu-id="f2f5e-121">Geben Sie Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-121">Enter the following information:</span></span>

   - <span data-ttu-id="f2f5e-122">**Servername**: Wählen Sie einen eindeutigen Namen für Ihren MySQL-Server aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoysmysql.mysql.database.azure.com*) verwendet.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-122">**Server name**: Choose a unique name for your MySQL server; this will be used to create a fully-qualified domain name like *wingtiptoysmysql.mysql.database.azure.com*.</span></span>
   - <span data-ttu-id="f2f5e-123">**Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="f2f5e-124">**Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="f2f5e-125">**Quelle auswählen**: Wählen Sie für dieses Tutorial `Blank` aus, um eine neue Datenbank zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="f2f5e-126">**Serveradministratoranmeldung**: Geben Sie den Namen des Datenbankadministrators an.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="f2f5e-127">**Kennwort** und **Kennwort bestätigen**: Geben Sie das Kennwort für den Datenbankadministrator an.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="f2f5e-128">**Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="f2f5e-129">**Version**: Geben Sie aktuelle Datenbankversion an.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="f2f5e-130">**Tarif**: Geben Sie für dieses Tutorial den kostengünstigsten Tarif an.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Festlegen der Eigenschaften der MySQL-Datenbank][MYSQL02]

1. <span data-ttu-id="f2f5e-132">Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="f2f5e-133">Konfigurieren einer Firewallregel für den MySQL-Datenbankserver im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="f2f5e-133">Configure a firewall rule for your MySQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="f2f5e-134">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="f2f5e-135">Klicken Sie auf **Alle Ressourcen** und anschließend auf die MySQL-Datenbank, die Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-135">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Auswählen der MySQL-Datenbank][MYSQL03]

1. <span data-ttu-id="f2f5e-137">Klicken Sie auf **Verbindungssicherheit**, und erstellen Sie im Abschnitt **Firewallregeln** eine neue Regel, indem Sie einen eindeutigen Namen für die Regel angeben, den Bereich der IP-Adressen eingeben, die Zugriff auf Ihre Datenbank benötigen, und anschließend auf **Speichern** klicken.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Konfigurieren der Verbindungssicherheit][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a><span data-ttu-id="f2f5e-139">Abrufen der Verbindungszeichenfolge für den MySQL-Server im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="f2f5e-139">Retrieve the connection string for your MySQL server using the Azure Portal</span></span>

1. <span data-ttu-id="f2f5e-140">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="f2f5e-141">Klicken Sie auf **Alle Ressourcen** und anschließend auf die MySQL-Datenbank, die Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-141">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Auswählen der MySQL-Datenbank][MYSQL03]

1. <span data-ttu-id="f2f5e-143">Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie den Wert im Textfeld **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Abrufen der JDBC-Verbindungszeichenfolge][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a><span data-ttu-id="f2f5e-145">Erstellen der MySQL-Datenbank mit dem Befehlszeilenprogramm `mysql`</span><span class="sxs-lookup"><span data-stu-id="f2f5e-145">Create MySQL database using the `mysql` command-line utility</span></span>

1. <span data-ttu-id="f2f5e-146">Öffnen Sie eine Befehlsshell, und stellen Sie wie im folgenden Beispiel gezeigt eine Verbindung mit Ihrem MySQL-Server her, indem Sie einen `mysql`-Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-146">Open a command shell and connect to your MySQL server by entering a `mysql` command like the following example:</span></span>

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   <span data-ttu-id="f2f5e-147">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-147">Where:</span></span>

   | <span data-ttu-id="f2f5e-148">Parameter</span><span class="sxs-lookup"><span data-stu-id="f2f5e-148">Parameter</span></span> | <span data-ttu-id="f2f5e-149">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="f2f5e-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="f2f5e-150">Der vollqualifizierte MySQL-Servername, den Sie weiter oben in diesem Artikel festgelegt haben</span><span class="sxs-lookup"><span data-stu-id="f2f5e-150">Specifies your fully qualified MySQL server name from earlier in this article.</span></span> |
   | `user` | <span data-ttu-id="f2f5e-151">Der MySQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen</span><span class="sxs-lookup"><span data-stu-id="f2f5e-151">Specifies your MySQL administrator and shortened server name from earlier in this article.</span></span> |
   | `p` | <span data-ttu-id="f2f5e-152">Gibt an, dass auf eine Aufforderung zur Kennworteingabe gewartet werden soll</span><span class="sxs-lookup"><span data-stu-id="f2f5e-152">Specifies to wait until prompted for a password.</span></span> |

   <span data-ttu-id="f2f5e-153">Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-153">Your MySQL server should respond with a display like the following example:</span></span>

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

1. <span data-ttu-id="f2f5e-154">Erstellen Sie eine Datenbank mit dem Namen *mysqldb*, indem Sie wie im folgenden Beispiel gezeigt einen `mysql`-Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-154">Create a database named *mysqldb* by entering a `mysql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   <span data-ttu-id="f2f5e-155">Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-155">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. <span data-ttu-id="f2f5e-156">OPTIONAL: Sie können überprüfen, ob Ihre Datenbank erstellt wurde, indem Sie wie im folgenden Beispiel gezeigt einen `mysql`-Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-156">OPTIONAL: You can verify that your database was created by entering a `mysql` command like the following example:</span></span>

   ```SQL
   SHOW DATABASES;
   ```

   <span data-ttu-id="f2f5e-157">Ihr MySQL-Server sollte mit einer Anzeige antworten, die dem folgenden Beispiel ähnelt:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-157">Your MySQL server should respond with a display like the following example:</span></span>

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

1. <span data-ttu-id="f2f5e-158">Geben Sie `\q` ein, um das Befehlszeilenprogramm `mysql` zu beenden.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-158">Enter `\q` to exit the `mysql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="f2f5e-159">Konfigurieren der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="f2f5e-159">Configure the sample application</span></span>

1. <span data-ttu-id="f2f5e-160">Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="f2f5e-161">Suchen Sie im Verzeichnis *resources* des Beispielprojekts nach der Datei *application.properties*, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="f2f5e-162">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu, bzw. konfigurieren Sie diese Zeilen. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false&serverTimezone=UTC
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   <span data-ttu-id="f2f5e-163">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-163">Where:</span></span>

   | <span data-ttu-id="f2f5e-164">Parameter</span><span class="sxs-lookup"><span data-stu-id="f2f5e-164">Parameter</span></span> | <span data-ttu-id="f2f5e-165">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="f2f5e-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="f2f5e-166">Die MySQL-JDBC-Zeichenfolge, die Sie weiter oben in diesem Artikel kopiert haben, mit hinzugefügter Zeitzone</span><span class="sxs-lookup"><span data-stu-id="f2f5e-166">Specifies your MySQL JDBC string from earlier in this article, with the time zone added.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="f2f5e-167">Der MySQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen</span><span class="sxs-lookup"><span data-stu-id="f2f5e-167">Specifies your MySQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="f2f5e-168">Das MySQL-Administratorkennwort, das Sie weiter oben in diesem Artikel festgelegt haben</span><span class="sxs-lookup"><span data-stu-id="f2f5e-168">Specifies your MySQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="f2f5e-169">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="f2f5e-170">Verpacken und Testen der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="f2f5e-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="f2f5e-171">Erstellen Sie die Beispielanwendung mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P mysql
   ```

1. <span data-ttu-id="f2f5e-172">Starten Sie die Beispielanwendung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="f2f5e-173">Erstellen Sie wie in den folgenden Beispielen dargestellt über eine Eingabeaufforderung mit `curl` neue Datensätze:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="f2f5e-174">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="f2f5e-175">Rufen Sie wie im folgenden Beispiel dargestellt über eine Eingabeaufforderung mit `curl` alle vorhandenen Datensätze ab:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="f2f5e-176">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="f2f5e-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="f2f5e-177">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="f2f5e-177">Summary</span></span>

<span data-ttu-id="f2f5e-178">In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen in einer Azure MySQL-Datenbank mithilfe von JDBC zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure MySQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2f5e-179">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="f2f5e-179">Next steps</span></span>

<span data-ttu-id="f2f5e-180">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f5e-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2f5e-181">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="f2f5e-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="f2f5e-182">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f2f5e-182">Additional Resources</span></span>

<span data-ttu-id="f2f5e-183">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="f2f5e-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[MYSQL01]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-05.png
