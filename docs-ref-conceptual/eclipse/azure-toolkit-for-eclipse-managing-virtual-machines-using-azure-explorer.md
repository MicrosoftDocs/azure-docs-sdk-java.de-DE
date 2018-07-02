---
title: Verwalten virtueller Computer mit dem Azure-Explorer für Eclipse
description: Erfahren Sie, wie Sie Ihre virtuellen Azure-Computer mit dem Azure-Explorer für Eclipse verwalten.
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
ms.openlocfilehash: c04f5225f0bb99898f69b26a4782aa57d75c4f22
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090661"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="4eb88-103">Verwalten virtueller Computer mit dem Azure-Explorer für Eclipse</span><span class="sxs-lookup"><span data-stu-id="4eb88-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="4eb88-104">Der Azure-Explorer gehört zum Azure-Toolkit für Eclipse und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von virtuellen Computern in ihrem Azure-Konto innerhalb der integrierten Entwicklungsumgebung (IDE) von Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4eb88-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="4eb88-105">Erstellen eines virtuellen Computers in Eclipse</span><span class="sxs-lookup"><span data-stu-id="4eb88-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="4eb88-106">Gehen Sie folgendermaßen vor, um einen virtuellen Computer mit dem Azure-Explorer zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="4eb88-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="4eb88-107">Melden Sie sich beim Azure-Konto gemäß den Anweisungen in [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) an.</span><span class="sxs-lookup"><span data-stu-id="4eb88-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

2. <span data-ttu-id="4eb88-108">Erweitern Sie in der Ansicht des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Virtuelle Computer**, und klicken Sie dann auf **VM erstellen**.</span><span class="sxs-lookup"><span data-stu-id="4eb88-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   ![Befehl „VM erstellen“][CR01]  

   <span data-ttu-id="4eb88-110">Der **Assistent zum Erstellen eines neuen virtuellen Computers** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="4eb88-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="4eb88-111">Wählen Sie im Dialogfeld **Abonnement auswählen** Ihr Abonnement aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="4eb88-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Fenster „Abonnement auswählen“][CR02]

