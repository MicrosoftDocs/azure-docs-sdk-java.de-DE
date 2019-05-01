---
title: Veröffentlichen einer Spring Boot-App als Docker-Container mit dem Azure-Toolkit für Eclipse
description: Erfahren Sie, wie Sie mit dem Azure-Toolkit für Eclipse eine Web-App in Microsoft Azure als Docker-Container veröffentlichen.
services: ''
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
ms.openlocfilehash: 5f70d8dd7e9b59c365d83c185f430a5a9c75e838
ms.sourcegitcommit: 4f1acf05e3bbb7eb6bca9b65300c1c5b9772185a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456317"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="e5058-103">Veröffentlichen einer Spring Boot-App als Docker-Container mit dem Azure-Toolkit für Eclipse</span><span class="sxs-lookup"><span data-stu-id="e5058-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="e5058-104">[Spring Framework] ist eine Open Source-Lösung, die Java-Entwickler bei der Erstellung professioneller Anwendungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e5058-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e5058-105">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="e5058-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="e5058-106">[Docker] ist eine Open Source-Lösung, die Entwickler beim Automatisieren der Bereitstellung, Skalierung und Verwaltung ihrer in Containern ausgeführten Anwendungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e5058-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="e5058-107">In diesem Tutorial erfahren Sie, wie Sie mithilfe des Azure-Toolkits für Eclipse eine Spring Boot-Anwendung als Docker-Container in Microsoft Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e5058-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a><span data-ttu-id="e5058-108">Klonen des standardmäßigen Spring Boot-Docker-Repositorys</span><span class="sxs-lookup"><span data-stu-id="e5058-108">Clone the default Spring Boot Docker repository</span></span>

### <a name="import-the-public-repository"></a><span data-ttu-id="e5058-109">Importieren des öffentlichen Repositorys</span><span class="sxs-lookup"><span data-stu-id="e5058-109">Import the public repository</span></span>

<span data-ttu-id="e5058-110">Mit den folgenden Schritte wird das Spring Boot-Docker-Repository auf Ihrem lokalen Computer mithilfe von IntelliJ geklont.</span><span class="sxs-lookup"><span data-stu-id="e5058-110">The following steps walk you through cloning the Spring Boot Docker repository to your local computer by using IntelliJ.</span></span> <span data-ttu-id="e5058-111">Informationen zur Verwendung einer Befehlszeile finden Sie unter [Deploy a Spring Boot application on Linux in the Azure Container Service][Deploy Spring Boot on Linux in AKS] (Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service).</span><span class="sxs-lookup"><span data-stu-id="e5058-111">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="e5058-112">Öffnen Sie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e5058-112">Open Eclipse.</span></span>

1. <span data-ttu-id="e5058-113">Klicken Sie auf **Datei** > **Importieren**.</span><span class="sxs-lookup"><span data-stu-id="e5058-113">Click **File** > **Import**.</span></span>

   ![Menü „Datei importieren“][CL01]

1. <span data-ttu-id="e5058-115">Wenn das Dialogfeld **Importieren** geöffnet wird:</span><span class="sxs-lookup"><span data-stu-id="e5058-115">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="e5058-116">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-116">a.</span></span> <span data-ttu-id="e5058-117">Erweitern Sie **Git**.</span><span class="sxs-lookup"><span data-stu-id="e5058-117">Expand **Git**.</span></span>

   <span data-ttu-id="e5058-118">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-118">b.</span></span> <span data-ttu-id="e5058-119">Wählen Sie **Projekte aus Git**.</span><span class="sxs-lookup"><span data-stu-id="e5058-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="e5058-120">c.</span><span class="sxs-lookup"><span data-stu-id="e5058-120">c.</span></span> <span data-ttu-id="e5058-121">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e5058-121">Click **Next**.</span></span>

   ![Dialogfeld „Importieren“][CL02]

