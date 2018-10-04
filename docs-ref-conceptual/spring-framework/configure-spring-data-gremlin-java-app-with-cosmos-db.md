---
title: Verwenden von Spring Data Gremlin Starter mit der SQL-API von Azure Cosmos DB
description: Hier erfahren Sie, wie eine mit dem Spring Boot-Initialisierer erstellte Anwendung mit der SQL-API von Azure Cosmos DB konfiguriert wird.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.date: 08/20/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 561dba84b0c1662fa6575e1816ff3dd2f0c6093b
ms.sourcegitcommit: bb7286fad75a2bb43e6ce1a8f1b09e701147c9f9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047167"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="bf88d-103">Verwenden von Spring Data Gremlin Starter mit der SQL-API von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf88d-103">How to use the Spring Data Gremlin Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="bf88d-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="bf88d-104">Overview</span></span>

<span data-ttu-id="bf88d-105">Spring Data Gremlin Starter bietet Spring-Datenunterstützung für die Gremlin-Abfragesprache von Apache, die Entwickler für jeden beliebigen, mit Gremlin kompatiblen Datenspeicher verwenden können.</span><span class="sxs-lookup"><span data-stu-id="bf88d-105">The Spring Data Gremlin Starter provides Spring Data support for the Gremlin query language from Apache, which developers can use with any Gremlin-compatible data store.</span></span>

<span data-ttu-id="bf88d-106">Dieser Artikel zeigt, wie über das Azure-Portal eine Azure Cosmos DB-Instanz für die Verwendung mit der Gremlin-API und dann mithilfe von **[Spring Initializr]** eine benutzerdefinierte Java-Anwendung erstellt wird. Anschließend wird veranschaulicht, wie Spring Data Gremlin Starter-Funktionen zu Ihrer benutzerdefinierten Anwendung hinzugefügt werden, um Daten mithilfe von Gremlin in Ihrer Azure Cosmos DB-Instanz zu speichern und daraus abzurufen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-106">This article demonstrates creating an Azure Cosmos DB by using the Azure portal for use with Gremlin API, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Data Gremlin Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Gremlin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf88d-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="bf88d-107">Prerequisites</span></span>

<span data-ttu-id="bf88d-108">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="bf88d-108">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="bf88d-109">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="bf88d-109">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="bf88d-110">[Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="bf88d-110">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="bf88d-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="bf88d-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="bf88d-112">Für die Schritte in diesem Artikel wird mindestens die Spring Boot-Version 2.0 benötigt.</span><span class="sxs-lookup"><span data-stu-id="bf88d-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a><span data-ttu-id="bf88d-113">Erstellen einer Azure Cosmos DB-Instanz über das Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="bf88d-113">Create an Azure Cosmos DB using the Azure portal</span></span>

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a><span data-ttu-id="bf88d-114">Erstellen Ihrer Azure-Cosmos-Datenbank für die Verwendung mit der Gremlin-API</span><span class="sxs-lookup"><span data-stu-id="bf88d-114">Create your Azure Cosmos Database for use with Gremlin API</span></span>

1. <span data-ttu-id="bf88d-115">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und klicken Sie auf **+Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Erstellen einer Ressource][AZ01]

1. <span data-ttu-id="bf88d-117">Klicken Sie auf **Datenbanken** und anschließend auf **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Erstellen von Azure Cosmos DB][AZ02]

