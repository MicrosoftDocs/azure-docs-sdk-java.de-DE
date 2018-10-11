---
title: Installieren des Azure-Toolkits für IntelliJ
description: Hier erfahren Sie, wie Sie das Plug-In für das Azure-Toolkit für IntelliJ installieren, um in Azure Cloudanwendungen zu erstellen und bereitzustellen.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 0f3df5c8cf3c83c1ce9a4ca32c753b5fc39ab1df
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892881"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="29727-103">Installieren des Azure-Toolkits für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="29727-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="29727-104">Das Azure-Toolkit für IntelliJ stellt Vorlagen und Funktionen bereit, die Ihnen das einfache Erstellen, Entwickeln, Testen und Bereitstellen von Cloudanwendungen in Azure mithilfe der IntelliJ IDEA-Entwicklungsumgebung ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="29727-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="29727-105">Das Azure-Toolkit für IntelliJ ist ein Open-Source-Projekt, dessen Quellcode unter der MIT-Lizenz auf der GitHub-Website des Projekts verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="29727-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="29727-106">Es gibt zwei Methoden zum Installieren des Azure-Toolkits für IntelliJ: über das Dialogfeld **Einstellungen** und über das Menü **Konfigurieren** auf dem Startbildschirm.</span><span class="sxs-lookup"><span data-stu-id="29727-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="29727-107">Beide Installationsmethoden werden in den folgenden Schritten veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="29727-107">Both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="29727-108">So installieren Sie das Azure-Toolkit für IntelliJ über das Dialogfeld „Einstellungen“</span><span class="sxs-lookup"><span data-stu-id="29727-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="29727-109">Starten Sie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="29727-109">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="29727-110">Wenn IntelliJ IDEA geöffnet wird, klicken Sie auf **File** (Datei), klicken Sie dann auf **Settings** (Einstellungen).</span><span class="sxs-lookup"><span data-stu-id="29727-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Das Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA öffnen][01a]

1. <span data-ttu-id="29727-112">Klicken Sie im Dialogfeld „Settings“ (Einstellungen) auf **Plugins**, und klicken Sie dann auf **Browse Repositories** (Repositorys durchsuchen).</span><span class="sxs-lookup"><span data-stu-id="29727-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA][02a]

1. <span data-ttu-id="29727-114">Geben Sie im Dialogfeld **Browse Repositories** (Repositorys durchsuchen) in das Suchfeld „Azure“ ein.</span><span class="sxs-lookup"><span data-stu-id="29727-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="29727-115">Markieren Sie **Azure Toolkit for IntelliJ** (Azure Toolkit für IntelliJ), und klicken Sie dann auf **Install** (Installieren).</span><span class="sxs-lookup"><span data-stu-id="29727-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Suchen nach dem Azure-Toolkit für IntelliJ][03]
   
   <span data-ttu-id="29727-117">IntelliJ IDEA zeigt den Installationsstatus in einem Dialogfeld an.</span><span class="sxs-lookup"><span data-stu-id="29727-117">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Installationsstatus][04]

1. <span data-ttu-id="29727-119">Klicken Sie nach Abschluss der Installation auf **Restart IntelliJ IDEA**(IntelliJ IDEA neu starten).</span><span class="sxs-lookup"><span data-stu-id="29727-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="29727-121">Klicken Sie auf **OK** , um das Dialogfeld „Settings“ (Einstellungen) zu schließen.</span><span class="sxs-lookup"><span data-stu-id="29727-121">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Das Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA schließen][06]

1. <span data-ttu-id="29727-123">Wenn Sie gefragt werden, ob Sie IntelliJ IDEA neu starten oder den Neustart später durchführen möchten, klicken Sie auf **Restart**(Neu starten).</span><span class="sxs-lookup"><span data-stu-id="29727-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="29727-124">1</span><span class="sxs-lookup"><span data-stu-id="29727-124">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="29727-126">So installieren Sie das Azure-Toolkit für IntelliJ über den Startbildschirm</span><span class="sxs-lookup"><span data-stu-id="29727-126">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="29727-127">Starten Sie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="29727-127">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="29727-128">Wenn der Startbildschirm von IntelliJ IDEA angezeigt wird, klicken Sie auf **Configure** (Konfigurieren), und klicken Sie dann auf **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="29727-128">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![IntelliJ IDEA-Plug-Ins installieren][01b]

1. <span data-ttu-id="29727-130">Klicken Sie im Dialogfeld **Plugins** auf **Browse Repositories** (Repositorys durchsuchen).</span><span class="sxs-lookup"><span data-stu-id="29727-130">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Die Plug-In-Repositorys von IntelliJ IDEA durchsuchen][02b]

1. <span data-ttu-id="29727-132">Geben Sie im Dialogfeld **Browse Repositories** (Repositorys durchsuchen) in das Suchfeld „Azure“ ein.</span><span class="sxs-lookup"><span data-stu-id="29727-132">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="29727-133">Markieren Sie **Azure Toolkit for IntelliJ** (Azure Toolkit für IntelliJ), und klicken Sie dann auf **Install** (Installieren).</span><span class="sxs-lookup"><span data-stu-id="29727-133">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Suchen nach dem Azure-Toolkit für IntelliJ][03]
   
   <span data-ttu-id="29727-135">IntelliJ IDEA zeigt den Installationsstatus in einem Dialogfeld an.</span><span class="sxs-lookup"><span data-stu-id="29727-135">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Installationsstatus][04]

1. <span data-ttu-id="29727-137">Klicken Sie nach Abschluss der Installation auf **Restart IntelliJ IDEA**(IntelliJ IDEA neu starten).</span><span class="sxs-lookup"><span data-stu-id="29727-137">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="29727-139">Wenn Sie gefragt werden, ob Sie IntelliJ IDEA neu starten oder den Neustart später durchführen möchten, klicken Sie auf **Restart**(Neu starten).</span><span class="sxs-lookup"><span data-stu-id="29727-139">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="29727-141">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="29727-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[01a]: media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