1. <span data-ttu-id="e5058-123">Auf der Seite **Repositoryquelle auswählen**:</span><span class="sxs-lookup"><span data-stu-id="e5058-123">On the **Select Repository Source** page:</span></span>

   <span data-ttu-id="e5058-124">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-124">a.</span></span> <span data-ttu-id="e5058-125">Wählen Sie **URI klonen** aus.</span><span class="sxs-lookup"><span data-stu-id="e5058-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="e5058-126">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-126">b.</span></span> <span data-ttu-id="e5058-127">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e5058-127">Click **Next**.</span></span>

   ![Seite „Repositoryquelle auswählen“][CL03]

1. <span data-ttu-id="e5058-129">Auf der Seite **Quelle Git-Repository**:</span><span class="sxs-lookup"><span data-stu-id="e5058-129">On the **Source Git Repository** page:</span></span>

   <span data-ttu-id="e5058-130">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-130">a.</span></span> <span data-ttu-id="e5058-131">Geben Sie `https://github.com/spring-guides/gs-spring-boot-docker.git` für den **URI** ein.</span><span class="sxs-lookup"><span data-stu-id="e5058-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="e5058-132">Dadurch sollten die Felder **Host** und **Repositorypfad** automatisch mit den korrekten Werten aufgefüllt werden.</span><span class="sxs-lookup"><span data-stu-id="e5058-132">This step should automatically populate the **Host** and **Repository path** fields with the correct values.</span></span>
   
   <span data-ttu-id="e5058-133">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-133">b.</span></span> <span data-ttu-id="e5058-134">Da das Spring Boot-Repository öffentlich ist, müssen Sie nicht Ihren Git-Benutzernamen und das Kennwort eingeben.</span><span class="sxs-lookup"><span data-stu-id="e5058-134">The Spring Boot repository is public, so you should not have to enter your Git username and password.</span></span>
   
   <span data-ttu-id="e5058-135">c.</span><span class="sxs-lookup"><span data-stu-id="e5058-135">c.</span></span> <span data-ttu-id="e5058-136">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e5058-136">Click **Next**.</span></span>

   ![Seite „Quelle Git-Repository“][CL04]

1. <span data-ttu-id="e5058-138">Klicken Sie auf der Seite **Verzweigungsauswahl** auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e5058-138">On the **Branch Selection** page, click **Next**.</span></span>

   ![Seite „Verzweigungsauswahl“][CL05]

1. <span data-ttu-id="e5058-140">Auf der Seite **Lokales Ziel**:</span><span class="sxs-lookup"><span data-stu-id="e5058-140">On the **Local Destination** page:</span></span>

   <span data-ttu-id="e5058-141">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-141">a.</span></span> <span data-ttu-id="e5058-142">Geben Sie den lokalen Ordner an, in dem Ihr lokales Repository angelegt werden soll.</span><span class="sxs-lookup"><span data-stu-id="e5058-142">Specify the local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="e5058-143">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-143">b.</span></span> <span data-ttu-id="e5058-144">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e5058-144">Click **Next**.</span></span>

   ![Seite „Lokales Ziel“][CL06]

1. <span data-ttu-id="e5058-146">Auf der Seite **Assistent zum Importieren von Projekten auswählen**:</span><span class="sxs-lookup"><span data-stu-id="e5058-146">On the **Select a wizard to use for importing projects** page:</span></span>

   <span data-ttu-id="e5058-147">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-147">a.</span></span> <span data-ttu-id="e5058-148">Wählen Sie **Als allgemeines Projekt importieren** aus.</span><span class="sxs-lookup"><span data-stu-id="e5058-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="e5058-149">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-149">b.</span></span> <span data-ttu-id="e5058-150">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e5058-150">Click **Next**.</span></span>

   ![Seite „Assistent zum Importieren von Projekten auswählen“][CL07]