1. <span data-ttu-id="bf88d-119">Geben Sie auf der Seite **Azure Cosmos DB** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="bf88d-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="bf88d-120">Geben Sie eine eindeutige **ID** ein, die als Teil des Gremlin-URIs für Ihre Datenbank verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="bf88d-120">Enter a unique **ID**, which you will use as part of the Gremlin URI for your database.</span></span> <span data-ttu-id="bf88d-121">Wenn Sie für die **ID** also beispielsweise **wingtiptoysdata** eingegeben haben, lautet der Gremlin-URI *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-121">For example: if you entered **wingtiptoysdata** for the **ID**, the Gremlin URI would be *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span></span>
   * <span data-ttu-id="bf88d-122">Wählen Sie **Gremlin (Diagramm)** für die API aus.</span><span class="sxs-lookup"><span data-stu-id="bf88d-122">Choose **Gremlin (Graph)** for the API.</span></span>
   * <span data-ttu-id="bf88d-123">Wählen Sie das **Abonnement**, das Sie für Ihre Datenbank verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="bf88d-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="bf88d-124">Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihre Datenbank erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="bf88d-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="bf88d-125">Geben Sie den **Speicherort** für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="bf88d-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="bf88d-126">Wenn Sie diese Optionen angegeben haben, klicken Sie zum Erstellen Ihrer Datenbank auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Angeben von Optionen für Azure Cosmos DB][AZ03]

1. <span data-ttu-id="bf88d-128">Wenn Ihre Datenbank erstellt wurde, wird Sie in Ihrem Azure-**Dashboard** sowie auf den Seiten **Alle Ressourcen** und **Azure Cosmos DB** aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="bf88d-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="bf88d-129">Sie können in Ihrer Datenbank auf eine beliebige Stelle klicken, um die Eigenschaftenseite für Ihren Cache zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Alle Ressourcen][AZ04]

1. <span data-ttu-id="bf88d-131">Wenn die Eigenschaftenseite für Ihre Datenbank angezeigt wird, klicken Sie auf **Zugriffsschlüssel**, und kopieren Sie Ihren URI sowie Ihre Zugriffsschlüssel für Ihre Datenbank. Diese Werte verwenden Sie in Ihrer Spring Boot-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="bf88d-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Zugriffsschlüssel][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a><span data-ttu-id="bf88d-133">Hinzufügen eines Diagramms zu Ihrer Azure-Cosmos-Datenbank</span><span class="sxs-lookup"><span data-stu-id="bf88d-133">Add a graph to your Azure Cosmos Database</span></span>

1. <span data-ttu-id="bf88d-134">Klicken Sie auf **Daten-Explorer** und anschließend auf **New Graph** (Neues Diagramm).</span><span class="sxs-lookup"><span data-stu-id="bf88d-134">Click **Data Explorer**, and then click **New Graph**.</span></span>

   ![Neues Diagramm][AZ06]

1. <span data-ttu-id="bf88d-136">Wenn **Diagramm hinzufügen** angezeigt wird, geben Sie folgende Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="bf88d-136">When the **Add Graph** is displayed, enter the following information:</span></span>

   * <span data-ttu-id="bf88d-137">Geben Sie eine eindeutige **Datenbank-ID** für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="bf88d-137">Specify a unique **Database id** for your database.</span></span>
   * <span data-ttu-id="bf88d-138">Geben Sie eine eindeutige **Diagramm-ID** für Ihr Diagramm an.</span><span class="sxs-lookup"><span data-stu-id="bf88d-138">Specify a unique **Graph id** for your graph.</span></span>
   * <span data-ttu-id="bf88d-139">Sie können Ihre **Speicherkapazität** angeben oder die Standardeinstellung übernehmen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-139">You can choose to specify your **Storage capacity**, or you can accept the default.</span></span>
   * <span data-ttu-id="bf88d-140">Geben Sie Ihren **Durchsatz** an. Für dieses Beispiel können Sie 400 Anforderungseinheiten (Request Units, RUs) auswählen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-140">Specify your **Throughput**, and for this example you can choose 400 Request Units (RUs).</span></span>
   
   <span data-ttu-id="bf88d-141">Wenn Sie diese Optionen angegeben haben, klicken Sie auf **OK**, um das Diagramm zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-141">When you have specified these options, click **OK** to create your graph.</span></span>

   ![Hinzufügen des Diagramms][AZ07]