4. <span data-ttu-id="4eb88-113">Geben Sie im Fenster **Virtuelles Computerimage auswählen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="4eb88-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="4eb88-114">**Standort:** gibt den Standort an, an dem Ihr virtueller Computer erstellt wird (z.B. *USA, Westen*).</span><span class="sxs-lookup"><span data-stu-id="4eb88-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="4eb88-115">**Herausgeber:** gibt den Herausgeber an, der das Image zum Erstellen des virtuellen Computers erstellt hat (z.B. *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="4eb88-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="4eb88-116">**Angebot:** gibt an, welches Angebot eines virtuellen Computers für den ausgewählten Herausgeber verwendet werden soll (z.B. *JDK*).</span><span class="sxs-lookup"><span data-stu-id="4eb88-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="4eb88-117">**SKU:** gibt die zu verwendende SKU (Stock-Keeping Unit, Artikelnummer) aus dem ausgewählten Angebot an (z.B. *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="4eb88-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="4eb88-118">**Versionsnummer:** gibt an, welche Version der ausgewählten SKU verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="4eb88-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Fenster „Virtuelles Computerimage auswählen“][CR03]

5. <span data-ttu-id="4eb88-120">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="4eb88-120">Click **Next**.</span></span>

6. <span data-ttu-id="4eb88-121">Geben Sie im Fenster **Grundlegende Einstellungen des virtuellen Computers** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="4eb88-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="4eb88-122">**Name des virtuellen Computers:** gibt den Namen Ihres virtuellen Computers an. Dieser muss mit einem Buchstaben beginnen und darf nur Buchstaben, Ziffern und Bindestriche enthalten.</span><span class="sxs-lookup"><span data-stu-id="4eb88-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="4eb88-123">**Größe:** gibt die Anzahl der Kerne und den Speicher an, die dem virtuellen Computer zugeordnet werden sollen</span><span class="sxs-lookup"><span data-stu-id="4eb88-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="4eb88-124">**Benutzername:** gibt das Administratorkonto an, das für die Verwaltung Ihres virtuellen Computer erstellt werden soll</span><span class="sxs-lookup"><span data-stu-id="4eb88-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="4eb88-125">**Kennwort** und **Bestätigen**: geben das Kennwort für Ihr Administratorkonto an</span><span class="sxs-lookup"><span data-stu-id="4eb88-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Fenster „Grundlegende Einstellungen des virtuellen Computers“][CR04]

7. <span data-ttu-id="4eb88-127">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="4eb88-127">Click **Next**.</span></span>

8. <span data-ttu-id="4eb88-128">Geben Sie im Fenster **Neues Speicherkonto erstellen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="4eb88-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="4eb88-129">**Ressourcengruppe:** Geben Sie die Ressourcengruppe für Ihren virtuellen Computer an.</span><span class="sxs-lookup"><span data-stu-id="4eb88-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="4eb88-130">Wählen Sie eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="4eb88-130">Select one of the following options:</span></span>
     * <span data-ttu-id="4eb88-131">**Neu erstellen:** gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="4eb88-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
     * <span data-ttu-id="4eb88-132">**Vorhandene verwenden:** gibt an, dass Sie eine Ressourcengruppe auswählen möchten, die Ihrem Azure-Konto bereits zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="4eb88-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

       ![Dialogfeld „Neues Speicherkonto erstellen“][CR05]

   * <span data-ttu-id="4eb88-134">**Speicherkonto:** gibt das Speicherkonto an, das zum Speichern des virtuellen Computers verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="4eb88-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="4eb88-135">Sie können ein vorhandenes Speicherkonto auswählen oder ein neues erstellen.</span><span class="sxs-lookup"><span data-stu-id="4eb88-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="4eb88-136">**Virtuelles Netzwerk** und **Subnetz**: geben das virtuelle Netzwerk und das Subnetz an, mit dem der virtuelle Computer eine Verbindung herstellen soll.</span><span class="sxs-lookup"><span data-stu-id="4eb88-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="4eb88-137">Sie können ein vorhandenes Netzwerk und Subnetz verwenden oder ein neues Netzwerk und Subnetz erstellen.</span><span class="sxs-lookup"><span data-stu-id="4eb88-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="4eb88-138">Wenn Sie **Neu erstellen** auswählen, wird das folgende Dialogfeld angezeigt:</span><span class="sxs-lookup"><span data-stu-id="4eb88-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![Dialogfeld „Neues virtuelles Netzwerk erstellen“][CR06]

9. <span data-ttu-id="4eb88-140">Geben Sie im Fenster **Zugeordnete Ressourcen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="4eb88-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="4eb88-141">**Öffentliche IP-Adresse:** gibt eine externe IP-Adresse für den virtuellen Computer an.</span><span class="sxs-lookup"><span data-stu-id="4eb88-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="4eb88-142">Sie können eine neue IP-Adresse erstellen oder **(Keine)** auswählen, wenn Ihr virtueller Computer nicht über eine öffentliche IP-Adresse verfügt.</span><span class="sxs-lookup"><span data-stu-id="4eb88-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="4eb88-143">**Netzwerksicherheitsgruppe:** gibt eine optionale Netzwerkfirewall für den virtuellen Computer an.</span><span class="sxs-lookup"><span data-stu-id="4eb88-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="4eb88-144">Sie können eine vorhandene Firewall auswählen oder **(Keine)** auswählen, wenn Ihr virtueller Computer keine Netzwerkfirewall verwendet.</span><span class="sxs-lookup"><span data-stu-id="4eb88-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="4eb88-145">**Verfügbarkeitsgruppe:** gibt eine optionale Verfügbarkeitsgruppe an, der Ihr virtueller Computer angehören kann.</span><span class="sxs-lookup"><span data-stu-id="4eb88-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="4eb88-146">Sie können eine vorhandene Verfügbarkeitsgruppe auswählen, eine neue erstellen oder **(Keine)** auswählen, wenn Ihr virtueller Computer keiner Verfügbarkeitsgruppe angehören soll.</span><span class="sxs-lookup"><span data-stu-id="4eb88-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![Fenster „Zugeordnete Ressourcen“][CR07]

10. <span data-ttu-id="4eb88-148">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="4eb88-148">Click **Finish**.</span></span>  

    <span data-ttu-id="4eb88-149">Der neue virtuelle Computer wird im Toolfenster von Azure-Explorer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4eb88-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

    ![Neuer virtueller Computer][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="4eb88-151">Neustarten eines virtuellen Computers in Eclipse</span><span class="sxs-lookup"><span data-stu-id="4eb88-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="4eb88-152">Um einen virtuellen Computer mithilfe des Azure-Explorers in Eclipse neu zu starten, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="4eb88-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="4eb88-153">Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Neu starten** aus.</span><span class="sxs-lookup"><span data-stu-id="4eb88-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Befehl „Neu starten“ für einen virtuellen Computer][RE01]

1. <span data-ttu-id="4eb88-155">Klicken Sie im Bestätigungsfenster auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="4eb88-155">In the confirmation window, click **Yes**.</span></span>

   ![Bestätigungsfenster für den Neustart][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="4eb88-157">Herunterfahren eines virtuellen Computers in Eclipse</span><span class="sxs-lookup"><span data-stu-id="4eb88-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="4eb88-158">Um einen ausgeführten virtuellen Computer mithilfe des Azure-Explorers in Eclipse herunterzufahren, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="4eb88-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="4eb88-159">Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Herunterfahren** aus.</span><span class="sxs-lookup"><span data-stu-id="4eb88-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Befehl „Herunterfahren“ für einen virtuellen Computer][SH01]

1. <span data-ttu-id="4eb88-161">Klicken Sie im Bestätigungsfenster auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="4eb88-161">In the confirmation window, click **Yes**.</span></span>

   ![Bestätigungsfenster für das Herunterfahren eines virtuellen Computers][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="4eb88-163">Löschen eines virtuellen Computers in Eclipse</span><span class="sxs-lookup"><span data-stu-id="4eb88-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="4eb88-164">Um einen virtuellen Computer mithilfe des Azure-Explorers in Eclipse zu löschen, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="4eb88-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="4eb88-165">Klicken Sie in der Ansicht **Azure-Explorer** mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **Löschen** aus.</span><span class="sxs-lookup"><span data-stu-id="4eb88-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Befehl „Löschen“ für einen virtuellen Computer][DE01]

1. <span data-ttu-id="4eb88-167">Klicken Sie im Bestätigungsfenster auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="4eb88-167">In the confirmation window, click **Yes**.</span></span>

   ![Bestätigungsfenster für das Löschen eines virtuellen Computers][DE02]

## <a name="next-steps"></a><span data-ttu-id="4eb88-169">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="4eb88-169">Next steps</span></span>

<span data-ttu-id="4eb88-170">Weitere Informationen zu den Größen und Preisen für virtuelle Azure-Computer finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="4eb88-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="4eb88-171">Größen für virtuelle Azure-Computer</span><span class="sxs-lookup"><span data-stu-id="4eb88-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="4eb88-172">[Größen für virtuelle Windows-Computer in Azure]</span><span class="sxs-lookup"><span data-stu-id="4eb88-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="4eb88-173">[Größen für virtuelle Linux-Computer in Azure]</span><span class="sxs-lookup"><span data-stu-id="4eb88-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="4eb88-174">Preise für virtuelle Azure-Computer</span><span class="sxs-lookup"><span data-stu-id="4eb88-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="4eb88-175">[Preise von virtuellen Windows-Computern]</span><span class="sxs-lookup"><span data-stu-id="4eb88-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="4eb88-176">[Preise von virtuellen Linux-Computern]</span><span class="sxs-lookup"><span data-stu-id="4eb88-176">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Größen für virtuelle Windows-Computer in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Größen für virtuelle Linux-Computer in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preise von virtuellen Windows-Computern]: /pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/
[Preise von virtuellen Linux-Computern]: /pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
