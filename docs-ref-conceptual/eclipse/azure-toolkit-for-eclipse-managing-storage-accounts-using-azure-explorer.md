---
title: "Verwalten von Speicherkonten mithilfe von Azure-Explorer für Eclipse"
description: "Erfahren Sie, wie Sie Ihre Azure Storage-Konten mit Azure-Explorer für Eclipse verwalten."
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
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: da08893abb6dc57083927ac3a90341f05dd9cfa9
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="b937b-103">Verwalten von Speicherkonten mithilfe von Azure-Explorer für Eclipse</span><span class="sxs-lookup"><span data-stu-id="b937b-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="b937b-104">Der Azure-Explorer gehört zum Azure-Toolkit für Eclipse und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von Speicherkonten in ihrem Azure-Konto innerhalb der integrierten Entwicklungsumgebung (IDE) von Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b937b-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="b937b-105">Erstellen eines Speicherkontos in Eclipse</span><span class="sxs-lookup"><span data-stu-id="b937b-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="b937b-106">Gehen Sie folgendermaßen vor, um ein Speicherkonto mit dem Azure-Explorer zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="b937b-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="b937b-107">Melden Sie sich beim Azure-Konto gemäß den Anweisungen unter [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse] an.</span><span class="sxs-lookup"><span data-stu-id="b937b-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

1. <span data-ttu-id="b937b-108">Erweitern Sie in der Ansicht des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Speicherkonten**, und klicken Sie dann auf **Speicherkonto erstellen**.</span><span class="sxs-lookup"><span data-stu-id="b937b-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Befehl „Speicherkonto erstellen“][CS01]

1. <span data-ttu-id="b937b-110">Geben Sie im Dialogfeld **Speicherkonto erstellen** folgende Details an:</span><span class="sxs-lookup"><span data-stu-id="b937b-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Dialogfeld „Neues Speicherkonto erstellen“][CS02]

   * <span data-ttu-id="b937b-112">**Name:** Geben Sie den Namen des neuen Speicherkontos an.</span><span class="sxs-lookup"><span data-stu-id="b937b-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="b937b-113">**Abonnement:** Geben Sie das Azure-Abonnement an, das Sie für das neue Speicherkonto verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="b937b-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="b937b-114">**Ressourcengruppe:** Geben Sie die Ressourcengruppe für Ihren virtuellen Computer an.</span><span class="sxs-lookup"><span data-stu-id="b937b-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="b937b-115">Wählen Sie eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="b937b-115">Select one of the following options:</span></span>
      * <span data-ttu-id="b937b-116">**Create New**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="b937b-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="b937b-117">**Vorhandene verwenden:** Geben Sie an, dass Sie in einer Liste von Ressourcengruppen, die Ihrem Azure-Konto zugeordnet sind, eine Auswahl treffen möchten.</span><span class="sxs-lookup"><span data-stu-id="b937b-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="b937b-118">**Standort:** Geben Sie den Standort an, an dem Ihr Speicherkonto erstellt wird, z.B. „USA, Westen“.</span><span class="sxs-lookup"><span data-stu-id="b937b-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="b937b-119">**Kontoart:** Geben Sie den Typ des zu erstellenden Speicherkontos an (z.B. „Blob-Speicher“).</span><span class="sxs-lookup"><span data-stu-id="b937b-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="b937b-120">Weitere Informationen finden Sie unter [Informationen zu Azure-Speicherkonten].</span><span class="sxs-lookup"><span data-stu-id="b937b-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="b937b-121">**Leistung:** Geben Sie an, welches Speicherkontoangebot vom ausgewählten Herausgeber verwendet werden soll (z.B. „Premium“).</span><span class="sxs-lookup"><span data-stu-id="b937b-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="b937b-122">Weitere Informationen finden Sie unter [Skalierbarkeits- und Leistungsziele für Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="b937b-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="b937b-123">**Replikation**: Gibt die Replikation des Speicherkontos an (z.B. „zonenredundant“).</span><span class="sxs-lookup"><span data-stu-id="b937b-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="b937b-124">Weitere Informationen finden Sie unter [Azure-Speicherreplikation].</span><span class="sxs-lookup"><span data-stu-id="b937b-124">For more information, see [Azure storage replication].</span></span>

1. <span data-ttu-id="b937b-125">Nachdem Sie alle vorhergehenden Optionen angegeben haben, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="b937b-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="b937b-126">Erstellen eines Speichercontainers in Eclipse</span><span class="sxs-lookup"><span data-stu-id="b937b-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="b937b-127">Gehen Sie folgendermaßen vor, um einen Speichercontainer mit dem Azure-Explorer zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="b937b-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="b937b-128">Klicken Sie in der **Azure-Explorer**-Ansicht mit der rechten Maustaste auf das Speicherkonto, in dem Sie einen Container erstellen möchten, und klicken Sie dann auf **Blobcontainer erstellen**.</span><span class="sxs-lookup"><span data-stu-id="b937b-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Befehl „Blobcontainer erstellen“][CC01]

