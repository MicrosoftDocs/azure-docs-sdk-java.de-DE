---
title: "Erstellen einer „Hello World“-Web-App für Azure mit Eclipse"
description: "In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für Eclipse eine „Hello World“-Web-App für Azure erstellen."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/15/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 7b82be727798a1edb58d99fe0d6b43e498e22a92
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a><span data-ttu-id="2d9d6-103">Erstellen einer „Hello World“-Web-App für Azure mit Eclipse</span><span class="sxs-lookup"><span data-stu-id="2d9d6-103">Create a Hello World web app for Azure using Eclipse</span></span>

<span data-ttu-id="2d9d6-104">Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe des [Azure-Toolkits für Eclipse].</span><span class="sxs-lookup"><span data-stu-id="2d9d6-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="2d9d6-105">Eine Version dieses Artikels, in dem das [Azure-Toolkit für IntelliJ] verwendet wird, finden Sie unter [Erstellen einer einfachen Azure-Web-App in IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="2d9d6-105">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="2d9d6-106">Das Azure-Toolkit für Eclipse wurde im August 2017 mit einem anderen Workflow aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-106">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="2d9d6-107">In diesem Artikel wird das Erstellen einer „Hello World“-Web-App mithilfe der Version 3.0.7 (oder höher) des Azure-Toolkits für Eclipse veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="2d9d6-108">Wenn Sie die Version 3.0.6 (oder eine ältere Version) des Toolkits verwenden, müssen Sie die Schritte unter [Create a Hello World web app for Azure using the legacy toolkit for Eclipse][Legacy Version] (Erstellen einer „Hello World“-Web-App für Azure mit dem Legacytoolkit für Eclipse) ausführen.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="2d9d6-109">Wenn Sie dieses Tutorial abgeschlossen haben, entspricht Ihre Anwendung bei der Anzeige in einem Webbrowser etwa der folgenden Abbildung:</span><span class="sxs-lookup"><span data-stu-id="2d9d6-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Vorschau der Hello World-App][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="2d9d6-111">Erstellen eines neuen Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="2d9d6-111">Create a new web app project</span></span>

1. <span data-ttu-id="2d9d6-112">Starten Sie Eclipse, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse][eclipse-sign-in-instructions] an.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-112">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="2d9d6-113">Klicken Sie auf **Datei**, dann auf **Neu** und schließlich auf **Dynamisches Webprojekt**.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-113">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="2d9d6-114">(Wenn **Dynamic Web Project** (Dynamisches Webprojekt) nach dem Klicken auf **File** (Datei) und **New** (Neu) nicht als verfügbares Projekt aufgeführt ist, gehen Sie wie folgt vor: Klicken Sie auf **File** (Datei), anschließend auf **New** (Neu) und dann auf **Project...** (Projekt...). Erweitern Sie die Option **Web**, klicken Sie auf **Dynamic Web Project** (Dynamisches Webprojekt) und dann auf **Next** (Weiter).)</span><span class="sxs-lookup"><span data-stu-id="2d9d6-114">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Erstellen eines neuen dynamischen Webprojekts][file-new-dynamic-web-project]

2. <span data-ttu-id="2d9d6-116">Nennen Sie das Projekt für die Zwecke dieses Tutorials **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-116">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="2d9d6-117">Ihr Bildschirm sieht dann in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="2d9d6-117">Your screen will appear similar to the following:</span></span>
   
   ![Eigenschaften des neuen dynamischen Webprojekts][dynamic-web-project-properties]

3. <span data-ttu-id="2d9d6-119">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-119">Click **Finish**.</span></span>

4. <span data-ttu-id="2d9d6-120">Erweitern Sie in der Project Explorer-Ansicht von Eclipse die Option **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-120">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="2d9d6-121">Klicken Sie mit der rechten Maustaste auf **WebContent**, und klicken Sie dann auf **Neu** sowie auf **JSP-Datei**.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-121">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Erstellen einer neuen JSP-Datei][create-new-jsp-file]

5. <span data-ttu-id="2d9d6-123">Geben Sie im Dialogfeld **New JSP File** (Neue JSP-Datei) den Namen **index.jsp** für die Datei ein. Behalten Sie den übergeordneten Ordner als **MyWebApp/WebContent** bei, und klicken Sie auf **Next** (Weiter).</span><span class="sxs-lookup"><span data-stu-id="2d9d6-123">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Dialogfeld „New JSP File“ (Neue JSP-Datei)][new-jsp-file-dialog]

