---
title: Verwenden von Spring Data Gremlin Starter mit der SQL-API von Azure Cosmos DB
description: Hier erfahren Sie, wie eine mit dem Spring Boot-Initialisierer erstellte Anwendung mit der SQL-API von Azure Cosmos DB konfiguriert wird.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.date: 11/21/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 47251c6bca1186a400020ba38e4b6596c7c5f2f1
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339024"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a>Verwenden von Spring Data Gremlin Starter mit der SQL-API von Azure Cosmos DB

## <a name="overview"></a>Übersicht

Spring Data Gremlin Starter bietet Spring-Datenunterstützung für die Gremlin-Abfragesprache von Apache, die Entwickler für jeden beliebigen, mit Gremlin kompatiblen Datenspeicher verwenden können.

Dieser Artikel zeigt, wie über das Azure-Portal eine Azure Cosmos DB-Instanz für die Verwendung mit der Gremlin-API und dann mithilfe von **[Spring Initializr]** eine benutzerdefinierte Java-Anwendung erstellt wird. Anschließend wird veranschaulicht, wie Spring Data Gremlin Starter-Funktionen zu Ihrer benutzerdefinierten Anwendung hinzugefügt werden, um Daten mithilfe von Gremlin in Ihrer Azure Cosmos DB-Instanz zu speichern und daraus abzurufen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher

> [!IMPORTANT]
>
> Für die Schritte in diesem Artikel wird mindestens die Spring Boot-Version 2.0 benötigt.
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a>Erstellen einer Azure Cosmos DB-Instanz über das Azure-Portal

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a>Erstellen Ihrer Azure-Cosmos-Datenbank für die Verwendung mit der Gremlin-API

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und klicken Sie auf **+Ressource erstellen**.

   ![Erstellen einer Ressource][AZ01]

1. Klicken Sie auf **Datenbanken** und anschließend auf **Azure Cosmos DB**.

   ![Erstellen von Azure Cosmos DB][AZ02]

1. Geben Sie auf der Seite **Azure Cosmos DB** die folgenden Informationen ein:

   * Geben Sie eine eindeutige **ID** ein, die als Teil des Gremlin-URIs für Ihre Datenbank verwendet wird. Wenn Sie für die **ID** also beispielsweise **wingtiptoysdata** eingegeben haben, lautet der Gremlin-URI *wingtiptoysdata.gremlin.cosmosdb.azure.com*.
   * Wählen Sie **Gremlin (Diagramm)** für die API aus.
   * Wählen Sie das **Abonnement**, das Sie für Ihre Datenbank verwenden möchten.
   * Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihre Datenbank erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.
   * Geben Sie den **Speicherort** für Ihre Datenbank an.
   
   Wenn Sie diese Optionen angegeben haben, klicken Sie zum Erstellen Ihrer Datenbank auf **Erstellen**.

   ![Angeben von Optionen für Azure Cosmos DB][AZ03]

1. Wenn Ihre Datenbank erstellt wurde, wird Sie in Ihrem Azure-**Dashboard** sowie auf den Seiten **Alle Ressourcen** und **Azure Cosmos DB** aufgeführt. Sie können in Ihrer Datenbank auf eine beliebige Stelle klicken, um die Eigenschaftenseite für Ihren Cache zu öffnen.

   ![Alle Ressourcen][AZ04]

