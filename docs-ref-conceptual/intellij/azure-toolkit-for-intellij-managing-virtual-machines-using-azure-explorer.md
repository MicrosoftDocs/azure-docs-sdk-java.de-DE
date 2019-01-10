---
title: Verwalten virtueller Computer mit dem Azure-Explorer für IntelliJ
description: Erfahren Sie, wie Sie Ihre virtuellen Azure-Computer mit dem Azure-Explorer für IntelliJ verwalten.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: a3aff77bc2fd2dac0396187d9e6b27910bc60e58
ms.sourcegitcommit: 24f037d133875f86761ec893dfa74e723de040b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2018
ms.locfileid: "53636415"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="764cd-103">Verwalten virtueller Computer mit dem Azure-Explorer für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="764cd-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="764cd-104">Der Azure-Explorer gehört zum Azure-Toolkit für IntelliJ und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von virtuellen Computern in ihrem Azure-Konto innerhalb der integrierten Entwicklungsumgebung (IDE) von IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="764cd-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="764cd-105">Erstellen eines virtuellen Computers in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="764cd-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="764cd-106">Gehen Sie folgendermaßen vor, um einen virtuellen Computer mit dem Azure-Explorer zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="764cd-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="764cd-107">Melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ] an.</span><span class="sxs-lookup"><span data-stu-id="764cd-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="764cd-108">Erweitern Sie in der Ansicht des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Virtuelle Computer**, und klicken Sie dann auf **VM erstellen**.</span><span class="sxs-lookup"><span data-stu-id="764cd-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="764cd-109">![Befehl „VM erstellen“][CR01]</span><span class="sxs-lookup"><span data-stu-id="764cd-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="764cd-110">Der **Assistent zum Erstellen eines neuen virtuellen Computers** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="764cd-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="764cd-111">Wählen Sie im Dialogfeld **Abonnement auswählen** Ihr Abonnement aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="764cd-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Fenster „Abonnement auswählen“][CR02]

