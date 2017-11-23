---
title: "Verwalten virtueller Computer mit dem Azure-Explorer für Eclipse"
description: "Erfahren Sie, wie Sie Ihre virtuellen Azure-Computer mit dem Azure-Explorer für Eclipse verwalten."
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
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 41bb9b8009c0cbae01fec42c56d6a74d84cc166b
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a>Verwalten virtueller Computer mit dem Azure-Explorer für Eclipse

Der Azure-Explorer gehört zum Azure-Toolkit für Eclipse und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von virtuellen Computern in ihrem Azure-Konto innerhalb der integrierten Entwicklungsumgebung (IDE) von Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Erstellen eines virtuellen Computers in Eclipse

Gehen Sie folgendermaßen vor, um einen virtuellen Computer mit dem Azure-Explorer zu erstellen:

1. Melden Sie sich beim Azure-Konto gemäß den Anweisungen unter [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse] an.

1. Erweitern Sie in der Ansicht des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Virtuelle Computer**, und klicken Sie dann auf **VM erstellen**.

   ![Befehl „VM erstellen“][CR01]  

   Der **Assistent zum Erstellen eines neuen virtuellen Computers** wird geöffnet.

1. Wählen Sie im Dialogfeld **Abonnement auswählen** Ihr Abonnement aus, und klicken Sie dann auf **Weiter**.

   ![Fenster „Abonnement auswählen“][CR02]

1. Geben Sie im Fenster **Virtuelles Computerimage auswählen** die folgenden Informationen ein:

   * **Standort:** gibt den Standort an, an dem Ihr virtueller Computer erstellt wird (z.B. *USA, Westen*).

   * **Herausgeber:** gibt den Herausgeber an, der das Image zum Erstellen des virtuellen Computers erstellt hat (z.B. *Microsoft*).

   * **Angebot:** gibt an, welches Angebot eines virtuellen Computers für den ausgewählten Herausgeber verwendet werden soll (z.B. *JDK*).

   * **SKU:** gibt die zu verwendende SKU (Stock-Keeping Unit, Artikelnummer) aus dem ausgewählten Angebot an (z.B. *JDK_8*).

   * **Versionsnummer:** gibt an, welche Version der ausgewählten SKU verwendet werden soll.

   ![Fenster „Virtuelles Computerimage auswählen“][CR03]

1. Klicken Sie auf **Weiter**.


1. Geben Sie im Fenster **Grundlegende Einstellungen des virtuellen Computers** die folgenden Informationen ein:

   * **Name des virtuellen Computers:** gibt den Namen Ihres virtuellen Computers an. Dieser muss mit einem Buchstaben beginnen und darf nur Buchstaben, Ziffern und Bindestriche enthalten.

   * **Größe:** gibt die Anzahl der Kerne und den Speicher an, die dem virtuellen Computer zugeordnet werden sollen

   * **Benutzername:** gibt das Administratorkonto an, das für die Verwaltung Ihres virtuellen Computer erstellt werden soll

   * **Kennwort** und **Bestätigen**: geben das Kennwort für Ihr Administratorkonto an

   ![Fenster „Grundlegende Einstellungen des virtuellen Computers“][CR04]

1. Klicken Sie auf **Weiter**.


1. Geben Sie im Fenster **Neues Speicherkonto erstellen** die folgenden Informationen ein:

   * **Ressourcengruppe:** Gibt die Ressourcengruppe für Ihren virtuellen Computer an. Wählen Sie eine der folgenden Optionen:
      * **Neu erstellen**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.
      * **Vorhandene verwenden:** gibt an, dass Sie eine Ressourcengruppe auswählen möchten, die Ihrem Azure-Konto bereits zugeordnet ist.

      ![Dialogfeld „Neues Speicherkonto erstellen“][CR05]

   * **Speicherkonto:** gibt das Speicherkonto an, das zum Speichern des virtuellen Computers verwendet werden soll. Sie können ein vorhandenes Speicherkonto auswählen oder ein neues erstellen.

   * **Virtuelles Netzwerk** und **Subnetz**: geben das virtuelle Netzwerk und das Subnetz an, mit dem der virtuelle Computer eine Verbindung herstellen soll. Sie können ein vorhandenes Netzwerk und Subnetz verwenden oder ein neues Netzwerk und Subnetz erstellen. Wenn Sie **Neu erstellen** auswählen, wird das folgende Dialogfeld angezeigt:

      ![Dialogfeld „Neues virtuelles Netzwerk erstellen“][CR06]

