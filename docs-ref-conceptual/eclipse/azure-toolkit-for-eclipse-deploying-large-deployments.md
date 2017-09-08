---
title: Bereitstellen umfangreicher Bereitstellungen
description: "Informationen Sie zum Bereitstellen von großer Bereitstellungen mit dem Azure-Toolkit für Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: e12e379e2b6727653e2377b1760c3745596a1e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2017
---
# <a name="deploying-large-deployments"></a>Bereitstellen umfangreicher Bereitstellungen
Wenn Ihre Bereitstellung zu groß, um in den Approot-Standardordner enthalten sein wird, können Sie eine lokale Speicherressource als Stammordner der Bereitstellung für Ihren JDK- und Anwendungsserver.

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>Um eine lokale Speicherressource als Stammordner der Bereitstellung für große Bereitstellungen zu verwenden.
1. Erstellen Sie eine neue lokale Speicherressource. Der Name der Ressource spielt keine Rolle. Speicherressourcen werden auf Rollenebene definiert. Das Konfigurationsdialogfeld des lokalen Speicher zugreifen, von dem Sie eine neue lokale Speicherressource erstellen konnte, am schnellsten mithilfe der folgenden Schritte wird: mit der rechten Maustaste in der Rolle in der **Projektexplorer** Ansicht (erweitern Ihre Azure-Projekt-Knoten aus, wenn Sie die Rolle nicht angezeigt), klicken Sie auf **Azure**, und klicken Sie dann auf **lokalen Speicher**. Innerhalb der **lokalen Speicher** Dialogfeld klicken Sie auf **hinzufügen** um eine neue lokale Speicherressource zu erstellen.

2. Legen Sie die gewünschte Größe auf mindestens 2048 MB (etwas weniger dieselbe Datei Größe Probleme verursachen wie dateigrößenproblemen im Ordner Approot).

3. Sicherstellen, dass **Inhalt bereinigen, wenn die Rolleninstanz wiederverwendet wird** aktiviert ist; dadurch wird verhindert, dass die Startlogik für die Bereitstellung in Konflikt mit vorhandenen Dateien in der Ressource ausgeführt, wenn die Rolleninstanz wiederverwendet wird.

4. Sicherstellen, dass die **Umgebungsvariable zum Speichern der Verzeichnispfad für die Ressource nach der Bereitstellung** Wert wird festgelegt, auf die Zeichenfolge **DEPLOYROOT**. Ihre lokalen Speicher das Dialogfeld sieht etwa wie folgt aus.

   ![][ic667943]

Alternativ können Sie bei Verwendung von **DEPLOYROOT** als die *Namen* Ihrer lokalen Ressource und ändern Sie nicht den Namen der automatisch generierten Umgebungsvariablen (dem festgelegt, um **DEPLOYROOT_PATH** in diesem Fall), würde, die für Ihre Anwendung auch funktionieren.

Weitere Informationen zum Erstellen einer lokalen Speicherressource finden Sie unter [Eigenschaften des lokalen Speichers][Local storage properties].

## <a name="see-also"></a>Siehe auch
[Azure-Toolkit für Eclipse][Azure Toolkit for Eclipse]

[Erstellen einer Hello World-Anwendung für Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Installieren des Azure-Toolkits für Eclipse][Installing the Azure Toolkit for Eclipse] 

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter der [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
