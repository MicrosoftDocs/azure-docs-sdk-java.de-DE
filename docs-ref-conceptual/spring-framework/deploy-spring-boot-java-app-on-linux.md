---
title: Bereitstellen einer Spring Boot-Web-App in Azure App Service für Container
description: In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung als Linux-Webanwendung in Microsoft Azure erläutert.
services: azure app service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: azure app service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 407b852e24ef88d2fb075bd064f1acf2b107ddc1
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270866"
---
# <a name="deploy-a-spring-boot-application-on-azure-app-service-for-container"></a>Bereitstellen einer Spring Boot-Anwendung in Azure App Service für Container

In diesem Tutorial wird die Verwendung von [Docker] zum Packen Ihrer [Spring Boot]-Anwendung in Container und zum Bereitstellen Ihres eigenen Docker-Images für einen Linux-Host in [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro) erläutert.

## <a name="prerequisites"></a>Voraussetzungen

Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
* Die [Azure-Befehlszeilenschnittstelle (CLI)]
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* Das Erstellungstool Apache [Maven] (Version 3)
* Einen [Git-Client]
* Einen [Docker]-Client

> [!NOTE]
>
> Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Erstellen der Web-App für erste Schritte mit Spring Boot in Docker

Die folgende Anleitung führt Sie durch die erforderlichen Schritte für das Erstellen einer einfachen Spring Boot-Webanwendung und das lokale Testen.

1. Öffnen Sie eine Eingabeaufforderung, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   – oder –
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Erstellen Sie die JAR-Datei mit Maven. Beispiel:
   ```
   mvn package
   ```

1. Wechseln Sie nach dem Erstellen der Web-App in das Verzeichnis `target` mit der JAR-Datei, und starten Sie die Web-App. Beispiel:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen. Wenn beispielsweise cURL verfügbar ist und Sie den Tomcat-Server so konfiguriert haben, dass er an Port 80 ausgeführt wird:
   ```
   curl http://localhost
   ```

