---
title: Bereitstellen der in einem Linux-Container in der Cloud ausgeführten Web-App „Hallo Welt“ mit dem Azure-Toolkit für IntelliJ
description: Führen Sie eine einfache Web-App vom Typ „Hallo Welt“ in einem Linux-Container aus, und stellen Sie sie mithilfe des Azure-Toolkits für IntelliJ in der Cloud bereit.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: fdff8dc2bd7a29473314d5c0bc99b7bcda369156
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2019
ms.locfileid: "55648724"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="e7511-103">Bereitstellen einer Web-App vom Typ „Hallo Welt“ in einem Linux-Container in der Cloud mit dem Azure-Toolkit für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="e7511-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="e7511-104">[Docker]-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen.</span><span class="sxs-lookup"><span data-stu-id="e7511-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="e7511-105">Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen.</span><span class="sxs-lookup"><span data-stu-id="e7511-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="e7511-106">Mit dem Azure-Toolkit für IntelliJ wird dieser Prozess für Java-Entwickler vereinfacht, indem Features für die Bereitstellung als Container in Microsoft Azure hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="e7511-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="e7511-107">In diesem Artikel werden die Schritte zum Erstellen einer einfachen „Hello World“-Web-App beschrieben. Außerdem erfahren Sie, wie Sie Ihre Web-App mithilfe des Azure-Toolkits für IntelliJ in einem Linux-Container in Azure veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="e7511-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="e7511-108">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="e7511-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e7511-109">Sie müssen für die Schritte in diesem Tutorial [Docker] so konfigurieren, dass der Daemon ohne TLS an Port 2375 verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="e7511-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="e7511-110">Sie können diese Einstellung beim Installieren von Docker oder über das Docker-Einstellungsmenü konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="e7511-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Docker-Einstellungsmenü][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="e7511-112">Erstellen eines neuen Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="e7511-112">Create a new web app project</span></span>

1. <span data-ttu-id="e7511-113">Starten Sie IntelliJ, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) an.</span><span class="sxs-lookup"><span data-stu-id="e7511-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="e7511-114">Klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="e7511-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Erstellen eines neuen Projekts][file-new-project]

1. <span data-ttu-id="e7511-116">Wählen Sie im Dialogfeld **Neues Projekt** die Option **Maven** und abschließend **maven-archetype-webapp** aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e7511-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Auswählen der Maven-archetype-Web-App][maven-archetype-webapp]
   
1. <span data-ttu-id="e7511-118">Geben Sie die **GroupId** und **ArtifactId** für Ihre Web-App an, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e7511-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Eingeben von GroupId und ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="e7511-120">Passen Sie alle gewünschten Maven-Einstellungen an, oder übernehmen Sie die Standardeinstellungen, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e7511-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Angeben von Maven-Einstellungen][maven-options]

1. <span data-ttu-id="e7511-122">Geben Sie den Projektnamen und einen Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="e7511-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Angeben des Projektnamens][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="e7511-124">Erstellen einer Azure-Containerregistrierung, die als private Docker-Registrierung verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="e7511-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="e7511-125">Die folgende Anleitung führt Sie durch die Verwendung des Azure-Portals zur Erstellung einer Azure-Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="e7511-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e7511-126">Wenn Sie statt des Azure-Portals die Azure CLI verwenden möchten, führen Sie die Schritte unter [Erstellen einer privaten Docker-Containerregistrierung mit der Azure CLI 2.0][Create Docker Registry using Azure CLI] aus.</span><span class="sxs-lookup"><span data-stu-id="e7511-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="e7511-127">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="e7511-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="e7511-128">Nachdem Sie sich im Azure-Portal bei Ihrem Konto angemeldet haben, können Sie die Schritte im Artikel [Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal] ausführen, die im Folgenden aus Gründen der Zweckmäßigkeit umschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="e7511-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="e7511-129">Klicken Sie auf das Menüsymbol für **+ Ressource erstellen** und dann auf **Container** und **Containerregistrierung**.</span><span class="sxs-lookup"><span data-stu-id="e7511-129">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![Erstellen einer neuen Azure-Containerregistrierung][create-container-registry-01]

1. <span data-ttu-id="e7511-131">Wenn die Seite **Containerregistrierung erstellen** angezeigt wird, geben Sie Ihren **Registrierungsnamen** und die **Ressourcengruppe** ein, wählen Sie bei dem **Administratorbenutzer** die Option **Aktivieren** aus, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e7511-131">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Konfigurieren der Einstellungen für die Azure-Containerregistrierung][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="e7511-133">Bereitstellen Ihrer Web-App in einem Docker-Container</span><span class="sxs-lookup"><span data-stu-id="e7511-133">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="e7511-134">Klicken Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie **Azure** aus, und klicken Sie dann auf **Docker-Unterstützung hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="e7511-134">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="e7511-135">Damit wird automatisch eine Docker-Datei mit einer Standardkonfiguration erstellt.</span><span class="sxs-lookup"><span data-stu-id="e7511-135">This will automatically create a Docker file with a default configuration.</span></span>

   ![Hinzufügen der Docker-Unterstützung][add-docker-support]

