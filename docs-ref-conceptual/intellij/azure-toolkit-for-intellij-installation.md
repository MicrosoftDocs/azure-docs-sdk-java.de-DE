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
ms.openlocfilehash: 86cef07873ae7a2ba75aab1044fe4d241cd5b13e
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270870"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="be3d3-103">Installieren des Azure-Toolkits für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="be3d3-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="be3d3-104">Das Azure-Toolkit für IntelliJ stellt Vorlagen und Funktionen bereit, die Ihnen das einfache Erstellen, Entwickeln, Testen und Bereitstellen von Cloudanwendungen in Azure mithilfe der IntelliJ IDEA-Entwicklungsumgebung ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="be3d3-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="be3d3-105">Das Azure-Toolkit für IntelliJ ist ein Open-Source-Projekt, dessen Quellcode unter der MIT-Lizenz auf der GitHub-Website des Projekts verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="be3d3-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="be3d3-106">Es gibt zwei Methoden zum Installieren des Azure-Toolkits für IntelliJ: über das Dialogfeld **Einstellungen** und über das Menü **Konfigurieren** auf dem Startbildschirm.</span><span class="sxs-lookup"><span data-stu-id="be3d3-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="be3d3-107">Beide Installationsmethoden werden in den folgenden Schritten veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="be3d3-107">Both installation methods will be demonstrated in the following steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be3d3-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="be3d3-108">Prerequisites</span></span>

<span data-ttu-id="be3d3-109">Für das Azure-Toolkit für IntelliJ sind folgende Softwarekomponenten erforderlich:</span><span class="sxs-lookup"><span data-stu-id="be3d3-109">The Azure Toolkit for IntelliJ requires to the following software components:</span></span>

* <span data-ttu-id="be3d3-110">Ein installiertes Java Development Kit (JDK) ab Version 8, beispielsweise: [OpenJDK](https://openjdk.java.net/) oder [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="be3d3-110">An Java Development Kit (JDK) 8+ installed, for example: [OpenJDK](https://openjdk.java.net/) or [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span></span>
* <span data-ttu-id="be3d3-111">Eine installierte Instanz von [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) (Ultimate Edition oder Community Edition)</span><span class="sxs-lookup"><span data-stu-id="be3d3-111">An [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition or Community Edition installed</span></span>

> [!NOTE]
> 
> <span data-ttu-id="be3d3-112">Auf der Seite [Azure-Toolkit für IntelliJ](https://plugins.jetbrains.com/plugin/8053) im Repository für JetBrains-Plug-Ins sind die mit dem Toolkit kompatiblen Builds aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="be3d3-112">The [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) page at the JetBrains Plugin Repository lists the builds that are compatible with the toolkit.</span></span>
> 

<!--
> [!IMPORTANT]
> 
> If you are using the Azure Toolkit for IntelliJ on Windows, the toolkit requires installing the Azure SDK 2.9.6 or later in order to use the Azure emulator. You have two options for installing the Azure SDK:
> 
> * You can download and install the Azure SDK by using the [Web Platform Installer (WebPI)](http://go.microsoft.com/fwlink/?LinkID=252838).
> * If you do not have the Azure SDK installed when you create your first Azure deployment project, you will be prompted to automatically download install the requisite version of the Azure SDK.
> 
> Note that the Azure SDK is only required on Windows.
> 
-->


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="be3d3-113">So installieren Sie das Azure-Toolkit für IntelliJ über das Dialogfeld „Einstellungen“</span><span class="sxs-lookup"><span data-stu-id="be3d3-113">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="be3d3-114">Starten Sie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="be3d3-114">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="be3d3-115">Wenn IntelliJ IDEA geöffnet wird, klicken Sie auf **File** (Datei), klicken Sie dann auf **Settings** (Einstellungen).</span><span class="sxs-lookup"><span data-stu-id="be3d3-115">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Das Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA öffnen][01a]

1. <span data-ttu-id="be3d3-117">Klicken Sie im Dialogfeld „Settings“ (Einstellungen) auf **Plugins**, und klicken Sie dann auf **Browse Repositories** (Repositorys durchsuchen).</span><span class="sxs-lookup"><span data-stu-id="be3d3-117">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA][02a]

1. <span data-ttu-id="be3d3-119">Geben Sie im Dialogfeld **Browse Repositories** (Repositorys durchsuchen) in das Suchfeld „Azure“ ein.</span><span class="sxs-lookup"><span data-stu-id="be3d3-119">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="be3d3-120">Markieren Sie **Azure Toolkit for IntelliJ** (Azure Toolkit für IntelliJ), und klicken Sie dann auf **Install** (Installieren).</span><span class="sxs-lookup"><span data-stu-id="be3d3-120">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Suchen nach dem Azure-Toolkit für IntelliJ][03]
   
   <span data-ttu-id="be3d3-122">IntelliJ IDEA zeigt den Installationsstatus in einem Dialogfeld an.</span><span class="sxs-lookup"><span data-stu-id="be3d3-122">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Installationsstatus][04]

