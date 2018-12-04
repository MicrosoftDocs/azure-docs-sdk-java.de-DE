---
title: Verwendung von Spring Boot Starter mit der SQL-API von Azure Cosmos DB
description: Hier erfahren Sie, wie eine mit dem Spring Boot-Initialisierer erstellte Anwendung mit der SQL-API von Azure Cosmos DB konfiguriert wird.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 6675b3f76f19ec0bfdb28351681258b8c4792104
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339104"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="8ae98-103">Verwendung von Spring Boot Starter mit der SQL-API von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8ae98-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="8ae98-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="8ae98-104">Overview</span></span>

<span data-ttu-id="8ae98-105">Azure Cosmos DB ist ein global verteilter Datenbankdienst, der Entwicklern durch eine Vielzahl von Standard-APIs wie der SQL-, MongoDB-, Graph- und Tabellen-API die Arbeit mit Daten ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="8ae98-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="8ae98-106">Mit Spring Boot Starter von Microsoft können Entwickler Spring Boot-Anwendungen verwenden, die sich mithilfe der SQL-APIs mühelos in Azure Cosmos DB integrieren lassen.</span><span class="sxs-lookup"><span data-stu-id="8ae98-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="8ae98-107">Dieser Artikel zeigt, wie zuerst über das Azure-Portal eine Azure Cosmos DB-Instanz und anschließend mit **[Spring Initializr]** eine benutzerdefinierte Java-Anwendung erstellt wird. Anschließend wird veranschaulicht, wie Spring Boot Starter-Funktionen zu Ihrer benutzerdefinierten Anwendung hinzugefügt werden, um Daten mithilfe der SQL-API in Ihrer Azure Cosmos DB-Instanz zu speichern und daraus abzurufen.</span><span class="sxs-lookup"><span data-stu-id="8ae98-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ae98-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="8ae98-108">Prerequisites</span></span>

<span data-ttu-id="8ae98-109">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="8ae98-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="8ae98-110">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="8ae98-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8ae98-111">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="8ae98-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="8ae98-112">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="8ae98-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="8ae98-113">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="8ae98-113">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="8ae98-114">Erstellen einer Azure Cosmos DB-Instanz mithilfe des Azure-Portals</span><span class="sxs-lookup"><span data-stu-id="8ae98-114">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="8ae98-115">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und klicken Sie auf **+Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="8ae98-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Azure-Portal][AZ01]

1. <span data-ttu-id="8ae98-117">Klicken Sie auf **Datenbanken** und anschließend auf **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="8ae98-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure-Portal][AZ02]

1. <span data-ttu-id="8ae98-119">Geben Sie auf der Seite **Azure Cosmos DB** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="8ae98-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="8ae98-120">Geben Sie eine eindeutige **ID** ein, die als URI für Ihre Datenbank verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="8ae98-120">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="8ae98-121">Beispiel: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="8ae98-121">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="8ae98-122">Wählen Sie für die API **SQL** aus.</span><span class="sxs-lookup"><span data-stu-id="8ae98-122">Choose **SQL** for the API.</span></span>
   * <span data-ttu-id="8ae98-123">Wählen Sie das **Abonnement**, das Sie für Ihre Datenbank verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="8ae98-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="8ae98-124">Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihre Datenbank erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="8ae98-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="8ae98-125">Geben Sie den **Speicherort** für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="8ae98-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="8ae98-126">Wenn Sie diese Optionen angegeben haben, klicken Sie zum Erstellen Ihrer Datenbank auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="8ae98-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Azure-Portal][AZ03]

1. <span data-ttu-id="8ae98-128">Wenn Ihre Datenbank erstellt wurde, wird Sie in Ihrem Azure-**Dashboard** sowie auf den Seiten **Alle Ressourcen** und **Azure Cosmos DB** aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="8ae98-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="8ae98-129">Sie können in Ihrer Datenbank auf eine beliebige Stelle klicken, um die Eigenschaftenseite für Ihren Cache zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="8ae98-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Azure-Portal][AZ04]

