---
title: Erstellen einer einfachen Azure-Web-App in IntelliJ
description: "In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine „Hello World“-Web-App für Azure erstellen."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 323ce74f2d4dad10460a0c2bc0fb59f2bbdbbf3c
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="6f9d5-103">Erstellen einer einfachen Azure-Web-App in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="6f9d5-103">Create a basic Azure web app in IntelliJ</span></span>

<span data-ttu-id="6f9d5-104">Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe des [Azure-Toolkits für IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="6f9d5-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6f9d5-105">Das Azure-Toolkit für IntelliJ wurde im August 2017 mit einem anderen Workflow aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-105">The Azure Toolkit for IntelliJ was updated in August 2017, with a different workflow.</span></span> <span data-ttu-id="6f9d5-106">Aus diesem Grund enthält dieser Artikel zwei verschiedene Abschnitte:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-106">With that in mind, this article contains two different sections:</span></span>
>
> * <span data-ttu-id="6f9d5-107">Im ersten Abschnitt wird das Erstellen einer „Hello World“-Web-App mithilfe der Version des Azure-Toolkits für IntelliJ von August 2017 (oder später) veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-107">The first section illustrates creating a Hello World web app by using the August 2017 (or later) version of the Azure Toolkit for IntelliJ.</span></span>
>
> * <span data-ttu-id="6f9d5-108">Im zweiten Abschnitt dieses Artikels wird das Erstellen einer „Hello World“-Web-App mit der Version des Toolkits von April 2017 (oder früher) veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-108">The second section of this article demonstrates creating a Hello World web app by using the April 2017 (or earlier) version of the toolkit.</span></span>
> 

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-hello-world-web-app-by-using-the-version-307-or-later-toolkit"></a><span data-ttu-id="6f9d5-109">Erstellen einer „Hello World“-Web-App mit Version 3.0.7 oder höher des Toolkits</span><span class="sxs-lookup"><span data-stu-id="6f9d5-109">Create a Hello World web app by using the version 3.0.7 or later toolkit</span></span>

### <a name="create-a-new-web-app-project"></a><span data-ttu-id="6f9d5-110">Erstellen eines neuen Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="6f9d5-110">Create a new web app project</span></span>

1. <span data-ttu-id="6f9d5-111">Starten Sie IntelliJ, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ] an.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-111">Start IntelliJ and sign-in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="6f9d5-112">Klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-112">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Erstellen eines neuen Projekts][file-new-project]

1. <span data-ttu-id="6f9d5-114">Wählen Sie im Dialogfeld **Neues Projekt** die Option **Maven** und abschließend **maven-archetype-webapp** aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-114">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Auswählen der Maven-archetype-Web-App][maven-archetype-webapp]
   
1. <span data-ttu-id="6f9d5-116">Geben Sie die **GroupId** und **ArtifactId** für Ihre Web-App an, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-116">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Eingeben von GroupId und ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="6f9d5-118">Passen Sie alle gewünschten Maven-Einstellungen an, oder übernehmen Sie die Standardeinstellungen, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-118">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Angeben von Maven-Einstellungen][maven-options]

1. <span data-ttu-id="6f9d5-120">Geben Sie den Projektnamen und einen Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-120">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Angeben des Projektnamens][project-name]

1. <span data-ttu-id="6f9d5-122">Erweitern Sie in der Projektexplorer-Ansicht von IntelliJ **src**, dann **main**, dann **webapp**, und doppelklicken Sie dann auf **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-122">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![Öffnen der Indexseite][open-index-page]

1. <span data-ttu-id="6f9d5-124">Wenn in IntelliJ die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein,</span><span class="sxs-lookup"><span data-stu-id="6f9d5-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="6f9d5-125">damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-125">within the existing `<body>` element.</span></span> <span data-ttu-id="6f9d5-126">Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Bearbeiten der Indexseite][edit-index-page]

1. <span data-ttu-id="6f9d5-128">Speichern Sie die Datei „index.jsp“.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-128">Save index.jsp.</span></span>