6. <span data-ttu-id="2d9d6-125">Wählen Sie im Dialogfeld **Select JSP Template** (JSP-Vorlage auswählen) im Rahmen dieses Tutorials **New JSP File (html)** (Neue JSP-Datei (HTML)) aus, und klicken Sie dann auf **Finish** (Fertig stellen).</span><span class="sxs-lookup"><span data-stu-id="2d9d6-125">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Auswählen einer JSP-Vorlage][select-jsp-template]

7. <span data-ttu-id="2d9d6-127">Wenn in Eclipse die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein,</span><span class="sxs-lookup"><span data-stu-id="2d9d6-127">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="2d9d6-128">damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-128">within the existing `<body>` element.</span></span> <span data-ttu-id="2d9d6-129">Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="2d9d6-129">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="2d9d6-130">Speichern Sie die Datei „index.jsp“.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-130">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="2d9d6-131">Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="2d9d6-131">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="2d9d6-132">Klicken Sie in der Projekt-Explorer-Ansicht von Eclipse mit der rechten Maustaste auf das Projekt, wählen Sie **Azure** aus, und wählen Sie dann **Publish as Azure Web App** (Als Azure-Web-App veröffentlichen) aus.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-132">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Veröffentlichen als Azure-Web-App][publish-as-azure-web-app]

1. <span data-ttu-id="2d9d6-134">Im Dialogfeld **Web-App bereitstellen** können Sie eine der folgenden Optionen auswählen:</span><span class="sxs-lookup"><span data-stu-id="2d9d6-134">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="2d9d6-135">Wählen Sie eine vorhandene Web-App aus, sofern vorhanden.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-135">Select an existing web app if one exists.</span></span>

      ![Auswählen eines App-Diensts][select-app-service]

   * <span data-ttu-id="2d9d6-137">Klicken Sie auf **Create New Web App** (Neue Web-App erstellen).</span><span class="sxs-lookup"><span data-stu-id="2d9d6-137">Click **Create New Web App**.</span></span>

      ![Erstellen eines App Service][create-app-service]

      <span data-ttu-id="2d9d6-139">Geben Sie die erforderlichen Informationen für Ihre Web-App im Dialogfeld **App Service erstellen** an, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-139">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      ![Dialogfeld „App Service erstellen“][create-app-service-dialog]

1. <span data-ttu-id="2d9d6-141">Wählen Sie Ihre Web-App aus, und klicken Sie dann auf **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-141">Select your web app and then click **Deploy**.</span></span>

   ![Bereitstellen eines App-Diensts][deploy-app-service]

1. <span data-ttu-id="2d9d6-143">Im Toolkit wird ein **Azure-Aktivitätsprotokoll** mit dem Status **Veröffentlicht** angezeigt, wenn die Web-App bereitgestellt wurde. Der Status ist als Link für die URL der bereitgestellten Web-App formatiert.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-143">The toolkit will display a **Published** status **Azure Activity Log** when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![Veröffentlichungsstatus][publish-status]

1. <span data-ttu-id="2d9d6-145">Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-145">You can browse to your web app using the link provided in the status message.</span></span>

   ![Navigieren zur Web-App][browse-web-app]

1. <span data-ttu-id="2d9d6-147">Nachdem Sie Ihre Web-App in Azure veröffentlicht haben, können Sie die App verwalten, indem Sie mit der rechten Maustaste darauf klicken und eine der Optionen im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-147">After you have published your web to Azure, you can manage your app by right-clicking on it and selecting one of the options on the context menu.</span></span> <span data-ttu-id="2d9d6-148">Sie können für die Web-App beispielsweise die Option zum **Starten**, **Beenden** oder **Löschen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="2d9d6-148">For example, you can **Start**, **Stop**, or **Delete** your web app.</span></span>

   ![Verwalten des App-Diensts][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="2d9d6-150">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="2d9d6-150">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="2d9d6-151">Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].</span><span class="sxs-lookup"><span data-stu-id="2d9d6-151">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure-Toolkits für Eclipse]: azure-toolkit-for-eclipse.md
[Azure-Toolkit für IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
