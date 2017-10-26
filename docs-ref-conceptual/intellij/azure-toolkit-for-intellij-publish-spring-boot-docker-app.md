---
title: "Veröffentlichen einer Spring Boot-App als Docker-Container mit dem Azure-Toolkit für IntelliJ"
description: "Erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine Web-App in Microsoft Azure als Docker-Container veröffentlichen."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm
ms.openlocfilehash: 19621d0b780cf0607171fd8c6d46aaf17d57cc49
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="a6889-103">Veröffentlichen einer Spring Boot-App als Docker-Container mit dem Azure-Toolkit für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a6889-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="a6889-104">[Spring Framework] ist eine Open Source-Lösung, die Java-Entwickler bei der Erstellung professioneller Anwendungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a6889-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="a6889-105">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="a6889-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="a6889-106">[Docker] ist eine Open Source-Lösung, die Entwickler beim Automatisieren der Bereitstellung, Skalierung und Verwaltung ihrer in Containern ausgeführten Anwendungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a6889-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="a6889-107">In diesem Tutorial erfahren Sie, wie Sie mithilfe des Azure-Toolkits für IntelliJ eine Spring Boot-Anwendung als Docker-Container in Microsoft Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a6889-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="a6889-108">Klonen des standardmäßigen Spring Boot-Docker-Repositorys</span><span class="sxs-lookup"><span data-stu-id="a6889-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="a6889-109">Mit den folgenden Schritten wird das Spring Boot-Docker-Repository mithilfe von IntelliJ geklont.</span><span class="sxs-lookup"><span data-stu-id="a6889-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="a6889-110">Informationen zur Verwendung einer Befehlszeile finden unter [Deploy a Spring Boot application on Linux in the Azure Container Service][Deploy Spring Boot on Linux in ACS] (Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service).</span><span class="sxs-lookup"><span data-stu-id="a6889-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="a6889-111">Öffnen Sie IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="a6889-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="a6889-112">Wählen Sie auf der Willkommensseite in der Liste **Check out from version control** (Von Versionskontrolle auschecken) die Option **GitHub** aus.</span><span class="sxs-lookup"><span data-stu-id="a6889-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![GitHub-Option für die Versionskontrolle][CL01]

1. <span data-ttu-id="a6889-114">Geben Sie Ihre Anmeldeinformationen ein, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="a6889-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="a6889-115">GitHub-Anmeldung unter Verwendung von Benutzername und Kennwort:</span><span class="sxs-lookup"><span data-stu-id="a6889-115">If you are using a username/password to log in to GitHub:</span></span> 

      ![Dialogfeld für die Eingabe von Benutzername und Kennwort für GitHub][CL02a]

   * <span data-ttu-id="a6889-117">Tokenbasierte GitHub-Anmeldung:</span><span class="sxs-lookup"><span data-stu-id="a6889-117">If you are using a token to log in to GitHub:</span></span> 

      ![Dialogfeld für die Eingabe eines GitHub-Tokens][CL02b]

1. <span data-ttu-id="a6889-119">Geben Sie **https://github.com/spring-guides/gs-spring-boot-docker.git** als Repository-URL sowie Ihren lokalen Pfad und Ordner an, und klicken Sie anschließend auf **Klonen**.</span><span class="sxs-lookup"><span data-stu-id="a6889-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Dialogfeld „Repository klonen“][CL03]

1. <span data-ttu-id="a6889-121">Wenn Sie zum Erstellen eines IntelliJ-Projekts aufgefordert werden, wählen Sie **Nein** aus.</span><span class="sxs-lookup"><span data-stu-id="a6889-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![Ablehnen der Erstellung eines IntelliJ-Projekts][CL04]

1. <span data-ttu-id="a6889-123">Klicken Sie auf der Willkommensseite auf **Projekt importieren**.</span><span class="sxs-lookup"><span data-stu-id="a6889-123">On the welcome page, click **Import Project**.</span></span>

   ![Klicken auf „Projekt importieren“][CL05]

1. <span data-ttu-id="a6889-125">Suchen Sie den Pfad, an dem Sie das Spring Boot-Repository geklont haben, wählen Sie den **gesamten** Ordner unter dem Stammverzeichnis aus, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6889-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![Auswählen eines zu importierenden Ordners][CL06]

1. <span data-ttu-id="a6889-127">Wählen Sie **Create project from existing sources** (Projekt aus vorhandenen Quellen erstellen) aus, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="a6889-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Option zum Erstellen eines Projekts auf der Grundlage vorhandener Quellen][CL07]

