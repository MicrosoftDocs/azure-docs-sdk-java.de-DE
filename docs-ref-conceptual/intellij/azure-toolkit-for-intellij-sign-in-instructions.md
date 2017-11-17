---
title: "Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ"
description: "Erfahren Sie, wie Sie sich bei Microsoft Azure mit dem Azure-Toolkit für IntelliJ anmelden."
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
ms.openlocfilehash: 2daef282b5f0cfd0bd592e8dc1872012bddd1c65
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="20d00-103">Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="20d00-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="20d00-104">Das Azure-Toolkit für IntelliJ bietet zwei Methoden für die Anmeldung bei Ihrem Azure-Konto:</span><span class="sxs-lookup"><span data-stu-id="20d00-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="20d00-105">**Automatisiert:** Sie erstellen eine Datei mit Anmeldeinformationen, die Sie für die automatische Anmeldung beim Azure-Konto verwenden können.</span><span class="sxs-lookup"><span data-stu-id="20d00-105">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>
  * <span data-ttu-id="20d00-106">**Interaktiv:** Sie geben Ihre Azure-Anmeldeinformationen bei jeder Anmeldung beim Azure-Konto ein.</span><span class="sxs-lookup"><span data-stu-id="20d00-106">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>

<span data-ttu-id="20d00-107">In den folgenden Abschnitten wird die Verwendung der beiden Methoden beschrieben.</span><span class="sxs-lookup"><span data-stu-id="20d00-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="20d00-108">Automatisches Anmelden bei Ihrem Azure-Konto</span><span class="sxs-lookup"><span data-stu-id="20d00-108">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="20d00-109">In diesem Abschnitt erfahren Sie, wie Sie eine Datei mit Anmeldeinformationen erstellen, die Ihre Dienstprinzipaldaten enthält.</span><span class="sxs-lookup"><span data-stu-id="20d00-109">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="20d00-110">Nachdem Sie dieses Verfahren abgeschlossen haben, verwendet Eclipse die Datei mit Anmeldeinformationen, um Sie bei jedem Öffnen Ihres Projekts automatisch bei Azure anzumelden.</span><span class="sxs-lookup"><span data-stu-id="20d00-110">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="20d00-111">Öffnen Sie das Projekt in IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="20d00-111">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="20d00-112">Zeigen Sie im Menü **Tools** (Extras) auf **Azure**, und klicken Sie dann auf **Azure Sign In** (Azure-Anmeldung).</span><span class="sxs-lookup"><span data-stu-id="20d00-112">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ-Befehl für Azure-Anmeldung][A01]

1. <span data-ttu-id="20d00-114">Wählen Sie im Fenster **Azure Sign In** (Azure-Anmeldung) die Option **Automated** (Automatisiert) aus, und klicken Sie dann auf **New** (Neu).</span><span class="sxs-lookup"><span data-stu-id="20d00-114">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Fenster für die Azure Anmeldung mit „Automated“ ausgewählt][A02]

1. <span data-ttu-id="20d00-116">Geben Sie im Fenster **Azure Log In** (Azure-Anmeldung) Ihre Azure-Anmeldeinformationen ein, und klicken Sie dann auf **Sign in** (Anmelden).</span><span class="sxs-lookup"><span data-stu-id="20d00-116">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Dialogfeld für Azure-Anmeldung][A03]

1. <span data-ttu-id="20d00-118">Wählen Sie im Dialogfeld **Create authentication files** (Authentifizierungsdateien erstellen) die gewünschten Abonnements und Ihr Zielverzeichnis aus, und klicken Sie dann auf **Start**.</span><span class="sxs-lookup"><span data-stu-id="20d00-118">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Fenster zum Erstellen der Authentifizierungsdateien][A04]

1. <span data-ttu-id="20d00-120">Klicken Sie im Dialogfeld **Service Principal Creation Status** (Dienstprinzipal-Erstellungsstatus) nach dem Erstellen Ihrer Dateien auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="20d00-120">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Dialogfeld für den Status der Dienstprinzipalerstellung][A05]

1. <span data-ttu-id="20d00-122">Klicken Sie im Fenster **Azure Sign In** (Azure-Anmeldung) auf **Sign in** (Anmelden).</span><span class="sxs-lookup"><span data-stu-id="20d00-122">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Dialogfeld für Azure-Anmeldung][A06]

1. <span data-ttu-id="20d00-124">Wenn das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="20d00-124">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="20d00-126">Abmelden von Ihrem Azure-Konto nach automatischer Anmeldung</span><span class="sxs-lookup"><span data-stu-id="20d00-126">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="20d00-127">Nachdem Sie Ihr Konto über die zuvor angegebenen Schritte konfiguriert haben, werden Sie bei jedem Neustart von IntelliJ IDEA automatisch durch das Azure-Toolkit bei Ihrem Azure-Konto angemeldet.</span><span class="sxs-lookup"><span data-stu-id="20d00-127">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="20d00-128">Um sich jedoch von Ihrem Azure-Konto abzumelden und zu verhindern, dass das Azure-Toolkit Sie automatisch anmeldet, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="20d00-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="20d00-129">Klicken Sie in IntelliJ IDEA auf **Tools** (Extras), zeigen Sie auf **Azure**, und klicken Sie dann auf **Azure Sign Out** (Azure-Abmeldung).</span><span class="sxs-lookup"><span data-stu-id="20d00-129">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![IntelliJ-Befehl für Azure-Abmeldung][L01]

