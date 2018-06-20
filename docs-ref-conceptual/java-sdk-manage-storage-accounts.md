---
title: Verwalten von Azure-Speicherkonten mit Java | Microsoft-Dokumentation
description: Beispielcode zum Verwalten von Azure-Speicherkonten mit dem Azure SDK für Java
author: rloutlaw
manager: douge
ms.assetid: 49be8b66-3b56-4c10-8f14-9d326d815cb4
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 5945164b2b04e1fa9169590a71f6c5f9f45842d6
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931056"
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a><span data-ttu-id="5a459-103">Verwalten von Azure-Speicherkonten über Ihre Java-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="5a459-103">Manage Azure storage accounts from your Java applications</span></span>

<span data-ttu-id="5a459-104">[Dieses Beispiel](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) erstellt mit den [Java-Verwaltungsbibliotheken](https://github.com/Azure/azure-sdk-for-java) ein [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction)-Konto und verwendet die Kontozugriffsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="5a459-104">[This sample](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) creates an [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) account and works with the account access keys using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="5a459-105">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="5a459-105">Run the sample</span></span>

<span data-ttu-id="5a459-106">Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest.</span><span class="sxs-lookup"><span data-stu-id="5a459-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="5a459-107">Führen Sie anschließend Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="5a459-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

<span data-ttu-id="5a459-108">Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) an.</span><span class="sxs-lookup"><span data-stu-id="5a459-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="5a459-109">Authentifizieren über Azure</span><span class="sxs-lookup"><span data-stu-id="5a459-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a><span data-ttu-id="5a459-110">Erstellen Sie ein Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="5a459-110">Create a storage account</span></span>

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

<span data-ttu-id="5a459-111">Der bereitgestellte Speichername muss in Azure eindeutig sein und darf nur Kleinbuchstaben und Ziffern enthalten.</span><span class="sxs-lookup"><span data-stu-id="5a459-111">The storage name provided must be unique across all names in Azure and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="5a459-112">Das für dieses Konto verwendete Leistungs- und Replikationsstandardprofil lautet [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="5a459-112">The default performance and replication profile used for this account is [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span></span>

## <a name="list-keys-in-a-storage-account"></a><span data-ttu-id="5a459-113">Auflisten von Schlüsseln in einem Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="5a459-113">List keys in a storage account</span></span>
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

<span data-ttu-id="5a459-114">In jedem Azure-Speicherkonto werden zwei Schlüssel bereitgestellt, sodass Sie einen Schlüssel erneut generieren können, während Sie mithilfe des anderen Schlüssels weiterhin Zugriff auf den Speicher gewähren.</span><span class="sxs-lookup"><span data-stu-id="5a459-114">Two keys are provided in each Azure storage account so that you can regenerate one key while still allowing access to storage using the other key.</span></span>

## <a name="regenerate-a-key-in-a-storage-account"></a><span data-ttu-id="5a459-115">Erneutes Generieren eines Schlüssels in einem Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="5a459-115">Regenerate a key in a storage account</span></span>

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

<span data-ttu-id="5a459-116">Nach dem Generieren eines neuen Schlüssels müssen Sie alle Azure-Ressourcen und -Anwendungen mit dem neuen Schlüssel aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="5a459-116">You must update all Azure resources and applications with the new key after generating a new one.</span></span>

## <a name="list-all-storage-accounts-in-a-resource-group"></a><span data-ttu-id="5a459-117">Auflisten aller Speicherkonten in einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="5a459-117">List all storage accounts in a resource group</span></span>
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

<span data-ttu-id="5a459-118">Unter [com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) finden Sie eine Reihe nützlicher Methoden zum Überprüfen der Konfiguration eines Speicherkontos.</span><span class="sxs-lookup"><span data-stu-id="5a459-118">[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) provides a set of useful methods to inspect the configuration of a storage account.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="5a459-119">Löschen eines Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="5a459-119">Delete a storage account</span></span>
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> <span data-ttu-id="5a459-120">Speicherkonten mit verwendeten Datenträgerimages, die mit virtuellen Computern verbunden sind, oder von anderen Artefakten verwendete Datenträger dürfen nicht mit diesen Methoden entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="5a459-120">Storage accounts with in-use disk images connected to virtual machines or disks in use by other artifacts may not remove with these methods.</span></span> <span data-ttu-id="5a459-121">Trennen Sie vor dem Entfernen des Kontos den Speicher von diesen Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="5a459-121">Detach the storage from these resources before removing the account.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="5a459-122">Erläuterung des Beispiels</span><span class="sxs-lookup"><span data-stu-id="5a459-122">Sample explanation</span></span>

<span data-ttu-id="5a459-123">Der [Beispielcode auf GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span><span class="sxs-lookup"><span data-stu-id="5a459-123">[The sample code on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span></span>

- <span data-ttu-id="5a459-124">erstellt ein Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="5a459-124">creates a storage account</span></span>
- <span data-ttu-id="5a459-125">liest und regeneriert erneut Zugriffsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="5a459-125">reads and regenerates access keys</span></span>
- <span data-ttu-id="5a459-126">listet alle Speicherkonten in einer Ressourcengruppe auf.</span><span class="sxs-lookup"><span data-stu-id="5a459-126">lists all storage accounts in a resource group</span></span>
- <span data-ttu-id="5a459-127">löscht das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="5a459-127">deletes the storage account</span></span> 

| <span data-ttu-id="5a459-128">Im Beispiel verwendete Klasse</span><span class="sxs-lookup"><span data-stu-id="5a459-128">Class used in sample</span></span> | <span data-ttu-id="5a459-129">Hinweise</span><span class="sxs-lookup"><span data-stu-id="5a459-129">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="5a459-130">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="5a459-130">StorageAccount</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | <span data-ttu-id="5a459-131">Darstellung eines Azure-Speicherkontos.</span><span class="sxs-lookup"><span data-stu-id="5a459-131">Representation of an Azure storage account.</span></span> <span data-ttu-id="5a459-132">Verwenden Sie die Methoden in der Klasse, um Informationen zum Speicherkonto abzurufen.</span><span class="sxs-lookup"><span data-stu-id="5a459-132">Use the methods in the class to get information about the storage account.</span></span>
| [<span data-ttu-id="5a459-133">StorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="5a459-133">StorageAccountKey</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | <span data-ttu-id="5a459-134">`StorageAccount.getKeys()` gibt die Speicherkontoschlüssel zurück.</span><span class="sxs-lookup"><span data-stu-id="5a459-134">`StorageAccount.getKeys()` returns the storage account keys.</span></span> <span data-ttu-id="5a459-135">Verwenden Sie die `regenerateKey`-Methoden in `StorageAccount`, um die Schlüssel zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="5a459-135">Use the `regenerateKey` methods in `StorageAccount` to update the keys.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a459-136">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="5a459-136">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]