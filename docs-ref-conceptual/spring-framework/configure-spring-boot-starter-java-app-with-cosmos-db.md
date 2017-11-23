---
title: Verwendung von Spring Boot Starter mit einer DocumentDB-API von Azure Cosmos DB
description: Erfahren Sie, wie eine Anwendung, die mit dem Spring Boot-Initialisierer erstellt wurde, mit der DocumentDB-API von Azure Cosmos DB konfiguriert wird.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Spring Starter, Cosmos DB, DocumentDB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a80ac6be1064e40cd0b693ac4e6c0b1a9723cfc4
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-use-the-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="c9689-104">Verwendung von Spring Boot Starter mit der DocumentDB-API von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9689-104">How to use the Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="c9689-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="c9689-105">Overview</span></span>

<span data-ttu-id="c9689-106">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="c9689-106">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="c9689-107">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="c9689-107">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="c9689-108">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="c9689-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="c9689-109">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="c9689-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="c9689-110">Azure Cosmos DB ist ein global verteilter Datenbankdienst, der Entwicklern durch eine Vielzahl von Standard-APIs wie der DocumentDB-, MongoDB-, Graph- und Tabellen-API die Arbeit mit Daten ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="c9689-110">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="c9689-111">Mit Spring Boot Starter von Microsoft können Entwickler Spring Boot-Anwendungen verwenden, die sich mithilfe von DocumentDB-APIs mühelos in Azure Cosmos DB integrieren lassen.</span><span class="sxs-lookup"><span data-stu-id="c9689-111">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="c9689-112">Dieser Artikel zeigt, wie eine Azure Cosmos DB-Instanz mithilfe des Azure-Portals erstellt, und anschließend mit **Spring Initializr** eine benutzerdefinierte Java-Anwendung erstellt wird. Anschließend wird veranschaulicht, wie Spring Boot Starter-Funktionen zu Ihrer benutzerdefinierten Anwendung hinzugefügt werden, um Daten mithilfe der DocumentDB-API zu speichern und von Ihrer Azure Cosmos DB-Instanz abzurufen.</span><span class="sxs-lookup"><span data-stu-id="c9689-112">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **Spring Initializr** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9689-113">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c9689-113">Prerequisites</span></span>

<span data-ttu-id="c9689-114">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="c9689-114">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="c9689-115">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="c9689-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="c9689-116">[Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="c9689-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="c9689-117">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="c9689-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="c9689-118">Erstellen einer Azure Cosmos DB-Instanz mithilfe des Azure-Portals</span><span class="sxs-lookup"><span data-stu-id="c9689-118">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="c9689-119">Navigieren Sie unter <https://portal.azure.com/> zum Azure-Portal, und klicken Sie auf **+Neu**.</span><span class="sxs-lookup"><span data-stu-id="c9689-119">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure-Portal][AZ01]

1. <span data-ttu-id="c9689-121">Klicken Sie auf **Datenbanken** und anschließend auf **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="c9689-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure-Portal][AZ02]

1. <span data-ttu-id="c9689-123">Geben Sie auf der Seite **Azure Cosmos DB** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="c9689-123">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="c9689-124">Geben Sie eine eindeutige **ID** ein, die als URI für Ihre Datenbank verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="c9689-124">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="c9689-125">Beispiel: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="c9689-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="c9689-126">Wählen Sie **SQL (Document DB)** für die API aus.</span><span class="sxs-lookup"><span data-stu-id="c9689-126">Choose **SQL (Document DB)** for the API.</span></span>
   * <span data-ttu-id="c9689-127">Wählen Sie das **Abonnement**, das Sie für Ihre Datenbank verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="c9689-127">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="c9689-128">Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihre Datenbank erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="c9689-128">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="c9689-129">Geben Sie den **Speicherort** für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="c9689-129">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="c9689-130">Wenn Sie diese Optionen angegeben haben, klicken Sie zum Erstellen Ihrer Datenbank auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c9689-130">When you have specified these options, click **Create** to create your database.</span></span>

   ![Azure-Portal][AZ03]

1. <span data-ttu-id="c9689-132">Wenn Ihre Datenbank erstellt wurde, wird Sie in Ihrem Azure-**Dashboard** sowie auf den Seiten **Alle Ressourcen** und **Azure Cosmos DB** aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="c9689-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="c9689-133">Sie können in Ihrer Datenbank auf eine beliebige Stelle klicken, um die Eigenschaftenseite für Ihren Cache zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="c9689-133">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Azure-Portal][AZ04]

1. <span data-ttu-id="c9689-135">Wenn die Eigenschaftenseite für Ihre Datenbank angezeigt wird, klicken Sie auf **Zugriffsschlüssel**, und kopieren Sie Ihren URI sowie Ihre Zugriffsschlüssel für Ihre Datenbank. Diese Werte verwenden Sie in Ihrer Spring Boot-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c9689-135">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure-Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="c9689-137">Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="c9689-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="c9689-138">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="c9689-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="c9689-139">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="c9689-139">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the button to **Generate Project**.</span></span>

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="c9689-141">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt**, z.B. *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="c9689-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="c9689-142">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="c9689-142">When prompted, download the project to a path on your local computer.</span></span>

   ![Herunterladen eines benutzerdefinierten Spring Boot-Projekts][SI02]

1. <span data-ttu-id="c9689-144">Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="c9689-144">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="c9689-146">Konfigurieren der Spring Boot-App für die Verwendung von Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="c9689-146">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="c9689-147">Suchen Sie die Datei *pom.xml* im Verzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c9689-147">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="c9689-148">Oder</span><span class="sxs-lookup"><span data-stu-id="c9689-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Suchen der Datei „pom.xml“][PM01]

