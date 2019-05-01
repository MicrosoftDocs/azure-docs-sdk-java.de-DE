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
ms.openlocfilehash: bcc5ed04143eebaff89e5688a818e464f077390e
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61590664"
---
# <a name="install-the-azure-toolkit-for-eclipse"></a>Installieren des Azure-Toolkits für Eclipse

Das Azure-Toolkit für Eclipse stellt Vorlagen und Funktionen bereit, die Ihnen das einfache Erstellen, Entwickeln, Testen und Bereitstellen von Cloudanwendungen in Azure mithilfe der Eclipse-Entwicklungsumgebung ermöglichen.

> [!NOTE] 
> 
> Das Azure Toolkit für Eclipse ist ein Open-Source-Projekt, dessen Quellcode unter der MIT-Lizenz auf der GitHub-Website des Projekts verfügbar ist: 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

Die folgenden Schritte veranschaulichen die Installation des Azure-Toolkits für Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>So installieren Sie das Azure-Toolkit für Eclipse

1. Starten Sie Eclipse.

1. Klicken Sie auf das Menü **Help** (Hilfe) und dann auf **Install New Software** (Neue Software installieren), wie in der folgenden Abbildung gezeigt.
   
   ![Installieren des Azure-Toolkits für Eclipse][01]

1. Geben Sie im Dialogfeld **Available Software** (Verfügbare Software) im Textfeld **Work with** (Arbeiten mit) `http://dl.microsoft.com/eclipse/` ein, und drücken Sie dann die **EINGABETASTE**.

1. Aktivieren Sie im Fenster **Name** die Option **Azure Toolkit for Java**, und deaktivieren Sie **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu finden). Der Bildschirm sieht dann etwa wie folgt aus:
   
   ![Installieren des Azure-Toolkits für Eclipse][02]

1. Wenn Sie **Azure-Toolkit für Eclipse** erweitern, wird eine Liste der Komponenten angezeigt, die installiert werden. Beispiel:

   | Feature | BESCHREIBUNG | 
   |---|---| 
   | **Application Insights Plugin for Java** (Application Insights-Plug-In für Java) | Ermöglicht Ihnen die Verwendung der Telemetriedatenprotokollierung und der Analysedienste von Azure für Ihre Anwendungen und Serverinstanzen. | 
   | **Azure Common Plugin** (Allgemeines Azure-Plug-In) | Stellt die allgemeine Funktionalität bereit, die für andere Toolkit-Komponenten erforderlich ist. | 
   | **Azure Container Tools for Eclipse** (Azure-Containertools für Eclipse) | Ermöglicht das Erstellen und Bereitstellen einer WAR-Datei als Docker-Container auf einem Docker-Computer. | 
   | **Azure Containers for Eclipse** (Azure-Container für Eclipse) | Ermöglicht das Bereitstellen eines WAR- oder JAR-Artefakts als Docker-Container auf einem virtuellen Azure-Computer. | 
   | **Azure Explorer for Eclipse** (Azure Explorer für Eclipse) | Bietet eine dem Explorer ähnliche Oberfläche zum Verwalten Ihrer Azure-Ressourcen. | 
   | **Microsoft JDBC-Treiber 6.1 für SQL Server** | Stellt die JDBC-API für SQL Server und Microsoft Azure SQL-Datenbank für Java Platform Enterprise Edition 8 bereit. | 
   | **Package for Microsoft Azure Libraries for Java** (Paket für Microsoft Azure-Bibliotheken für Java) | Stellt APIs für den Zugriff auf Microsoft Azure-Dienste wie Storage, Service Bus, Service Runtime usw. bereit. | 

1. Klicken Sie auf **Weiter**. (Wenn ungewöhnliche Verzögerungen bei der Installation des Toolkits auftreten, achten Sie darauf, dass **Contact all update sites during install to find required software** deaktiviert ist.)

1. Klicken Sie im Dialogfeld **Install Details** (Installationsdetails) auf **Weiter**.
   
   ![Installationsdetails überprüfen][03]

1. Überprüfen Sie im Dialogfeld **Review Licences** die Bedingungen der Lizenzverträge. Wenn Sie dem Lizenzvertrag zustimmen, klicken Sie auf **I accept the terms of the license agreements** (Ich akzeptiere die Bedingungen der Lizenzvereinbarungen), und klicken Sie dann auf **Fertig stellen**. (Bei den restlichen Schritten wird davon ausgegangen, dass Sie dem Lizenzvertrag zugestimmt haben. Wenn Sie die Bedingungen der Lizenzverträge nicht akzeptieren, beenden Sie den Installationsprozess.)
   
   ![Review Licences][04]
   
   Eclipse lädt die erforderlichen Pakete herunter und installiert diese.
   
   ![Installationsstatus][05]

1. Wenn Sie aufgefordert werden, Eclipse zum Abschließen der Installation neu zu starten, klicken Sie auf **Yes**(Ja).
   
   ![Aufforderung zum Neustarten][06]

## <a name="next-steps"></a>Nächste Schritte

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
