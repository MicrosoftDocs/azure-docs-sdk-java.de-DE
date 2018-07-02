---
title: Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps
description: Erfahren Sie, wie Sie eine Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps bereitstellen.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: d9f2cf5c15bb8f990c8e82fddd6455ecbf8cc02c
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090763"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a>Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps

In diesem Artikel wird veranschaulicht, wie Sie mithilfe des [Maven-Plug-Ins für Azure-Web-Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) eine Spring Boot-Beispielanwendung in einem Docker-Container in Azure App Services bereitstellen.

> [!NOTE]
> 
> Das Maven-Plug-In für Azure-Web-Apps für [Apache Maven](http://maven.apache.org/) ermöglicht die nahtlose Integration von Azure App Service in Maven-Projekte und optimiert für Entwickler den Bereitstellungsprozess für Web-Apps in Azure App Service.
> 
> Das Maven-Plug-In für Azure-Web-Apps ist derzeit als Vorschauversion verfügbar. Zur Zeit wird nur FTP-Veröffentlichung unterstützt. Für die Zukunft sind jedoch weitere Features geplant.
> 

## <a name="prerequisites"></a>Voraussetzungen

Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
* Die [Azure CLI (Command-Line Interface, Befehlszeilenschnittstelle)]
* Ein aktuelles [Java Development Kit (JDK)], Version 1.7 oder höher
* Das Erstellungstool Apache [Maven] (Version 3)
* Einen [Git]
* Einen [Docker]-Client

> [!NOTE]
>
> Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a>Klonen der Beispiel-Web-App für Spring Boot in Docker

In diesem Abschnitt klonen Sie eine containerbasierte Spring Boot-Anwendung und testen sie lokal.

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

1. Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:
   ```shell
   cd gs-spring-boot-docker/complete
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

1. Es sollte die folgende Meldung angezeigt werden: **Hello Docker World**.

## <a name="create-an-azure-service-principal"></a>Erstellen eines Azure-Dienstprinzipals

In diesem Abschnitt erstellen Sie einen Azure-Dienstprinzipal, den das Maven-Plug-In beim Bereitstellen des Containers in Azure verwendet.

1. Öffnen Sie eine Eingabeaufforderung.

2. Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:
   ```shell
   az login
   ```
   Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.

3. Erstellen Sie einen Azure-Dienstprinzipal:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Hinweis:

   | Parameter  |                    BESCHREIBUNG                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | Gibt den Benutzernamen für den Dienstprinzipal an. |
   | `pppppppp` | Gibt das Kennwort für den Dienstprinzipal an.  |


4. Azure antwortet mit JSON-Code, der etwa wie folgendes Beispiel aussieht:
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
   > Sie verwenden die Werte aus dieser JSON-Antwort, wenn Sie das Maven-Plug-In für die Bereitstellung des Containers in Azure konfigurieren. `aaaaaaaa`, `uuuuuuuu`, `pppppppp` und `tttttttt` sind Platzhalterwerte. Sie werden in diesem Beispiel dazu verwendet, die Zuordnung der Werte zu ihren entsprechenden Elementen zu vereinfachen, wenn Sie die Maven-Datei `settings.xml` im nächsten Abschnitt konfigurieren.
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a>Konfigurieren von Maven zur Verwendung des Azure-Dienstprinzipals

In diesem Abschnitt verwenden Sie die Werte Ihres Azure-Dienstprinzipals zum Konfigurieren der Authentifizierung, die Maven bei der Bereitstellung Ihres Containers in Azure verwendet.

1. Öffnen Sie die Maven-Datei `settings.xml` in einem Text-Editor. Diese Datei kann sich beispielsweise in einem der folgenden Pfade befinden:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. Fügen Sie Ihre Azure-Dienstprinzipaleinstellungen aus dem vorherigen Abschnitt dieses Tutorials zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:

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
   Hinweis:

   |     Element     |                                                                                   BESCHREIBUNG                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                Gibt einen eindeutigen Namen an, mit dem Maven Ihre Sicherheitseinstellungen abruft, wenn Sie die Web-App in Azure bereitstellen.                                |
   |   `<client>`    |                                                             Enthält den Wert `appId` aus dem Dienstprinzipal.                                                             |
   |   `<tenant>`    |                                                            Enthält den Wert `tenant` aus dem Dienstprinzipal.                                                             |
   |     `<key>`     |                                                           Enthält den Wert `password` aus dem Dienstprinzipal.                                                            |
   | `<environment>` | Definiert die Azure-Zielcloudumgebung (in diesem Beispiel: `AZURE`). (Eine vollständige Liste der Umgebungen finden Sie in der Dokumentation zum [Maven Plugin for Azure Web Apps].) |


3. Speichern und schließen Sie die Datei *settings.xml*.

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a>OPTIONAL: Bereitstellen der lokalen Docker-Datei auf Docker Hub

Wenn Sie ein Docker-Konto besitzen, können Sie das Docker-Containerimage lokal erstellen und per Push an Docker Hub übertragen. Führen Sie dazu die folgenden Schritte aus:

1. Öffnen Sie die Datei `pom.xml` für Ihre Spring Boot-Anwendung in einem Text-Editor.

1. Suchen Sie das untergeordnete Element `<imageName>` des `<containerSettings>`-Elements.

1. Aktualisieren Sie den Wert `${docker.image.prefix}` mit dem Namen Ihres Docker-Kontos:
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. Wählen Sie eine der folgenden Bereitstellungsmethoden aus:

   * Erstellen Sie Ihr Containerimage lokal mit Maven, und übertragen Sie den Container anschließend mithilfe von Docker per Push an Docker Hub:
      ```shell
      mvn clean package docker:build
      docker push
      ```

   * Falls das [Docker plugin for Maven] installiert ist, können Sie das Containerimage mithilfe des `-DpushImage`-Parameters automatisch erstellen und per Push an Docker Hub übertragen:
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a>OPTIONAL: Anpassen der Datei „pom.xml“ vor der Bereitstellung des Containers in Azure

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
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Für das Maven-Plug-In können mehrere Werte angepasst werden. Eine ausführliche Beschreibung der einzelnen Elemente finden Sie in der Dokumentation zum [Maven Plugin for Azure Web Apps]. Für diesen Artikel sind jedoch besonders folgende Werte hervorzuheben:

| Element | BESCHREIBUNG |
|---|---|
| `<version>` | Gibt die Version des [Maven Plugin for Azure Web Apps] an. Überprüfen Sie die im [zentralen Maven-Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) angegebene Version, um sicherzustellen, dass Sie die neueste Version verwenden. |
| `<authentication>` | Gibt die Authentifizierungsinformationen für Azure an, die in diesem Beispiel ein `<serverId>`-Element enthalten, das `azure-auth` enthält. Maven nutzt diesen Wert, um die Azure-Dienstprinzipalwerte in Ihrer Maven-Datei *settings.xml* abzurufen, die Sie weiter oben in diesem Artikel festgelegt haben. |
| `<resourceGroup>` | Gibt die Zielressourcengruppe an (in diesem Beispiel: `maven-plugin`). Wenn die Ressourcengruppe nicht bereits vorhanden ist, wird sie während der Bereitstellung erstellt. |
| `<appName>` | Gibt den Zielnamen für Ihre Web-App an. In diesem Beispiel lautet der Zielname `maven-linux-app-${maven.build.timestamp}`. Dabei wird das Suffix `${maven.build.timestamp}` angehängt, um Konflikte zu vermeiden. (Der Zeitstempel ist optional. Sie können eine beliebige eindeutige Zeichenfolge für den App-Namen angeben.) |
| `<region>` | Gibt die Zielregion an (in diesem Beispiel: `westus`). (Eine vollständige Liste finden Sie in der Dokumentation zum [Maven Plugin for Azure Web Apps].) |
| `<appSettings>` | Gibt eindeutige Einstellungen für Maven an, die beim Bereitstellen der Web-App in Azure verwendet werden sollen. In diesem Beispiel enthält ein `<property>`-Element ein Name/Wert-Paar untergeordneter Elemente, die den Port für Ihre App angeben. |

> [!NOTE]
>
> Die Einstellungen zum Ändern der Portnummer in diesem Beispiel sind nur erforderlich, wenn Sie nicht die Standardeinstellung für den Port verwenden.
>

## <a name="build-and-deploy-your-container-to-azure"></a>Erstellen und Bereitstellen Ihres Containers in Azure

Nachdem Sie alle Einstellungen in den vorhergehenden Abschnitten in diesem Artikel konfiguriert haben, können Sie Ihren Container in Azure bereitstellen. Führen Sie dazu die folgenden Schritte aus:

1. Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:
   ```shell
   mvn clean package
   ```

1. Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App noch nicht vorhanden ist, wird sie erstellt.

> [!NOTE]
>
> Falls in der Region, die Sie im `<region>`-Element der Datei *pom.xml* angeben, beim Starten der Bereitstellung nicht genügend Server verfügbar sind, wird unter Umständen ein Fehler wie im folgenden Beispiel angezeigt:
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> In diesem Fall können Sie eine andere Region angeben und den Maven-Befehl zum Bereitstellen Ihrer Anwendung erneut ausführen.
>
>

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

* [Maven Plugin for Azure Web Apps] (Maven-Plug-In für Azure-Web-Apps)

* [Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)](/azure/xplat-cli-connect)

* [How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service ](deploy-spring-boot-java-app-with-maven-plugin.md) (Bereitstellen einer Spring Boot-App in Azure App Service mithilfe des Maven-Plug-Ins für Azure-Web-Apps)

* [Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)

* [Docker plugin for Maven] (Docker-Plug-In für Maven)

<!-- URL List -->

[Azure CLI (Command-Line Interface, Befehlszeilenschnittstelle)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin (Docker-Plug-In für Maven)
[Kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin (Maven-Plug-In für Azure-Web-Apps)

<!-- IMG List -->

[AP01]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP02.png
