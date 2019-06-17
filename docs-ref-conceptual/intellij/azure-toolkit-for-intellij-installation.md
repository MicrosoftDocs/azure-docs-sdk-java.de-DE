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
# <a name="installing-the-azure-toolkit-for-intellij"></a>Installieren des Azure-Toolkits für IntelliJ

Das Azure-Toolkit für IntelliJ stellt Vorlagen und Funktionen bereit, die Ihnen das einfache Erstellen, Entwickeln, Testen und Bereitstellen von Cloudanwendungen in Azure mithilfe der IntelliJ IDEA-Entwicklungsumgebung ermöglichen.

> [!NOTE] 
> 
> Das Azure-Toolkit für IntelliJ ist ein Open-Source-Projekt, dessen Quellcode unter der MIT-Lizenz auf der GitHub-Website des Projekts verfügbar ist: 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

Es gibt zwei Methoden zum Installieren des Azure-Toolkits für IntelliJ: über das Dialogfeld **Einstellungen** und über das Menü **Konfigurieren** auf dem Startbildschirm. Beide Installationsmethoden werden in den folgenden Schritten veranschaulicht.

## <a name="prerequisites"></a>Voraussetzungen

Für das Azure-Toolkit für IntelliJ sind folgende Softwarekomponenten erforderlich:

* Ein installiertes Java Development Kit (JDK) ab Version 8, beispielsweise: [OpenJDK](https://openjdk.java.net/) oder [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* Eine installierte Instanz von [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) (Ultimate Edition oder Community Edition)

> [!NOTE]
> 
> Auf der Seite [Azure-Toolkit für IntelliJ](https://plugins.jetbrains.com/plugin/8053) im Repository für JetBrains-Plug-Ins sind die mit dem Toolkit kompatiblen Builds aufgeführt.
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


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a>So installieren Sie das Azure-Toolkit für IntelliJ über das Dialogfeld „Einstellungen“

1. Starten Sie IntelliJ IDEA.

1. Wenn IntelliJ IDEA geöffnet wird, klicken Sie auf **File** (Datei), klicken Sie dann auf **Settings** (Einstellungen).
   
   ![Das Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA öffnen][01a]

1. Klicken Sie im Dialogfeld „Settings“ (Einstellungen) auf **Plugins**, und klicken Sie dann auf **Browse Repositories** (Repositorys durchsuchen).
   
   ![Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA][02a]

1. Geben Sie im Dialogfeld **Browse Repositories** (Repositorys durchsuchen) in das Suchfeld „Azure“ ein. Markieren Sie **Azure Toolkit for IntelliJ** (Azure Toolkit für IntelliJ), und klicken Sie dann auf **Install** (Installieren).
   
   ![Suchen nach dem Azure-Toolkit für IntelliJ][03]
   
   IntelliJ IDEA zeigt den Installationsstatus in einem Dialogfeld an.
   
   ![Installationsstatus][04]

1. Klicken Sie nach Abschluss der Installation auf **Restart IntelliJ IDEA**(IntelliJ IDEA neu starten).
   
   ![Restart IntelliJ IDEA][05]

1. Klicken Sie auf **OK** , um das Dialogfeld „Settings“ (Einstellungen) zu schließen.
   
   ![Das Dialogfeld „Settings“ (Einstellungen) von IntelliJ IDEA schließen][06]

1. Wenn Sie gefragt werden, ob Sie IntelliJ IDEA neu starten oder den Neustart später durchführen möchten, klicken Sie auf **Restart**(Neu starten).
   
1   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a>So installieren Sie das Azure-Toolkit für IntelliJ über den Startbildschirm

1. Starten Sie IntelliJ IDEA.

1. Wenn der Startbildschirm von IntelliJ IDEA angezeigt wird, klicken Sie auf **Configure** (Konfigurieren), und klicken Sie dann auf **Plugins**.
   
   ![IntelliJ IDEA-Plug-Ins installieren][01b]

1. Klicken Sie im Dialogfeld **Plugins** auf **Browse Repositories** (Repositorys durchsuchen).
   
   ![Die Plug-In-Repositorys von IntelliJ IDEA durchsuchen][02b]

1. Geben Sie im Dialogfeld **Browse Repositories** (Repositorys durchsuchen) in das Suchfeld „Azure“ ein. Markieren Sie **Azure Toolkit for IntelliJ** (Azure Toolkit für IntelliJ), und klicken Sie dann auf **Install** (Installieren).
   
   ![Suchen nach dem Azure-Toolkit für IntelliJ][03]
   
   IntelliJ IDEA zeigt den Installationsstatus in einem Dialogfeld an.
   
   ![Installationsstatus][04]

1. Klicken Sie nach Abschluss der Installation auf **Restart IntelliJ IDEA**(IntelliJ IDEA neu starten).
   
   ![Restart IntelliJ IDEA][05]

1. Wenn Sie gefragt werden, ob Sie IntelliJ IDEA neu starten oder den Neustart später durchführen möchten, klicken Sie auf **Restart**(Neu starten).
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a>Nächste Schritte

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
