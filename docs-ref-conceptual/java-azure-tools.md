---
title: Tools für Azure-Java-Entwickler | Microsoft-Dokumentation
description: IDE-Integrationen, Emulatoren, Ressourcen-Explorer und Befehlszeilenschnittstellen für Java-Entwickler, die in Azure arbeiten.
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 11/13/2018
ms.author: routlaw
ms.openlocfilehash: 9e9828540ddc678f69eab11f5a61eef8bf8e916c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339014"
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="ee989-103">Azure-Tools für Java-Entwickler</span><span class="sxs-lookup"><span data-stu-id="ee989-103">Azure tools for Java developers</span></span>

## <a name="supported-jdk-runtimes"></a><span data-ttu-id="ee989-104">Unterstützte JDK-Runtimes</span><span class="sxs-lookup"><span data-stu-id="ee989-104">Supported JDK runtimes</span></span>

<span data-ttu-id="ee989-105">Java-Entwickler, die mit Azure und Azure Stack arbeiten, können Java 7-, 8- und 11-Produktionsanwendungen mithilfe von [Zulu Enterprise, einem OpenJDK-Build von Azul Systems](https://www.azul.com/downloads/azure-only/zulu/), erstellen und ausführen, ohne dabei zusätzliche Supportkosten zu erzeugen.</span><span class="sxs-lookup"><span data-stu-id="ee989-105">Java developers on Azure and Azure Stack can build and run production Java 7,8, and 11 applications using [Azul Systems Zulu Enterprise builds of OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="ee989-106">Wenn Sie Java-Apps derzeit mit anderen JDKs ausführen, sollten Sie über eine Migration zu Zulu in Azure nachdenken, um kostenlosen Support und kostenlose Wartung in Anspruch nehmen zu können.</span><span class="sxs-lookup"><span data-stu-id="ee989-106">If you’re currently running Java apps with other JDKs, consider migrating to Zulu on Azure for free support and maintenance.</span></span> 

<span data-ttu-id="ee989-107">Weitere Informationen zu den unterstützten JDKs, die für die Entwicklung in Azure verfügbar sind, finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="ee989-107">For more information about the supported JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="ee989-108">Eclipse- und IntelliJ-Plug-Ins</span><span class="sxs-lookup"><span data-stu-id="ee989-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="ee989-109">Mit den Azure-Toolkits für [Eclipse](eclipse/azure-toolkit-for-eclipse.md) und [IntelliJ](intellij/azure-toolkit-for-intellij.md) können Sie Azure-Ressourcen verwalten und Apps aus Ihrer IDE bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="ee989-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![IntelliJ-Toolkit mit dem Azure-Explorer](media/intelliJ-azure-explorer.png)

<span data-ttu-id="ee989-111">[Erste Schritte mit dem Azure-Toolkit für Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Erste Schritte mit dem Azure-Toolkit für IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="ee989-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="visual-studio-code"></a><span data-ttu-id="ee989-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ee989-112">Visual Studio Code</span></span>

<span data-ttu-id="ee989-113">[VS Code](https://code.visualstudio.com/) ist ein einfacher, aber leistungsstarker Code-Editor für MacOS, Windows und Linux.</span><span class="sxs-lookup"><span data-stu-id="ee989-113">[VS Code](https://code.visualstudio.com/) is a lightweight but powerful code editor available for MacOS, Windows, and Linux.</span></span> <span data-ttu-id="ee989-114">VS Code unterstützt über verschiedene Erweiterungen für Projektunterstützung, Codevervollständigung, Debugging, Linting und Navigation einen einfachen, modernen Java-Entwicklungsworkflow.</span><span class="sxs-lookup"><span data-stu-id="ee989-114">VS Code supports a simple, modern Java development workflow through a set of extensions that provide project support, code completion, debugging, linting, and navigation.</span></span>

<span data-ttu-id="ee989-115">[Erste Schritte mit VS Code und Java](https://code.visualstudio.com/docs/java)
[Java-Erweiterungspaket für VS Code](https://code.visualstudio.com/docs/java/extensions)</span><span class="sxs-lookup"><span data-stu-id="ee989-115">[Get Started with VS Code and Java](https://code.visualstudio.com/docs/java)
[Java extension pack for VS Code](https://code.visualstudio.com/docs/java/extensions)</span></span>  

## <a name="azure-cli-20"></a><span data-ttu-id="ee989-116">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ee989-116">Azure CLI 2.0</span></span>

<span data-ttu-id="ee989-117">Die Azure CLI 2.0 bietet eine Befehlszeilenumgebung für die Verwaltung von Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="ee989-117">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="ee989-118">Sie können sie in Ihrem Browser mit [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) verwenden oder unter macOS, Linux und Windows [installieren](https://docs.microsoft.com/cli/azure/install-azure-cli) und über die Befehlszeile ausführen.</span><span class="sxs-lookup"><span data-stu-id="ee989-118">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="ee989-119">[Erste Schritte mit der Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="ee989-119">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="ee989-120">Azure Storage-Explorer</span><span class="sxs-lookup"><span data-stu-id="ee989-120">Azure Storage Explorer</span></span> 

<span data-ttu-id="ee989-121">Verwalten Sie Azure-Speicherkonten, Container und Blobs/Dateien von Ihrem Desktop aus.</span><span class="sxs-lookup"><span data-stu-id="ee989-121">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="ee989-122">Der Azure Storage-Explorer ist derzeit als Vorschauversion für Windows, macOS und Linux verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ee989-122">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="ee989-123">Erste Schritte mit dem Azure Storage-Explorer (Vorschau)</span><span class="sxs-lookup"><span data-stu-id="ee989-123">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)
