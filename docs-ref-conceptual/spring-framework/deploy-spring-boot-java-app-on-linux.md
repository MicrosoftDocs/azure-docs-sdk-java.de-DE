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
# <a name="deploy-a-spring-boot-application-on-azure-app-service-for-container"></a><span data-ttu-id="6176c-103">Bereitstellen einer Spring Boot-Anwendung in Azure App Service für Container</span><span class="sxs-lookup"><span data-stu-id="6176c-103">Deploy a Spring Boot application on Azure App Service for Container</span></span>

<span data-ttu-id="6176c-104">In diesem Tutorial wird die Verwendung von [Docker] zum Packen Ihrer [Spring Boot]-Anwendung in Container und zum Bereitstellen Ihres eigenen Docker-Images für einen Linux-Host in [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro) erläutert.</span><span class="sxs-lookup"><span data-stu-id="6176c-104">This tutorial walks you through using [Docker] to containerize your [Spring Boot] application and deploy your own docker image to a Linux host in the [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6176c-105">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="6176c-105">Prerequisites</span></span>

<span data-ttu-id="6176c-106">Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6176c-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="6176c-107">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="6176c-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="6176c-108">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="6176c-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="6176c-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="6176c-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="6176c-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="6176c-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="6176c-111">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="6176c-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="6176c-112">Einen [Git-Client]</span><span class="sxs-lookup"><span data-stu-id="6176c-112">A [Git] client.</span></span>
* <span data-ttu-id="6176c-113">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="6176c-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6176c-114">Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="6176c-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="6176c-115">Erstellen der Web-App für erste Schritte mit Spring Boot in Docker</span><span class="sxs-lookup"><span data-stu-id="6176c-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="6176c-116">Die folgende Anleitung führt Sie durch die erforderlichen Schritte für das Erstellen einer einfachen Spring Boot-Webanwendung und das lokale Testen.</span><span class="sxs-lookup"><span data-stu-id="6176c-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="6176c-117">Öffnen Sie eine Eingabeaufforderung, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6176c-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="6176c-118">– oder –</span><span class="sxs-lookup"><span data-stu-id="6176c-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="6176c-119">Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6176c-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="6176c-120">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6176c-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="6176c-121">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6176c-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="6176c-122">Wechseln Sie nach dem Erstellen der Web-App in das Verzeichnis `target` mit der JAR-Datei, und starten Sie die Web-App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6176c-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="6176c-123">Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="6176c-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="6176c-124">Wenn beispielsweise cURL verfügbar ist und Sie den Tomcat-Server so konfiguriert haben, dass er an Port 80 ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="6176c-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="6176c-125">Die folgende Meldung sollte angezeigt werden: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="6176c-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Lokales Durchsuchen von Beispiel-Apps][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="6176c-127">Erstellen einer Azure-Containerregistrierung, die als private Docker-Registrierung verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="6176c-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="6176c-128">Die folgende Anleitung führt Sie durch die Verwendung des Azure-Portals zur Erstellung einer Azure-Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="6176c-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6176c-129">Wenn Sie statt des Azure-Portals die Azure CLI verwenden möchten, führen Sie die Schritte unter [Erstellen einer privaten Docker-Containerregistrierung mit Azure-CLI-2.0](/azure/container-registry/container-registry-get-started-azure-cli) aus.</span><span class="sxs-lookup"><span data-stu-id="6176c-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="6176c-130">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="6176c-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="6176c-131">Nachdem Sie sich im Azure-Portal bei Ihrem Konto angemeldet haben, können Sie die Schritte im Artikel [Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal] ausführen, die im Folgenden aus Gründen der Zweckmäßigkeit umschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="6176c-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="6176c-132">Klicken Sie auf das Menüsymbol für **+ Neu**, auf **Container** und anschließend auf **Azure-Containerregistrierung**.</span><span class="sxs-lookup"><span data-stu-id="6176c-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Erstellen einer neuen Azure-Containerregistrierung][AR01]

1. <span data-ttu-id="6176c-134">Wenn die Informationsseite für die Vorlage der Azure-Containerregistrierung angezeigt wird, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="6176c-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Erstellen einer neuen Azure-Containerregistrierung][AR02]

