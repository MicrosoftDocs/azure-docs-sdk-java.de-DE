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
ms.openlocfilehash: eb6099ab0c19bf3588cb7fd668f070771e58fe74
ms.sourcegitcommit: 8230cf6b15ac51a9f8a209e9b76411a0385029aa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2018
ms.locfileid: "34216024"
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="cfb36-103">Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse</span><span class="sxs-lookup"><span data-stu-id="cfb36-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="cfb36-104">Das Azure-Toolkit für Eclipse bietet zwei Methoden für die Anmeldung bei Ihrem Azure-Konto:</span><span class="sxs-lookup"><span data-stu-id="cfb36-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="cfb36-105">**Automatisch:** Für diese Methode erstellen Sie eine Datei mit Anmeldeinformationen, die Ihre Dienstprinzipaldaten enthält. Anschließend können Sie sich mithilfe dieser Datei automatisch bei Ihrem Azure-Konto anmelden.</span><span class="sxs-lookup"><span data-stu-id="cfb36-105">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>
  * <span data-ttu-id="cfb36-106">**Interaktiv:** Bei Auswahl dieser Methode geben Sie bei jeder Anmeldung bei Ihrem Azure-Konto Ihre Azure-Anmeldeinformationen ein.</span><span class="sxs-lookup"><span data-stu-id="cfb36-106">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>

<span data-ttu-id="cfb36-107">In den folgenden Abschnitten wird die Verwendung der beiden Methoden beschrieben.</span><span class="sxs-lookup"><span data-stu-id="cfb36-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="cfb36-108">Automatisches Anmelden bei Ihrem Azure-Konto und Erstellen einer Datei mit Anmeldeinformationen für die zukünftige Nutzung</span><span class="sxs-lookup"><span data-stu-id="cfb36-108">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="cfb36-109">Nachstehend werden die Schritte zum Erstellen einer Datei mit Anmeldeinformationen erläutert, die Ihre Dienstprinzipaldaten enthält.</span><span class="sxs-lookup"><span data-stu-id="cfb36-109">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="cfb36-110">Nachdem Sie diese Schritte abgeschlossen haben, verwendet Eclipse automatisch die Datei mit Anmeldeinformationen, damit Sie beim Öffnen Ihres Projekts automatisch bei Azure angemeldet werden.</span><span class="sxs-lookup"><span data-stu-id="cfb36-110">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="cfb36-111">Öffnen Sie das Projekt in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="cfb36-111">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="cfb36-112">Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-112">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse-Menü für die Anmeldung bei Azure][A01]

1. <span data-ttu-id="cfb36-114">Wählen Sie im angezeigten Dialogfeld **Azure-Anmeldung** die Option **Automatisiert** aus, und klicken Sie dann auf **Neu**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-114">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Anmeldedialogfeld][A02]

1. <span data-ttu-id="cfb36-116">Wenn das Dialogfeld **Azure Log In** angezeigt wird, geben Sie Ihre Azure-Anmeldeinformationen ein, und klicken Sie dann auf **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-116">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Dialogfeld für Azure-Anmeldung][A03]

1. <span data-ttu-id="cfb36-118">Wenn das Dialogfeld **Create authentication files** angezeigt wird, wählen Sie die gewünschten Abonnements aus. Wählen Sie Ihr Zielverzeichnis, und klicken Sie dann auf **Start**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-118">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Dialogfeld für Azure-Anmeldung][A04]

1. <span data-ttu-id="cfb36-120">Das Dialogfeld **Dienstprinzipal-Erstellungsstatus** wird angezeigt. Nachdem Ihre Dateien erstellt wurden, klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-120">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Dialogfeld mit dem Status der Dienstprinzipalerstellung][A05]

1. <span data-ttu-id="cfb36-122">Wenn das Dialogfeld **Azure-Anmeldung** angezeigt wird, klicken Sie auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-122">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Dialogfeld für Azure-Anmeldung][A06]

1. <span data-ttu-id="cfb36-124">Wenn das Dialogfeld **Select Subscriptions** angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-124">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="cfb36-126">Automatisches Abmelden von Ihrem Azure-Konto bei zuvor erfolgter automatischer Anmeldung</span><span class="sxs-lookup"><span data-stu-id="cfb36-126">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="cfb36-127">Nachdem Sie die Schritte im vorherigen Abschnitt konfiguriert haben, meldet das Azure-Toolkit Sie bei jedem Neustart von Eclipse automatisch bei Ihrem Azure-Konto an.</span><span class="sxs-lookup"><span data-stu-id="cfb36-127">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="cfb36-128">Um sich jedoch von Ihrem Azure-Konto abzumelden und zu verhindern, dass das Azure-Toolkit Sie automatisch anmeldet, führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="cfb36-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="cfb36-129">Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Abmelden**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-129">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Eclipse-Menü für die Abmeldung bei Azure][L01]

1. <span data-ttu-id="cfb36-131">Wenn das Dialogfeld **Azure-Anmeldung** angezeigt wird, klicken Sie auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-131">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Dialogfeld zum Abmelden][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="cfb36-133">Automatisches Anmelden bei Ihrem Azure-Konto mithilfe einer bereits erstellten Datei mit Anmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="cfb36-133">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="cfb36-134">Wenn Sie sich bei Verwendung von Eclipse von Azure abmelden, müssen Sie das Azure-Toolkit für Eclipse so neu konfigurieren, dass eine zuvor erstellte Datei mit Anmeldeinformationen verwendet wird, bevor Sie sich automatisch bei Ihrem Azure-Konto anmelden können.</span><span class="sxs-lookup"><span data-stu-id="cfb36-134">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="cfb36-135">Die folgenden Schritte begleiten Sie durch die Konfiguration des Azure-Toolkits, damit eine vorhandene Datei mit Anmeldeinformationen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cfb36-135">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="cfb36-136">Öffnen Sie das Projekt in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="cfb36-136">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="cfb36-137">Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-137">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse-Menü für die Anmeldung bei Azure][A01]

1. <span data-ttu-id="cfb36-139">Wählen Sie im angezeigten Dialogfeld **Azure-Anmeldung** die Option **Automatisiert** aus, und klicken Sie dann auf **Durchsuchen**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-139">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Anmeldedialogfeld][A02]

1. <span data-ttu-id="cfb36-141">Wenn das Dialogfeld **Authentifizierungsdatei auswählen** angezeigt wird, wählen Sie eine zuvor erstellte Datei mit Anmeldeinformationen aus, und klicken Sie dann auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-141">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Open**.</span></span>

   ![Anmeldedialogfeld][A08]

1. <span data-ttu-id="cfb36-143">Wenn das Dialogfeld **Azure Sign In** angezeigt wird, klicken Sie auf **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-143">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Dialogfeld für Azure-Anmeldung][A06]

1. <span data-ttu-id="cfb36-145">Wenn das Dialogfeld **Select Subscriptions** angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-145">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="cfb36-147">Interaktive Anmeldung bei Ihrem Azure-Konto</span><span class="sxs-lookup"><span data-stu-id="cfb36-147">Signing into your Azure account interactively</span></span>

<span data-ttu-id="cfb36-148">Nachstehend wird erläutert, wie Sie sich bei Azure durch manuelles Eingeben Ihrer Azure-Anmeldeinformationen anmelden.</span><span class="sxs-lookup"><span data-stu-id="cfb36-148">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="cfb36-149">Öffnen Sie das Projekt in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="cfb36-149">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="cfb36-150">Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-150">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse-Menü für die Anmeldung bei Azure][I01]

1. <span data-ttu-id="cfb36-152">Wählen Sie im angezeigten Dialogfeld **Azure-Anmeldung** die Option **Interaktiv** aus, und klicken Sie dann auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-152">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Anmeldedialogfeld][I02]

1. <span data-ttu-id="cfb36-154">Wenn das Dialogfeld **Azure Log In** angezeigt wird, geben Sie Ihre Azure-Anmeldeinformationen ein, und klicken Sie dann auf **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-154">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Dialogfeld „Azure-Anmeldung“][I03]

1. <span data-ttu-id="cfb36-156">Wenn das Dialogfeld **Select Subscriptions** angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-156">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialogfeld „Abonnements auswählen“][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="cfb36-158">Abmelden von Ihrem Azure-Konto bei zuvor erfolgter interaktiver Anmeldung</span><span class="sxs-lookup"><span data-stu-id="cfb36-158">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="cfb36-159">Nachdem Sie die Schritte im vorherigen Abschnitt konfiguriert haben, werden Sie bei jedem Neustart von Eclipse automatisch von Ihrem Azure-Konto abgemeldet.</span><span class="sxs-lookup"><span data-stu-id="cfb36-159">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="cfb36-160">Wenn Sie sich jedoch von Ihrem Azure-Konto abmelden möchten, ohne Eclipse neu zu starten, führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="cfb36-160">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="cfb36-161">Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Abmelden**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-161">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Eclipse-Menü für die Abmeldung bei Azure][L01]

1. <span data-ttu-id="cfb36-163">Wenn das Dialogfeld **Azure-Anmeldung** angezeigt wird, klicken Sie auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="cfb36-163">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Dialogfeld zum Abmelden][L02]

## <a name="next-steps"></a><span data-ttu-id="cfb36-165">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="cfb36-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

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