1. <span data-ttu-id="e5058-152">Auf der Seite **Projekte importieren**:</span><span class="sxs-lookup"><span data-stu-id="e5058-152">On the **Import Projects** page:</span></span>

   <span data-ttu-id="e5058-153">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-153">a.</span></span> <span data-ttu-id="e5058-154">Geben Sie Ihren Projektnamen an.</span><span class="sxs-lookup"><span data-stu-id="e5058-154">Specify your project name.</span></span>
   
   <span data-ttu-id="e5058-155">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-155">b.</span></span> <span data-ttu-id="e5058-156">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="e5058-156">Click **Finish**.</span></span>

   ![Seite „Projekte importieren“][CL08]

1. <span data-ttu-id="e5058-158">Nachdem das Repository erfolgreich geklont wurde, wird eine Liste aller Dateien in Eclipse angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e5058-158">When the repository is cloned successfully, you see all the files listed in Eclipse.</span></span>

   ![Lokales Repository][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="e5058-160">Erstellen eines Maven-Projekts aus dem lokalen Repository</span><span class="sxs-lookup"><span data-stu-id="e5058-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="e5058-161">Das Docker-Repository von Spring Boot enthält ein abgeschlossenes Maven-Projekt, das Sie für dieses Tutorial verwenden können.</span><span class="sxs-lookup"><span data-stu-id="e5058-161">The Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="e5058-162">Klicken Sie auf **Datei** > **Importieren**.</span><span class="sxs-lookup"><span data-stu-id="e5058-162">Click **File** > **Import**.</span></span>

   ![Befehl zum Importieren im Menü „Datei“][CL01]

1. <span data-ttu-id="e5058-164">Wenn das Dialogfeld **Importieren** geöffnet wird:</span><span class="sxs-lookup"><span data-stu-id="e5058-164">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="e5058-165">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-165">a.</span></span> <span data-ttu-id="e5058-166">Erweitern Sie **Maven**.</span><span class="sxs-lookup"><span data-stu-id="e5058-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="e5058-167">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-167">b.</span></span> <span data-ttu-id="e5058-168">Wählen Sie **Vorhandene Maven-Projekte**.</span><span class="sxs-lookup"><span data-stu-id="e5058-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="e5058-169">c.</span><span class="sxs-lookup"><span data-stu-id="e5058-169">c.</span></span> <span data-ttu-id="e5058-170">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e5058-170">Click **Next**.</span></span>

   ![Dialogfeld „Importieren“][MV01]

1. <span data-ttu-id="e5058-172">Auf der Seite **Maven-Projekte**:</span><span class="sxs-lookup"><span data-stu-id="e5058-172">On the **Maven Projects** page:</span></span>

   <span data-ttu-id="e5058-173">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-173">a.</span></span> <span data-ttu-id="e5058-174">Geben Sie unter **Stammverzeichnis** den **vollständigen** Ordner in Ihrem lokalen Repository an.</span><span class="sxs-lookup"><span data-stu-id="e5058-174">For **Root Directory**, specify the **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="e5058-175">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-175">b.</span></span> <span data-ttu-id="e5058-176">Erweitern Sie den Abschnitt **Erweitert**, und geben Sie einen benutzerdefinierten Namen für **Namensvorlage** ein.</span><span class="sxs-lookup"><span data-stu-id="e5058-176">Expand the **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="e5058-177">c.</span><span class="sxs-lookup"><span data-stu-id="e5058-177">c.</span></span> <span data-ttu-id="e5058-178">Aktivieren Sie das Kontrollkästchen für die Datei **pom.xml** im Projekt.</span><span class="sxs-lookup"><span data-stu-id="e5058-178">Select the box for the **pom.xml** file in the project.</span></span>
   
   <span data-ttu-id="e5058-179">d.</span><span class="sxs-lookup"><span data-stu-id="e5058-179">d.</span></span> <span data-ttu-id="e5058-180">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="e5058-180">Click **Finish**.</span></span>

   ![Seite „Maven-Projekte“][MV02]

1. <span data-ttu-id="e5058-182">Nachdem das Maven-Projekt erfolgreich geöffnet wurde, wird ein zweites Projekt in Eclipse aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="e5058-182">When the Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Lokales Maven-Projekt][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="e5058-184">Erstellen der Spring Boot-App mithilfe von Maven</span><span class="sxs-lookup"><span data-stu-id="e5058-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="e5058-185">Wählen Sie im Projekt-Explorer von Eclipse das Maven-Projekt aus.</span><span class="sxs-lookup"><span data-stu-id="e5058-185">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="e5058-186">Klicken Sie auf **Ausführen** > **Ausführen als** > **Maven-Build**.</span><span class="sxs-lookup"><span data-stu-id="e5058-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Befehle zum Ausführen als Maven-Build][BU01]

