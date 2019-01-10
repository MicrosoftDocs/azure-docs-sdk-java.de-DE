---
title: Verwalten von Speicherkonten mithilfe von Azure-Explorer für Eclipse
description: Erfahren Sie, wie Sie Ihre Azure Storage-Konten mit Azure-Explorer für Eclipse verwalten.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: dc39298d88f2fb0b2f56d6fbc0071b68b8d27989
ms.sourcegitcommit: 24f037d133875f86761ec893dfa74e723de040b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2018
ms.locfileid: "53636656"
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="58c94-103">Verwalten von Speicherkonten mithilfe von Azure-Explorer für Eclipse</span><span class="sxs-lookup"><span data-stu-id="58c94-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="58c94-104">Der Azure-Explorer gehört zum Azure-Toolkit für Eclipse und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von Speicherkonten in ihrem Azure-Konto innerhalb der integrierten Entwicklungsumgebung (IDE) von Eclipse.</span><span class="sxs-lookup"><span data-stu-id="58c94-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="58c94-105">Erstellen eines Speicherkontos in Eclipse</span><span class="sxs-lookup"><span data-stu-id="58c94-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="58c94-106">Gehen Sie folgendermaßen vor, um ein Speicherkonto mit dem Azure-Explorer zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="58c94-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="58c94-107">Melden Sie sich beim Azure-Konto gemäß den Anweisungen in [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) an.</span><span class="sxs-lookup"><span data-stu-id="58c94-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

1. <span data-ttu-id="58c94-108">Erweitern Sie in der Ansicht des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Speicherkonten**, und klicken Sie dann auf **Speicherkonto erstellen**.</span><span class="sxs-lookup"><span data-stu-id="58c94-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Befehl „Speicherkonto erstellen“][CS01]

1. <span data-ttu-id="58c94-110">Geben Sie im Dialogfeld **Speicherkonto erstellen** folgende Details an:</span><span class="sxs-lookup"><span data-stu-id="58c94-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Dialogfeld „Neues Speicherkonto erstellen“][CS02]

   * <span data-ttu-id="58c94-112">**Name**: Der Name für das neue Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="58c94-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="58c94-113">**Abonnement**: Das Azure-Abonnement, das Sie für das neue Speicherkonto verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="58c94-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="58c94-114">**Ressourcengruppe**: Die Ressourcengruppe für Ihre VM.</span><span class="sxs-lookup"><span data-stu-id="58c94-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="58c94-115">Wählen Sie eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="58c94-115">Select one of the following options:</span></span>
      * <span data-ttu-id="58c94-116">**Neue erstellen**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="58c94-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="58c94-117">**Vorhandene verwenden**: Gibt an, dass Sie in einer Liste von Ressourcengruppen, die Ihrem Azure-Konto zugeordnet sind, eine Auswahl treffen möchten.</span><span class="sxs-lookup"><span data-stu-id="58c94-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="58c94-118">**Region**: Der Standort, an dem Ihr Speicherkonto erstellt wird (z. B. „USA, Westen“).</span><span class="sxs-lookup"><span data-stu-id="58c94-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="58c94-119">**Kontoart**: Der Typ des zu erstellenden Speicherkontos (z. B. „Blob Storage“).</span><span class="sxs-lookup"><span data-stu-id="58c94-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="58c94-120">Weitere Informationen finden Sie unter [Informationen zu Azure-Speicherkonten].</span><span class="sxs-lookup"><span data-stu-id="58c94-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="58c94-121">**Leistung**: Das zu verwendende Speicherkontoangebot des ausgewählten Herausgebers (z. B. „Premium“).</span><span class="sxs-lookup"><span data-stu-id="58c94-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="58c94-122">Weitere Informationen finden Sie unter [Skalierbarkeits- und Leistungsziele für Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="58c94-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="58c94-123">**Replikation**: Die Replikation für das Speicherkonto (z. B. „Zonenredundant“).</span><span class="sxs-lookup"><span data-stu-id="58c94-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="58c94-124">Weitere Informationen finden Sie unter [Azure-Speicherreplikation].</span><span class="sxs-lookup"><span data-stu-id="58c94-124">For more information, see [Azure storage replication].</span></span>

1. <span data-ttu-id="58c94-125">Nachdem Sie alle vorhergehenden Optionen angegeben haben, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="58c94-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="58c94-126">Erstellen eines Speichercontainers in Eclipse</span><span class="sxs-lookup"><span data-stu-id="58c94-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="58c94-127">Gehen Sie folgendermaßen vor, um einen Speichercontainer mit dem Azure-Explorer zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="58c94-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="58c94-128">Klicken Sie in der **Azure-Explorer**-Ansicht mit der rechten Maustaste auf das Speicherkonto, in dem Sie einen Container erstellen möchten, und klicken Sie dann auf **Blobcontainer erstellen**.</span><span class="sxs-lookup"><span data-stu-id="58c94-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Befehl „Blobcontainer erstellen“][CC01]

