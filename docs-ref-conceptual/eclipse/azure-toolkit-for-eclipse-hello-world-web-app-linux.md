---
title: Bereitstellen der in einem Linux-Container in der Cloud ausgeführten Web-App „Hallo Welt“ mit dem Azure-Toolkit für Eclipse
description: Führen Sie eine einfache Web-App vom Typ „Hallo Welt“ in einem Linux-Container aus, und stellen Sie sie mithilfe des Azure-Toolkits für Eclipse in der Cloud bereit.
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
ms.openlocfilehash: 799f21a282956f9a88aa35743157fc1292197569
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2019
ms.locfileid: "55649246"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="ca06f-103">Bereitstellen einer Web-App vom Typ „Hallo Welt“ in einem Linux-Container in der Cloud mit dem Azure-Toolkit für Eclipse</span><span class="sxs-lookup"><span data-stu-id="ca06f-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="ca06f-104">[Docker]-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen.</span><span class="sxs-lookup"><span data-stu-id="ca06f-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="ca06f-105">Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen.</span><span class="sxs-lookup"><span data-stu-id="ca06f-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="ca06f-106">Mit dem Azure-Toolkit für Eclipse wird dieser Prozess für Java-Entwickler vereinfacht, indem Features für die Bereitstellung von Containern in Microsoft Azure hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="ca06f-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="ca06f-107">In diesem Artikel werden die Schritte zum Erstellen einer einfachen „Hallo Welt“-Web-App beschrieben. Außerdem erfahren Sie, wie Sie Ihre Web-App mithilfe des Azure-Toolkits für Eclipse in einem Linux-Container in Azure veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="ca06f-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]
* <span data-ttu-id="ca06f-108">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="ca06f-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ca06f-109">Sie müssen für die Schritte in diesem Tutorial [Docker] so konfigurieren, dass der Daemon ohne TLS an Port 2375 verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="ca06f-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="ca06f-110">Sie können diese Einstellung beim Installieren von Docker oder über das Docker-Einstellungsmenü konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="ca06f-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Docker-Einstellungsmenü][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="ca06f-112">Erstellen eines neuen Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="ca06f-112">Create a new web app project</span></span>

1. <span data-ttu-id="ca06f-113">Starten Sie Eclipse, und melden Sie sich beim Azure-Konto an, indem Sie die Schritte im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) befolgen.</span><span class="sxs-lookup"><span data-stu-id="ca06f-113">Start Eclipse and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="ca06f-114">Klicken Sie auf das Menü **Datei** und dann auf **Neu** und **Dynamisches Webprojekt**.</span><span class="sxs-lookup"><span data-stu-id="ca06f-114">Click the **File** menu, then click **New**, and then click **Dynamic Web Project**.</span></span>
   
   ![Erstellen eines neuen Projekts][file-new-project]