1. <span data-ttu-id="8ae98-131">Wenn die Eigenschaftenseite für Ihre Datenbank angezeigt wird, klicken Sie auf **Zugriffsschlüssel**, und kopieren Sie Ihren URI sowie Ihre Zugriffsschlüssel für Ihre Datenbank. Diese Werte verwenden Sie in Ihrer Spring Boot-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="8ae98-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure-Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="8ae98-133">Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="8ae98-133">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="8ae98-134">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="8ae98-134">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="8ae98-135">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und geben Sie Ihre **Spring Boot**-Version an. Klicken Sie anschließend auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="8ae98-135">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version, and then click the button to **Generate Project**.</span></span>

   > [!IMPORTANT]
   >
   > <span data-ttu-id="8ae98-136">An den APIs in Spring Boot Version 2.0.n, die zum Durchführen der Schritte in diesem Artikel verwendet werden, sind mehrere Breaking Changes erfolgt.</span><span class="sxs-lookup"><span data-stu-id="8ae98-136">There were several breaking changes to the APIs in Spring Boot version 2.0.n, which will be used to complete the steps in this article.</span></span> <span data-ttu-id="8ae98-137">Sie können weiterhin eine der Spring Boot 1.5.n-Versionen verwenden, um die Schritte in diesem Tutorial auszuführen. Die Unterschiede sind ggf. hervorgehoben.</span><span class="sxs-lookup"><span data-stu-id="8ae98-137">You can still use one of the Spring Boot 1.5.n versions to complete the steps in this tutorial, and the differences will be highlighted when necessary.</span></span>
   >

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="8ae98-139">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt**, z.B. *com.example.wintiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="8ae98-139">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="8ae98-140">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="8ae98-140">When prompted, download the project to a path on your local computer.</span></span>

   ![Herunterladen eines benutzerdefinierten Spring Boot-Projekts][SI02]

1. <span data-ttu-id="8ae98-142">Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="8ae98-142">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="8ae98-144">Konfigurieren der Spring Boot-App für die Verwendung von Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="8ae98-144">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="8ae98-145">Suchen Sie die Datei *pom.xml* im Verzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8ae98-145">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="8ae98-146">Oder</span><span class="sxs-lookup"><span data-stu-id="8ae98-146">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Suchen der Datei „pom.xml“][PM01]