1. <span data-ttu-id="6176c-136">Wenn die Seite **Containerregistrierung erstellen** angezeigt wird, geben Sie Ihren **Registrierungsnamen** und die **Ressourcengruppe** ein, wählen Sie bei dem **Administratorbenutzer** die Option **Aktivieren** aus, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="6176c-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Konfigurieren der Einstellungen für die Azure-Containerregistrierung][AR03]

1. <span data-ttu-id="6176c-138">Navigieren Sie nach der Erstellung der Containerregistrierung im Azure-Portal zu Ihrer Containerregistrierung, und klicken Sie anschließend auf **Zugriffsschlüssel**.</span><span class="sxs-lookup"><span data-stu-id="6176c-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="6176c-139">Notieren Sie sich den Benutzernamen und das Kennwort für die nächsten Schritte.</span><span class="sxs-lookup"><span data-stu-id="6176c-139">Take note of the username and password for the next steps.</span></span>

   ![Zugriffsschlüssel für die Azure-Containerregistrierung][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="6176c-141">Konfigurieren von Maven für die Verwendung Ihrer Zugriffsschlüssel für die Azure-Containerregistrierung</span><span class="sxs-lookup"><span data-stu-id="6176c-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="6176c-142">Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung (z. B. „*C:\SpringBoot\gs-spring-boot-docker\complete*“ oder „ */users/robert/SpringBoot/gs-spring-boot-docker/complete*“), und öffnen Sie die Datei *pom.xml* mit einem Texteditor.</span><span class="sxs-lookup"><span data-stu-id="6176c-142">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="6176c-143">Aktualisieren Sie die Auflistung `<properties>` in der Datei *pom.xml* mit der aktuellen Version von [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin), dem Wert des Anmeldeservers und den Zugriffseinstellungen für Ihre Azure Container Registry-Instanz aus dem vorherigen Abschnitt dieses Tutorials.</span><span class="sxs-lookup"><span data-stu-id="6176c-143">Update the `<properties>` collection in the *pom.xml* file with the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) and login server value and access settings for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="6176c-144">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6176c-144">For example:</span></span>

   ```xml
   <properties>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <username>wingtiptoysregistry</username>
      <password>{put your Azure Container Registry access key here}</password>
   </properties>
   ```

1. <span data-ttu-id="6176c-145">Fügen Sie [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) der Auflistung `<plugins>` in der Datei *pom.xml* hinzu, und geben Sie das Basisimage unter `<from>/<image>` sowie den endgültigen Imagenamen `<to>/<image>` an. Geben Sie den Benutzernamen und das Kennwort aus dem vorherigen Abschnitt unter `<to>/<auth>` an.</span><span class="sxs-lookup"><span data-stu-id="6176c-145">Add [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) to the `<plugins>` collection in the *pom.xml* file, specify the base image at `<from>/<image>` and  final image name `<to>/<image>`, specify the username and password from previous section at `<to>/<auth>`.</span></span> <span data-ttu-id="6176c-146">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6176c-146">For example:</span></span>

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

1. <span data-ttu-id="6176c-147">Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Befehl aus, um die Anwendung erneut zu erstellen und den Container in die Azure-Containerregistrierung zu übertragen:</span><span class="sxs-lookup"><span data-stu-id="6176c-147">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> <span data-ttu-id="6176c-148">Wenn Sie Jib zum Übertragen Ihres Images an Azure Container Registry per Push verwenden, berücksichtigt das Image *Dockerfile* nicht. Ausführliche Informationen finden Sie in [diesem Dokument](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html).</span><span class="sxs-lookup"><span data-stu-id="6176c-148">When you are using Jib to push your image to the Azure Container Registry, the image will not honor *Dockerfile*, see [this](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) document for details.</span></span>
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="6176c-149">Erstellen einer Web-App unter Linux in Azure App Service über Ihr Containerimage</span><span class="sxs-lookup"><span data-stu-id="6176c-149">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="6176c-150">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="6176c-150">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="6176c-151">Klicken Sie auf das Menüsymbol für **+ Ressource erstellen** und dann auf **Web** und **Web-App für Container**.</span><span class="sxs-lookup"><span data-stu-id="6176c-151">Click the menu icon for **+ Create a resource**, then click **Web**, and then click **Web App for Containers**.</span></span>
   
   ![Erstellen einer neuen Web-App im Azure-Portal][LX01]

3. <span data-ttu-id="6176c-153">Wenn die Seite **Web-App unter Linux** angezeigt wird, geben Sie folgende Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="6176c-153">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="6176c-154">a.</span><span class="sxs-lookup"><span data-stu-id="6176c-154">a.</span></span> <span data-ttu-id="6176c-155">Geben Sie einen eindeutigen Namen für **App-Name** ein, z. B. *wingtiptoyslinux*.</span><span class="sxs-lookup"><span data-stu-id="6176c-155">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*"</span></span>

   <span data-ttu-id="6176c-156">b.</span><span class="sxs-lookup"><span data-stu-id="6176c-156">b.</span></span> <span data-ttu-id="6176c-157">Wählen Sie Ihr **Abonnement** aus der Dropdown-Liste aus.</span><span class="sxs-lookup"><span data-stu-id="6176c-157">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="6176c-158">c.</span><span class="sxs-lookup"><span data-stu-id="6176c-158">c.</span></span> <span data-ttu-id="6176c-159">Wählen Sie eine vorhandene **Ressourcengruppe** aus, oder geben Sie einen Namen an, um eine neue Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6176c-159">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="6176c-160">d.</span><span class="sxs-lookup"><span data-stu-id="6176c-160">d.</span></span> <span data-ttu-id="6176c-161">Wählen Sie *Linux* als **Betriebssystem** aus.</span><span class="sxs-lookup"><span data-stu-id="6176c-161">Choose *Linux* as the **OS**.</span></span>

   <span data-ttu-id="6176c-162">e.</span><span class="sxs-lookup"><span data-stu-id="6176c-162">e.</span></span> <span data-ttu-id="6176c-163">Klicken Sie auf **App Service-Planlan/Standort**, und wählen Sie einen vorhandenen App Service-Plan aus. Klicken Sie alternativ auf **Neu erstellen**, um einen neuen App Service-Plan zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6176c-163">Click **App Service plan/Location** and choose an existing app service plan, or click **Create new** to create a new app service plan.</span></span>

   <span data-ttu-id="6176c-164">f.</span><span class="sxs-lookup"><span data-stu-id="6176c-164">f.</span></span> <span data-ttu-id="6176c-165">Klicken Sie auf **Container konfigurieren**, und geben Sie folgende Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="6176c-165">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="6176c-166">Wählen Sie **Einzelner Container** und **Azure Container Registry** aus.</span><span class="sxs-lookup"><span data-stu-id="6176c-166">Choose **Single Container** and  **Azure Container Registry**.</span></span>

   * <span data-ttu-id="6176c-167">**Registrierung**: Wählen Sie den zuvor erstellten Containernamen aus, etwa *wingtiptoysregistry*.</span><span class="sxs-lookup"><span data-stu-id="6176c-167">**Registry**: Choose your container name created earlier; for example: "*wingtiptoysregistry*"</span></span>

   * <span data-ttu-id="6176c-168">**Image**: Wählen Sie den Imagenamen aus, z. B. *gs-spring-boot-docker*.</span><span class="sxs-lookup"><span data-stu-id="6176c-168">**Image**: Choose the image name; for example: "*gs-spring-boot-docker*"</span></span>
   
   * <span data-ttu-id="6176c-169">**Tag:** Wählen Sie das Tag für das Image aus, etwa *latest*.</span><span class="sxs-lookup"><span data-stu-id="6176c-169">**Tag**: Choose the tag for the image; for example: "*latest*"</span></span>
   
   * <span data-ttu-id="6176c-170">**Startdatei**: Lassen Sie dieses Feld leer, da das Image bereits den Startbefehl enthält.</span><span class="sxs-lookup"><span data-stu-id="6176c-170">**Startup File**: Keep it blank since the image already has the start up command</span></span>
   
   <span data-ttu-id="6176c-171">e.</span><span class="sxs-lookup"><span data-stu-id="6176c-171">e.</span></span> <span data-ttu-id="6176c-172">Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Anwenden**.</span><span class="sxs-lookup"><span data-stu-id="6176c-172">Once you have entered all of the above information, click **Apply**.</span></span>

   ![Konfigurieren von Einstellungen für Web-Apps][LX02]

4. <span data-ttu-id="6176c-174">Klicken Sie auf **Create**.</span><span class="sxs-lookup"><span data-stu-id="6176c-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6176c-175">Azure ordnet dem eingebetteten Tomcat-Server, der an dem Standardport 80 oder 8080 ausgeführt wird, automatisch Internetanforderungen zu.</span><span class="sxs-lookup"><span data-stu-id="6176c-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="6176c-176">Wenn Sie Ihren eingebetteten Tomcat-Server jedoch so konfiguriert haben, dass er an einem benutzerdefinierten Port ausgeführt wird, müssen Sie eine Umgebungsvariable zu Ihrer Web-App hinzufügen, die den Port für Ihren eingebetteten Tomcat-Server definiert.</span><span class="sxs-lookup"><span data-stu-id="6176c-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="6176c-177">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="6176c-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="6176c-178">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="6176c-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="6176c-179">Klicken Sie auf das Symbol für **App Services**, und wählen Sie in der Liste Ihre Web-App aus.</span><span class="sxs-lookup"><span data-stu-id="6176c-179">Click the icon for **App Services**, and select your web app from the list.</span></span>
>
> 4. <span data-ttu-id="6176c-180">Klicken Sie auf **Konfiguration**.</span><span class="sxs-lookup"><span data-stu-id="6176c-180">Click **Configuration**.</span></span> <span data-ttu-id="6176c-181">(Element 1 in der nachfolgenden Abbildung)</span><span class="sxs-lookup"><span data-stu-id="6176c-181">(Item #1 in the image below.)</span></span>
>
> 5. <span data-ttu-id="6176c-182">Fügen Sie im Abschnitt **App-Einstellungen** eine neue Einstellung mit dem Namen **PORT** hinzu, und geben Sie Ihre benutzerdefinierte Portnummer für den Wert ein.</span><span class="sxs-lookup"><span data-stu-id="6176c-182">In the **Application settings** section, add a new setting named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="6176c-183">(Elemente 2, 3 und 4 in der nachfolgenden Abbildung)</span><span class="sxs-lookup"><span data-stu-id="6176c-183">(Item #2, #3, #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="6176c-184">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="6176c-184">Click **Save**.</span></span> <span data-ttu-id="6176c-185">(Element #5 im nachfolgenden Bild.)</span><span class="sxs-lookup"><span data-stu-id="6176c-185">(Item #5 in the image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="6176c-187">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6176c-187">Next steps</span></span>

<span data-ttu-id="6176c-188">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="6176c-188">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6176c-189">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="6176c-189">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="6176c-190">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6176c-190">Additional Resources</span></span>

<span data-ttu-id="6176c-191">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="6176c-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="6176c-192">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6176c-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* <span data-ttu-id="6176c-193">[Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md) (Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service)</span><span class="sxs-lookup"><span data-stu-id="6176c-193">[Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)</span></span>

<span data-ttu-id="6176c-194">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="6176c-194">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="6176c-195">Weitere Informationen zum Spring Boot-Beispielprojekt in Docker finden Sie unter [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="6176c-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="6176c-196">Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie bei **Spring Initializr** unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="6176c-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="6176c-197">Weitere Informationen zu den ersten Schritten beim Erstellen einer einfachen Spring Boot-Anwendung finden Sie bei Spring Initializr unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="6176c-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="6176c-198">Weitere Beispiele zur Vorgehensweise bei der Verwendung benutzerdefinierter Docker-Images mit Azure finden Sie unter [Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux].</span><span class="sxs-lookup"><span data-stu-id="6176c-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure für Java-Entwickler]: /java/azure/
[Azure for Java Developers]: /java/azure/
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
[Working with Azure DevOps and Java]: /azure/devops/java/ (Arbeiten mit Azure DevOps und Java)
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
