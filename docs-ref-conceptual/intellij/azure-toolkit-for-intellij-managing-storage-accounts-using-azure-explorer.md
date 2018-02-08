---
title: "Verwalten von Speicherkonten mithilfe von Azure-Explorer für IntelliJ"
description: "Erfahren Sie, wie Sie Ihre Azure-Speicherkonten mit Azure-Explorer für IntelliJ verwalten."
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
ms.openlocfilehash: 4edb8c1ceef508dd251db693ccc3b98d77ec452b
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a>Verwalten von Speicherkonten mithilfe von Azure-Explorer für IntelliJ

Der Azure-Explorer gehört zum Azure-Toolkit für IntelliJ und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von Speicherkonten in ihrem Azure-Konto innerhalb der integrierten Entwicklungsumgebung (IDE) von IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Erstellen eines Speicherkontos in IntelliJ

Gehen Sie folgendermaßen vor, um ein Speicherkonto mit dem Azure-Explorer zu erstellen:

1. Melden Sie sich beim Azure-Konto gemäß den Anweisungen in [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ] an. 

2. Erweitern Sie in der Ansicht des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Speicherkonten**, und klicken Sie dann auf **Speicherkonto erstellen**.

   ![Befehl „Speicherkonto erstellen“][CS01]

3. Geben Sie im Dialogfeld **Speicherkonto erstellen** folgende Details an:

   ![Dialogfeld „Neues Speicherkonto erstellen“][CS02]

   * **Name:** Geben Sie den Namen des neuen Speicherkontos an.

   * **Kontoart:** Geben Sie den Typ des zu erstellenden Speicherkontos an (z.B. „Blob Storage“). Weitere Informationen finden Sie unter [Informationen zu Azure-Speicherkonten]. 

   * **Leistung:** Geben Sie an, welches Speicherkontoangebot vom ausgewählten Herausgeber verwendet werden soll (z.B. „Premium“). Weitere Informationen finden Sie unter [Skalierbarkeits- und Leistungsziele für Azure Storage]. 

   * **Replikation**: Gibt die Replikation des Speicherkontos an (z.B. „zonenredundant“). Weitere Informationen finden Sie unter [Azure-Speicherreplikation]. 

   * **Abonnement:** Wählen Sie das Azure-Abonnement aus, das Sie für das neue Speicherkonto verwenden möchten.

   * **Ort**: Gibt den Speicherort an, an dem Ihr Speicherkonto erstellt wird (z.B. USA, Westen).

   * **Ressourcengruppe:** Gibt die Ressourcengruppe für Ihren virtuellen Computer an. Wählen Sie eine der folgenden Optionen:
      * **Neu erstellen**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.
      * **Vorhandene verwenden**: Gibt an, dass Sie in einer Liste von Ressourcengruppen, die Ihrem Azure-Konto zugeordnet sind, eine Auswahl treffen möchten.

4. Nachdem Sie alle vorstehenden Optionen angegeben haben, klicken Sie auf **OK**.

## <a name="create-a-storage-container-in-intellij"></a>Erstellen eines Speichercontainers in IntelliJ

Gehen Sie folgendermaßen vor, um einen Speichercontainer mit dem Azure-Explorer zu erstellen:

1. Klicken Sie in der Azure-Exploreransicht mit der rechten Maustaste auf das Speicherkonto, in dem Sie einen Container erstellen möchten, und klicken Sie dann auf **Blobcontainer erstellen**.

   ![Befehl „Blobcontainer erstellen“][CC01]

2. Geben Sie im Dialogfeld **Blobcontainer erstellen** den Namen für Ihren Container ein, und klicken Sie dann auf **OK**. Weitere Informationen zum Benennen von Speichercontainern finden Sie unter [Benennen von Containern, Blobs und Metadaten und Verweisen auf diese].

   ![Dialogfeld „Speichercontainer erstellen“][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Löschen eines Speichercontainers in IntelliJ

Gehen Sie folgendermaßen vor, um einen Speichercontainer mit dem Azure-Explorer zu löschen:

1. Klicken Sie in der Azure-Exploreransicht mit der rechten Maustaste auf den Speichercontainer, und klicken Sie dann auf **Löschen**.

   ![Befehl „Speichercontainer löschen“][DC01]

2. Klicken Sie im Bestätigungsfenster auf **Ja**.

   ![Bestätigungsfenster für „Speichercontainer löschen“][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Löschen eines Speicherkontos in IntelliJ

Gehen Sie folgendermaßen vor, um ein Speicherkonto mit dem Azure-Explorer zu löschen:

1. Klicken Sie in der Ansicht des **Azure-Explorers** mit der rechten Maustaste auf das Speicherkonto, und wählen Sie dann **Löschen** aus.

   ![Menü „Speicherkonto löschen“][DS01]

2. Klicken Sie im Bestätigungsfenster auf **Ja**.

   ![Bestätigungsfenster für „Speicherkonto löschen“][DS02]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Azure Storage-Konten sowie Größen und Preisen finden Sie in den folgenden Ressourcen:

* [Einführung in Microsoft Azure Storage]
* [Informationen zu Azure-Speicherkonten]
* Größen für Azure Storage-Konten
  * [Größen für Windows-Speicherkonten in Azure]
  * [Größen für Linux-Speicherkonten in Azure]
* Preise von Azure Storage-Konten
  * [Preise von Windows-Speicherkonten]
  * [Preise von Linux-Speicherkonten]

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Einführung in Microsoft Azure Storage]: /azure/storage/storage-introduction
[Informationen zu Azure-Speicherkonten]: /azure/storage/storage-create-storage-account
[Azure-Speicherreplikation]: /azure/storage/storage-redundancy
[Skalierbarkeits- und Leistungsziele für Azure Storage]: /azure/storage/storage-scalability-targets
[Benennen von Containern, Blobs und Metadaten und Verweisen auf diese]: http://go.microsoft.com/fwlink/?LinkId=255555

[Größen für Windows-Speicherkonten in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Größen für Linux-Speicherkonten in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preise von Windows-Speicherkonten]: /pricing/details/virtual-machines/windows/
[Preise von Linux-Speicherkonten]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
