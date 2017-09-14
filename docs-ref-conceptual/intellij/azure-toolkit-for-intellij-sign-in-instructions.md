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
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 85fa5eb979e4d28d49db215ee1653b4c064a87c5
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a>Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ

Das Azure-Toolkit für IntelliJ bietet zwei Methoden für die Anmeldung bei Ihrem Azure-Konto:

  * **Automatisiert:** Sie erstellen eine Datei mit Anmeldeinformationen, die Sie für die automatische Anmeldung beim Azure-Konto verwenden können.
  * **Interaktiv:** Sie geben Ihre Azure-Anmeldeinformationen bei jeder Anmeldung beim Azure-Konto ein.

In den folgenden Abschnitten wird die Verwendung der beiden Methoden beschrieben.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a>Automatisches Anmelden bei Ihrem Azure-Konto

In diesem Abschnitt erfahren Sie, wie Sie eine Datei mit Anmeldeinformationen erstellen, die Ihre Dienstprinzipaldaten enthält. Nachdem Sie dieses Verfahren abgeschlossen haben, verwendet Eclipse die Datei mit Anmeldeinformationen, um Sie bei jedem Öffnen Ihres Projekts automatisch bei Azure anzumelden.

1. Öffnen Sie das Projekt in IntelliJ IDEA.

1. Zeigen Sie im Menü **Tools** (Extras) auf **Azure**, und klicken Sie dann auf **Azure Sign In** (Azure-Anmeldung).

   ![IntelliJ-Befehl für Azure-Anmeldung][A01]

1. Wählen Sie im Fenster **Azure Sign In** (Azure-Anmeldung) die Option **Automated** (Automatisiert) aus, und klicken Sie dann auf **New** (Neu).

   ![Fenster für die Azure Anmeldung mit „Automated“ ausgewählt][A02]

1. Geben Sie im Fenster **Azure Log In** (Azure-Anmeldung) Ihre Azure-Anmeldeinformationen ein, und klicken Sie dann auf **Sign in** (Anmelden).

   ![Dialogfeld für Azure-Anmeldung][A03]

1. Wählen Sie im Dialogfeld **Create authentication files** (Authentifizierungsdateien erstellen) die gewünschten Abonnements und Ihr Zielverzeichnis aus, und klicken Sie dann auf **Start**.

   ![Fenster zum Erstellen der Authentifizierungsdateien][A04]

1. Klicken Sie im Dialogfeld **Service Principal Creation Status** (Dienstprinzipal-Erstellungsstatus) nach dem Erstellen Ihrer Dateien auf **OK**.

   ![Dialogfeld für den Status der Dienstprinzipalerstellung][A05]

1. Klicken Sie im Fenster **Azure Sign In** (Azure-Anmeldung) auf **Sign in** (Anmelden).

   ![Dialogfeld für Azure-Anmeldung][A06]

1. Wenn das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Abmelden von Ihrem Azure-Konto nach automatischer Anmeldung

Nachdem Sie Ihr Konto über die zuvor angegebenen Schritte konfiguriert haben, werden Sie bei jedem Neustart von IntelliJ IDEA automatisch durch das Azure-Toolkit bei Ihrem Azure-Konto angemeldet. Um sich jedoch von Ihrem Azure-Konto abzumelden und zu verhindern, dass das Azure-Toolkit Sie automatisch anmeldet, gehen Sie folgendermaßen vor:

1. Klicken Sie in IntelliJ IDEA auf **Tools** (Extras), zeigen Sie auf **Azure**, und klicken Sie dann auf **Azure Sign Out** (Azure-Abmeldung).

   ![IntelliJ-Befehl für Azure-Abmeldung][L01]

