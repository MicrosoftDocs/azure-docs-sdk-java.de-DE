---
title: Installieren des Azure-Toolkits für Eclipse
description: Hier erfahren Sie, wie Sie das Plug-In für das Azure-Toolkit für Eclipse installieren, um in Azure Cloudanwendungen zu erstellen und bereitzustellen.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 8e6630f7e019d950249e7e84024ac800a0f2f136
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270844"
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="c8f25-103">Installieren des Azure-Toolkits für Eclipse</span><span class="sxs-lookup"><span data-stu-id="c8f25-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="c8f25-104">Das Azure-Toolkit für Eclipse kann auf zwei Arten installiert werden:</span><span class="sxs-lookup"><span data-stu-id="c8f25-104">There are two ways to install Azure Toolkit for Eclipse:</span></span>

  - [<span data-ttu-id="c8f25-105">Eclipse-Marketplace</span><span class="sxs-lookup"><span data-stu-id="c8f25-105">Eclipse marketplace</span></span>](#eclipse-marketplace)
  - [<span data-ttu-id="c8f25-106">Installieren neuer Software</span><span class="sxs-lookup"><span data-stu-id="c8f25-106">Install new software</span></span>](#install-new-software)

> [!NOTE] 
> 
> <span data-ttu-id="c8f25-107">Das Azure Toolkit für Eclipse ist ein Open-Source-Projekt, dessen Quellcode unter der MIT-Lizenz auf der GitHub-Website des Projekts verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="c8f25-107">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

[!INCLUDE [azure-toolkit-for-eclipse-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="eclipse-marketplace"></a><span data-ttu-id="c8f25-108">Eclipse-Marketplace</span><span class="sxs-lookup"><span data-stu-id="c8f25-108">Eclipse marketplace</span></span>

1. <span data-ttu-id="c8f25-109">Ziehen Sie die folgende Schaltfläche in Ihren aktiven Eclipse-Arbeitsbereich.</span><span class="sxs-lookup"><span data-stu-id="c8f25-109">Drag the following button to your running Eclipse workspace.</span></span>

    <span data-ttu-id="c8f25-110">[![Ziehen Sie dieses Element in Ihren aktiven Eclipse*-Arbeitsbereich. *Eclipse Marketplace-Client erforderlich.](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Ziehen Sie dieses Element in Ihren aktiven Eclipse*-Arbeitsbereich. *Eclipse Marketplace-Client erforderlich.")</span><span class="sxs-lookup"><span data-stu-id="c8f25-110">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

2. <span data-ttu-id="c8f25-111">Sie können alternativ auch unter **Help > Eclipse Marketplace** (Hilfe >Eclipse Marketplace) nach dem Plug-In **Azure-Toolkit für Eclipse** suchen.</span><span class="sxs-lookup"><span data-stu-id="c8f25-111">Otherwise, it is also possible to search and install the **Azure Toolkit for Eclipse plugin** at **Help/Eclipse Marketplace**.</span></span>

    ![Marketplace](./media/azure-toolkit-for-eclipse-installation/marketplace.png)

## <a name="install-new-software"></a><span data-ttu-id="c8f25-113">Installieren neuer Software</span><span class="sxs-lookup"><span data-stu-id="c8f25-113">Install new software</span></span>

1. <span data-ttu-id="c8f25-114">Starten Sie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c8f25-114">Start Eclipse.</span></span>

1. <span data-ttu-id="c8f25-115">Klicken Sie auf das Menü **Help** (Hilfe) und dann auf **Install New Software** (Neue Software installieren), wie in der folgenden Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="c8f25-115">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>

   ![Installieren des Azure-Toolkits für Eclipse][01]

1. <span data-ttu-id="c8f25-117">Geben Sie im Dialogfeld **Available Software** (Verfügbare Software) im Textfeld **Work with** (Arbeiten mit) `http://dl.microsoft.com/eclipse/` ein, und drücken Sie dann die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="c8f25-117">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="c8f25-118">Aktivieren Sie im Fenster **Name** die Option **Azure Toolkit for Java**, und deaktivieren Sie **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu finden).</span><span class="sxs-lookup"><span data-stu-id="c8f25-118">In the **Name** pane, check **Azure Toolkit for Java**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="c8f25-119">Der Bildschirm sieht dann etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="c8f25-119">Your screen should appear similar to the following:</span></span>

   ![Installieren des Azure-Toolkits für Eclipse][02]

1. <span data-ttu-id="c8f25-121">Wenn Sie **Azure-Toolkit für Eclipse** erweitern, wird eine Liste der Komponenten angezeigt, die installiert werden. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c8f25-121">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="c8f25-122">Feature</span><span class="sxs-lookup"><span data-stu-id="c8f25-122">Feature</span></span> | <span data-ttu-id="c8f25-123">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c8f25-123">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="c8f25-124">**Application Insights Plugin for Java** (Application Insights-Plug-In für Java)</span><span class="sxs-lookup"><span data-stu-id="c8f25-124">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="c8f25-125">Ermöglicht Ihnen die Verwendung der Telemetriedatenprotokollierung und der Analysedienste von Azure für Ihre Anwendungen und Serverinstanzen.</span><span class="sxs-lookup"><span data-stu-id="c8f25-125">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="c8f25-126">**Azure Common Plugin** (Allgemeines Azure-Plug-In)</span><span class="sxs-lookup"><span data-stu-id="c8f25-126">**Azure Common Plugin**</span></span> | <span data-ttu-id="c8f25-127">Stellt die allgemeine Funktionalität bereit, die für andere Toolkit-Komponenten erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="c8f25-127">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="c8f25-128">**Azure Container Tools for Eclipse** (Azure-Containertools für Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c8f25-128">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="c8f25-129">Ermöglicht das Erstellen und Bereitstellen einer WAR-Datei als Docker-Container auf einem Docker-Computer.</span><span class="sxs-lookup"><span data-stu-id="c8f25-129">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="c8f25-130">**Azure Containers for Eclipse** (Azure-Container für Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c8f25-130">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="c8f25-131">Ermöglicht das Bereitstellen eines WAR- oder JAR-Artefakts als Docker-Container auf einem virtuellen Azure-Computer.</span><span class="sxs-lookup"><span data-stu-id="c8f25-131">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="c8f25-132">**Azure Explorer for Eclipse** (Azure Explorer für Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c8f25-132">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="c8f25-133">Bietet eine dem Explorer ähnliche Oberfläche zum Verwalten Ihrer Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="c8f25-133">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="c8f25-134">**Microsoft JDBC-Treiber 6.1 für SQL Server**</span><span class="sxs-lookup"><span data-stu-id="c8f25-134">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="c8f25-135">Stellt die JDBC-API für SQL Server und Microsoft Azure SQL-Datenbank für Java Platform Enterprise Edition 8 bereit.</span><span class="sxs-lookup"><span data-stu-id="c8f25-135">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="c8f25-136">**Package for Microsoft Azure Libraries for Java** (Paket für Microsoft Azure-Bibliotheken für Java)</span><span class="sxs-lookup"><span data-stu-id="c8f25-136">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="c8f25-137">Stellt APIs für den Zugriff auf Microsoft Azure-Dienste wie Storage, Service Bus, Service Runtime usw. bereit.</span><span class="sxs-lookup"><span data-stu-id="c8f25-137">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="c8f25-138">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="c8f25-138">Click **Next**.</span></span> <span data-ttu-id="c8f25-139">(Wenn ungewöhnliche Verzögerungen bei der Installation des Toolkits auftreten, achten Sie darauf, dass **Contact all update sites during install to find required software** deaktiviert ist.)</span><span class="sxs-lookup"><span data-stu-id="c8f25-139">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="c8f25-140">Klicken Sie im Dialogfeld **Install Details** (Installationsdetails) auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="c8f25-140">In the **Install Details** dialog, click **Next**.</span></span>

   ![Installationsdetails überprüfen][03]

1. <span data-ttu-id="c8f25-142">Überprüfen Sie im Dialogfeld **Review Licences** die Bedingungen der Lizenzverträge.</span><span class="sxs-lookup"><span data-stu-id="c8f25-142">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="c8f25-143">Wenn Sie dem Lizenzvertrag zustimmen, klicken Sie auf **I accept the terms of the license agreements** (Ich akzeptiere die Bedingungen der Lizenzvereinbarungen), und klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="c8f25-143">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="c8f25-144">(Bei den restlichen Schritten wird davon ausgegangen, dass Sie dem Lizenzvertrag zugestimmt haben.</span><span class="sxs-lookup"><span data-stu-id="c8f25-144">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="c8f25-145">Wenn Sie die Bedingungen der Lizenzverträge nicht akzeptieren, beenden Sie den Installationsprozess.)</span><span class="sxs-lookup"><span data-stu-id="c8f25-145">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>

   ![Review Licences][04]

   <span data-ttu-id="c8f25-147">Eclipse lädt die erforderlichen Pakete herunter und installiert diese.</span><span class="sxs-lookup"><span data-stu-id="c8f25-147">Eclipse will download and install the requisite packages.</span></span>

   ![Installationsstatus][05]

1. <span data-ttu-id="c8f25-149">Wenn Sie aufgefordert werden, Eclipse zum Abschließen der Installation neu zu starten, klicken Sie auf **Yes**(Ja).</span><span class="sxs-lookup"><span data-stu-id="c8f25-149">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>

   ![Aufforderung zum Neustarten][06]

## <a name="next-steps"></a><span data-ttu-id="c8f25-151">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c8f25-151">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->
[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
