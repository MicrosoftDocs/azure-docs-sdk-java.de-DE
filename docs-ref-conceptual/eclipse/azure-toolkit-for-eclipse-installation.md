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
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Installieren des Azure-Toolkits für Eclipse

Das Azure Toolkit für Eclipse stellt Vorlagen und Funktionen bereit, die Ihnen das einfache Erstellen, Entwickeln, Testen und Bereitstellen von Azure-Anwendungen mithilfe der Eclipse-Entwicklungsumgebung ermöglichen. Das Azure Toolkit für Eclipse ist ein Open-Source-Projekt. Der Quellcode ist verfügbar unter der MIT-Lizenz unter <https://github.com/microsoft/azure-tools-for-java>.

Die folgenden Schritte veranschaulichen die Installation des Azure-Toolkits für Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>So installieren Sie das Azure-Toolkit für Eclipse

1. Starten Sie Eclipse.

1. Klicken Sie auf das Menü **Help** (Hilfe) und dann auf **Install New Software** (Neue Software installieren), wie in der folgenden Abbildung gezeigt.
   
   ![Installieren des Azure-Toolkits für Eclipse][01]

1. Geben Sie im Dialogfeld **Available Software** (Verfügbare Software) im Textfeld **Work with** (Arbeiten mit) `http://dl.microsoft.com/eclipse/` ein, und drücken Sie dann die **EINGABETASTE**.

1. Aktivieren Sie im Fenster **Name** die Option **Azure Toolkit for Eclipse**, und deaktivieren Sie **Contact all update sites during install to find required software**. Der Bildschirm sieht dann etwa wie folgt aus:
   
   ![Installieren des Azure-Toolkits für Eclipse][02]

1. Nach dem Erweitern von **Azure Toolkit for Eclipse**(Azure Toolkit für Eclipse) wird eine Liste mit Elementen wie im folgenden Beispiel angezeigt:
   
   * **Application Insights-Plug-In for Java:**Diese Komponente ermöglicht Ihnen die Verwendung der Telemetriedatenprotokollierung und der Analysedienste von Azure für Ihre Anwendungen und Server-Instanzen.
   * **Azure Access Control Services Filter:**Diese Komponente bietet Unterstützung für die Authentifizierung von Anwendungsbenutzern mit Azure ACS, sodass Szenarios mit einmaligem Anmelden ermöglicht werden und die Identitätslogik aus der Anwendung externalisiert wird.
   * **Azure Common Plugin (Allgemeines Azure-Plug-In):**Diese Komponente stellt die allgemeine Funktionalität bereit, die für andere Toolkit-Komponenten erforderlich ist.
   * **Azure Explorer for Eclipse (Azure-Explorer für Eclipse):**Diese Komponente stellt die allgemeine Funktionalität bereit, die für andere Toolkit-Komponenten erforderlich ist.
   * **Azure Plugin for Eclipse with Java (Azure-Plug-In für Eclipse mit Java):**Diese Komponente bietet Unterstützung für die Entwicklung von Projekten, mit deren Hilfe Java-Anwendungen für die Microsoft Azure-Cloud in Eclipse und über die Befehlszeile erstellt, getestet und bereitgestellt werden können.
   * **Azure Web Apps Plugin with Java (Azure Web Apps-Plug-In mit Java):**Diese Komponente bietet Unterstützung für die Bereitstellung von Java-Webanwendungen in Microsoft Azure-Web-App-Containern.
   * **Microsoft JDBC Driver 4.2 for SQL Server (Microsoft JDBC-Treiber 4.2 für SQL Server):**Diese Komponente stellt die JDBC-API für SQL Server und Microsoft Azure SQL-Datenbank für die Java Platform Enterprise Edition 8 bereit.
   * **Package for Apache Qpid Client Libraries for JMS (Paket für Apache Qpid-Clientbibliotheken für JMS):**Diese Komponente stellt die JMS-Clientkomponente aus dem Apache Qpid-Projekt bereit, um Ihrer Anwendung die Verwendung von AMQP-Messaging in Microsoft Azure zu ermöglichen.
   * **Package for Microsoft Azure Libraries for Java (Paket für Microsoft Azure-Bibliotheken für Java):** Diese Komponente stellt APIs für den Zugriff auf Microsoft Azure-Dienste wie Storage, Service Bus, Service Runtime usw. bereit.

1. Klicken Sie auf **Weiter**.
 (Wenn ungewöhnliche Verzögerungen bei der Installation des Toolkits auftreten, achten Sie darauf, dass **Contact all update sites during install to find required software** deaktiviert ist.)

1. Klicken Sie im Dialogfeld **Install Details** (Installationsdetails) auf **Weiter**.
   
   ![Installationsdetails überprüfen][03]

1. Überprüfen Sie im Dialogfeld **Review Licences** die Bedingungen der Lizenzverträge. Wenn Sie dem Lizenzvertrag zustimmen, klicken Sie auf **I accept the terms of the license agreements** (Ich akzeptiere die Bedingungen der Lizenzvereinbarungen), und klicken Sie dann auf **Fertig stellen**. (Bei den restlichen Schritten wird davon ausgegangen, dass Sie dem Lizenzvertrag zugestimmt haben. Wenn Sie die Bedingungen der Lizenzverträge nicht akzeptieren, beenden Sie den Installationsprozess.)
   
   ![Review Licences][04]
   
   Eclipse lädt die erforderlichen Pakete herunter und installiert diese.
   
   ![Installationsstatus][05]

1. Wenn Sie aufgefordert werden, Eclipse zum Abschließen der Installation neu zu starten, klicken Sie auf **Yes**(Ja).
   
   ![Aufforderung zum Neustarten][06]

## <a name="next-steps"></a>Nächste Schritte

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