1. Geben Sie im Fenster **Zugeordnete Ressourcen** die folgenden Informationen ein:

   * **Öffentliche IP-Adresse:** gibt eine externe IP-Adresse für den virtuellen Computer an. Sie können eine neue IP-Adresse erstellen oder **(Keine)** auswählen, wenn Ihr virtueller Computer nicht über eine öffentliche IP-Adresse verfügt.

   * **Netzwerksicherheitsgruppe:** gibt eine optionale Netzwerkfirewall für den virtuellen Computer an. Sie können eine vorhandene Firewall auswählen oder **(Keine)** auswählen, wenn Ihr virtueller Computer keine Netzwerkfirewall verwendet.

   * **Verfügbarkeitsgruppe:** gibt eine optionale Verfügbarkeitsgruppe an, der Ihr virtueller Computer angehören kann. Sie können eine vorhandene Verfügbarkeitsgruppe auswählen, eine neue erstellen oder **(Keine)** auswählen, wenn Ihr virtueller Computer keiner Verfügbarkeitsgruppe angehören soll.

   ![Fenster „Zugeordnete Ressourcen“][CR07]

1. Klicken Sie auf **Fertig stellen**.  

   Der neue virtuelle Computer wird im Toolfenster von Azure-Explorer angezeigt.

   ![Neuer virtueller Computer][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Neustarten eines virtuellen Computers in Eclipse

Um einen virtuellen Computer mithilfe des Azure-Explorers in Eclipse neu zu starten, gehen Sie folgendermaßen vor:

1. Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Neu starten** aus.

   ![Befehl „Neu starten“ für einen virtuellen Computer][RE01]

1. Klicken Sie im Bestätigungsfenster auf **Ja**.

   ![Bestätigungsfenster für den Neustart][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Herunterfahren eines virtuellen Computers in Eclipse

Um einen ausgeführten virtuellen Computer mithilfe des Azure-Explorers in Eclipse herunterzufahren, gehen Sie folgendermaßen vor:

1. Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Herunterfahren** aus.

   ![Befehl „Herunterfahren“ für einen virtuellen Computer][SH01]

1. Klicken Sie im Bestätigungsfenster auf **Ja**.

   ![Bestätigungsfenster für das Herunterfahren eines virtuellen Computers][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Löschen eines virtuellen Computers in Eclipse

Um einen virtuellen Computer mithilfe des Azure-Explorers in Eclipse zu löschen, gehen Sie folgendermaßen vor:

1. Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Löschen** aus.

   ![Befehl „Löschen“ für einen virtuellen Computer][DE01]

1. Klicken Sie im Bestätigungsfenster auf **Ja**.

   ![Bestätigungsfenster für das Löschen eines virtuellen Computers][DE02]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den Größen und Preisen für virtuelle Azure-Computer finden Sie in den folgenden Ressourcen:

* Größen für virtuelle Azure-Computer
  * [Größen für virtuelle Windows-Computer in Azure]
  * [Größen für virtuelle Linux-Computer in Azure]
* Preise für virtuelle Azure-Computer
  * [Preise von virtuellen Windows-Computern]
  * [Preise von virtuellen Linux-Computern]

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Größen für virtuelle Windows-Computer in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Größen für virtuelle Linux-Computer in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preise von virtuellen Windows-Computern]: /pricing/details/virtual-machines/windows/
[Preise von virtuellen Linux-Computern]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