1. Klicken Sie im Bestätigungsfenster **Azure Sign Out** (Azure-Abmeldung) auf **Yes** (Ja).

   ![Bestätigungsfenster für Azure-Abmeldung][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a>Automatisches Anmelden bei Ihrem Azure-Konto mithilfe einer vorhandenen Datei mit Anmeldeinformationen

Wenn Sie sich bei Verwendung von IntelliJ IDEA von Ihrem Azure-Konto abmelden, müssen Sie eine vorhandene Datei mit Anmeldeinformationen verwenden, um sich automatisch wieder bei dem Konto anzumelden. Zum Konfigurieren des Azure-Toolkits für Eclipse, sodass eine vorhandene Datei mit Anmeldeinformationen verwendet werden, gehen Sie folgendermaßen vor:

1. Öffnen Sie das Projekt in IntelliJ IDEA.

1. Zeigen Sie im Menü **Tools** (Extras) auf **Azure**, und klicken Sie dann auf **Azure Sign In** (Azure-Anmeldung).

   ![IntelliJ-Befehl für Azure-Anmeldung][A01]

1. Wählen Sie im Fenster **Azure Sign In** (Azure-Anmeldung) die Option **Automated** (Automatisiert) aus, und klicken Sie dann auf **Browse** (Durchsuchen).

   ![Fenster für die Azure Anmeldung mit „Automated“ ausgewählt][A02]

1. Wählen Sie im Dialogfeld **Select Authentication File** (Authentifizierungsdatei auswählen) eine zuvor erstellte Datei mit Anmeldeinformationen aus, und klicken Sie dann auf **Select** (Auswählen).

   ![Dialogfeld zum Auswählen einer Authentifizierungsdatei][A08]

1. Klicken Sie im Fenster **Azure Sign In** (Azure-Anmeldung) auf **Sign in** (Anmelden).

   ![Fenster für die Azure Anmeldung mit „Automated“ ausgewählt][A06]

1. Wenn das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a>Interaktive Anmeldung bei Ihrem Azure-Konto

Gehen Sie folgendermaßen vor, um sich durch manuelles Eingeben Ihrer Azure-Anmeldeinformationen bei Azure anzumelden:

1. Öffnen Sie das Projekt in IntelliJ IDEA.

1. Klicken Sie auf **Tools** (Extras), zeigen Sie auf **Azure**, und klicken Sie dann auf **Azure Sign In** (Azure-Anmeldung).

   ![IntelliJ-Befehl für Azure-Anmeldung][I01]

1. Wählen Sie im Fenster **Azure Sign In** (Azure-Anmeldung) die Option **Interactive** (Interaktiv) aus, und klicken Sie dann auf **Sign in** (Anmelden).

   ![Fenster für die Azure Anmeldung mit „Interactive“ ausgewählt][I02]

1. Geben Sie im Dialogfeld **Azure Log In** (Azure-Anmeldung) Ihre Azure-Anmeldeinformationen ein, und klicken Sie dann auf **Sign in** (Anmelden).

   ![Dialogfeld für Azure-Anmeldung][I03]

1. Wenn das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld zum Auswählen von Abonnements][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Abmelden von Ihrem Azure-Konto nach interaktiver Anmeldung

Nachdem Sie Ihr Konto über die zuvor angegebenen Schritte konfiguriert haben, werden Sie bei jedem Neustart von IntelliJ IDEA automatisch von Ihrem Azure-Konto abgemeldet. Wenn Sie sich jedoch von Ihrem Azure-Konto abmelden möchten, *ohne* IntelliJ IDEA neu zu starten, gehen Sie folgendermaßen vor.

1. Klicken Sie in IntelliJ IDEA auf **Tools** (Extras), zeigen Sie auf **Azure**, und klicken Sie dann auf **Azure Sign Out** (Azure-Abmeldung).

   ![IntelliJ-Befehl für Azure-Abmeldung][L01]

1. Klicken Sie im Bestätigungsfenster **Azure Sign Out** (Azure-Abmeldung) auf **Yes** (Ja).

   ![Bestätigungsfenster für Azure-Abmeldung][L02]

## <a name="next-steps"></a>Nächste Schritte

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
