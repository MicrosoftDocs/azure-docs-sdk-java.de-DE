---
title: "Aktivieren der Sitzungsaffinität mit dem Azure-Toolkit für Eclipse"
description: "Erfahren Sie, wie mit dem Azure-Toolkit für Eclipse sitzungsaffinität zu aktivieren."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a>Aktivieren der Sitzungsaffinität
Im Azure-Toolkit für Eclipse können Sie die HTTP-sitzungsaffinität oder "persistente Sitzungen" für Ihre Rollen aktivieren. Die folgende Abbildung zeigt die **Lastenausgleich** Eigenschaftendialogfeld verwendet, um die sitzungsaffinitätsfunktion aktiviert:

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a>So aktivieren Sie die sitzungsaffinität für Ihre Rolle
1. Mit der rechten Maustaste in der Rolle im Projektexplorer von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Lastenausgleich**.

2. In der **Eigenschaften for WorkerRole1 Load Balancing** Dialogfeld:

   a. Überprüfen Sie **aktivieren Sie HTTP-sitzungsaffinität (sticky Sessions) für diese Rolle.**

   b. Für **Eingabeendpunkt mit**, wählen Sie einen eingangsendpunkt verwenden, z. B. **http (Public: 80, Private: 8080)**. Die Anwendung muss diesen Endpunkt als HTTP-Endpunkt verwendet. Sie können mehrere Endpunkte für Ihre Rolle aktivieren, aber Auszuwählender nur einer von ihnen persistente Sitzungen zu unterstützen.

   c. Erstellen Sie die Anwendung neu.

Nach der Aktivierung, wenn Sie mehrere Rolleninstanzen verfügen, werden von einem bestimmten Client stammende HTTP-Anforderungen weiterhin von derselben Rolleninstanz behandelt wird.

Das Eclipse-Toolkit ermöglicht dies durch Installieren eines speziellen IIS-Moduls namens Application Request Routing (ARR) in jeder der Rolleninstanzen. ARR leitet HTTP-Anforderungen an die entsprechende Rolleninstanz. Das Toolkit konfiguriert automatisch den ausgewählten Endpunkt, damit der eingehende HTTP-Datenverkehr zunächst an die ARR-Software weitergeleitet wird. Das Toolkit erstellt außerdem einen neuen internen Endpunkt, die Ihr Java-Server zum Abhören konfiguriert ist. Dies ist der Endpunkt, der von ARR verwendet, um den HTTP-Datenverkehr an die entsprechende Rolleninstanz umgeleitet. Auf diese Weise fungiert jede Rolleninstanz in der mehrinstanzbereitstellung als Reverseproxy für alle anderen Instanzen, wodurch persistente Sitzungen aktiviert.

## <a name="notes-about-session-affinity"></a>Hinweise zur sitzungsaffinität
* Sitzungsaffinität funktioniert nicht im Serveremulator. Die Einstellungen im Serveremulator angewendet werden können, ohne Beeinträchtigung des Buildprozesses oder compute Emulator ausführen, aber die Funktion selbst funktioniert im Serveremulator nicht.

* Aktivieren der sitzungsaffinität führt zu einer Erhöhung hinsichtlich der Menge an Speicherplatz beanspruchen von Ihrer Bereitstellung in Azure, wie zusätzlicher Software heruntergeladen und in Ihren Rolleninstanzen installiert werden, wenn der Dienst in der Azure-Cloud gestartet wird.

* Die Zeit für die Initialisierung der einzelnen Rollen dauert länger.

* Ein interner Endpunkt als eine Datenverkehr Rerouter funktioniert, wie bereits erwähnt, werden hinzugefügt.


## <a name="see-also"></a>Siehe auch
[Azure-Toolkit für Eclipse][Azure Toolkit for Eclipse]

[Erstellen einer Hello World-Anwendung für Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Installieren des Azure-Toolkits für Eclipse][Installing the Azure Toolkit for Eclipse] 

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter der [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
