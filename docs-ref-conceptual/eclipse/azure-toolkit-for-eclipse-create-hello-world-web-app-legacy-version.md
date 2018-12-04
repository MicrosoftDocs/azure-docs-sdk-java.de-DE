---
title: ''
description: In diesem Tutorial erfahren Sie, wie Sie mit Version 3.0.6 (oder einer älteren Version) des Azure-Toolkits für Eclipse eine „Hello World“-Web-App für Azure erstellen.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: b05dcd52f36524ab17652f83c6ced4006f874365
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338714"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a><span data-ttu-id="37e9a-102">Erstellen einer „Hello World“-Web-App für Azure mit dem Legacytoolkit für Eclipse</span><span class="sxs-lookup"><span data-stu-id="37e9a-102">Create a Hello World web app for Azure using the legacy toolkit for Eclipse</span></span>

<span data-ttu-id="37e9a-103">Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe von Version 3.0.6 (oder einer älteren Version) des [Azure-Toolkit für Eclipse].</span><span class="sxs-lookup"><span data-stu-id="37e9a-103">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="37e9a-104">Eine Version dieses Artikels, in dem das [Azure-Toolkit für IntelliJ] verwendet wird, finden Sie unter [Erstellen einer einfachen Azure-Web-App in IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="37e9a-104">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="37e9a-105">Das Azure-Toolkit für Eclipse wurde im August 2017 mit einem anderen Workflow aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="37e9a-105">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="37e9a-106">In diesem Artikel wird das Erstellen einer „Hello World“-Web-App mithilfe der Version 3.0.6 (oder einer älteren Version) des Azure-Toolkits für Eclipse veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="37e9a-106">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="37e9a-107">Wenn Sie die Version 3.0.7 (oder eine höhere Version) des Toolkits verwenden, müssen Sie die Schritte unter [Erstellen einer einfachen Azure-Web-App mit Eclipse][Updated Version] ausführen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-107">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse][Updated Version].</span></span>
>

<span data-ttu-id="37e9a-108">Wenn Sie dieses Tutorial abgeschlossen haben, entspricht Ihre Anwendung bei der Anzeige in einem Webbrowser etwa der folgenden Abbildung:</span><span class="sxs-lookup"><span data-stu-id="37e9a-108">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Vorschau der Hello World-App][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="37e9a-110">Erstellen eines neuen Web-App-Projekts</span><span class="sxs-lookup"><span data-stu-id="37e9a-110">Create a new web app project</span></span>

1. <span data-ttu-id="37e9a-111">Starten Sie Eclipse, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse][eclipse-sign-in-instructions] an.</span><span class="sxs-lookup"><span data-stu-id="37e9a-111">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="37e9a-112">Klicken Sie auf **Datei**, dann auf **Neu** und schließlich auf **Dynamisches Webprojekt**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-112">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="37e9a-113">(Wenn **Dynamic Web Project** (Dynamisches Webprojekt) nach dem Klicken auf **File** (Datei) und **New** (Neu) nicht als verfügbares Projekt aufgeführt ist, gehen Sie wie folgt vor: Klicken Sie auf **File** (Datei), anschließend auf **New** (Neu) und dann auf **Project...** (Projekt...). Erweitern Sie die Option **Web**, klicken Sie auf **Dynamic Web Project** (Dynamisches Webprojekt) und dann auf **Next** (Weiter).)</span><span class="sxs-lookup"><span data-stu-id="37e9a-113">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="37e9a-114">Nennen Sie das Projekt für die Zwecke dieses Tutorials **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-114">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="37e9a-115">Ihr Bildschirm sieht dann in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="37e9a-115">Your screen will appear similar to the following:</span></span>
   
   ![Erstellen eines neuen dynamischen Webprojekts][02]

3. <span data-ttu-id="37e9a-117">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-117">Click **Finish**.</span></span>

