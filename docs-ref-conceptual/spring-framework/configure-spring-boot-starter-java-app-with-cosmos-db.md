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
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: f00afbdd09ce617f863ed758f4bdddcb40701e27
ms.sourcegitcommit: 5bbf64121a99019207ed8cca29280fc5183c7314
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2019
ms.locfileid: "66840837"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="315e1-103">Verwendung von Spring Boot Starter mit der SQL-API von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="315e1-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="315e1-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="315e1-104">Overview</span></span>

<span data-ttu-id="315e1-105">Azure Cosmos DB ist ein global verteilter Datenbankdienst, der Entwicklern durch eine Vielzahl von Standard-APIs wie der SQL-, MongoDB-, Graph- und Tabellen-API die Arbeit mit Daten ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="315e1-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="315e1-106">Mit Spring Boot Starter von Microsoft können Entwickler Spring Boot-Anwendungen verwenden, die sich mithilfe der SQL-APIs mühelos in Azure Cosmos DB integrieren lassen.</span><span class="sxs-lookup"><span data-stu-id="315e1-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="315e1-107">Dieser Artikel zeigt, wie zuerst über das Azure-Portal eine Azure Cosmos DB-Instanz und anschließend mit **[Spring Initializr]** eine benutzerdefinierte Spring Boot-Anwendung erstellt wird. Anschließend wird veranschaulicht, wie [Spring Boot Cosmos DB Starter für Azure] zu Ihrer benutzerdefinierten Anwendung hinzugefügt wird, um Daten mithilfe von Spring Data und der Cosmos DB-SQL-API in Ihrer Azure Cosmos DB-Instanz zu speichern und daraus abzurufen.</span><span class="sxs-lookup"><span data-stu-id="315e1-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom Spring Boot application, and then add the [Spring Boot Cosmos DB Starter for Azure] to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Spring Data and the Cosmos DB SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="315e1-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="315e1-108">Prerequisites</span></span>

<span data-ttu-id="315e1-109">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="315e1-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="315e1-110">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="315e1-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="315e1-111">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="315e1-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="315e1-112">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="315e1-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="315e1-113">Erstellen einer Azure Cosmos DB-Instanz mithilfe des Azure-Portals</span><span class="sxs-lookup"><span data-stu-id="315e1-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="315e1-114">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und klicken Sie auf **+Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="315e1-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Azure-Portal][AZ01]

1. <span data-ttu-id="315e1-116">Klicken Sie auf **Datenbanken** und anschließend auf **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="315e1-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure-Portal][AZ02]

1. <span data-ttu-id="315e1-118">Geben Sie auf der Seite **Azure Cosmos DB** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="315e1-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="315e1-119">Wählen Sie das **Abonnement**, das Sie für Ihre Datenbank verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="315e1-119">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="315e1-120">Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihre Datenbank erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="315e1-120">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="315e1-121">Geben Sie einen eindeutigen **Kontonamen** ein, der als URI für Ihre Datenbank verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="315e1-121">Enter a unique **Account Name**, which you will use as the URI for your database.</span></span> <span data-ttu-id="315e1-122">Beispiel: *wingtiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="315e1-122">For example: *wingtiptoysdata*.</span></span>
   * <span data-ttu-id="315e1-123">Wählen Sie für die API **Core (SQL)** aus.</span><span class="sxs-lookup"><span data-stu-id="315e1-123">Choose **Core (SQL)** for the API.</span></span>
   * <span data-ttu-id="315e1-124">Geben Sie den **Speicherort** für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="315e1-124">Specify the **Location** for your database.</span></span>

   <span data-ttu-id="315e1-125">Wenn Sie diese Optionen angegeben haben, klicken Sie zum Erstellen Ihrer Datenbank auf **Überprüfen und erstellen**.</span><span class="sxs-lookup"><span data-stu-id="315e1-125">When you have specified these options, click **Review + create** to create your database.</span></span>

   ![Azure-Portal][AZ03]