### <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="6f9d5-129">Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="6f9d5-129">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="6f9d5-130">Klicken Sie in der Projekt-Explorer-Ansicht von IntelliJ mit der rechten Maustaste auf das Projekt, wählen Sie **Azure** aus, und wählen Sie dann **Run on Web App** (In Web-App ausführen) aus.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-130">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![Menü „Run on web app“ (In Web-App ausführen)][run-on-web-app-menu]

1. <span data-ttu-id="6f9d5-132">Im Dialogfeld „Run on Web App“ (In Web-App ausführen) können Sie eine der folgenden Optionen auswählen:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-132">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="6f9d5-133">Wählen Sie eine vorhandene Web-App aus (sofern vorhanden), und klicken Sie dann auf **Run** (Ausführen).</span><span class="sxs-lookup"><span data-stu-id="6f9d5-133">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![Dialogfeld „Run on Web App“ (In Web-App ausführen)][run-on-web-app-dialog]

   * <span data-ttu-id="6f9d5-135">Klicken Sie auf **Create New Web App** (Neue Web-App erstellen).</span><span class="sxs-lookup"><span data-stu-id="6f9d5-135">Click **Create New Web App**.</span></span> <span data-ttu-id="6f9d5-136">Wenn Sie eine neue Web-App erstellen, geben Sie die erforderlichen Informationen für Ihre Web-App an, und klicken Sie dann auf **Run** (Ausführen).</span><span class="sxs-lookup"><span data-stu-id="6f9d5-136">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![Create new web app (Neue Web-App erstellen)][create-new-web-app-dialog]

1. <span data-ttu-id="6f9d5-138">Im Toolkit wird eine Statusmeldung angezeigt, sobald Ihre Web-App bereitgestellt wurde. Dies schließt auch die URL Ihrer bereitgestellten Web-App ein.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-138">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![Erfolgreiche Bereitstellung][successfully-deployed]

1. <span data-ttu-id="6f9d5-140">Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-140">You can browse to your web app using the link provided in the status message.</span></span>

   ![Navigieren zur Web-App][browse-web-app]

1. <span data-ttu-id="6f9d5-142">Nachdem Sie Ihre Web-App veröffentlicht haben, werden die Einstellungen als Standard gespeichert. Sie können Ihre Anwendung in Azure ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-142">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="6f9d5-143">Sie können die Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-143">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. <span data-ttu-id="6f9d5-145">Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-145">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

<hr />

## <a name="create-a-hello-world-web-app-by-using-the-version-306-or-earlier-toolkit"></a><span data-ttu-id="6f9d5-147">Erstellen einer „Hello World“-Web-App mit Version 3.0.6 oder niedriger des Toolkits</span><span class="sxs-lookup"><span data-stu-id="6f9d5-147">Create a Hello World web app by using the version 3.0.6 or earlier toolkit</span></span>

### <a name="create-a-new-web-app-project"></a><span data-ttu-id="6f9d5-148">Erstellen eines neuen Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="6f9d5-148">Create a new web app project</span></span>

1. <span data-ttu-id="6f9d5-149">Starten Sie IntelliJ, klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-149">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Datei Neu Projekt][02]

2. <span data-ttu-id="6f9d5-151">Wählen Sie im Dialogfeld **Neues Projekt** die Option **Java** und dann **Webanwendung** aus, und klicken Sie dann auf **Neu**, um ein Projekt-SDK hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-151">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![Dialogfeld "Neues Projekt"][03a]
   
3. <span data-ttu-id="6f9d5-153">Wählen Sie im Dialogfeld für die Auswahl des Stammverzeichnisses für JDK den Ordner aus, in dem Ihr JDK installiert ist, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-153">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="6f9d5-154">Klicken Sie im Dialogfeld „Neues Projekt“ auf **Weiter**, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-154">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![Festlegen des JDK-Stammverzeichnisses][03b]

4. <span data-ttu-id="6f9d5-156">Für die Zwecke dieses Tutorials benennen Sie das Projekt mit **Java-Web-App-On-Azure**, und klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-156">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![Dialogfeld "Neues Projekt"][04]

