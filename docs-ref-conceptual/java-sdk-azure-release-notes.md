---
title: Versionshinweise zu Azure-Verwaltungsbibliotheken für Java | Microsoft-Dokumentation
description: Informieren Sie sich über Neuigkeiten und wichtige Änderungen in den Azure-Verwaltungsbibliotheken für Java.
keywords: Azure, Java, API, Referenz, Hinweise, Updates, veraltet
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 0aaa83ceb42192441decb5972baae56fed337fb2
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090683"
---
# <a name="release-notes"></a><span data-ttu-id="d195b-104">Versionsinformationen</span><span class="sxs-lookup"><span data-stu-id="d195b-104">Release Notes</span></span> 

## <a name="october-5-2017---130"></a><span data-ttu-id="d195b-105">5. Oktober 2017 – 1.3.0</span><span class="sxs-lookup"><span data-stu-id="d195b-105">October 5, 2017 - 1.3.0</span></span> 

<span data-ttu-id="d195b-106">Version 1.3.0 ist abwärtskompatibel mit vorherigen Versionen zur Verwendung von Diensten und Features, die in vorherigen Releases die (stabile) Phase der allgemeinen Verfügbarkeit erreicht haben.</span><span class="sxs-lookup"><span data-stu-id="d195b-106">Version 1.3.0 is backwards compatible with previous versions for services and features use that reached the general availability (stable) stage in previous releases.</span></span>

<span data-ttu-id="d195b-107">Für diese Dienste sind wichtige Änderungen aus Vorschauversionen mit der Anmerkung @Beta versehen.</span><span class="sxs-lookup"><span data-stu-id="d195b-107">Any breaking changes from Preview versions for those services are marked with the @Beta annotation.</span></span>

<span data-ttu-id="d195b-108">Wenn Sie Ihren Code zu 1.3.0 migrieren möchten, können Sie Ihren vorhandenen Code anhand [dieser Hinweise](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) für die Version 1.3 vorbereiten.</span><span class="sxs-lookup"><span data-stu-id="d195b-108">If you are migrating your code to 1.3.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) to prepare your existing code for the 1.3 version.</span></span>

### <a name="generally-availabile-in-v13"></a><span data-ttu-id="d195b-109">Allgemein verfügbar in V1.3</span><span class="sxs-lookup"><span data-stu-id="d195b-109">Generally availabile in V1.3</span></span>

<span data-ttu-id="d195b-110">Einige der Beta-APIs aus vorherigen Releases sind nun allgemein verfügbar. Hierzu zählen insbesondere folgende:</span><span class="sxs-lookup"><span data-stu-id="d195b-110">Some of the APIs that were still in Beta in previous releases are now GA, in particular:</span></span>

- <span data-ttu-id="d195b-111">Asynchrone Methoden</span><span class="sxs-lookup"><span data-stu-id="d195b-111">async methods</span></span>
- <span data-ttu-id="d195b-112">Alle Methoden im CDN, die sich zuvor noch in der Betaphase befanden</span><span class="sxs-lookup"><span data-stu-id="d195b-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="d195b-113">Alle Methoden und Schnittstellen in Anwendungsgateways, die sich zuvor noch in der Betaphase befanden</span><span class="sxs-lookup"><span data-stu-id="d195b-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

  <span data-ttu-id="d195b-114">Teile der Bibliothek befinden sich immer noch in der Vorschauphase.</span><span class="sxs-lookup"><span data-stu-id="d195b-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="d195b-115">Die folgende Tabelle gibt Aufschluss über den aktuellen Status der Bibliotheken:</span><span class="sxs-lookup"><span data-stu-id="d195b-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="d195b-116">Dienst oder Feature</span><span class="sxs-lookup"><span data-stu-id="d195b-116">Service or feature</span></span> | <span data-ttu-id="d195b-117">Allgemein verfügbar</span><span class="sxs-lookup"><span data-stu-id="d195b-117">Available as GA</span></span> | <span data-ttu-id="d195b-118">Als Vorschauversion verfügbar</span><span class="sxs-lookup"><span data-stu-id="d195b-118">Available as Preview</span></span> 
