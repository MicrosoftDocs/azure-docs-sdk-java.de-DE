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
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="8935f-103">Verwalten von Speicherkonten mithilfe von Azure-Explorer für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8935f-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="8935f-104">Der Azure-Explorer gehört zum Azure-Toolkit für IntelliJ und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von Speicherkonten in ihrem Azure-Konto innerhalb der integrierten Entwicklungsumgebung (IDE) von IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8935f-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="8935f-105">Erstellen eines Speicherkontos in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8935f-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="8935f-106">Gehen Sie folgendermaßen vor, um ein Speicherkonto mit dem Azure-Explorer zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="8935f-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="8935f-107">Melden Sie sich beim Azure-Konto gemäß den Anweisungen in [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ] an.</span><span class="sxs-lookup"><span data-stu-id="8935f-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for IntelliJ].</span></span> 

2. <span data-ttu-id="8935f-108">Erweitern Sie in der Ansicht des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Speicherkonten**, und klicken Sie dann auf **Speicherkonto erstellen**.</span><span class="sxs-lookup"><span data-stu-id="8935f-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Befehl „Speicherkonto erstellen“][CS01]

3. <span data-ttu-id="8935f-110">Geben Sie im Dialogfeld **Speicherkonto erstellen** folgende Details an:</span><span class="sxs-lookup"><span data-stu-id="8935f-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Dialogfeld „Neues Speicherkonto erstellen“][CS02]

   * <span data-ttu-id="8935f-112">**Name:** Geben Sie den Namen des neuen Speicherkontos an.</span><span class="sxs-lookup"><span data-stu-id="8935f-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="8935f-113">**Kontoart:** Geben Sie den Typ des zu erstellenden Speicherkontos an (z.B. „Blob Storage“).</span><span class="sxs-lookup"><span data-stu-id="8935f-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="8935f-114">Weitere Informationen finden Sie unter [Informationen zu Azure-Speicherkonten].</span><span class="sxs-lookup"><span data-stu-id="8935f-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="8935f-115">**Leistung:** Geben Sie an, welches Speicherkontoangebot vom ausgewählten Herausgeber verwendet werden soll (z.B. „Premium“).</span><span class="sxs-lookup"><span data-stu-id="8935f-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="8935f-116">Weitere Informationen finden Sie unter [Skalierbarkeits- und Leistungsziele für Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="8935f-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="8935f-117">**Replikation**: Gibt die Replikation des Speicherkontos an (z.B. „zonenredundant“).</span><span class="sxs-lookup"><span data-stu-id="8935f-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="8935f-118">Weitere Informationen finden Sie unter [Azure-Speicherreplikation].</span><span class="sxs-lookup"><span data-stu-id="8935f-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="8935f-119">**Abonnement:** Wählen Sie das Azure-Abonnement aus, das Sie für das neue Speicherkonto verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="8935f-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="8935f-120">**Ort**: Gibt den Speicherort an, an dem Ihr Speicherkonto erstellt wird (z.B. USA, Westen).</span><span class="sxs-lookup"><span data-stu-id="8935f-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="8935f-121">**Ressourcengruppe:** Gibt die Ressourcengruppe für Ihren virtuellen Computer an.</span><span class="sxs-lookup"><span data-stu-id="8935f-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="8935f-122">Wählen Sie eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="8935f-122">Select one of the following options:</span></span>
      * <span data-ttu-id="8935f-123">**Neu erstellen**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="8935f-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="8935f-124">**Vorhandene verwenden**: Gibt an, dass Sie in einer Liste von Ressourcengruppen, die Ihrem Azure-Konto zugeordnet sind, eine Auswahl treffen möchten.</span><span class="sxs-lookup"><span data-stu-id="8935f-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="8935f-125">Nachdem Sie alle vorstehenden Optionen angegeben haben, klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8935f-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="8935f-126">Erstellen eines Speichercontainers in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8935f-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="8935f-127">Gehen Sie folgendermaßen vor, um einen Speichercontainer mit dem Azure-Explorer zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="8935f-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="8935f-128">Klicken Sie in der Azure-Exploreransicht mit der rechten Maustaste auf das Speicherkonto, in dem Sie einen Container erstellen möchten, und klicken Sie dann auf **Blobcontainer erstellen**.</span><span class="sxs-lookup"><span data-stu-id="8935f-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Befehl „Blobcontainer erstellen“][CC01]

2. <span data-ttu-id="8935f-130">Geben Sie im Dialogfeld **Blobcontainer erstellen** den Namen für Ihren Container ein, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8935f-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="8935f-131">Weitere Informationen zum Benennen von Speichercontainern finden Sie unter [Benennen von Containern, Blobs und Metadaten und Verweisen auf diese].</span><span class="sxs-lookup"><span data-stu-id="8935f-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Dialogfeld „Speichercontainer erstellen“][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="8935f-133">Löschen eines Speichercontainers in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8935f-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="8935f-134">Gehen Sie folgendermaßen vor, um einen Speichercontainer mit dem Azure-Explorer zu löschen:</span><span class="sxs-lookup"><span data-stu-id="8935f-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="8935f-135">Klicken Sie in der Azure-Exploreransicht mit der rechten Maustaste auf den Speichercontainer, und klicken Sie dann auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="8935f-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Befehl „Speichercontainer löschen“][DC01]

2. <span data-ttu-id="8935f-137">Klicken Sie im Bestätigungsfenster auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="8935f-137">In the confirmation window, click **Yes**.</span></span>

   ![Bestätigungsfenster für „Speichercontainer löschen“][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="8935f-139">Löschen eines Speicherkontos in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8935f-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="8935f-140">Gehen Sie folgendermaßen vor, um ein Speicherkonto mit dem Azure-Explorer zu löschen:</span><span class="sxs-lookup"><span data-stu-id="8935f-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="8935f-141">Klicken Sie in der Ansicht des **Azure-Explorers** mit der rechten Maustaste auf das Speicherkonto, und wählen Sie dann **Löschen** aus.</span><span class="sxs-lookup"><span data-stu-id="8935f-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Menü „Speicherkonto löschen“][DS01]

2. <span data-ttu-id="8935f-143">Klicken Sie im Bestätigungsfenster auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="8935f-143">In the confirmation window, click **Yes**.</span></span>

   ![Bestätigungsfenster für „Speicherkonto löschen“][DS02]

## <a name="next-steps"></a><span data-ttu-id="8935f-145">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="8935f-145">Next steps</span></span>

<span data-ttu-id="8935f-146">Weitere Informationen zu Azure Storage-Konten sowie Größen und Preisen finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="8935f-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="8935f-147">[Einführung in Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="8935f-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="8935f-148">[Informationen zu Azure-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="8935f-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="8935f-149">Größen für Azure Storage-Konten</span><span class="sxs-lookup"><span data-stu-id="8935f-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="8935f-150">[Größen für Windows-Speicherkonten in Azure]</span><span class="sxs-lookup"><span data-stu-id="8935f-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="8935f-151">[Größen für Linux-Speicherkonten in Azure]</span><span class="sxs-lookup"><span data-stu-id="8935f-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="8935f-152">Preise von Azure Storage-Konten</span><span class="sxs-lookup"><span data-stu-id="8935f-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="8935f-153">[Preise von Windows-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="8935f-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="8935f-154">[Preise von Linux-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="8935f-154">[Linux storage-account pricing]</span></span>

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
