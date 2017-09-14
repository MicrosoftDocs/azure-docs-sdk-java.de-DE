---
title: "Versionshinweise zu Azure-Verwaltungsbibliotheken für Java | Microsoft-Dokumentation"
description: "Informieren Sie sich über Neuigkeiten und wichtige Änderungen in den Azure-Verwaltungsbibliotheken für Java."
keywords: Azure, Java, API, Referenz, Hinweise, Updates, veraltet
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a><span data-ttu-id="db946-104">Versionsinformationen</span><span class="sxs-lookup"><span data-stu-id="db946-104">Release Notes</span></span> 

## <a name="june-30-2017---110"></a><span data-ttu-id="db946-105">30. Juni 2017: 1.1.0</span><span class="sxs-lookup"><span data-stu-id="db946-105">June 30, 2017 - 1.1.0</span></span> 

<span data-ttu-id="db946-106">V1.1 ist in den für die öffentliche Verwendung vorgesehenen APIs, die in V1.0 die (stabile) Phase der allgemeinen Verfügbarkeit erreicht haben, abwärtskompatibel mit V1.0.</span><span class="sxs-lookup"><span data-stu-id="db946-106">V1.1 is backwards compatible with V1.0 in the APIs intended for public use that reached the general availability (stable) stage in V1.0.</span></span>

<span data-ttu-id="db946-107">Für APIs, die in V.0 mit der Anmerkung @Beta markiert waren, wurden einige wichtige Änderungen eingeführt.</span><span class="sxs-lookup"><span data-stu-id="db946-107">Some breaking changes were introduced in APIs marked with the @Beta annotation in V.0</span></span>

<span data-ttu-id="db946-108">Wenn Sie Ihren Code zu 1.1.0 migrieren möchten, können Sie Ihren 1.0.0-Code anhand [dieser Hinweise](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) für 1.1.0 vorbereiten.</span><span class="sxs-lookup"><span data-stu-id="db946-108">If you are migrating your code to 1.1.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) for preparing your code for 1.1.0 from 1.0.0.</span></span>

### <a name="generally-availabile-in-v11"></a><span data-ttu-id="db946-109">Allgemein verfügbar in V1.1</span><span class="sxs-lookup"><span data-stu-id="db946-109">Generally availabile in V1.1</span></span>

<span data-ttu-id="db946-110">Einige der Beta-APIs aus V1.0 sind in V1.1 nun allgemein verfügbar. Hierzu zählen insbesondere folgende:</span><span class="sxs-lookup"><span data-stu-id="db946-110">Some of the APIs that were still in Beta in V1.0 are now GA in V1.1, in particular:</span></span>

- <span data-ttu-id="db946-111">Asynchrone Methoden</span><span class="sxs-lookup"><span data-stu-id="db946-111">async methods</span></span>
- <span data-ttu-id="db946-112">Alle Methoden im CDN, die sich zuvor noch in der Betaphase befanden</span><span class="sxs-lookup"><span data-stu-id="db946-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="db946-113">Alle Methoden und Schnittstellen in Anwendungsgateways, die sich zuvor noch in der Betaphase befanden</span><span class="sxs-lookup"><span data-stu-id="db946-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="db946-114">Teile der Bibliothek befinden sich immer noch in der Vorschauphase.</span><span class="sxs-lookup"><span data-stu-id="db946-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="db946-115">Die folgende Tabelle gibt Aufschluss über den aktuellen Status der Bibliotheken:</span><span class="sxs-lookup"><span data-stu-id="db946-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="db946-116">Dienst oder Feature</span><span class="sxs-lookup"><span data-stu-id="db946-116">Service or feature</span></span> | <span data-ttu-id="db946-117">Allgemein verfügbar</span><span class="sxs-lookup"><span data-stu-id="db946-117">Available as GA</span></span> | <span data-ttu-id="db946-118">Als Vorschauversion verfügbar</span><span class="sxs-lookup"><span data-stu-id="db946-118">Available as Preview</span></span>  | <span data-ttu-id="db946-119">In Kürze verfügbar</span><span class="sxs-lookup"><span data-stu-id="db946-119">Coming soon</span></span> |
---------|---------|---------|---------|
<span data-ttu-id="db946-120">Compute</span><span class="sxs-lookup"><span data-stu-id="db946-120">Compute</span></span>  | <span data-ttu-id="db946-121">Virtuelle Computer und VM-Erweiterungen, VM-Skalierungsgruppen, verwaltete Datenträger</span><span class="sxs-lookup"><span data-stu-id="db946-121">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="db946-122">Azure Container Service, Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="db946-122">Azure container service, Azure container registry</span></span> |    |
<span data-ttu-id="db946-123">Speicher</span><span class="sxs-lookup"><span data-stu-id="db946-123">Storage</span></span>   |  <span data-ttu-id="db946-124">Speicherkonten</span><span class="sxs-lookup"><span data-stu-id="db946-124">Storage accounts</span></span>       |         |   <span data-ttu-id="db946-125">Verschlüsselung</span><span class="sxs-lookup"><span data-stu-id="db946-125">Encryption</span></span>      |
<span data-ttu-id="db946-126">SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="db946-126">SQL Database</span></span>  | <span data-ttu-id="db946-127">Datenbanken, Firewalls, Pools für elastische Datenbanken</span><span class="sxs-lookup"><span data-stu-id="db946-127">Databases, firewalls, elastic pools</span></span>        |         |   <span data-ttu-id="db946-128">Weitere Features</span><span class="sxs-lookup"><span data-stu-id="db946-128">More features</span></span>      |
<span data-ttu-id="db946-129">Netzwerk</span><span class="sxs-lookup"><span data-stu-id="db946-129">Networking</span></span>    |  <span data-ttu-id="db946-130">Virtuelle Netzwerke, Netzwerkschnittstellen, IP-Adressen, Routingtabellen, Netzwerksicherheitsgruppen, DNS, Traffic Manager, Anwendungsgateways</span><span class="sxs-lookup"><span data-stu-id="db946-130">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="db946-131">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="db946-131">Load balancers</span></span>     |   <span data-ttu-id="db946-132">VPN, Network Watcher</span><span class="sxs-lookup"><span data-stu-id="db946-132">VPN, Network watchers</span></span>   |
<span data-ttu-id="db946-133">Weitere Dienste</span><span class="sxs-lookup"><span data-stu-id="db946-133">More services</span></span>    |  <span data-ttu-id="db946-134">Ressourcen-Manager, Key Vault, Redis, CDN, Batch</span><span class="sxs-lookup"><span data-stu-id="db946-134">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="db946-135">Web-Apps, Funkions-Apps, Service Bus, Graph RBAC, DocumentDB</span><span class="sxs-lookup"><span data-stu-id="db946-135">Web apps, Function apps, Service Bus, Graph RBAC, DocumentDB</span></span>   | <span data-ttu-id="db946-136">Überwachung, Planung, Funktionsverwaltung, Suche, weitere Graph RBAC-Features</span><span class="sxs-lookup"><span data-stu-id="db946-136">Monitor ,Scheduler, Functions management, Search, more Graph RBAC features</span></span>        |
<span data-ttu-id="db946-137">Grundlagen</span><span class="sxs-lookup"><span data-stu-id="db946-137">Fundamentals</span></span>     |   <span data-ttu-id="db946-138">Authentifizierung: Core, asynchrone Methoden</span><span class="sxs-lookup"><span data-stu-id="db946-138">Authentication - core , Async methods</span></span>       |      |         |

### <a name="import-with-maven"></a><span data-ttu-id="db946-139">Importieren mit Maven</span><span class="sxs-lookup"><span data-stu-id="db946-139">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="db946-140">Hilfe und Feedback</span><span class="sxs-lookup"><span data-stu-id="db946-140">Get help and give feedback</span></span>

<span data-ttu-id="db946-141">Besuchen Sie die [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk)-Community, um Hilfe bei der Verwendung der Bibliotheken in Ihrem eigenen Code zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="db946-141">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="db946-142">Fehler oder Verbesserungsvorschläge für die Bibliotheken können über [GitHub](https://github.com/Azure/azure-sdk-for-java/issues) gemeldet bzw. eingereicht werden.</span><span class="sxs-lookup"><span data-stu-id="db946-142">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>

### <a name="migrate-from-previous-releases"></a><span data-ttu-id="db946-143">Migrieren von früheren Versionen</span><span class="sxs-lookup"><span data-stu-id="db946-143">Migrate from previous releases</span></span>

<span data-ttu-id="db946-144">[Migrieren von 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [Migrieren von 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span><span class="sxs-lookup"><span data-stu-id="db946-144">[Migrate from 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migrate from 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span></span>


