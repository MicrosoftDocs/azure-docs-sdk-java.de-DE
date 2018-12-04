---
title: Konfigurieren einer Spring Boot Initializer-App für die Verwendung von Azure Application Insights Spring Boot Starter
description: Hier erfahren Sie, wie Sie eine mit Spring Initializr erstellte Spring Boot-Anwendung für die Verwendung von Application Insights Spring Boot Starter konfigurieren.
services: Application-Insights
documentationcenter: java
author: dhaval24
manager: alexklim
editor: ''
ms.assetid: ''
ms.author: dhdoshi
ms.date: 11/21/2018
ms.devlang: java
ms.service: Azure Monitor
ms.tgt_pltfrm: application-insights
ms.topic: article
ms.workload: na
ms.openlocfilehash: eef5afa1bcd8ceb92eca1584df8816b73ac78948
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338734"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a>Konfigurieren einer Spring Boot Initializer-App für die Verwendung von Application Insights

In diesem Artikel erfahren Sie Schritt für Schritt, wie Sie eine Spring Boot-Anwendung unter Verwendung von **[Spring Initializr]** erstellen, die Azure Application Insights Spring Boot Starter für die End-to-End-Überwachung von Java-Anwendungen in der Cloud verwendet.

> [!NOTE]
> 
> *Diese Starter-Option ist momentan als **Betaversion (Public Preview)* <em>erhältlich.</em>

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Erstellen einer benutzerdefinierten Anwendung mit dem Spring Initializr

1. Navigieren Sie zu [https://start.spring.io/](https://start.spring.io/).

1. Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und wählen Sie im Abschnitt mit den Abhängigkeiten die Webabhängigkeit aus.

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt** (also beispielsweise *com.example.demo*).
   >

1. Klicken Sie auf die Schaltfläche **Projekt generieren**.

1. Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.

1. Nachdem Sie die Dateien auf dem lokalen System extrahiert haben, kann Ihre benutzerdefinierte Spring Boot-Anwendung bearbeitet werden.

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a>Erstellen einer Application Insights-Ressource in Azure

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und klicken Sie auf **+Neu**.

   ![Azure-Portal][AZ01]

1. Klicken Sie auf **Verwaltungstools** und anschließend auf **Application Insights**.

   ![Azure-Portal][AZ02]

1. Geben Sie auf der Seite **Neue Application Insights-Ressource** folgende Informationen an:

   * Geben Sie unter **Name** den Namen für Ihre Application Insights-Ressource ein.
   * Legen Sie den **Anwendungstyp** auf „Java-Webanwendung“ fest.
   * Geben Sie Ihr **Abonnement**, Ihre **Ressourcengruppe** und Ihren **Standort** an.
   * Aktivieren Sie die Option „An Dashboard anheften“, wenn Sie die Ressource an Ihr Azure-Portal anheften möchten.

   Wenn Sie diese Optionen angegeben haben, klicken Sie auf **Erstellen**, um Ihre Application Insights-Ressource zu erstellen.

   ![Azure-Portal][AZ03]

1. Die erstellte Ressource wird auf Ihrem **Azure-Dashboard** sowie auf den Seiten **Alle Ressourcen** angezeigt. Klicken Sie an einem dieser Orte auf Ihre Ressource, um die Übersichtsseite der Application Insights-Ressource zu öffnen. Kopieren Sie auf dieser Übersichtsseite den **Instrumentierungsschlüssel**.

   ![Azure-Portal][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a>Konfigurieren Ihrer heruntergeladenen Spring Boot-Anwendung für die Verwendung von Application Insights

1. Suchen Sie im Stammverzeichnis Ihrer App nach der Datei *POM.xml*, und fügen Sie dem Abschnitt mit den Abhängigkeiten die folgende Abhängigkeit hinzu. 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.0.1-BETA</version>
</dependency>
```

1. Suchen Sie die Datei *application.properties* im *Ressourcen*-Verzeichnis Ihrer App, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.

   ![Suchen der Datei „application.properties“][RE01]

1. Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie der Datei die folgenden Zeilen hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften mit entsprechenden Anmeldeinformationen:

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   Weitere Optimierungsoptionen für Application Insights finden Sie in der [Infodatei für Application Insights Spring Boot Starter](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).

   > [!NOTE]
   > 
   > Sie können verschiedene Application Insights-Instrumentierungsschlüssel (sprich: verschiedene Ressourcen) für verschiedene Profile (etwa PROD oder DEV) verwenden. Weitere Informationen finden Sie unter [Spezifische Eigenschaften für Spring Boot-Profile] für zusätzliche Informationen. 

1. Speichern und schließen Sie die Datei *application.properties*.

1. Erstellen Sie einen Ordner mit dem Namen *controller* unter den Quellordner für Ihr Paket, zum Beispiel:

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   Oder

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. Erstellen Sie im Ordner *controller* eine neue Datei mit dem Namen *TestController.java*. Öffnen Sie die Datei in einem Text-Editor, und fügen Sie den folgenden Code hinzu:

   ```java
    package com.example.demo;

    import com.microsoft.applicationinsights.TelemetryClient;
    import java.io.IOException;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    import com.microsoft.applicationinsights.telemetry.Duration;

    @RestController
    @RequestMapping("/sample")
    public class TestController {

        @Autowired
        TelemetryClient telemetryClient;

        @GetMapping("/hello")
        public String hello() {

            //track a custom event  
            telemetryClient.trackEvent("Sending a custom event...");

            //trace a custom trace
            telemetryClient.trackTrace("Sending a custom trace....");

            //track a custom metric
            telemetryClient.trackMetric("custom metric", 1.0);

            //track a custom dependency
            telemetryClient.trackDependency("SQL", "Insert", new Duration(0, 0, 1, 1, 1), true);

            return "hello";
        }
    }
   ```

   Dabei müssen Sie `com.example.demo` durch den Paketnamen für das Projekt ersetzen.

1. Speichern und schließen Sie die Datei *TestController.java*.

1. Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Testen Sie die Web-App unter http://localhost:8080/sample/hello in einem Webbrowser, oder verwenden Sie die Syntax aus dem folgenden Beispiel (sofern Curl verfügbar ist):

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   Es sollte die Nachricht „hello“ von Ihrem Beispielcontroller angezeigt werden. Application Insights erfasst diese Anforderung automatisch und sendet sie gemäß Angabe in der Controllerlogik als Telemetrieelement mit dem dazugehörigen benutzerdefinierten Ereignis, der benutzerdefinierten Metrik, der benutzerdefinierten Abhängigkeit und der benutzerdefinierten Ablaufverfolgung. 

   Die Daten sollten nach wenigen Sekunden im Azure-Portal angezeigt werden. 

   ![Azure-Portal][AZ05]

   Sie können auf die Kachel „Anwendungsübersicht“ klicken, um übergeordnete Komponenten und deren Interaktionen anzuzeigen. Hier können Sie sich einen allgemeinen Überblick über die gesamte Anwendung verschaffen. Jeder Spring Boot-Microservice wird anhand des Spring-Anwendungsnamens erkannt. Vergessen Sie nicht, ihn festzulegen.

   ![Azure-Portal][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a>Konfigurieren der Spring Boot-Anwendung zum Senden von log4j-Protokollen an Application Insights

1. Bearbeiten Sie die Datei „POM.xml“ des Projekts, und fügen Sie den Abschnitt „dependencies“ mit Folgendem hinzu (oder passen Sie ihn entsprechend an). 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-spring-boot-starter</artifactId>
        <version>1.0.1-BETA</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. Speichern und schließen Sie die Datei *POM.xml*.

3. Erstellen Sie im Ordner „\src\main\resources“ eine neue Datei namens *log4j2.xml*, und konfigurieren Sie sie. Beispiel: 

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Configuration packages="com.microsoft.applicationinsights.log4j.v2">
  <Properties>
    <Property name="LOG_PATTERN">
      %d{yyyy-MM-dd HH:mm:ss.SSS} %5p ${hostName} --- [%15.15t] %-40.40c{1.} : %m%n%ex
    </Property>
  </Properties>
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
    <ApplicationInsightsAppender name="aiAppender">
    </ApplicationInsightsAppender>
  </Appenders>
  <Loggers>
    <Root level="trace">
      <AppenderRef ref="Console"  />
      <AppenderRef ref="aiAppender"  />
    </Root>
  </Loggers>
</Configuration>
```
4. Erstellen Sie die Spring Boot-Anwendung wie oben gezeigt, und führen Sie sie erneut aus. 

Innerhalb weniger Sekunden sollten alle Spring-Protokolle angezeigt werden, die im Azure-Portal verfügbar sind. 

![Azure-Portal][AZ06]

Sie können sich sogar die ausführlichen Protokollmeldungen ansehen und Analysen im Analytics-Portal durchführen. 

![Azure-Portal][AZ07]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Application Insights unterstützt die automatische Erfassung externer Abhängigkeiten und deren Korrelation mit eingehenden Anforderungen. Aktuell wird die automatische Erfassung von Oracle, MsSQL, MySQL und Redis unterstützt. Weitere Informationen zum Aktivieren der automatischen Erfassung finden Sie im Artikel [Überwachen von Abhängigkeiten, abgefangene Ausnahmen und Methodenausführungszeiten in Java-Web-Apps](https://docs.microsoft.com/azure/application-insights/app-insights-java-agent).

Weitere Informationen zu Azure Application Insights und den verfügbaren Überwachungsfunktionen finden Sie unter **[Application Insights]**.

Weitere Informationen zu weiteren Konfigurationsdetails von Application Insights Spring Boot Starter finden Sie [hier](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).

Wenn Sie Funktionen anfragen oder potenzielle Fehler melden möchten, stellen Sie bitte eine entsprechende Anfrage über unser [GitHub-Repository](https://github.com/Microsoft/ApplicationInsights-Java/issues).

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen. Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter [https://github.com/spring-guides/](https://github.com/spring-guides/) mehrere Spring Boot-Beispielpakete bereitgestellt. Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.

<!-- URL List -->

[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spezifische Eigenschaften für Spring Boot-Profile]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: https://docs.microsoft.com/azure/application-insights/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_2.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_3.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Get_IKey.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/OverviewBladeResults.png
[AZ06]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Search_and_traces.png
[AZ07]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/traces_details.png
[AZ08]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/AppMap.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/spring_start.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/After_extract.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationproperties_loc.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationinsightsproperties.png