---------|---------|---------|-
<span data-ttu-id="d195b-119">Compute</span><span class="sxs-lookup"><span data-stu-id="d195b-119">Compute</span></span>  | <span data-ttu-id="d195b-120">Virtuelle Computer und VM-Erweiterungen, VM-Skalierungsgruppen, verwaltete Datenträger</span><span class="sxs-lookup"><span data-stu-id="d195b-120">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="d195b-121">Azure Container Service, Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d195b-121">Azure container service, Azure container registry</span></span> 
<span data-ttu-id="d195b-122">Speicher</span><span class="sxs-lookup"><span data-stu-id="d195b-122">Storage</span></span>   |  <span data-ttu-id="d195b-123">Speicherkonten</span><span class="sxs-lookup"><span data-stu-id="d195b-123">Storage accounts</span></span>       |    <span data-ttu-id="d195b-124">Verschlüsselung</span><span class="sxs-lookup"><span data-stu-id="d195b-124">Encryption</span></span>     
<span data-ttu-id="d195b-125">SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="d195b-125">SQL Database</span></span>  | <span data-ttu-id="d195b-126">Datenbanken, Firewalls, Pools für elastische Datenbanken</span><span class="sxs-lookup"><span data-stu-id="d195b-126">Databases, firewalls, elastic pools</span></span>              
<span data-ttu-id="d195b-127">Netzwerk</span><span class="sxs-lookup"><span data-stu-id="d195b-127">Networking</span></span>    |  <span data-ttu-id="d195b-128">Virtuelle Netzwerke, Netzwerkschnittstellen, IP-Adressen, Routingtabellen, Netzwerksicherheitsgruppen, DNS, Traffic Manager, Anwendungsgateways</span><span class="sxs-lookup"><span data-stu-id="d195b-128">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="d195b-129">Lastenausgleichsmodule, Netzwerkpeering, Gateway für virtuelle Netzwerke, Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d195b-129">Load balancers, Network peering, Virtual Network Gateway, Network watchers</span></span> 
<span data-ttu-id="d195b-130">Weitere Dienste</span><span class="sxs-lookup"><span data-stu-id="d195b-130">More services</span></span>    |  <span data-ttu-id="d195b-131">Ressourcen-Manager, Key Vault, Redis, CDN, Batch</span><span class="sxs-lookup"><span data-stu-id="d195b-131">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="d195b-132">Web-Apps, Funktions-Apps, Service Bus, Graph (rollenbasierte Zugriffssteuerung), Cosmos DB, Search</span><span class="sxs-lookup"><span data-stu-id="d195b-132">Web apps, Function apps, Service Bus, Graph RBAC, Cosmos DB, Search</span></span>  
<span data-ttu-id="d195b-133">Grundlagen</span><span class="sxs-lookup"><span data-stu-id="d195b-133">Fundamentals</span></span>     |   <span data-ttu-id="d195b-134">Authentifizierung: Core, asynchrone Methoden, verwaltete Dienstidentität</span><span class="sxs-lookup"><span data-stu-id="d195b-134">Authentication - core , Async methods , Managed Service Identity</span></span>      |      |

> <span data-ttu-id="d195b-135">Vorschaufeatures sind in Bibliotheken auf Klassen-, Schnittstellen- oder Methodenebene mit dem Hinweis `@Beta` gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="d195b-135">Preview features are marked with a `@Beta` annotation at the class or interface or method level in libraries.</span></span> <span data-ttu-id="d195b-136">Bei diesen Funktionen sind Änderungen vorbehalten.</span><span class="sxs-lookup"><span data-stu-id="d195b-136">These features are subject to change.</span></span> <span data-ttu-id="d195b-137">Sie können in Zukunft auf beliebige Weise geändert (oder sogar entfernt) werden.</span><span class="sxs-lookup"><span data-stu-id="d195b-137">They can be modified in any way, or even removed, in the future.</span></span>

### <a name="import-with-maven"></a><span data-ttu-id="d195b-138">Importieren mit Maven</span><span class="sxs-lookup"><span data-stu-id="d195b-138">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="d195b-139">Hilfe und Feedback</span><span class="sxs-lookup"><span data-stu-id="d195b-139">Get help and give feedback</span></span>

<span data-ttu-id="d195b-140">Besuchen Sie die [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk)-Community, um Hilfe bei der Verwendung der Bibliotheken in Ihrem eigenen Code zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="d195b-140">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="d195b-141">Fehler oder Verbesserungsvorschläge für die Bibliotheken können über [GitHub](https://github.com/Azure/azure-sdk-for-java/issues) gemeldet bzw. eingereicht werden.</span><span class="sxs-lookup"><span data-stu-id="d195b-141">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>


