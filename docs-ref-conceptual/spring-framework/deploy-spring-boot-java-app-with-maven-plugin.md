---
title: Bereitstellen einer Spring Boot-App mit JAR-Datei in der Cloud mit Maven und Azure
description: Hier erfahren Sie, wie Sie eine Spring Boot-App mithilfe des Maven-Plug-Ins für Azure-Web-Apps für Linux in der Cloud bereitstellen.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.author: robmcm;kevinzha;brborges
ms.date: 10/04/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 36afcc764c1cb984779518ddec004ecbfa1b7c57
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48876394"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a>Bereitstellen einer Spring Boot-App mit JAR-Datei in Azure App Service unter Linux

In diesem Artikel wird veranschaulicht, wie Sie mithilfe des [Maven-Plug-Ins für Azure App Service-Web-Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) eine Spring Boot-Anwendung als Java SE-JAR-Paket in [Azure App Service unter Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/) bereitstellen. Wählen Sie eine Java SE-Bereitstellung über [Tomcat- und WAR-Dateien](/azure/app-service/containers/quickstart-java), wenn Sie die Abhängigkeiten, Runtime und Konfiguration Ihrer App in einem einzigen bereitstellbaren Artefakt zusammenfassen möchten.


Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

## <a name="prerequisites"></a>Voraussetzungen

Zur Durchführung der Schritte in diesem Tutorial müssen die folgenden Komponenten installiert und konfiguriert sein:

* Die [Azure CLI](/cli/azure/), entweder lokal oder über [Azure Cloud Shell](https://shell.azure.com)
* [Java Development Kit (JDK)](https://www.azul.com/downloads/azure-only/zulu/), mindestens Version 1.7
* [Maven](https://maven.apache.org/) von Apache, Version 3)
* Einen [Git-Client](https://git-scm.com/downloads)

## <a name="clone-the-sample-app"></a>Klonen der Beispiel-App

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

## <a name="configure-maven-plugin-for-azure-app-service"></a>Konfigurieren des Maven-Plug-Ins für Azure App Service

In diesem Abschnitt konfigurieren Sie das Spring Boot-Projekt `pom.xml` so, dass Maven die App in Azure App Service unter Linux bereitstellen kann.

1. Öffnen Sie `pom.xml` in einem Code-Editor.

1. Fügen Sie im `<build>`-Abschnitt der Datei „pom.xml“ den folgenden `<plugin>`-Eintrag innerhalb des `<plugins>`-Tag hinzu.

   ```xml
  <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
  </plugin>
  ```

1. Aktualisieren Sie die folgenden Platzhalter in der Plug-In-Konfiguration:

| Platzhalter | BESCHREIBUNG |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | Der Name der neuen Ressourcengruppe, in der Ihre Web-App erstellt wird. Indem Sie alle Ressourcen für eine App in einer Gruppe zusammenfassen, können Sie sie zusammen verwalten. Wenn Sie beispielsweise die Ressourcengruppe löschen, werden alle Ressourcen gelöscht, die der App zugeordnet sind. Aktualisieren Sie diesen Wert mit einem neuen eindeutigen Ressourcengruppennamen, z.B. *TestResources*. In einem Abschnitt weiter unten verwenden Sie diesen Ressourcengruppennamen zum Bereinigen aller Azure-Ressourcen. |
| `WEBAPP_NAME` | Der App-Name wird bei der Bereitstellung in Azure als Teil des Hostnamens für die Web-App (WEBAPP_NAME.azurewebsites.net) verwendet. Aktualisieren Sie diesen Wert mit einem eindeutigen Namen für die neue Azure-Web-App, die Ihre Java-App hostet (z.B. *contoso*). |
| `REGION` | Eine Azure-Region, in der die Web-App gehostet wird, z. B. `westus2`. Sie können eine Liste von Regionen über die Cloud Shell oder CLI mit dem Befehl `az account list-locations` abrufen. |

Eine vollständige Liste der Konfigurationsoptionen finden Sie der [Referenz zum Maven-Plug-In auf GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).

## <a name="install-and-log-in-to-azure-cli"></a>Installieren der Azure CLI und Anmelden bei der Azure CLI

Bei Verwendung des Maven-Plug-Ins lässt sich die Spring Boot-Anwendung am einfachsten und komfortabelsten über die [Azure CLI](https://docs.microsoft.com/cli/azure/) bereitstellen.

1. Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:
   
   ```shell
   az login
   ```
   
   Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.

## <a name="deploy-the-app-to-azure"></a>Bereitstellen der Anwendung in Azure

Nachdem Sie alle Einstellungen in den vorhergehenden Abschnitten in diesem Artikel konfiguriert haben, können Sie Ihre Web-App in Azure bereitstellen. Führen Sie dazu die folgenden Schritte aus:

1. Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:
   ```shell
   mvn clean package
   ```

1. Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App oder der Web-App-Plan noch nicht vorhanden ist, wird sie bzw. er erstellt.

Wenn Ihre Web-App bereitgestellt wurde, können Sie sie über das [Azure-Portal] verwalten.

* Ihre Web-App wird unter **App Services** aufgeführt:

   ![Im Azure-Portal unter „App Services“ aufgeführte Web-App][AP01]

* Die URL für Ihre Web-App wird in der **Übersicht** für Ihre Web-App aufgeführt:

   ![Festlegen der URL für Ihre Web-App][AP02]

Stellen Sie mit dem gleichen cURL-Befehl wie zuvor sicher, dass die Bereitstellung erfolgreich war. Verwenden Sie dabei die URL Ihrer Web-App aus dem Portal anstelle von `localhost`. Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**. 

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:

* [Maven Plugin for Azure Web Apps] (Maven-Plug-In für Azure-Web-Apps)

* [Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme (Maven-Plug-In für Azure-Web-Apps)

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
