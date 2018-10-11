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
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: d281f37b027d4011ea2e3106990c5e45b69ebc88
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892591"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="6a049-103">Bereitstellen einer Web-App vom Typ „Hallo Welt“ in einem Linux-Container in der Cloud mit dem Azure-Toolkit für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="6a049-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="6a049-104">[Docker]-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen.</span><span class="sxs-lookup"><span data-stu-id="6a049-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="6a049-105">Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen.</span><span class="sxs-lookup"><span data-stu-id="6a049-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="6a049-106">Mit dem Azure-Toolkit für IntelliJ wird dieser Prozess für Java-Entwickler vereinfacht, indem Features für die Bereitstellung als Container in Microsoft Azure hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="6a049-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="6a049-107">In diesem Artikel werden die Schritte zum Erstellen einer einfachen „Hello World“-Web-App beschrieben. Außerdem erfahren Sie, wie Sie Ihre Web-App mithilfe des Azure-Toolkits für IntelliJ in einem Linux-Container in Azure veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="6a049-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="6a049-108">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="6a049-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6a049-109">Sie müssen für die Schritte in diesem Tutorial [Docker] so konfigurieren, dass der Daemon ohne TLS an Port 2375 verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="6a049-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="6a049-110">Sie können diese Einstellung beim Installieren von Docker oder über das Docker-Einstellungsmenü konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="6a049-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Docker-Einstellungsmenü][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="6a049-112">Erstellen eines neuen Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="6a049-112">Create a new web app project</span></span>

1. <span data-ttu-id="6a049-113">Starten Sie IntelliJ, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) an.</span><span class="sxs-lookup"><span data-stu-id="6a049-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="6a049-114">Klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="6a049-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Erstellen eines neuen Projekts][file-new-project]

1. <span data-ttu-id="6a049-116">Wählen Sie im Dialogfeld **Neues Projekt** die Option **Maven** und abschließend **maven-archetype-webapp** aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6a049-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Auswählen der Maven-archetype-Web-App][maven-archetype-webapp]
   
1. <span data-ttu-id="6a049-118">Geben Sie die **GroupId** und **ArtifactId** für Ihre Web-App an, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6a049-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Eingeben von GroupId und ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="6a049-120">Passen Sie alle gewünschten Maven-Einstellungen an, oder übernehmen Sie die Standardeinstellungen, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6a049-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Angeben von Maven-Einstellungen][maven-options]

1. <span data-ttu-id="6a049-122">Geben Sie den Projektnamen und einen Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="6a049-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Angeben des Projektnamens][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="6a049-124">Erstellen einer Azure-Containerregistrierung, die als private Docker-Registrierung verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="6a049-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="6a049-125">Die folgende Anleitung führt Sie durch die Verwendung des Azure-Portals zur Erstellung einer Azure-Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="6a049-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6a049-126">Wenn Sie statt des Azure-Portals die Azure CLI verwenden möchten, führen Sie die Schritte unter [Erstellen einer privaten Docker-Containerregistrierung mit der Azure CLI 2.0][Create Docker Registry using Azure CLI] aus.</span><span class="sxs-lookup"><span data-stu-id="6a049-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="6a049-127">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="6a049-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="6a049-128">Nachdem Sie sich im Azure-Portal bei Ihrem Konto angemeldet haben, können Sie die Schritte im Artikel [Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal] ausführen, die im Folgenden aus Gründen der Zweckmäßigkeit umschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="6a049-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="6a049-129">Klicken Sie auf das Menüsymbol für **+ Neu**, auf **Container** und anschließend auf **Azure-Containerregistrierung**.</span><span class="sxs-lookup"><span data-stu-id="6a049-129">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Erstellen einer neuen Azure-Containerregistrierung][AR01]

1. <span data-ttu-id="6a049-131">Wenn die Informationsseite für die Vorlage der Azure-Containerregistrierung angezeigt wird, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="6a049-131">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Erstellen einer neuen Azure-Containerregistrierung][AR02]

1. <span data-ttu-id="6a049-133">Wenn die Seite **Containerregistrierung erstellen** angezeigt wird, geben Sie Ihren **Registrierungsnamen** und die **Ressourcengruppe** ein, wählen Sie bei dem **Administratorbenutzer** die Option **Aktivieren** aus, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="6a049-133">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Konfigurieren der Einstellungen für die Azure-Containerregistrierung][AR03]

