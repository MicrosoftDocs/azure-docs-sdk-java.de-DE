---
title: Anleitung zur Anmeldung für das Azure-Toolkit für Eclipse
description: Erfahren Sie, wie Sie sich bei Microsoft Azure mit dem Azure-Toolkit für Eclipse anmelden.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: b4b13de38913ae6e7ae2bb09210ac742efc9d0ad
ms.sourcegitcommit: d18d9dce22b7f7af178f756bd341433d24e3c3b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2019
ms.locfileid: "66575317"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Anleitung zur Anmeldung für das Azure-Toolkit für Eclipse

Das Azure-Toolkit für Eclipse bietet zwei Methoden für die Anmeldung bei Ihrem Azure-Konto:

  - [Anmelden bei Ihrem Azure-Konto per Geräteanmeldung](#sign-in-to-your-azure-account-by-device-login)
  - [Anmelden bei Ihrem Azure-Konto per Dienstprinzipal](#sign-in-to-your-azure-account-by-service-principal)

Auch [**Abmeldemethoden**](#sign-out-of-your-azure-account) stehen zur Verfügung.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a>Anmelden bei Ihrem Azure-Konto per Geräteanmeldung

Gehen Sie wie folgt vor, um sich per Geräteanmeldung bei Azure anzumelden:

1. Öffnen Sie das Projekt in Eclipse.

2. Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.
   ![Eclipse-Menü für die Anmeldung bei Azure][I01]

3. Wählen Sie im Fenster **Azure Sign In** (Azure-Anmeldung) die Option **Device Login** (Geräteanmeldung) aus, und klicken Sie anschließend auf **Sign in** (Anmelden).

   ![Fenster für die Azure-Anmeldung mit ausgewählter Geräteanmeldung][I02]

4. Klicken Sie im Dialogfeld **Azure Device Login** (Azure-Geräteanmeldung) auf **Copy&Open** (Kopieren und öffnen).

   ![Dialogfeld für Azure-Anmeldung][I03]

> [!NOTE]
>
> Sollte der Browser nicht geöffnet werden, konfigurieren Sie Eclipse für die Verwendung eines externen Browsers wie Internet Explorer, Firefox oder Chrome:
>
> 1. Öffnen Sie „Preferences“ (Voreinstellungen) > „General“ (Allgemein) > „Web Browser“ (Webbrowser) > „Use external web browser in Eclipse“ (Externen Webbrowser in Eclipse verwenden).
>
> 2. Wählen Sie den gewünschten Browser aus.
>

5. Fügen Sie im Browser Ihren Gerätecode ein, den Sie im vorherigen Schritt durch Klicken auf **Copy&Open** (Kopieren und öffnen) kopiert haben, und klicken Sie anschließend auf **Next** (Weiter).

   ![Der Browser für die Geräteanmeldung][I04]

6. Wenn schließlich das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld zum Auswählen von Abonnements][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a>Anmelden bei Ihrem Azure-Konto per Dienstprinzipal

In diesem Abschnitt erfahren Sie, wie Sie eine Datei mit Anmeldeinformationen erstellen, die Ihre Dienstprinzipaldaten enthält. Danach verwendet Eclipse die Datei mit Anmeldeinformationen, um Sie beim Öffnen Ihres Projekts automatisch bei Azure anzumelden.

1. Öffnen Sie das Projekt in Eclipse.

2. Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Anmelden**.
   ![Der Eclipse-Befehl für Azure-Anmeldung][A01]

3. Wählen Sie im Fenster für die Azure-Anmeldung **** die Option **Service Principal** (Dienstprinzipal) aus. Sollten Sie noch nicht über die Datei für die Dienstprinzipalauthentifizierung verfügen, klicken Sie auf **New** (Neu), um eine zu erstellen. Andernfalls können Sie auf **Browse** (Durchsuchen) klicken und direkt mit Schritt 8 fortfahren.

   ![Das Fenster für die Azure-Anmeldung mit ausgewählter Dienstprinzipaloption][A02]

4. Klicken Sie im Dialogfeld **Azure Device Login** (Azure-Geräteanmeldung) auf **Copy&Open** (Kopieren und öffnen).

   ![Dialogfeld für Azure-Anmeldung][A08]

> [!NOTE]
>
> Sollte der Browser nicht geöffnet werden, konfigurieren Sie Eclipse für die Verwendung eines externen Browsers wie Internet Explorer oder Chrome:
>
> 1. Öffnen Sie „Preferences“ (Voreinstellungen) > „General“ (Allgemein) > „Web Browser“ (Webbrowser) > „Use external web browser in Eclipse“ (Externen Webbrowser in Eclipse verwenden).
>
> 2. Wählen Sie den gewünschten Browser aus.
>

5. Fügen Sie im Browser Ihren Gerätecode ein, den Sie im vorherigen Schritt durch Klicken auf **Copy&Open** (Kopieren und öffnen) kopiert haben, und klicken Sie anschließend auf **Next** (Weiter).

   ![Der Browser für die Geräteanmeldung][A03]

6. Wählen Sie im Dialogfeld **Create authentication files** (Authentifizierungsdateien erstellen) die gewünschten Abonnements und Ihr Zielverzeichnis aus, und klicken Sie dann auf **Start**.

   ![Fenster zum Erstellen der Authentifizierungsdateien][A04]

7. Klicken Sie im Dialogfeld **Service Principal Creation Status** (Dienstprinzipal-Erstellungsstatus) nach erfolgreicher Erstellung Ihrer Dateien auf **OK**.

   ![Dialogfeld für den Status der Dienstprinzipalerstellung][A05]

8. Die Adresse der erstellten Datei wird im Fenster für die Azure-Anmeldung **** automatisch ausgefüllt. Klicken Sie als Nächstes auf **Sign in** (Anmelden).

   ![Dialogfeld für Azure-Anmeldung][A06]

9. Wenn schließlich das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld zum Auswählen von Abonnements][A07]

## <a name="sign-out-of-your-azure-account"></a>Abmelden von Ihrem Azure-Abonnement

Nachdem Sie Ihr Konto mithilfe der obigen Schritte konfiguriert haben, werden Sie bei jedem Start von Eclipse automatisch angemeldet. Mit den folgenden Schritten können Sie sich bei Bedarf von Ihrem Azure-Konto abmelden:

1. Klicken Sie auf **Extras**, anschließend auf **Azure** und dann auf **Abmelden**.

   ![Eclipse-Menü für die Abmeldung bei Azure][L01]

2. Wenn das Dialogfeld **Azure-Anmeldung** angezeigt wird, klicken Sie auf **Ja**.

   ![Dialogfeld zum Abmelden][L02]

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

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