5. <span data-ttu-id="6f9d5-158">Erweitern Sie in der Projektexplorer-Ansicht von IntelliJ **Java-Web-App-On-Azure**, erweitern Sie anschließend **web**, und doppelklicken Sie dann auf **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-158">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![Öffnen der Indexseite][05c]

6. <span data-ttu-id="6f9d5-160">Wenn in IntelliJ die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein,</span><span class="sxs-lookup"><span data-stu-id="6f9d5-160">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="6f9d5-161">damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-161">within the existing `<body>` element.</span></span> <span data-ttu-id="6f9d5-162">Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-162">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="6f9d5-163">Speichern Sie die Datei „index.jsp“.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-163">Save index.jsp.</span></span>

### <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="6f9d5-164">Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="6f9d5-164">Deploy your web app to Azure</span></span>
<span data-ttu-id="6f9d5-165">Es gibt mehrere Möglichkeiten, eine Java-Web-App in Azure bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-165">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="6f9d5-166">In diesem Tutorial wird eine der einfachsten beschrieben: Ihre Anwendung wird in einem Azure-Web-App-Container bereitgestellt – weder ein spezieller Projekttyp noch zusätzliche Tools sind erforderlich.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-166">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="6f9d5-167">Das JDK und die Webcontainersoftware werden von Azure für Sie bereitgestellt, sodass Sie weder ein eigenes JDK noch eigene Webcontainersoftware hochladen müssen; Sie benötigen lediglich Ihre Java Web-App.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-167">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="6f9d5-168">Darum dauert der Veröffentlichungsprozess für Ihre Anwendung nur Sekunden, nicht Minuten.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-168">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="6f9d5-169">Vor der Veröffentlichung Ihrer Anwendung müssen Sie zuerst die Moduleinstellungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-169">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="6f9d5-170">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-170">To do so, use the following steps:</span></span>

1. <span data-ttu-id="6f9d5-171">Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf das Projekt **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="6f9d5-171">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="6f9d5-172">Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Moduleinstellungen öffnen**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-172">When the context menu appears, click **Open Module Settings**.</span></span>

   ![Öffnen der Moduleinstellungen][05a]

2. <span data-ttu-id="6f9d5-174">Wenn das Dialogfeld „Projektstruktur“ angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-174">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="6f9d5-175">a.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-175">a.</span></span> <span data-ttu-id="6f9d5-176">Klicken Sie in der Liste der **Projekteinstellungen** auf **Artefakte**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-176">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="6f9d5-177">b.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-177">b.</span></span> <span data-ttu-id="6f9d5-178">Ändern Sie den Artefaktnamen im Feld **Name** so, dass er keine Leerzeichen oder Sonderzeichen enthält; dies ist erforderlich, da der Name im Uniform Resource Identifier (URI) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-178">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="6f9d5-179">c.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-179">c.</span></span> <span data-ttu-id="6f9d5-180">Ändern Sie den **Typ** in **Webanwendung: Archiv**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-180">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="6f9d5-181">d.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-181">d.</span></span> <span data-ttu-id="6f9d5-182">Klicken Sie auf **OK**, um das Dialogfeld mit der Projektstruktur zu schließen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-182">Click **OK** to close the Project Structure dialog box.</span></span>

   ![Öffnen der Moduleinstellungen][05b]

<span data-ttu-id="6f9d5-184">Nachdem Sie die Moduleinstellungen konfiguriert haben, können Sie Ihre Anwendung mithilfe der folgenden Schritte in Azure veröffentlichen:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-184">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="6f9d5-185">Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf das Projekt **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="6f9d5-185">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="6f9d5-186">Wählen Sie im Kontextmenü **Azure** aus, und klicken Sie dann auf **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen).</span><span class="sxs-lookup"><span data-stu-id="6f9d5-186">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Kontextmenü zur Azure-Veröffentlichung][06]

