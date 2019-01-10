---
title: Erstellen einer Spring Cloud Stream Binder-Anwendung mit Azure Event Hubs
description: Erfahren Sie, wie Sie eine mit Spring Boot Initializer erstellte Java-basierte Spring Cloud Stream Binder-Anwendung mit Azure Event Hubs konfigurieren.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: 98b3dc1243bf293ede121eafd51b041649d165db
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991424"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a>Erstellen einer Spring Cloud Stream Binder-Anwendung mit Azure Event Hubs

## <a name="overview"></a>Übersicht

In diesem Artikel wird beschrieben, wie Sie eine mit Spring Boot Initializer erstellte Java-basierte Spring Cloud Stream Binder-Anwendung mit Azure Event Hubs konfigurieren.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher

> [!IMPORTANT]
>
> Für die Schritte in diesem Artikel wird mindestens die Spring Boot-Version 2.0 benötigt.
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a>Erstellen eines Azure Event Hubs über das Azure-Portal

### <a name="create-an-azure-event-hub-namespace"></a>Erstellen eines Azure Event Hub-Namespaces

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **+ Ressource erstellen**, auf **Internet der Dinge** und dann auf **Event Hubs**.

   ![Erstellen eines Azure Event Hub-Namespaces][IMG01]

1. Geben Sie auf der Seite **Namespace erstellen** die folgenden Informationen ein:

   * Geben Sie einen eindeutigen **Namen** ein, der als Teil des URI für Ihren Event Hub-Namespace verwendet wird. Beispiel: Wenn Sie **wingtiptoys** für **Name** eingegeben haben, lautet der URI *wingtiptoys.servicebus.windows.net*.
   * Wählen Sie einen **Tarif** für Ihren Event Hub-Namespace aus.
   * Wählen Sie das **Abonnement** aus, das Sie für Ihren Namespace verwenden möchten.
   * Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihren Namespace erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.
   * Geben Sie den **Speicherort** für Ihren Event Hub-Namespace an.

   ![Angeben der Optionen für den Azure Event Hub-Namespace][IMG02]

1. Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Erstellen**, um den Namespace zu erstellen.

### <a name="create-an-azure-event-hub-in-your-namespace"></a>Erstellen eines Azure Event Hubs in Ihrem Namespace

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>.

1. Klicken Sie auf **Alle Ressourcen** und dann auf den von Ihnen erstellten Namespace.

   ![Auswählen des Azure Event Hub-Namespaces][IMG03]

1. Klicken Sie auf **Event Hubs** und dann auf **+ Event Hub**.

   ![Hinzufügen eines neuen Azure Event Hubs][IMG04]

1. Geben Sie auf der Seite **Event Hub erstellen** einen eindeutigen **Namen** für Ihren Event Hub ein, und klicken Sie dann auf **Erstellen**.

   ![Erstellen eines Azure Event Hubs][IMG05]