1. <span data-ttu-id="a6889-129">Geben Sie einen Projektnamen ein, oder übernehmen Sie den Standardnamen, überprüfen Sie den Pfad für den **gesamten** Ordner, und klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="a6889-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![Angeben des Projektnamens][CL08]

1. <span data-ttu-id="a6889-131">Passen Sie Verzeichnisse für den Import an, und klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="a6889-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Auswahl von Verzeichnissen][CL09]

1. <span data-ttu-id="a6889-133">Überprüfen Sie die zu importierenden Bibliotheken, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="a6889-133">Review the libraries to import, and then click **Next**.</span></span>

   ![Überprüfen der Projektbibliotheken][CL10]

1. <span data-ttu-id="a6889-135">Überprüfen Sie die Modulstruktur, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="a6889-135">Review the module structure, and then click **Next**.</span></span>

   ![Überprüfen der Modulstruktur][CL11]

1. <span data-ttu-id="a6889-137">Geben Sie Ihr JDK, an und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="a6889-137">Specify your JDK, and then click **Next**.</span></span>

   ![Angeben eines JDKs][CL12]

1. <span data-ttu-id="a6889-139">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="a6889-139">Click **Finish**.</span></span>

   ![Schaltfläche „Fertig stellen“][CL13]

<span data-ttu-id="a6889-141">IntelliJ importiert die Spring Boot-App als Projekt und zeigt nach Abschluss des Importvorgangs die Struktur an.</span><span class="sxs-lookup"><span data-stu-id="a6889-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![Spring Boot-App in IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="a6889-143">Erstellen Ihrer Spring Boot-App</span><span class="sxs-lookup"><span data-stu-id="a6889-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="a6889-144">Erstellen der App mithilfe des Maven-POMs</span><span class="sxs-lookup"><span data-stu-id="a6889-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="a6889-145">Öffnen Sie das Maven-Toolfenster, sofern es nicht bereits geöffnet ist.</span><span class="sxs-lookup"><span data-stu-id="a6889-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="a6889-146">Klicken Sie auf **Ansicht** > **Toolfenster** > **Maven-Projekte**.</span><span class="sxs-lookup"><span data-stu-id="a6889-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Befehle „Toolfenster“ und „Maven-Projekte“][BU01]

1. <span data-ttu-id="a6889-148">Klicken Sie im Maven-Toolfenster mit der rechten Maustaste auf **Paket**, und wählen Sie **Run Maven Build** (Maven-Build ausführen) aus.</span><span class="sxs-lookup"><span data-stu-id="a6889-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="a6889-149">(Sollte Ihr Maven-Projekt nicht automatisch angezeigt werden, klicken Sie auf der Maven-Symbolleiste auf das Symbol **Reimport** (Erneut importieren).)</span><span class="sxs-lookup"><span data-stu-id="a6889-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Befehl zum Ausführen des Maven-Builds][BU02]

1. <span data-ttu-id="a6889-151">Wenn Ihre Spring Boot-App erfolgreich erstellt wurde, zeigt IntelliJ eine entsprechende **Meldung** an.</span><span class="sxs-lookup"><span data-stu-id="a6889-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Meldung nach erfolgreicher Erstellung][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="a6889-153">Erstellen eines bereitstellungsfähigen Artefakts</span><span class="sxs-lookup"><span data-stu-id="a6889-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="a6889-154">Zum Veröffentlichen Ihrer Spring Boot-App müssen Sie ein bereitstellungsfähiges Artefakt erstellen.</span><span class="sxs-lookup"><span data-stu-id="a6889-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="a6889-155">Führen Sie die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="a6889-155">Use the following steps:</span></span>

1. <span data-ttu-id="a6889-156">Öffnen Sie Ihr Web-App-Projekt in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="a6889-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="a6889-157">Klicken Sie auf **Datei** und dann auf **Projektstruktur**.</span><span class="sxs-lookup"><span data-stu-id="a6889-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Befehl „Projektstruktur“][ART01]

1. <span data-ttu-id="a6889-159">Klicken Sie auf das grüne Plussymbol (**+**), um ein Artefakt hinzuzufügen. Klicken Sie anschließend auf **JAR** und dann auf **Leer**.</span><span class="sxs-lookup"><span data-stu-id="a6889-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Hinzufügen eines Artefakts][ART02]

1. <span data-ttu-id="a6889-161">Benennen Sie Ihr Artefakt und stellen Sie dabei sicher, dass Sie nicht die Erweiterung „.jar“ anfügen. Geben Sie anschließend den Zielordner für die Maven-Ausgabe an.</span><span class="sxs-lookup"><span data-stu-id="a6889-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![Angeben der Eigenschaften des Artefakts][ART03]

