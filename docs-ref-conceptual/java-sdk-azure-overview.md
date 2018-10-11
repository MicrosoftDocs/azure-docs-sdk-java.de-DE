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
# <a name="azure-libraries-for-java"></a><span data-ttu-id="b92ec-104">Azure-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="b92ec-104">Azure libraries for Java</span></span>

<span data-ttu-id="b92ec-105">Die Azure-Bibliotheken für Java unterstützen Sie beim Verwalten von Azure-Ressourcen und stellen über Ihren Anwendungscode eine Verbindung mit Diensten her.</span><span class="sxs-lookup"><span data-stu-id="b92ec-105">The Azure libraries for Java help you manage Azure resources and connect to services from your application code.</span></span> <span data-ttu-id="b92ec-106">Die Bibliotheken stehen als [Maven-Importe](java-sdk-azure-install.md) für die Verwendung in Ihren Java-Projekten zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="b92ec-106">The libraries are available as [Maven imports](java-sdk-azure-install.md) for use in your Java projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="b92ec-107">Verwalten von Azure-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="b92ec-107">Manage Azure resources</span></span>

<span data-ttu-id="b92ec-108">Erstellen und verwalten Sie Azure-Ressourcen in Ihren Java-Anwendungen mithilfe der [Azure-Verwaltungsbibliotheken für Java](java-sdk-azure-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b92ec-108">Create and manage Azure resources from your Java applications using the [Azure management libraries for Java](java-sdk-azure-get-started.md).</span></span> <span data-ttu-id="b92ec-109">Erstellen Sie mit diesen Bibliotheken eigene Azure-Automatisierungstools und -dienste.</span><span class="sxs-lookup"><span data-stu-id="b92ec-109">Use these libraries to build your own Azure automation tools and services.</span></span> 

<span data-ttu-id="b92ec-110">Zum Erstellen eines virtuellen Linux-Computers würden Sie beispielsweise den folgenden Code schreiben:</span><span class="sxs-lookup"><span data-stu-id="b92ec-110">For example, to create a Linux VM you would write the following code:</span></span>

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

<span data-ttu-id="b92ec-111">Eine vollständige Liste der Bibliotheken und Informationen zu ihrem Import in Ihre Projekte finden Sie in den [Installationsanweisungen](java-sdk-azure-install.md). Lesen Sie anschließend den [Artikel mit den ersten Schritten](java-sdk-azure-get-started.md), um die Authentifizierung einzurichten und Beispielcode für Ihr eigenes Azure-Abonnement auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b92ec-111">Review the [install instructions](java-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](java-sdk-azure-get-started.md) to set up your authentication and run sample code against your own Azure subscription.</span></span> 

## <a name="connect-to-azure-services"></a><span data-ttu-id="b92ec-112">Herstellen einer Verbindung mit Azure-Diensten</span><span class="sxs-lookup"><span data-stu-id="b92ec-112">Connect to Azure services</span></span>

<span data-ttu-id="b92ec-113">Mit Java-Bibliotheken können Sie nicht nur Ressourcen in Azure erstellen und verwalten, sondern diese auch in Ihren Apps verbinden und nutzen.</span><span class="sxs-lookup"><span data-stu-id="b92ec-113">In addition to using Java libraries to create and manage resources within Azure, you can also use Java libraries to connect  and use those resources in your apps.</span></span> <span data-ttu-id="b92ec-114">Beispielsweise können Sie eine tabellarische SQL-Datenbank aktualisieren oder Dateien in Azure Storage speichern.</span><span class="sxs-lookup"><span data-stu-id="b92ec-114">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="b92ec-115">Wählen Sie die für einen bestimmten Dienst erforderliche Bibliothek aus der [vollständigen Liste der Bibliotheken](java-sdk-azure-install.md) aus, und sehen Sie sich im [Java Developer Center](https://azure.microsoft.com/develop/java/) Tutorials und Beispielcode zur Verwendung in Ihren Apps an.</span><span class="sxs-lookup"><span data-stu-id="b92ec-115">Select the library you need for a particular service from the [complete list of libraries](java-sdk-azure-install.md) and visit the [Java developer center](https://azure.microsoft.com/develop/java/) for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="b92ec-116">So drucken Sie beispielsweise die Inhalte der einzelnen Blobs in einem Azure-Speichercontainer aus:</span><span class="sxs-lookup"><span data-stu-id="b92ec-116">For example, to print out the contents of every blob in an Azure storage container:</span></span>

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

## <a name="sample-code-and-reference"></a><span data-ttu-id="b92ec-117">Beispielcode und Referenz</span><span class="sxs-lookup"><span data-stu-id="b92ec-117">Sample code and reference</span></span>

<span data-ttu-id="b92ec-118">Die folgenden Beispiele behandeln allgemeine Automatisierungsaufgaben mit den Azure-Verwaltungsbibliotheken für Java und enthalten Code, der direkt in Ihren eigenen Apps verwendet werden kann:</span><span class="sxs-lookup"><span data-stu-id="b92ec-118">The following samples cover common automation tasks with the Azure management libraries for Java and have code ready to use in your own apps:</span></span>

- [<span data-ttu-id="b92ec-119">Virtuelle Computer</span><span class="sxs-lookup"><span data-stu-id="b92ec-119">Virtual machines</span></span>](java-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="b92ec-120">Web-Apps</span><span class="sxs-lookup"><span data-stu-id="b92ec-120">Web apps</span></span>](java-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="b92ec-121">SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="b92ec-121">SQL Database</span></span>](java-sdk-azure-sql-database-samples.md)
   
<span data-ttu-id="b92ec-122">Sowohl in den Dienst- als auch den Verwaltungsbibliotheken ist eine [Referenz](https://docs.microsoft.com/java/api) für alle Pakete verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b92ec-122">A [reference](https://docs.microsoft.com/java/api) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="b92ec-123">Neue Funktionen, wichtige Änderungen und Migrationsanweisungen aus älteren Versionen finden Sie in den [Versionshinweisen](java-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="b92ec-123">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](java-sdk-azure-release-notes.md).</span></span>