1. <span data-ttu-id="be3d3-124">Klicken Sie nach Abschluss der Installation auf **Restart IntelliJ IDEA**(IntelliJ IDEA neu starten).</span><span class="sxs-lookup"><span data-stu-id="be3d3-124">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="be3d3-126">Klicken Sie auf **OK** , um das Dialogfeld „Settings“ (Einstellungen) zu schließen.</span><span class="sxs-lookup"><span data-stu-id="be3d3-126">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Das Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA schließen][06]

1. <span data-ttu-id="be3d3-128">Wenn Sie gefragt werden, ob Sie IntelliJ IDEA neu starten oder den Neustart später durchführen möchten, klicken Sie auf **Restart**(Neu starten).</span><span class="sxs-lookup"><span data-stu-id="be3d3-128">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="be3d3-129">1</span><span class="sxs-lookup"><span data-stu-id="be3d3-129">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="be3d3-131">So installieren Sie das Azure-Toolkit für IntelliJ über den Startbildschirm</span><span class="sxs-lookup"><span data-stu-id="be3d3-131">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="be3d3-132">Starten Sie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="be3d3-132">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="be3d3-133">Wenn der Startbildschirm von IntelliJ IDEA angezeigt wird, klicken Sie auf **Configure** (Konfigurieren), und klicken Sie dann auf **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="be3d3-133">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![IntelliJ IDEA-Plug-Ins installieren][01b]

1. <span data-ttu-id="be3d3-135">Klicken Sie im Dialogfeld **Plugins** auf **Browse Repositories** (Repositorys durchsuchen).</span><span class="sxs-lookup"><span data-stu-id="be3d3-135">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Die Plug-In-Repositorys von IntelliJ IDEA durchsuchen][02b]

1. <span data-ttu-id="be3d3-137">Geben Sie im Dialogfeld **Browse Repositories** (Repositorys durchsuchen) in das Suchfeld „Azure“ ein.</span><span class="sxs-lookup"><span data-stu-id="be3d3-137">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="be3d3-138">Markieren Sie **Azure Toolkit for IntelliJ** (Azure Toolkit für IntelliJ), und klicken Sie dann auf **Install** (Installieren).</span><span class="sxs-lookup"><span data-stu-id="be3d3-138">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Suchen nach dem Azure-Toolkit für IntelliJ][03]
   
   <span data-ttu-id="be3d3-140">IntelliJ IDEA zeigt den Installationsstatus in einem Dialogfeld an.</span><span class="sxs-lookup"><span data-stu-id="be3d3-140">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Installationsstatus][04]

1. <span data-ttu-id="be3d3-142">Klicken Sie nach Abschluss der Installation auf **Restart IntelliJ IDEA**(IntelliJ IDEA neu starten).</span><span class="sxs-lookup"><span data-stu-id="be3d3-142">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="be3d3-144">Wenn Sie gefragt werden, ob Sie IntelliJ IDEA neu starten oder den Neustart später durchführen möchten, klicken Sie auf **Restart**(Neu starten).</span><span class="sxs-lookup"><span data-stu-id="be3d3-144">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="be3d3-146">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="be3d3-146">Next steps</span></span>

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
