---
title: Erstellen einer „Hello World“-Web-App für Azure App Service mit Eclipse
description: In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für Eclipse eine „Hello World“-Web-App für Azure erstellen.
services: app-service
keywords: Java, Eclipse, Web-App, Azure App Service, Hallo Welt, Hello World, Schnellstart
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 7e88298afaf0b4601d85d6063b7096c79e677421
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625865"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-eclipse"></a><span data-ttu-id="97d25-104">Erstellen einer „Hello World“-Web-App für Azure App Service mit Eclipse</span><span class="sxs-lookup"><span data-stu-id="97d25-104">Create a Hello World web app for Azure App Service using Eclipse</span></span>

<span data-ttu-id="97d25-105">Mithilfe des Open-Source-Plug-Ins [Azure-Toolkit für Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) können Sie innerhalb weniger Minuten eine einfache „Hello World“-Anwendung erstellen und als Web-App in Azure App Service bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="97d25-105">Using open sourced [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="97d25-106">Ein ähnliches Tutorial für IntelliJ IDEA finden Sie [hier][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="97d25-106">If you prefer using IntelliJ IDEA, check out our [similar tutorial for IntelliJ][intellij-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="97d25-107">Denken Sie daran, die Ressourcen nach Abschluss dieses Tutorials zu bereinigen.</span><span class="sxs-lookup"><span data-stu-id="97d25-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="97d25-108">In diesem Fall wird Ihr kostenloses Kontokontingent im Rahmen dieses Leitfadens nicht überschritten.</span><span class="sxs-lookup"><span data-stu-id="97d25-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="97d25-109">Installation und Anmeldung</span><span class="sxs-lookup"><span data-stu-id="97d25-109">Installation and sign-in</span></span>

1. <span data-ttu-id="97d25-110">Ziehen Sie die folgende Schaltfläche in Ihren aktiven Eclipse-Arbeitsbereich, um das Plug-In „Azure-Toolkit für Eclipse“ zu installieren. Weitere Installationsoptionen finden Sie [hier](azure-toolkit-for-eclipse-installation.md).</span><span class="sxs-lookup"><span data-stu-id="97d25-110">Drag the following button to your running Eclipse workspace to install the Azure Toolkit for Eclipse plugin ([other installation options](azure-toolkit-for-eclipse-installation.md)).</span></span>

    <span data-ttu-id="97d25-111">[![Ziehen Sie dieses Element in Ihren aktiven Eclipse*-Arbeitsbereich. *Eclipse Marketplace-Client erforderlich.](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Ziehen Sie dieses Element in Ihren aktiven Eclipse*-Arbeitsbereich. *Eclipse Marketplace-Client erforderlich.")</span><span class="sxs-lookup"><span data-stu-id="97d25-111">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

1. <span data-ttu-id="97d25-112">Melden Sie sich bei Ihrem Azure-Konto an. Klicken Sie hierzu auf **Tools** (Extras) > **Azure** > **Sign In** (Anmelden).</span><span class="sxs-lookup"><span data-stu-id="97d25-112">To sign in to your Azure account, click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="97d25-113">![Eclipse-Menü für die Anmeldung bei Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="97d25-113">![Eclipse Menu for Azure Sign In][I01]</span></span>

1. <span data-ttu-id="97d25-114">Wählen Sie im Fenster für die Azure-Anmeldung \*\*\*\* die Option **Device Login** (Geräteanmeldung) aus, und klicken Sie anschließend auf **Sign in** (Anmelden). Weitere Anmeldeoptionen finden Sie [hier](azure-toolkit-for-eclipse-sign-in-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="97d25-114">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign-in options](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span></span>

   ![Fenster für die Azure Anmeldung mit ausgewählter Geräteanmeldung][I02]

1. <span data-ttu-id="97d25-116">Klicken Sie im Dialogfeld **Azure Device Login** (Azure-Geräteanmeldung) auf **Copy&Open** (Kopieren und öffnen).</span><span class="sxs-lookup"><span data-stu-id="97d25-116">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Dialogfeld für Azure-Anmeldung][I03]

1. <span data-ttu-id="97d25-118">Fügen Sie im Browser Ihren Gerätecode ein, den Sie im vorherigen Schritt durch Klicken auf **Copy&Open** (Kopieren und öffnen) kopiert haben, und klicken Sie anschließend auf **Next** (Weiter).</span><span class="sxs-lookup"><span data-stu-id="97d25-118">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Der Browser für die Geräteanmeldung][I04]

1. <span data-ttu-id="97d25-120">Wenn schließlich das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="97d25-120">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="97d25-122">Erstellen des Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="97d25-122">Creating web app project</span></span>

1. <span data-ttu-id="97d25-123">Klicken Sie auf **Datei**, dann auf **Neu** und schließlich auf **Dynamisches Webprojekt**.</span><span class="sxs-lookup"><span data-stu-id="97d25-123">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="97d25-124">(Wenn **Dynamic Web Project** (Dynamisches Webprojekt) nach dem Klicken auf **File** (Datei) und **New** (Neu) nicht als verfügbares Projekt aufgeführt ist, gehen Sie wie folgt vor: Klicken Sie auf **File** (Datei), anschließend auf **New** (Neu) und dann auf **Project...** (Projekt...). Erweitern Sie die Option **Web**, klicken Sie auf **Dynamic Web Project** (Dynamisches Webprojekt) und dann auf **Next** (Weiter).)</span><span class="sxs-lookup"><span data-stu-id="97d25-124">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Erstellen eines neuen dynamischen Webprojekts][file-new-dynamic-web-project]

2. <span data-ttu-id="97d25-126">Nennen Sie das Projekt für die Zwecke dieses Tutorials **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="97d25-126">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="97d25-127">Ihr Bildschirm sieht dann in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="97d25-127">Your screen will appear similar to the following:</span></span>
   
   ![Eigenschaften des neuen dynamischen Webprojekts][dynamic-web-project-properties]

3. <span data-ttu-id="97d25-129">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="97d25-129">Click **Finish**.</span></span>

4. <span data-ttu-id="97d25-130">Erweitern Sie in der Project Explorer-Ansicht von Eclipse die Option **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="97d25-130">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="97d25-131">Klicken Sie mit der rechten Maustaste auf **WebContent**, und klicken Sie dann auf **Neu** sowie auf **JSP-Datei**.</span><span class="sxs-lookup"><span data-stu-id="97d25-131">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Erstellen einer neuen JSP-Datei][create-new-jsp-file]

5. <span data-ttu-id="97d25-133">Geben Sie im Dialogfeld **New JSP File** (Neue JSP-Datei) den Namen **index.jsp** für die Datei ein. Behalten Sie den übergeordneten Ordner als **MyWebApp/WebContent** bei, und klicken Sie auf **Next** (Weiter).</span><span class="sxs-lookup"><span data-stu-id="97d25-133">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Dialogfeld „New JSP File“ (Neue JSP-Datei)][new-jsp-file-dialog]

6. <span data-ttu-id="97d25-135">Wählen Sie im Dialogfeld **Select JSP Template** (JSP-Vorlage auswählen) im Rahmen dieses Tutorials **New JSP File (html)** (Neue JSP-Datei (HTML)) aus, und klicken Sie dann auf **Finish** (Fertig stellen).</span><span class="sxs-lookup"><span data-stu-id="97d25-135">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Auswählen einer JSP-Vorlage][select-jsp-template]

7. <span data-ttu-id="97d25-137">Wenn in Eclipse die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein,</span><span class="sxs-lookup"><span data-stu-id="97d25-137">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="97d25-138">damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="97d25-138">within the existing `<body>` element.</span></span> <span data-ttu-id="97d25-139">Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="97d25-139">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="97d25-140">Speichern Sie die Datei „index.jsp“.</span><span class="sxs-lookup"><span data-stu-id="97d25-140">Save index.jsp.</span></span>

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="97d25-141">Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="97d25-141">Deploying web app to Azure</span></span>

1. <span data-ttu-id="97d25-142">Klicken Sie in der Projekt-Explorer-Ansicht von Eclipse mit der rechten Maustaste auf das Projekt, wählen Sie **Azure** aus, und wählen Sie dann **Publish as Azure Web App** (Als Azure-Web-App veröffentlichen) aus.</span><span class="sxs-lookup"><span data-stu-id="97d25-142">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Veröffentlichen als Azure-Web-App][publish-as-azure-web-app]