4. <span data-ttu-id="37e9a-118">Erweitern Sie in der **Project Explorer**-Ansicht von Eclipse die Option **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-118">Within Eclipse's **Project Explorer** view, expand **MyWebApp**.</span></span> <span data-ttu-id="37e9a-119">Klicken Sie mit der rechten Maustaste auf **WebContent**, und klicken Sie dann auf **Neu** sowie auf **JSP-Datei**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-119">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="37e9a-120">Geben Sie im Dialogfeld **New JSP File** (Neue JSP-Datei) den Namen **index.jsp** für die Datei ein. Behalten Sie den übergeordneten Ordner als **MyWebApp/WebContent** bei, und klicken Sie auf **Next** (Weiter).</span><span class="sxs-lookup"><span data-stu-id="37e9a-120">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="37e9a-121">Wählen Sie im Dialogfeld **Select JSP Template** (JSP-Vorlage auswählen) im Rahmen dieses Tutorials **New JSP File (html)** (Neue JSP-Datei (HTML)) aus, und klicken Sie dann auf **Finish** (Fertig stellen).</span><span class="sxs-lookup"><span data-stu-id="37e9a-121">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="37e9a-122">Wenn in Eclipse die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein,</span><span class="sxs-lookup"><span data-stu-id="37e9a-122">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="37e9a-123">damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="37e9a-123">within the existing `<body>` element.</span></span> <span data-ttu-id="37e9a-124">Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="37e9a-124">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="37e9a-125">Speichern Sie die Datei „index.jsp“.</span><span class="sxs-lookup"><span data-stu-id="37e9a-125">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="37e9a-126">Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="37e9a-126">Deploy your web app to Azure</span></span>

<span data-ttu-id="37e9a-127">Es gibt mehrere Möglichkeiten, eine Java-Webanwendung in Azure bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-127">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="37e9a-128">In diesem Tutorial wird eine der einfachsten beschrieben: Ihre Anwendung wird in einem Azure-Web-App-Container bereitgestellt – weder ein spezieller Projekttyp noch zusätzliche Tools sind erforderlich.</span><span class="sxs-lookup"><span data-stu-id="37e9a-128">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="37e9a-129">Das JDK und die Webcontainersoftware werden von Azure für Sie bereitgestellt, sodass Sie weder ein eigenes JDK noch eigene Webcontainersoftware hochladen müssen; Sie benötigen lediglich Ihre Java Web-App.</span><span class="sxs-lookup"><span data-stu-id="37e9a-129">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="37e9a-130">Darum dauert der Veröffentlichungsprozess für Ihre Anwendung nur Sekunden, nicht Minuten.</span><span class="sxs-lookup"><span data-stu-id="37e9a-130">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="37e9a-131">Klicken Sie in Eclipse Project Explorer mit der rechten Maustaste auf **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-131">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="37e9a-132">Wählen Sie im Kontextmenü **Azure** aus, und klicken Sie dann auf **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen...).</span><span class="sxs-lookup"><span data-stu-id="37e9a-132">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Veröffentlichen als Azure-Web-App][03]
   
   <span data-ttu-id="37e9a-134">Alternativ können Sie auch das Webanwendungsprojekt im Projekt-Explorer auswählen und auf der Symbolleiste auf die Dropdownschaltfläche **Publish** (Veröffentlichen) klicken. Wählen Sie anschließend **Publish as Azure Web App** (Als Azure-Web-App veröffentlichen) aus:</span><span class="sxs-lookup"><span data-stu-id="37e9a-134">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Veröffentlichen als Azure-Web-App][14]

3. <span data-ttu-id="37e9a-136">Wenn Sie sich noch nicht von Eclipse aus bei Azure angemeldet haben, werden Sie aufgefordert, sich bei Ihrem Azure-Konto anzumelden:</span><span class="sxs-lookup"><span data-stu-id="37e9a-136">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Azure-Anmeldedialogfeld][04]
   
   <span data-ttu-id="37e9a-138">Wenn Sie über mehrere Azure-Konten verfügen, können einige der Eingabeaufforderungen während des Anmeldeprozesses mehrmals angezeigt werden, auch wenn sie scheinbar identisch sind.</span><span class="sxs-lookup"><span data-stu-id="37e9a-138">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="37e9a-139">Befolgen Sie in diesem Fall weiterhin die Anweisungen zur Anmeldung.</span><span class="sxs-lookup"><span data-stu-id="37e9a-139">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="37e9a-140">Nachdem Sie sich erfolgreich bei Ihrem Azure-Konto angemeldet haben, wird im Dialogfeld **Manage Subscriptions** (Abonnements verwalten) eine Liste der Abonnements angezeigt, die mit Ihren Anmeldeinformationen verknüpft sind.</span><span class="sxs-lookup"><span data-stu-id="37e9a-140">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="37e9a-141">Wenn mehrere Abonnements aufgeführt sind und Sie nur mit einer bestimmten Teilmenge davon arbeiten möchten, können Sie optional die Abonnements deaktivieren, die Sie nicht verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="37e9a-141">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="37e9a-142">Wenn Sie Ihre Abonnements ausgewählt haben, klicken Sie auf **Schließen**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-142">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Dialogfeld zum Verwalten von Abonnements][05]

