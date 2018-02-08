---
title: "Anleitung zur Anmeldung für das Azure-Toolkit für Eclipse"
description: "Erfahren Sie, wie Sie sich bei Microsoft Azure mit dem Azure-Toolkit für Eclipse anmelden."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 498a22c455e54b8038169cf4e9f6ac7d7287c0bb
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse

Das Azure-Toolkit für Eclipse bietet zwei Methoden für die Anmeldung bei Ihrem Azure-Konto:

  * **Automatisch:** Für diese Methode erstellen Sie eine Datei mit Anmeldeinformationen, die Ihre Dienstprinzipaldaten enthält. Anschließend können Sie sich mithilfe dieser Datei automatisch bei Ihrem Azure-Konto anmelden.
  * **Interaktiv:** Bei Auswahl dieser Methode geben Sie bei jeder Anmeldung bei Ihrem Azure-Konto Ihre Azure-Anmeldeinformationen ein.

In den folgenden Abschnitten wird die Verwendung der beiden Methoden beschrieben.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Automatisches Anmelden bei Ihrem Azure-Konto und Erstellen einer Datei mit Anmeldeinformationen für die zukünftige Nutzung

Nachstehend werden die Schritte zum Erstellen einer Datei mit Anmeldeinformationen erläutert, die Ihre Dienstprinzipaldaten enthält. Nachdem Sie diese Schritte abgeschlossen haben, verwendet Eclipse automatisch die Datei mit Anmeldeinformationen, damit Sie beim Öffnen Ihres Projekts automatisch bei Azure angemeldet werden.

1. Öffnen Sie das Projekt in Eclipse.

1. Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.

   ![Eclipse-Menü für die Anmeldung bei Azure][A01]

1. Wählen Sie im angezeigten Dialogfeld **Azure-Anmeldung** die Option **Automatisiert** aus, und klicken Sie dann auf **Neu**.

   ![Anmeldedialogfeld][A02]

1. Wenn das Dialogfeld **Azure Log In** angezeigt wird, geben Sie Ihre Azure-Anmeldeinformationen ein, und klicken Sie dann auf **Sign In**.

   ![Dialogfeld für Azure-Anmeldung][A03]

1. Wenn das Dialogfeld **Create authentication files** angezeigt wird, wählen Sie die gewünschten Abonnements aus. Wählen Sie Ihr Zielverzeichnis, und klicken Sie dann auf **Start**.

   ![Dialogfeld für Azure-Anmeldung][A04]

1. Das Dialogfeld **Dienstprinzipal-Erstellungsstatus** wird angezeigt. Nachdem Ihre Dateien erstellt wurden, klicken Sie auf **OK**.

   ![Dialogfeld mit dem Status der Dienstprinzipalerstellung][A05]

1. Wenn das Dialogfeld **Azure-Anmeldung** angezeigt wird, klicken Sie auf **Anmelden**.

   ![Dialogfeld für Azure-Anmeldung][A06]

1. Wenn das Dialogfeld **Select Subscriptions** angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Automatisches Abmelden von Ihrem Azure-Konto bei zuvor erfolgter automatischer Anmeldung

Nachdem Sie die Schritte im vorherigen Abschnitt konfiguriert haben, meldet das Azure-Toolkit Sie bei jedem Neustart von Eclipse automatisch bei Ihrem Azure-Konto an. Um sich jedoch von Ihrem Azure-Konto abzumelden und zu verhindern, dass das Azure-Toolkit Sie automatisch anmeldet, führen Sie die folgenden Schritte aus.

1. Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Abmelden**.

   ![Eclipse-Menü für die Abmeldung bei Azure][L01]

1. Wenn das Dialogfeld **Azure-Anmeldung** angezeigt wird, klicken Sie auf **Ja**.

   ![Dialogfeld zum Abmelden][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Automatisches Anmelden bei Ihrem Azure-Konto mithilfe einer bereits erstellten Datei mit Anmeldeinformationen

Wenn Sie sich bei Verwendung von Eclipse von Azure abmelden, müssen Sie das Azure-Toolkit für Eclipse so neu konfigurieren, dass eine zuvor erstellte Datei mit Anmeldeinformationen verwendet wird, bevor Sie sich automatisch bei Ihrem Azure-Konto anmelden können. Die folgenden Schritte begleiten Sie durch die Konfiguration des Azure-Toolkits, damit eine vorhandene Datei mit Anmeldeinformationen verwendet wird.

1. Öffnen Sie das Projekt in Eclipse.

1. Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.

   ![Eclipse-Menü für die Anmeldung bei Azure][A01]

1. Wählen Sie im angezeigten Dialogfeld **Azure-Anmeldung** die Option **Automatisiert** aus, und klicken Sie dann auf **Durchsuchen**.

   ![Anmeldedialogfeld][A02]

1. Wenn das Dialogfeld **Authentifizierungsdatei auswählen** angezeigt wird, wählen Sie eine zuvor erstellte Datei mit Anmeldeinformationen aus, und klicken Sie dann auf **Auswählen**.

   ![Anmeldedialogfeld][A08]

1. Wenn das Dialogfeld **Azure Sign In** angezeigt wird, klicken Sie auf **Sign In**.

   ![Dialogfeld für Azure-Anmeldung][A06]

1. Wenn das Dialogfeld **Select Subscriptions** angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="signing-into-your-azure-account-interactively"></a>Interaktive Anmeldung bei Ihrem Azure-Konto

Nachstehend wird erläutert, wie Sie sich bei Azure durch manuelles Eingeben Ihrer Azure-Anmeldeinformationen anmelden.

1. Öffnen Sie das Projekt in Eclipse.

1. Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.

   ![Eclipse-Menü für die Anmeldung bei Azure][I01]

1. Wählen Sie im angezeigten Dialogfeld **Azure-Anmeldung** die Option **Interaktiv** aus, und klicken Sie dann auf **Anmelden**.

   ![Anmeldedialogfeld][I02]

1. Wenn das Dialogfeld **Azure Log In** angezeigt wird, geben Sie Ihre Azure-Anmeldeinformationen ein, und klicken Sie dann auf **Sign In**.

   ![Dialogfeld „Azure-Anmeldung“][I03]

1. Wenn das Dialogfeld **Select Subscriptions** angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld „Abonnements auswählen“][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Abmelden von Ihrem Azure-Konto bei zuvor erfolgter interaktiver Anmeldung

Nachdem Sie die Schritte im vorherigen Abschnitt konfiguriert haben, werden Sie bei jedem Neustart von Eclipse automatisch von Ihrem Azure-Konto abgemeldet. Wenn Sie sich jedoch von Ihrem Azure-Konto abmelden möchten, ohne Eclipse neu zu starten, führen Sie die folgenden Schritte aus.

1. Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Abmelden**.

   ![Eclipse-Menü für die Abmeldung bei Azure][L01]

1. Wenn das Dialogfeld **Azure-Anmeldung** angezeigt wird, klicken Sie auf **Ja**.

   ![Dialogfeld zum Abmelden][L02]

## <a name="next-steps"></a>Nächste Schritte

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