1. <span data-ttu-id="b937b-130">Geben Sie im Dialogfeld **Blobcontainer erstellen** den Namen für Ihren Container ein, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b937b-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="b937b-131">Weitere Informationen zum Benennen von Speichercontainern finden Sie unter [Benennen von Containern, Blobs und Metadaten und Verweisen auf diese].</span><span class="sxs-lookup"><span data-stu-id="b937b-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Dialogfeld „Blobcontainer erstellen“][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="b937b-133">Löschen eines Speichercontainers in Eclipse</span><span class="sxs-lookup"><span data-stu-id="b937b-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="b937b-134">Gehen Sie folgendermaßen vor, um einen Speichercontainer mit dem Azure-Explorer zu löschen:</span><span class="sxs-lookup"><span data-stu-id="b937b-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="b937b-135">Klicken Sie in der **Azure-Explorer**-Ansicht mit der rechten Maustaste auf den Speichercontainer, und klicken Sie dann auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="b937b-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![Befehl „Speichercontainer löschen“][DC01]

1. <span data-ttu-id="b937b-137">Klicken Sie im Bestätigungsfenster auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b937b-137">In the confirmation window, click **OK**.</span></span>

   ![Bestätigungsfenster für „Speichercontainer löschen“][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="b937b-139">Löschen eines Speicherkontos in Eclipse</span><span class="sxs-lookup"><span data-stu-id="b937b-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="b937b-140">Gehen Sie folgendermaßen vor, um ein Speicherkonto mit dem Azure-Explorer zu löschen:</span><span class="sxs-lookup"><span data-stu-id="b937b-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="b937b-141">Klicken Sie in der **Azure-Explorers**-Ansicht mit der rechten Maustaste auf das Speicherkonto, und klicken Sie dann auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="b937b-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![Befehl „Speicherkonto löschen“][DS01]

1. <span data-ttu-id="b937b-143">Klicken Sie im Bestätigungsfenster auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="b937b-143">In the confirmation window, click **OK**.</span></span>

   ![Bestätigungsfenster für „Speicherkonto löschen“][DS02]

## <a name="next-steps"></a><span data-ttu-id="b937b-145">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="b937b-145">Next steps</span></span>

<span data-ttu-id="b937b-146">Weitere Informationen zu Azure Storage-Konten sowie Größen und Preisen finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="b937b-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="b937b-147">[Einführung in Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="b937b-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="b937b-148">[Informationen zu Azure-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="b937b-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="b937b-149">Größen für Azure Storage-Konten</span><span class="sxs-lookup"><span data-stu-id="b937b-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="b937b-150">[Größen für Windows-Speicherkonten in Azure]</span><span class="sxs-lookup"><span data-stu-id="b937b-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="b937b-151">[Größen für Linux-Speicherkonten in Azure]</span><span class="sxs-lookup"><span data-stu-id="b937b-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="b937b-152">Preise von Azure Storage-Konten</span><span class="sxs-lookup"><span data-stu-id="b937b-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="b937b-153">[Preise von Windows-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="b937b-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="b937b-154">[Preise von Linux-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="b937b-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Einführung in Microsoft Azure Storage]: /azure/storage/storage-introduction
[Informationen zu Azure-Speicherkonten]: /azure/storage/storage-create-storage-account
[Azure-Speicherreplikation]: /azure/storage/storage-redundancy
[Skalierbarkeits- und Leistungsziele für Azure Storage]: /azure/storage/storage-scalability-targets
[Benennen von Containern, BLOBs und Metadaten und Verweisen auf diese]: http://go.microsoft.com/fwlink/?LinkId=255555

[Größen für Windows-Speicherkonten in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Größen für Linux-Speicherkonten in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preise von Windows-Speicherkonten]: /pricing/details/virtual-machines/windows/
[Preise von Linux-Speicherkonten]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
