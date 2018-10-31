---
title: CI/CD für MicroProfile-Anwendungen mit Azure DevOps
description: Erfahren Sie, wie Sie mithilfe von Azure DevOps einen CI/CD-Releasezyklus zum Bereitstellen einer MicroProfile-Anwendung in einer Azure-Web-App für Container-Instanz einrichten.
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: 818e37291fa47f99cb161c63a86062bddbf6248c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799936"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="b677e-103">CI/CD für MicroProfile-Anwendungen mit Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="b677e-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="b677e-104">In diesem Tutorial wird beschrieben, wie Java EE-Entwickler mithilfe von Azure DevOps (früher bekannt als VSTS) mühelos einen CI/CD-Releasezyklus zum Bereitstellen ihrer [MicroProfile](http://microprofile.io)-Anwendungen in einer Azure-Web-App für Container-Instanz einrichten können.</span><span class="sxs-lookup"><span data-stu-id="b677e-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="b677e-105">In diesem Beispiel verwenden wir eine MicroProfile-Anwendung, die [Payara Micro](https://www.payara.fish/payara_micro) als Basisimage nutzt.</span><span class="sxs-lookup"><span data-stu-id="b677e-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="b677e-106">Wir beginnen mit dem Azure DevOps-Containerisierungsprozess, indem wir ein Docker-Image erstellen und das Containerimage in eine Azure Container Registry-Instanz pushen.</span><span class="sxs-lookup"><span data-stu-id="b677e-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="b677e-107">Anschließend stellen wir das Containerimage mithilfe einer Azure DevOps-Releasepipeline in einer Web-App bereit.</span><span class="sxs-lookup"><span data-stu-id="b677e-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b677e-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="b677e-108">Prerequisites</span></span>
- <span data-ttu-id="b677e-109">Kopieren und speichern Sie die Git-URL aus [GitHub](https://github.com/Azure-Samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="b677e-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="b677e-110">Registrieren Sie sich für ein [Azure DevOps](https://dev.azure.com)-Konto, oder melden Sie sich mit Ihrem Azure DevOps-Konto an.</span><span class="sxs-lookup"><span data-stu-id="b677e-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="b677e-111">Erstellen Sie ein neues [Azure DevOps-Projekt](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav), und verwenden Sie die oben genannte Git-URL zum **Importieren eines Repositorys**.</span><span class="sxs-lookup"><span data-stu-id="b677e-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="b677e-112">Erstellen Sie eine [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry)-Instanz (ACR).</span><span class="sxs-lookup"><span data-stu-id="b677e-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="b677e-113">Erstellen Sie eine Azure-Web-App für Container-Instanz.</span><span class="sxs-lookup"><span data-stu-id="b677e-113">Create an Azure Web App for Container</span></span>
  > [!NOTE]
  >
  > <span data-ttu-id="b677e-114">Wählen Sie beim Bereitstellen der Web-App-Instanz die Option „Schnellstart“ in den Containereinstellungen aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="b677e-115">Erstellen einer Builddefinition</span><span class="sxs-lookup"><span data-stu-id="b677e-115">Create a Build definition</span></span>

<span data-ttu-id="b677e-116">Jedes Mal, wenn in der Java EE-Quellanwendung Commit ausgeführt wird, führt die Builddefinition in Azure DevOps automatisch alle Aufgaben im Build aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="b677e-117">In diesem Beispiel verwendet Azure DevOps Maven zum Erstellen des Java-MicroProfile-Projekts.</span><span class="sxs-lookup"><span data-stu-id="b677e-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="b677e-118">Klicken Sie oben auf der Azure DevOps-Projektseite auf die Registerkarte „Build und Release“.</span><span class="sxs-lookup"><span data-stu-id="b677e-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="b677e-119">Klicken Sie dann auf den Link **Builds**.</span><span class="sxs-lookup"><span data-stu-id="b677e-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="b677e-120">Klicken Sie auf die Schaltfläche **Neue Pipeline** und dann auf **Weiter**, um mit der Definition Ihrer Buildaufgaben zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="b677e-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="b677e-121">Wählen Sie in der Vorlagenliste die Option „Maven“ aus, und klicken Sie auf die Schaltfläche **Anwenden**, um Ihr Java-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b677e-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="b677e-122">Wählen Sie im Dropdownmenü des Felds „Agentpool“ die Option **Gehostete Linux-Vorschau** aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
   > [!NOTE]
   >
   > <span data-ttu-id="b677e-123">Dadurch wird Azure DevOps der zu verwendende Server mitgeteilt.</span><span class="sxs-lookup"><span data-stu-id="b677e-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="b677e-124">Sie können Ihren privaten angepassten Buildserver verwenden.</span><span class="sxs-lookup"><span data-stu-id="b677e-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="b677e-125">Um Ihren Build für Continuous Integration zu konfigurieren, klicken Sie auf die Registerkarte **Trigger**, und aktivieren Sie das Kontrollkästchen **Continuous Integration aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="b677e-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 

6. <span data-ttu-id="b677e-126">Klicken Sie auf die Registerkarte <strong>Aufgaben</strong>, um zur Hauptseite für die Buildpipeline zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="b677e-126">Select the <strong>Tasks</strong> tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="b677e-127">Wählen Sie im Dropdownmenü <strong>Speichern und in Warteschlange einreihen&amp; die Option <strong>Speichern</strong> aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-127">Use the <strong>Save &amp; queue</strong> drop-down menu to select the <strong>Save</strong> option</span></span>


## <a name="create-a-docker-build-image"></a><span data-ttu-id="b677e-128">Erstellen eines Docker-Buildimages</span><span class="sxs-lookup"><span data-stu-id="b677e-128">Create a Docker Build Image</span></span>

<span data-ttu-id="b677e-129">In dieser Aufgabe erstellt Azure DevOps anhand einer Dockerfile-Datei mit einem Basisimage von Payara Micro ein Docker-Image.</span><span class="sxs-lookup"><span data-stu-id="b677e-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="b677e-130">Klicken Sie auf die Registerkarte **Aufgaben**, um zur Hauptseite für die Buildpipeline zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="b677e-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="b677e-131">Klicken Sie auf das Symbol **+**, um der Builddefinition eine neue Aufgabe hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="b677e-131">Click on the **+** icon to add new task to the build definition</span></span>

<img src="media/VSTS/Tasks-add4.png">

3. <span data-ttu-id="b677e-132">Wählen Sie in der Vorlagenliste die Option &quot;Docker&quot; aus, und klicken Sie dann auf die Schaltfläche <strong>Hinzufügen</strong>.</span><span class="sxs-lookup"><span data-stu-id="b677e-132">Select &quot;Docker&quot; from the list of templates, then click on the <strong>Add</strong> button</span></span>
4. <span data-ttu-id="b677e-133">Geben Sie einen beschreibenden Namen in das Feld <strong>Anzeigename</strong> ein.</span><span class="sxs-lookup"><span data-stu-id="b677e-133">Enter a description name for the <strong>Display name</strong> field</span></span>
5. <span data-ttu-id="b677e-134">Vergewissern Sie sich, dass im Dropdownmenü <strong>Containerregistrierungstyp</strong> die Option <strong>Azure Container Registry</strong> ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="b677e-134">Verify that <strong>Azure Container Registry</strong> is selected in the drop-down menu for <strong>Container registry type</strong>.</span></span>
<span data-ttu-id="b677e-135">&gt;</span><span class="sxs-lookup"><span data-stu-id="b677e-135">&gt;</span></span> [!NOTE]
<span data-ttu-id="b677e-136">&gt; &gt;  Wenn Sie Docker-Hub oder eine andere Registrierung verwenden, wählen Sie stattdessen &quot;Containerregistrierung&quot; aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-136">&gt; &gt;  If you are using Docker Hub or another registry, select &quot;Container Registry&quot; instead.</span></span>  <span data-ttu-id="b677e-137">Klicken Sie dann auf die Schaltfläche &quot;+ Neu&quot;, um die zugehörigen Anmelde- und Verbindungsinformationen anzugeben.</span><span class="sxs-lookup"><span data-stu-id="b677e-137">Then click on the &quot;+ New&quot; button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="b677e-138">Wechseln Sie anschließend zum Abschnitt „Befehle“, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="b677e-138">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="b677e-139">Wählen Sie im Dropdownmenü **Azure-Abonnement** Ihre Azure-Abonnement-ID aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-139">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="b677e-140">Klicken Sie auf die Schaltfläche **Autorisieren**.</span><span class="sxs-lookup"><span data-stu-id="b677e-140">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="b677e-141">Wählen Sie im Dropdownmenü **Azure Container Registry** den Namen der Registrierung aus, die Sie in Azure erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="b677e-141">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="b677e-142">Vergewissern Sie sich, dass im Dropdownmenü **Befehl** die Option **Erstellen** ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="b677e-142">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="b677e-143">Klicken Sie für die **Dockerfile** auf das Pfadnavigationssymbol neben dem Textfeld, um die Dockerfile-Datei aus dem GitHub-Projekt auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="b677e-143">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="b677e-144">Klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b677e-144">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="b677e-145">Aktivieren Sie unter **Imagename** das Kontrollkästchen **Aktuelles Tag einschließen**.</span><span class="sxs-lookup"><span data-stu-id="b677e-145">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="b677e-146">Wählen Sie im Dropdownmenü **Speichern und in Warteschlange einreihen** die Option **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-146">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="b677e-147">Pushen des Docker-Images in ACR</span><span class="sxs-lookup"><span data-stu-id="b677e-147">Push Docker Image to ACR</span></span>

<span data-ttu-id="b677e-148">In dieser Aufgabe pusht Azure DevOps das Docker-Image in Ihre Azure Container Registry-Instanz.</span><span class="sxs-lookup"><span data-stu-id="b677e-148">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="b677e-149">Dieses Image wird verwendet, um die MicroProfile-API-Anwendung als Java-Container-Web-App auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b677e-149">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="b677e-150">Da wir Docker in Azure DevOps verwenden, erstellen Sie eine neue Docker-Vorlage, indem Sie die Schritte 1 bis 7 im obigen Abschnitt **Erstellen eines Docker-Buildimages** wiederholen.</span><span class="sxs-lookup"><span data-stu-id="b677e-150">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="b677e-151">Wählen Sie im Dropdownmenü **Befehl** die Option **Push** aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-151">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="b677e-152">Klicken Sie auf die Registerkarte **Speichern und in Warteschlange einreihen**, und wählen Sie dann **Speichern und in Warteschlange einreihen** aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-152">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="b677e-153">Vergewissern Sie sich im Popupfenster, dass **Gehostete Linux-Vorschau** für den Agentpool ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="b677e-153">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="b677e-154">Klicken Sie dann auf die Schaltfläche **Speichern und in Warteschlange einreihen**.</span><span class="sxs-lookup"><span data-stu-id="b677e-154">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="b677e-155">Klicken Sie auf die Buildnummer, um zu überprüfen, ob die Buildpipeline für das Java-Projekt erfolgreich abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="b677e-155">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">


## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="b677e-156">Erstellen einer Releasedefinition für eine Java-App</span><span class="sxs-lookup"><span data-stu-id="b677e-156">Create a release definition for a Java app</span></span>

<span data-ttu-id="b677e-157">Die Releasepipeline in Azure DevOps löst die Bereitstellung von Buildartefakten in einer Zielumgebung wie Azure automatisch aus, sobald der Buildprozess erfolgreich abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="b677e-157">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="b677e-158">Die Releasepipeline kann für Entwicklungs-, Test-, Staging- oder Produktionsumgebungen erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="b677e-158">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="b677e-159">Klicken Sie oben auf der Azure DevOps-Projektseite auf die Registerkarte „Build und Release“.</span><span class="sxs-lookup"><span data-stu-id="b677e-159">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="b677e-160">Klicken Sie dann auf den Link **Releases**.</span><span class="sxs-lookup"><span data-stu-id="b677e-160">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">

2. <span data-ttu-id="b677e-161">Klicken Sie auf die Schaltfläche &quot;Neue Pipeline\*\*.</span><span class="sxs-lookup"><span data-stu-id="b677e-161">Click on the &quot;New pipeline\*\* button</span></span>
3. <span data-ttu-id="b677e-162">Wählen Sie in der Vorlagenliste die Option <strong>Java-App in Azure App Service bereitstellen</strong> aus, und klicken Sie dann auf die Schaltfläche <strong>Anwenden</strong>.</span><span class="sxs-lookup"><span data-stu-id="b677e-162">Select the <strong>Deploy a Java app to Azure App Service</strong> in the list of templates, then click on the <strong>Apply</strong> button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">

4. <span data-ttu-id="b677e-163">Legen Sie einen <strong>Stufennamen</strong> fest (z. B. „Entwicklung“, „Test“, „Staging“ oder „Produktion“).</span><span class="sxs-lookup"><span data-stu-id="b677e-163">Set a <strong>Stage name</strong> (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="b677e-164">Klicken Sie dann auf die Schaltfläche mit dem <strong>X</strong>, um das Popupfenster zu schließen.</span><span class="sxs-lookup"><span data-stu-id="b677e-164">Then click on the <strong>X</strong> button to close the pop-up window</span></span>
5. <span data-ttu-id="b677e-165">Klicken Sie im Abschnitt „Artefakte“ auf die Schaltfläche <strong>+ Hinzufügen</strong>.</span><span class="sxs-lookup"><span data-stu-id="b677e-165">Click on the <strong>+ Add</strong> button in the Artifacts section.</span></span>  <span data-ttu-id="b677e-166">Dadurch werden Artefakte aus der Builddefinition mit dieser Releasedefinition verknüpft.</span><span class="sxs-lookup"><span data-stu-id="b677e-166">This will link artifacts from the build definition to this release definition.</span></span><br/><span data-ttu-id="b677e-167">6. Wählen Sie im Dropdownmenü <strong>Source (build pipeline)</strong> (Quelle (Buildpipeline)) Ihre Builddefinition aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-167">6. Use the drop-down menu for the <strong>Source (build pipeline)</strong> to select your build definition.</span></span> <span data-ttu-id="b677e-168">Klicken Sie dann auf die Schaltfläche <strong>Hinzufügen</strong>, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="b677e-168">Then click the <strong>Add</strong> button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">

7. <span data-ttu-id="b677e-169">Klicken Sie auf die Registerkarte <strong>Aufgaben</strong> für die Pipeline.</span><span class="sxs-lookup"><span data-stu-id="b677e-169">Click on the <strong>Tasks</strong> tab on the pipeline.</span></span>  <span data-ttu-id="b677e-170">Wählen Sie dann Ihren Stufennamen aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-170">Then, select your stage name.</span></span>

<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="b677e-171">Wählen Sie im Dropdownmenü **Azure-Abonnement** Ihre Azure-Abonnement-ID aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-171">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="b677e-172">Wählen Sie im Dropdownmenü **App-Typ** die Option **Linux-App** aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-172">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="b677e-173">Wählen Sie im Dropdownmenü **App Service-Name** den Namen der Web-App für Container-Instanz aus, die Sie soeben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="b677e-173">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="b677e-174">Geben Sie den Namen Ihrer Azure Container Registry-Instanz in das Feld **Registrierung oder Namespace** ein,</span><span class="sxs-lookup"><span data-stu-id="b677e-174">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="b677e-175">beispielsweise **myregistry.azure.io**.</span><span class="sxs-lookup"><span data-stu-id="b677e-175">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="b677e-176">Geben Sie den Namen der Registrierung in das Feld **Repository** ein.</span><span class="sxs-lookup"><span data-stu-id="b677e-176">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="b677e-177">Klicken Sie auf **Azure App Service bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="b677e-177">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="b677e-178">Geben Sie das Tag für das Containerimage in das Textfeld **Tag** ein.</span><span class="sxs-lookup"><span data-stu-id="b677e-178">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="b677e-179">Klicken Sie auf **Auf Agent ausführen**.</span><span class="sxs-lookup"><span data-stu-id="b677e-179">Click on **Run on agent**.</span></span>  <span data-ttu-id="b677e-180">Wählen Sie im Dropdownmenü „Agentpool“ die Option **Gehostete Linux-Vorschau** aus</span><span class="sxs-lookup"><span data-stu-id="b677e-180">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="b677e-181">Einrichten von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="b677e-181">Setup Environment Variables</span></span>

1. <span data-ttu-id="b677e-182">Klicken Sie auf die Registerkarte **Variablen**.  Klicken Sie dann auf die Schaltfläche **+ Hinzufügen**, um Ihre Umgebungsvariablen zu definieren.</span><span class="sxs-lookup"><span data-stu-id="b677e-182">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="b677e-183">Fügen Sie die Variablennamen und -werte für die Containerregistrierungs-URL, den Benutzernamen und das Kennwort hinzu.</span><span class="sxs-lookup"><span data-stu-id="b677e-183">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="b677e-184">Klicken Sie aus Sicherheitsgründen auf das Schlosssymbol, um den Kennwortwert auszublenden.</span><span class="sxs-lookup"><span data-stu-id="b677e-184">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="b677e-185">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="b677e-185">For example:</span></span>
- <span data-ttu-id="b677e-186">registry.password</span><span class="sxs-lookup"><span data-stu-id="b677e-186">registry.password</span></span>
- <span data-ttu-id="b677e-187">registry.url</span><span class="sxs-lookup"><span data-stu-id="b677e-187">registry.url</span></span>
- <span data-ttu-id="b677e-188">registry.username</span><span class="sxs-lookup"><span data-stu-id="b677e-188">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="b677e-189">Klicken Sie auf die Registerkarte **Aufgaben**, um zur Hauptseite für die Definition der Releasepipeline zurückkehren.</span><span class="sxs-lookup"><span data-stu-id="b677e-189">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="b677e-190">Klicken Sie auf **Azure App Service bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="b677e-190">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="b677e-191">Erweitern Sie den Abschnitt **Anwendungs- und Konfigurationseinstellungen**, und klicken Sie dann auf den Navigationspfad für das Feld **App-Einstellungen**, um Umgebungsvariablen hinzuzufügen, damit während der Bereitstellung eine Verbindung mit der Containerregistrierung hergestellt wird.</span><span class="sxs-lookup"><span data-stu-id="b677e-191">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="b677e-192">Klicken Sie auf die Schaltfläche „+ Hinzufügen“, um die folgenden App-Einstellungen zu definieren und die Umgebungsvariablen zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="b677e-192">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
7. <span data-ttu-id="b677e-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span><span class="sxs-lookup"><span data-stu-id="b677e-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
8. <span data-ttu-id="b677e-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="b677e-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
9. <span data-ttu-id="b677e-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span><span class="sxs-lookup"><span data-stu-id="b677e-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">

7. <span data-ttu-id="b677e-196">Klicken Sie auf <strong>OK</strong>, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="b677e-196">Click on the <strong>OK</strong> button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="b677e-197">Einrichten von Continuous Deployment und Bereitstellen der Java-Anwendung</span><span class="sxs-lookup"><span data-stu-id="b677e-197">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="b677e-198">Klicken Sie zum Aktivieren von Continuous Deployment auf die Registerkarte **Pipelines**.</span><span class="sxs-lookup"><span data-stu-id="b677e-198">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="b677e-199">Klicken Sie im Abschnitt „Artefakte“ auf das Blitzsymbol.</span><span class="sxs-lookup"><span data-stu-id="b677e-199">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="b677e-200">Legen Sie dann **Continuous Deployment-Trigger** auf „Aktiviert“ fest.</span><span class="sxs-lookup"><span data-stu-id="b677e-200">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">

3. <span data-ttu-id="b677e-201">Klicken Sie auf die Schaltfläche <strong>Speichern</strong> und dann auf <strong>OK</strong>.</span><span class="sxs-lookup"><span data-stu-id="b677e-201">Click on the <strong>Save</strong> button, then the <strong>OK</strong> button</span></span> 
4. <span data-ttu-id="b677e-202">Klicken Sie auf das Dropdownmenü <strong>+ Freigabe</strong>, und wählen Sie dann <strong>Create a release</strong> (Release erstellen) aus.</span><span class="sxs-lookup"><span data-stu-id="b677e-202">Click on the <strong>+ Release</strong> drop-down menu, then select <strong>Create a release</strong> link</span></span>
5. <span data-ttu-id="b677e-203">Aktivieren Sie im Dropdownmenü <strong>Stages for a trigger change from automated to manual</strong> (Stufen für einen Trigger werden von automatisiert in manuell geändert) das Kontrollkästchen für Ihren Stufennamen.</span><span class="sxs-lookup"><span data-stu-id="b677e-203">Use the <strong>Stages for a trigger change from automated to manual</strong> drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="b677e-204">Klicken Sie auf die Schaltfläche <strong>Erstellen</strong>, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="b677e-204">Click the <strong>Create</strong> button to continue</span></span>
7. <span data-ttu-id="b677e-205">Klicken Sie auf die Releasenummer.</span><span class="sxs-lookup"><span data-stu-id="b677e-205">Click on the release number.</span></span>  <span data-ttu-id="b677e-206">Zeigen Sie anschließend mit dem Mauscursor auf den Stufennamen, und klicken Sie auf die Schaltfläche <strong>Bereitstellen</strong>.</span><span class="sxs-lookup"><span data-stu-id="b677e-206">Then hover your mouse cursor over the stage name and click on the <strong>Deploy</strong> button</span></span>
8. <span data-ttu-id="b677e-207">Klicken Sie im Popupfenster auf die Schaltfläche <strong>Bereitstellen</strong>, um den Prozess der Bereitstellung in Azure zu starten.</span><span class="sxs-lookup"><span data-stu-id="b677e-207">The click on the <strong>Deploy</strong> button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="b677e-208">Testen der Java-Webanwendung</span><span class="sxs-lookup"><span data-stu-id="b677e-208">Test the Java Web Application</span></span>
1. <span data-ttu-id="b677e-209">Geben Sie die Web-App-URL im Webbrowser ein:</span><span class="sxs-lookup"><span data-stu-id="b677e-209">Run the web app url in web browser:</span></span>  
   <span data-ttu-id="b677e-210">https://{Ihr-App-Service-Name}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="b677e-210">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>


<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="b677e-211">Auf der Webseite sollte **Hello Azure!** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="b677e-211">The web page should say **Hello Azure!**</span></span>

<img src="media/VSTS/web-api17.png">