5. <span data-ttu-id="37e9a-144">Wenn das Dialogfeld **Deploy to Azure Web App Container** (In Azure-Web-App-Container bereitstellen) angezeigt wird, werden alle Web-App-Container angezeigt, die Sie zuvor erstellt haben. Wenn Sie keine Container erstellt haben, ist die Liste leer.</span><span class="sxs-lookup"><span data-stu-id="37e9a-144">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Dialogfeld zum Bereitstellen im Azure-Web-App-Container][06]

6. <span data-ttu-id="37e9a-146">Wenn Sie zuvor keinen Azure-Web-App-Container erstellt haben, oder Sie Ihre Anwendung in einem neuen Container veröffentlichen möchten, führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="37e9a-146">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="37e9a-147">Wählen Sie andernfalls einen vorhandenen Web-App-Container, und fahren Sie mit Schritt 7 fort.</span><span class="sxs-lookup"><span data-stu-id="37e9a-147">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="37e9a-148">a.</span><span class="sxs-lookup"><span data-stu-id="37e9a-148">a.</span></span> <span data-ttu-id="37e9a-149">Klicken Sie auf **New...**</span><span class="sxs-lookup"><span data-stu-id="37e9a-149">Click **New...**</span></span>
      
      ![Dialogfeld zum Bereitstellen im Azure-Web-App-Container][15]

   <span data-ttu-id="37e9a-151">b.</span><span class="sxs-lookup"><span data-stu-id="37e9a-151">b.</span></span> <span data-ttu-id="37e9a-152">Das Dialogfeld **New Web App Container** (Neuer Web-App-Container) wird angezeigt:</span><span class="sxs-lookup"><span data-stu-id="37e9a-152">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![Dialogfeld für neuen Web-App-Container][07a]

   <span data-ttu-id="37e9a-154">c.</span><span class="sxs-lookup"><span data-stu-id="37e9a-154">c.</span></span> <span data-ttu-id="37e9a-155">Geben Sie eine **DNS-Bezeichnung** für Ihren Web-App-Container ein; dies ist die Blatt-DNS-Bezeichnung der Host-URL für Ihre Webanwendung in Azure.</span><span class="sxs-lookup"><span data-stu-id="37e9a-155">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="37e9a-156">(Hinweis: Der Name muss verfügbar sein und den Azure-Web-App-Namenskonventionen entsprechen.)</span><span class="sxs-lookup"><span data-stu-id="37e9a-156">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="37e9a-157">d.</span><span class="sxs-lookup"><span data-stu-id="37e9a-157">d.</span></span> <span data-ttu-id="37e9a-158">Wählen Sie im Dropdownmenü **Web Container** (Webcontainer) die passende Software für Ihre Anwendung aus.</span><span class="sxs-lookup"><span data-stu-id="37e9a-158">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="37e9a-159">Aktuell können Sie zwischen Tomcat 8, Tomcat 7 und Jetty 9 wählen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-159">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="37e9a-160">Azure stellt eine aktuelle Distribution der gewählten Software bereit und diese wird auf einer aktuellen Distribution des von Azure bereitgestellten JDK ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="37e9a-160">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of the JDK provided by Azure.</span></span>

   <span data-ttu-id="37e9a-161">e.</span><span class="sxs-lookup"><span data-stu-id="37e9a-161">e.</span></span> <span data-ttu-id="37e9a-162">Wählen Sie im Dropdownmenü **Subscription** (Abonnement) das Abonnement aus, das Sie für diese Bereitstellung verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="37e9a-162">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="37e9a-163">f.</span><span class="sxs-lookup"><span data-stu-id="37e9a-163">f.</span></span> <span data-ttu-id="37e9a-164">Wählen Sie im Dropdownmenü **Resource Group** (Ressourcengruppe) die Ressourcengruppe aus, der Sie Ihre Web-App zuordnen möchten.</span><span class="sxs-lookup"><span data-stu-id="37e9a-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="37e9a-165">(Mithilfe von Azure-Ressourcengruppen können Sie verwandte Ressourcen gruppieren, um diese z.B. gemeinsam löschen zu können.)</span><span class="sxs-lookup"><span data-stu-id="37e9a-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="37e9a-166">Sie können eine vorhandene Ressourcengruppe auswählen (sofern vorhanden) und direkt mit Schritt g unten fortfahren oder die folgenden Schritte ausführen, um eine neue Ressourcengruppe zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="37e9a-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
   * <span data-ttu-id="37e9a-167">Klicken Sie auf **New...**</span><span class="sxs-lookup"><span data-stu-id="37e9a-167">Click **New...**</span></span>
   * <span data-ttu-id="37e9a-168">Das Dialogfeld **New Resource Group** (Neue Ressourcengruppe) wird angezeigt:</span><span class="sxs-lookup"><span data-stu-id="37e9a-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
       ![Dialogfeld für neue Ressourcengruppe][08]
   * <span data-ttu-id="37e9a-170">Geben Sie im Textfeld **Name** einen Namen für die neue Ressourcengruppe ein.</span><span class="sxs-lookup"><span data-stu-id="37e9a-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
   * <span data-ttu-id="37e9a-171">Wählen Sie im Dropdownmenü **Region** den entsprechenden Azure-Rechenzentrumsstandort für Ihre Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="37e9a-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
   * <span data-ttu-id="37e9a-172">OPTIONAL: Standardmäßig stellt Azure automatisch eine aktuelle Distribution von Java 8 in Ihrem Web-App-Container als JVM bereit.</span><span class="sxs-lookup"><span data-stu-id="37e9a-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="37e9a-173">Sie können jedoch eine andere JVM-Version und -Distribution angeben, wenn Ihre Web-App dies erfordert.</span><span class="sxs-lookup"><span data-stu-id="37e9a-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="37e9a-174">Um das JDK für Ihre Web-App anzugeben, klicken Sie auf die Registerkarte **JDK** , und wählen Sie eine der folgenden Optionen aus:</span><span class="sxs-lookup"><span data-stu-id="37e9a-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
     * <span data-ttu-id="37e9a-175">**Deploy the default JDK offered by Azure Web Apps service**(Das vom Azure-Web-Apps-Dienst angebotene Standard-JDK bereitstellen): Diese Option stellt eine aktuelle Distribution von Java bereit.</span><span class="sxs-lookup"><span data-stu-id="37e9a-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java.</span></span>
     * <span data-ttu-id="37e9a-176">**Deploy a 3rd party JDK available on Azure**(Ein in Azure verfügbares JDK eines Drittanbieters bereitstellen): Mit dieser Option können Sie aus einer Liste der von Microsoft Azure angebotenen JDKs auswählen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
     * <span data-ttu-id="37e9a-177">**Deploy my own JDK from this download location**(Eigenes JDK von diesem Downloadspeicherort bereitstellen): Mit dieser Option können Sie Ihre eigene JDK-Distribution angeben, die als ZIP-Datei gepackt und entweder in einen öffentlich verfügbaren Speicherort oder in ein Azure-Speicherkonto hochgeladen sein muss, auf das Sie Zugriff haben.</span><span class="sxs-lookup"><span data-stu-id="37e9a-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
       ![Dialogfeld für neuen Web-App-Container][07b]

   <span data-ttu-id="37e9a-179">g.</span><span class="sxs-lookup"><span data-stu-id="37e9a-179">g.</span></span> <span data-ttu-id="37e9a-180">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-180">Click **OK**.</span></span>

   <span data-ttu-id="37e9a-181">h.</span><span class="sxs-lookup"><span data-stu-id="37e9a-181">h.</span></span> <span data-ttu-id="37e9a-182">Im Dropdownmenü **App Service Plan** (App Service-Plan) werden die App Service-Pläne aufgelistet, die der ausgewählten Ressourcengruppe zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="37e9a-182">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="37e9a-183">(App Service-Pläne enthalten verschiedene Informationen wie z.B. den Speicherort Ihrer Web-App, den Tarif und die Größe der Compute-Instanz.</span><span class="sxs-lookup"><span data-stu-id="37e9a-183">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="37e9a-184">Da ein App Service-Plan für mehrere Web-Apps verwendet werden kann, wird er getrennt von einer bestimmten Web-App-Bereitstellung verwaltet.)</span><span class="sxs-lookup"><span data-stu-id="37e9a-184">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="37e9a-185">Klicken Sie auf **New...**</span><span class="sxs-lookup"><span data-stu-id="37e9a-185">Click **New...**</span></span>
      * <span data-ttu-id="37e9a-186">Das Dialogfeld **New App Service Plan** (Neuer App Service-Plan) wird angezeigt:</span><span class="sxs-lookup"><span data-stu-id="37e9a-186">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Dialogfeld für neuen App Service-Plan][09]
      * <span data-ttu-id="37e9a-188">Geben Sie im Textfeld **Name** einen Namen für den neuen App Service-Plan ein.</span><span class="sxs-lookup"><span data-stu-id="37e9a-188">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="37e9a-189">Wählen Sie im Dropdownmenü **Location** (Standort) den entsprechenden Azure-Rechenzentrumsstandort für den Plan aus.</span><span class="sxs-lookup"><span data-stu-id="37e9a-189">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="37e9a-190">Wählen Sie im Dropdownmenü **Pricing Tier** (Tarif) die entsprechenden Preise für den Plan aus.</span><span class="sxs-lookup"><span data-stu-id="37e9a-190">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="37e9a-191">Zu Testzwecken können Sie **Free**(Kostenlos) auswählen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-191">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="37e9a-192">Wählen Sie im Dropdownmenü **Instance Size** (Instanzgröße) die entsprechende Instanzgröße für den Plan aus.</span><span class="sxs-lookup"><span data-stu-id="37e9a-192">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="37e9a-193">Zu Testzwecken können Sie **Small**(Klein) wählen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-193">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="37e9a-194">i.</span><span class="sxs-lookup"><span data-stu-id="37e9a-194">i.</span></span> <span data-ttu-id="37e9a-195">Wenn Sie alle oben genannten Schritte abgeschlossen haben, sollte das Dialogfeld „New Web App Container“ (Neuer Web-App-Container) folgender Abbildung ähneln:</span><span class="sxs-lookup"><span data-stu-id="37e9a-195">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Dialogfeld für neuen Web-App-Container][10]

   <span data-ttu-id="37e9a-197">j.</span><span class="sxs-lookup"><span data-stu-id="37e9a-197">j.</span></span> <span data-ttu-id="37e9a-198">Klicken Sie auf **OK** , um die Erstellung Ihres neuen Web-App-Containers abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-198">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="37e9a-199">Warten Sie einige Sekunden, bis die Liste der Web-App-Container aktualisiert wurde. Ihr neu erstellter Web-App-Container sollte nun in der Liste angezeigt werden und markiert sein.</span><span class="sxs-lookup"><span data-stu-id="37e9a-199">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="37e9a-200">Sie können jetzt die erste Bereitstellung Ihrer Web-App in Azure abschließen:</span><span class="sxs-lookup"><span data-stu-id="37e9a-200">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Dialogfeld zum Bereitstellen im Azure-Web-App-Container][11]
   
   <span data-ttu-id="37e9a-202">Klicken Sie auf **OK** , um Ihre Java-Anwendung im ausgewählten Web-App-Container bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-202">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="37e9a-203">Standardmäßig wird die Anwendung als Unterverzeichnis des Anwendungsservers bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="37e9a-203">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="37e9a-204">Wenn sie als Stammanwendung bereitgestellt werden soll, aktivieren Sie das Kontrollkästchen **Deploy to root** (In Stamm bereitstellen), bevor Sie auf **OK** klicken.</span><span class="sxs-lookup"><span data-stu-id="37e9a-204">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="37e9a-205">Als Nächstes sollte das **Azure-Aktivitätsprotokoll** mit dem Bereitstellungsstatus der Web-App angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="37e9a-205">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Azure-Aktivitätsprotokoll][12]
   
   <span data-ttu-id="37e9a-207">Die Bereitstellung Ihrer Web-App in Azure sollte nur einige Sekunden dauern.</span><span class="sxs-lookup"><span data-stu-id="37e9a-207">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="37e9a-208">Wenn Ihre Anwendung bereit ist, wird in der Spalte **Veröffentlicht** in the **Veröffentlicht** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="37e9a-208">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="37e9a-209">Wenn Sie auf den Link klicken, gelangen Sie zur Startseite Ihrer bereitgestellten Web-App.</span><span class="sxs-lookup"><span data-stu-id="37e9a-209">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="37e9a-210">Aktualisieren Ihrer Web-App</span><span class="sxs-lookup"><span data-stu-id="37e9a-210">Updating your web app</span></span>