1. Wenn die Eigenschaftenseite für Ihre Datenbank angezeigt wird, klicken Sie auf **Zugriffsschlüssel**, und kopieren Sie Ihren URI sowie Ihre Zugriffsschlüssel für Ihre Datenbank. Diese Werte verwenden Sie in Ihrer Spring Boot-Anwendung.

   ![Zugriffsschlüssel][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a>Hinzufügen eines Diagramms zu Ihrer Azure-Cosmos-Datenbank

1. Klicken Sie auf **Daten-Explorer** und anschließend auf **New Graph** (Neues Diagramm).

   ![Neues Diagramm][AZ06]

1. Wenn **Diagramm hinzufügen** angezeigt wird, geben Sie folgende Informationen ein:

   * Geben Sie eine eindeutige **Datenbank-ID** für Ihre Datenbank an.
   * Geben Sie eine eindeutige **Diagramm-ID** für Ihr Diagramm an.
   * Sie können Ihre **Speicherkapazität** angeben oder die Standardeinstellung übernehmen.
   * Geben Sie Ihren **Durchsatz** an. Für dieses Beispiel können Sie 400 Anforderungseinheiten (Request Units, RUs) auswählen.
   
   Wenn Sie diese Optionen angegeben haben, klicken Sie auf **OK**, um das Diagramm zu erstellen.

   ![Hinzufügen des Diagramms][AZ07]

1. Das erstellte Diagramm kann über den **Daten-Explorer** angezeigt werden.

   ![Anzeige der Diagrammeigenschaften][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr

1. Navigieren Sie zu <https://start.spring.io/>.

1. Geben Sie an, dass Sie ein Projekt vom Typ **Maven** mit **Java** generieren möchten, benennen Sie **Gruppe** und **Artefakt** für Ihre Anwendung, und geben Sie als **Spring Boot**-Version mindestens die Version 2.0 an. Klicken Sie anschließend auf die Schaltfläche **Projekt generieren**.

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt** (also beispielsweise „*com.example.wintiptoysdata“).
   >

1. Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.

   ![Herunterladen eines benutzerdefinierten Spring Boot-Projekts][SI02]

1. Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a>Konfigurieren Ihrer Spring Boot-App für die Verwendung von Spring Data Gremlin Starter

1. Suchen Sie die Datei *pom.xml* im Verzeichnis Ihrer App. Beispiel:

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   Oder

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Suchen der Datei „pom.xml“][PM01]

1. Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie Spring Data Gremlin Starter der Liste mit `<dependencies>` hinzu:

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][PM02]

1. Speichern und schließen Sie die Datei *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Konfigurieren der Spring Boot-App für die Verwendung von Azure Cosmos DB

1. Suchen Sie das Verzeichnis *resources* Ihrer App, und erstellen Sie eine neue Datei namens *application.yml*. Beispiel: 

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   Oder

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Erstellen der Datei „application.yml“][RE01]

