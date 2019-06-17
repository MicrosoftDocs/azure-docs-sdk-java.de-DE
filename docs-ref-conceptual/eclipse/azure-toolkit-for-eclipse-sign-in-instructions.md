---
title: Anleitung zur Anmeldung für das Azure-Toolkit für Eclipse
description: Erfahren Sie, wie Sie sich bei Microsoft Azure mit dem Azure-Toolkit für Eclipse anmelden.
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
ms.openlocfilehash: b4b13de38913ae6e7ae2bb09210ac742efc9d0ad
ms.sourcegitcommit: d18d9dce22b7f7af178f756bd341433d24e3c3b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2019
ms.locfileid: "66575317"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="8f787-103">Anleitung zur Anmeldung für das Azure-Toolkit für Eclipse</span><span class="sxs-lookup"><span data-stu-id="8f787-103">Sign-in instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="8f787-104">Das Azure-Toolkit für Eclipse bietet zwei Methoden für die Anmeldung bei Ihrem Azure-Konto:</span><span class="sxs-lookup"><span data-stu-id="8f787-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  - [<span data-ttu-id="8f787-105">Anmelden bei Ihrem Azure-Konto per Geräteanmeldung</span><span class="sxs-lookup"><span data-stu-id="8f787-105">Sign in to your Azure account by Device Login</span></span>](#sign-in-to-your-azure-account-by-device-login)
  - [<span data-ttu-id="8f787-106">Anmelden bei Ihrem Azure-Konto per Dienstprinzipal</span><span class="sxs-lookup"><span data-stu-id="8f787-106">Sign in to your Azure account by Service Principal</span></span>](#sign-in-to-your-azure-account-by-service-principal)

<span data-ttu-id="8f787-107">Auch [**Abmeldemethoden**](#sign-out-of-your-azure-account) stehen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="8f787-107">[**Sign out**](#sign-out-of-your-azure-account) methods are also provided.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a><span data-ttu-id="8f787-108">Anmelden bei Ihrem Azure-Konto per Geräteanmeldung</span><span class="sxs-lookup"><span data-stu-id="8f787-108">Sign in to your Azure account by Device Login</span></span>

<span data-ttu-id="8f787-109">Gehen Sie wie folgt vor, um sich per Geräteanmeldung bei Azure anzumelden:</span><span class="sxs-lookup"><span data-stu-id="8f787-109">To sign in Azure by device login, do the following:</span></span>

1. <span data-ttu-id="8f787-110">Öffnen Sie das Projekt in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8f787-110">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="8f787-111">Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="8f787-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="8f787-112">![Eclipse-Menü für die Anmeldung bei Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="8f787-112">![Eclipse Menu for Azure Sign In][I01]</span></span>

3. <span data-ttu-id="8f787-113">Wählen Sie im Fenster **Azure Sign In** (Azure-Anmeldung) die Option **Device Login** (Geräteanmeldung) aus, und klicken Sie anschließend auf **Sign in** (Anmelden).</span><span class="sxs-lookup"><span data-stu-id="8f787-113">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in**.</span></span>

   ![Fenster für die Azure-Anmeldung mit ausgewählter Geräteanmeldung][I02]

4. <span data-ttu-id="8f787-115">Klicken Sie im Dialogfeld **Azure Device Login** (Azure-Geräteanmeldung) auf **Copy&Open** (Kopieren und öffnen).</span><span class="sxs-lookup"><span data-stu-id="8f787-115">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Dialogfeld für Azure-Anmeldung][I03]

> [!NOTE]
>
> <span data-ttu-id="8f787-117">Sollte der Browser nicht geöffnet werden, konfigurieren Sie Eclipse für die Verwendung eines externen Browsers wie Internet Explorer, Firefox oder Chrome:</span><span class="sxs-lookup"><span data-stu-id="8f787-117">If the browser doesn't open, configure Eclipse to use an external browser like Internet Explorer, Firefox, or Chrome:</span></span>
>
> 1. <span data-ttu-id="8f787-118">Öffnen Sie „Preferences“ (Voreinstellungen) > „General“ (Allgemein) > „Web Browser“ (Webbrowser) > „Use external web browser in Eclipse“ (Externen Webbrowser in Eclipse verwenden).</span><span class="sxs-lookup"><span data-stu-id="8f787-118">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="8f787-119">Wählen Sie den gewünschten Browser aus.</span><span class="sxs-lookup"><span data-stu-id="8f787-119">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="8f787-120">Fügen Sie im Browser Ihren Gerätecode ein, den Sie im vorherigen Schritt durch Klicken auf **Copy&Open** (Kopieren und öffnen) kopiert haben, und klicken Sie anschließend auf **Next** (Weiter).</span><span class="sxs-lookup"><span data-stu-id="8f787-120">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Der Browser für die Geräteanmeldung][I04]

6. <span data-ttu-id="8f787-122">Wenn schließlich das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f787-122">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a><span data-ttu-id="8f787-124">Anmelden bei Ihrem Azure-Konto per Dienstprinzipal</span><span class="sxs-lookup"><span data-stu-id="8f787-124">Sign in to your Azure account by Service Principal</span></span>

<span data-ttu-id="8f787-125">In diesem Abschnitt erfahren Sie, wie Sie eine Datei mit Anmeldeinformationen erstellen, die Ihre Dienstprinzipaldaten enthält.</span><span class="sxs-lookup"><span data-stu-id="8f787-125">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="8f787-126">Danach verwendet Eclipse die Datei mit Anmeldeinformationen, um Sie beim Öffnen Ihres Projekts automatisch bei Azure anzumelden.</span><span class="sxs-lookup"><span data-stu-id="8f787-126">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure when open your project.</span></span>

1. <span data-ttu-id="8f787-127">Öffnen Sie das Projekt in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8f787-127">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="8f787-128">Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="8f787-128">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="8f787-129">![Der Eclipse-Befehl für Azure-Anmeldung][A01]</span><span class="sxs-lookup"><span data-stu-id="8f787-129">![The Eclipse Azure Sign In command][A01]</span></span>

3. <span data-ttu-id="8f787-130">Wählen Sie im Fenster für die Azure-Anmeldung \*\*\*\* die Option **Service Principal** (Dienstprinzipal) aus.</span><span class="sxs-lookup"><span data-stu-id="8f787-130">In the **Azure Sign In** window, select **Service Principal**.</span></span> <span data-ttu-id="8f787-131">Sollten Sie noch nicht über die Datei für die Dienstprinzipalauthentifizierung verfügen, klicken Sie auf **New** (Neu), um eine zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8f787-131">If you do not have the service principal authentication file yet, click **New** to create one.</span></span> <span data-ttu-id="8f787-132">Andernfalls können Sie auf **Browse** (Durchsuchen) klicken und direkt mit Schritt 8 fortfahren.</span><span class="sxs-lookup"><span data-stu-id="8f787-132">Otherwise you can click **Browse** to open it and jump to step 8.</span></span>

   ![Das Fenster für die Azure-Anmeldung mit ausgewählter Dienstprinzipaloption][A02]

4. <span data-ttu-id="8f787-134">Klicken Sie im Dialogfeld **Azure Device Login** (Azure-Geräteanmeldung) auf **Copy&Open** (Kopieren und öffnen).</span><span class="sxs-lookup"><span data-stu-id="8f787-134">Click **Copy&Open** in **Azure Device Login** dialog.</span></span>

   ![Dialogfeld für Azure-Anmeldung][A08]

> [!NOTE]
>
> <span data-ttu-id="8f787-136">Sollte der Browser nicht geöffnet werden, konfigurieren Sie Eclipse für die Verwendung eines externen Browsers wie Internet Explorer oder Chrome:</span><span class="sxs-lookup"><span data-stu-id="8f787-136">If the browser doesn't open, configure eclipse to use an external browser like IE or Chrome:</span></span>
>
> 1. <span data-ttu-id="8f787-137">Öffnen Sie „Preferences“ (Voreinstellungen) > „General“ (Allgemein) > „Web Browser“ (Webbrowser) > „Use external web browser in Eclipse“ (Externen Webbrowser in Eclipse verwenden).</span><span class="sxs-lookup"><span data-stu-id="8f787-137">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="8f787-138">Wählen Sie den gewünschten Browser aus.</span><span class="sxs-lookup"><span data-stu-id="8f787-138">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="8f787-139">Fügen Sie im Browser Ihren Gerätecode ein, den Sie im vorherigen Schritt durch Klicken auf **Copy&Open** (Kopieren und öffnen) kopiert haben, und klicken Sie anschließend auf **Next** (Weiter).</span><span class="sxs-lookup"><span data-stu-id="8f787-139">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Der Browser für die Geräteanmeldung][A03]

