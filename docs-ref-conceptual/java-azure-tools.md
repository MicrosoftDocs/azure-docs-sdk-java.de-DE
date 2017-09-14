---
title: "Tools für Azure-Java-Entwickler | Microsoft-Dokumentation"
description: "IDE-Integrationen, Emulatoren, Ressourcen-Explorer und Befehlszeilenschnittstellen für Java-Entwickler, die in Azure arbeiten."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: ce0b003cc7c48c8690f4236547ddec36e6ea9d53
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2017
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="e0583-103">Azure-Tools für Java-Entwickler</span><span class="sxs-lookup"><span data-stu-id="e0583-103">Azure tools for Java developers</span></span>

## <a name="client-and-management-libraries"></a><span data-ttu-id="e0583-104">Client- und Verwaltungsbibliotheken</span><span class="sxs-lookup"><span data-stu-id="e0583-104">Client and management libraries</span></span>

<span data-ttu-id="e0583-105">Mit den Azure-Bibliotheken für Java können Sie über Ihre Anwendungen eine Verbindung mit Diensten herstellen und Azure-Ressourcen verwalten.</span><span class="sxs-lookup"><span data-stu-id="e0583-105">Connect to services and manage Azure resources from your applications with the Azure libraries for Java.</span></span> <span data-ttu-id="e0583-106">Fügen Sie Ihrer Projektdatei *pom.xml* die folgende Abhängigkeit hinzu, um die Verwaltungsbibliotheken in Ihre Maven-Projekte zu importieren:</span><span class="sxs-lookup"><span data-stu-id="e0583-106">Import the management libraries into your Maven projects by adding this dependency to your project *pom.xml*.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

<span data-ttu-id="e0583-107">Weitere Informationen finden Sie in der [vollständigen Bibliothekenliste](java-sdk-azure-install.md) und in den [ersten Schritten mit den Azure-Bibliotheken für Java](java-sdk-azure-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0583-107">View the [complete list of libraries](java-sdk-azure-install.md) and [get started](java-sdk-azure-get-started.md) with the Azure libraries for Java.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="e0583-108">Eclipse- und IntelliJ-Plug-Ins</span><span class="sxs-lookup"><span data-stu-id="e0583-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="e0583-109">Mit den Azure-Toolkits für [Eclipse](eclipse/azure-toolkit-for-eclipse.md) und [IntelliJ](intellij/azure-toolkit-for-intellij.md) können Sie Azure-Ressourcen verwalten und Apps aus Ihrer IDE bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e0583-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![IntelliJ-Toolkit mit dem Azure-Explorer](media/intelliJ-azure-explorer.png)

<span data-ttu-id="e0583-111">[Erste Schritte mit dem Azure-Toolkit für Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Erste Schritte mit dem Azure-Toolkit für IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="e0583-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="azure-cli-20"></a><span data-ttu-id="e0583-112">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e0583-112">Azure CLI 2.0</span></span>

<span data-ttu-id="e0583-113">Die Azure CLI 2.0 bietet eine Befehlszeilenumgebung für die Verwaltung von Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="e0583-113">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="e0583-114">Sie können sie in Ihrem Browser mit [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) verwenden oder unter macOS, Linux und Windows [installieren](https://docs.microsoft.com/cli/azure/install-azure-cli) und über die Befehlszeile ausführen.</span><span class="sxs-lookup"><span data-stu-id="e0583-114">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="e0583-115">[Erste Schritte mit der Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="e0583-115">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="e0583-116">Azure-Speicher-Explorer</span><span class="sxs-lookup"><span data-stu-id="e0583-116">Azure Storage Explorer</span></span> 

<span data-ttu-id="e0583-117">Verwalten Sie Azure-Speicherkonten, Container und Blobs/Dateien von Ihrem Desktop aus.</span><span class="sxs-lookup"><span data-stu-id="e0583-117">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="e0583-118">Der Azure-Speicher-Explorer ist derzeit als Vorschauversion für Windows, macOS und Linux verfügbar.</span><span class="sxs-lookup"><span data-stu-id="e0583-118">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="e0583-119">Erste Schritte mit dem Speicher-Explorer (Vorschau)</span><span class="sxs-lookup"><span data-stu-id="e0583-119">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)