1. <span data-ttu-id="bf88d-143">Das erstellte Diagramm kann über den **Daten-Explorer** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="bf88d-143">After your graph has been created, you can use the **Data Explorer** to view it.</span></span>

   ![Anzeige der Diagrammeigenschaften][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="bf88d-145">Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="bf88d-145">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="bf88d-146">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="bf88d-146">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="bf88d-147">Geben Sie an, dass Sie ein Projekt vom Typ **Maven** mit **Java** generieren möchten, benennen Sie **Gruppe** und **Artefakt** für Ihre Anwendung, und geben Sie als **Spring Boot**-Version mindestens die Version 2.0 an. Klicken Sie anschließend auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-147">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version with a version that is equal to or greater than 2.0, and then click **Generate Project**.</span></span>

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="bf88d-149">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt** (also beispielsweise „\*com.example.wintiptoysdata“).</span><span class="sxs-lookup"><span data-stu-id="bf88d-149">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: \*com.example.wintiptoysdata.</span></span>
   >

1. <span data-ttu-id="bf88d-150">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="bf88d-150">When prompted, download the project to a path on your local computer.</span></span>

   ![Herunterladen eines benutzerdefinierten Spring Boot-Projekts][SI02]

1. <span data-ttu-id="bf88d-152">Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="bf88d-152">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a><span data-ttu-id="bf88d-154">Konfigurieren Ihrer Spring Boot-App für die Verwendung von Spring Data Gremlin Starter</span><span class="sxs-lookup"><span data-stu-id="bf88d-154">Configure your Spring Boot app to use the Spring Data Gremlin Starter</span></span>

1. <span data-ttu-id="bf88d-155">Suchen Sie die Datei *pom.xml* im Verzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bf88d-155">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="bf88d-156">Oder</span><span class="sxs-lookup"><span data-stu-id="bf88d-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Suchen der Datei „pom.xml“][PM01]

