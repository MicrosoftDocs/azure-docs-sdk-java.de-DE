---
title: "Azure Batch-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Batch-Bibliotheken"
keywords: "Azure, Java, SDK, API, Batch, Verarbeitung, Planung, lange Ausführungszeit"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: 2c9fab2834ea6d9c906d9483aed839a0411aaa40
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2017
---
# <a name="azure-batch-libraries-for-java"></a>Azure Batch-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Effizientes Ausführen umfangreicher paralleler HPC-Anwendungen in der Cloud mit [Azure Batch](/azure/batch/batch-technical-overview).   

Informationen zu den ersten Schritte mit Azure Batch finden Sie unter [Erstellen eines Batch-Kontos mit dem Azure-Portal](/azure/batch/batch-account-create-portal).

## <a name="client-library"></a>Clientbibliothek

Mit den Azure Batch-Clientbibliotheken können Sie Computeknoten und -pools konfigurieren, Aufgaben definieren und ihre Ausführung in Aufträgen konfigurieren sowie einen Auftrags-Manager zum Steuern und Überwachen der Auftragsausführung einrichten. [Erfahren Sie mehr](/azure/batch/batch-api-basics) über die Verwendung dieser Objekte zum Ausführen umfangreicher paralleler Computelösungen.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Einrichten eines Pools mit Linux-Computeknoten in einem Batch-Konto:

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/java/api/overview/azure/batch/clientlibrary)


## <a name="management-api"></a>Verwaltungs-API

Verwenden Sie die Azure Batch-Verwaltungsbibliotheken zum Erstellen und Löschen von Batch-Konten, zum Lesen und erneuten Generieren von Batch-Kontoschlüsseln sowie zum Verwalten von Batch-Kontospeicher.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Beispiel

Erstellen Sie ein Azure Batch-Konto, und konfigurieren Sie dafür eine neue Anwendung und ein neues Azure-Speicherkonto.

```java
BatchAccount batchAccount = azure.batchAccounts().define("newBatchAcct")
    .withRegion(Region.US_EAST)
    .withNewResourceGroup("myResourceGroup")
    .defineNewApplication("batchAppName")
        .defineNewApplicationPackage(applicationPackageName)
        .withAllowUpdates(true)
        .withDisplayName(applicationDisplayName)
        .attach()
    .withNewStorageAccount("batchStorageAcct")
    .create();
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/batch/managementapi)


## <a name="samples"></a>Beispiele

[Verwalten von Batch-Konten][1]   

Sehen Sie sich weitere [Java-Codebeispiele für Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) an, die Sie in Ihren Apps verwenden können.

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts