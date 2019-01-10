---
title: Verwalten virtueller Computer mit dem Azure-Explorer für Eclipse
description: Erfahren Sie, wie Sie Ihre virtuellen Azure-Computer mit dem Azure-Explorer für Eclipse verwalten.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 7f3b4a6adb4234bbf11f0f7cddafbe99fa0ff3df
ms.sourcegitcommit: 24f037d133875f86761ec893dfa74e723de040b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2018
ms.locfileid: "53636696"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a>Verwalten virtueller Computer mit dem Azure-Explorer für Eclipse

Der Azure-Explorer gehört zum Azure-Toolkit für Eclipse und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von virtuellen Computern in ihrem Azure-Konto innerhalb der integrierten Entwicklungsumgebung (IDE) von Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Erstellen eines virtuellen Computers in Eclipse

Gehen Sie folgendermaßen vor, um einen virtuellen Computer mit dem Azure-Explorer zu erstellen:

1. Melden Sie sich beim Azure-Konto gemäß den Anweisungen in [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) an.

2. Erweitern Sie in der Ansicht des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Virtuelle Computer**, und klicken Sie dann auf **VM erstellen**.

   ![Befehl „VM erstellen“][CR01]  

   Der **Assistent zum Erstellen eines neuen virtuellen Computers** wird geöffnet.

3. Wählen Sie im Dialogfeld **Abonnement auswählen** Ihr Abonnement aus, und klicken Sie dann auf **Weiter**.

   ![Fenster „Abonnement auswählen“][CR02]

4. Geben Sie im Fenster **Virtuelles Computerimage auswählen** die folgenden Informationen ein:

   * **Standort**: Der Standort, an dem Ihre VM erstellt wird (z. B. *USA, Westen*).

   * **Herausgeber**: Der Herausgeber, der das zum Erstellen der VM verwendete Image erstellt hat (z. B. *Microsoft*).

   * **Angebot**: Das zu verwendende VM-Angebot des ausgewählten Herausgebers (z. B. *JDK*).

   * **SKU**: Die zu verwendende SKU (Stock Keeping Unit) des ausgewählten Angebots (z. B. *JDK_8*).

   * **Versionsnummer**: Die zu verwendende Version der ausgewählten SKU.

   ![Fenster „Virtuelles Computerimage auswählen“][CR03]

5. Klicken Sie auf **Weiter**.

6. Geben Sie im Fenster **Grundlegende Einstellungen des virtuellen Computers** die folgenden Informationen ein:

   * **Name des virtuellen Computers**: Der Name Ihrer neuen VM. Der Name muss mit einem Buchstaben beginnen und darf nur Buchstaben, Ziffern und Bindestriche enthalten.

   * **Größe**: Die Anzahl von Kernen und der Arbeitsspeicher, die der VM zugeordnet werden sollen.

   * **Benutzername**: Das Administratorkonto, das für die Verwaltung Ihrer VM erstellt werden soll.

   * **Kennwort** und **Bestätigen**: Das Kennwort für Ihr Administratorkonto.

   ![Fenster „Grundlegende Einstellungen des virtuellen Computers“][CR04]

7. Klicken Sie auf **Weiter**.

8. Geben Sie im Fenster **Neues Speicherkonto erstellen** die folgenden Informationen ein:

   * **Ressourcengruppe**: Die Ressourcengruppe für Ihre VM. Wählen Sie eine der folgenden Optionen:
     * **Neue erstellen**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.
     * **Vorhandene verwenden**: Gibt an, dass Sie eine Ressourcengruppe auswählen möchten, die Ihrem Azure-Konto bereits zugeordnet ist.

       ![Dialogfeld „Neues Speicherkonto erstellen“][CR05]

   * **Speicherkonto**: Das Speicherkonto, das zum Speichern der VM verwendet werden soll. Sie können ein vorhandenes Speicherkonto auswählen oder ein neues erstellen.

   * **Virtuelles Netzwerk** und **Subnetz**: Das virtuelle Netzwerk und das Subnetz, mit denen Ihre VM eine Verbindung herstellt. Sie können ein vorhandenes Netzwerk und Subnetz verwenden oder ein neues Netzwerk und Subnetz erstellen. Wenn Sie **Neu erstellen** auswählen, wird das folgende Dialogfeld angezeigt:

      ![Dialogfeld „Neues virtuelles Netzwerk erstellen“][CR06]

9. Geben Sie im Fenster **Zugeordnete Ressourcen** die folgenden Informationen ein:

   * **Öffentliche IP-Adresse**: Eine externe IP-Adresse für Ihre VM. Sie können eine neue IP-Adresse erstellen oder **(Keine)** auswählen, wenn Ihr virtueller Computer nicht über eine öffentliche IP-Adresse verfügt.

   * **Netzwerksicherheitsgruppe**: Eine optionale Netzwerkfirewall für Ihre VM. Sie können eine vorhandene Firewall auswählen oder **(Keine)** auswählen, wenn Ihr virtueller Computer keine Netzwerkfirewall verwendet.

   * **Verfügbarkeitsgruppe**: Eine optionale Verfügbarkeitsgruppe, der Ihre VM angehören kann. Sie können eine vorhandene Verfügbarkeitsgruppe auswählen, eine neue erstellen oder **(Keine)** auswählen, wenn Ihr virtueller Computer keiner Verfügbarkeitsgruppe angehören soll.

   ![Fenster „Zugeordnete Ressourcen“][CR07]

10. Klicken Sie auf **Fertig stellen**.  

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
[Preise von virtuellen Windows-Computern]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Preise von virtuellen Linux-Computern]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/

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