1. <span data-ttu-id="bf88d-158">Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie Spring Data Gremlin Starter der Liste mit `<dependencies>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-158">Open the *pom.xml* file in a text editor, and add the Spring Data Gremlin Starter to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][PM02]

1. <span data-ttu-id="bf88d-160">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-160">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="bf88d-161">Konfigurieren der Spring Boot-App für die Verwendung von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf88d-161">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="bf88d-162">Suchen Sie das Verzeichnis *resources* Ihrer App, und erstellen Sie eine neue Datei namens *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-162">Locate the *resources* directory of your app, and create a new file named *application.yml*.</span></span> <span data-ttu-id="bf88d-163">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="bf88d-163">For example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   <span data-ttu-id="bf88d-164">Oder</span><span class="sxs-lookup"><span data-stu-id="bf88d-164">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Erstellen der Datei „application.yml“][RE01]

1. <span data-ttu-id="bf88d-166">Öffnen Sie die Datei *application.yml* in einem Text-Editor, und fügen Sie ihr die folgenden Zeilen hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften für Ihre Datenbank:</span><span class="sxs-lookup"><span data-stu-id="bf88d-166">Open the *application.yml* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   
   <span data-ttu-id="bf88d-167">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="bf88d-167">Where:</span></span>
   
   | <span data-ttu-id="bf88d-168">Feld</span><span class="sxs-lookup"><span data-stu-id="bf88d-168">Field</span></span> | <span data-ttu-id="bf88d-169">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="bf88d-169">Description</span></span> |
   |---|---|
   | `endpoint` | <span data-ttu-id="bf88d-170">Gibt den Gremlin-URI für Ihre Datenbank an. Dieser wird von der eindeutigen **ID** abgeleitet, die Sie zuvor in diesem Tutorial beim Erstellen Ihrer Azure Cosmos DB-Instanz angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="bf88d-170">Specifies the Gremlin URI for your database, which is derived from the unique **ID** that you specified when you created your Azure Cosmos DB earlier in this tutorial.</span></span> |
   | `port` | <span data-ttu-id="bf88d-171">Gibt den TCP/IP-Port an (**443** für HTTPS).</span><span class="sxs-lookup"><span data-stu-id="bf88d-171">Specifies the TCP/IP port, which should be **443** for HTTPS.</span></span> |
   | `username` | <span data-ttu-id="bf88d-172">Gibt die eindeutige **Datenbank-ID** und **Diagramm-ID** an, die Sie zuvor in diesem Tutorial beim Hinzufügen Ihres Diagramms verwendet haben (Syntax: /dbs/**{Datenbank-ID}**/colls/**{Diagramm-ID}**).</span><span class="sxs-lookup"><span data-stu-id="bf88d-172">Specifies the unique **Database id** and **Graph id** that you used when you added your graph earlier in this tutorial; this must be entered using the following syntax: "/dbs/**{Database id}**/colls/**{Graph id}**".</span></span> |
   | `password` | <span data-ttu-id="bf88d-173">Gibt den primären oder sekundären **Zugriffsschlüssel** an, den Sie zuvor in diesem Tutorial kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="bf88d-173">Specifies either the primary or secondary **Access key** that you copied earlier in this tutorial.</span></span> |
   | `telemetryAllowed` | <span data-ttu-id="bf88d-174">Geben Sie **true** an, wenn Sie Telemetriedaten aktivieren möchten (oder **false**, falls nicht).</span><span class="sxs-lookup"><span data-stu-id="bf88d-174">Specify **true** if you want to enable telemetry; otherwise, **false**.</span></span>

1. <span data-ttu-id="bf88d-175">Speichern und schließen Sie die Datei *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-175">Save and close the *application.yml* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="bf88d-176">Hinzufügen eines Beispielcodes zur Implementierung von grundlegenden Datenbankfunktionen</span><span class="sxs-lookup"><span data-stu-id="bf88d-176">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="bf88d-177">In diesem Abschnitt werden die Java-Klassen erstellt, die erforderlich sind, um Daten in Ihrer Datenbank zu speichern.</span><span class="sxs-lookup"><span data-stu-id="bf88d-177">In this section, you create the necessary Java classes for storing data in your database.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="bf88d-178">Ändern der Hauptanwendungsklasse</span><span class="sxs-lookup"><span data-stu-id="bf88d-178">Modify the main application class</span></span>

1. <span data-ttu-id="bf88d-179">Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bf88d-179">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="bf88d-180">Oder</span><span class="sxs-lookup"><span data-stu-id="bf88d-180">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Suchen der Java-Anwendungsdatei][JV01]

1. <span data-ttu-id="bf88d-182">Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-182">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.example.wingtiptoysdata.domain.Network;
   import com.example.wingtiptoysdata.domain.Person;
   import com.example.wingtiptoysdata.domain.Relation;
   import com.example.wingtiptoysdata.repository.NetworkRepository;
   import com.example.wingtiptoysdata.repository.PersonRepository;
   import com.example.wingtiptoysdata.repository.RelationRepository;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import javax.annotation.PostConstruct;
   import javax.annotation.PreDestroy;
   
   @SpringBootApplication
   public class WingtiptoysdataApplication {
   
       // Define several person classes to store personal data.
       private final Person person1 = new Person("01", "Nellie Hughes", "23");
       private final Person person2 = new Person("02", "Delmar Alfred", "34");
       private final Person person3 = new Person("03", "Kelley Hunter", "45");
       private final Person person4 = new Person("04", "Roscoe Guerin", "56");
       private final Person person5 = new Person("05", "Gracie Chavez", "67");
   
       // Define relationship classes to define the relationships between some of the persons.
       private final Relation relation1 = new Relation("0102", "siblings", person1, person2);
       private final Relation relation2 = new Relation("0203", "coworkers", person2, person3);
       private final Relation relation3 = new Relation("0301", "parent", person3, person1);
       private final Relation relation4 = new Relation("0302", "parent", person3, person2);
       private final Relation relation5 = new Relation("0501", "grandparent", person5, person1);
       private final Relation relation6 = new Relation("0502", "grandparent", person5, person2);
   
       // Define the network.
       private final Network network = new Network();
   
       // Autowire the repositories and factory.
       @Autowired
       private PersonRepository personRepo;
       @Autowired
       private RelationRepository relationRepo;
       @Autowired
       private NetworkRepository networkRepo;
       @Autowired
       private GremlinFactory factory;
   
       // Run the Spring application and exit.
    public static void main(String[] args) {
           SpringApplication.run(WingtiptoysdataApplication.class, args);
           System.exit(0);
    }
   
       // Perform post-construct operations.    
       @PostConstruct
       public void setup() {
           // Delete any existing data from the database.
           this.networkRepo.deleteAll();
   
           // Add the relationship classes as edges.
           this.network.getEdges().add(this.relation1);
           this.network.getEdges().add(this.relation2);
           this.network.getEdges().add(this.relation3);
           this.network.getEdges().add(this.relation4);
           this.network.getEdges().add(this.relation5);
           this.network.getEdges().add(this.relation6);
   
           // Add the person classes as vertices.
           this.network.getVertexes().add(this.person1);
           this.network.getVertexes().add(this.person2);
           this.network.getVertexes().add(this.person3);
           this.network.getVertexes().add(this.person4);
           this.network.getVertexes().add(this.person5);
   
           // Save the network.
           this.networkRepo.save(this.network);
       }
   }
   ```

