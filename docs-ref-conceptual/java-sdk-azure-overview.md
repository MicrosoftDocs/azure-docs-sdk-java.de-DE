---
title: Azure-Bibliotheken für Java
description: Übersicht über die Azure-Verwaltungsbibliotheken und -Dienstbibliotheken für Java
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892731"
---
# <a name="azure-libraries-for-java"></a>Azure-Bibliotheken für Java

Die Azure-Bibliotheken für Java unterstützen Sie beim Verwalten von Azure-Ressourcen und stellen über Ihren Anwendungscode eine Verbindung mit Diensten her. Die Bibliotheken stehen als [Maven-Importe](java-sdk-azure-install.md) für die Verwendung in Ihren Java-Projekten zur Verfügung. 

## <a name="manage-azure-resources"></a>Verwalten von Azure-Ressourcen

Erstellen und verwalten Sie Azure-Ressourcen in Ihren Java-Anwendungen mithilfe der [Azure-Verwaltungsbibliotheken für Java](java-sdk-azure-get-started.md). Erstellen Sie mit diesen Bibliotheken eigene Azure-Automatisierungstools und -dienste. 

Zum Erstellen eines virtuellen Linux-Computers würden Sie beispielsweise den folgenden Code schreiben:

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

Eine vollständige Liste der Bibliotheken und Informationen zu ihrem Import in Ihre Projekte finden Sie in den [Installationsanweisungen](java-sdk-azure-install.md). Lesen Sie anschließend den [Artikel mit den ersten Schritten](java-sdk-azure-get-started.md), um die Authentifizierung einzurichten und Beispielcode für Ihr eigenes Azure-Abonnement auszuführen. 

## <a name="connect-to-azure-services"></a>Herstellen einer Verbindung mit Azure-Diensten

Mit Java-Bibliotheken können Sie nicht nur Ressourcen in Azure erstellen und verwalten, sondern diese auch in Ihren Apps verbinden und nutzen. Beispielsweise können Sie eine tabellarische SQL-Datenbank aktualisieren oder Dateien in Azure Storage speichern. Wählen Sie die für einen bestimmten Dienst erforderliche Bibliothek aus der [vollständigen Liste der Bibliotheken](java-sdk-azure-install.md) aus, und sehen Sie sich im [Java Developer Center](https://azure.microsoft.com/develop/java/) Tutorials und Beispielcode zur Verwendung in Ihren Apps an.

So drucken Sie beispielsweise die Inhalte der einzelnen Blobs in einem Azure-Speichercontainer aus:

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a>Beispielcode und Referenz

Die folgenden Beispiele behandeln allgemeine Automatisierungsaufgaben mit den Azure-Verwaltungsbibliotheken für Java und enthalten Code, der direkt in Ihren eigenen Apps verwendet werden kann:

- [Virtuelle Computer](java-sdk-azure-virtual-machine-samples.md)
- [Web-Apps](java-sdk-azure-web-apps-samples.md)
- [SQL-Datenbank](java-sdk-azure-sql-database-samples.md)
   
Sowohl in den Dienst- als auch den Verwaltungsbibliotheken ist eine [Referenz](https://docs.microsoft.com/java/api) für alle Pakete verfügbar. Neue Funktionen, wichtige Änderungen und Migrationsanweisungen aus älteren Versionen finden Sie in den [Versionshinweisen](java-sdk-azure-release-notes.md).