1. <span data-ttu-id="20d00-131">Klicken Sie im Bestätigungsfenster **Azure Sign Out** (Azure-Abmeldung) auf **Yes** (Ja).</span><span class="sxs-lookup"><span data-stu-id="20d00-131">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Bestätigungsfenster für Azure-Abmeldung][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="20d00-133">Automatisches Anmelden bei Ihrem Azure-Konto mithilfe einer vorhandenen Datei mit Anmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="20d00-133">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="20d00-134">Wenn Sie sich bei Verwendung von IntelliJ IDEA von Ihrem Azure-Konto abmelden, müssen Sie eine vorhandene Datei mit Anmeldeinformationen verwenden, um sich automatisch wieder bei dem Konto anzumelden.</span><span class="sxs-lookup"><span data-stu-id="20d00-134">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="20d00-135">Zum Konfigurieren des Azure-Toolkits für Eclipse, sodass eine vorhandene Datei mit Anmeldeinformationen verwendet werden, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="20d00-135">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="20d00-136">Öffnen Sie das Projekt in IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="20d00-136">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="20d00-137">Zeigen Sie im Menü **Tools** (Extras) auf **Azure**, und klicken Sie dann auf **Azure Sign In** (Azure-Anmeldung).</span><span class="sxs-lookup"><span data-stu-id="20d00-137">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ-Befehl für Azure-Anmeldung][A01]

1. <span data-ttu-id="20d00-139">Wählen Sie im Fenster **Azure Sign In** (Azure-Anmeldung) die Option **Automated** (Automatisiert) aus, und klicken Sie dann auf **Browse** (Durchsuchen).</span><span class="sxs-lookup"><span data-stu-id="20d00-139">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Fenster für die Azure Anmeldung mit „Automated“ ausgewählt][A02]

1. <span data-ttu-id="20d00-141">Wählen Sie im Dialogfeld **Select Authentication File** (Authentifizierungsdatei auswählen) eine zuvor erstellte Datei mit Anmeldeinformationen aus, und klicken Sie dann auf **Select** (Auswählen).</span><span class="sxs-lookup"><span data-stu-id="20d00-141">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Dialogfeld zum Auswählen einer Authentifizierungsdatei][A08]

1. <span data-ttu-id="20d00-143">Klicken Sie im Fenster **Azure Sign In** (Azure-Anmeldung) auf **Sign in** (Anmelden).</span><span class="sxs-lookup"><span data-stu-id="20d00-143">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Fenster für die Azure Anmeldung mit „Automated“ ausgewählt][A06]

1. <span data-ttu-id="20d00-145">Wenn das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="20d00-145">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="20d00-147">Interaktive Anmeldung bei Ihrem Azure-Konto</span><span class="sxs-lookup"><span data-stu-id="20d00-147">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="20d00-148">Gehen Sie folgendermaßen vor, um sich durch manuelles Eingeben Ihrer Azure-Anmeldeinformationen bei Azure anzumelden:</span><span class="sxs-lookup"><span data-stu-id="20d00-148">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="20d00-149">Öffnen Sie das Projekt in IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="20d00-149">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="20d00-150">Klicken Sie auf **Tools** (Extras), zeigen Sie auf **Azure**, und klicken Sie dann auf **Azure Sign In** (Azure-Anmeldung).</span><span class="sxs-lookup"><span data-stu-id="20d00-150">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ-Befehl für Azure-Anmeldung][I01]

1. <span data-ttu-id="20d00-152">Wählen Sie im Fenster **Azure Sign In** (Azure-Anmeldung) die Option **Interactive** (Interaktiv) aus, und klicken Sie dann auf **Sign in** (Anmelden).</span><span class="sxs-lookup"><span data-stu-id="20d00-152">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Fenster für die Azure Anmeldung mit „Interactive“ ausgewählt][I02]

1. <span data-ttu-id="20d00-154">Geben Sie im Dialogfeld **Azure Log In** (Azure-Anmeldung) Ihre Azure-Anmeldeinformationen ein, und klicken Sie dann auf **Sign in** (Anmelden).</span><span class="sxs-lookup"><span data-stu-id="20d00-154">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Dialogfeld für Azure-Anmeldung][I03]

1. <span data-ttu-id="20d00-156">Wenn das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="20d00-156">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="20d00-158">Abmelden von Ihrem Azure-Konto nach interaktiver Anmeldung</span><span class="sxs-lookup"><span data-stu-id="20d00-158">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="20d00-159">Nachdem Sie Ihr Konto über die zuvor angegebenen Schritte konfiguriert haben, werden Sie bei jedem Neustart von IntelliJ IDEA automatisch von Ihrem Azure-Konto abgemeldet.</span><span class="sxs-lookup"><span data-stu-id="20d00-159">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="20d00-160">Wenn Sie sich jedoch von Ihrem Azure-Konto abmelden möchten, *ohne* IntelliJ IDEA neu zu starten, gehen Sie folgendermaßen vor.</span><span class="sxs-lookup"><span data-stu-id="20d00-160">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="20d00-161">Klicken Sie in IntelliJ IDEA auf **Tools** (Extras), zeigen Sie auf **Azure**, und klicken Sie dann auf **Azure Sign Out** (Azure-Abmeldung).</span><span class="sxs-lookup"><span data-stu-id="20d00-161">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![IntelliJ-Befehl für Azure-Abmeldung][L01]

1. <span data-ttu-id="20d00-163">Klicken Sie im Bestätigungsfenster **Azure Sign Out** (Azure-Abmeldung) auf **Yes** (Ja).</span><span class="sxs-lookup"><span data-stu-id="20d00-163">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Bestätigungsfenster für Azure-Abmeldung][L02]

## <a name="next-steps"></a><span data-ttu-id="20d00-165">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="20d00-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