1. <span data-ttu-id="bf88d-183">Speichern und schließen Sie die Java-Hauptanwendungsdatei.</span><span class="sxs-lookup"><span data-stu-id="bf88d-183">Save and close the main application Java file.</span></span>

### <a name="define-a-basic-class-for-storing-configuration-information"></a><span data-ttu-id="bf88d-184">Definieren einer einfachen Klasse zum Speichern von Konfigurationsinformationen</span><span class="sxs-lookup"><span data-stu-id="bf88d-184">Define a basic class for storing configuration information</span></span>

1. <span data-ttu-id="bf88d-185">Erstellen Sie unter dem Paketverzeichnis Ihrer App einen Ordner namens *config*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bf88d-185">Create a folder named *config* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   <span data-ttu-id="bf88d-186">Oder</span><span class="sxs-lookup"><span data-stu-id="bf88d-186">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. <span data-ttu-id="bf88d-187">Erstellen Sie im Verzeichnis *config* eine neue Java-Datei namens *UserRepositoryConfiguration.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-187">Create a new Java file named *UserRepositoryConfiguration.java* in the *config* directory, then open the file in a text editor, and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.config;

   import com.microsoft.spring.data.gremlin.common.GremlinConfiguration;
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.microsoft.spring.data.gremlin.config.AbstractGremlinConfiguration;
   import com.microsoft.spring.data.gremlin.repository.config.EnableGremlinRepositories;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.context.properties.EnableConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.context.annotation.PropertySource;
   
   @Configuration
   @EnableGremlinRepositories(basePackages = "com.example.wingtiptoysdata.repository")
   @EnableConfigurationProperties(GremlinConfiguration.class)
   @PropertySource("classpath:application.yml")
   public class UserRepositoryConfiguration extends AbstractGremlinConfiguration {
   
       @Autowired
       private GremlinConfiguration config;
   
       @Override
       public GremlinConfiguration getGremlinConfiguration() {
           return this.config;
       }
   }
   ```

1. <span data-ttu-id="bf88d-188">Speichern und schließen Sie die Datei *UserRepositoryConfiguration.java*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-188">Save and close the *UserRepositoryConfiguration.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a><span data-ttu-id="bf88d-189">Definieren einer Gruppe von Klassen zum Definieren der Elemente Ihrer Diagrammdatenbank</span><span class="sxs-lookup"><span data-stu-id="bf88d-189">Define a set of classes that define the elements of your graph database</span></span>

1. <span data-ttu-id="bf88d-190">Erstellen Sie unter dem Paketverzeichnis Ihrer App einen Ordner namens *domain*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bf88d-190">Create a folder named *domain* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   <span data-ttu-id="bf88d-191">Oder</span><span class="sxs-lookup"><span data-stu-id="bf88d-191">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. <span data-ttu-id="bf88d-192">Erstellen Sie im Verzeichnis *domain* eine neue Java-Datei namens *Person.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-192">Create a new Java file named *Person.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Vertex;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Vertex
   @AllArgsConstructor
   @NoArgsConstructor
   public class Person {
   
       @Id
       private String id;
   
       private String name;
   
       private String age;
   }
   ```

1. <span data-ttu-id="bf88d-193">Speichern und schließen Sie die Datei *Person.java*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-193">Save and close the *Person.java* file.</span></span>

1. <span data-ttu-id="bf88d-194">Erstellen Sie im Verzeichnis *domain* eine neue Java-Datei namens *Relation.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-194">Create a new Java file named *Relation.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Edge;
   import com.microsoft.spring.data.gremlin.annotation.EdgeFrom;
   import com.microsoft.spring.data.gremlin.annotation.EdgeTo;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Edge
   @AllArgsConstructor
   @NoArgsConstructor
   public class Relation {
   
       @Id
       private String id;
   
       private String name;
   
       @EdgeFrom
       private Person personFrom;
   
       @EdgeTo
       private Person personTo;
   }
   ```

1. <span data-ttu-id="bf88d-195">Speichern und schließen Sie die Datei *Relation.java*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-195">Save and close the *Relation.java* file.</span></span>

1. <span data-ttu-id="bf88d-196">Erstellen Sie im Verzeichnis *domain* eine neue Java-Datei namens *Network.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-196">Create a new Java file named *Network.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.EdgeSet;
   import com.microsoft.spring.data.gremlin.annotation.Graph;
   import com.microsoft.spring.data.gremlin.annotation.VertexSet;
   import lombok.Getter;
   import org.springframework.data.annotation.Id;
   
   import java.util.ArrayList;
   import java.util.List;
   
   @Graph
   public class Network {
   
       @Id
       private String id;
   
       public Network() {
           this.edges = new ArrayList<Object>();
           this.vertexes = new ArrayList<Object>();
       }
   
       @EdgeSet
       @Getter
       private List<Object> edges;
   
       @VertexSet
       @Getter
       private List<Object> vertexes;
   }
   ```

1. <span data-ttu-id="bf88d-197">Speichern und schließen Sie die Datei *Network.java*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-197">Save and close the *Network.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a><span data-ttu-id="bf88d-198">Definieren einer Gruppe von Klassen zum Definieren der Repositorys für Ihre Diagrammdatenbank</span><span class="sxs-lookup"><span data-stu-id="bf88d-198">Define a set of classes that define the repositories for your graph database</span></span>

1. <span data-ttu-id="bf88d-199">Erstellen Sie unter dem Paketverzeichnis Ihrer App einen Ordner namens *repository*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bf88d-199">Create a folder named *repository* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   <span data-ttu-id="bf88d-200">Oder</span><span class="sxs-lookup"><span data-stu-id="bf88d-200">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. <span data-ttu-id="bf88d-201">Erstellen Sie im Verzeichnis *repository* eine neue Java-Datei namens *NetworkRepository.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-201">Create a new Java file named *NetworkRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. <span data-ttu-id="bf88d-202">Speichern und schließen Sie die Datei *NetworkRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-202">Save and close the *NetworkRepository.java* file.</span></span>

1. <span data-ttu-id="bf88d-203">Erstellen Sie im Verzeichnis *repository* eine neue Java-Datei namens *PersonRepository.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-203">Create a new Java file named *PersonRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. <span data-ttu-id="bf88d-204">Speichern und schließen Sie die Datei *PersonRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-204">Save and close the *PersonRepository.java* file.</span></span>

