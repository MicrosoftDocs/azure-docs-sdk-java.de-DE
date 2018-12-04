---
title: Bereitstellen einer Spring Boot-Web-App unter Linux in Azure Container Service
description: In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung als Linux-Webanwendung in Microsoft Azure erläutert.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 30be16aebb18e3c9e18f9a023ea9b82e5d614e94
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339144"
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="764f0-103">Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="764f0-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="764f0-104">In diesem Tutorial wird die Verwendung von [Docker] zur Entwicklung und Bereitstellung einer [Spring Boot]-Anwendung für einen Linux-Host in [Azure Container Service (AKS)] erläutert.</span><span class="sxs-lookup"><span data-stu-id="764f0-104">This tutorial walks you through using [Docker] to develop and deploy a [Spring Boot] application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="764f0-105">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="764f0-105">Prerequisites</span></span>

<span data-ttu-id="764f0-106">Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="764f0-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="764f0-107">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="764f0-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="764f0-108">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="764f0-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="764f0-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="764f0-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="764f0-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="764f0-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="764f0-111">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="764f0-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="764f0-112">Einen [Git-Client]</span><span class="sxs-lookup"><span data-stu-id="764f0-112">A [Git] client.</span></span>
* <span data-ttu-id="764f0-113">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="764f0-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="764f0-114">Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="764f0-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="764f0-115">Erstellen der Web-App für erste Schritte mit Spring Boot in Docker</span><span class="sxs-lookup"><span data-stu-id="764f0-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="764f0-116">Die folgende Anleitung führt Sie durch die erforderlichen Schritte für das Erstellen einer einfachen Spring Boot-Webanwendung und das lokale Testen.</span><span class="sxs-lookup"><span data-stu-id="764f0-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="764f0-117">Öffnen Sie eine Eingabeaufforderung, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="764f0-118">– oder –</span><span class="sxs-lookup"><span data-stu-id="764f0-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="764f0-119">Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="764f0-120">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="764f0-121">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="764f0-122">Wechseln Sie nach dem Erstellen der Web-App in das Verzeichnis `target` mit der JAR-Datei, und starten Sie die Web-App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="764f0-123">Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="764f0-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="764f0-124">Wenn beispielsweise cURL verfügbar ist und Sie den Tomcat-Server so konfiguriert haben, dass er an Port 80 ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="764f0-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="764f0-125">Ihnen sollte die folgende Meldung angezeigt: **Hallo Docker-Welt!**</span><span class="sxs-lookup"><span data-stu-id="764f0-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Lokales Durchsuchen von Beispiel-Apps][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="764f0-127">Erstellen einer Azure-Containerregistrierung, die als private Docker-Registrierung verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="764f0-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="764f0-128">Die folgende Anleitung führt Sie durch die Verwendung des Azure-Portals zur Erstellung einer Azure-Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="764f0-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="764f0-129">Wenn Sie statt des Azure-Portals die Azure CLI verwenden möchten, führen Sie die Schritte unter [Erstellen einer privaten Docker-Containerregistrierung mit Azure-CLI-2.0](/azure/container-registry/container-registry-get-started-azure-cli) aus.</span><span class="sxs-lookup"><span data-stu-id="764f0-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="764f0-130">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="764f0-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="764f0-131">Nachdem Sie sich im Azure-Portal bei Ihrem Konto angemeldet haben, können Sie die Schritte im Artikel [Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal] ausführen, die im Folgenden aus Gründen der Zweckmäßigkeit umschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="764f0-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="764f0-132">Klicken Sie auf das Menüsymbol für **+ Neu**, auf **Container** und anschließend auf **Azure-Containerregistrierung**.</span><span class="sxs-lookup"><span data-stu-id="764f0-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Erstellen einer neuen Azure-Containerregistrierung][AR01]

1. <span data-ttu-id="764f0-134">Wenn die Informationsseite für die Vorlage der Azure-Containerregistrierung angezeigt wird, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="764f0-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Erstellen einer neuen Azure-Containerregistrierung][AR02]

1. <span data-ttu-id="764f0-136">Wenn die Seite **Containerregistrierung erstellen** angezeigt wird, geben Sie Ihren **Registrierungsnamen** und die **Ressourcengruppe** ein, wählen Sie bei dem **Administratorbenutzer** die Option **Aktivieren** aus, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="764f0-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Konfigurieren der Einstellungen für die Azure-Containerregistrierung][AR03]