1. <span data-ttu-id="315e1-127">Wenn Ihre Datenbank erstellt wurde, wird Sie in Ihrem Azure-**Dashboard** sowie auf den Seiten **Alle Ressourcen** und **Azure Cosmos DB** aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="315e1-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="315e1-128">Sie können in Ihrer Datenbank auf eine beliebige Stelle klicken, um die Eigenschaftenseite für Ihren Cache zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="315e1-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Azure-Portal][AZ04]

1. <span data-ttu-id="315e1-130">Wenn die Eigenschaftenseite für Ihre Datenbank angezeigt wird, klicken Sie auf **Schlüssel**, und kopieren Sie Ihren URI sowie Ihre Zugriffsschlüssel für Ihre Datenbank. Diese Werte verwenden Sie in Ihrer Spring Boot-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="315e1-130">When the properties page for your database is displayed, click **Keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure-Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="315e1-132">Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="315e1-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="315e1-133">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="315e1-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="315e1-134">Geben Sie an, dass Sie ein **Maven-Projekt** mit **Java** generieren möchten, und geben Sie Ihre **Spring Boot**-Version sowie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein. Fügen Sie in den Abhängigkeiten **Azure-Support** hinzu, und klicken Sie anschließend auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="315e1-134">Specify that you want to generate a **Maven Project** with **Java**, specify your **Spring Boot** version, enter the **Group** and **Artifact** names for your application, add **Azure Support** in the dependencies, and then click the button to **Generate Project**.</span></span>

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="315e1-136">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt**, z.B. *com.example.wintiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="315e1-136">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="315e1-137">Laden Sie das Projekt nach entsprechender Aufforderung in einen Pfad auf dem lokalen Computer herunter, und extrahieren Sie die Dateien.</span><span class="sxs-lookup"><span data-stu-id="315e1-137">When prompted, download the project to a path on your local computer and extract the files.</span></span>

   ![Extrahieren eines benutzerdefinierten Spring Boot-Projekts][SI02]

1. <span data-ttu-id="315e1-139">Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="315e1-139">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI03]

## <a name="configure-your-spring-boot-application-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="315e1-141">Konfigurieren der Spring Boot-Anwendung für die Verwendung von Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="315e1-141">Configure your Spring Boot application to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="315e1-142">Suchen Sie die Datei *pom.xml* im Verzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="315e1-142">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="315e1-143">Oder</span><span class="sxs-lookup"><span data-stu-id="315e1-143">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Suchen der Datei „pom.xml“][PM01]

1. <span data-ttu-id="315e1-145">Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Liste der `<dependencies>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="315e1-145">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-cosmosdb-spring-boot-starter</artifactId>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][PM02]

1. <span data-ttu-id="315e1-147">Stellen Sie sicher, dass die Spring Boot-Version die Version ist, die Sie beim Erstellen Ihrer Anwendung mit Spring Initializr ausgewählt haben; zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="315e1-147">Verify that the Spring Boot version is the version that you chose when you created your application with the Spring Initializr; for example:</span></span>

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.1.5.RELEASE</version>
      <relativePath/>
   </parent>
   ```