4. <span data-ttu-id="764cd-113">Geben Sie im Fenster **Virtuelles Computerimage auswählen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="764cd-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="764cd-114">**Standort**: Der Standort, an dem Ihre VM erstellt wird (z. B. *USA, Westen*).</span><span class="sxs-lookup"><span data-stu-id="764cd-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="764cd-115">**Empfohlenes Image**: Gibt an, dass Sie ein Image aus einer gekürzten Liste häufig verwendeter Images auswählen.</span><span class="sxs-lookup"><span data-stu-id="764cd-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="764cd-116">**Benutzerdefiniertes Image**: Gibt an, dass Sie ein benutzerdefiniertes Image auswählen, indem Sie die folgenden Informationen angeben:</span><span class="sxs-lookup"><span data-stu-id="764cd-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="764cd-117">**Herausgeber**: Der Herausgeber, der das zu verwendende Image für die VM erstellt hat (z. B. *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="764cd-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="764cd-118">**Angebot**: Das zu verwendende VM-Angebot des ausgewählten Herausgebers (z. B. *JDK*).</span><span class="sxs-lookup"><span data-stu-id="764cd-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="764cd-119">**SKU**: Die zu verwendende SKU (Stock Keeping Unit) des ausgewählten Angebots (z. B. *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="764cd-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="764cd-120">**Versionsnummer**: Die zu verwendende Version der ausgewählten SKU.</span><span class="sxs-lookup"><span data-stu-id="764cd-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Fenster „Virtuelles Computerimage auswählen“][CR03]

5. <span data-ttu-id="764cd-122">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="764cd-122">Click **Next**.</span></span> 

6. <span data-ttu-id="764cd-123">Geben Sie im Fenster **Grundlegende Einstellungen des virtuellen Computers** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="764cd-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="764cd-124">**Name des virtuellen Computers**: Der Name Ihrer neuen VM. Der Name muss mit einem Buchstaben beginnen und darf nur Buchstaben, Ziffern und Bindestriche enthalten.</span><span class="sxs-lookup"><span data-stu-id="764cd-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="764cd-125">**Größe**: Die Anzahl von Kernen und der Arbeitsspeicher, die der VM zugeordnet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="764cd-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="764cd-126">**Benutzername**: Das Administratorkonto, das für die Verwaltung Ihrer VM erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="764cd-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="764cd-127">**Kennwort** und **Bestätigen**: Das Kennwort für Ihr Administratorkonto.</span><span class="sxs-lookup"><span data-stu-id="764cd-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Fenster „Grundlegende Einstellungen des virtuellen Computers“][CR04]

7. <span data-ttu-id="764cd-129">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="764cd-129">Click **Next**.</span></span> 

8. <span data-ttu-id="764cd-130">Geben Sie im Fenster **Zugeordnete Ressourcen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="764cd-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="764cd-131">**Ressourcengruppe**: Die Ressourcengruppe für Ihre VM.</span><span class="sxs-lookup"><span data-stu-id="764cd-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="764cd-132">Wählen Sie eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="764cd-132">Select one of the following options:</span></span>
      * <span data-ttu-id="764cd-133">**Neue erstellen**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="764cd-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="764cd-134">**Vorhandene verwenden**: Gibt an, dass Sie in einer Liste von Ressourcengruppen, die Ihrem Azure-Konto zugeordnet sind, eine Auswahl treffen möchten.</span><span class="sxs-lookup"><span data-stu-id="764cd-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![Fenster „Zugeordnete Ressourcen“][CR07]

   * <span data-ttu-id="764cd-136">**Speicherkonto**: Das Speicherkonto, das zum Speichern der VM verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="764cd-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="764cd-137">Sie können ein vorhandenes Speicherkonto auswählen oder ein neues erstellen.</span><span class="sxs-lookup"><span data-stu-id="764cd-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="764cd-138">Wenn Sie **Neu erstellen** auswählen, wird das folgende Dialogfeld angezeigt:</span><span class="sxs-lookup"><span data-stu-id="764cd-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![Dialogfeld „Speicherkonto erstellen“][CR05]

   * <span data-ttu-id="764cd-140">**Virtuelles Netzwerk** und **Subnetz**: Das virtuelle Netzwerk und das Subnetz, mit denen Ihre VM eine Verbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="764cd-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="764cd-141">Sie können ein vorhandenes Netzwerk und Subnetz verwenden oder ein neues Netzwerk und Subnetz erstellen.</span><span class="sxs-lookup"><span data-stu-id="764cd-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="764cd-142">Wenn Sie **Neu erstellen** auswählen, wird das folgende Dialogfeld angezeigt:</span><span class="sxs-lookup"><span data-stu-id="764cd-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![Dialogfeld „Virtuelles Netzwerk erstellen“][CR06]

   * <span data-ttu-id="764cd-144">**Öffentliche IP-Adresse**: Eine externe IP-Adresse für Ihre VM.</span><span class="sxs-lookup"><span data-stu-id="764cd-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="764cd-145">Sie können eine neue IP-Adresse erstellen oder **(Keine)** auswählen, wenn Ihr virtueller Computer nicht über eine öffentliche IP-Adresse verfügt.</span><span class="sxs-lookup"><span data-stu-id="764cd-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="764cd-146">**Netzwerksicherheitsgruppe**: Eine optionale Netzwerkfirewall für Ihre VM.</span><span class="sxs-lookup"><span data-stu-id="764cd-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="764cd-147">Sie können eine vorhandene Firewall auswählen oder **(Keine)** auswählen, wenn Ihr virtueller Computer keine Netzwerkfirewall verwendet.</span><span class="sxs-lookup"><span data-stu-id="764cd-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="764cd-148">**Verfügbarkeitsgruppe**: Eine optionale Verfügbarkeitsgruppe, der Ihre VM angehören kann.</span><span class="sxs-lookup"><span data-stu-id="764cd-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="764cd-149">Sie können eine vorhandene Verfügbarkeitsgruppe auswählen, eine neue erstellen oder **(Keine)** auswählen, wenn Ihr virtueller Computer keiner Verfügbarkeitsgruppe angehören soll.</span><span class="sxs-lookup"><span data-stu-id="764cd-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="764cd-150">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="764cd-150">Click **Finish**.</span></span>  
    <span data-ttu-id="764cd-151">Der neue virtuelle Computer wird im Toolfenster von Azure-Explorer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="764cd-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Neuer virtueller Computer in der Azure-Explorer-Ansicht][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="764cd-153">Neustarten eines virtuellen Computers in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="764cd-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="764cd-154">Um einen virtuellen Computer mithilfe des Azure-Explorers in IntelliJ neu zu starten, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="764cd-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="764cd-155">Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Neu starten** aus.</span><span class="sxs-lookup"><span data-stu-id="764cd-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Befehl „Neu starten“ für einen virtuellen Computer][RE01]

