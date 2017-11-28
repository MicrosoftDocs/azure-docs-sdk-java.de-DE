---
title: "Erstellen einer „Hello World“-Web-App für Azure mit IntelliJ"
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
ms.date: 11/15/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 900e64667bcc2eed79fe80954c118d54a9ef957f
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a><span data-ttu-id="4467a-103">Erstellen einer „Hello World“-Web-App für Azure mit IntelliJ</span><span class="sxs-lookup"><span data-stu-id="4467a-103">Create a Hello World web app for Azure using IntelliJ</span></span>

<span data-ttu-id="4467a-104">Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe des [Azure-Toolkits für IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="4467a-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="4467a-105">Eine Version dieses Artikels, in dem das [Azure-Toolkit für Eclipse] verwendet wird, finden Sie unter [Erstellen einer einfachen Azure-Web-App mit Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="4467a-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="4467a-106">Das Azure-Toolkit für IntelliJ wurde im August 2017 mit einem anderen Workflow aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="4467a-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="4467a-107">In diesem Artikel wird das Erstellen einer „Hello World“-Web-App mithilfe der Version 3.0.7 (oder höher) des Azure-Toolkits für IntelliJ veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="4467a-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="4467a-108">Wenn Sie die Version 3.0.6 (oder eine ältere Version) des Toolkits verwenden, müssen Sie die Schritte unter [Create a Hello World web app for Azure using the legacy toolkit for IntelliJ][Legacy Version] (Erstellen einer „Hello World“-Web-App für Azure mit dem Legacytoolkit für IntelliJ) ausführen.</span><span class="sxs-lookup"><span data-stu-id="4467a-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="4467a-109">Wenn Sie dieses Tutorial abgeschlossen haben, entspricht Ihre Anwendung bei der Anzeige in einem Webbrowser etwa der folgenden Abbildung:</span><span class="sxs-lookup"><span data-stu-id="4467a-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Vorschau der Hello World-App][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="4467a-111">Erstellen eines neuen Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="4467a-111">Create a new web app project</span></span>

1. <span data-ttu-id="4467a-112">Starten Sie IntelliJ, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ][intelliJ-sign-in-instructions] an.</span><span class="sxs-lookup"><span data-stu-id="4467a-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="4467a-113">Klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="4467a-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Erstellen eines neuen Projekts][file-new-project]

1. <span data-ttu-id="4467a-115">Wählen Sie im Dialogfeld **Neues Projekt** die Option **Maven** und abschließend **maven-archetype-webapp** aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="4467a-115">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Auswählen der Maven-archetype-Web-App][maven-archetype-webapp]
   
1. <span data-ttu-id="4467a-117">Geben Sie die **GroupId** und **ArtifactId** für Ihre Web-App an, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="4467a-117">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Eingeben von GroupId und ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="4467a-119">Passen Sie alle gewünschten Maven-Einstellungen an, oder übernehmen Sie die Standardeinstellungen, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="4467a-119">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Angeben von Maven-Einstellungen][maven-options]

1. <span data-ttu-id="4467a-121">Geben Sie den Projektnamen und einen Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="4467a-121">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Angeben des Projektnamens][project-name]

1. <span data-ttu-id="4467a-123">Erweitern Sie in der Projektexplorer-Ansicht von IntelliJ **src**, dann **main**, dann **webapp**, und doppelklicken Sie dann auf **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="4467a-123">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![Öffnen der Indexseite][open-index-page]

1. <span data-ttu-id="4467a-125">Wenn in IntelliJ die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein,</span><span class="sxs-lookup"><span data-stu-id="4467a-125">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="4467a-126">damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="4467a-126">within the existing `<body>` element.</span></span> <span data-ttu-id="4467a-127">Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="4467a-127">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Bearbeiten der Indexseite][edit-index-page]

1. <span data-ttu-id="4467a-129">Speichern Sie die Datei „index.jsp“.</span><span class="sxs-lookup"><span data-stu-id="4467a-129">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="4467a-130">Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="4467a-130">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="4467a-131">Klicken Sie in der Projekt-Explorer-Ansicht von IntelliJ mit der rechten Maustaste auf das Projekt, wählen Sie **Azure** aus, und wählen Sie dann **Run on Web App** (In Web-App ausführen) aus.</span><span class="sxs-lookup"><span data-stu-id="4467a-131">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![Menü „Run on web app“ (In Web-App ausführen)][run-on-web-app-menu]

1. <span data-ttu-id="4467a-133">Im Dialogfeld „Run on Web App“ (In Web-App ausführen) können Sie eine der folgenden Optionen auswählen:</span><span class="sxs-lookup"><span data-stu-id="4467a-133">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="4467a-134">Wählen Sie eine vorhandene Web-App aus (sofern vorhanden), und klicken Sie dann auf **Run** (Ausführen).</span><span class="sxs-lookup"><span data-stu-id="4467a-134">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![Dialogfeld „Run on Web App“ (In Web-App ausführen)][run-on-web-app-dialog]

   * <span data-ttu-id="4467a-136">Klicken Sie auf **Create New Web App** (Neue Web-App erstellen).</span><span class="sxs-lookup"><span data-stu-id="4467a-136">Click **Create New Web App**.</span></span> <span data-ttu-id="4467a-137">Wenn Sie eine neue Web-App erstellen, geben Sie die erforderlichen Informationen für Ihre Web-App an, und klicken Sie dann auf **Run** (Ausführen).</span><span class="sxs-lookup"><span data-stu-id="4467a-137">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![Create new web app (Neue Web-App erstellen)][create-new-web-app-dialog]

1. <span data-ttu-id="4467a-139">Im Toolkit wird eine Statusmeldung angezeigt, sobald Ihre Web-App bereitgestellt wurde. Dies schließt auch die URL Ihrer bereitgestellten Web-App ein.</span><span class="sxs-lookup"><span data-stu-id="4467a-139">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![Erfolgreiche Bereitstellung][successfully-deployed]

1. <span data-ttu-id="4467a-141">Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.</span><span class="sxs-lookup"><span data-stu-id="4467a-141">You can browse to your web app using the link provided in the status message.</span></span>

   ![Navigieren zur Web-App][browse-web-app]

1. <span data-ttu-id="4467a-143">Nachdem Sie Ihre Web-App veröffentlicht haben, werden die Einstellungen als Standard gespeichert. Sie können Ihre Anwendung in Azure ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken.</span><span class="sxs-lookup"><span data-stu-id="4467a-143">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="4467a-144">Sie können die Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.</span><span class="sxs-lookup"><span data-stu-id="4467a-144">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. <span data-ttu-id="4467a-146">Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="4467a-146">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="4467a-148">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="4467a-148">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="4467a-149">Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].</span><span class="sxs-lookup"><span data-stu-id="4467a-149">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure-Toolkits für IntelliJ]: azure-toolkit-for-intellij.md
[Azure-Toolkit für Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

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
