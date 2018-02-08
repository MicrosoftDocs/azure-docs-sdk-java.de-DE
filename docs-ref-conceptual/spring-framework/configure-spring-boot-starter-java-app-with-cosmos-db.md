---
title: Verwendung von Spring Boot Starter mit einer DocumentDB-API von Azure Cosmos DB
description: Erfahren Sie, wie eine Anwendung, die mit dem Spring Boot-Initialisierer erstellt wurde, mit der DocumentDB-API von Azure Cosmos DB konfiguriert wird.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm;yungez;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 8190a7c45443ead9855d5a62194e02d7e9a919ee
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Verwendung von Spring Boot Starter mit der DocumentDB-API von Azure Cosmos DB

## <a name="overview"></a>Übersicht

Azure Cosmos DB ist ein global verteilter Datenbankdienst, der Entwicklern durch eine Vielzahl von Standard-APIs wie der DocumentDB-, MongoDB-, Graph- und Tabellen-API die Arbeit mit Daten ermöglicht. Mit Spring Boot Starter von Microsoft können Entwickler Spring Boot-Anwendungen verwenden, die sich mithilfe von DocumentDB-APIs mühelos in Azure Cosmos DB integrieren lassen.

Dieser Artikel zeigt, wie zuerst über das Azure-Portal eine Azure Cosmos DB-Instanz und anschließend mit **[Spring Initializr]** eine benutzerdefinierte Java-Anwendung erstellt wird. Anschließend wird veranschaulicht, wie Spring Boot Starter-Funktionen zu Ihrer benutzerdefinierten Anwendung hinzugefügt werden, um Daten mithilfe der DocumentDB-API zu speichern und aus Ihrer Azure Cosmos DB-Instanz abzurufen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
* [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), Version 1.7 oder höher
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a>Erstellen einer Azure Cosmos DB-Instanz mithilfe des Azure-Portals

1. Navigieren Sie unter <https://portal.azure.com/> zum Azure-Portal, und klicken Sie auf **+Neu**.

   ![Azure-Portal][AZ01]

1. Klicken Sie auf **Datenbanken** und anschließend auf **Azure Cosmos DB**.

   ![Azure-Portal][AZ02]

1. Geben Sie auf der Seite **Azure Cosmos DB** die folgenden Informationen ein:

   * Geben Sie eine eindeutige **ID** ein, die als URI für Ihre Datenbank verwendet werden soll. Beispiel: *wingtiptoysdata.documents.azure.com*.
   * Wählen Sie **SQL (Document DB)** für die API aus.
   * Wählen Sie das **Abonnement**, das Sie für Ihre Datenbank verwenden möchten.
   * Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihre Datenbank erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.
   * Geben Sie den **Speicherort** für Ihre Datenbank an.
   
   Wenn Sie diese Optionen angegeben haben, klicken Sie zum Erstellen Ihrer Datenbank auf **Erstellen**.

   ![Azure-Portal][AZ03]

1. Wenn Ihre Datenbank erstellt wurde, wird Sie in Ihrem Azure-**Dashboard** sowie auf den Seiten **Alle Ressourcen** und **Azure Cosmos DB** aufgeführt. Sie können in Ihrer Datenbank auf eine beliebige Stelle klicken, um die Eigenschaftenseite für Ihren Cache zu öffnen.

   ![Azure-Portal][AZ04]

1. Wenn die Eigenschaftenseite für Ihre Datenbank angezeigt wird, klicken Sie auf **Zugriffsschlüssel**, und kopieren Sie Ihren URI sowie Ihre Zugriffsschlüssel für Ihre Datenbank. Diese Werte verwenden Sie in Ihrer Spring Boot-Anwendung.

   ![Azure-Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr

1. Navigieren Sie zu <https://start.spring.io/>.

1. Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf die Schaltfläche **Projekt generieren**.

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt**, z.B. *com.example.wintiptoys*.
   >

1. Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.

   ![Herunterladen eines benutzerdefinierten Spring Boot-Projekts][SI02]

1. Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a>Konfigurieren der Spring Boot-App für die Verwendung von Azure Spring Boot Starter

1. Suchen Sie die Datei *pom.xml* im Verzeichnis Ihrer App. Beispiel:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   Oder

   `/users/example/home/wingtiptoys/pom.xml`

   ![Suchen der Datei „pom.xml“][PM01]

1. Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Liste der `<dependencies>` hinzu:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][PM02]

1. Speichern und schließen Sie die Datei *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Konfigurieren der Spring Boot-App für die Verwendung von Azure Cosmos DB

1. Suchen Sie die Datei *application.properties* im *Ressourcen*-Verzeichnis Ihrer App. Beispiel:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   Oder

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Suchen der Datei „application.properties“][RE01]

1. Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften für Ihre Datenbank:

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Bearbeiten der Datei „application.properties“][RE02]

1. Speichern und schließen Sie die Datei *application.properties*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Hinzufügen eines Beispielcodes zur Implementierung von grundlegenden Datenbankfunktionen

In diesem Abschnitt erstellen Sie zwei Java-Klassen zum Speichern von Benutzerdaten und ändern dann die Hauptanwendungsklasse, um eine Instanz der Benutzerklasse zu erstellen und in der Datenbank zu speichern.

### <a name="define-a-basic-class-for-storing-user-data"></a>Definieren einer einfachen Klasse zum Speichern von Benutzerdaten

1. Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *User.java*.

1. Öffnen Sie in einem Text-Editor die Datei *User.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um eine generische Benutzerklasse zu definieren, die Werte speichert und diese von Ihrer Datenbank abruft:

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

1. Speichern und schließen Sie die Datei *User.java*.

### <a name="define-a-data-repository-interface"></a>Definieren einer Datenrepositoryschnittstelle

1. Erstellen Sie im selben Verzeichnis wie die Java-Hauptanwendungsdatei eine neue Datei mit dem Namen *UserRepository.java*.

1. Öffnen Sie in einem Text-Editor die Datei *UserRepository.java*, und fügen Sie die folgenden Zeilen zur Datei hinzu, um zur Erweiterung der standardmäßigen DocumentDB-Repositoryschnittstelle eine Benutzerrepositoryschnittstelle zu definieren:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Speichern und schließen Sie die Datei *UserRepository.java*.

### <a name="modify-the-main-application-class"></a>Ändern der Hauptanwendungsklasse

1. Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   Oder

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Suchen der Java-Anwendungsdatei][JV01]

1. Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:

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

1. Speichern und schließen Sie die Java-Hauptanwendungsdatei.

## <a name="build-and-test-your-app"></a>Erstellen und Testen der App

1. Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:

   `cd C:\SpringBoot\wingtiptoys`

   Oder

   `cd /users/example/home/wingtiptoys`

1. Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. Die Anwendung zeigt mehrere Laufzeitmeldungen an. Dabei sollte die Meldung `User: testFirstName testLastName` angezeigt werden, die darauf hinweist, dass Werte erfolgreich gespeichert und von Ihrer Datenbank abgerufen wurden.

   ![Erfolgreiche Ausgabe aus der Anwendung][JV02]

1. OPTIONAL: Im Azure-Portal können Sie auf der Eigenschaftenseite die Inhalte von Azure Cosmos DB für Ihre Datenbank anzeigen, indem Sie auf **Dokument-Explorer** klicken und dann zum Anzeigen der Inhalte ein Element in der angezeigten Liste auswählen.

   ![Anzeigen von Daten mit dem Document-Explorer][JV03]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von Azure Cosmos DB und Java finden Sie in den folgenden Artikeln:

* [Dokumentation für Azure Cosmos DB]

* [Azure Cosmos DB: Erstellen einer DocumentDB-API-App mit Java und dem Azure-Portal][Build a DocumentDB API app with Java]

Weitere Informationen zur Verwendung von Spring Boot in Azure finden Sie in den folgenden Artikeln:

* [Spring Boot DocumenDB Starter für Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [Bereitstellen einer Spring Boot-Anwendung in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen. Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt. Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.

<!-- URL List -->

[Dokumentation für Azure Cosmos DB]: /azure/cosmos-db/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
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