1. <span data-ttu-id="315e1-148">Vergewissern Sie sich, dass Sie die aktuelle Version der [Spring Boot Starter-Optionen für Azure](https://github.com/microsoft/azure-spring-boot) verwenden, etwa:</span><span class="sxs-lookup"><span data-stu-id="315e1-148">Verify that you use the most recent [Azure Spring Boot starters](https://github.com/microsoft/azure-spring-boot) version, for example:</span></span>

   ```xml
   <azure.version>2.1.6</azure.version>
   ```

1. <span data-ttu-id="315e1-149">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="315e1-149">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-application-to-use-your-azure-cosmos-db"></a><span data-ttu-id="315e1-150">Konfigurieren der Spring Boot-Anwendung für die Verwendung von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="315e1-150">Configure your Spring Boot application to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="315e1-151">Suchen Sie die Datei *application.properties* im *Ressourcen*-Verzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="315e1-151">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="315e1-152">Oder</span><span class="sxs-lookup"><span data-stu-id="315e1-152">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Suchen der Datei „application.properties“][RE01]

1. <span data-ttu-id="315e1-154">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften für Ihre Datenbank:</span><span class="sxs-lookup"><span data-stu-id="315e1-154">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.cosmosdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.cosmosdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.cosmosdb.database=wingtiptoysdata
   ```

   ![Bearbeiten der Datei „application.properties“][RE02]

1. <span data-ttu-id="315e1-156">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="315e1-156">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="315e1-157">Hinzufügen eines Beispielcodes zur Implementierung von grundlegenden Datenbankfunktionen</span><span class="sxs-lookup"><span data-stu-id="315e1-157">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="315e1-158">In diesem Abschnitt erstellen Sie zwei Java-Klassen zum Speichern von Benutzerdaten und ändern dann die Hauptanwendungsklasse, um eine Instanz der *Benutzerklasse* zu erstellen und in der Datenbank zu speichern.</span><span class="sxs-lookup"><span data-stu-id="315e1-158">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the *User* class and save it to your database.</span></span>

### <a name="define-a-base-class-for-storing-user-data"></a><span data-ttu-id="315e1-159">Definieren einer Basisklasse zum Speichern von Benutzerdaten</span><span class="sxs-lookup"><span data-stu-id="315e1-159">Define a base class for storing user data</span></span>

1. <span data-ttu-id="315e1-160">Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *User.java*.</span><span class="sxs-lookup"><span data-stu-id="315e1-160">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="315e1-161">Öffnen Sie in einem Text-Editor die Datei *User.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um eine generische Benutzerklasse zu definieren, die Werte speichert und diese von Ihrer Datenbank abruft:</span><span class="sxs-lookup"><span data-stu-id="315e1-161">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="315e1-162">Speichern und schließen Sie die Datei *User.java*.</span><span class="sxs-lookup"><span data-stu-id="315e1-162">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="315e1-163">Definieren einer Datenrepositoryschnittstelle</span><span class="sxs-lookup"><span data-stu-id="315e1-163">Define a data repository interface</span></span>

1. <span data-ttu-id="315e1-164">Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="315e1-164">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="315e1-165">Öffnen Sie in einem Text-Editor die Datei *UserRepository.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um zur Erweiterung der standardmäßigen DocumentDB-Repositoryschnittstelle eine Benutzerrepositoryschnittstelle zu definieren:</span><span class="sxs-lookup"><span data-stu-id="315e1-165">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   import com.microsoft.azure.spring.data.cosmosdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { }
   ```

1. <span data-ttu-id="315e1-166">Speichern und schließen Sie die Datei *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="315e1-166">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="315e1-167">Ändern der Hauptanwendungsklasse</span><span class="sxs-lookup"><span data-stu-id="315e1-167">Modify the main application class</span></span>

1. <span data-ttu-id="315e1-168">Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer Anwendung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="315e1-168">Locate the main application Java file in the package directory of your application, for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="315e1-169">Oder</span><span class="sxs-lookup"><span data-stu-id="315e1-169">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Suchen der Java-Anwendungsdatei][JV01]