1. Nachdem Ihr Event Hub erstellt wurde, wird er auf der Seite **Event Hubs** aufgelistet.

   ![Erstellen eines Azure Event Hubs][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a>Erstellen eines Azure-Speicherkontos für Ihre Event Hub-Prüfpunkte

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>.

1. Klicken Sie auf **+ Ressource erstellen**, auf **Speicher** und dann auf **Speicherkonto**.

   ![Erstellen eines Azure-Speicherkontos][IMG07]

1. Geben Sie auf der Seite **Namespace erstellen** die folgenden Informationen ein:

   * Geben Sie einen eindeutigen **Namen** ein, der als Teil des URI für Ihr Speicherkonto verwendet wird. Beispiel: Wenn Sie **wingtiptoys** für **Name** eingegeben haben, lautet der URI *wingtiptoys.core.windows.net*.
   * Wählen Sie für **Kontoart** die Option **BLOB-Speicher** aus.
   * Geben Sie den **Speicherort** für das Speicherkonto an.
   * Wählen Sie das **Abonnement** aus, das Sie für Ihr Speicherkonto verwenden möchten.
   * Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihr Speicherkonto erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.

   ![Angeben der Optionen für das Azure-Speicherkonto][IMG08]

1. Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Erstellen**, um das Speicherkonto zu erstellen.

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr

1. Navigieren Sie zu <https://start.spring.io/>.

1. Verwenden Sie die folgenden Optionen:

   * Generieren Sie ein **Maven**-Projekt mit **Java**.
   * Geben Sie eine **Spring Boot**-Version ab 2.0 an.
   * Geben Sie Namen für die **Gruppe** und das **Artefakt** für Ihre Anwendung an.
   * Fügen Sie die **Web**-Abhängigkeit hinzu.

      ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für die **Gruppe** und das **Artefakt**, beispielsweise *com.wingtiptoys.eventhub*.
   >

1. Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Generate Project** (Projekt generieren).

1. Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.

   ![Herunterladen des Spring-Projekts][SI02]

1. Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a>Konfigurieren der Spring Boot-App zur Verwendung von Azure Event Hub Starter

1. Suchen Sie im Stammverzeichnis Ihrer App nach der Datei *pom.xml*. Beispiel:

   `C:\SpringBoot\eventhub\pom.xml`

   Oder

   `/users/example/home/eventhub/pom.xml`

1. Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie Spring Cloud Azure Event Hub Stream Binder Starter der Liste von `<dependencies>` hinzu:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][SI03]

1. Speichern und schließen Sie die Datei *pom.xml*.

## <a name="create-an-azure-credential-file"></a>Erstellen einer Azure-Anmeldeinformationsdatei

1. Öffnen Sie eine Eingabeaufforderung.

1. Navigieren Sie zum Verzeichnis *resources* Ihrer Spring Boot-App. Beispiel:

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   Oder

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. Melden Sie sich bei Ihrem Azure-Konto an:

   ```azurecli
   az login
   ```

1. Listen Sie Ihre Abonnements auf:

   ```azurecli
   az account list
   ```
   Azure gibt eine Liste mit Ihren Abonnements zurück. Kopieren Sie die GUID für das Abonnement, das Sie verwenden möchten. Beispiel:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```
1. Geben Sie die GUID für das Abonnement an, das Sie mit Azure verwenden möchten. Beispiel:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. Erstellen Sie die Azure-Anmeldeinformationsdatei:

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   Dieser Befehl erstellt im Verzeichnis *resources* eine Datei *my.azureauth*, deren Inhalt in etwa wie folgt aussieht:

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a>Konfigurieren der Spring Boot-App zur Verwendung Ihres Azure Event Hubs

1. Suchen Sie im Verzeichnis *resources* Ihrer App nach der Datei *application.properties*. Beispiel:

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   Oder

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. Öffnen Sie die Datei *application.properties* in einem Text-Editor, fügen Sie die folgenden Zeilen hinzu, und ersetzen Sie dann die Beispielwerte durch die entsprechenden Eigenschaften für Ihren Event Hub:

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace
   spring.cloud.azure.eventhub.checkpoint-storage-account=wingtiptoysstorage
   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   spring.cloud.stream.eventhub.bindings.input.consumer.checkpoint-mode=MANUAL
   ```
   Hinweis:

   |                          Feld                           |                                                                                   BESCHREIBUNG                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    Gibt die Azure-Anmeldeinformationsdatei an, die Sie zuvor in diesem Tutorial erstellt haben.                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      Gibt die Azure-Ressourcengruppe an, die Ihren Azure Event Hub enthält.                                                      |
   |               `spring.cloud.azure.region`                |                                           Gibt die geografische Region an, die Sie beim Erstellen Ihres Azure Event Hubs angegeben haben.                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          Gibt den eindeutigen Namen an, den Sie beim Erstellen Ihres Azure Event Hub-Namespaces angegeben haben.                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    Gibt das Azure-Speicherkonto an, das Sie zuvor in diesem Tutorial erstellt haben.                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            Gibt den Azure Event Hub an, der das Eingabeziel ist (in diesem Fall ist dies der Hub, den Sie zuvor in diesem Tutorial erstellt haben).                            |
   |       `spring.cloud.stream.bindings.input.group `        | Gibt eine Consumergruppe von Azure Event Hub an, die auf „$Default“ festgelegt werden kann, um die grundlegende Consumergruppe zu verwenden, die bei der Erstellung Ihres Azure Event Hubs erstellt wurde. |
   |    `spring.cloud.stream.bindings.output.destination`     |                               Gibt den Azure Event Hub an, der das Ausgabeziel ist (in diesem Tutorial ist das Ausgabeziel mit dem Eingabeziel identisch).                               |


