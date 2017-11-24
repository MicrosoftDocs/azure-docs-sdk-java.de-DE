---
title: Bereitstellen umfangreicher Bereitstellungen
description: "Erfahren Sie mehr über das Bereitstellen umfangreicher Bereitstellungen mit dem Azure-Toolkit für Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 0e367e74d038043f1626dbf19aab87db6451bc02
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2017
---
# <a name="deploying-large-deployments"></a>Bereitstellen umfangreicher Bereitstellungen

Falls die Bereitstellung zu groß für den Standardordner „approot“ ist, kann eine lokale Speicherressource als Stammordner der Bereitstellung für das JDK und den Anwendungsserver verwendet werden.

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>So verwenden Sie eine lokale Speicherressource als Stammordner für große Bereitstellungen

1. Erstellen Sie zunächst eine lokale Speicherressource. Der Name dieser Ressource ist unwichtig. Speicherressourcen werden auf Rollenebene definiert. Die schnellste Möglichkeit zum Aufrufen des Dialogfelds für das Konfigurieren von lokalem Speicher, in dem eine neue lokale Speicherressource erstellt werden kann, besteht in folgenden Schritten: Klicken Sie in der Ansicht **Projekt-Explorer** mit der rechten Maustaste auf die Rolle (erweitern Sie den Azure-Projektknoten, wenn die Rolle nicht angezeigt wird), und klicken Sie auf **Azure** und dann auf **Lokaler Speicher**. Klicken Sie im Dialogfeld **Lokaler Speicher** auf **Hinzufügen**, um eine neue lokale Speicherressource zu erstellen.

1. Legen Sie die gewünschte Größe auf mindestens 2.048 MB fest (eine geringere Größe kann zu denselben Dateigrößenproblemen wie im Ordner „approot“ führen.)

1. Achten Sie darauf, dass das Kontrollkästchen **Clean the contents when the role instance is recycled** (Inhalte bei Wiederverwendung der Rolleninstanz löschen) aktiviert ist. Dadurch wird verhindert, dass die Startlogik für die Bereitstellung in Konflikt mit vorhandenen Dateien in der Ressource gerät, wenn die Rolleninstanz wiederverwendet wird.

1. Achten Sie darauf, dass der Wert von **Environment variable storing the resource's directory path after deployment** (Umgebungsvariable, die nach der Bereitstellung den Verzeichnispfad der Ressource speichert) auf die Zeichenfolge **DEPLOYROOT** festgelegt ist. Das Dialogfeld Ihrer lokalen Speicherressource sieht ungefähr folgendermaßen aus.

   ![][ic667943]

Wenn Sie **DEPLOYROOT** für das Feld *Name* Ihrer lokalen Ressource verwenden und den Namen der automatisch generierten Umgebungsvariablen nicht ändern (die in diesem Fall auf **DEPLOYROOT_PATH** festgelegt wird), funktioniert Ihre Anwendung auch.

Weitere Informationen zum Erstellen einer lokalen Speicherressource finden Sie unter [Eigenschaften für lokalen Speicher][Local storage properties].

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