1. <span data-ttu-id="58c94-130">Geben Sie im Dialogfeld **Blobcontainer erstellen** den Namen für Ihren Container ein, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="58c94-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="58c94-131">Weitere Informationen zum Benennen von Speichercontainern finden Sie unter [Benennen von Containern, Blobs und Metadaten und Verweisen auf diese].</span><span class="sxs-lookup"><span data-stu-id="58c94-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Dialogfeld „Blobcontainer erstellen“][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="58c94-133">Löschen eines Speichercontainers in Eclipse</span><span class="sxs-lookup"><span data-stu-id="58c94-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="58c94-134">Gehen Sie folgendermaßen vor, um einen Speichercontainer mit dem Azure-Explorer zu löschen:</span><span class="sxs-lookup"><span data-stu-id="58c94-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="58c94-135">Klicken Sie in der **Azure-Explorer**-Ansicht mit der rechten Maustaste auf den Speichercontainer, und klicken Sie dann auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="58c94-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![Befehl „Speichercontainer löschen“][DC01]

1. <span data-ttu-id="58c94-137">Klicken Sie im Bestätigungsfenster auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="58c94-137">In the confirmation window, click **OK**.</span></span>

   ![Bestätigungsfenster für „Speichercontainer löschen“][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="58c94-139">Löschen eines Speicherkontos in Eclipse</span><span class="sxs-lookup"><span data-stu-id="58c94-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="58c94-140">Gehen Sie folgendermaßen vor, um ein Speicherkonto mit dem Azure-Explorer zu löschen:</span><span class="sxs-lookup"><span data-stu-id="58c94-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="58c94-141">Klicken Sie in der **Azure-Explorers**-Ansicht mit der rechten Maustaste auf das Speicherkonto, und klicken Sie dann auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="58c94-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![Befehl „Speicherkonto löschen“][DS01]

1. <span data-ttu-id="58c94-143">Klicken Sie im Bestätigungsfenster auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="58c94-143">In the confirmation window, click **OK**.</span></span>

   ![Bestätigungsfenster für „Speicherkonto löschen“][DS02]

## <a name="next-steps"></a><span data-ttu-id="58c94-145">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="58c94-145">Next steps</span></span>

<span data-ttu-id="58c94-146">Weitere Informationen zu Azure Storage-Konten sowie Größen und Preisen finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="58c94-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="58c94-147">[Einführung in Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="58c94-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="58c94-148">[Informationen zu Azure-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="58c94-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="58c94-149">Größen für Azure Storage-Konten</span><span class="sxs-lookup"><span data-stu-id="58c94-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="58c94-150">[Größen für Windows-Speicherkonten in Azure]</span><span class="sxs-lookup"><span data-stu-id="58c94-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="58c94-151">[Größen für Linux-Speicherkonten in Azure]</span><span class="sxs-lookup"><span data-stu-id="58c94-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="58c94-152">Preise von Azure Storage-Konten</span><span class="sxs-lookup"><span data-stu-id="58c94-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="58c94-153">[Preise von Windows-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="58c94-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="58c94-154">[Preise von Linux-Speicherkonten]</span><span class="sxs-lookup"><span data-stu-id="58c94-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Einführung in Microsoft Azure Storage]: /azure/storage/storage-introduction
[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction
[Informationen zu Azure-Speicherkonten]: /azure/storage/storage-create-storage-account
[About Azure storage accounts]: /azure/storage/storage-create-storage-account
[Azure-Speicherreplikation]: /azure/storage/storage-redundancy
[Azure storage replication]: /azure/storage/storage-redundancy
[Skalierbarkeits- und Leistungsziele für Azure Storage]: /azure/storage/storage-scalability-targets
[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets
[Benennen von Containern, BLOBs und Metadaten und Verweisen auf diese]: http://go.microsoft.com/fwlink/?LinkId=255555
[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555

[Größen für Windows-Speicherkonten in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Größen für Linux-Speicherkonten in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preise von Windows-Speicherkonten]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Windows storage-account pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Preise von Linux-Speicherkonten]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/
[Linux storage-account pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