2. <span data-ttu-id="6f9d5-188">Wenn Sie sich noch nicht über IntelliJ bei Azure angemeldet haben, werden Sie aufgefordert, sich bei Ihrem Azure-Konto anzumelden.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-188">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="6f9d5-189">(Wenn Sie über mehrere Azure-Konten verfügen, können einige der Eingabeaufforderungen während des Anmeldeprozesses mehrmals angezeigt werden, auch wenn sie scheinbar identisch sind.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-189">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="6f9d5-190">Befolgen Sie in diesem Fall weiterhin die Anweisungen zur Anmeldung.)</span><span class="sxs-lookup"><span data-stu-id="6f9d5-190">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Anmeldedialogfeld von Azure][07]

3. <span data-ttu-id="6f9d5-192">Nachdem Sie sich erfolgreich bei Ihrem Azure-Konto angemeldet haben, wird im Dialogfeld **Manage Subscriptions** (Abonnements verwalten) eine Liste der Abonnements angezeigt, die mit Ihren Anmeldeinformationen verknüpft sind.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-192">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="6f9d5-193">(Wenn mehrere Abonnements aufgeführt sind und Sie nur mit einer bestimmten Teilmenge davon arbeiten möchten, können Sie optional die Abonnements deaktivieren, die Sie nicht verwenden möchten.) Wenn Sie Ihre Abonnements ausgewählt haben, klicken Sie auf **Schließen**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-193">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Verwalten von Abonnements][08]

4. <span data-ttu-id="6f9d5-195">Wenn das Dialogfeld **Deploy to Azure Web App Container** (In Azure-Web-App-Container bereitstellen) angezeigt wird, werden alle Web-App-Container angezeigt, die Sie zuvor erstellt haben. Wenn Sie keine Container erstellt haben, ist die Liste leer.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-195">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![App-Container][09]

