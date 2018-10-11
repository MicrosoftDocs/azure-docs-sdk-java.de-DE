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
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893061"
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a>Verwalten von Azure-Speicherkonten über Ihre Java-Anwendungen

[Dieses Beispiel](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) erstellt mit den [Java-Verwaltungsbibliotheken](https://github.com/Azure/azure-sdk-for-java) ein [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction)-Konto und verwendet die Kontozugriffsschlüssel. 

## <a name="run-the-sample"></a>Ausführen des Beispiels

Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest. Führen Sie anschließend Folgendes aus:

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

Sehen Sie sich das [vollständige Codebeispiel auf GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) an.

## <a name="authenticate-with-azure"></a>Authentifizieren über Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a>Speicherkonto erstellen

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

Der bereitgestellte Speichername muss in Azure eindeutig sein und darf nur Kleinbuchstaben und Ziffern enthalten. Das für dieses Konto verwendete Leistungs- und Replikationsstandardprofil lautet [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).

## <a name="list-keys-in-a-storage-account"></a>Auflisten von Schlüsseln in einem Speicherkonto
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

In jedem Azure-Speicherkonto werden zwei Schlüssel bereitgestellt, sodass Sie einen Schlüssel erneut generieren können, während Sie mithilfe des anderen Schlüssels weiterhin Zugriff auf den Speicher gewähren.

## <a name="regenerate-a-key-in-a-storage-account"></a>Erneutes Generieren eines Schlüssels in einem Speicherkonto

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

Nach dem Generieren eines neuen Schlüssels müssen Sie alle Azure-Ressourcen und -Anwendungen mit dem neuen Schlüssel aktualisieren.

## <a name="list-all-storage-accounts-in-a-resource-group"></a>Auflisten aller Speicherkonten in einer Ressourcengruppe
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

Unter [com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) finden Sie eine Reihe nützlicher Methoden zum Überprüfen der Konfiguration eines Speicherkontos.

## <a name="delete-a-storage-account"></a>Löschen von Speicherkonten
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> Speicherkonten mit verwendeten Datenträgerimages, die mit virtuellen Computern verbunden sind, oder von anderen Artefakten verwendete Datenträger dürfen nicht mit diesen Methoden entfernt werden. Trennen Sie vor dem Entfernen des Kontos den Speicher von diesen Ressourcen.

## <a name="sample-explanation"></a>Erläuterung des Beispiels

Der [Beispielcode auf GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):

- erstellt ein Speicherkonto.
- liest und regeneriert erneut Zugriffsschlüssel.
- listet alle Speicherkonten in einer Ressourcengruppe auf.
- löscht das Speicherkonto. 

| Im Beispiel verwendete Klasse | Notizen
|-------|-------|
| [StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | Darstellung eines Azure-Speicherkontos. Verwenden Sie die Methoden in der Klasse, um Informationen zum Speicherkonto abzurufen.
| [StorageAccountKey](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | `StorageAccount.getKeys()` gibt die Speicherkontoschlüssel zurück. Verwenden Sie die `regenerateKey`-Methoden in `StorageAccount`, um die Schlüssel zu aktualisieren.

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [next-steps](includes/java-next-steps.md)]