1. <span data-ttu-id="e7511-137">Nachdem Sie die Docker-Unterstützung hinzugefügt haben, können Sie wie folgt vorgehen: Klicken Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie **Azure**, und klicken Sie dann auf **Run on Web App for Containers** (In Web-App für Container ausführen).</span><span class="sxs-lookup"><span data-stu-id="e7511-137">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App for Containers**.</span></span>

   ![Ausführen von Web-App für Container][run-on-web-app-for-containers]

1. <span data-ttu-id="e7511-139">Geben Sie die erforderlichen Informationen ein, wenn das Dialogfeld **Run on Web App for Containers** (In Web-App für Container ausführen) angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="e7511-139">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="e7511-140">**Name**: Gibt den Anzeigenamen an, der im Azure-Toolkit angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="e7511-140">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="e7511-141">**Containerregistrierung**: Wählen Sie im Dropdownmenü die Containerregistrierung aus, die Sie im vorherigen Abschnitt dieses Artikels erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="e7511-141">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="e7511-142">Die Felder für **Server-URL**, **Benutzername** und **Kennwort** werden automatisch ausgefüllt.</span><span class="sxs-lookup"><span data-stu-id="e7511-142">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="e7511-143">**Image und Tag**: Gibt den Namen des Containerimages an, wobei in der Regel die folgende Syntax verwendet wird: „*Registrierung*.azurecr.io/*App-Name*:latest“. Hierbei gilt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="e7511-143">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="e7511-144">*Registrierung* ist Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels.</span><span class="sxs-lookup"><span data-stu-id="e7511-144">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="e7511-145">*App-Name* ist der Name Ihrer Web-App.</span><span class="sxs-lookup"><span data-stu-id="e7511-145">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="e7511-146">**Use Existing Web App** (Vorhandene Web-App verwenden) oder **Create New Web App** (Neue Web-App erstellen): Gibt an, ob Sie Ihren Container in einer vorhandenen Web-App bereitstellen oder eine neue Web-App erstellen.</span><span class="sxs-lookup"><span data-stu-id="e7511-146">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> <span data-ttu-id="e7511-147">Mit dem von Ihnen angegebenen **App-Namen** wird die URL für Ihre Web-App erstellt, z. B. *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="e7511-147">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="e7511-148">**Ressourcengruppe**: Gibt an, ob Sie eine vorhandene Ressourcengruppe verwenden oder eine neue erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="e7511-148">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="e7511-149">**App Service-Plan**: Gibt an, ob Sie einen vorhandenen App Service-Plan verwenden oder einen neuen erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="e7511-149">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Ausführen von Web-App für Container][run-on-web-app-linux]

1. <span data-ttu-id="e7511-151">Wenn Sie mit dem Konfigurieren der oben aufgeführten Einstellungen fertig sind, klicken Sie auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="e7511-151">When you have finished configuring the settings listed above, click **Run**.</span></span> <span data-ttu-id="e7511-152">Nachdem Ihre Web-App erfolgreich bereitgestellt wurde, wird der Status im Fenster **Ausführen** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e7511-152">When your web app has been successfully deployed, the status will be displayed in the **Run** window.</span></span>

   ![Web-App wurde erfolgreich bereitgestellt][successfully-deployed]

1. <span data-ttu-id="e7511-154">Nach der Veröffentlichung Ihrer Web-App können Sie zu der URL navigieren, die für Ihre Web-App zuvor angegeben wurde, z. B. *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="e7511-154">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![Navigieren zu Ihrer Web-App][browsing-to-web-app]

## <a name="optional-modify-your-web-app-publish-settings"></a><span data-ttu-id="e7511-156">Optional: Ändern der Veröffentlichungseinstellungen für die Web-App</span><span class="sxs-lookup"><span data-stu-id="e7511-156">Optional: Modify your web app publish settings</span></span>

1. <span data-ttu-id="e7511-157">Nachdem Sie Ihre Web-App veröffentlicht haben, werden die Einstellungen als Standard gespeichert. Sie können Ihre Anwendung in Azure ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken.</span><span class="sxs-lookup"><span data-stu-id="e7511-157">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="e7511-158">Sie können diese Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.</span><span class="sxs-lookup"><span data-stu-id="e7511-158">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. <span data-ttu-id="e7511-160">Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="e7511-160">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="e7511-162">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="e7511-162">Next steps</span></span>

<span data-ttu-id="e7511-163">Weitere Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website][Docker].</span><span class="sxs-lookup"><span data-stu-id="e7511-163">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure-Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-intellij-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