3. Speichern und schließen Sie die Datei *application.properties*.

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a>Hinzufügen von Beispielcode zum Implementieren grundlegender Event Hub-Funktionen

In diesem Abschnitt erstellen Sie die Java-Klassen, die erforderlich sind, um Ereignisse an Ihren Event Hub zu senden.

### <a name="modify-the-main-application-class"></a>Ändern der Hauptanwendungsklasse

1. Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   Oder

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class EventhubApplication {
      public static void main(String[] args) {
         SpringApplication.run(EventhubApplication.class, args);
      }
   }
   ```

1. Speichern und schließen Sie die Java-Hauptanwendungsdatei.

### <a name="create-a-new-class-for-the-source-connector"></a>Erstellen einer neuen Klasse für den Quellconnector

1. Erstellen Sie eine neue Java-Datei mit dem Namen *EventhubSource.java* im Paketverzeichnis Ihrer App, öffnen Sie die Datei in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class EventhubSource {

      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String postMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```
1. Speichern und schließen Sie die Datei *EventhubSource.java*.

### <a name="create-a-new-class-for-the-sink-connector"></a>Erstellen einer neuen Klasse für den Senkenconnector

1. Erstellen Sie eine neue Java-Datei mit dem Namen *EventhubSink.java* im Paketverzeichnis Ihrer App, öffnen Sie die Datei in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:

   ```java
   package com.wingtiptoys.eventhub;

   import com.microsoft.azure.spring.integration.core.AzureHeaders;
   import com.microsoft.azure.spring.integration.core.api.Checkpointer;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   import org.springframework.messaging.handler.annotation.Header;

   @EnableBinding(Sink.class)
   public class EventhubSink {

      private static final Logger LOGGER = LoggerFactory.getLogger(EventhubSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message, @Header(AzureHeaders.CHECKPOINTER) Checkpointer checkpointer) {
         LOGGER.info("New message received: '{}'", message);
         checkpointer.success().handle((r, ex) -> {
            if (ex == null) {
               LOGGER.info("Message '{}' successfully checkpointed", message);
            }
            return null;
         });
      }
   }
   ```

1. Speichern und schließen Sie die Datei *EventhubSink.java*.

## <a name="build-and-test-your-application"></a>Erstellen und Testen der Anwendung

1. Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:

   `cd C:\SpringBoot\eventhub`

   Oder

   `cd /users/example/home/eventhub`

1. Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Sobald Ihre Anwendung ausgeführt wird, können Sie sie mit *curl* testen. Beispiel:

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   In den Protokollen Ihrer Anwendung sollte „hello“ angezeigt werden. Beispiel: 

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.

> [!div class="nextstepaction"]
> [Spring Framework in Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Weitere Ressourcen

Weitere Informationen zur Azure-Unterstützung für Event Hub Stream Binder finden Sie in den folgenden Artikeln:

* [Was ist Azure Event Hubs?](/azure/event-hubs/event-hubs-about)

* [Erstellen eines Event Hubs-Namespaces und eines Event Hubs mithilfe des Azure-Portals](/azure/event-hubs/event-hubs-create)

* [Verwenden von Spring Boot Starter für Apache Kafka mit Azure Event Hubs](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter „Azure für Java-Entwickler“ und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).

**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen. Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt. Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.

<!-- URL List -->

[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Arbeiten mit Azure DevOps und Java)
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-03.png