<span data-ttu-id="37e9a-211">Das Aktualisieren einer vorhandenen, ausgeführten Azure-Web-App ist ein schneller und einfacher Prozess, und Ihnen stehen zwei Optionen für die Aktualisierung zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="37e9a-211">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="37e9a-212">Sie können die Bereitstellung einer vorhandenen Java-Web-App aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="37e9a-212">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="37e9a-213">Sie können eine weitere Java-Anwendung in dem gleichen Web-App-Container veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-213">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="37e9a-214">In beiden Fällen ist der Prozess identisch und dauert nur wenige Sekunden:</span><span class="sxs-lookup"><span data-stu-id="37e9a-214">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="37e9a-215">Klicken Sie im Projektexplorer von Eclipse mit der rechten Maustaste auf die Java-Anwendung, die Sie aktualisieren oder einem vorhandenen Web-App-Container hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="37e9a-215">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="37e9a-216">Wählen Sie im Kontextmenü **Azure** und dann **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen) aus.</span><span class="sxs-lookup"><span data-stu-id="37e9a-216">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="37e9a-217">Da Sie sich bereits zuvor angemeldet haben, sehen Sie eine Liste Ihrer vorhandenen Web-App-Container.</span><span class="sxs-lookup"><span data-stu-id="37e9a-217">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="37e9a-218">Wählen Sie den Container aus, in dem Sie Ihre Java-Anwendung veröffentlichen oder erneut veröffentlichen möchten, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-218">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="37e9a-219">Wenige Sekunden später wird Ihre aktualisierte Bereitstellung in der Ansicht **Azure Activity Log** (Azure-Aktivitätsprotokoll) als **Published** (Veröffentlicht) angezeigt, und Sie können die aktualisierte Anwendung in einem Webbrowser überprüfen.</span><span class="sxs-lookup"><span data-stu-id="37e9a-219">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="37e9a-220">Starten, Beenden oder Neustarten einer vorhandenen Web-App</span><span class="sxs-lookup"><span data-stu-id="37e9a-220">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="37e9a-221">Um einen vorhandenen Azure-Web-App-Container zu starten oder zu beenden (einschließlich aller darin bereitgestellten Java-Anwendungen), können Sie die Ansicht **Azure Explorer** verwenden.</span><span class="sxs-lookup"><span data-stu-id="37e9a-221">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="37e9a-222">Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in Eclipse auf das Menü **Window** (Fenster) und dann auf **Show View** (Ansicht anzeigen), **Other...** (Andere...), **Azure** und **Azure Explorer** klicken.</span><span class="sxs-lookup"><span data-stu-id="37e9a-222">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="37e9a-223">Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="37e9a-223">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="37e9a-224">Wenn die Ansicht **Azure Explorer** angezeigt wird, starten oder beenden Sie Ihre Web-App mit folgenden Schritten:</span><span class="sxs-lookup"><span data-stu-id="37e9a-224">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="37e9a-225">Erweitern Sie den Knoten **Azure** .</span><span class="sxs-lookup"><span data-stu-id="37e9a-225">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="37e9a-226">Erweitern Sie den Knoten **Web Apps** (Web-Apps).</span><span class="sxs-lookup"><span data-stu-id="37e9a-226">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="37e9a-227">Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.</span><span class="sxs-lookup"><span data-stu-id="37e9a-227">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="37e9a-228">Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Starten**, **Beenden** oder **Neu starten**.</span><span class="sxs-lookup"><span data-stu-id="37e9a-228">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="37e9a-229">Beachten Sie, dass die Menüoptionen kontextabhängig sind. Sie können nur eine ausgeführte Web-App beenden oder eine Web-App starten, die zurzeit nicht ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="37e9a-229">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Beenden einer vorhandenen Web-App][13]

## <a name="next-steps"></a><span data-ttu-id="37e9a-231">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="37e9a-231">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="37e9a-232">Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].</span><span class="sxs-lookup"><span data-stu-id="37e9a-232">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure-Toolkit für Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure-Toolkit für IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-eclipse-create-hello-world-web-app.md
[eclipse-sign-in-instructions]: azure-toolkit-for-eclipse-sign-in-instructions.md


<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/15-New-Azure-Web-Container.png
