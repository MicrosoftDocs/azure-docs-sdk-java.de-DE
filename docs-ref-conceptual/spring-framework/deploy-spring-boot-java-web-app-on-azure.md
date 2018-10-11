---
title: Bereitstellen von Spring Boot-Anwendungen in der Cloud mit Azure App Service
description: Dieses Tutorial führt Entwickler durch die Schritte zum Bereitstellen einer Web-App für erste Schritte mit Spring Boot in der Cloud mit Azure App Service.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: adf779e2ba6ca73ea3a2406613f9622cc9ecbf99
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893161"
---
# <a name="deploy-a-spring-boot-application-to-the-cloud-with-azure-app-service"></a><span data-ttu-id="72696-103">Bereitstellen von Spring Boot-Anwendungen in der Cloud mit Azure App Service</span><span class="sxs-lookup"><span data-stu-id="72696-103">Deploy a Spring Boot application to the cloud with Azure App Service</span></span>

<span data-ttu-id="72696-104">Dieses Tutorial führt Sie durch das Erstellen einer Beispiel-Web-App für die ersten Schritte mit [Spring Boot] und ihrer Bereitstellung in [Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="72696-104">This tutorial will walk you though creating a sample [Spring Boot] Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="72696-105">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="72696-105">Prerequisites</span></span>

<span data-ttu-id="72696-106">Zum Durchführen der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="72696-106">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="72696-107">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="72696-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="72696-108">Ein aktuelles [Java Developer Kit (JDK)]</span><span class="sxs-lookup"><span data-stu-id="72696-108">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="72696-109">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="72696-109">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="72696-110">Einen [Git-Client]</span><span class="sxs-lookup"><span data-stu-id="72696-110">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="72696-111">Erstellen der Web-App für erste Schritte mit Spring Boot</span><span class="sxs-lookup"><span data-stu-id="72696-111">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="72696-112">Die folgende Anleitung führt Sie durch die erforderlichen Schritte für das Erstellen einer einfachen Spring Boot-Webanwendung und das lokale Testen.</span><span class="sxs-lookup"><span data-stu-id="72696-112">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="72696-113">Öffnen Sie eine Eingabeaufforderung, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="72696-113">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="72696-114">– oder –</span><span class="sxs-lookup"><span data-stu-id="72696-114">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="72696-115">Klonen Sie das Beispielprojekt [Spring Boot Getting Started] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="72696-115">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="72696-116">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="72696-116">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="72696-117">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="72696-117">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="72696-118">Wechseln Sie nach dem Erstellen der Web-App in das Verzeichnis mit der JAR-Datei, und starten Sie die Web-App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="72696-118">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="72696-119">Testen Sie die Web-App unter http://localhost:8080 in einem Webbrowser, oder verwenden Sie die Syntax aus dem folgenden Beispiel (sofern Curl verfügbar ist):</span><span class="sxs-lookup"><span data-stu-id="72696-119">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="72696-120">Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.</span><span class="sxs-lookup"><span data-stu-id="72696-120">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Browsen zur Beispiel-App][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="72696-122">Erstellen einer Azure-Web-App zur Verwendung mit Java</span><span class="sxs-lookup"><span data-stu-id="72696-122">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="72696-123">Die folgende Anleitung führt Sie durch die Schritte zum Erstellen einer Azure-Web-App, zum Konfigurieren der erforderlichen Einstellungen für Java und zum Konfigurieren Ihre FTP-Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="72696-123">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="72696-124">Browsen Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="72696-124">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="72696-125">Nachdem Sie sich bei Ihrem Konto im Azure-Portal angemeldet haben, klicken Sie auf das Menüsymbol für **App Services**:</span><span class="sxs-lookup"><span data-stu-id="72696-125">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Azure-Portal][AZ01]

1. <span data-ttu-id="72696-127">Wenn die Seite **App Services** angezeigt wird, klicken Sie auf **+ Hinzufügen**, um einen neuen App Service zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="72696-127">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Erstellen eines App Service][AZ02]

1. <span data-ttu-id="72696-129">Wenn die Liste der Web-App-Vorlagen angezeigt wird, klicken Sie auf den Link für die grundlegende Microsoft-Web-App.</span><span class="sxs-lookup"><span data-stu-id="72696-129">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Web-App-Vorlagen][AZ03]

