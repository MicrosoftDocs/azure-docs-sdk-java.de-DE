---
title: Azure Batch-Bibliotheken für Java
description: Referenzdokumentation für die Java-Batch-Bibliotheken
keywords: Azure, Java, SDK, API, Batch, Verarbeitung, Planung, lange Ausführungszeit
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: d8e7a6969bf35d98f03c5d3e335fbaf2f6b3a51d
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324357"
---
# <a name="azure-batch-libraries-for-java"></a><span data-ttu-id="ad617-104">Azure Batch-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="ad617-104">Azure Batch libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="ad617-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="ad617-105">Overview</span></span>

<span data-ttu-id="ad617-106">Effizientes Ausführen umfangreicher paralleler HPC-Anwendungen in der Cloud mit [Azure Batch](/azure/batch/batch-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="ad617-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>   

<span data-ttu-id="ad617-107">Informationen zu den ersten Schritte mit Azure Batch finden Sie unter [Erstellen eines Batch-Kontos mit dem Azure-Portal](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="ad617-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="client-library"></a><span data-ttu-id="ad617-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="ad617-108">Client library</span></span>

<span data-ttu-id="ad617-109">Mit den Azure Batch-Clientbibliotheken können Sie Computeknoten und -pools konfigurieren, Aufgaben definieren und ihre Ausführung in Aufträgen konfigurieren sowie einen Auftrags-Manager zum Steuern und Überwachen der Auftragsausführung einrichten.</span><span class="sxs-lookup"><span data-stu-id="ad617-109">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="ad617-110">[Erfahren Sie mehr](/azure/batch/batch-api-basics) über die Verwendung dieser Objekte zum Ausführen umfangreicher paralleler Computelösungen.</span><span class="sxs-lookup"><span data-stu-id="ad617-110">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

<span data-ttu-id="ad617-111">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ad617-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span> <span data-ttu-id="ad617-112">Der Quellcode der Clientbibliothek steht auf [GitHub](https://github.com/Azure/azure-batch-sdk-for-java) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="ad617-112">The client library source code can be found in [Github](https://github.com/Azure/azure-batch-sdk-for-java).</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>4.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="ad617-113">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ad617-113">Example</span></span>

<span data-ttu-id="ad617-114">Einrichten eines Pools mit Linux-Computeknoten in einem Batch-Konto:</span><span class="sxs-lookup"><span data-stu-id="ad617-114">Set up a pool of Linux compute nodes in a batch account:</span></span>

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad617-115">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="ad617-115">Explore the Client APIs</span></span>](/java/api/overview/azure/batch/client)


## <a name="management-api"></a><span data-ttu-id="ad617-116">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="ad617-116">Management API</span></span>

<span data-ttu-id="ad617-117">Verwenden Sie die Azure Batch-Verwaltungsbibliotheken zum Erstellen und Löschen von Batch-Konten, zum Lesen und erneuten Generieren von Batch-Kontoschlüsseln sowie zum Verwalten von Batch-Kontospeicher.</span><span class="sxs-lookup"><span data-stu-id="ad617-117">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

<span data-ttu-id="ad617-118">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ad617-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="ad617-119">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ad617-119">Example</span></span>

<span data-ttu-id="ad617-120">Erstellen Sie ein Azure Batch-Konto, und konfigurieren Sie dafür eine neue Anwendung und ein neues Azure-Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="ad617-120">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

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
> [<span data-ttu-id="ad617-121">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="ad617-121">Explore the Management APIs</span></span>](/java/api/overview/azure/batch/management)


## <a name="samples"></a><span data-ttu-id="ad617-122">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ad617-122">Samples</span></span>

<span data-ttu-id="ad617-123">[Verwalten von Batch-Konten][1]</span><span class="sxs-lookup"><span data-stu-id="ad617-123">[Manage Batch accounts][1]</span></span>   

<span data-ttu-id="ad617-124">Sehen Sie sich weitere [Java-Codebeispiele für Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ad617-124">Explore more [sample Java code for Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) you can use in your apps.</span></span>

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts
