---
title: Verwenden der Spring Data-JPA mit Azure SQL-Datenbank
description: Erfahren Sie, wie Sie die Spring Data-JPA (Java-Persistenz-API) mit einer Azure SQL-Datenbank verwenden.
services: sql-database
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: sql-database
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 7119283bec250a4ab0854ba2c29b0906624448e9
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992333"
---
# <a name="how-to-use-spring-data-jpa-with-azure-sql-database"></a><span data-ttu-id="04d4a-103">Verwenden der Spring Data-JPA mit Azure SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="04d4a-103">How to use Spring Data JPA with Azure SQL Database</span></span>

## <a name="overview"></a><span data-ttu-id="04d4a-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="04d4a-104">Overview</span></span>

<span data-ttu-id="04d4a-105">In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen in einer [Azure SQL-Datenbank](https://azure.microsoft.com/services/sql-database/) mithilfe der [Java-Persistenz-API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="04d4a-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04d4a-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="04d4a-106">Prerequisites</span></span>

<span data-ttu-id="04d4a-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="04d4a-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="04d4a-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="04d4a-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="04d4a-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="04d4a-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="04d4a-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="04d4a-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="04d4a-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="04d4a-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="04d4a-112">[cURL](https://curl.haxx.se/) oder ein ähnliches HTTP-Hilfsprogramm zum Testen der Funktionalität</span><span class="sxs-lookup"><span data-stu-id="04d4a-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="04d4a-113">Einen [Git-Client](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="04d4a-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-sql-satabase"></a><span data-ttu-id="04d4a-114">Erstellen einer Azure SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="04d4a-114">Create an Azure SQL Satabase</span></span>

### <a name="create-a-sql-database-server-using-the-azure-portal"></a><span data-ttu-id="04d4a-115">Erstellen eines Azure SQL-Datenbankservers im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="04d4a-115">Create a SQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="04d4a-116">Ausführlichere Informationen zum Erstellen von Azure SQL-Datenbanken finden Sie unter [Erstellen einer Azure SQL-Datenbank im Azure-Portal](/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="04d4a-116">You can read more detailed information about creating Azure SQL databases in [Create an Azure SQL database in the Azure portal](/azure/sql-database/sql-database-get-started-portal).</span></span>

1. <span data-ttu-id="04d4a-117">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="04d4a-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="04d4a-118">Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **SQL-Datenbank**.</span><span class="sxs-lookup"><span data-stu-id="04d4a-118">Click **+Create a resource**, then **Databases**, and then click **SQL Database**.</span></span>

   ![Erstellen einer SQL-Datenbank][SQL01]

1. <span data-ttu-id="04d4a-120">Geben Sie die folgenden Informationen an:</span><span class="sxs-lookup"><span data-stu-id="04d4a-120">Specify the following information:</span></span>

   - <span data-ttu-id="04d4a-121">**Datenbankname**: Wählen Sie einen eindeutigen Namen für Ihre SQL-Datenbank aus. Die Datenbank wird auf dem SQL-Server erstellt, den Sie später angeben.</span><span class="sxs-lookup"><span data-stu-id="04d4a-121">**Database name**: Choose a unique name for your SQL database; this will be created in the SQL server that you will specify later.</span></span>
   - <span data-ttu-id="04d4a-122">**Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="04d4a-122">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="04d4a-123">**Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="04d4a-123">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="04d4a-124">**Quelle auswählen**: Wählen Sie für dieses Tutorial `Blank database` aus, um eine neue Datenbank zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="04d4a-124">**Select source**: For this tutorial, select `Blank database` to create a new database.</span></span>

   ![Festlegen der Eigenschaften der SQL-Datenbank][SQL02]
   
1. <span data-ttu-id="04d4a-126">Klicken Sie auf **Server** und dann auf **Neuen Server erstellen**, und geben Sie die folgenden Informationen an:</span><span class="sxs-lookup"><span data-stu-id="04d4a-126">Click **Server**, then **Create a new server**, and then specify the following information:</span></span>

   - <span data-ttu-id="04d4a-127">**Servername**: Wählen Sie einen eindeutigen Namen für Ihren SQL-Server aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoyssql.database.windows.net*) verwendet.</span><span class="sxs-lookup"><span data-stu-id="04d4a-127">**Server name**: Choose a unique name for your SQL server; this will be used to create a fully-qualified domain name like *wingtiptoyssql.database.windows.net*.</span></span>
   - <span data-ttu-id="04d4a-128">**Serveradministratoranmeldung**: Geben Sie den Namen des Datenbankadministrators an.</span><span class="sxs-lookup"><span data-stu-id="04d4a-128">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="04d4a-129">**Kennwort** und **Kennwort bestätigen**: Geben Sie das Kennwort für den Datenbankadministrator an.</span><span class="sxs-lookup"><span data-stu-id="04d4a-129">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="04d4a-130">**Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="04d4a-130">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Angeben des SQL-Servers][SQL03]

1. <span data-ttu-id="04d4a-132">Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="04d4a-132">When you have entered all of the above information, click **Select**.</span></span>

1. <span data-ttu-id="04d4a-133">Geben Sie für dieses Tutorial den kostengünstigsten **Tarif** an, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="04d4a-133">For this tutorial, specify the least-expensive **Pricing tier**, and then click **Create**.</span></span>

   ![Erstellen der SQL-Datenbank][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="04d4a-135">Konfigurieren einer Firewallregel für den SQL-Server im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="04d4a-135">Configure a firewall rule for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="04d4a-136">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="04d4a-136">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="04d4a-137">Klicken Sie auf **Alle Ressourcen** und anschließend auf den SQL-Server, den Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="04d4a-137">Click **All Resources**, then click the SQL server you just created.</span></span>

   ![Auswählen des SQL-Servers][SQL05]

1. <span data-ttu-id="04d4a-139">Klicken Sie im Abschnitt **Übersicht** auf **Firewalleinstellungen anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="04d4a-139">In the **Overview** section, click **Show firewall settings**</span></span>

   ![Firewalleinstellungen anzeigen][SQL06]

1. <span data-ttu-id="04d4a-141">Erstellen Sie im Abschnitt **Firewalls und virtuelle Netzwerke** eine neue Regel, indem Sie einen eindeutigen Namen für die Regel angeben, den Bereich der IP-Adressen eingeben, die Zugriff auf Ihre Datenbank benötigen, und anschließend auf **Speichern** klicken.</span><span class="sxs-lookup"><span data-stu-id="04d4a-141">In the **Firewalls and virtual networks** section, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Konfigurieren der Firewalleinstellungen][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="04d4a-143">Abrufen der Verbindungszeichenfolge für den SQL-Server im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="04d4a-143">Retrieve the connection string for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="04d4a-144">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="04d4a-144">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="04d4a-145">Klicken Sie auf **Alle Ressourcen** und anschließend auf die SQL-Datenbank, die Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="04d4a-145">Click **All Resources**, then click the SQL database you just created.</span></span>

   ![Auswählen der SQL-Datenbank][SQL08]

1. <span data-ttu-id="04d4a-147">Klicken Sie auf **Verbindungszeichenfolgen** und dann auf **JDBC**, und kopieren Sie den Wert im Textfeld „JDBC“.</span><span class="sxs-lookup"><span data-stu-id="04d4a-147">Click **Connection strings**, then click **JDBC**, and copy the value in the JDBC text field.</span></span>

   ![Abrufen der JDBC-Verbindungszeichenfolge][SQL09]

## <a name="configure-the-sample-application"></a><span data-ttu-id="04d4a-149">Konfigurieren der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="04d4a-149">Configure the sample application</span></span>

1. <span data-ttu-id="04d4a-150">Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:</span><span class="sxs-lookup"><span data-stu-id="04d4a-150">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="04d4a-151">Suchen Sie im Verzeichnis *resources* des Beispielprojekts nach der Datei *application.properties*, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="04d4a-151">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="04d4a-152">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu, bzw. konfigurieren Sie diese Zeilen. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:</span><span class="sxs-lookup"><span data-stu-id="04d4a-152">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   <span data-ttu-id="04d4a-153">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="04d4a-153">Where:</span></span>

   | <span data-ttu-id="04d4a-154">Parameter</span><span class="sxs-lookup"><span data-stu-id="04d4a-154">Parameter</span></span> | <span data-ttu-id="04d4a-155">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="04d4a-155">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="04d4a-156">Eine bearbeitete Version der SQL-JDBC-Zeichenfolge, die Sie weiter oben in diesem Artikel abgerufen haben</span><span class="sxs-lookup"><span data-stu-id="04d4a-156">Specifies an edited version of your SQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="04d4a-157">Der SQL-Administratorname, den Sie weiter oben in diesem Artikel festgelegt haben, mit angefügtem gekürzten Servernamen</span><span class="sxs-lookup"><span data-stu-id="04d4a-157">Specifies your SQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="04d4a-158">Das SQL-Administratorkennwort, das Sie weiter oben in diesem Artikel festgelegt haben</span><span class="sxs-lookup"><span data-stu-id="04d4a-158">Specifies your SQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="04d4a-159">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="04d4a-159">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="04d4a-160">Verpacken und Testen der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="04d4a-160">Package and test the sample application</span></span> 

1. <span data-ttu-id="04d4a-161">Erstellen Sie die Beispielanwendung mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="04d4a-161">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P sql
   ```

1. <span data-ttu-id="04d4a-162">Starten Sie die Beispielanwendung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="04d4a-162">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="04d4a-163">Erstellen Sie wie in den folgenden Beispielen dargestellt über eine Eingabeaufforderung mit `curl` neue Datensätze:</span><span class="sxs-lookup"><span data-stu-id="04d4a-163">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="04d4a-164">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="04d4a-164">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="04d4a-165">Rufen Sie wie im folgenden Beispiel dargestellt über eine Eingabeaufforderung mit `curl` alle vorhandenen Datensätze ab:</span><span class="sxs-lookup"><span data-stu-id="04d4a-165">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="04d4a-166">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="04d4a-166">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="04d4a-167">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="04d4a-167">Summary</span></span>

<span data-ttu-id="04d4a-168">In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen in einer Azure SQL-Datenbank mithilfe der Java-Persistenz-API (JPA) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="04d4a-168">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure SQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04d4a-169">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="04d4a-169">Next steps</span></span>

<span data-ttu-id="04d4a-170">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="04d4a-170">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04d4a-171">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="04d4a-171">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="04d4a-172">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="04d4a-172">Additional Resources</span></span>

<span data-ttu-id="04d4a-173">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="04d4a-173">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[SQL01]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-09.png