1. <span data-ttu-id="764f0-138">Navigieren Sie nach der Erstellung der Containerregistrierung im Azure-Portal zu Ihrer Containerregistrierung, und klicken Sie anschließend auf **Zugriffsschlüssel**.</span><span class="sxs-lookup"><span data-stu-id="764f0-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="764f0-139">Notieren Sie sich den Benutzernamen und das Kennwort für die nächsten Schritte.</span><span class="sxs-lookup"><span data-stu-id="764f0-139">Take note of the username and password for the next steps.</span></span>

   ![Zugriffsschlüssel für die Azure-Containerregistrierung][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="764f0-141">Konfigurieren von Maven für die Verwendung Ihrer Zugriffsschlüssel für die Azure-Containerregistrierung</span><span class="sxs-lookup"><span data-stu-id="764f0-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="764f0-142">Navigieren Sie zu dem Konfigurationsverzeichnis Ihrer Maven-Installation, und öffnen Sie die Datei *settings.xml* mit einem Texteditor.</span><span class="sxs-lookup"><span data-stu-id="764f0-142">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="764f0-143">Fügen Sie Ihre Zugriffseinstellungen für die Azure-Containerregistrierung aus dem vorherigen Abschnitt dieses Tutorials zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-143">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="764f0-144">Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung (z.B. „*C:\SpringBoot\gs-spring-boot-docker\complete*“ oder „*/users/robert/SpringBoot/gs-spring-boot-docker/complete*“), und öffnen Sie die Datei *pom.xml* mit einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="764f0-144">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="764f0-145">Aktualisieren Sie die Auflistung `<properties>` in der Datei *pom.xml* mit dem Wert des Anmeldeservers für Ihre Azure-Containerregistrierung aus dem vorherigen Abschnitt dieses Tutorials. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-145">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="764f0-146">Aktualisieren Sie die Auflistung `<plugins>` in der Datei *pom.xml* so, dass `<plugin>` die Adresse des Anmeldeservers und den Registrierungsnamen für Ihre Azure-Containerregistrierung aus dem vorherigen Abschnitt dieses Tutorials enthält.</span><span class="sxs-lookup"><span data-stu-id="764f0-146">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="764f0-147">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="764f0-147">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="764f0-148">Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Befehl aus, um die Anwendung erneut zu erstellen und den Container in die Azure-Containerregistrierung zu übertragen:</span><span class="sxs-lookup"><span data-stu-id="764f0-148">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="764f0-149">Wenn Sie Ihren Docker-Container in Azure übertragen, erhalten Sie möglicherweise eine Fehlermeldung, auch wenn Ihr Docker-Container erfolgreich erstellt wurde. Sie ähnelt einer der folgenden Fehlermeldungen:</span><span class="sxs-lookup"><span data-stu-id="764f0-149">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="764f0-150">In diesem Fall müssen Sie sich möglicherweise über die Docker-Befehlszeile bei Ihrem Azure-Konto anmelden. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-150">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="764f0-151">Anschließend können Sie Ihren Container über die Befehlszeile übertragen. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="764f0-151">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="764f0-152">Erstellen einer Web-App unter Linux in Azure App Service über Ihr Containerimage</span><span class="sxs-lookup"><span data-stu-id="764f0-152">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="764f0-153">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="764f0-153">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="764f0-154">Klicken Sie auf das Menüsymbol für **+ Neu**, auf **Web + Mobil** und anschließend auf **Web-App unter Linux**.</span><span class="sxs-lookup"><span data-stu-id="764f0-154">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Erstellen einer neuen Web-App im Azure-Portal][LX01]

3. <span data-ttu-id="764f0-156">Wenn die Seite **Web-App unter Linux** angezeigt wird, geben Sie folgende Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="764f0-156">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="764f0-157">a.</span><span class="sxs-lookup"><span data-stu-id="764f0-157">a.</span></span> <span data-ttu-id="764f0-158">Geben Sie einen eindeutigen Namen für den **App-Namen** ein, z.B. „*wingtiptoyslinux*“.</span><span class="sxs-lookup"><span data-stu-id="764f0-158">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="764f0-159">b.</span><span class="sxs-lookup"><span data-stu-id="764f0-159">b.</span></span> <span data-ttu-id="764f0-160">Wählen Sie Ihr **Abonnement** aus der Dropdown-Liste aus.</span><span class="sxs-lookup"><span data-stu-id="764f0-160">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="764f0-161">c.</span><span class="sxs-lookup"><span data-stu-id="764f0-161">c.</span></span> <span data-ttu-id="764f0-162">Wählen Sie eine vorhandene **Ressourcengruppe** aus, oder geben Sie einen Namen an, um eine neue Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="764f0-162">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="764f0-163">d.</span><span class="sxs-lookup"><span data-stu-id="764f0-163">d.</span></span> <span data-ttu-id="764f0-164">Klicken Sie auf **Container konfigurieren**, und geben Sie folgende Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="764f0-164">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="764f0-165">Wählen Sie **Private Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="764f0-165">Choose **Private registry**.</span></span>

   * <span data-ttu-id="764f0-166">**Image und optionales Tag**: Geben Sie Ihren vorherigen Containernamen an, z.B. „*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*“</span><span class="sxs-lookup"><span data-stu-id="764f0-166">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

   * <span data-ttu-id="764f0-167">**Server-URL**: Geben Sie Ihre Registrierungs-URL von vorhin an. Beispiel: *<https://wingtiptoysregistry.azurecr.io>*</span><span class="sxs-lookup"><span data-stu-id="764f0-167">**Server URL**: Specify your registry URL from earlier; for example: "*<https://wingtiptoysregistry.azurecr.io>*"</span></span>

   * <span data-ttu-id="764f0-168">**Benutzername für Anmeldung** und **Kennwort**: Geben Sie die Anmeldeinformationen von Ihren **Zugriffsschlüsseln** an, die Sie in den vorherigen Schritten verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="764f0-168">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="764f0-169">e.</span><span class="sxs-lookup"><span data-stu-id="764f0-169">e.</span></span> <span data-ttu-id="764f0-170">Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="764f0-170">Once you have entered all of the above information, click **OK**.</span></span>

   ![Konfigurieren von Einstellungen für Web-Apps][LX02]