1. <span data-ttu-id="a6889-163">Erstellen Sie ein Manifest für Ihr Artefakt (optional):</span><span class="sxs-lookup"><span data-stu-id="a6889-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="a6889-164">a.</span><span class="sxs-lookup"><span data-stu-id="a6889-164">a.</span></span> <span data-ttu-id="a6889-165">Klicken Sie auf **Create Manifest** (Manifest erstellen).</span><span class="sxs-lookup"><span data-stu-id="a6889-165">Click **Create Manifest**.</span></span>

      ![Klicken auf die Schaltfläche „Create Manifest“ (Manifest erstellen)][ART04a]

   <span data-ttu-id="a6889-167">b.</span><span class="sxs-lookup"><span data-stu-id="a6889-167">b.</span></span> <span data-ttu-id="a6889-168">Wählen Sie den Standardpfad für das Artefakt aus, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6889-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![Angeben des Artefaktpfads][ART04b]

   <span data-ttu-id="a6889-170">c.</span><span class="sxs-lookup"><span data-stu-id="a6889-170">c.</span></span> <span data-ttu-id="a6889-171">Klicken Sie auf die Auslassungspunkte (**...**), um die Hauptklasse zu suchen.</span><span class="sxs-lookup"><span data-stu-id="a6889-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![Suchen der Hauptklasse][ART04c]

   <span data-ttu-id="a6889-173">d.</span><span class="sxs-lookup"><span data-stu-id="a6889-173">d.</span></span> <span data-ttu-id="a6889-174">Wählen Sie die Hauptklasse aus, und klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6889-174">Choose your main class, and then click **OK**.</span></span>

      ![Angeben der Hauptklasse][ART04d]

1. <span data-ttu-id="a6889-176">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6889-176">Click **OK**.</span></span>

   ![Schließen des Dialogfelds mit der Projektstruktur][ART05]

> [!NOTE]
> <span data-ttu-id="a6889-178">Weitere Informationen zum Erstellen von Artefakten in IntelliJ finden Sie auf der JetBrains-Website unter [Konfigurieren von Artefakten].</span><span class="sxs-lookup"><span data-stu-id="a6889-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="a6889-179">Erstellen des Artefakts für die Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="a6889-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="a6889-180">Klicken Sie auf **Erstellen** und anschließend auf **Artefakte**.</span><span class="sxs-lookup"><span data-stu-id="a6889-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Befehl zum Erstellen von Artefakten][BU04]

1. <span data-ttu-id="a6889-182">Klicken Sie auf **Erstellen**, wenn das Kontextmenü **Build Artifact** (Artefakt erstellen) angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="a6889-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Kontextmenü für die Artefakterstellung][BU05]

<span data-ttu-id="a6889-184">IntelliJ zeigt das vollständige Artefakt für Ihre Spring Boot-App im Projekt-Toolfenster an.</span><span class="sxs-lookup"><span data-stu-id="a6889-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![Erstelltes Artefakt][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="a6889-186">Veröffentlichen Ihrer Web-App in Azure mithilfe eines Docker-Containers</span><span class="sxs-lookup"><span data-stu-id="a6889-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="a6889-187">Melden Sie sich gemäß der [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ][Azure Sign In for IntelliJ] bei Ihrem Azure-Konto an, sofern noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="a6889-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="a6889-188">Klicken Sie im Toolfenster „Project Explorer“ mit der rechten Maustaste auf das Projekt, und wählen Sie dann **Azure** > **Publish as Docker Container** (Als Docker-Container veröffentlichen) aus.</span><span class="sxs-lookup"><span data-stu-id="a6889-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Befehl zum Veröffentlichen als Docker-Container][PU01]