1. <span data-ttu-id="c9689-150">Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Liste der `<dependencies>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="c9689-150">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][PM02]

1. <span data-ttu-id="c9689-152">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="c9689-152">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="c9689-153">Konfigurieren der Spring Boot-App für die Verwendung von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9689-153">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="c9689-154">Suchen Sie die Datei *application.properties* im *Ressourcen*-Verzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c9689-154">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="c9689-155">Oder</span><span class="sxs-lookup"><span data-stu-id="c9689-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Suchen der Datei „application.properties“][RE01]

1. <span data-ttu-id="c9689-157">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften für Ihre Datenbank:</span><span class="sxs-lookup"><span data-stu-id="c9689-157">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Bearbeiten der Datei „application.properties“][RE02]

1. <span data-ttu-id="c9689-159">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="c9689-159">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="c9689-160">Hinzufügen eines Beispielcodes zur Implementierung von grundlegenden Datenbankfunktionen</span><span class="sxs-lookup"><span data-stu-id="c9689-160">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="c9689-161">In diesem Abschnitt erstellen Sie zwei Java-Klassen zum Speichern von Benutzerdaten und ändern dann die Hauptanwendungsklasse, um eine Instanz der Benutzerklasse zu erstellen und in der Datenbank zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c9689-161">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="c9689-162">Definieren einer einfachen Klasse zum Speichern von Benutzerdaten</span><span class="sxs-lookup"><span data-stu-id="c9689-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="c9689-163">Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *User.java*.</span><span class="sxs-lookup"><span data-stu-id="c9689-163">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="c9689-164">Öffnen Sie in einem Text-Editor die Datei *User.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um eine generische Benutzerklasse zu definieren, die Werte speichert und diese von Ihrer Datenbank abruft:</span><span class="sxs-lookup"><span data-stu-id="c9689-164">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="c9689-165">Speichern und schließen Sie die Datei *User.java*.</span><span class="sxs-lookup"><span data-stu-id="c9689-165">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="c9689-166">Definieren einer Datenrepositoryschnittstelle</span><span class="sxs-lookup"><span data-stu-id="c9689-166">Define a data repository interface</span></span>

1. <span data-ttu-id="c9689-167">Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="c9689-167">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="c9689-168">Öffnen Sie in einem Text-Editor die Datei *UserRepository.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um zur Erweiterung der standardmäßigen DocumentDB-Repositoryschnittstelle eine Benutzerrepositoryschnittstelle zu definieren:</span><span class="sxs-lookup"><span data-stu-id="c9689-168">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="c9689-169">Speichern und schließen Sie die Datei *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="c9689-169">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="c9689-170">Ändern der Hauptanwendungsklasse</span><span class="sxs-lookup"><span data-stu-id="c9689-170">Modify the main application class</span></span>

1. <span data-ttu-id="c9689-171">Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c9689-171">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="c9689-172">Oder</span><span class="sxs-lookup"><span data-stu-id="c9689-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Suchen der Java-Anwendungsdatei][JV01]

1. <span data-ttu-id="c9689-174">Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="c9689-174">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="c9689-175">Speichern und schließen Sie die Java-Hauptanwendungsdatei.</span><span class="sxs-lookup"><span data-stu-id="c9689-175">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="c9689-176">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="c9689-176">Build and test your app</span></span>

1. <span data-ttu-id="c9689-177">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c9689-177">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="c9689-178">Oder</span><span class="sxs-lookup"><span data-stu-id="c9689-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="c9689-179">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c9689-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="c9689-180">Die Anwendung zeigt mehrere Laufzeitmeldungen an. Dabei sollte die Meldung `User: testFirstName testLastName` angezeigt werden, die darauf hinweist, dass Werte erfolgreich gespeichert und von Ihrer Datenbank abgerufen wurden.</span><span class="sxs-lookup"><span data-stu-id="c9689-180">Your application will display several runtime messages, and you should see the message `User: testFirstName testLastName` displayed to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Erfolgreiche Ausgabe aus der Anwendung][JV02]

1. <span data-ttu-id="c9689-182">OPTIONAL: Im Azure-Portal können Sie auf der Eigenschaftenseite die Inhalte von Azure Cosmos DB für Ihre Datenbank anzeigen, indem Sie auf **Dokument-Explorer** klicken und dann zum Anzeigen der Inhalte ein Element in der angezeigten Liste auswählen.</span><span class="sxs-lookup"><span data-stu-id="c9689-182">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Document Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Anzeigen von Daten mit dem Document-Explorer][JV03]

## <a name="next-steps"></a><span data-ttu-id="c9689-184">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c9689-184">Next steps</span></span>

<span data-ttu-id="c9689-185">Weitere Informationen zur Verwendung von Azure Cosmos DB und Java finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="c9689-185">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="c9689-186">[Dokumentation für Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="c9689-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="c9689-187">[Azure Cosmos DB: Erstellen einer DocumentDB-API-App mit Java und dem Azure-Portal][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="c9689-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and the Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="c9689-188">Weitere Informationen zur Verwendung von Spring Boot in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="c9689-188">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="c9689-189">Spring Boot DocumenDB Starter für Azure</span><span class="sxs-lookup"><span data-stu-id="c9689-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="c9689-190">Bereitstellen einer Spring Boot-Anwendung in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c9689-190">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="c9689-191">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="c9689-191">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="c9689-192">Weitere Informationen zum Verwenden von Azure mit Java finden Sie im [Azure Java Developer Center] und in den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c9689-192">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Dokumentation für Azure Cosmos DB]: /azure/cosmos-db/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV03.png