1. <span data-ttu-id="97d25-144">Im Dialogfeld **Web-App bereitstellen** können Sie eine der folgenden Optionen auswählen:</span><span class="sxs-lookup"><span data-stu-id="97d25-144">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="97d25-145">Wählen Sie eine vorhandene Web-App aus, sofern vorhanden.</span><span class="sxs-lookup"><span data-stu-id="97d25-145">Select an existing web app if one exists.</span></span>

      ![Auswählen eines App-Diensts][select-app-service]

   * <span data-ttu-id="97d25-147">Klicken Sie auf **Create New Web App** (Neue Web-App erstellen).</span><span class="sxs-lookup"><span data-stu-id="97d25-147">Click **Create New Web App**.</span></span>

      ![Erstellen eines App Service][create-app-service]

      <span data-ttu-id="97d25-149">Geben Sie die erforderlichen Informationen für Ihre Web-App im Dialogfeld **App Service erstellen** an, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="97d25-149">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      <span data-ttu-id="97d25-150">Hier können Sie die Runtime-Umgebung, App-Einstellungen, den Dienstplan und die Ressourcengruppe konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="97d25-150">Here you can configure the runtime environment, app settings, service plan and resource group.</span></span>

      ![Dialogfeld „App Service erstellen“][create-app-service-dialog]