1. <span data-ttu-id="a6889-190">Wenn das Dialogfeld **Deploy Docker Container on Azure** (Bereitstellen des Docker-Containers in Azure) erscheint, werden alle vorhandenen Docker-Hosts angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a6889-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="a6889-191">Wenn Sie in einem vorhandenen Host bereitstellen möchten, fahren Sie mit Schritt 4 fort.</span><span class="sxs-lookup"><span data-stu-id="a6889-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="a6889-192">Führen Sie andernfalls die folgenden Schritte aus, um einen Host zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="a6889-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="a6889-193">a.</span><span class="sxs-lookup"><span data-stu-id="a6889-193">a.</span></span> <span data-ttu-id="a6889-194">Klicken Sie auf das grüne Plussymbol (**+**).</span><span class="sxs-lookup"><span data-stu-id="a6889-194">Click the green plus (**+**) symbol.</span></span>

      ![Hinzufügen eines neuen Docker-Hosts][PU02]

   <span data-ttu-id="a6889-196">b.</span><span class="sxs-lookup"><span data-stu-id="a6889-196">b.</span></span> <span data-ttu-id="a6889-197">Wenn das Dialogfeld **Create Docker Host** (Docker-Host erstellen) angezeigt wird, können Sie wahlweise die Standardeinstellungen übernehmen oder beliebige benutzerdefinierte Einstellungen für den neuen Docker-Host angeben.</span><span class="sxs-lookup"><span data-stu-id="a6889-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="a6889-198">(Ausführliche Beschreibungen der verschiedenen Einstellungen finden Sie unter [Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für IntelliJ][Publish Container with Azure Toolkit].) Klicken Sie auf **Weiter**, nachdem Sie die gewünschten Einstellungen eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="a6889-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Angeben von Docker-Hostoptionen][PU03a]

   <span data-ttu-id="a6889-200">c.</span><span class="sxs-lookup"><span data-stu-id="a6889-200">c.</span></span> <span data-ttu-id="a6889-201">Sie können wahlweise vorhandene Anmeldeinformationen aus einem Azure-Schlüsseltresor verwenden oder neue Docker-Anmeldeinformationen eingeben.</span><span class="sxs-lookup"><span data-stu-id="a6889-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="a6889-202">Klicken Sie auf **Fertig stellen**, nachdem Sie Ihre Optionen angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="a6889-202">Click **Finish** when you have specified your options.</span></span>

      ![Angeben von Docker-Hostanmeldeinformationen][PU03b]

1. <span data-ttu-id="a6889-204">Wählen Sie Ihren Docker-Host aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="a6889-204">Select your Docker host, and then click **Next**.</span></span>

   ![Auswählen des zu verwendenden Docker-Hosts][PU04]

1. <span data-ttu-id="a6889-206">Geben Sie auf der letzten Seite des Dialogfelds **Deploy Docker Container on Azure** (Bereitstellen des Docker-Containers in Azure) folgende Optionen an:</span><span class="sxs-lookup"><span data-stu-id="a6889-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="a6889-207">a.</span><span class="sxs-lookup"><span data-stu-id="a6889-207">a.</span></span> <span data-ttu-id="a6889-208">Sie können entweder einen benutzerdefinierten Namen für den Container angeben, der Ihren Docker-Container hostet, oder die Standardeinstellung übernehmen.</span><span class="sxs-lookup"><span data-stu-id="a6889-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="a6889-209">b.</span><span class="sxs-lookup"><span data-stu-id="a6889-209">b.</span></span> <span data-ttu-id="a6889-210">Geben Sie die TCP-Ports für Ihren Docker-Host mit folgender Syntax ein: *[externer Port]*:*[interner Port]*.</span><span class="sxs-lookup"><span data-stu-id="a6889-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="a6889-211">**80:8080** gibt beispielsweise den externen Port 80 und den internen Spring Boot-Standardport 8080 an.</span><span class="sxs-lookup"><span data-stu-id="a6889-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="a6889-212">Wenn Sie den internen Port angepasst haben (beispielsweise durch Bearbeiten der Datei „application.yml“), müssen Sie diese Portnummer angeben, damit das Routing in Azure ordnungsgemäß funktioniert.</span><span class="sxs-lookup"><span data-stu-id="a6889-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="a6889-213">c.</span><span class="sxs-lookup"><span data-stu-id="a6889-213">c.</span></span> <span data-ttu-id="a6889-214">Klicken Sie nach dem Konfigurieren dieser Optionen auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="a6889-214">After you have configured these options, click **Finish**.</span></span>

   ![Bereitstellen eines Docker-Containers in Azure][PU05]

1. <span data-ttu-id="a6889-216">Nachdem die Veröffentlichung des Azure-Toolkits abgeschlossen ist, zeigt das Azure-Aktivitätsprotokoll den Status **Veröffentlicht** an.</span><span class="sxs-lookup"><span data-stu-id="a6889-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Docker-Host erfolgreich bereitgestellt][PU06]

## <a name="next-steps"></a><span data-ttu-id="a6889-218">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="a6889-218">Next steps</span></span>

<span data-ttu-id="a6889-219">Informationen zu weiteren Spring Boot-App-Erstellungsmethoden mit IntelliJ finden Sie auf der JetBrains-Website unter [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) (Erstellen von Spring Boot-Projekten).</span><span class="sxs-lookup"><span data-stu-id="a6889-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Konfigurieren von Artefakten]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