1. Öffnen Sie die Datei *application.yml* in einem Text-Editor, und fügen Sie ihr die folgenden Zeilen hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften für Ihre Datenbank:

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   
   Hinweis:
   
   | Feld | BESCHREIBUNG |
   |---|---|
   | `endpoint` | Gibt den Gremlin-URI für Ihre Datenbank an. Dieser wird von der eindeutigen **ID** abgeleitet, die Sie zuvor in diesem Tutorial beim Erstellen Ihrer Azure Cosmos DB-Instanz angegeben haben. |
   | `port` | Gibt den TCP/IP-Port an (**443** für HTTPS). |
   | `username` | Gibt die eindeutige **Datenbank-ID** und **Diagramm-ID** an, die Sie zuvor in diesem Tutorial beim Hinzufügen Ihres Diagramms verwendet haben (Syntax: /dbs/**{Datenbank-ID}**/colls/**{Diagramm-ID}**). |
   | `password` | Gibt den primären oder sekundären **Zugriffsschlüssel** an, den Sie zuvor in diesem Tutorial kopiert haben. |
   | `telemetryAllowed` | Geben Sie **true** an, wenn Sie Telemetriedaten aktivieren möchten (oder **false**, falls nicht).

1. Speichern und schließen Sie die Datei *application.yml*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Hinzufügen eines Beispielcodes zur Implementierung von grundlegenden Datenbankfunktionen

In diesem Abschnitt werden die Java-Klassen erstellt, die erforderlich sind, um Daten in Ihrer Datenbank zu speichern.

### <a name="modify-the-main-application-class"></a>Ändern der Hauptanwendungsklasse

1. Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   Oder

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Suchen der Java-Anwendungsdatei][JV01]

1. Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:

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

1. Speichern und schließen Sie die Java-Hauptanwendungsdatei.

### <a name="define-a-basic-class-for-storing-configuration-information"></a>Definieren einer einfachen Klasse zum Speichern von Konfigurationsinformationen

1. Erstellen Sie unter dem Paketverzeichnis Ihrer App einen Ordner namens *config*. Beispiel:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   Oder

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. Erstellen Sie im Verzeichnis *config* eine neue Java-Datei namens *UserRepositoryConfiguration.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

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

1. Speichern und schließen Sie die Datei *UserRepositoryConfiguration.java*.

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a>Definieren einer Gruppe von Klassen zum Definieren der Elemente Ihrer Diagrammdatenbank

1. Erstellen Sie unter dem Paketverzeichnis Ihrer App einen Ordner namens *domain*. Beispiel:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   Oder

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. Erstellen Sie im Verzeichnis *domain* eine neue Java-Datei namens *Person.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

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

1. Speichern und schließen Sie die Datei *Person.java*.

1. Erstellen Sie im Verzeichnis *domain* eine neue Java-Datei namens *Relation.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

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

1. Speichern und schließen Sie die Datei *Relation.java*.

1. Erstellen Sie im Verzeichnis *domain* eine neue Java-Datei namens *Network.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

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

1. Speichern und schließen Sie die Datei *Network.java*.

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a>Definieren einer Gruppe von Klassen zum Definieren der Repositorys für Ihre Diagrammdatenbank

1. Erstellen Sie unter dem Paketverzeichnis Ihrer App einen Ordner namens *repository*. Beispiel:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   Oder

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. Erstellen Sie im Verzeichnis *repository* eine neue Java-Datei namens *NetworkRepository.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. Speichern und schließen Sie die Datei *NetworkRepository.java*.

1. Erstellen Sie im Verzeichnis *repository* eine neue Java-Datei namens *PersonRepository.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. Speichern und schließen Sie die Datei *PersonRepository.java*.

1. Erstellen Sie im Verzeichnis *repository* eine neue Java-Datei namens *RelationRepository.java*, öffnen Sie sie in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. Speichern und schließen Sie die Datei *RelationRepository.java*.

## <a name="build-and-test-your-app"></a>Erstellen und Testen der App

1. Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:

   `cd C:\SpringBoot\wingtiptoysdata`

   Oder

   `cd /users/example/home/wingtiptoysdata`

1. Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Die Anwendung zeigt mehrere Laufzeitmeldungen an. Sind keine Fehler aufgetreten, können Sie im Azure-Portal den Inhalt Ihrer Azure Cosmos DB-Instanz anzeigen. Klicken Sie hierzu auf der Eigenschaftenseite für Ihre Datenbank auf **Daten-Explorer**, klicken Sie auf **Execute Gremlin Query** (Gremlin-Abfrage ausführen), und wählen Sie anschließend ein Element aus der Ergebnisliste aus, um die Daten anzuzeigen.

   ![Anzeigen von Daten mit dem Document-Explorer][JV03]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Azure-Unterstützung für Gremlin und Graph-API finden Sie in den folgenden Artikeln:

* [Einführung in die Graph-API von Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [Unterstützung für Gremlin-Diagramme in Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [Azure Cosmos DB: Erstellen einer Graphdatenbank mit Java und dem Azure-Portal](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [Tutorial: Abfragen der Graph-API von Azure Cosmos DB mithilfe von Gremlin](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* [Spring Data Gremlin Starter]

Weitere Informationen zur Verwendung von Azure Cosmos DB und Java finden Sie in den folgenden Artikeln:

* [Dokumentation für Azure Cosmos DB]

* [Azure Cosmos DB: Erstellen einer Dokumentdatenbank mit Java und dem Azure-Portal][Build a SQL API app with Java]

* [Spring-Daten für SQL-API von Azure Cosmos DB]

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen. Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt. Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.


<!-- URL List -->

[Dokumentation für Azure Cosmos DB]: /azure/cosmos-db/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring-Daten für SQL-API von Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