1. Die folgende Meldung sollte angezeigt werden: **Hello Docker World!**

   ![Lokales Durchsuchen von Beispiel-Apps][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Erstellen einer Azure-Containerregistrierung, die als private Docker-Registrierung verwendet werden soll

Die folgende Anleitung führt Sie durch die Verwendung des Azure-Portals zur Erstellung einer Azure-Containerregistrierung.

> [!NOTE]
>
> Wenn Sie statt des Azure-Portals die Azure CLI verwenden möchten, führen Sie die Schritte unter [Erstellen einer privaten Docker-Containerregistrierung mit Azure-CLI-2.0](/azure/container-registry/container-registry-get-started-azure-cli) aus.
>

1. Navigieren Sie zum [Azure-Portal], und melden Sie sich an.

   Nachdem Sie sich im Azure-Portal bei Ihrem Konto angemeldet haben, können Sie die Schritte im Artikel [Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal] ausführen, die im Folgenden aus Gründen der Zweckmäßigkeit umschrieben werden.

1. Klicken Sie auf das Menüsymbol für **+ Neu**, auf **Container** und anschließend auf **Azure-Containerregistrierung**.
   
   ![Erstellen einer neuen Azure-Containerregistrierung][AR01]

1. Wenn die Informationsseite für die Vorlage der Azure-Containerregistrierung angezeigt wird, klicken Sie auf **Erstellen**. 

   ![Erstellen einer neuen Azure-Containerregistrierung][AR02]

1. Wenn die Seite **Containerregistrierung erstellen** angezeigt wird, geben Sie Ihren **Registrierungsnamen** und die **Ressourcengruppe** ein, wählen Sie bei dem **Administratorbenutzer** die Option **Aktivieren** aus, und klicken Sie anschließend auf **Erstellen**.

   ![Konfigurieren der Einstellungen für die Azure-Containerregistrierung][AR03]

1. Navigieren Sie nach der Erstellung der Containerregistrierung im Azure-Portal zu Ihrer Containerregistrierung, und klicken Sie anschließend auf **Zugriffsschlüssel**. Notieren Sie sich den Benutzernamen und das Kennwort für die nächsten Schritte.

   ![Zugriffsschlüssel für die Azure-Containerregistrierung][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a>Konfigurieren von Maven für die Verwendung Ihrer Zugriffsschlüssel für die Azure-Containerregistrierung

1. Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung (z. B. „*C:\SpringBoot\gs-spring-boot-docker\complete*“ oder „ */users/robert/SpringBoot/gs-spring-boot-docker/complete*“), und öffnen Sie die Datei *pom.xml* mit einem Texteditor.

1. Aktualisieren Sie die Auflistung `<properties>` in der Datei *pom.xml* mit der aktuellen Version von [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin), dem Wert des Anmeldeservers und den Zugriffseinstellungen für Ihre Azure Container Registry-Instanz aus dem vorherigen Abschnitt dieses Tutorials. Beispiel:

   ```xml
   <properties>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <username>wingtiptoysregistry</username>
      <password>{put your Azure Container Registry access key here}</password>
   </properties>
   ```

1. Fügen Sie [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) der Auflistung `<plugins>` in der Datei *pom.xml* hinzu, und geben Sie das Basisimage unter `<from>/<image>` sowie den endgültigen Imagenamen `<to>/<image>` an. Geben Sie den Benutzernamen und das Kennwort aus dem vorherigen Abschnitt unter `<to>/<auth>` an. Beispiel:

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
            <auth>
               <username>${username}</username>
               <password>${password}</password>
            </auth>
        </to>
     </configuration>
   </plugin>
   ```

1. Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Befehl aus, um die Anwendung erneut zu erstellen und den Container in die Azure-Containerregistrierung zu übertragen:

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> Wenn Sie Jib zum Übertragen Ihres Images an Azure Container Registry per Push verwenden, berücksichtigt das Image *Dockerfile* nicht. Ausführliche Informationen finden Sie in [diesem Dokument](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html).
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Erstellen einer Web-App unter Linux in Azure App Service über Ihr Containerimage

1. Navigieren Sie zum [Azure-Portal], und melden Sie sich an.

2. Klicken Sie auf das Menüsymbol für **+ Ressource erstellen** und dann auf **Web** und **Web-App für Container**.
   
   ![Erstellen einer neuen Web-App im Azure-Portal][LX01]

3. Wenn die Seite **Web-App unter Linux** angezeigt wird, geben Sie folgende Informationen ein:

   a. Geben Sie einen eindeutigen Namen für **App-Name** ein, z. B. *wingtiptoyslinux*.

   b. Wählen Sie Ihr **Abonnement** aus der Dropdown-Liste aus.

   c. Wählen Sie eine vorhandene **Ressourcengruppe** aus, oder geben Sie einen Namen an, um eine neue Ressourcengruppe zu erstellen.

   d. Wählen Sie *Linux* als **Betriebssystem** aus.

   e. Klicken Sie auf **App Service-Planlan/Standort**, und wählen Sie einen vorhandenen App Service-Plan aus. Klicken Sie alternativ auf **Neu erstellen**, um einen neuen App Service-Plan zu erstellen.

   f. Klicken Sie auf **Container konfigurieren**, und geben Sie folgende Informationen ein:

   * Wählen Sie **Einzelner Container** und **Azure Container Registry** aus.

   * **Registrierung**: Wählen Sie den zuvor erstellten Containernamen aus, etwa *wingtiptoysregistry*.

   * **Image**: Wählen Sie den Imagenamen aus, z. B. *gs-spring-boot-docker*.
   
   * **Tag:** Wählen Sie das Tag für das Image aus, etwa *latest*.
   
   * **Startdatei**: Lassen Sie dieses Feld leer, da das Image bereits den Startbefehl enthält.
   
   e. Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Anwenden**.

   ![Konfigurieren von Einstellungen für Web-Apps][LX02]

4. Klicken Sie auf **Create**.

> [!NOTE]
>
> Azure ordnet dem eingebetteten Tomcat-Server, der an dem Standardport 80 oder 8080 ausgeführt wird, automatisch Internetanforderungen zu. Wenn Sie Ihren eingebetteten Tomcat-Server jedoch so konfiguriert haben, dass er an einem benutzerdefinierten Port ausgeführt wird, müssen Sie eine Umgebungsvariable zu Ihrer Web-App hinzufügen, die den Port für Ihren eingebetteten Tomcat-Server definiert. Führen Sie dazu die folgenden Schritte aus:
>
> 1. Navigieren Sie zum [Azure-Portal], und melden Sie sich an.
> 
> 2. Klicken Sie auf das Symbol für **App Services**, und wählen Sie in der Liste Ihre Web-App aus.
>
> 4. Klicken Sie auf **Konfiguration**. (Element 1 in der nachfolgenden Abbildung)
>
> 5. Fügen Sie im Abschnitt **App-Einstellungen** eine neue Einstellung mit dem Namen **PORT** hinzu, und geben Sie Ihre benutzerdefinierte Portnummer für den Wert ein. (Elemente 2, 3 und 4 in der nachfolgenden Abbildung)
>
> 6. Klicken Sie auf **Speichern**. (Element #5 im nachfolgenden Bild.)
>
> ![Speichern einer benutzerdefinierten Portnummer im Azure-Portal][LX03]
>

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

Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.

> [!div class="nextstepaction"]
> [Spring Framework in Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Weitere Ressourcen

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)
* [Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md) (Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service)

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).

Weitere Informationen zum Spring Boot-Beispielprojekt in Docker finden Sie unter [Spring Boot on Docker Getting Started].

Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie bei **Spring Initializr** unter https://start.spring.io/.

Weitere Informationen zu den ersten Schritten beim Erstellen einer einfachen Spring Boot-Anwendung finden Sie bei Spring Initializr unter https://start.spring.io/.

Weitere Beispiele zur Vorgehensweise bei der Verwendung benutzerdefinierter Docker-Images mit Azure finden Sie unter [Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux].

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure für Java-Entwickler]: /java/azure/
[Azure-Portal]: https://portal.azure.com/
[Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal]: /azure/container-registry/container-registry-get-started-portal
[Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Arbeiten mit Azure DevOps und Java)
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
