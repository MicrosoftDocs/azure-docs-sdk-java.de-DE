---
title: Erstellen einer „Hello World“-Web-App für Azure App Service mit IntelliJ
description: In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine „Hello World“-Web-App für Azure erstellen.
services: app-service
keywords: Java, IntelliJ, Web-App, Azure App Service, Hallo Welt, Hello World, Schnellstart
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ae0749ce1ddab971f1a83e2e5e58492fd8ccb287
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626118"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a><span data-ttu-id="91194-104">Erstellen einer „Hello World“-Web-App für Azure App Service mit IntelliJ</span><span class="sxs-lookup"><span data-stu-id="91194-104">Create a Hello World web app for Azure App Service using IntelliJ</span></span>

<span data-ttu-id="91194-105">Mithilfe des Open-Source-Plug-Ins [Azure-Toolkit für IntelliJ](https://plugins.jetbrains.com/plugin/8053) können Sie innerhalb weniger Minuten eine einfache „Hello World“-Anwendung erstellen und als Web-App in Azure App Service bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="91194-105">Using open sourced [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="91194-106">Ein ähnliches Tutorial für Eclipse finden Sie [hier][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="91194-106">If you prefer using Eclipse, check out our [similar tutorial for Eclipse][eclipse-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="91194-107">Denken Sie daran, die Ressourcen nach Abschluss dieses Tutorials zu bereinigen.</span><span class="sxs-lookup"><span data-stu-id="91194-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="91194-108">In diesem Fall wird Ihr kostenloses Kontokontingent im Rahmen dieses Leitfadens nicht überschritten.</span><span class="sxs-lookup"><span data-stu-id="91194-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="91194-109">Installation und Anmeldung</span><span class="sxs-lookup"><span data-stu-id="91194-109">Installation and Sign-in</span></span>

1. <span data-ttu-id="91194-110">Wählen Sie im Dialogfeld mit den Einstellungen/Voreinstellungen von IntelliJ IDEA (STRG+ALT+S) die Option **Plugins** (Plug-Ins) aus.</span><span class="sxs-lookup"><span data-stu-id="91194-110">In IntelliJ IDEA's Settings/Preferences dialog (Ctrl+Alt+S), select **Plugins**.</span></span> <span data-ttu-id="91194-111">Suchen Sie anschließend unter **Marketplace** nach **Azure Toolkit for IntelliJ** (Azure-Toolkit für IntelliJ), und klicken Sie auf **Install** (Installieren).</span><span class="sxs-lookup"><span data-stu-id="91194-111">Then, find the **Azure Toolkit for IntelliJ** in the **Marketplace** and click **Install**.</span></span> <span data-ttu-id="91194-112">Klicken Sie nach Abschluss der Installation auf **Restart** (Neu starten), um das Plug-In zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="91194-112">After installed, click **Restart** to activate the plugin.</span></span> 

   ![Plug-In „Azure-Toolkit für IntelliJ“ im Marketplace][marketplace]

2. <span data-ttu-id="91194-114">Melden Sie sich bei Ihrem Azure-Konto an. Öffnen Sie hierzu über die Seitenleiste den \*\*\*\* Azure-Explorer, und klicken Sie anschließend auf der Leiste am oberen Rand auf das Symbol \*\*\*\* für die Azure-Anmeldung, oder navigieren Sie im IDEA-Menü zu **Tools > Azure >Azure Sign in** (Extras > Azure > Azure-Anmeldung).</span><span class="sxs-lookup"><span data-stu-id="91194-114">To sign in to your Azure account, open sidebar **Azure Explorer**, and then click the **Azure Sign In** icon in the bar on top (or from IDEA menu **Tools/Azure/Azure Sign in**).</span></span>

   ![IntelliJ-Befehl für Azure-Anmeldung][I01]

3. <span data-ttu-id="91194-116">Wählen Sie im Fenster für die Azure-Anmeldung \*\*\*\* die Option **Device Login** (Geräteanmeldung) aus, und klicken Sie anschließend auf **Sign in** (Anmelden). Weitere Anmeldeoptionen finden Sie [hier](azure-toolkit-for-intellij-sign-in-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="91194-116">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign in options](azure-toolkit-for-intellij-sign-in-instructions.md)).</span></span>

   ![Fenster für die Azure-Anmeldung mit ausgewählter Geräteanmeldung][I02]

4. <span data-ttu-id="91194-118">Klicken Sie im Dialogfeld **Azure Device Login** (Azure-Geräteanmeldung) auf **Copy&Open** (Kopieren und öffnen).</span><span class="sxs-lookup"><span data-stu-id="91194-118">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Dialogfeld für Azure-Anmeldung][I03]

5. <span data-ttu-id="91194-120">Fügen Sie im Browser Ihren Gerätecode ein, den Sie im vorherigen Schritt durch Klicken auf **Copy&Open** (Kopieren und öffnen) kopiert haben, und klicken Sie anschließend auf **Next** (Weiter).</span><span class="sxs-lookup"><span data-stu-id="91194-120">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Der Browser für die Geräteanmeldung][I04]

6. <span data-ttu-id="91194-122">Wenn das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="91194-122">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="91194-124">Erstellen des Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="91194-124">Creating web app project</span></span>

1. <span data-ttu-id="91194-125">Klicken Sie in IntelliJ im Menü **File** (Datei) auf **New** (Neu) und anschließend auf **Project** (Projekt).</span><span class="sxs-lookup"><span data-stu-id="91194-125">In IntelliJ, click the **File** menu, then click **New**, and then click **Project**.</span></span>

   ![Erstellen eines neuen Projekts][file-new-project]

2. <span data-ttu-id="91194-127">Wählen Sie im Dialogfeld **Neues Projekt** die Option **Maven** und abschließend **maven-archetype-webapp** aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="91194-127">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>

   ![Auswählen von „maven-archetype-webapp“][maven-archetype-webapp]

3. <span data-ttu-id="91194-129">Geben Sie die **GroupId** und **ArtifactId** für Ihre Web-App an, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="91194-129">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>

   ![Eingeben von GroupId und ArtifactId][groupid-and-artifactid]

4. <span data-ttu-id="91194-131">Passen Sie alle gewünschten Maven-Einstellungen an, oder übernehmen Sie die Standardeinstellungen, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="91194-131">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>

   ![Angeben von Maven-Einstellungen][maven-options]

5. <span data-ttu-id="91194-133">Geben Sie den Projektnamen und einen Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="91194-133">Specify your project name and location, and then click **Finish**.</span></span>

   ![Angeben des Projektnamens][project-name]

6. <span data-ttu-id="91194-135">Öffnen Sie die Datei **src/main/webapp/index.jsp** im Projektexplorer, bearbeiten Sie sie wie folgt, und **speichern Sie die Änderungen**:</span><span class="sxs-lookup"><span data-stu-id="91194-135">Under Project Explorer view, open and edit the file **src/main/webapp/index.jsp** as following and **save the changes**:</span></span>

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Bearbeiten der Indexseite][edit-index-page]

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="91194-137">Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="91194-137">Deploying web app to Azure</span></span>

1. <span data-ttu-id="91194-138">Klicken Sie im Projektexplorer mit der rechten Maustaste auf Ihr Projekt, erweitern Sie **Azure**, und klicken Sie anschließend auf **Deploy to Azure** (In Azure bereitstellen).</span><span class="sxs-lookup"><span data-stu-id="91194-138">Under Project Explorer view, right-click your project, expand **Azure**, then click **Deploy to Azure**.</span></span>

   ![Menüoption zum Bereitstellen in Azure][deploy-to-azure-menu]

1. <span data-ttu-id="91194-140">Im Dialogfeld für die Bereitstellung in Azure können Sie die Anwendung direkt für eine vorhandene Tomcat-Web-App bereitstellen, sofern Sie bereits über eine solche Web-App verfügen. Andernfalls müssen Sie zunächst eine neue Web-App erstellen.</span><span class="sxs-lookup"><span data-stu-id="91194-140">In the Deploy to Azure dialog box, you can directly deploy the application to an existing Tomcat webapp if you already have one, otherwise you should create a new one first.</span></span>
   1. <span data-ttu-id="91194-141">Klicken Sie auf den Link **No available webapp, click to create a new one** (Keine Web-App verfügbar. Klicken Sie hier, um eine neue zu erstellen.), um eine neue Web-App zu erstellen. Falls in Ihrem Abonnement bereits Web-Apps vorhanden sind, können Sie in der Web-App-Dropdownliste die Option **Create New WebApp** (Neue Web-App erstellen) auswählen.</span><span class="sxs-lookup"><span data-stu-id="91194-141">Click the link **No Available webapp, click to create a new one** to crete a new web app, you could choose **Create New WebApp** from WebApp dropdown if there are existing webapps in your subscription.</span></span>

      ![Dialogfeld zum Bereitstellen in Azure][deploy-to-azure-dialog]

   1. <span data-ttu-id="91194-143">Wählen Sie im Popupdialogfeld die Option **TOMCAT 8.5-jre8** als Webcontainer aus, und geben Sie die übrigen erforderlichen Informationen an. Klicken Sie abschließend auf **OK**, um die Web-App zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="91194-143">In the pop-up dialog box, chose **TOMCAT 8.5-jre8** as Web Container and specify other required information, then click **OK** to create the webapp.</span></span>

      ![Create new web app (Neue Web-App erstellen)][create-new-web-app-dialog]

   1. <span data-ttu-id="91194-145">Wählen Sie in der Web-App-Dropdownliste die Web-App aus, und klicken Sie anschließend auf **Run** (Ausführen). (Wenn Sie die Bereitstellung für eine bereits vorhandene Web-App ausführen möchten, können Sie an dieser Stelle beginnen.)</span><span class="sxs-lookup"><span data-stu-id="91194-145">Choose the web app from WebApp drop down, and then click **Run**.(You could start from here if you want deploy to an existing webapp)</span></span>

      ![Bereitstellen für eine vorhandene Web-App][deploy-to-existing-webapp]

1. <span data-ttu-id="91194-147">Nachdem Ihre Web-App bereitgestellt wurde, wird im Toolkit eine Statusmeldung angezeigt. Diese enthält auch die URL Ihrer bereitgestellten Web-App, sofern die Bereitstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="91194-147">The toolkit will display a status message when it has successfully deployed your web app, along with the URL of your deployed web app if succeed.</span></span>

   ![Erfolgreiche Bereitstellung][successfully-deployed]

1. <span data-ttu-id="91194-149">Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.</span><span class="sxs-lookup"><span data-stu-id="91194-149">You can browse to your web app using the link provided in the status message.</span></span>

   ![Navigieren zur Web-App][browse-web-app]

## <a name="managing-deploy-configurations"></a><span data-ttu-id="91194-151">Verwalten von Bereitstellungskonfigurationen</span><span class="sxs-lookup"><span data-stu-id="91194-151">Managing deploy configurations</span></span>

1. <span data-ttu-id="91194-152">Nachdem Sie Ihre Web-App veröffentlicht haben, werden Ihre Einstellungen als Standard gespeichert, und Sie können die Bereitstellung ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken.</span><span class="sxs-lookup"><span data-stu-id="91194-152">After you have published your web app, your settings will be saved as the default, and you can run the deployment by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="91194-153">Sie können die Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.</span><span class="sxs-lookup"><span data-stu-id="91194-153">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. <span data-ttu-id="91194-155">Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="91194-155">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a><span data-ttu-id="91194-157">Bereinigen der Ressourcen</span><span class="sxs-lookup"><span data-stu-id="91194-157">Cleaning up resources</span></span>

1. <span data-ttu-id="91194-158">Löschen von Web-Apps im Azure-Explorer</span><span class="sxs-lookup"><span data-stu-id="91194-158">Deleting Web Apps in Azure Explorer</span></span>

     ![Ressourcenbereinigung][clean-resources]

## <a name="next-steps"></a><span data-ttu-id="91194-160">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="91194-160">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="91194-161">Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].</span><span class="sxs-lookup"><span data-stu-id="91194-161">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->
[marketplace]:./media/azure-toolkit-for-intellij-create-hello-world-web-app/marketplace.png
[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[deploy-to-azure-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[deploy-to-azure-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[deploy-to-existing-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/deploy-to-existing-webapp.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
[clean-resources]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/clean-resource.png
[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-intellij-sign-in-instructions/I05.png
