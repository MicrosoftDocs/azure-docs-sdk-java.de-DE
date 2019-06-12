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
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a>Verwendung von Spring Boot Starter mit der SQL-API von Azure Cosmos DB

## <a name="overview"></a>Übersicht

Azure Cosmos DB ist ein global verteilter Datenbankdienst, der Entwicklern durch eine Vielzahl von Standard-APIs wie der SQL-, MongoDB-, Graph- und Tabellen-API die Arbeit mit Daten ermöglicht. Mit Spring Boot Starter von Microsoft können Entwickler Spring Boot-Anwendungen verwenden, die sich mithilfe der SQL-APIs mühelos in Azure Cosmos DB integrieren lassen.

Dieser Artikel zeigt, wie zuerst über das Azure-Portal eine Azure Cosmos DB-Instanz und anschließend mit **[Spring Initializr]** eine benutzerdefinierte Spring Boot-Anwendung erstellt wird. Anschließend wird veranschaulicht, wie [Spring Boot Cosmos DB Starter für Azure] zu Ihrer benutzerdefinierten Anwendung hinzugefügt wird, um Daten mithilfe von Spring Data und der Cosmos DB-SQL-API in Ihrer Azure Cosmos DB-Instanz zu speichern und daraus abzurufen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a>Erstellen einer Azure Cosmos DB-Instanz mithilfe des Azure-Portals

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und klicken Sie auf **+Ressource erstellen**.

   ![Azure-Portal][AZ01]

1. Klicken Sie auf **Datenbanken** und anschließend auf **Azure Cosmos DB**.

   ![Azure-Portal][AZ02]

1. Geben Sie auf der Seite **Azure Cosmos DB** die folgenden Informationen ein:

   * Wählen Sie das **Abonnement**, das Sie für Ihre Datenbank verwenden möchten.
   * Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihre Datenbank erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.
   * Geben Sie einen eindeutigen **Kontonamen** ein, der als URI für Ihre Datenbank verwendet werden soll. Beispiel: *wingtiptoysdata*.
   * Wählen Sie für die API **Core (SQL)** aus.
   * Geben Sie den **Speicherort** für Ihre Datenbank an.

   Wenn Sie diese Optionen angegeben haben, klicken Sie zum Erstellen Ihrer Datenbank auf **Überprüfen und erstellen**.

   ![Azure-Portal][AZ03]

1. Wenn Ihre Datenbank erstellt wurde, wird Sie in Ihrem Azure-**Dashboard** sowie auf den Seiten **Alle Ressourcen** und **Azure Cosmos DB** aufgeführt. Sie können in Ihrer Datenbank auf eine beliebige Stelle klicken, um die Eigenschaftenseite für Ihren Cache zu öffnen.

   ![Azure-Portal][AZ04]

1. Wenn die Eigenschaftenseite für Ihre Datenbank angezeigt wird, klicken Sie auf **Schlüssel**, und kopieren Sie Ihren URI sowie Ihre Zugriffsschlüssel für Ihre Datenbank. Diese Werte verwenden Sie in Ihrer Spring Boot-Anwendung.

   ![Azure-Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr

1. Navigieren Sie zu <https://start.spring.io/>.

1. Geben Sie an, dass Sie ein **Maven-Projekt** mit **Java** generieren möchten, und geben Sie Ihre **Spring Boot**-Version sowie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein. Fügen Sie in den Abhängigkeiten **Azure-Support** hinzu, und klicken Sie anschließend auf die Schaltfläche **Projekt generieren**.

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt**, z.B. *com.example.wintiptoysdata*.
   >

1. Laden Sie das Projekt nach entsprechender Aufforderung in einen Pfad auf dem lokalen Computer herunter, und extrahieren Sie die Dateien.

   ![Extrahieren eines benutzerdefinierten Spring Boot-Projekts][SI02]

1. Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI03]

## <a name="configure-your-spring-boot-application-to-use-the-azure-spring-boot-starter"></a>Konfigurieren der Spring Boot-Anwendung für die Verwendung von Azure Spring Boot Starter

1. Suchen Sie die Datei *pom.xml* im Verzeichnis Ihrer App. Beispiel:

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   Oder

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Suchen der Datei „pom.xml“][PM01]

1. Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Liste der `<dependencies>` hinzu:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-cosmosdb-spring-boot-starter</artifactId>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][PM02]

1. Stellen Sie sicher, dass die Spring Boot-Version die Version ist, die Sie beim Erstellen Ihrer Anwendung mit Spring Initializr ausgewählt haben; zum Beispiel:

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.1.5.RELEASE</version>
      <relativePath/>
   </parent>
   ```

1. Vergewissern Sie sich, dass Sie die aktuelle Version der [Spring Boot Starter-Optionen für Azure](https://github.com/microsoft/azure-spring-boot) verwenden, etwa:

   ```xml
   <azure.version>2.1.6</azure.version>
   ```

1. Speichern und schließen Sie die Datei *pom.xml*.

## <a name="configure-your-spring-boot-application-to-use-your-azure-cosmos-db"></a>Konfigurieren der Spring Boot-Anwendung für die Verwendung von Azure Cosmos DB

1. Suchen Sie die Datei *application.properties* im *Ressourcen*-Verzeichnis Ihrer App. Beispiel:

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   Oder

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Suchen der Datei „application.properties“][RE01]

1. Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften für Ihre Datenbank:

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.cosmosdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.cosmosdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.cosmosdb.database=wingtiptoysdata
   ```

   ![Bearbeiten der Datei „application.properties“][RE02]

1. Speichern und schließen Sie die Datei *application.properties*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Hinzufügen eines Beispielcodes zur Implementierung von grundlegenden Datenbankfunktionen

In diesem Abschnitt erstellen Sie zwei Java-Klassen zum Speichern von Benutzerdaten und ändern dann die Hauptanwendungsklasse, um eine Instanz der *Benutzerklasse* zu erstellen und in der Datenbank zu speichern.

### <a name="define-a-base-class-for-storing-user-data"></a>Definieren einer Basisklasse zum Speichern von Benutzerdaten

1. Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *User.java*.

1. Öffnen Sie in einem Text-Editor die Datei *User.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um eine generische Benutzerklasse zu definieren, die Werte speichert und diese von Ihrer Datenbank abruft:

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

1. Speichern und schließen Sie die Datei *User.java*.

### <a name="define-a-data-repository-interface"></a>Definieren einer Datenrepositoryschnittstelle

1. Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *UserRepository.java*.

1. Öffnen Sie in einem Text-Editor die Datei *UserRepository.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um zur Erweiterung der standardmäßigen DocumentDB-Repositoryschnittstelle eine Benutzerrepositoryschnittstelle zu definieren:

   ```java
   package com.example.wingtiptoysdata;

   import com.microsoft.azure.spring.data.cosmosdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { }
   ```

1. Speichern und schließen Sie die Datei *UserRepository.java*.

### <a name="modify-the-main-application-class"></a>Ändern der Hauptanwendungsklasse

1. Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer Anwendung. Beispiel:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   Oder

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Suchen der Java-Anwendungsdatei][JV01]

1. Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:

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

1. Speichern und schließen Sie die Java-Hauptanwendungsdatei.

## <a name="build-and-test-your-app"></a>Erstellen und Testen der App

1. Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:

   `cd C:\SpringBoot\wingtiptoysdata`

   Oder

   `cd /users/example/home/wingtiptoysdata`

1. Erstellen Sie Ihre Spring Boot-Anwendung mit Maven, und führen Sie sie aus. Beispiel:

   ```shell
   mvnw clean spring-boot:run
   ```

1. Ihre Anwendung zeigt mehrere Laufzeitmeldungen an. Dabei wird eine Meldung wie die folgenden Beispiele angezeigt, die darauf hinweist, dass Werte erfolgreich gespeichert und von Ihrer Datenbank abgerufen wurden.

   ```shell
   Saved user is: Optional[User: 24093cb5-55fe-4d2c-b459-cb8bafdd39fe John Doe]
   ```

   ![Erfolgreiche Ausgabe aus der Anwendung][JV02]

1. OPTIONAL: Sie können im Azure-Portal auf der Eigenschaftenseite für Ihre Datenbank Ihre Azure Cosmos DB-Inhalte anzeigen, indem Sie auf **Daten-Explorer** klicken und dann zum Anzeigen der Inhalte ein Element in der angezeigten Liste auswählen.

   ![Anzeigen von Daten mit dem Document-Explorer][JV03]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.

> [!div class="nextstepaction"]
> [Spring Framework in Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Weitere Ressourcen

Weitere Informationen zur Verwendung von Azure Cosmos DB und Java finden Sie in den folgenden Artikeln:

* [Dokumentation für Azure Cosmos DB]

* [Azure Cosmos DB: Erstellen einer Dokumentdatenbank mit Java und dem Azure-Portal][Build a SQL API app with Java]

* [Spring-Daten für SQL-API von Azure Cosmos DB]

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Spring Boot Cosmos DB Starter für Azure]

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).

**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen. Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt. Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.

<!-- URL List -->

[Dokumentation für Azure Cosmos DB]: /azure/cosmos-db/
[Azure für Java-Entwickler]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring-Daten für SQL-API von Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot Cosmos DB Starter für Azure]: https://github.com/microsoft/azure-spring-boot/tree/master/azure-spring-boot-starters/azure-cosmosdb-spring-boot-starter
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: https://azure.microsoft.com/services/devops/java/ (Arbeiten mit Azure DevOps und Java)
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
