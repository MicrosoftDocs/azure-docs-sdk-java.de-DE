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
# <a name="deploying-large-deployments"></a><span data-ttu-id="1f055-103">Bereitstellen umfangreicher Bereitstellungen</span><span class="sxs-lookup"><span data-stu-id="1f055-103">Deploying Large Deployments</span></span>

<span data-ttu-id="1f055-104">Falls die Bereitstellung zu groß für den Standardordner „approot“ ist, kann eine lokale Speicherressource als Stammordner der Bereitstellung für das JDK und den Anwendungsserver verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1f055-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="1f055-105">So verwenden Sie eine lokale Speicherressource als Stammordner für große Bereitstellungen</span><span class="sxs-lookup"><span data-stu-id="1f055-105">To use a local storage resource as the deployment root folder for large deployments</span></span>

1. <span data-ttu-id="1f055-106">Erstellen Sie zunächst eine lokale Speicherressource.</span><span class="sxs-lookup"><span data-stu-id="1f055-106">Create a new local storage resource.</span></span> <span data-ttu-id="1f055-107">Der Name dieser Ressource ist unwichtig.</span><span class="sxs-lookup"><span data-stu-id="1f055-107">The name of the resource does not matter.</span></span> <span data-ttu-id="1f055-108">Speicherressourcen werden auf Rollenebene definiert.</span><span class="sxs-lookup"><span data-stu-id="1f055-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="1f055-109">Die schnellste Möglichkeit zum Aufrufen des Dialogfelds für das Konfigurieren von lokalem Speicher, in dem eine neue lokale Speicherressource erstellt werden kann, besteht in folgenden Schritten: Klicken Sie in der Ansicht **Projekt-Explorer** mit der rechten Maustaste auf die Rolle (erweitern Sie den Azure-Projektknoten, wenn die Rolle nicht angezeigt wird), und klicken Sie auf **Azure** und dann auf **Lokaler Speicher**.</span><span class="sxs-lookup"><span data-stu-id="1f055-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="1f055-110">Klicken Sie im Dialogfeld **Lokaler Speicher** auf **Hinzufügen**, um eine neue lokale Speicherressource zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1f055-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>

1. <span data-ttu-id="1f055-111">Legen Sie die gewünschte Größe auf mindestens 2.048 MB fest (eine geringere Größe kann zu denselben Dateigrößenproblemen wie im Ordner „approot“ führen.)</span><span class="sxs-lookup"><span data-stu-id="1f055-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>

1. <span data-ttu-id="1f055-112">Achten Sie darauf, dass das Kontrollkästchen **Clean the contents when the role instance is recycled** (Inhalte bei Wiederverwendung der Rolleninstanz löschen) aktiviert ist. Dadurch wird verhindert, dass die Startlogik für die Bereitstellung in Konflikt mit vorhandenen Dateien in der Ressource gerät, wenn die Rolleninstanz wiederverwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1f055-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>

1. <span data-ttu-id="1f055-113">Achten Sie darauf, dass der Wert von **Environment variable storing the resource's directory path after deployment** (Umgebungsvariable, die nach der Bereitstellung den Verzeichnispfad der Ressource speichert) auf die Zeichenfolge **DEPLOYROOT** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="1f055-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="1f055-114">Das Dialogfeld Ihrer lokalen Speicherressource sieht ungefähr folgendermaßen aus.</span><span class="sxs-lookup"><span data-stu-id="1f055-114">Your local storage resource dialog will look similar to the following.</span></span>

   ![][ic667943]

<span data-ttu-id="1f055-115">Wenn Sie **DEPLOYROOT** für das Feld *Name* Ihrer lokalen Ressource verwenden und den Namen der automatisch generierten Umgebungsvariablen nicht ändern (die in diesem Fall auf **DEPLOYROOT_PATH** festgelegt wird), funktioniert Ihre Anwendung auch.</span><span class="sxs-lookup"><span data-stu-id="1f055-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="1f055-116">Weitere Informationen zum Erstellen einer lokalen Speicherressource finden Sie unter [Eigenschaften für lokalen Speicher][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="1f055-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f055-117">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="1f055-117">Next steps</span></span>

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