1. <span data-ttu-id="72696-131">Wenn die Seite „Informationen“ für die Web-App-Vorlage angezeigt wird, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="72696-131">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Web-App erstellen][AZ04]

1. <span data-ttu-id="72696-133">Geben Sie einen eindeutigen Namen für Ihre Web-App und alle zusätzlichen Einstellungen an, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="72696-133">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Erstellen von Web-App-Einstellungen][AZ05]

1. <span data-ttu-id="72696-135">Klicken Sie, nachdem Ihre Web-App erstellt wurde, auf das Menüsymbol für **App Services** und dann auf die neu erstellte Web-App:</span><span class="sxs-lookup"><span data-stu-id="72696-135">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Auflisten von Web-Apps][AZ06]

1. <span data-ttu-id="72696-137">Wenn Ihre Web-App angezeigt wird, geben Sie die Java-Version mithilfe der folgenden Schritte an:</span><span class="sxs-lookup"><span data-stu-id="72696-137">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="72696-138">a.</span><span class="sxs-lookup"><span data-stu-id="72696-138">a.</span></span> <span data-ttu-id="72696-139">Klicken Sie auf das Menüelement **Anwendungseinstellung**.</span><span class="sxs-lookup"><span data-stu-id="72696-139">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="72696-140">b.</span><span class="sxs-lookup"><span data-stu-id="72696-140">b.</span></span> <span data-ttu-id="72696-141">Wählen Sie als Java-Version **Java 8** aus.</span><span class="sxs-lookup"><span data-stu-id="72696-141">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="72696-142">c.</span><span class="sxs-lookup"><span data-stu-id="72696-142">c.</span></span> <span data-ttu-id="72696-143">Wählen Sie als Java-Unterversion **Neueste** aus.</span><span class="sxs-lookup"><span data-stu-id="72696-143">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="72696-144">d.</span><span class="sxs-lookup"><span data-stu-id="72696-144">d.</span></span> <span data-ttu-id="72696-145">Wählen Sie **Newest Tomcat 8.5** für den Webcontainer aus.</span><span class="sxs-lookup"><span data-stu-id="72696-145">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="72696-146">(Dieser Container wird nicht tatsächlich verwendet. Azure verwendet den Container aus Ihrer Spring Boot-Anwendung.)</span><span class="sxs-lookup"><span data-stu-id="72696-146">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="72696-147">e.</span><span class="sxs-lookup"><span data-stu-id="72696-147">e.</span></span> <span data-ttu-id="72696-148">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="72696-148">Click **Save**.</span></span>

   ![Anwendungseinstellungen][AZ07]

1. <span data-ttu-id="72696-150">Geben Sie die FTP-Anmeldeinformationen für die Bereitstellung mithilfe der folgenden Schritte an:</span><span class="sxs-lookup"><span data-stu-id="72696-150">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="72696-151">a.</span><span class="sxs-lookup"><span data-stu-id="72696-151">a.</span></span> <span data-ttu-id="72696-152">Klicken Sie auf das Menüelement **Anmeldeinformationen für Bereitstellung**.</span><span class="sxs-lookup"><span data-stu-id="72696-152">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="72696-153">b.</span><span class="sxs-lookup"><span data-stu-id="72696-153">b.</span></span> <span data-ttu-id="72696-154">Geben Sie Ihren Benutzernamen und Ihr Kennwort ein.</span><span class="sxs-lookup"><span data-stu-id="72696-154">Specify your username and password.</span></span>

   <span data-ttu-id="72696-155">c.</span><span class="sxs-lookup"><span data-stu-id="72696-155">c.</span></span> <span data-ttu-id="72696-156">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="72696-156">Click **Save**.</span></span>

   ![Angeben der Anmeldeinformationen für die Bereitstellung][AZ08]