1. <span data-ttu-id="ca06f-116">Geben Sie im Dialogfeld **Neues dynamisches Webprojekt** Ihren Projektnamen und den Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="ca06f-116">In the **New Dynamic Web Project** dialog box, specify your project name and location, and then click **Finish**.</span></span>
   
   ![Angeben des Projektnamens][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="ca06f-118">Erstellen einer Azure-Containerregistrierung, die als private Docker-Registrierung verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="ca06f-118">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="ca06f-119">Die folgende Anleitung führt Sie durch die Verwendung des Azure-Portals zur Erstellung einer Azure-Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="ca06f-119">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ca06f-120">Wenn Sie statt des Azure-Portals die Azure CLI verwenden möchten, führen Sie die Schritte unter [Erstellen einer privaten Docker-Containerregistrierung mit der Azure CLI 2.0][Create Docker Registry using Azure CLI] aus.</span><span class="sxs-lookup"><span data-stu-id="ca06f-120">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="ca06f-121">Navigieren Sie zum [Azure-Portal], und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="ca06f-121">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="ca06f-122">Nachdem Sie sich im Azure-Portal bei Ihrem Konto angemeldet haben, können Sie die Schritte im Artikel [Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal] ausführen, die im Folgenden aus Gründen der Zweckmäßigkeit umschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="ca06f-122">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="ca06f-123">Klicken Sie auf das Menüsymbol für **+ Ressource erstellen** und dann auf **Container** und **Containerregistrierung**.</span><span class="sxs-lookup"><span data-stu-id="ca06f-123">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![Erstellen einer neuen Azure-Containerregistrierung][create-container-registry-01]

1. <span data-ttu-id="ca06f-125">Wenn die Seite **Containerregistrierung erstellen** angezeigt wird, geben Sie Ihren **Registrierungsnamen** und die **Ressourcengruppe** ein, wählen Sie bei dem **Administratorbenutzer** die Option **Aktivieren** aus, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="ca06f-125">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Konfigurieren der Einstellungen für die Azure-Containerregistrierung][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="ca06f-127">Bereitstellen Ihrer Web-App in einem Docker-Container</span><span class="sxs-lookup"><span data-stu-id="ca06f-127">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="ca06f-128">Klicken Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie **Azure** aus, und klicken Sie dann auf **Docker-Unterstützung hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="ca06f-128">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="ca06f-129">Damit wird automatisch eine Docker-Datei mit einer Standardkonfiguration erstellt.</span><span class="sxs-lookup"><span data-stu-id="ca06f-129">This will automatically create a Docker file with a default configuration.</span></span>

   ![Hinzufügen der Docker-Unterstützung][add-docker-support]

1. <span data-ttu-id="ca06f-131">Nachdem Sie die Docker-Unterstützung hinzugefügt haben, können Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt klicken, die Option **Azure** wählen und dann auf **Publish to Web App for Containers** (In Web-App für Container veröffentlichen) klicken.</span><span class="sxs-lookup"><span data-stu-id="ca06f-131">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Publish to Web App for Containers**.</span></span>

   ![Veröffentlichen in Web-App für Container][run-on-web-app-for-containers]

1. <span data-ttu-id="ca06f-133">Geben Sie die erforderlichen Informationen ein, wenn das Dialogfeld **Run on Web App for Containers** (In Web-App für Container ausführen) angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="ca06f-133">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="ca06f-134">**Docker-Datei**: Hiermit wird der Pfad zu der Docker-Datei angegeben, die erstellt wurde, als Sie Ihrem Projekt die Docker-Unterstützung hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="ca06f-134">**Docker File**: This specifies the path to the Docker file that was created when you added Docker support to your project.</span></span> 

   * <span data-ttu-id="ca06f-135">**Containerregistrierung**: Wählen Sie im Dropdownmenü die Containerregistrierung aus, die Sie im vorherigen Abschnitt dieses Artikels erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="ca06f-135">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="ca06f-136">Die Felder für **Server-URL**, **Benutzername** und **Kennwort** werden automatisch ausgefüllt.</span><span class="sxs-lookup"><span data-stu-id="ca06f-136">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="ca06f-137">**Image und Tag**: Gibt den Namen des Containerimages an, wobei in der Regel die folgende Syntax verwendet wird: „*Registrierung*.azurecr.io/*App-Name*:latest“. Hierbei gilt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="ca06f-137">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="ca06f-138">*Registrierung* ist Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels.</span><span class="sxs-lookup"><span data-stu-id="ca06f-138">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="ca06f-139">*App-Name* ist der Name Ihrer Web-App.</span><span class="sxs-lookup"><span data-stu-id="ca06f-139">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="ca06f-140">**Web-App für Container**: Wählen Sie **Vorhandene verwenden** oder **Neu erstellen**, um anzugeben, ob Sie den Container in einer vorhandenen Web-App bereitstellen oder eine neue Web-App erstellen.</span><span class="sxs-lookup"><span data-stu-id="ca06f-140">**Web App for Container**: Choose **Use Existing** or **Create New** to specify whether you will deploy your container to an existing web app or create a new web app.</span></span>  <span data-ttu-id="ca06f-141">Mit dem von Ihnen angegebenen **App-Namen** wird die URL für Ihre Web-App erstellt, z. B. *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="ca06f-141">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="ca06f-142">**Ressourcengruppe**: Gibt an, ob Sie eine vorhandene Ressourcengruppe verwenden oder eine neue erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="ca06f-142">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="ca06f-143">**App Service-Plan**: Gibt an, ob Sie einen vorhandenen App Service-Plan verwenden oder einen neuen erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="ca06f-143">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Ausführen von Web-App für Container][run-on-web-app-linux]

1. <span data-ttu-id="ca06f-145">Wenn Sie das Konfigurieren der oben aufgeführten Einstellungen abgeschlossen haben, können Sie auf **OK** klicken, um Ihre Web-App in Azure zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="ca06f-145">When you have finished configuring the settings listed above, click **OK** to publish your web app to Azure.</span></span>

1. <span data-ttu-id="ca06f-146">Nach der Veröffentlichung Ihrer Web-App können Sie zu der URL navigieren, die für Ihre Web-App zuvor angegeben wurde, z. B. *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="ca06f-146">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![Navigieren zu Ihrer Web-App][browsing-to-web-app]

## <a name="next-steps"></a><span data-ttu-id="ca06f-148">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="ca06f-148">Next steps</span></span>

<span data-ttu-id="ca06f-149">Weitere Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website][Docker].</span><span class="sxs-lookup"><span data-stu-id="ca06f-149">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

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

[add-docker-support]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-eclipse-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/file-new-project.png
[project-name]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-linux.png
