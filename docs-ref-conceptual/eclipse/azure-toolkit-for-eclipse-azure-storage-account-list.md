---
title: Azure-Speicherkontoliste
description: "Verwalten Sie Ihrer speicherkontoeinstellungen mit dem Azure-Toolkit für Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a>Azure-Speicherkontoliste
Azure-Speicherkonten bieten Downloadspeicherorte, die für Ihr JDK, Anwendungsserver und beliebige Komponenten sowie zum Speichern des Status bei Verwendung von caching verwendet werden. Eclipse verwaltet eine Liste der bekannten Speicherkonten, die für Ihre Projekte in Ihrem Eclipse-Arbeitsbereich verfügbar sind. So öffnen die **Speicherkonten** Dialogfeld dient zum Verwalten der Liste wird in Eclipse, klicken Sie auf **Fenster**, klicken Sie auf **Voreinstellungen**, erweitern Sie **Azure**, und klicken Sie dann auf **Speicherkonten**.

Im folgenden gezeigt die **Speicherkonten** Dialogfeld.

![][ic719496]

Dieses Dialogfeld kann auch geöffnet werden, aus einer **Konten** -Link in Dialogfeldern, die Speicherkonten, wie die folgende verwenden:

* Die **JDK** auf der Registerkarte die **Serverkonfiguration** Dialogfeld.
* Die **Server** auf der Registerkarte die **Serverkonfiguration** Dialogfeld.
* Die **Komponente hinzufügen** Dialogfeld.
* Die **Caching** Dialogfeld "Eigenschaften".

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a>So importieren Sie Ihre Speicherkonten mithilfe einer Datei mit veröffentlichungseinstellungen
1. Innerhalb der **Speicherkonten** Dialogfeld klicken Sie auf **Import from PUBLISH-SETTINGS File**.

2. (Überspringen Sie diesen Schritt aus, wenn Sie bereits eine Datei mit veröffentlichungseinstellungen auf Ihrem lokalen Computer gespeichert haben.) In der **Import Subscription Information** Dialogfeld klicken Sie auf **Download PUBLISH-SETTINGS File**. Wenn Sie noch nicht in Ihrem Azure-Konto angemeldet sind, werden Sie aufgefordert, um sich anzumelden. Klicken Sie dann werden Sie aufgefordert, speichern Sie eine Azure Einstellungsdatei veröffentlichen. (Sie können die resultierenden Anweisungen auf den Anmeldeseiten - ignorieren sie über das Azure-Portal bereitgestellt werden und für Visual Studio-Benutzer vorgesehen sind.) Speichern Sie es auf Ihrem lokalen Computer.

3. Immer noch in der **Import Subscription Information** Dialogfeld klicken Sie auf die **Durchsuchen** Schaltfläche auswählen, die Sie zuvor lokal gespeicherte Datei mit den veröffentlichungseinstellungen, und klicken Sie dann auf **öffnen**.

4. Klicken Sie auf **OK** schließen die **Import Subscription Information** Dialogfeld.

## <a name="to-create-a-new-storage-account"></a>Um ein neues Speicherkonto erstellen
1. Innerhalb der **Speicherkonten** Dialogfeld klicken Sie auf **hinzufügen**.

2. Innerhalb der **Add Storage Account** Dialogfeld klicken Sie auf **neu**.

3. Innerhalb der **New Storage Account** Dialogfeld, geben Sie Werte für Folgendes:

   * Name des Speicherkontos.

   * Der Speicherort des Speicherkontos.

   * Beschreibung des Speicherkontos.

   * Das Abonnement, zu dem das Speicherkonto gehört.

4. Klicken Sie auf **OK** schließen die **New Storage Account** Dialogfeld.

Es kann mehrere Minuten für Ihr Speicherkonto erstellt werden soll. Nachdem sie erstellt wurde, klicken Sie auf **OK** schließen die **Add Storage Account** Dialogfeld und das neue Speicherkonto wird die Liste der verfügbaren Speicherkonten hinzugefügt werden.

## <a name="to-add-an-existing-storage-account-to-the-list"></a>Die Liste ein vorhandenes Speicherkonto hinzu
1. Wenn Sie nicht bereits über ein Azure Storage-Konto verfügen, erstellen Sie ein solches anhand der Schritte in der **So erstellen einen neuen Abschnitt "Speicher-Konto"** oben. (Alternativ können Sie ein neues Speicherkonto erstellen die [Azure-Verwaltungsportal][Azure Management Portal].)

2. Innerhalb der **Speicherkonten** Dialogfeld klicken Sie auf **hinzufügen**.

3. Innerhalb der **Add Storage Account** Dialogfeld, geben Sie Werte für **Namen** und **Zugriffsschlüssel**. Das Konto und den Zugriffsschlüssel muss für einen vorhandenen Azure Storage-Konto sein. Verwenden der **Speicher** Teil der [Azure-Verwaltungsportal] [ Azure Management Portal] Ihren speicherkontonamen und Schlüssel anzeigen. Ihre **Add Storage Account** Dialogfeld sieht etwa wie folgt.
   
   ![][ic719497]

4. Klicken Sie auf **OK** schließen die **Add Storage Account** Dialogfeld.

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a>So ändern Sie ein Speicherkonto, um einen neuen Zugriffsschlüssel zu verwenden.
1. Innerhalb der **Speicherkonten** Dialogfeld, auf das Speicherkonto an, die Sie bearbeiten möchten, und klicken Sie dann auf **bearbeiten**.

2. Innerhalb der **Edit Storage Account Access Key** im Dialogfeld ändern Sie die **Zugriffsschlüssel** Wert.

3. Klicken Sie auf **OK** schließen die **Edit Storage Account Access Key** Dialogfeld.

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a>So entfernen Sie ein Speicherkonto, das aus der in Eclipse verwalteten Liste
1. Innerhalb der **Speicherkonten** Dialogfeld, auf das Speicherkonto an, die Sie bearbeiten möchten, und klicken Sie dann auf **entfernen**.

2. Klicken Sie auf **OK** bei der Aufforderung zum Entfernen des Speicherkontos.

> [!NOTE]
> Entfernen das Speicherkonto, das über die **Speicherkonten** Dialogfeld entfernt ihn nur aus der Liste der Speicherkonten in Eclipse angezeigt werden kann. Es ist nicht das Speicherkonto aus Ihrem Azure-Abonnement entfernen. Darüber hinaus konnte das Speicherkonto erneut in der Liste angezeigt, wenn Eclipse die Details Ihres Abonnements neu geladen.
> 
> 

## <a name="see-also"></a>Siehe auch
[Azure-Toolkit für Eclipse][Azure Toolkit for Eclipse]

[Installieren des Azure-Toolkits für Eclipse][Installing the Azure Toolkit for Eclipse] 

[Erstellen einer Hello World-Anwendung für Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter der [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