1. <span data-ttu-id="72696-158">Rufen Sie Ihre FTP-Verbindungsinformationen mithilfe der folgenden Schritte ab:</span><span class="sxs-lookup"><span data-stu-id="72696-158">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="72696-159">a.</span><span class="sxs-lookup"><span data-stu-id="72696-159">a.</span></span> <span data-ttu-id="72696-160">Klicken Sie auf das Menüelement **Anmeldeinformationen für Bereitstellung**.</span><span class="sxs-lookup"><span data-stu-id="72696-160">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="72696-161">b.</span><span class="sxs-lookup"><span data-stu-id="72696-161">b.</span></span> <span data-ttu-id="72696-162">Kopieren Sie Ihren vollständigen FTP-Benutzernamen und die URL, und speichern Sie sie für den nächsten Abschnitt dieses Tutorials.</span><span class="sxs-lookup"><span data-stu-id="72696-162">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![FTP-URL und -Anmeldeinformationen][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="72696-164">Bereitstellen der Spring Boot-Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="72696-164">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="72696-165">Die folgende Anleitung führt Sie durch die Schritte zum Bereitstellen Ihrer Spring Boot-Web-App in Azure.</span><span class="sxs-lookup"><span data-stu-id="72696-165">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="72696-166">Öffnen Sie einen Text-Editor wie Editor von Windows, fügen Sie den folgenden Text in ein neues Dokument ein, und speichern Sie die Datei unter dem Namen *web.config*:</span><span class="sxs-lookup"><span data-stu-id="72696-166">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
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

1. <span data-ttu-id="72696-167">Stellen Sie, nachdem die Datei *web.config* im System gespeichert wurde, per FTP mithilfe der URL, des Benutzernamens und des Kennworts aus dem vorherigen Abschnitt dieses Tutorials eine Verbindung mit Ihrer Web-App her.</span><span class="sxs-lookup"><span data-stu-id="72696-167">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="72696-168">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="72696-168">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="72696-169">Wechseln Sie im Remoteverzeichnis in den Stammordner der Web-App (in */site/wwwroot*), und kopieren Sie die JAR-Datei Ihrer Spring Boot-Anwendung sowie die Datei *web.config* von oben.</span><span class="sxs-lookup"><span data-stu-id="72696-169">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="72696-170">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="72696-170">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="72696-171">Nachdem Sie die JAR-Datei und die Datei *web.config* in Ihrer Web-App bereitgestellt haben, müssen Sie Ihre Web-App über das Azure-Portal neu starten:</span><span class="sxs-lookup"><span data-stu-id="72696-171">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![Neustarten der Web-App][AZ10]

1. <span data-ttu-id="72696-173">Testen Sie die Web-App, indem Sie in einem Webbrowser zur URL Ihrer Web-App browsen, oder verwenden Sie die Syntax im folgenden Beispiel – sofern Curl verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="72696-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="72696-174">Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.</span><span class="sxs-lookup"><span data-stu-id="72696-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Browsen zur Beispiel-App][SB02]

## <a name="next-steps"></a><span data-ttu-id="72696-176">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="72696-176">Next steps</span></span>

<span data-ttu-id="72696-177">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="72696-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="72696-178">Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="72696-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

* <span data-ttu-id="72696-179">[Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md) (Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service)</span><span class="sxs-lookup"><span data-stu-id="72696-179">[Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)</span></span>

<span data-ttu-id="72696-180">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="72696-180">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="72696-181">Weitere Informationen zum Bereitstellen von Web-Apps in Azure mithilfe von FTP finden Sie unter [Bereitstellen der App in Azure App Service mithilfe von FTP/S].</span><span class="sxs-lookup"><span data-stu-id="72696-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="72696-182">Weitere Informationen zum Spring Boot-Beispielprojekt finden Sie unter [Spring Boot Getting Started] (Erste Schritte mit Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="72696-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="72696-183">Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie bei **Spring Initializr** unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="72696-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="72696-184">Weitere Informationen zum Konfigurieren zusätzlicher Einstellungen für Ihre Web-App finden Sie unter [Konfigurieren von Web-Apps in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="72696-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Konfigurieren von Web-Apps in Azure App Service]: /azure/app-service/web-sites-configure
[Configure web apps in Azure App Service]: /azure/app-service/web-sites-configure
[Bereitstellen der App in Azure App Service mithilfe von FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[Kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
