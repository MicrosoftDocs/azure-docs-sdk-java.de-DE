---
title: "Bereitstellen einer Spring Boot-App in Azure Container Registry in Azure App Service mithilfe des Maven-Plug-Ins für Azure-Web-Apps"
description: "In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung in Azure Container Registry in Azure App Service mithilfe eines Maven-Plug-Ins erläutert."
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 7fa375ca805ddd037173f9dbd26b6631021e60a3
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a>Bereitstellen einer Spring Boot-App in Azure Container Registry in Azure App Service mithilfe des Maven-Plug-Ins für Azure-Web-Apps

In diesem Artikel wird veranschaulicht, wie Sie eine [Spring Boot]-Beispielanwendung in Azure Container Registry und dann mithilfe des Maven-Plug-Ins für Azure-Web-Apps in Azure App Services bereitstellen.

> [!NOTE]
> 
> Das Maven-Plug-In für Azure-Web-Apps für [Apache Maven](http://maven.apache.org/) ermöglicht die nahtlose Integration von Azure App Service in Maven-Projekte und optimiert für Entwickler den Bereitstellungsprozess für Web-Apps in Azure App Service.
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

1. Klonen Sie das Beispielprojekt [Erste Schritte mit Spring Boot in Docker] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
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

   ![Lokales Durchsuchen von Beispiel-Apps][SB01]

> [!NOTE]
>
> Wenn Sie Docker lokal verwenden, wird unter Umständen ein Fehler mit dem Hinweis angezeigt, dass Sie keine Verbindung mit Localhost an Port 2375 herstellen können. In diesem Fall müssen Sie möglicherweise die lokale Verwendung von Docker ohne TLS aktivieren. Öffnen Sie dazu die Docker-Einstellungen, und aktivieren Sie die Option **Expose daemon on TCP://localhost:2375 without TLS** (Daemon unter TCP://localhost:2375 ohne TLS verfügbar machen).
>
> ![Docker-Daemon am lokalen TCP-Port 2375 verfügbar machen][TL01]

## <a name="create-an-azure-service-principal"></a>Erstellen eines Azure-Dienstprinzipals

In diesem Abschnitt erstellen Sie einen Azure-Dienstprinzipal, den das Maven-Plug-In beim Bereitstellen des Containers in Azure verwendet.

1. Öffnen Sie eine Eingabeaufforderung.

1. Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:
   ```azurecli
   az login
   ```
   Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.

1. Erstellen Sie einen Azure-Dienstprinzipal:
   ```azurecli
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
   > Sie verwenden die Werte aus dieser JSON-Antwort, wenn Sie das Maven-Plug-In für die Bereitstellung des Containers in Azure konfigurieren. `aaaaaaaa`, `uuuuuuuu`, `pppppppp` und `tttttttt` sind Platzhalterwerte. Sie werden in diesem Beispiel dazu verwendet, die Zuordnung der Werte zu ihren entsprechenden Elementen zu vereinfachen, wenn Sie die Maven-Datei `settings.xml` im nächsten Abschnitt konfigurieren.
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Erstellen einer Azure Container Registry-Instanz über die Azure-Befehlszeilenschnittstelle

1. Öffnen Sie eine Eingabeaufforderung.

1. Melden Sie sich bei Ihrem Azure-Konto an:
   ```azurecli
   az login
   ```

1. Erstellen Sie eine Ressourcengruppe für die in diesem Artikel verwendeten Azure-Ressourcen:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Ersetzen Sie `wingtiptoysresources` in diesem Beispiel durch einen eindeutigen Namen für Ihre Ressourcengruppe.

1. Erstellen Sie eine private Azure-Containerregistrierung in der Ressourcengruppe für Ihre Spring Boot-App: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Ersetzen Sie `wingtiptoysregistry` in diesem Beispiel durch einen eindeutigen Namen für Ihre Containerregistrierung.

1. Rufen Sie das Kennwort für Ihre Containerregistrierung ab:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure antwortet mit Ihrem Kennwort. Beispiel:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a>Hinzufügen der Azure-Containerregistrierung und des Azure-Dienstprinzipals zu den Maven-Einstellungen

1. Öffnen Sie die Maven-Datei `settings.xml` in einem Text-Editor. Diese Datei kann sich beispielsweise unter folgenden Pfaden befinden:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Fügen Sie Ihre Zugriffseinstellungen für Azure Container Registry aus dem vorherigen Abschnitt dieses Artikels zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Hierbei gilt:
   Element | Beschreibung
   ---|---|---
   `<id>` | Enthält den Namen Ihrer privaten Azure-Containerregistrierung.
   `<username>` | Enthält den Namen Ihrer privaten Azure-Containerregistrierung.
   `<password>` | Enthält das Kennwort, das Sie im vorherigen Abschnitt dieses Artikels abgerufen haben.

1. Fügen Sie Ihre Azure-Dienstprinzipaleinstellungen aus einem vorherigen Abschnitt dieses Artikels zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:

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
   `<environment>` | Definiert die Azure-Zielcloudumgebung (in diesem Beispiel: `AZURE`). (Eine vollständige Liste der Umgebungen finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)

1. Speichern und schließen Sie die Datei *settings.xml*.

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a>Erstellen des Docker-Containerimages und Übertragen des Images an die Azure-Containerregistrierung

1. Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung (z.B. „*C:\SpringBoot\gs-spring-boot-docker\complete*“ oder „*/users/robert/SpringBoot/gs-spring-boot-docker/complete*“), und öffnen Sie die Datei *pom.xml* mit einem Texteditor.

1. Aktualisieren Sie die Auflistung `<properties>` in der Datei *pom.xml* mit dem Wert des Anmeldeservers für Ihre Azure-Containerregistrierung aus dem vorherigen Abschnitt dieses Tutorials. Beispiel:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Hierbei gilt:
   Element | Beschreibung
   ---|---|---
   `<azure.containerRegistry>` | Gibt den Namen Ihrer privaten Azure-Containerregistrierung an.
   `<docker.image.prefix>` | Gibt die URL Ihrer privaten Azure-Containerregistrierung an. Sie wird durch Anfügen von „.azurecr.io“ an den Namen der privaten Containerregistrierung abgeleitet.

1. Vergewissern Sie sich, dass `<plugin>` für das Docker-Plug-In in der Datei *pom.xml* die richtigen Eigenschaften für Anmeldeserveradresse und Registrierungsname aus dem vorherigen Schritt in diesem Tutorial enthält. Beispiel:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Hierbei gilt:
   Element | Beschreibung
   ---|---|---
   `<serverId>` | Gibt die Eigenschaft an, die den Namen Ihrer privaten Azure-Containerregistrierung enthält.
   `<registryUrl>` | Gibt die Eigenschaft an, die die URL Ihrer privaten Azure-Containerregistrierung enthält.

1. Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Befehl aus, um die Anwendung erneut zu erstellen und den Container per Push in die Azure-Containerregistrierung zu übertragen:

   ```
   mvn package docker:build -DpushImage 
   ```

1. OPTIONAL: Navigieren Sie zum [Azure-Portal], und vergewissern Sie sich, dass Ihre Containerregistrierung das Docker-Containerimage **gs-spring-boot-docker** enthält.

   ![Überprüfen des Containers im Azure-Portal][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a>Anpassen der Datei „pom.xml“ und anschließendes Erstellen und Bereitstellen des Containers in Azure

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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

Für das Maven-Plug-In können mehrere Werte angepasst werden. Eine ausführliche Beschreibung der einzelnen Elemente finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps]. Für diesen Artikel sind jedoch besonders folgende Werte hervorzuheben:

Element | Beschreibung
---|---|---
`<version>` | Gibt die Version des [Maven-Plug-In für Azure-Web-Apps] an. Überprüfen Sie die im [zentralen Maven-Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) angegebene Version, um sicherzustellen, dass Sie die neueste Version verwenden.
`<authentication>` | Gibt die Authentifizierungsinformationen für Azure an, die in diesem Beispiel ein `<serverId>`-Element enthalten, das `azure-auth` enthält. Maven nutzt diesen Wert, um die Azure-Dienstprinzipalwerte in Ihrer Maven-Datei *settings.xml* abzurufen, die Sie weiter oben in diesem Artikel festgelegt haben.
`<resourceGroup>` | Gibt die Zielressourcengruppe an (in diesem Beispiel: `wingtiptoysresources`). Wenn die Ressourcengruppe nicht bereits vorhanden ist, wird sie während der Bereitstellung erstellt.
`<appName>` | Gibt den Zielnamen für Ihre Web-App an. In diesem Beispiel lautet der Zielname `maven-linux-app-${maven.build.timestamp}`. Dabei wird das Suffix `${maven.build.timestamp}` angehängt, um Konflikte zu vermeiden. (Der Zeitstempel ist optional. Sie können eine beliebige eindeutige Zeichenfolge für den App-Namen angeben.)
`<region>` | Gibt die Zielregion an (in diesem Beispiel: `westus`). (Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)
`<containerSettings>` | Gibt die Eigenschaften an, die den Namen und die URL des Containers enthalten.
`<appSettings>` | Gibt eindeutige Einstellungen für Maven an, die beim Bereitstellen der Web-App in Azure verwendet werden sollen. In diesem Beispiel enthält ein `<property>`-Element ein Name/Wert-Paar untergeordneter Elemente, die den Port für Ihre App angeben.

> [!NOTE]
>
> Die Einstellungen zum Ändern der Portnummer in diesem Beispiel sind nur erforderlich, wenn Sie nicht die Standardeinstellung für den Port verwenden.
>

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

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:

* [Maven-Plug-In für Azure-Web-Apps] (Maven-Plug-In für Azure-Web-Apps)

* [Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)](/azure/xplat-cli-connect)

* [Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)

* [Docker plugin for Maven] (Docker-Plug-In für Maven)

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Maven-Plug-In für Azure-Web-Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin (Maven-Plug-In für Azure-Web-Apps)
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin (Docker-Plug-In für Maven)
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Erste Schritte mit Spring Boot in Docker]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