5. <span data-ttu-id="6f9d5-197">Wenn Sie zuvor keinen Azure-Web-App-Container erstellt haben, oder Sie Ihre Anwendung in einem neuen Container veröffentlichen möchten, führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-197">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="6f9d5-198">Wählen Sie andernfalls einen vorhandenen Web-App-Container aus, und fahren Sie mit Schritt 6 fort.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-198">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="6f9d5-199">a.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-199">a.</span></span> <span data-ttu-id="6f9d5-200">Klicken Sie auf das Symbol **+**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-200">Click the **+** sign.</span></span>
      
      ![App-Container hinzufügen][10]

   <span data-ttu-id="6f9d5-202">b.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-202">b.</span></span> <span data-ttu-id="6f9d5-203">Das Dialogfeld **New Web App Container** (Neuer Web-App-Container) wird angezeigt, in dem Sie die nächsten Schritte ausführen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-203">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![Neuer App-Container][11a]
   
   <span data-ttu-id="6f9d5-205">c.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-205">c.</span></span> <span data-ttu-id="6f9d5-206">Geben Sie eine **DNS-Bezeichnung** für Ihren Web-App-Container ein; dies ist die Blatt-DNS-Bezeichnung der Host-URL für Ihre Webanwendung in Azure.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-206">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="6f9d5-207">Hinweis: Der Name muss verfügbar sein und den Azure-Web-App-Namenskonventionen entsprechen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-207">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="6f9d5-208">d.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-208">d.</span></span> <span data-ttu-id="6f9d5-209">Wählen Sie im Dropdownmenü **Web Container** (Webcontainer) die passende Software für Ihre Anwendung aus.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-209">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="6f9d5-210">Aktuell können Sie zwischen Tomcat 8, Tomcat 7 und Jetty 9 wählen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-210">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="6f9d5-211">Azure stellt eine aktuelle Distribution der gewählten Software bereit und diese wird auf einer aktuellen Distribution von JDK 8 ausgeführt, die von Oracle erstellt und von Azure bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-211">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="6f9d5-212">e.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-212">e.</span></span> <span data-ttu-id="6f9d5-213">Wählen Sie im Dropdownmenü **Subscription** (Abonnement) das Abonnement aus, das Sie für diese Bereitstellung verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-213">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="6f9d5-214">f.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-214">f.</span></span> <span data-ttu-id="6f9d5-215">Wählen Sie im Dropdownmenü **Resource Group** (Ressourcengruppe) die Ressourcengruppe aus, der Sie Ihre Web-App zuordnen möchten.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-215">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="6f9d5-216">(Mithilfe von Azure-Ressourcengruppen können Sie verwandte Ressourcen gruppieren, um diese z.B. gemeinsam löschen zu können.)</span><span class="sxs-lookup"><span data-stu-id="6f9d5-216">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="6f9d5-217">(Sie können eine vorhandene Ressourcengruppe auswählen (sofern vorhanden) und direkt mit Schritt g unten fortfahren oder die Schritte zum Erstellen einer neuen Ressourcengruppe ausführen:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-217">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="6f9d5-218">Wählen Sie im Dropdownmenü **Ressourcengruppe** die Option **&lt;&lt;Neue Ressourcengruppe erstellen&gt;&gt;**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-218">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="6f9d5-219">Das Dialogfeld **New Resource Group** (Neue Ressourcengruppe) wird angezeigt:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-219">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![Neue Ressourcengruppe][12]

      * <span data-ttu-id="6f9d5-221">Geben Sie im Textfeld **Name** einen Namen für die neue Ressourcengruppe ein.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-221">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="6f9d5-222">Wählen Sie im Dropdownmenü **Region** den entsprechenden Azure-Rechenzentrumsstandort für Ihre Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-222">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="6f9d5-223">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-223">Click **OK**.</span></span>

   <span data-ttu-id="6f9d5-224">g.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-224">g.</span></span> <span data-ttu-id="6f9d5-225">Im Dropdownmenü **App Service Plan** (App Service-Plan) werden die App Service-Pläne aufgelistet, die der ausgewählten Ressourcengruppe zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-225">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="6f9d5-226">Ein App Service-Plan enthält verschiedene Informationen wie z.B. den Speicherort Ihrer Web-App, den Tarif und die Größe der Compute-Instanz.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-226">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="6f9d5-227">Da ein App Service-Plan für mehrere Web-Apps verwendet werden kann, wird er getrennt von einer bestimmten Web-App-Bereitstellung verwaltet.)</span><span class="sxs-lookup"><span data-stu-id="6f9d5-227">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="6f9d5-228">Sie können einen vorhandenen App Service-Plan auswählen (sofern vorhanden) und direkt mit Schritt h unten fortfahren oder die folgenden Schritte ausführen, um einen neuen App Service-Plan zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-228">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="6f9d5-229">Wählen Sie in der Dropdownliste **App Service-Plan** die Option **&lt;&lt;Neuen App Service-Plan erstellen&gt;&gt;**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-229">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="6f9d5-230">Das Dialogfeld **New App Service Plan** (Neuer App Service-Plan) wird angezeigt:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-230">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![Neuer App Service-Plan][13]

      * <span data-ttu-id="6f9d5-232">Geben Sie im Textfeld **Name** einen Namen für den neuen App Service-Plan ein.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-232">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="6f9d5-233">Wählen Sie im Dropdownmenü **Location** (Standort) den entsprechenden Azure-Rechenzentrumsstandort für den Plan aus.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-233">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="6f9d5-234">Wählen Sie im Dropdownmenü **Pricing Tier** (Tarif) die entsprechenden Preise für den Plan aus.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-234">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="6f9d5-235">Zu Testzwecken können Sie **Free**(Kostenlos) auswählen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-235">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="6f9d5-236">Wählen Sie im Dropdownmenü **Instance Size** (Instanzgröße) die entsprechende Instanzgröße für den Plan aus.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-236">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="6f9d5-237">Zu Testzwecken können Sie **Small**(Klein) wählen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-237">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="6f9d5-238">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-238">Click **OK**.</span></span>

   <span data-ttu-id="6f9d5-239">h.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-239">h.</span></span> <span data-ttu-id="6f9d5-240">(Optional) Azure stellt standardmäßig automatisch eine aktuelle Distribution von Java 8 in Ihrem Web-App-Container als JVM bereit.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-240">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="6f9d5-241">Sie können jedoch eine andere JVM-Version und -Distribution auswählen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-241">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="6f9d5-242">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-242">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="6f9d5-243">Klicken Sie im Dialogfeld **New Web App Container** (Neuer Web-App-Container) auf die Registerkarte **JDK**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-243">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="6f9d5-244">Folgende Optionen stehen zur Auswahl:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-244">You can choose from one of the following options:</span></span>
        
         * <span data-ttu-id="6f9d5-245">Bereitstellen des Standard-JDKs von Azure</span><span class="sxs-lookup"><span data-stu-id="6f9d5-245">Deploy the default JDK which is offered by Azure</span></span>
         * <span data-ttu-id="6f9d5-246">Bereitstellen eines Drittanbieter-JDKs aus einer Dropdownliste mit zusätzlichen JDKs, die in Azure verfügbar sind</span><span class="sxs-lookup"><span data-stu-id="6f9d5-246">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
         * <span data-ttu-id="6f9d5-247">Bereitstellen eines benutzerdefinierten JDKs, das als ZIP-Datei verpackt und entweder öffentlich verfügbar sein oder sich in Ihrem Azure-Speicherkonto befinden muss</span><span class="sxs-lookup"><span data-stu-id="6f9d5-247">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
      ![New App Container (Neuer App-Container) Registerkarte „JDK“][11b]

   <span data-ttu-id="6f9d5-249">i.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-249">i.</span></span> <span data-ttu-id="6f9d5-250">Wenn Sie alle oben genannten Schritte abgeschlossen haben, sollte das Dialogfeld „New Web App Container“ (Neuer Web-App-Container) folgender Abbildung ähneln:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-250">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Neuer App-Container][14]
   
   <span data-ttu-id="6f9d5-252">j.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-252">j.</span></span> <span data-ttu-id="6f9d5-253">Klicken Sie auf **OK** , um die Erstellung Ihres neuen Web-App-Containers abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-253">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="6f9d5-254">Warten Sie einige Sekunden, bis die Liste der Web-App-Container aktualisiert wurde. Ihr neu erstellter Web-App-Container sollte nun in der Liste angezeigt werden und markiert sein.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-254">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="6f9d5-255">Sie sind nun bereit für die erste Bereitstellung der Web-App in Azure. Klicken Sie auf **OK**, um Ihre Java-Anwendung im ausgewählten Web-App-Container bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-255">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="6f9d5-256">Standardmäßig wird die Anwendung als Unterverzeichnis des Anwendungsservers bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-256">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="6f9d5-257">Wenn sie als Stammanwendung bereitgestellt werden soll, aktivieren Sie das Kontrollkästchen **Deploy to root** (In Stamm bereitstellen), bevor Sie auf **OK** klicken.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-257">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![In Azure bereitstellen][15]

