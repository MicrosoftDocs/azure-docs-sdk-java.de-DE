---
title: "Azure Resource Manager-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Resource Manager-Bibliotheken"
keywords: Azure, Java, SDK, API, Ressourcengruppen, ARM, Resource Manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 56199b87fa64e9cbf0a14716a58c01f11f0e433b
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/14/2017
---
# <a name="azure-resource-manager-libraries-for-java"></a><span data-ttu-id="e845c-104">Azure Resource Manager-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="e845c-104">Azure Resource Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="e845c-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="e845c-105">Overview</span></span>

<span data-ttu-id="e845c-106">Mit [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) können Sie Ressourcen in Gruppen bereitstellen, überwachen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="e845c-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="e845c-107">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="e845c-107">Management API</span></span>

<span data-ttu-id="e845c-108">Verwenden Sie die Verwaltungs-API zum Erstellen von Ressourcengruppen und Bereitstellen von Ressourcen aus Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="e845c-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

<span data-ttu-id="e845c-109">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="e845c-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="e845c-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="e845c-110">Example</span></span>

<span data-ttu-id="e845c-111">Erstellen Sie eine neue Ressourcengruppe in der Azure-Region „USA, Osten“.</span><span class="sxs-lookup"><span data-stu-id="e845c-111">Create a new resource group in the Azure Eastern US region.</span></span>

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e845c-112">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="e845c-112">Explore the Management APIs</span></span>](/java/api/overview/azure/resources/managementapi)

## <a name="samples"></a><span data-ttu-id="e845c-113">Beispiele</span><span class="sxs-lookup"><span data-stu-id="e845c-113">Samples</span></span>

<span data-ttu-id="e845c-114">[Verwalten von Azure-Ressourcengruppen mit Java][1] 
[Bereitstellen von Ressourcen mit einer ARM-Vorlage][2]</span><span class="sxs-lookup"><span data-stu-id="e845c-114">[Manage Azure Resource Groups with Java][1] 
[Deploy resources using an ARM template][2]</span></span>

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

<span data-ttu-id="e845c-115">Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) mit Azure Resource Manager-Beispielen an.</span><span class="sxs-lookup"><span data-stu-id="e845c-115">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) of Azure Resource Manager samples.</span></span>
