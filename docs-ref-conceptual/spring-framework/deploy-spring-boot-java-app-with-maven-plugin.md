---
title: Bereitstellen einer Spring Boot-App in der Cloud mit Maven und Azure
description: Hier erfahren Sie, wie Sie eine Spring Boot-App mithilfe des Maven-Plug-Ins für Azure-Web-Apps in der Cloud bereitstellen.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ca788354d26964bd9f1e21a0d3a8005ff65ce4bc
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324346"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a>Bereitstellen einer Spring Boot-App in der Cloud mithilfe des Maven-Plug-Ins für Azure App Service

In diesem Artikel erfahren Sie, wie Sie mithilfe des Maven-Plug-Ins für Azure App Service-Web-Apps eine Spring Boot-Beispielanwendung bereitstellen.

> [!NOTE]
> 
> Das [Maven-Plug-In für Azure App Service-Web-Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) für [Apache Maven](http://maven.apache.org/) ermöglicht die nahtlose Integration von Azure App Service in Maven-Projekte und optimiert für Entwickler den Bereitstellungsprozess für Web-Apps in Azure App Service.

Suchen Sie vor der Verwendung des Maven-Plug-Ins auf Maven Central nach der neuesten verfügbaren Version des Plug-Ins: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22) 

## <a name="prerequisites"></a>Voraussetzungen

Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:

* Ein Azure-Abonnement. Sollten Sie noch nicht über ein Azure-Abonnement verfügen, können Sie sich für ein [kostenloses Azure-Konto] registrieren.
* Die [Azure-Befehlszeilenschnittstelle (CLI)]
* Ein aktuelles [Java Development Kit (JDK)], Version 1.7 oder höher
* Das Erstellungstool Apache [Maven] (Version 3)
* Einen [Git]

## <a name="clone-the-sample-spring-boot-web-app"></a>Klonen der Beispiel-Web-App für Spring Boot

In diesem Abschnitt klonen Sie eine vollständige Spring Boot-Anwendung und testen sie lokal.

1. Öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Spring Boot-Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   – oder –
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. Klonen Sie das Beispielprojekt [Spring Boot Getting Started] in das Verzeichnis, das Sie erstellt haben. Beispiel:
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Erstellen Sie die JAR-Datei mit Maven. Beispiel:
   ```shell
   mvn clean package
   ```

1. Starten Sie die Web-App nach der Erstellung mithilfe von Maven. Beispiel:
   ```shell
   mvn spring-boot:run
   ```

1. Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen. Sie können beispielsweise den folgenden Befehl verwenden, wenn curl verfügbar ist:
   ```shell
   curl http://localhost:8080
   ```

1. Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a>Anpassen des Projekts für die WAR-basierte Bereitstellung in Azure App Service

In diesem Abschnitt wird das Spring Boot-Projekt mit wenigen Handgriffen für die Bereitstellung als WAR-Datei in Azure App Service angepasst, wobei standardmäßig Tomcat als Laufzeit bereitgestellt wird. Hierzu müssen zwei Dateien geändert werden:

- Die Maven-Datei `pom.xml`
- Die Java-Klasse `Application`

Beginnen wir mit den Maven-Einstellungen:

1. Öffnen Sie `pom.xml`.

1. Fügen Sie `<packaging>war</packaging>` direkt nach der Definition `<artifactId>` am Anfang der Datei hinzu:
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. Fügen Sie die folgende Abhängigkeit hinzu:
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

Öffnen Sie als Nächstes die Klasse `Application`, und nehmen Sie die folgenden Änderungen vor. (Die neuen Abhängigkeiten sollten bereits von der IDE erkannt worden sein.)

1. Legen Sie die Application-Klasse als Unterklasse von `SpringBootServletInitializer` fest:
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. Fügen Sie der Application-Klasse die folgende Methode hinzu:
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```
1. Strukturieren Sie Ihre Importe, um sicherzustellen, dass `SpringApplicationBuilder` und `SpringBootServletInitializer` richtig importiert werden.

Ihre Anwendung kann jetzt für Tomcat sowie für jede andere Servlet-Laufzeit (beispielsweise Jetty) bereitgestellt werden.

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a>Hinzufügen des Maven-Plug-Ins für Azure App Service-Web-Apps

In diesem Abschnitt wird ein Maven-Plug-In hinzugefügt, das die gesamte Bereitstellung dieser Anwendung in Azure App Service-Web-Apps automatisiert.

1. Öffnen Sie erneut `pom.xml`.

1. Legen Sie in `<properties>` mithilfe der Eigenschaft `maven.build.timestamp.format` ein benutzerdefiniertes Zeitstempelformat fest. Da Azure App Service eine öffentliche URL für Ihre Anwendung erstellt, wird diese Einstellung verwendet, um den Namen Ihrer Bereitstellung zu generieren und so Konflikte mit Livebereitstellungen anderer Benutzer zu vermeiden.
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. Fügen Sie im Element `<plugins>` Folgendes hinzu:
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

Mit diesen Einstellungen ist Ihr Maven-Projekt nun für die Livebereitstellung in Azure App Service-Web-Apps bereit.

## <a name="install-and-log-in-to-azure-cli"></a>Installieren der Azure CLI und Anmelden bei der Azure CLI

Bei Verwendung des Maven-Plug-Ins lässt sich die Spring Boot-Anwendung am einfachsten und komfortabelsten über die [Azure CLI](https://docs.microsoft.com/cli/azure/) bereitstellen. Vergewissern Sie sich, dass sie installiert ist.

1. Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:
   
   ```shell
   az login
   ```
   
   Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.

## <a name="optionally-customize-pomxml-before-deploying"></a>Optional: Anpassen der Datei „pom.xml“ vor der Bereitstellung

Öffnen Sie die Datei `pom.xml` für Ihre Spring Boot-Anwendung in einem Text-Editor, und suchen Sie das Element `<plugin>` für `azure-webapp-maven-plugin`. Dieses Element sollte etwa wie folgendes Beispiel aussehen:

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

Für das Maven-Plug-In können mehrere Werte angepasst werden. Eine ausführliche Beschreibung der einzelnen Elemente finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps]. Für diesen Artikel sind jedoch besonders folgende Werte hervorzuheben:

| Element | BESCHREIBUNG |
|---|---|
| `<version>` | Gibt die Version des [Maven-Plug-In für Azure-Web-Apps] an. Überprüfen Sie die im [zentralen Maven-Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) angegebene Version, um sicherzustellen, dass Sie die neueste Version verwenden. |
| `<resourceGroup>` | Gibt die Zielressourcengruppe an (in diesem Beispiel: `maven-plugin`). Wenn die Ressourcengruppe nicht bereits vorhanden ist, wird sie während der Bereitstellung erstellt. |
| `<appName>` | Gibt den Zielnamen für Ihre Web-App an. In diesem Beispiel lautet der Zielname `maven-web-app-${maven.build.timestamp}`. Dabei wird das Suffix `${maven.build.timestamp}` angehängt, um Konflikte zu vermeiden. (Der Zeitstempel ist optional. Sie können eine beliebige eindeutige Zeichenfolge für den App-Namen angeben.) |
| `<region>` | Gibt die Zielregion an (in diesem Beispiel: `westus`). (Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].) |
| `<javaVersion>` | Gibt die Java Runtime-Version für Ihre Web-App an. (Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].) |
| `<deploymentType>` | Gibt den Bereitstellungstyp für Ihre Web-App an. Der Standardwert ist `war`. |

## <a name="build-and-deploy-your-web-app-to-azure"></a>Erstellen und Bereitstellen der Web-App in Azure

Nachdem Sie alle Einstellungen in den vorhergehenden Abschnitten in diesem Artikel konfiguriert haben, können Sie Ihre Web-App in Azure bereitstellen. Führen Sie dazu die folgenden Schritte aus:

1. Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:
   ```shell
   mvn clean package
   ```

1. Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App noch nicht vorhanden ist, wird sie erstellt.

Wenn Ihre Web-App bereitgestellt wurde, können Sie sie mit dem [Azure-Portal] verwalten.

* Ihre Web-App wird unter **App Services** aufgeführt:

   ![Im Azure-Portal unter „App Services“ aufgeführte Web-App][AP01]

* Die URL für Ihre Web-App wird in der **Übersicht** für Ihre Web-App aufgeführt:

   ![Festlegen der URL für Ihre Web-App][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:

* [Maven-Plug-In für Azure-Web-Apps] (Maven-Plug-In für Azure-Web-Apps)

* [Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)](/azure/xplat-cli-connect)

* [Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven-Plug-In für Azure-Web-Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme (Maven-Plug-In für Azure-Web-Apps)

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
