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
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: f8b2bc7adce71a27f1a059ef8ef691e52f66157e
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-intellij"></a>Verwalten von Redis Caches mit dem Azure-Explorer für IntelliJ

Der Azure-Explorer gehört zum Azure-Toolkit für IntelliJ und bietet Java-Entwicklern eine einfach zu bedienende Lösung zum Verwalten von Redis Caches in ihrem Azure-Konto innerhalb der IDE von IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Erstellen eines Redis Cache mithilfe von IntelliJ

Mit den folgenden Schritten werden die Schritte zum Erstellen eines Redis Cache mit dem Azure-Explorer erläutert.

1. Melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für IntelliJ] an.

1. Erweitern Sie im Toolfenster des **Azure-Explorers** den Knoten **Azure**. Klicken Sie mit der rechten Maustaste auf **Redis Caches**, und klicken Sie dann auf **Redis Cache erstellen**.

   ![Menü „Redis Cache erstellen“][CR01]

1. Wenn das Dialogfeld **Neuer Redis Cache** angezeigt wird, geben Sie die folgenden Optionen an:

   ![Dialogfeld zum Erstellen eines neuen Redis Cache][CR02]

   a. **DNS-Name**: Gibt die DNS-Unterdomäne für den neuen Redis Cache an. Sie wird „.redis.cache.windows.net“ vorangestellt, z.B.: *wingtiptoys.redis.cache.windows.net*.

   b. **Abonnement:** Wählen Sie das Azure-Abonnement aus, das Sie für den neuen Redis Cache verwenden möchten.

   c. **Ressourcengruppe**: Gibt die Ressourcengruppe für den neuen Redis Cache an. Sie müssen eine der folgenden Optionen auswählen: 
      * **Create New**: Gibt an, dass Sie eine neue Ressourcengruppe erstellen möchten. 
      * **Vorhandene verwenden:** Gibt an, dass Sie in einer Liste von Ressourcengruppen, die Ihrem Azure-Konto zugeordnet sind, eine Auswahl treffen möchten. 

   d. **Ort**: Gibt den Ort an, an dem Ihr Redis Cache erstellt wird, z.B. *USA, Westen*.

   e. **Tarif**: Gibt an, welcher Tarif für Ihren Redis Cache verwendet wird. Diese Einstellung bestimmt die Anzahl von Clientverbindungen. (Weitere Informationen finden Sie unter [Redis Cache – Preise].)

   f. **Nicht-SSL-Port**: Gibt an, ob Ihr Redis Cache andere Verbindungen als SSL-Verbindungen zulässt. Standardmäßig sind nur SSL-Verbindungen zulässig.

1. Wenn Sie alle Redis Cache-Einstellungen angegeben haben, klicken Sie auf **OK**.

Nachdem Ihr Redis Cache erstellt wurde, wird er im Azure-Explorer angezeigt.

   ![Redis Cache im Azure-Explorer][CR03]

> [!NOTE]
>
> Weitere Informationen zum Konfigurieren der Azure Redis Cache-Einstellungen finden Sie unter [Konfigurieren von Azure Redis Cache].
>

## <a name="display-the-properties-for-your-redis-cache-in-intellij"></a>Anzeigen der Eigenschaften für den Redis Cache in IntelliJ

1. Klicken Sie im Azure-Explorer mit der rechten Maustaste auf den Redis Cache, und klicken Sie auf **Eigenschaften anzeigen**.

   ![Azure Explorer-Kontextmenü zum Anzeigen der Eigenschaften für einen Redis Cache][SP01]

1. Der Azure-Explorer zeigt die Eigenschaften für den Redis Cache an.

   ![Redis Cache: Eigenschaften][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Löschen des Redis Cache mithilfe von IntelliJ

1. Klicken Sie im Azure-Explorer mit der rechten Maustaste auf den Redis Cache, und klicken Sie auf **Löschen**.

   ![Azure Explorer-Kontextmenü zum Löschen eines Redis Cache][DE01]

1. Klicken Sie auf **Ja**, wenn die Aufforderung zum Löschen des Redis Cache angezeigt wird.

   ![Aufforderung zum Löschen des Redis Cache][DE02]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Azure Redis Caches, Konfigurationseinstellungen und Preisen finden Sie unter den folgenden Links:

* [Azure Redis Cache]
* [Dokumentation zu Redis Cache]
* [Redis Cache – Preise]
* [Konfigurieren von Azure Redis Cache]

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Redis Cache – Preise]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Dokumentation zu Redis Cache]: /azure/redis-cache
[Konfigurieren von Azure Redis Cache]: /azure/redis-cache/cache-configure
[Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