7. <span data-ttu-id="6f9d5-259">Als Nächstes sollte das **Azure-Aktivitätsprotokoll** mit dem Bereitstellungsstatus der Web-App angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-259">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Statusanzeige][16]
   
   <span data-ttu-id="6f9d5-261">Die Bereitstellung Ihrer Web-App in Azure sollte nur einige Sekunden dauern.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-261">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="6f9d5-262">Wenn Ihre Anwendung bereit ist, wird in der Spalte **Status** der Link **Veröffentlicht** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-262">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="6f9d5-263">Wenn Sie auf den Link klicken, gelangen Sie zur Startseite der bereitgestellten Web-App. Sie können auch anhand der Schritte im folgenden Abschnitt zu Ihrer Web-App navigieren.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-263">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

### <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="6f9d5-264">Navigieren zur Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="6f9d5-264">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="6f9d5-265">Um in Azure zu Ihrer Web-App zu navigieren, können Sie die Ansicht **Azure Explorer** verwenden.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-265">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="6f9d5-266">Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in IntelliJ auf das Menü **Ansicht**, auf **Toolfenster** und dann auf **Service Explorer** klicken.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-266">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="6f9d5-267">Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-267">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="6f9d5-268">Wenn die Ansicht **Azure Explorer** angezeigt wird, führen Sie folgende Schritte aus, um zu Ihrer Web-App zu navigieren:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-268">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="6f9d5-269">Erweitern Sie den Knoten **Azure** .</span><span class="sxs-lookup"><span data-stu-id="6f9d5-269">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="6f9d5-270">Erweitern Sie den Knoten **Web Apps** (Web-Apps).</span><span class="sxs-lookup"><span data-stu-id="6f9d5-270">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="6f9d5-271">Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-271">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="6f9d5-272">Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Im Browser öffnen**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-272">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![Durchsuchen von Web-App][17]