4. <span data-ttu-id="764f0-172">Klicken Sie auf **Create**.</span><span class="sxs-lookup"><span data-stu-id="764f0-172">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="764f0-173">Azure ordnet dem eingebetteten Tomcat-Server, der an dem Standardport 80 oder 8080 ausgeführt wird, automatisch Internetanforderungen zu.</span><span class="sxs-lookup"><span data-stu-id="764f0-173">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="764f0-174">Wenn Sie Ihren eingebetteten Tomcat-Server jedoch so konfiguriert haben, dass er an einem benutzerdefinierten Port ausgeführt wird, müssen Sie eine Umgebungsvariable zu Ihrer Web-App hinzufügen, die den Port für Ihren eingebetteten Tomcat-Server definiert.</span><span class="sxs-lookup"><span data-stu-id="764f0-174">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="764f0-175">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="764f0-175">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="764f0-176">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="764f0-176">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="764f0-177">Klicken Sie auf das Symbol für **App Services**.</span><span class="sxs-lookup"><span data-stu-id="764f0-177">Click the icon for **App Services**.</span></span> <span data-ttu-id="764f0-178">(Siehe Element #1 im nachfolgenden Bild.)</span><span class="sxs-lookup"><span data-stu-id="764f0-178">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="764f0-179">Wählen Sie Ihre Web-App aus der Liste aus.</span><span class="sxs-lookup"><span data-stu-id="764f0-179">Select your web app from the list.</span></span> <span data-ttu-id="764f0-180">(Element #2 im nachfolgenden Bild.)</span><span class="sxs-lookup"><span data-stu-id="764f0-180">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="764f0-181">Klicken Sie auf **Anwendungseinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="764f0-181">Click **Application Settings**.</span></span> <span data-ttu-id="764f0-182">(Element #3 im nachfolgenden Bild.)</span><span class="sxs-lookup"><span data-stu-id="764f0-182">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="764f0-183">Fügen Sie im Abschnitt **App-Einstellungen** eine neue Umgebungsvariable mit dem Namen **PORT** hinzu, und geben Sie Ihre benutzerdefinierte Portnummer für den Wert ein.</span><span class="sxs-lookup"><span data-stu-id="764f0-183">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="764f0-184">(Element #4 im nachfolgenden Bild.)</span><span class="sxs-lookup"><span data-stu-id="764f0-184">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="764f0-185">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="764f0-185">Click **Save**.</span></span> <span data-ttu-id="764f0-186">(Element #5 im nachfolgenden Bild.)</span><span class="sxs-lookup"><span data-stu-id="764f0-186">(Item #5 in the image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="764f0-188">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="764f0-188">Next steps</span></span>

<span data-ttu-id="764f0-189">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="764f0-189">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="764f0-190">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="764f0-190">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* <span data-ttu-id="764f0-191">[Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md) (Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service)</span><span class="sxs-lookup"><span data-stu-id="764f0-191">[Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)</span></span>

<span data-ttu-id="764f0-192">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="764f0-192">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="764f0-193">Weitere Informationen zum Spring Boot-Beispielprojekt in Docker finden Sie unter [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="764f0-193">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="764f0-194">Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie bei **Spring Initializr** unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="764f0-194">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="764f0-195">Weitere Informationen zu den ersten Schritten beim Erstellen einer einfachen Spring Boot-Anwendung finden Sie bei Spring Initializr unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="764f0-195">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="764f0-196">Weitere Beispiele zur Vorgehensweise bei der Verwendung benutzerdefinierter Docker-Images mit Azure finden Sie unter [Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux].</span><span class="sxs-lookup"><span data-stu-id="764f0-196">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Git]: https://github.com/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