1. <span data-ttu-id="315e1-171">Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="315e1-171">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
    package com.example.wingtiptoysdata;

    import org.springframework.boot.CommandLineRunner;
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    import java.util.Optional;
    import java.util.UUID;

    @SpringBootApplication
    public class WingtiptoysdataApplication implements CommandLineRunner {

        private final UserRepository repository;

        public WingtiptoysdataApplication(UserRepository repository) {
            this.repository = repository;
        }

        public static void main(String[] args) {
            // Execute the command line runner.
            SpringApplication.run(WingtiptoysdataApplication.class, args);
            System.exit(0);
        }

        public void run(String... args) throws Exception {
            // Create a unique identifier.
            String uuid = UUID.randomUUID().toString();

            // Create a new User class.
            final User testUser = new User(uuid, "John", "Doe");

            // For this example, remove all of the existing records.
            repository.deleteAll();

            // Save the User class to the Azure database.
            repository.save(testUser);

            // Retrieve the database record for the User class you just saved by ID.
            Optional<User> result = repository.findById(testUser.getId());

            // Display the results of the database record retrieval.
            System.out.println("\nSaved user is: " + result + "\n")
        }
    }
   ```

1. <span data-ttu-id="315e1-172">Speichern und schließen Sie die Java-Hauptanwendungsdatei.</span><span class="sxs-lookup"><span data-stu-id="315e1-172">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="315e1-173">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="315e1-173">Build and test your app</span></span>

1. <span data-ttu-id="315e1-174">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="315e1-174">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="315e1-175">Oder</span><span class="sxs-lookup"><span data-stu-id="315e1-175">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="315e1-176">Erstellen Sie Ihre Spring Boot-Anwendung mit Maven, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="315e1-176">Build your Spring Boot application with Maven and run it, for example:</span></span>

   ```shell
   mvnw clean spring-boot:run
   ```

1. <span data-ttu-id="315e1-177">Ihre Anwendung zeigt mehrere Laufzeitmeldungen an. Dabei wird eine Meldung wie die folgenden Beispiele angezeigt, die darauf hinweist, dass Werte erfolgreich gespeichert und von Ihrer Datenbank abgerufen wurden.</span><span class="sxs-lookup"><span data-stu-id="315e1-177">Your application will display several runtime messages, and it will display a message like the following examples to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ```shell
   Saved user is: Optional[User: 24093cb5-55fe-4d2c-b459-cb8bafdd39fe John Doe]
   ```

   ![Erfolgreiche Ausgabe aus der Anwendung][JV02]

1. <span data-ttu-id="315e1-179">OPTIONAL: Sie können im Azure-Portal auf der Eigenschaftenseite für Ihre Datenbank Ihre Azure Cosmos DB-Inhalte anzeigen, indem Sie auf **Daten-Explorer** klicken und dann zum Anzeigen der Inhalte ein Element in der angezeigten Liste auswählen.</span><span class="sxs-lookup"><span data-stu-id="315e1-179">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Anzeigen von Daten mit dem Document-Explorer][JV03]

## <a name="next-steps"></a><span data-ttu-id="315e1-181">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="315e1-181">Next steps</span></span>

<span data-ttu-id="315e1-182">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="315e1-182">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="315e1-183">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="315e1-183">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="315e1-184">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="315e1-184">Additional Resources</span></span>

<span data-ttu-id="315e1-185">Weitere Informationen zur Verwendung von Azure Cosmos DB und Java finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="315e1-185">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="315e1-186">[Dokumentation für Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="315e1-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="315e1-187">[Azure Cosmos DB: Erstellen einer Dokumentdatenbank mit Java und dem Azure-Portal][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="315e1-187">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="315e1-188">[Spring-Daten für SQL-API von Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="315e1-188">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="315e1-189">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="315e1-189">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="315e1-190">[Spring Boot Cosmos DB Starter für Azure]</span><span class="sxs-lookup"><span data-stu-id="315e1-190">[Spring Boot Cosmos DB Starter for Azure]</span></span>

* [<span data-ttu-id="315e1-191">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="315e1-191">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="315e1-192">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="315e1-192">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="315e1-193">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="315e1-193">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="315e1-194">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="315e1-194">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="315e1-195">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="315e1-195">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="315e1-196">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="315e1-196">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="315e1-197">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="315e1-197">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Dokumentation für Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure für Java-Entwickler]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring-Daten für SQL-API von Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot Cosmos DB Starter für Azure]: https://github.com/microsoft/azure-spring-boot/tree/master/azure-spring-boot-starters/azure-cosmosdb-spring-boot-starter
[Spring Boot Cosmos DB Starter for Azure]: https://github.com/microsoft/azure-spring-boot/tree/master/azure-spring-boot-starters/azure-cosmosdb-spring-boot-starter
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: https://azure.microsoft.com/services/devops/java/ (Arbeiten mit Azure DevOps und Java)
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
