---
title: "Installieren des Azure-Toolkits für Eclipse"
description: "Erfahren Sie, wie Sie das Azure Toolkit für Eclipse installieren."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 59a8bfb6ab4db8ea8c6c9025ca3ced8a13192628
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="27b69-103">Installieren des Azure-Toolkits für Eclipse</span><span class="sxs-lookup"><span data-stu-id="27b69-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="27b69-104">Das Azure Toolkit für Eclipse stellt Vorlagen und Funktionen bereit, die Ihnen das einfache Erstellen, Entwickeln, Testen und Bereitstellen von Azure-Anwendungen mithilfe der Eclipse-Entwicklungsumgebung ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="27b69-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="27b69-105">Das Azure Toolkit für Eclipse ist ein Open-Source-Projekt.</span><span class="sxs-lookup"><span data-stu-id="27b69-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="27b69-106">Der Quellcode ist verfügbar unter der MIT-Lizenz unter <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="27b69-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="27b69-107">Die folgenden Schritte veranschaulichen die Installation des Azure-Toolkits für Eclipse.</span><span class="sxs-lookup"><span data-stu-id="27b69-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="27b69-108">So installieren Sie das Azure-Toolkit für Eclipse</span><span class="sxs-lookup"><span data-stu-id="27b69-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="27b69-109">Starten Sie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="27b69-109">Start Eclipse.</span></span>

1. <span data-ttu-id="27b69-110">Klicken Sie auf das Menü **Help** (Hilfe) und dann auf **Install New Software** (Neue Software installieren), wie in der folgenden Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="27b69-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Installieren des Azure-Toolkits für Eclipse][01]

1. <span data-ttu-id="27b69-112">Geben Sie im Dialogfeld **Available Software** (Verfügbare Software) im Textfeld **Work with** (Arbeiten mit) `http://dl.microsoft.com/eclipse/` ein, und drücken Sie dann die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="27b69-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="27b69-113">Aktivieren Sie im Fenster **Name** die Option **Azure Toolkit for Eclipse**, und deaktivieren Sie **Contact all update sites during install to find required software**.</span><span class="sxs-lookup"><span data-stu-id="27b69-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="27b69-114">Der Bildschirm sieht dann etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="27b69-114">Your screen should appear similar to the following:</span></span>
   
   ![Installieren des Azure-Toolkits für Eclipse][02]