1. <span data-ttu-id="6a049-135">Navigieren Sie nach der Erstellung der Containerregistrierung im Azure-Portal zu Ihrer Containerregistrierung, und klicken Sie anschließend auf **Zugriffsschlüssel**.</span><span class="sxs-lookup"><span data-stu-id="6a049-135">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="6a049-136">Notieren Sie sich den Benutzernamen und das Kennwort für die nächsten Schritte.</span><span class="sxs-lookup"><span data-stu-id="6a049-136">Take note of the username and password for the next steps.</span></span>

   ![Zugriffsschlüssel für die Azure-Containerregistrierung][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="6a049-138">Bereitstellen Ihrer Web-App in einem Docker-Container</span><span class="sxs-lookup"><span data-stu-id="6a049-138">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="6a049-139">Klicken Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie **Azure** aus, und klicken Sie dann auf **Docker-Unterstützung hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="6a049-139">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="6a049-140">Damit wird automatisch eine Docker-Datei mit einer Standardkonfiguration erstellt.</span><span class="sxs-lookup"><span data-stu-id="6a049-140">This will automatically create a Docker file with a default configuration.</span></span>

   ![Hinzufügen der Docker-Unterstützung][add-docker-support]

1. <span data-ttu-id="6a049-142">Nachdem Sie die Docker-Unterstützung hinzugefügt haben, klicken Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie **Azure** aus, und klicken Sie dann auf **Run on Web App (Linux)** (In Web-App ausführen (Linux)) aus.</span><span class="sxs-lookup"><span data-stu-id="6a049-142">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App (Linux)**.</span></span>

   ![In Web-App ausführen (Linux)][run-on-web-app-linux]

1. <span data-ttu-id="6a049-144">Wenn das Dialogfeld **Run on Web App (Linux)** (In Web-App ausführen (Linux)) angezeigt wird, geben Sie die erforderlichen Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="6a049-144">When the **Run on Web App (Linux)** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="6a049-145">**Name:** gibt den Anzeigenamen im Azure-Toolkit an.</span><span class="sxs-lookup"><span data-stu-id="6a049-145">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="6a049-146">**Server-URL:** gibt die URL für Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels an; dabei wird in der Regel die folgende Syntax verwendet: „*Registrierung*.azurecr.io“.</span><span class="sxs-lookup"><span data-stu-id="6a049-146">**Server URL**: This specifies the URL for your container registry from the previous section of this article; typically this will use the following syntax: "*registry*.azurecr.io".</span></span> 

   * <span data-ttu-id="6a049-147">**Benutzername** und **Kennwort**: geben die Zugriffsschlüssel für Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels an.</span><span class="sxs-lookup"><span data-stu-id="6a049-147">**Username** and **Password**: Specifies the access keys for your container registry from the previous section of this article.</span></span> 

   * <span data-ttu-id="6a049-148">**Image und Tag:** gibt den Namen des Containerimages an; dabei wird in der Regel die folgende Syntax verwendet: „*Registrierung*.azurecr.io/*App-Name*:latest“; dabei gilt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6a049-148">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="6a049-149">*Registrierung* ist Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels.</span><span class="sxs-lookup"><span data-stu-id="6a049-149">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="6a049-150">*App-Name* ist der Name Ihrer Web-App.</span><span class="sxs-lookup"><span data-stu-id="6a049-150">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="6a049-151">**Use Existing Web App** (Vorhandene Web-App verwenden) oder **Create New Web App** (Neue Web-App erstellen): gibt an, ob Sie den Container in einer vorhandenen Web-App bereitstellen oder eine neue Web-App erstellen.</span><span class="sxs-lookup"><span data-stu-id="6a049-151">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> 

   * <span data-ttu-id="6a049-152">**Ressourcengruppe:** gibt an, ob Sie eine vorhandene Ressourcengruppe verwenden oder eine neue erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="6a049-152">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="6a049-153">**App Service-Plan:** gibt an, ob Sie einen vorhandenen App Service-Plan verwenden oder einen neuen erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="6a049-153">**App Service Plan**: Specifies whether you willuse an existing or create a new app service plan.</span></span> 

1. <span data-ttu-id="6a049-154">Wenn Sie mit dem Konfigurieren der oben aufgeführten Einstellungen fertig sind, klicken Sie auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="6a049-154">When you have finished configuring the settings listed above, click **Run**.</span></span>

   ![Web-App erstellen][create-web-app]

1. <span data-ttu-id="6a049-156">Nachdem Sie Ihre Web-App veröffentlicht haben, werden die Einstellungen als Standard gespeichert. Sie können Ihre Anwendung in Azure ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken.</span><span class="sxs-lookup"><span data-stu-id="6a049-156">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="6a049-157">Sie können diese Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.</span><span class="sxs-lookup"><span data-stu-id="6a049-157">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. <span data-ttu-id="6a049-159">Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a049-159">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="6a049-161">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6a049-161">Next steps</span></span>

<span data-ttu-id="6a049-162">Weitere Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website][Docker].</span><span class="sxs-lookup"><span data-stu-id="6a049-162">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

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

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
