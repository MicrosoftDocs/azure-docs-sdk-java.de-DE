---
title: "Verwalten von Redis Caches mit dem Azure-Explorer für IntelliJ"
description: "Erfahren Sie, wie Sie Ihre Azure Redis Caches mit dem Azure-Explorer für IntelliJ verwalten."
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
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: b715ffb97a4ca2b13e8020d354341139be4be45b
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="d27c5-103">Verwalten von Redis Caches mit dem Azure-Explorer für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d27c5-103">Managing Redis Caches using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="d27c5-104">Der Azure-Explorer gehört zum Azure-Toolkit für IntelliJ und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von Redis Caches in ihrem Azure-Konto innerhalb der IDE von IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="d27c5-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="d27c5-105">Erstellen eines Redis Cache mithilfe von IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d27c5-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="d27c5-106">Mit den folgenden Schritten werden die Schritte zum Erstellen eines Redis Cache mit dem Azure-Explorer erläutert.</span><span class="sxs-lookup"><span data-stu-id="d27c5-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="d27c5-107">Melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für IntelliJ] an.</span><span class="sxs-lookup"><span data-stu-id="d27c5-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="d27c5-108">Erweitern Sie im Toolfenster des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Redis Caches**, und klicken Sie dann auf **Redis Cache erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d27c5-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Menü „Redis Cache erstellen“][CR01]

1. <span data-ttu-id="d27c5-110">Wenn das Dialogfeld **Neuer Redis Cache** angezeigt wird, geben Sie die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="d27c5-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![Dialogfeld zum Erstellen eines neuen Redis Cache][CR02]

   <span data-ttu-id="d27c5-112">a.</span><span class="sxs-lookup"><span data-stu-id="d27c5-112">a.</span></span> <span data-ttu-id="d27c5-113">**DNS-Name**: Gibt die DNS-Unterdomäne für den neuen Redis Cache an. Sie wird „.redis.cache.windows.net“ vorangestellt, z.B.: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="d27c5-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which are prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="d27c5-114">b.</span><span class="sxs-lookup"><span data-stu-id="d27c5-114">b.</span></span> <span data-ttu-id="d27c5-115">**Abonnement:** Wählen Sie das Azure-Abonnement aus, das Sie für den neuen Redis Cache verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="d27c5-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="d27c5-116">c.</span><span class="sxs-lookup"><span data-stu-id="d27c5-116">c.</span></span> <span data-ttu-id="d27c5-117">**Ressourcengruppe**: Gibt die Ressourcengruppe für den neuen Redis Cache an. Sie müssen eine der folgenden Optionen auswählen:</span><span class="sxs-lookup"><span data-stu-id="d27c5-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span> 
      * <span data-ttu-id="d27c5-118">**Create New**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="d27c5-118">**Create New**: Specifies that you want to create a new resource group.</span></span> 
      * <span data-ttu-id="d27c5-119">**Vorhandene verwenden:** Gibt an, dass Sie in einer Liste von Ressourcengruppen, die Ihrem Azure-Konto zugeordnet sind, eine Auswahl treffen möchten.</span><span class="sxs-lookup"><span data-stu-id="d27c5-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span> 

   <span data-ttu-id="d27c5-120">d.</span><span class="sxs-lookup"><span data-stu-id="d27c5-120">d.</span></span> <span data-ttu-id="d27c5-121">**Ort**: Gibt den Ort an, an dem Ihr Redis Cache erstellt wird, z.B. *USA, Westen*.</span><span class="sxs-lookup"><span data-stu-id="d27c5-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="d27c5-122">e.</span><span class="sxs-lookup"><span data-stu-id="d27c5-122">e.</span></span> <span data-ttu-id="d27c5-123">**Tarif**: Gibt an, welcher Tarif für Ihren Redis Cache verwendet wird. Diese Einstellung bestimmt die Anzahl von Clientverbindungen.</span><span class="sxs-lookup"><span data-stu-id="d27c5-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="d27c5-124">(Weitere Informationen finden Sie unter [Redis Cache – Preise].)</span><span class="sxs-lookup"><span data-stu-id="d27c5-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="d27c5-125">f.</span><span class="sxs-lookup"><span data-stu-id="d27c5-125">f.</span></span> <span data-ttu-id="d27c5-126">**Nicht-SSL-Port**: Gibt an, ob Ihr Redis Cache andere Verbindungen als SSL-Verbindungen zulässt. Standardmäßig sind nur SSL-Verbindungen zulässig.</span><span class="sxs-lookup"><span data-stu-id="d27c5-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="d27c5-127">Wenn Sie alle Redis Cache-Einstellungen angegeben haben, klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="d27c5-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="d27c5-128">Nachdem Ihr Redis Cache erstellt wurde, wird er im Azure-Explorer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d27c5-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Redis Cache im Azure-Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="d27c5-130">Weitere Informationen zum Konfigurieren der Azure Redis Cache-Einstellungen finden Sie unter [Konfigurieren von Azure Redis Cache].</span><span class="sxs-lookup"><span data-stu-id="d27c5-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="d27c5-131">Anzeigen der Eigenschaften für den Redis Cache in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d27c5-131">Display the properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="d27c5-132">Klicken Sie im Azure-Explorer mit der rechten Maustaste auf den Redis Cache, und klicken Sie auf **Eigenschaften anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="d27c5-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure Explorer-Kontextmenü zum Anzeigen der Eigenschaften für einen Redis Cache][SP01]

1. <span data-ttu-id="d27c5-134">Der Azure-Explorer zeigt die Eigenschaften für den Redis Cache an.</span><span class="sxs-lookup"><span data-stu-id="d27c5-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Redis Cache: Eigenschaften][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="d27c5-136">Löschen des Redis Cache mithilfe von IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d27c5-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="d27c5-137">Klicken Sie im Azure-Explorer mit der rechten Maustaste auf den Redis Cache, und klicken Sie auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="d27c5-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Azure Explorer-Kontextmenü zum Löschen eines Redis Cache][DE01]

1. <span data-ttu-id="d27c5-139">Klicken Sie auf **Ja**, wenn die Aufforderung zum Löschen des Redis Cache angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="d27c5-139">Click **Yes** when prompted to delete your redis cache.</span></span>

   ![Aufforderung zum Löschen des Redis Cache][DE02]

## <a name="next-steps"></a><span data-ttu-id="d27c5-141">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="d27c5-141">Next steps</span></span>

<span data-ttu-id="d27c5-142">Weitere Informationen zu Azure Redis Caches, Konfigurationseinstellungen und Preisen finden Sie unter den folgenden Links:</span><span class="sxs-lookup"><span data-stu-id="d27c5-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="d27c5-143">[Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="d27c5-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="d27c5-144">[Dokumentation zu Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="d27c5-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="d27c5-145">[Redis Cache – Preise]</span><span class="sxs-lookup"><span data-stu-id="d27c5-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="d27c5-146">[Konfigurieren von Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="d27c5-146">[How to configure Azure Redis Cache]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Redis Cache – Preise]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Dokumentation zu Redis Cache]: /azure/redis-cache
[Konfigurieren von Azure Redis Cache]: /azure/redis-cache/cache-configure
[Anleitung zur Azure-Anmeldung für das Azure-Toolkit für IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