1. <span data-ttu-id="27b69-116">Nach dem Erweitern von **Azure Toolkit for Eclipse**(Azure Toolkit für Eclipse) wird eine Liste mit Elementen wie im folgenden Beispiel angezeigt:</span><span class="sxs-lookup"><span data-stu-id="27b69-116">If you expand the **Azure Toolkit for Eclipse**, you will see a list of items like following example:</span></span>
   
   * <span data-ttu-id="27b69-117">**Application Insights-Plug-In for Java:**Diese Komponente ermöglicht Ihnen die Verwendung der Telemetriedatenprotokollierung und der Analysedienste von Azure für Ihre Anwendungen und Server-Instanzen.</span><span class="sxs-lookup"><span data-stu-id="27b69-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="27b69-118">**Azure Access Control Services Filter:**Diese Komponente bietet Unterstützung für die Authentifizierung von Anwendungsbenutzern mit Azure ACS, sodass Szenarios mit einmaligem Anmelden ermöglicht werden und die Identitätslogik aus der Anwendung externalisiert wird.</span><span class="sxs-lookup"><span data-stu-id="27b69-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="27b69-119">**Azure Common Plugin (Allgemeines Azure-Plug-In):**Diese Komponente stellt die allgemeine Funktionalität bereit, die für andere Toolkit-Komponenten erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="27b69-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="27b69-120">**Azure Explorer for Eclipse (Azure-Explorer für Eclipse):**Diese Komponente stellt die allgemeine Funktionalität bereit, die für andere Toolkit-Komponenten erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="27b69-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="27b69-121">**Azure Plugin for Eclipse with Java (Azure-Plug-In für Eclipse mit Java):**Diese Komponente bietet Unterstützung für die Entwicklung von Projekten, mit deren Hilfe Java-Anwendungen für die Microsoft Azure-Cloud in Eclipse und über die Befehlszeile erstellt, getestet und bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="27b69-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="27b69-122">**Azure Web Apps Plugin with Java (Azure Web Apps-Plug-In mit Java):**Diese Komponente bietet Unterstützung für die Bereitstellung von Java-Webanwendungen in Microsoft Azure-Web-App-Containern.</span><span class="sxs-lookup"><span data-stu-id="27b69-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="27b69-123">**Microsoft JDBC Driver 4.2 for SQL Server (Microsoft JDBC-Treiber 4.2 für SQL Server):**Diese Komponente stellt die JDBC-API für SQL Server und Microsoft Azure SQL-Datenbank für die Java Platform Enterprise Edition 8 bereit.</span><span class="sxs-lookup"><span data-stu-id="27b69-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="27b69-124">**Package for Apache Qpid Client Libraries for JMS (Paket für Apache Qpid-Clientbibliotheken für JMS):**Diese Komponente stellt die JMS-Clientkomponente aus dem Apache Qpid-Projekt bereit, um Ihrer Anwendung die Verwendung von AMQP-Messaging in Microsoft Azure zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="27b69-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="27b69-125">**Package for Microsoft Azure Libraries for Java (Paket für Microsoft Azure-Bibliotheken für Java):** Diese Komponente stellt APIs für den Zugriff auf Microsoft Azure-Dienste wie Storage, Service Bus, Service Runtime usw. bereit.</span><span class="sxs-lookup"><span data-stu-id="27b69-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>

1. <span data-ttu-id="27b69-126">Klicken Sie auf **Weiter**.
</span><span class="sxs-lookup"><span data-stu-id="27b69-126">Click **Next**.</span></span> <span data-ttu-id="27b69-127">(Wenn ungewöhnliche Verzögerungen bei der Installation des Toolkits auftreten, achten Sie darauf, dass **Contact all update sites during install to find required software** deaktiviert ist.)</span><span class="sxs-lookup"><span data-stu-id="27b69-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="27b69-128">Klicken Sie im Dialogfeld **Install Details** (Installationsdetails) auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="27b69-128">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Installationsdetails überprüfen][03]

1. <span data-ttu-id="27b69-130">Überprüfen Sie im Dialogfeld **Review Licences** die Bedingungen der Lizenzverträge.</span><span class="sxs-lookup"><span data-stu-id="27b69-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="27b69-131">Wenn Sie dem Lizenzvertrag zustimmen, klicken Sie auf **I accept the terms of the license agreements** (Ich akzeptiere die Bedingungen der Lizenzvereinbarungen), und klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="27b69-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="27b69-132">(Bei den restlichen Schritten wird davon ausgegangen, dass Sie dem Lizenzvertrag zugestimmt haben.</span><span class="sxs-lookup"><span data-stu-id="27b69-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="27b69-133">Wenn Sie die Bedingungen der Lizenzverträge nicht akzeptieren, beenden Sie den Installationsprozess.)</span><span class="sxs-lookup"><span data-stu-id="27b69-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Review Licences][04]
   
   <span data-ttu-id="27b69-135">Eclipse lädt die erforderlichen Pakete herunter und installiert diese.</span><span class="sxs-lookup"><span data-stu-id="27b69-135">Eclipse will download and install the requisite packages.</span></span>
   
   ![Installationsstatus][05]

1. <span data-ttu-id="27b69-137">Wenn Sie aufgefordert werden, Eclipse zum Abschließen der Installation neu zu starten, klicken Sie auf **Yes**(Ja).</span><span class="sxs-lookup"><span data-stu-id="27b69-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Aufforderung zum Neustarten][06]

## <a name="next-steps"></a><span data-ttu-id="27b69-139">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="27b69-139">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