1. <span data-ttu-id="e5058-188">Nachdem die Anwendung erfolgreich erstellt wurde, wird im Konsolenfenster der Status angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e5058-188">When your application is successfully built, the console window shows the status.</span></span>

   ![Erfolgreicher Maven-Build][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="e5058-190">Veröffentlichen Ihrer Web-App in Azure mithilfe eines Docker-Containers</span><span class="sxs-lookup"><span data-stu-id="e5058-190">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="e5058-191">Wählen Sie im Projekt-Explorer von Eclipse das Maven-Projekt aus.</span><span class="sxs-lookup"><span data-stu-id="e5058-191">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="e5058-192">Klicken Sie auf das Azure-Menü **Veröffentlichen** und anschließend auf **Publish as Docker Container** (Als Docker-Container veröffentlichen).</span><span class="sxs-lookup"><span data-stu-id="e5058-192">Click the Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Befehl „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PU01]

1. <span data-ttu-id="e5058-194">Wenn das Dialogfeld **Deploying Docker Container on Azure** (Docker-Container wird in Azure bereitgestellt) angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="e5058-194">When the **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="e5058-195">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-195">a.</span></span> <span data-ttu-id="e5058-196">Geben Sie einen benutzerdefinierten Docker-Imagenamen ein.</span><span class="sxs-lookup"><span data-stu-id="e5058-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="e5058-197">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-197">b.</span></span> <span data-ttu-id="e5058-198">Geben Sie für **Artifact to deploy** (Bereitzustellendes Artefakt) den Pfad zur Datei **gs-spring-boot-docker-0.1.0.jar** an, die Sie soeben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="e5058-198">For **Artifact to deploy**, specify the path to the **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Angeben von Docker-Optionen][PU02]

   <span data-ttu-id="e5058-200">Alle vorhandenen Docker-Hosts werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e5058-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="e5058-201">Fahren Sie für die Bereitstellung in einem vorhandenen Host mit Schritt 5 fort.</span><span class="sxs-lookup"><span data-stu-id="e5058-201">If you choose to deploy to an existing host, you can skip to step 5.</span></span> <span data-ttu-id="e5058-202">Führen Sie andernfalls die folgenden Schritte aus, um einen Host zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="e5058-202">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="e5058-203">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-203">a.</span></span> <span data-ttu-id="e5058-204">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="e5058-204">Click **Add**.</span></span>

      ![Hinzufügen eines neuen Docker-Hosts][PU03]

   <span data-ttu-id="e5058-206">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-206">b.</span></span> <span data-ttu-id="e5058-207">Wenn das Dialogfeld **Create Docker Host** (Docker-Host erstellen) angezeigt wird, können Sie wahlweise die Standardeinstellungen übernehmen oder beliebige benutzerdefinierte Einstellungen für den neuen Docker-Host angeben.</span><span class="sxs-lookup"><span data-stu-id="e5058-207">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="e5058-208">(Ausführliche Beschreibungen der verschiedenen Einstellungen finden Sie unter [Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für IntelliJ][Publish Container with Azure Toolkit].) Klicken Sie auf **Weiter**, nachdem Sie die gewünschten Einstellungen eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="e5058-208">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Angeben von Docker-Hostoptionen][PU04]

   <span data-ttu-id="e5058-210">c.</span><span class="sxs-lookup"><span data-stu-id="e5058-210">c.</span></span> <span data-ttu-id="e5058-211">Sie können wahlweise vorhandene Anmeldeinformationen aus einem Azure-Schlüsseltresor verwenden oder neue Docker-Anmeldeinformationen eingeben.</span><span class="sxs-lookup"><span data-stu-id="e5058-211">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="e5058-212">Klicken Sie auf **Fertig stellen**, nachdem Sie Ihre Optionen angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="e5058-212">Click **Finish** when you have specified your options.</span></span>

      ![Angeben von Docker-Hostanmeldeinformationen][PU05]