6. <span data-ttu-id="8f787-141">Wählen Sie im Dialogfeld **Create authentication files** (Authentifizierungsdateien erstellen) die gewünschten Abonnements und Ihr Zielverzeichnis aus, und klicken Sie dann auf **Start**.</span><span class="sxs-lookup"><span data-stu-id="8f787-141">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Fenster zum Erstellen der Authentifizierungsdateien][A04]

7. <span data-ttu-id="8f787-143">Klicken Sie im Dialogfeld **Service Principal Creation Status** (Dienstprinzipal-Erstellungsstatus) nach erfolgreicher Erstellung Ihrer Dateien auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f787-143">In the **Service Principal Creation Status** dialog box, click **OK** after your files have been created successfully.</span></span>

   ![Dialogfeld für den Status der Dienstprinzipalerstellung][A05]

8. <span data-ttu-id="8f787-145">Die Adresse der erstellten Datei wird im Fenster für die Azure-Anmeldung \*\*\*\* automatisch ausgefüllt. Klicken Sie als Nächstes auf **Sign in** (Anmelden).</span><span class="sxs-lookup"><span data-stu-id="8f787-145">Address of the created file will be automatically filled in the **Azure Sign In** window, now click **Sign in**.</span></span>

   ![Dialogfeld für Azure-Anmeldung][A06]

