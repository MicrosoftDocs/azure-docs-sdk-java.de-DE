---
title: Azure-Dienstendpunkte
description: "Beschreibt die Azure-Dienstendpunkt-Einstellungen im Azure-Toolkit für Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a>Azure-Dienstendpunkte
Azure-Dienstendpunkte bestimmen, ob Ihre Anwendung bereitgestellt und von der globalen Azure-Plattform verwaltet werden, von Azure 21Vianet in China oder einer privaten Azure-Plattform. Die **Dienstendpunkte** Dialogfeld können Sie Dienstendpunkte angeben, Sie verwenden möchten. So öffnen die **Dienstendpunkte** Dialogfeld in Eclipse, klicken Sie auf **Fenster**, klicken Sie auf **Voreinstellungen**, erweitern Sie **Azure**, und klicken Sie dann auf **Dienstendpunkte**. Festlegen der **Active Set** Feld bestimmt, welche Azure-Dienstendpunkte für die Azure-Projekte in Ihrem aktuellen Arbeitsbereich verwendet werden soll.

Im folgenden gezeigt die **Dienstendpunkte** Dialogfeld.

![][ic719493]

## <a name="to-set-the-service-endpoints"></a>Die Dienstendpunkte fest
In der **Dienstendpunkte** Dialogfeld, eine der folgenden Aktionen:

* Wenn Sie aus die globalen Azure-Plattform verwenden möchten die **Active Set** Dropdownliste **windowsazure.com** , und klicken Sie auf **OK**.

* Wenn Sie Azure bei Betrieb über 21Vianet in China aus verwenden möchten die **Active Set** Dropdownliste **windowsazure.cn (China)** , und klicken Sie auf **OK**.

* Wenn Sie eine private Azure-Plattform verwenden möchten:

  1. Klicken Sie auf **Bearbeiten**.

  2. Ein Dialogfeld geöffnet wird, informiert Sie darüber, die die **Dienstendpunkte** Dialogfeld wird geschlossen, und die Datei wird geöffnet. Klicken Sie auf **OK**.

  3. Erstellen Sie in der Datei "preferencesets.xml" ein neues `preferenceset` Element. Erstellen Sie für dieses neue Element `name`, `blob`, `management`, `portalURL` und `publishsettings` Attribute und Werte dafür entsprechen, Ihrer privaten Azure-Plattform hinzufügen. Können Sie die Werte für die vorhandene `preferenceset` Elemente wie Vorlagen. **Hinweis**: der Wert für die `blob` Attribut muss den Text "Blob" in der URL enthalten.

  4. Speichern Sie und schließen Sie "preferencesets.xml".

  5. Öffnen Sie erneut die **Dienstendpunkte** Dialogfeld.

  6. Aus der **Active Set** Dropdown-Liste, wählen Sie das aktive set aus, die Sie erstellt haben, und klicken Sie auf **OK**.

  7. Nach der Erstellung Ihrer privaten Azure-Plattform `preferenceset` Element, ändern Sie die Werte zugewiesen, indem Sie auf die **bearbeiten** Schaltfläche der **-Dienstendpunkt** Dialogfeld. Sie können auch mehrere private Azure-Plattform erstellen `preferenceset` Elemente, wenn Sie Arbeit am PC versprechen.

## <a name="see-also"></a>Siehe auch
[Azure-Toolkit für Eclipse][Azure Toolkit for Eclipse]

[Installieren des Azure-Toolkits für Eclipse][Installing the Azure Toolkit for Eclipse] 

[Erstellen einer Hello World-Anwendung für Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter der [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