2. <span data-ttu-id="764cd-157">Klicken Sie im Bestätigungsfenster auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="764cd-157">In the confirmation window, click **Yes**.</span></span> 

   ![Bestätigungsfenster für den Neustart eines virtuellen Computers][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="764cd-159">Herunterfahren eines virtuellen Computers in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="764cd-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="764cd-160">Um einen ausgeführten virtuellen Computer mithilfe des Azure-Explorers in IntelliJ herunterzufahren, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="764cd-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="764cd-161">Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Herunterfahren** aus.</span><span class="sxs-lookup"><span data-stu-id="764cd-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Befehl „Herunterfahren“ für einen virtuellen Computer][SH01]

2. <span data-ttu-id="764cd-163">Klicken Sie im Bestätigungsfenster auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="764cd-163">In the confirmation window, click **Yes**.</span></span> 

   ![Bestätigungsfenster für das Herunterfahren eines virtuellen Computers][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="764cd-165">Löschen eines virtuellen Computers in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="764cd-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="764cd-166">Um einen virtuellen Computer mithilfe des Azure-Explorers in IntelliJ zu löschen, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="764cd-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="764cd-167">Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Löschen** aus.</span><span class="sxs-lookup"><span data-stu-id="764cd-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Befehl „Löschen“ für einen virtuellen Computer][DE01]

2. <span data-ttu-id="764cd-169">Klicken Sie im Bestätigungsfenster auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="764cd-169">In the confirmation window, click **Yes**.</span></span> 

   ![Bestätigungsfenster für das Löschen eines virtuellen Computers][DE02]

## <a name="next-steps"></a><span data-ttu-id="764cd-171">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="764cd-171">Next steps</span></span>

<span data-ttu-id="764cd-172">Weitere Informationen zu den Größen und Preisen für virtuelle Azure-Computer finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="764cd-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="764cd-173">Größen für virtuelle Azure-Computer</span><span class="sxs-lookup"><span data-stu-id="764cd-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="764cd-174">[Größen für virtuelle Windows-Computer in Azure]</span><span class="sxs-lookup"><span data-stu-id="764cd-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="764cd-175">[Größen für virtuelle Linux-Computer in Azure]</span><span class="sxs-lookup"><span data-stu-id="764cd-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="764cd-176">Preise für virtuelle Azure-Computer</span><span class="sxs-lookup"><span data-stu-id="764cd-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="764cd-177">[Preise von virtuellen Windows-Computern]</span><span class="sxs-lookup"><span data-stu-id="764cd-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="764cd-178">[Preise von virtuellen Linux-Computern]</span><span class="sxs-lookup"><span data-stu-id="764cd-178">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Größen für virtuelle Windows-Computer in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Größen für virtuelle Linux-Computer in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preise von virtuellen Windows-Computern]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Preise von virtuellen Linux-Computern]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
