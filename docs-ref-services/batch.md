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
# <a name="azure-batch-libraries-for-java"></a><span data-ttu-id="185a2-104">Azure Batch-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="185a2-104">Azure Batch libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="185a2-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="185a2-105">Overview</span></span>

<span data-ttu-id="185a2-106">Effizientes Ausführen umfangreicher paralleler HPC-Anwendungen in der Cloud mit [Azure Batch](/azure/batch/batch-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="185a2-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>   

<span data-ttu-id="185a2-107">Informationen zu den ersten Schritte mit Azure Batch finden Sie unter [Erstellen eines Batch-Kontos mit dem Azure-Portal](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="185a2-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="client-library"></a><span data-ttu-id="185a2-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="185a2-108">Client library</span></span>

<span data-ttu-id="185a2-109">Mit den Azure Batch-Clientbibliotheken können Sie Computeknoten und -pools konfigurieren, Aufgaben definieren und ihre Ausführung in Aufträgen konfigurieren sowie einen Auftrags-Manager zum Steuern und Überwachen der Auftragsausführung einrichten.</span><span class="sxs-lookup"><span data-stu-id="185a2-109">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="185a2-110">[Erfahren Sie mehr](/azure/batch/batch-api-basics) über die Verwendung dieser Objekte zum Ausführen umfangreicher paralleler Computelösungen.</span><span class="sxs-lookup"><span data-stu-id="185a2-110">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

<span data-ttu-id="185a2-111">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="185a2-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="185a2-112">Beispiel</span><span class="sxs-lookup"><span data-stu-id="185a2-112">Example</span></span>

<span data-ttu-id="185a2-113">Einrichten eines Pools mit Linux-Computeknoten in einem Batch-Konto:</span><span class="sxs-lookup"><span data-stu-id="185a2-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="185a2-114">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="185a2-114">Explore the Client APIs</span></span>](/java/api/overview/azure/batch/clientlibrary)


## <a name="management-api"></a><span data-ttu-id="185a2-115">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="185a2-115">Management API</span></span>

<span data-ttu-id="185a2-116">Verwenden Sie die Azure Batch-Verwaltungsbibliotheken zum Erstellen und Löschen von Batch-Konten, zum Lesen und erneuten Generieren von Batch-Kontoschlüsseln sowie zum Verwalten von Batch-Kontospeicher.</span><span class="sxs-lookup"><span data-stu-id="185a2-116">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

<span data-ttu-id="185a2-117">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="185a2-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="185a2-118">Beispiel</span><span class="sxs-lookup"><span data-stu-id="185a2-118">Example</span></span>

<span data-ttu-id="185a2-119">Erstellen Sie ein Azure Batch-Konto, und konfigurieren Sie dafür eine neue Anwendung und ein neues Azure-Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="185a2-119">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

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
> [<span data-ttu-id="185a2-120">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="185a2-120">Explore the Management APIs</span></span>](/java/api/overview/azure/batch/managementapi)


## <a name="samples"></a><span data-ttu-id="185a2-121">Beispiele</span><span class="sxs-lookup"><span data-stu-id="185a2-121">Samples</span></span>

<span data-ttu-id="185a2-122">[Verwalten von Batch-Konten][1]</span><span class="sxs-lookup"><span data-stu-id="185a2-122">[Manage Batch accounts][1]</span></span>   

<span data-ttu-id="185a2-123">Sehen Sie sich weitere [Java-Codebeispiele für Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="185a2-123">Explore more [sample Java code for Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) you can use in your apps.</span></span>

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts