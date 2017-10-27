---
title: "Bereitstellen einer Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps"
description: "Erfahren Sie, wie Sie eine Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps bereitstellen."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 32781b3ee923f4d64d4e1a11df73f077281eee40
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-to-azure"></a>Bereitstellen einer Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps

Das [Maven-Plug-In für Azure-Web-Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) für [Apache Maven](http://maven.apache.org/) ermöglicht die nahtlose Integration von Azure App Service in Maven-Projekte und optimiert für Entwickler den Bereitstellungsprozess für Web-Apps in Azure App Service .

In diesem Artikel wird veranschaulicht, wie Sie mithilfe des Maven-Plug-Ins für Azure-Web-Apps eine Spring Boot-Beispielanwendung in Azure App Services bereitstellen.

> [!NOTE]
>
> Das Maven-Plug-In für Azure-Web-Apps ist derzeit als Vorschauversion verfügbar. Zur Zeit wird nur FTP-Veröffentlichung unterstützt. Für die Zukunft sind jedoch weitere Features geplant.
>

## <a name="prerequisites"></a>Voraussetzungen

Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
* Die [Azure-Befehlszeilenschnittstelle (CLI)]
* Ein aktuelles [Java Development Kit (JDK)], Version 1.7 oder höher
* Das Erstellungstool Apache [Maven] (Version 3)
* Einen [Git-Client]

## <a name="clone-the-sample-spring-boot-web-app"></a>Klonen der Beispiel-Web-App für Spring Boot

In diesem Abschnitt klonen Sie eine vollständige Spring Boot-Anwendung und testen sie lokal.

1. Öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Spring Boot-Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   – oder –
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Klonen Sie das Beispielprojekt [Spring Boot Getting Started] in das Verzeichnis, das Sie erstellt haben. Beispiel:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
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

## <a name="create-an-azure-service-principal"></a>Erstellen eines Azure-Dienstprinzipals

In diesem Abschnitt erstellen Sie einen Azure-Dienstprinzipal, den das Maven-Plug-In beim Bereitstellen der Web-App in Azure verwendet.

1. Öffnen Sie eine Eingabeaufforderung.

1. Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:
   ```shell
   az login
   ```
   Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.

1. Erstellen Sie einen Azure-Dienstprinzipal:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Dabei ist `uuuuuuuu` der Benutzername und `pppppppp` das Kennwort für den Dienstprinzipal.

1. Azure antwortet mit JSON-Code, der etwa wie folgendes Beispiel aussieht:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Sie verwenden die Werte aus dieser JSON-Antwort, wenn Sie das Maven-Plug-In für die Bereitstellung der Web-App in Azure konfigurieren. `aaaaaaaa`, `uuuuuuuu`, `pppppppp` und `tttttttt` sind Platzhalterwerte. Sie werden in diesem Beispiel dazu verwendet, die Zuordnung der Werte zu ihren entsprechenden Elementen zu vereinfachen, wenn Sie die Maven-Datei `settings.xml` im nächsten Abschnitt konfigurieren.
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a>Konfigurieren von Maven zur Verwendung des Azure-Dienstprinzipals

In diesem Abschnitt verwenden Sie die Werte Ihres Azure-Dienstprinzipals zum Konfigurieren der Authentifizierung, die Maven bei der Bereitstellung Ihrer Web-App in Azure verwendet.

1. Öffnen Sie die Maven-Datei `settings.xml` in einem Text-Editor. Diese Datei kann sich beispielsweise unter folgenden Pfaden befinden:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Fügen Sie Ihre Azure-Dienstprinzipaleinstellungen aus dem vorherigen Abschnitt dieses Tutorials zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Hierbei gilt:
   Element | Beschreibung
   ---|---|---
   `<id>` | Gibt einen eindeutigen Namen an, mit dem Maven Ihre Sicherheitseinstellungen abruft, wenn Sie die Web-App in Azure bereitstellen.
   `<client>` | Enthält den Wert `appId` aus dem Dienstprinzipal.
   `<tenant>` | Enthält den Wert `tenant` aus dem Dienstprinzipal.
   `<key>` | Enthält den Wert `password` aus dem Dienstprinzipal.
   `<environment>` | Definiert die Azure-Zielcloudumgebung (in diesem Beispiel: `AZURE`). (Eine vollständige Liste der Umgebungen finden Sie in der Dokumentation zum [Maven-Plug-Ins für Azure-Web-Apps].)

1. Speichern und schließen Sie die Datei *settings.xml*.

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a>OPTIONAL: Anpassen der Datei „pom.xml“ vor der Bereitstellung der Web-App in Azure

Öffnen Sie die Datei `pom.xml` für Ihre Spring Boot-Anwendung in einem Text-Editor, und suchen Sie das Element `<plugin>` für `azure-webapp-maven-plugin`. Dieses Element sollte etwa wie folgendes Beispiel aussehen:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Für das Maven-Plug-In können mehrere Werte angepasst werden. Eine ausführliche Beschreibung der einzelnen Elemente finden Sie in der Dokumentation zum [Maven-Plug-Ins für Azure-Web-Apps]. Für diesen Artikel sind jedoch besonders folgende Werte hervorzuheben:

Element | Beschreibung
---|---|---
`<version>` | Gibt die Version des [Maven-Plug-Ins für Azure-Web-Apps] an. Überprüfen Sie die im [zentralen Maven-Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) angegebene Version, um sicherzustellen, dass Sie die neueste Version verwenden.
`<authentication>` | Gibt die Authentifizierungsinformationen für Azure an, die in diesem Beispiel ein `<serverId>`-Element enthalten, das `azure-auth` enthält. Maven nutzt diesen Wert, um die Azure-Dienstprinzipalwerte in Ihrer Maven-Datei *settings.xml* abzurufen, die Sie weiter oben in diesem Artikel festgelegt haben.
`<resourceGroup>` | Gibt die Zielressourcengruppe an (in diesem Beispiel: `maven-plugin`). Wenn die Ressourcengruppe nicht bereits vorhanden ist, wird sie während der Bereitstellung erstellt.
`<appName>` | Gibt den Zielnamen für Ihre Web-App an. In diesem Beispiel lautet der Zielname `maven-web-app-${maven.build.timestamp}`. Dabei wird das Suffix `${maven.build.timestamp}` angehängt, um Konflikte zu vermeiden. (Der Zeitstempel ist optional. Sie können eine beliebige eindeutige Zeichenfolge für den App-Namen angeben.)
`<region>` | Gibt die Zielregion an (in diesem Beispiel: `westus`). (Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-Ins für Azure-Web-Apps].)
`<javaVersion>` | Gibt die Java Runtime-Version für Ihre Web-App an. (Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-Ins für Azure-Web-Apps].)
`<deploymentType>` | Gibt den Bereitstellungstyp für Ihre Web-App an. Derzeit wird nur `ftp` unterstützt. An der Unterstützung anderer Bereitstellungstypen wird jedoch bereits gearbeitet.
`<resources>` | Gibt Ressourcen und Ziele an, die von Maven bei der Bereitstellung Ihrer Web-App in Azure verwendet werden. In diesem Beispiel geben zwei `<resource>`-Elemente an, dass Maven die JAR-Datei für Ihre Web-App und die Datei *web.config* aus dem Spring Boot-Projekt bereitstellt.

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

* [Maven-Plug-Ins für Azure-Web-Apps] (Maven-Plug-In für Azure-Web-Apps)

* [Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)](/azure/xplat-cli-connect)

* [Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-Portal]: https://portal.azure.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven-Plug-Ins für Azure-Web-Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin (Maven-Plug-In für Azure-Web-Apps)

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