### <a name="updating-your-web-app"></a><span data-ttu-id="6f9d5-274">Aktualisieren Ihrer Web-App</span><span class="sxs-lookup"><span data-stu-id="6f9d5-274">Updating your web app</span></span>
<span data-ttu-id="6f9d5-275">Das Aktualisieren einer vorhandenen, ausgeführten Azure-Web-App ist ein schneller und einfacher Prozess, und Ihnen stehen zwei Optionen für die Aktualisierung zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-275">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="6f9d5-276">Sie können die Bereitstellung einer vorhandenen Java-Web-App aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-276">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="6f9d5-277">Sie können eine weitere Java-Anwendung in dem gleichen Web-App-Container veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-277">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="6f9d5-278">In beiden Fällen ist der Prozess identisch und dauert nur wenige Sekunden:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-278">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="6f9d5-279">Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf die Java-Anwendung, die Sie aktualisieren oder einem vorhandenen Web-App-Container hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-279">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="6f9d5-280">Wählen Sie im Kontextmenü **Azure** und dann **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen) aus.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-280">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="6f9d5-281">Da Sie sich bereits zuvor angemeldet haben, sehen Sie eine Liste Ihrer vorhandenen Web-App-Container.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-281">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="6f9d5-282">Wählen Sie den Container aus, in dem Sie Ihre Java-Anwendung veröffentlichen oder erneut veröffentlichen möchten, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-282">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="6f9d5-283">Wenige Sekunden später wird Ihre aktualisierte Bereitstellung in der Ansicht **Azure Activity Log** (Azure-Aktivitätsprotokoll) als **Published** (Veröffentlicht) angezeigt, und Sie können die aktualisierte Anwendung in einem Webbrowser überprüfen.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-283">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

### <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="6f9d5-284">Starten, Beenden oder Neustarten einer vorhandenen Web-App</span><span class="sxs-lookup"><span data-stu-id="6f9d5-284">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="6f9d5-285">Um einen vorhandenen Azure-Web-App-Container zu starten oder zu beenden (einschließlich aller darin bereitgestellten Java-Anwendungen), können Sie die Ansicht **Azure Explorer** verwenden.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-285">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="6f9d5-286">Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in IntelliJ auf das Menü **Ansicht**, auf **Toolfenster** und dann auf **Service Explorer** klicken.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-286">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="6f9d5-287">Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-287">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="6f9d5-288">Wenn die Ansicht **Azure Explorer** angezeigt wird, starten oder beenden Sie Ihre Web-App mit folgenden Schritten:</span><span class="sxs-lookup"><span data-stu-id="6f9d5-288">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="6f9d5-289">Erweitern Sie den Knoten **Azure** .</span><span class="sxs-lookup"><span data-stu-id="6f9d5-289">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="6f9d5-290">Erweitern Sie den Knoten **Web Apps** (Web-Apps).</span><span class="sxs-lookup"><span data-stu-id="6f9d5-290">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="6f9d5-291">Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-291">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="6f9d5-292">Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Starten**, **Beenden** oder **Neu starten**.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-292">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="6f9d5-293">Beachten Sie, dass die Menüoptionen kontextabhängig sind. Sie können nur eine ausgeführte Web-App beenden oder eine Web-App starten, die zurzeit nicht ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="6f9d5-293">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Beenden von Web-App][18]

## <a name="next-steps"></a><span data-ttu-id="6f9d5-295">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6f9d5-295">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="6f9d5-296">Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].</span><span class="sxs-lookup"><span data-stu-id="6f9d5-296">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure-Toolkits für IntelliJ]: azure-toolkit-for-intellij.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/18-Stop-Web-App.png

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