1. <span data-ttu-id="e5058-214">Wählen Sie Ihren Docker-Host aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e5058-214">Select your Docker host, and then click **Next**.</span></span>

   ![Auswählen des Docker-Hosts, der verwendet werden soll][PU06]

1. <span data-ttu-id="e5058-216">Geben Sie auf der letzten Seite des Dialogfelds **Deploying Docker Container on Azure** (Docker-Container wird in Azure bereitgestellt) folgende Optionen an:</span><span class="sxs-lookup"><span data-stu-id="e5058-216">On the last page of the **Deploying Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="e5058-217">a.</span><span class="sxs-lookup"><span data-stu-id="e5058-217">a.</span></span> <span data-ttu-id="e5058-218">Sie können entweder einen benutzerdefinierten Namen für den Container angeben, der Ihren Docker-Container hostet, oder die Standardeinstellung übernehmen.</span><span class="sxs-lookup"><span data-stu-id="e5058-218">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="e5058-219">b.</span><span class="sxs-lookup"><span data-stu-id="e5058-219">b.</span></span> <span data-ttu-id="e5058-220">Geben Sie die TCP-Ports für Ihren Docker-Host mit folgender Syntax ein: *[externer Port]*:*[interner Port]*.</span><span class="sxs-lookup"><span data-stu-id="e5058-220">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="e5058-221">**80:8080** gibt beispielsweise den externen Port 80 und den internen Spring Boot-Standardport 8080 an.</span><span class="sxs-lookup"><span data-stu-id="e5058-221">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="e5058-222">Wenn Sie den internen Port angepasst haben (beispielsweise durch Bearbeiten der Datei „application.yml“), müssen Sie diese Portnummer angeben, damit das Routing in Azure ordnungsgemäß funktioniert.</span><span class="sxs-lookup"><span data-stu-id="e5058-222">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="e5058-223">c.</span><span class="sxs-lookup"><span data-stu-id="e5058-223">c.</span></span> <span data-ttu-id="e5058-224">Klicken Sie nach dem Konfigurieren dieser Optionen auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="e5058-224">After you configure these options, click **Finish**.</span></span>

   ![Bereitstellen eines Docker-Containers in Azure][PU07]

1. <span data-ttu-id="e5058-226">Nachdem die Veröffentlichung des Azure-Toolkits abgeschlossen ist, zeigt das Azure-Aktivitätsprotokoll den Status **Veröffentlicht** an.</span><span class="sxs-lookup"><span data-stu-id="e5058-226">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Docker-Host erfolgreich bereitgestellt][PU08]

## <a name="next-steps"></a><span data-ttu-id="e5058-228">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="e5058-228">Next steps</span></span>

<span data-ttu-id="e5058-229">Zusätzliche Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website](https://www.docker.com/).</span><span class="sxs-lookup"><span data-stu-id="e5058-229">For additional resources for Docker, see the official [Docker website](https://www.docker.com/).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: azure-toolkit-for-eclipse-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
