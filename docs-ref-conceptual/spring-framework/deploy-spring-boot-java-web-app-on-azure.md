---
title: Bereitstellen von Spring Boot-Anwendungen in Azure App Service
description: "Dieses Tutorial führt Entwickler durch die Schritte zum Bereitstellen der Web-App für erste Schritte mit Spring Boot in Azure App Service."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: b520cc80360f8162c929bb2cc88c24311a7e20f8
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a>Bereitstellen von Spring Boot-Anwendungen in Azure App Service

Dieses Tutorial führt Sie durch das Erstellen einer Beispiel-Web-App für die ersten Schritte mit [Spring Boot] und ihrer Bereitstellung in [Azure App Service].

### <a name="prerequisites"></a>Voraussetzungen

Zum Durchführen der Schritte in diesem Tutorial benötigen Sie Folgendes:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
* Ein aktuelles [Java Developer Kit (JDK)]
* Das Erstellungstool Apache [Maven] (Version 3)
* Einen [Git-Client]

## <a name="create-the-spring-boot-getting-started-web-app"></a>Erstellen der Web-App für erste Schritte mit Spring Boot

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

1. Klonen Sie das Beispielprojekt [Spring Boot Getting Started] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Erstellen Sie die JAR-Datei mit Maven. Beispiel:
   ```
   mvn package
   ```

1. Wechseln Sie nach dem Erstellen der Web-App in das Verzeichnis mit der JAR-Datei, und starten Sie die Web-App. Beispiel:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Testen Sie die Web-App, indem Sie zu http://localhost:8080 browsen, oder verwenden Sie die Syntax im folgenden Beispiel – sofern Curl verfügbar ist:
   ```
   curl http://localhost:8080
   ```

1. Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.

   ![Browsen zur Beispiel-App][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Erstellen einer Azure-Web-App zur Verwendung mit Java

Die folgende Anleitung führt Sie durch die Schritte zum Erstellen einer Azure-Web-App, zum Konfigurieren der erforderlichen Einstellungen für Java und zum Konfigurieren Ihre FTP-Anmeldeinformationen.

1. Browsen Sie zum [Azure-Portal], und melden Sie sich an.

1. Nachdem Sie sich bei Ihrem Konto im Azure-Portal angemeldet haben, klicken Sie auf das Menüsymbol für **App Services**:
   
   ![Azure-Portal][AZ01]

1. Wenn die Seite **App Services** angezeigt wird, klicken Sie auf **+ Hinzufügen**, um einen neuen App Service zu erstellen.

   ![Erstellen eines App Service][AZ02]

1. Wenn die Liste der Web-App-Vorlagen angezeigt wird, klicken Sie auf den Link für die grundlegende Microsoft-Web-App.

   ![Web-App-Vorlagen][AZ03]

1. Wenn die Seite „Informationen“ für die Web-App-Vorlage angezeigt wird, klicken Sie auf **Erstellen**.

   ![Web-App erstellen][AZ04]

1. Geben Sie einen eindeutigen Namen für Ihre Web-App und alle zusätzlichen Einstellungen an, und klicken Sie dann auf **Erstellen**.

   ![Erstellen von Web-App-Einstellungen][AZ05]

1. Klicken Sie, nachdem Ihre Web-App erstellt wurde, auf das Menüsymbol für **App Services** und dann auf die neu erstellte Web-App:

   ![Auflisten von Web-Apps][AZ06]

1. Wenn Ihre Web-App angezeigt wird, geben Sie die Java-Version mithilfe der folgenden Schritte an:

   a. Klicken Sie auf das Menüelement **Anwendungseinstellung**.

   b. Wählen Sie als Java-Version **Java 8** aus.

   c. Wählen Sie als Java-Unterversion **Neueste** aus.

   d. Wählen Sie **Newest Tomcat 8.5** für den Webcontainer aus. (Dieser Container wird nicht tatsächlich verwendet. Azure verwendet den Container aus Ihrer Spring Boot-Anwendung.)

   e. Klicken Sie auf **Speichern**.

   ![Anwendungseinstellungen][AZ07]

1. Geben Sie die FTP-Anmeldeinformationen für die Bereitstellung mithilfe der folgenden Schritte an:

   a. Klicken Sie auf das Menüelement **Anmeldeinformationen für Bereitstellung**.

   b. Geben Sie Ihren Benutzernamen und Ihr Kennwort ein.

   c. Klicken Sie auf **Speichern**.

   ![Angeben der Anmeldeinformationen für die Bereitstellung][AZ08]

1. Rufen Sie Ihre FTP-Verbindungsinformationen mithilfe der folgenden Schritte ab:

   a. Klicken Sie auf das Menüelement **Anmeldeinformationen für Bereitstellung**.

   b. Kopieren Sie Ihren vollständigen FTP-Benutzernamen und die URL, und speichern Sie sie für den nächsten Abschnitt dieses Tutorials.

   ![FTP-URL und -Anmeldeinformationen][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a>Bereitstellen der Spring Boot-Web-App in Azure

Die folgende Anleitung führt Sie durch die Schritte zum Bereitstellen Ihrer Spring Boot-Web-App in Azure.

1. Öffnen Sie einen Text-Editor wie Editor von Windows, fügen Sie den folgenden Text in ein neues Dokument ein, und speichern Sie die Datei unter dem Namen *web.config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. Stellen Sie, nachdem die Datei *web.config* im System gespeichert wurde, per FTP mithilfe der URL, des Benutzernamens und des Kennworts aus dem vorherigen Abschnitt dieses Tutorials eine Verbindung mit Ihrer Web-App her. Beispiel:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Wechseln Sie im Remoteverzeichnis in den Stammordner der Web-App (in */site/wwwroot*), und kopieren Sie die JAR-Datei Ihrer Spring Boot-Anwendung sowie die Datei *web.config* von oben. Beispiel:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. Nachdem Sie die JAR-Datei und die Datei *web.config* in Ihrer Web-App bereitgestellt haben, müssen Sie Ihre Web-App über das Azure-Portal neu starten:

   ![][AZ10]

1. Testen Sie die Web-App, indem Sie in einem Webbrowser zur URL Ihrer Web-App browsen, oder verwenden Sie die Syntax im folgenden Beispiel – sofern Curl verfügbar ist:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.

   ![Browsen zur Beispiel-App][SB02]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von Spring Boot in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service](deploy-spring-boot-java-app-on-linux.md)

* [Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md) (Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service)

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

Weitere Informationen zum Bereitstellen von Web-Apps in Azure mithilfe von FTP finden Sie unter [Bereitstellen der App in Azure App Service mithilfe von FTP/S].

Weitere Informationen zum Spring Boot-Beispielprojekt finden Sie unter [Spring Boot Getting Started] (Erste Schritte mit Spring Boot).

Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie im **Spring Initializr** unter https://start.spring.io/.

Weitere Informationen zum Konfigurieren zusätzlicher Einstellungen für Ihre Web-App finden Sie unter [Konfigurieren von Web-Apps in Azure App Service].

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Konfigurieren von Web-Apps in Azure App Service]: /azure/app-service/web-sites-configure
[Bereitstellen der App in Azure App Service mithilfe von FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-web-app-on-azure/SB01.png
[SB02]: ./media/deploy-spring-boot-java-web-app-on-azure/SB02.png

[AZ01]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ01.png
[AZ02]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ02.png
[AZ03]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ03.png
[AZ04]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ04.png
[AZ05]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ05.png
[AZ06]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ06.png
[AZ07]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ07.png
[AZ08]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ08.png
[AZ09]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ09.png
[AZ10]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ10.png
