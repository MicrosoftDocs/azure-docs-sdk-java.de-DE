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
ms.openlocfilehash: d5f685fa62ad74c8b8cd842b3667f8161e7c5760
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893005"
---
# <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="c40c3-103">Installieren des Azure-Toolkits für Eclipse</span><span class="sxs-lookup"><span data-stu-id="c40c3-103">Install the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="c40c3-104">Das Azure-Toolkit für Eclipse stellt Vorlagen und Funktionen bereit, die Ihnen das einfache Erstellen, Entwickeln, Testen und Bereitstellen von Cloudanwendungen in Azure mithilfe der Eclipse-Entwicklungsumgebung ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="c40c3-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy cloud applications to Azure from the Eclipse development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c40c3-105">Das Azure Toolkit für Eclipse ist ein Open-Source-Projekt, dessen Quellcode unter der MIT-Lizenz auf der GitHub-Website des Projekts verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="c40c3-105">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="c40c3-106">Die folgenden Schritte veranschaulichen die Installation des Azure-Toolkits für Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c40c3-106">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="c40c3-107">So installieren Sie das Azure-Toolkit für Eclipse</span><span class="sxs-lookup"><span data-stu-id="c40c3-107">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="c40c3-108">Starten Sie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c40c3-108">Start Eclipse.</span></span>

1. <span data-ttu-id="c40c3-109">Klicken Sie auf das Menü **Help** (Hilfe) und dann auf **Install New Software** (Neue Software installieren), wie in der folgenden Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="c40c3-109">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Installieren des Azure-Toolkits für Eclipse][01]

1. <span data-ttu-id="c40c3-111">Geben Sie im Dialogfeld **Available Software** (Verfügbare Software) im Textfeld **Work with** (Arbeiten mit) `http://dl.microsoft.com/eclipse/` ein, und drücken Sie dann die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="c40c3-111">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="c40c3-112">Aktivieren Sie im Fenster **Name** die Option **Azure Toolkit for Java**, und deaktivieren Sie **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu finden).</span><span class="sxs-lookup"><span data-stu-id="c40c3-112">In the **Name** pane, check **Azure Toolkit for Java**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="c40c3-113">Der Bildschirm sieht dann etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="c40c3-113">Your screen should appear similar to the following:</span></span>
   
   ![Installieren des Azure-Toolkits für Eclipse][02]

1. <span data-ttu-id="c40c3-115">Wenn Sie **Azure-Toolkit für Eclipse** erweitern, wird eine Liste der Komponenten angezeigt, die installiert werden. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c40c3-115">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="c40c3-116">Feature</span><span class="sxs-lookup"><span data-stu-id="c40c3-116">Feature</span></span> | <span data-ttu-id="c40c3-117">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c40c3-117">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="c40c3-118">**Application Insights Plugin for Java** (Application Insights-Plug-In für Java)</span><span class="sxs-lookup"><span data-stu-id="c40c3-118">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="c40c3-119">Ermöglicht Ihnen die Verwendung der Telemetriedatenprotokollierung und der Analysedienste von Azure für Ihre Anwendungen und Serverinstanzen.</span><span class="sxs-lookup"><span data-stu-id="c40c3-119">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="c40c3-120">**Azure Common Plugin** (Allgemeines Azure-Plug-In)</span><span class="sxs-lookup"><span data-stu-id="c40c3-120">**Azure Common Plugin**</span></span> | <span data-ttu-id="c40c3-121">Stellt die allgemeine Funktionalität bereit, die für andere Toolkit-Komponenten erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="c40c3-121">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="c40c3-122">**Azure Container Tools for Eclipse** (Azure-Containertools für Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c40c3-122">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="c40c3-123">Ermöglicht das Erstellen und Bereitstellen einer WAR-Datei als Docker-Container auf einem Docker-Computer.</span><span class="sxs-lookup"><span data-stu-id="c40c3-123">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="c40c3-124">**Azure Containers for Eclipse** (Azure-Container für Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c40c3-124">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="c40c3-125">Ermöglicht das Bereitstellen eines WAR- oder JAR-Artefakts als Docker-Container auf einem virtuellen Azure-Computer.</span><span class="sxs-lookup"><span data-stu-id="c40c3-125">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="c40c3-126">**Azure Explorer for Eclipse** (Azure Explorer für Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c40c3-126">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="c40c3-127">Bietet eine dem Explorer ähnliche Oberfläche zum Verwalten Ihrer Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="c40c3-127">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="c40c3-128">**Microsoft JDBC-Treiber 6.1 für SQL Server**</span><span class="sxs-lookup"><span data-stu-id="c40c3-128">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="c40c3-129">Stellt die JDBC-API für SQL Server und Microsoft Azure SQL-Datenbank für Java Platform Enterprise Edition 8 bereit.</span><span class="sxs-lookup"><span data-stu-id="c40c3-129">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="c40c3-130">**Package for Microsoft Azure Libraries for Java** (Paket für Microsoft Azure-Bibliotheken für Java)</span><span class="sxs-lookup"><span data-stu-id="c40c3-130">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="c40c3-131">Stellt APIs für den Zugriff auf Microsoft Azure-Dienste wie Storage, Service Bus, Service Runtime usw. bereit.</span><span class="sxs-lookup"><span data-stu-id="c40c3-131">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="c40c3-132">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="c40c3-132">Click **Next**.</span></span> <span data-ttu-id="c40c3-133">(Wenn ungewöhnliche Verzögerungen bei der Installation des Toolkits auftreten, achten Sie darauf, dass **Contact all update sites during install to find required software** deaktiviert ist.)</span><span class="sxs-lookup"><span data-stu-id="c40c3-133">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="c40c3-134">Klicken Sie im Dialogfeld **Install Details** (Installationsdetails) auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="c40c3-134">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Installationsdetails überprüfen][03]

1. <span data-ttu-id="c40c3-136">Überprüfen Sie im Dialogfeld **Review Licences** die Bedingungen der Lizenzverträge.</span><span class="sxs-lookup"><span data-stu-id="c40c3-136">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="c40c3-137">Wenn Sie dem Lizenzvertrag zustimmen, klicken Sie auf **I accept the terms of the license agreements** (Ich akzeptiere die Bedingungen der Lizenzvereinbarungen), und klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="c40c3-137">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="c40c3-138">(Bei den restlichen Schritten wird davon ausgegangen, dass Sie dem Lizenzvertrag zugestimmt haben.</span><span class="sxs-lookup"><span data-stu-id="c40c3-138">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="c40c3-139">Wenn Sie die Bedingungen der Lizenzverträge nicht akzeptieren, beenden Sie den Installationsprozess.)</span><span class="sxs-lookup"><span data-stu-id="c40c3-139">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Review Licences][04]
   
   <span data-ttu-id="c40c3-141">Eclipse lädt die erforderlichen Pakete herunter und installiert diese.</span><span class="sxs-lookup"><span data-stu-id="c40c3-141">Eclipse will download and install the requisite packages.</span></span>
   
   ![Installationsstatus][05]

1. <span data-ttu-id="c40c3-143">Wenn Sie aufgefordert werden, Eclipse zum Abschließen der Installation neu zu starten, klicken Sie auf **Yes**(Ja).</span><span class="sxs-lookup"><span data-stu-id="c40c3-143">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Aufforderung zum Neustarten][06]

## <a name="next-steps"></a><span data-ttu-id="c40c3-145">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c40c3-145">Next steps</span></span>

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