1. <span data-ttu-id="bf88d-205">Erstellen Sie im Verzeichnis *repository* eine neue Java-Datei namens *RelationRepository.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="bf88d-205">Create a new Java file named *RelationRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. <span data-ttu-id="bf88d-206">Speichern und schließen Sie die Datei *RelationRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-206">Save and close the *RelationRepository.java* file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="bf88d-207">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="bf88d-207">Build and test your app</span></span>

1. <span data-ttu-id="bf88d-208">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bf88d-208">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="bf88d-209">Oder</span><span class="sxs-lookup"><span data-stu-id="bf88d-209">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="bf88d-210">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bf88d-210">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="bf88d-211">Die Anwendung zeigt mehrere Laufzeitmeldungen an. Sind keine Fehler aufgetreten, können Sie im Azure-Portal den Inhalt Ihrer Azure Cosmos DB-Instanz anzeigen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-211">Your application will display several runtime messages, and if there were no errors, you can use the Azure portal to view the contents of your Azure Cosmos DB.</span></span> <span data-ttu-id="bf88d-212">Klicken Sie hierzu auf der Eigenschaftenseite für Ihre Datenbank auf **Daten-Explorer**, klicken Sie auf **Execute Gremlin Query** (Gremlin-Abfrage ausführen), und wählen Sie anschließend ein Element aus der Ergebnisliste aus, um die Daten anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-212">To do so, click **Data Explorer** on the properties page for your database, then click **Execute Gremlin Query**, and then select an item from the list of results to view the data.</span></span>

   ![Anzeigen von Daten mit dem Document-Explorer][JV03]

## <a name="next-steps"></a><span data-ttu-id="bf88d-214">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="bf88d-214">Next steps</span></span>

<span data-ttu-id="bf88d-215">Weitere Informationen zur Azure-Unterstützung für Gremlin und Graph-API finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="bf88d-215">For more information about Azure support for Gremlin and Graph API, see the following articles:</span></span>

* [<span data-ttu-id="bf88d-216">Einführung in die Graph-API von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf88d-216">Introduction to Azure Cosmos DB: Graph API</span></span>](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [<span data-ttu-id="bf88d-217">Unterstützung für Gremlin-Diagramme in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf88d-217">Azure Cosmos DB Gremlin graph support</span></span>](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [<span data-ttu-id="bf88d-218">Azure Cosmos DB: Erstellen einer Graphdatenbank mit Java und dem Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="bf88d-218">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [<span data-ttu-id="bf88d-219">Tutorial: Abfragen der Graph-API von Azure Cosmos DB mithilfe von Gremlin</span><span class="sxs-lookup"><span data-stu-id="bf88d-219">Tutorial: Query Azure Cosmos DB Graph API by using Gremlin</span></span>](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* <span data-ttu-id="bf88d-220">[Spring Data Gremlin Starter]</span><span class="sxs-lookup"><span data-stu-id="bf88d-220">[Spring Data Gremlin Starter]</span></span>

<span data-ttu-id="bf88d-221">Weitere Informationen zur Verwendung von Azure Cosmos DB und Java finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="bf88d-221">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="bf88d-222">[Dokumentation für Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="bf88d-222">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="bf88d-223">[Azure Cosmos DB: Erstellen einer Dokumentdatenbank mit Java und dem Azure-Portal][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="bf88d-223">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="bf88d-224">[Spring-Daten für SQL-API von Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="bf88d-224">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="bf88d-225">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="bf88d-225">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="bf88d-226">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bf88d-226">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="bf88d-227">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="bf88d-227">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="bf88d-228">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="bf88d-228">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="bf88d-229">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="bf88d-229">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="bf88d-230">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-230">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="bf88d-231">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="bf88d-231">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="bf88d-232">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="bf88d-232">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>


<!-- URL List -->

[Dokumentation für Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring-Daten für SQL-API von Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ05.png
[AZ06]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ06.png
[AZ07]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ07.png
[AZ08]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ08.png

[SI01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV03.png