1. <span data-ttu-id="97d25-152">Wählen Sie Ihre Web-App aus, und klicken Sie dann auf **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="97d25-152">Select your web app and then click **Deploy**.</span></span>

   ![Bereitstellen eines App-Diensts][deploy-app-service]

1. <span data-ttu-id="97d25-154">Im Toolkit wird auf der Registerkarte **Azure-Aktivitätsprotokoll** der Status **Veröffentlicht** angezeigt, wenn die Web-App bereitgestellt wurde. Der Status ist als Link für die URL der bereitgestellten Web-App formatiert.</span><span class="sxs-lookup"><span data-stu-id="97d25-154">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![Veröffentlichungsstatus][publish-status]

1. <span data-ttu-id="97d25-156">Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.</span><span class="sxs-lookup"><span data-stu-id="97d25-156">You can browse to your web app using the link provided in the status message.</span></span>

   ![Navigieren zur Web-App][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="cleaning-up-resources"></a><span data-ttu-id="97d25-158">Bereinigen der Ressourcen</span><span class="sxs-lookup"><span data-stu-id="97d25-158">Cleaning up resources</span></span>

1. <span data-ttu-id="97d25-159">Nachdem Sie Ihre Web-App in Azure veröffentlicht haben, können Sie sie verwalten, indem Sie im Azure-Explorer mit der rechten Maustaste darauf klicken und eine der Optionen aus dem Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="97d25-159">After you have published your web app to Azure, you can manage it by right-clicking in Azure Explorer and selecting one of the options in the context menu.</span></span> <span data-ttu-id="97d25-160">Dort können Sie beispielsweise Ihre Web-App \*\*\*\* löschen, um die Ressourcen für dieses Tutorial zu bereinigen.</span><span class="sxs-lookup"><span data-stu-id="97d25-160">For example, you can **Delete** your web app here to clean up the resource for this tutorial.</span></span>

   ![Verwalten des App-Diensts][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="97d25-162">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="97d25-162">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="97d25-163">Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].</span><span class="sxs-lookup"><span data-stu-id="97d25-163">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->
[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

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