1. <span data-ttu-id="8ae98-148">Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Liste der `<dependencies>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="8ae98-148">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>2.0.4</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][PM02]

   > [!IMPORTANT]
   >
   > <span data-ttu-id="8ae98-150">Wenn Sie eine der Spring Boot-1.5.n-Versionen zum Abschließen dieses Tutorials verwenden, müssen Sie die ältere Version des Azure Cosmos DB-Starters angeben; zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8ae98-150">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to specify the older version of the Azure Cosmos DB starter; for example:</span></span>
   >
   > ```xml
   > <dependency>
   >   <groupId>com.microsoft.azure</groupId>
   >   <artifactId>azure-documentdb-spring-boot-starter</artifactId>
   >   <version>0.1.4</version>
   > </dependency>
   > ```

1. <span data-ttu-id="8ae98-151">Stellen Sie sicher, dass die Spring Boot-Version die Version ist, die Sie beim Erstellen Ihrer Anwendung mit Spring Initializr ausgewählt haben; zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8ae98-151">Verify that the Spring Boot version is the version that you chose when you created your application with the Spring Initializr; for example:</span></span>

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.1.RELEASE</version>
      <relativePath/>
   </parent>
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="8ae98-152">Wenn Sie eine der Spring Boot-1.5.n-Versionen zum Abschließen dieses Tutorials verwenden, müssen Sie sicherstellen, dass die richtige Version verwendet wird; zum Beispiel: `<version>1.5.14.RELEASE</version>`.</span><span class="sxs-lookup"><span data-stu-id="8ae98-152">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to verify the correct version; for example: `<version>1.5.14.RELEASE</version>`.</span></span>
   >

1. <span data-ttu-id="8ae98-153">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="8ae98-153">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="8ae98-154">Konfigurieren der Spring Boot-App für die Verwendung von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8ae98-154">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="8ae98-155">Suchen Sie die Datei *application.properties* im *Ressourcen*-Verzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8ae98-155">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="8ae98-156">Oder</span><span class="sxs-lookup"><span data-stu-id="8ae98-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Suchen der Datei „application.properties“][RE01]

1. <span data-ttu-id="8ae98-158">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften für Ihre Datenbank:</span><span class="sxs-lookup"><span data-stu-id="8ae98-158">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Bearbeiten der Datei „application.properties“][RE02]

1. <span data-ttu-id="8ae98-160">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="8ae98-160">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="8ae98-161">Hinzufügen eines Beispielcodes zur Implementierung von grundlegenden Datenbankfunktionen</span><span class="sxs-lookup"><span data-stu-id="8ae98-161">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="8ae98-162">In diesem Abschnitt erstellen Sie zwei Java-Klassen zum Speichern von Benutzerdaten und ändern dann die Hauptanwendungsklasse, um eine Instanz der Benutzerklasse zu erstellen und in der Datenbank zu speichern.</span><span class="sxs-lookup"><span data-stu-id="8ae98-162">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="8ae98-163">Definieren einer einfachen Klasse zum Speichern von Benutzerdaten</span><span class="sxs-lookup"><span data-stu-id="8ae98-163">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="8ae98-164">Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *User.java*.</span><span class="sxs-lookup"><span data-stu-id="8ae98-164">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="8ae98-165">Öffnen Sie in einem Text-Editor die Datei *User.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um eine generische Benutzerklasse zu definieren, die Werte speichert und diese von Ihrer Datenbank abruft:</span><span class="sxs-lookup"><span data-stu-id="8ae98-165">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   // Define a generic User class.
   public class User {
      private String id;
      private String firstName;
      private String lastName;
   
      public User() {
      }
   
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
         return String.format("User: %s %s %s", id, firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="8ae98-166">Speichern und schließen Sie die Datei *User.java*.</span><span class="sxs-lookup"><span data-stu-id="8ae98-166">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="8ae98-167">Definieren einer Datenrepositoryschnittstelle</span><span class="sxs-lookup"><span data-stu-id="8ae98-167">Define a data repository interface</span></span>

1. <span data-ttu-id="8ae98-168">Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="8ae98-168">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="8ae98-169">Öffnen Sie in einem Text-Editor die Datei *UserRepository.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um zur Erweiterung der standardmäßigen DocumentDB-Repositoryschnittstelle eine Benutzerrepositoryschnittstelle zu definieren:</span><span class="sxs-lookup"><span data-stu-id="8ae98-169">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. <span data-ttu-id="8ae98-170">Speichern und schließen Sie die Datei *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="8ae98-170">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="8ae98-171">Ändern der Hauptanwendungsklasse</span><span class="sxs-lookup"><span data-stu-id="8ae98-171">Modify the main application class</span></span>

1. <span data-ttu-id="8ae98-172">Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8ae98-172">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="8ae98-173">Oder</span><span class="sxs-lookup"><span data-stu-id="8ae98-173">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Suchen der Java-Anwendungsdatei][JV01]

1. <span data-ttu-id="8ae98-175">Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="8ae98-175">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   // These imports are required for the application.
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   // These imports are only used to create an ID for this example.
   import java.util.Date;
   import java.text.SimpleDateFormat;

   @SpringBootApplication
   public class wingtiptoysdataApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;

      public static void main(String[] args) {
         // Execute the command line runner.
         SpringApplication.run(wingtiptoysdataApplication.class, args);
         System.exit(0);
      }

      public void run(String... args) throws Exception {
         // Create a simple date/time ID.
         SimpleDateFormat userId = new SimpleDateFormat("yyyyMMddHHmmssSSS");
         Date currentDate = new Date();

         // Create a new User class.
         final User testUser = new User(userId.format(currentDate), "Gena", "Soto");

         // For this example, remove all of the existing records.
         repository.deleteAll();

         // Save the User class to the Azure database.
         repository.save(testUser);
      
         // Retrieve the database record for the User class you just saved by ID.
         // final User result = repository.findOne(testUser.getId());
         final User result = repository.findById(testUser.getId()).get();

         // Display the results of the database record retrieval.
         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

   > [!IMPORTANT]
   >
   > <span data-ttu-id="8ae98-176">Wenn Sie eine der Spring Boot-1.5.n-Versionen zum Abschließen dieses Tutorials verwenden, müssen Sie die `final User result = repository.findById(testUser.getId()).get();`-Syntax durch `final User result = repository.findOne(testUser.getId());` ersetzen.</span><span class="sxs-lookup"><span data-stu-id="8ae98-176">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to replace the `final User result = repository.findById(testUser.getId()).get();` syntax with `final User result = repository.findOne(testUser.getId());`.</span></span>
   >

1. <span data-ttu-id="8ae98-177">Speichern und schließen Sie die Java-Hauptanwendungsdatei.</span><span class="sxs-lookup"><span data-stu-id="8ae98-177">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="8ae98-178">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="8ae98-178">Build and test your app</span></span>

1. <span data-ttu-id="8ae98-179">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8ae98-179">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="8ae98-180">Oder</span><span class="sxs-lookup"><span data-stu-id="8ae98-180">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="8ae98-181">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8ae98-181">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="8ae98-182">Ihre Anwendung zeigt mehrere Laufzeitmeldungen an. Dabei wird eine Meldung wie die folgenden Beispiele angezeigt, die darauf hinweist, dass Werte erfolgreich gespeichert und von Ihrer Datenbank abgerufen wurden.</span><span class="sxs-lookup"><span data-stu-id="8ae98-182">Your application will display several runtime messages, and it will display a message like the following examples to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ```
   User: 20170724025215132 Gena Soto
   ```

   ![Erfolgreiche Ausgabe aus der Anwendung][JV02]

1. <span data-ttu-id="8ae98-184">OPTIONAL: Im Azure-Portal können Sie auf der Eigenschaftenseite die Inhalte von Azure Cosmos DB für Ihre Datenbank anzeigen, indem Sie auf **Daten-Explorer** klicken und dann zum Anzeigen der Inhalte ein Element in der angezeigten Liste auswählen.</span><span class="sxs-lookup"><span data-stu-id="8ae98-184">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Anzeigen von Daten mit dem Document-Explorer][JV03]

## <a name="next-steps"></a><span data-ttu-id="8ae98-186">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="8ae98-186">Next steps</span></span>

<span data-ttu-id="8ae98-187">Weitere Informationen zur Verwendung von Azure Cosmos DB und Java finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="8ae98-187">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="8ae98-188">[Dokumentation für Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="8ae98-188">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="8ae98-189">[Azure Cosmos DB: Erstellen einer Dokumentdatenbank mit Java und dem Azure-Portal][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="8ae98-189">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="8ae98-190">[Spring-Daten für SQL-API von Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="8ae98-190">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="8ae98-191">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="8ae98-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="8ae98-192">[Spring Boot Document DB Starter für Azure]</span><span class="sxs-lookup"><span data-stu-id="8ae98-192">[Spring Boot Document DB Starter for Azure]</span></span>

* [<span data-ttu-id="8ae98-193">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8ae98-193">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="8ae98-194">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="8ae98-194">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="8ae98-195">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="8ae98-195">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="8ae98-196">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="8ae98-196">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="8ae98-197">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="8ae98-197">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="8ae98-198">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="8ae98-198">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="8ae98-199">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="8ae98-199">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Dokumentation für Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring-Daten für SQL-API von Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot Document DB Starter für Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[Spring Boot Document DB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
[Java Tools for Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