9. <span data-ttu-id="8f787-147">Wenn schließlich das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f787-147">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="sign-out-of-your-azure-account"></a><span data-ttu-id="8f787-149">Abmelden von Ihrem Azure-Abonnement</span><span class="sxs-lookup"><span data-stu-id="8f787-149">Sign out of your Azure account</span></span>

<span data-ttu-id="8f787-150">Nachdem Sie Ihr Konto mithilfe der obigen Schritte konfiguriert haben, werden Sie bei jedem Start von Eclipse automatisch angemeldet.</span><span class="sxs-lookup"><span data-stu-id="8f787-150">After you have configured your account by preceding steps, you will be automatically signed in each time you start Eclipse.</span></span> <span data-ttu-id="8f787-151">Mit den folgenden Schritten können Sie sich bei Bedarf von Ihrem Azure-Konto abmelden:</span><span class="sxs-lookup"><span data-stu-id="8f787-151">However, if you want to sign out of your Azure account, use the following steps.</span></span>

1. <span data-ttu-id="8f787-152">Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Abmelden**.</span><span class="sxs-lookup"><span data-stu-id="8f787-152">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Eclipse-Menü für die Abmeldung bei Azure][L01]

2. <span data-ttu-id="8f787-154">Wenn das Dialogfeld **Azure-Anmeldung** angezeigt wird, klicken Sie auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="8f787-154">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Dialogfeld zum Abmelden][L02]

## <a name="next-steps"></a><span data-ttu-id="8f787-156">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="8f787-156">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

[A01]: media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
