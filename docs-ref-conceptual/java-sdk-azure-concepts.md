---
title: Entwicklerhandbuch für die Azure-Verwaltungsbibliotheken für Java
description: Muster und Konzepte für die Verwendung der Java-Verwaltungsbibliotheken zum Verwalten von Cloudressourcen in Azure.
keywords: Azure, Java, SDK, API, Maven, Gradle, Authentifizierung, Active Directory, Dienstprinzipal
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: f452468b-7aae-4944-abad-0b1aaf19170d
ms.openlocfilehash: 4e7d5ea8b796733ab9386ea5ee37f935a4347a18
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593217"
---
# <a name="patterns-and-best-practices-for-development-with-the-azure-libraries-for-java"></a><span data-ttu-id="c886a-104">Muster und bewährte Methoden für die Entwicklung mit den Azure-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="c886a-104">Patterns and best practices for development with the Azure libraries for Java</span></span> 

<span data-ttu-id="c886a-105">In diesem Artikel sind verschiedene Muster und bewährte Methoden für die Verwendung der Azure-Bibliotheken für Java in Ihren Projekten aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="c886a-105">This article lists a series of patterns and best practices when using the Azure libraries for Java in your projects.</span></span> <span data-ttu-id="c886a-106">Verwenden Sie bei der Entwicklung diese Muster und Richtlinien, um die zu verwaltende Codemenge zu reduzieren und das Hinzufügen oder Konfigurieren zusätzlicher Ressourcen in künftigen Aktualisierungen der Verwaltungsbibliotheken zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="c886a-106">Develop with these patterns and guidelines to reduce the amount of code to maintain and make it easier to add or configure additional resources in future updates to the management libraries.</span></span>

## <a name="build-resources-through-a-fluent-interface"></a><span data-ttu-id="c886a-107">Erstellen von Ressourcen über eine Fluent-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="c886a-107">Build resources through a fluent interface</span></span>

<span data-ttu-id="c886a-108">Eine Fluent-Schnittstelle ist ein Muster, das Objekte mithilfe einer Methodenkette erstellt, die die Attribute des Objekts korrekt konfiguriert –</span><span class="sxs-lookup"><span data-stu-id="c886a-108">A fluent interface is a pattern that creates objects using a method chain that correctly configures the object's attributes.</span></span> <span data-ttu-id="c886a-109">beispielsweise, um ein neues Azure Storage-Konto zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c886a-109">For example, to create a new Azure Storage account</span></span>

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

<span data-ttu-id="c886a-110">Beim Durchlaufen der Methodenkette schlägt die IDE den nächsten Methodenaufruf in der Fluent-Konversation vor.</span><span class="sxs-lookup"><span data-stu-id="c886a-110">As you go through the method chain, your IDE suggests the next method to call in the fluent conversation.</span></span>   

![GIF der IntelliJ-Befehlsvervollständigung im Rahmen einer Fluent-Kette](media/intelliJFluent.gif)

<span data-ttu-id="c886a-112">Verketten Sie die von der IDE vorgeschlagenen Methoden, solange diese für die zu definierende Azure-Ressource sinnvoll sind.</span><span class="sxs-lookup"><span data-stu-id="c886a-112">Chain the methods suggested by the IDE as long as they make sense for the Azure resource being defined.</span></span> <span data-ttu-id="c886a-113">Sollte in der Kette eine erforderliche Methode fehlen, wird dies durch die IDE mit einem Fehler gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="c886a-113">If you are missing a required method in the chain your IDE will highlight it with an error.</span></span>

## <a name="resource-collections"></a><span data-ttu-id="c886a-114">Ressourcensammlungen</span><span class="sxs-lookup"><span data-stu-id="c886a-114">Resource collections</span></span>

<span data-ttu-id="c886a-115">Die Verwaltungsbibliothek besitzt für die Erstellung und Aktualisierung von Ressourcen einen einzelnen Zugangspunkt über das Objekt `com.microsoft.azure.management.Azure` der obersten Ebene.</span><span class="sxs-lookup"><span data-stu-id="c886a-115">The management library has a single point of entry through the top-level `com.microsoft.azure.management.Azure` object to create and update resources.</span></span> <span data-ttu-id="c886a-116">Wählen Sie mithilfe der im Objekt `Azure` definierten Ressourcensammlungsmethoden aus, mit welcher Art von Ressourcen Sie arbeiten möchten.</span><span class="sxs-lookup"><span data-stu-id="c886a-116">Select which type of resources to work with using the resource collection methods defined in the `Azure` object.</span></span> <span data-ttu-id="c886a-117">Beispiel für SQL-Datenbank:</span><span class="sxs-lookup"><span data-stu-id="c886a-117">For example, SQL Database:</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a><span data-ttu-id="c886a-118">Listen und Iterationen</span><span class="sxs-lookup"><span data-stu-id="c886a-118">Lists and iterations</span></span>

<span data-ttu-id="c886a-119">Jede Ressourcensammlung verfügt über eine `list()`-Methode, um jede Instanz der Ressource in Ihrem aktuellen Abonnement zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="c886a-119">Each resource collection has a `list()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="c886a-120">`azure.sqlServers().list()` gibt beispielsweise alle SQL-Datenbanken im Abonnement zurück.</span><span class="sxs-lookup"><span data-stu-id="c886a-120">For example, `azure.sqlServers().list()` returns all SQL databases in the subscription.</span></span>

<span data-ttu-id="c886a-121">Verwenden Sie die Methode `listByResourceGroup(String groupname)`, um die zurückgegebene Liste auf eine bestimmte [Azure-Ressourcengruppe](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) einzugrenzen.</span><span class="sxs-lookup"><span data-stu-id="c886a-121">Use the `listByResourceGroup(String groupname)` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="c886a-122">Die zurückgegebene `PagedList<T>`-Sammlung kann genau wie ein normales `List<T>`-Element durchsucht und durchlaufen werden:</span><span class="sxs-lookup"><span data-stu-id="c886a-122">Search and iterate over the returned `PagedList<T>` collection just as you would a normal `List<T>`:</span></span>

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a><span data-ttu-id="c886a-123">Von Abfragen zurückgegebene Sammlungen</span><span class="sxs-lookup"><span data-stu-id="c886a-123">Collections returned from queries</span></span>

<span data-ttu-id="c886a-124">Die Verwaltungsbibliotheken geben aus Abfragen bestimmte Sammlungstypen zurück (abhängig von der Struktur der Ergebnisse).</span><span class="sxs-lookup"><span data-stu-id="c886a-124">The management libraries return specific collection types from queries based on the structure of the results.</span></span>

- <span data-ttu-id="c886a-125">`List<T>`: Unsortierte Daten, die sich einfach durchsuchen und durchlaufen lassen.</span><span class="sxs-lookup"><span data-stu-id="c886a-125">`List<T>`: Unordered data that is easy to search and iterate over.</span></span>
- <span data-ttu-id="c886a-126">`Map<T>`: Zuordnungen sind Schlüssel-Wert-Paare mit eindeutigen Schlüsseln und nicht unbedingt eindeutigen Werten.</span><span class="sxs-lookup"><span data-stu-id="c886a-126">`Map<T>`: Maps are key/value pairs with unique keys, but not necessarily unique values.</span></span> <span data-ttu-id="c886a-127">Ein Beispiel für eine Zuordnung sind App-Einstellungen für eine App Service-Web-App.</span><span class="sxs-lookup"><span data-stu-id="c886a-127">An example of a Map would be app settings for an App Service Web App.</span></span>
- <span data-ttu-id="c886a-128">`Set<T>`: Sätze verfügen über eindeutige Schlüssel und Werte.</span><span class="sxs-lookup"><span data-stu-id="c886a-128">`Set<T>`: Sets have unique keys and values.</span></span> <span data-ttu-id="c886a-129">Ein Beispiel für einen Satz sind an einen virtuellen Computer angefügte Netzwerke, die sowohl einen eindeutigen Bezeichner (Schlüssel) als auch eine eindeutige Netzwerkkonfiguration (Wert) besitzen.</span><span class="sxs-lookup"><span data-stu-id="c886a-129">An example of a Set would be networks attached to a virtual machine, which would have both an unique identifier (the key) and a unique network configuration (the value).</span></span>

## <a name="actionable-verbs"></a><span data-ttu-id="c886a-130">Handlungsrelevante Verben</span><span class="sxs-lookup"><span data-stu-id="c886a-130">Actionable verbs</span></span>

<span data-ttu-id="c886a-131">Methoden, deren Name ein Verb enthält, haben das sofortige Ausführen einer Aktion in Azure zur Folge.</span><span class="sxs-lookup"><span data-stu-id="c886a-131">Methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="c886a-132">Diese Methoden werden synchron ausgeführt und blockieren bis zu ihrem Abschluss die Ausführung im aktuellen Thread.</span><span class="sxs-lookup"><span data-stu-id="c886a-132">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="c886a-133">Verb</span><span class="sxs-lookup"><span data-stu-id="c886a-133">Verb</span></span>   |  <span data-ttu-id="c886a-134">Beispielverwendung</span><span class="sxs-lookup"><span data-stu-id="c886a-134">Sample Usage</span></span> |
|--------|---------------|
| <span data-ttu-id="c886a-135">create</span><span class="sxs-lookup"><span data-stu-id="c886a-135">create</span></span> | `azure.virtualMachines().create(listOfVMCreatables)` |
| <span data-ttu-id="c886a-136">apply</span><span class="sxs-lookup"><span data-stu-id="c886a-136">apply</span></span>  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| <span data-ttu-id="c886a-137">delete</span><span class="sxs-lookup"><span data-stu-id="c886a-137">delete</span></span> | `azure.disks().deleteById(id)` | 
| <span data-ttu-id="c886a-138">list</span><span class="sxs-lookup"><span data-stu-id="c886a-138">list</span></span>   | `azure.sqlServers().list()` | 
| <span data-ttu-id="c886a-139">get</span><span class="sxs-lookup"><span data-stu-id="c886a-139">get</span></span>    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="c886a-140">`define()` und `update()` sind zwar Verben, blockieren den Ablauf aber nur, wenn im Anschluss `create()` oder `apply()` folgt.</span><span class="sxs-lookup"><span data-stu-id="c886a-140">`define()` and `update()` are verbs but do not block unless followed by a `create()` or `apply()`.</span></span>
 
<span data-ttu-id="c886a-141">Für einige dieser Methoden sind asynchrone Versionen mit dem Suffix `Async` vorhanden, die [reaktive Erweiterungen](https://github.com/ReactiveX/RxJava) verwenden.</span><span class="sxs-lookup"><span data-stu-id="c886a-141">Asynchronous versions of some of these  methods exist with the `Async` suffix using [Reactive extensions](https://github.com/ReactiveX/RxJava).</span></span> 

<span data-ttu-id="c886a-142">Einige Objekte verfügen über andere Methoden, die den Zustand der Ressource in Azure ändern.</span><span class="sxs-lookup"><span data-stu-id="c886a-142">Some objects have other methods with that change the state of the resource in Azure.</span></span> <span data-ttu-id="c886a-143">Beispielsweise `restart()` für ein `VirtualMachine`-Element.</span><span class="sxs-lookup"><span data-stu-id="c886a-143">For example, `restart()` on a `VirtualMachine`.</span></span>

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
<span data-ttu-id="c886a-144">Diese Methoden verfügen nicht immer über asynchrone Versionen und blockieren bis zu ihrem Abschluss die Ausführung in ihrem Thread.</span><span class="sxs-lookup"><span data-stu-id="c886a-144">These methods do not always have asynchronous versions and will block execution on their thread until they complete.</span></span>

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a><span data-ttu-id="c886a-145">Verzögerte Ressourcenerstellung</span><span class="sxs-lookup"><span data-stu-id="c886a-145">Lazy resource creation</span></span>

<span data-ttu-id="c886a-146">Eine Herausforderung beim Erstellen von Azure-Ressourcen ergibt sich, wenn eine neue Ressource von einer anderen Ressource abhängt, die noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="c886a-146">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="c886a-147">Ein Beispiel für dieses Szenario ist das Reservieren einer öffentlichen IP-Adresse und das Einrichten eines Datenträgers beim Erstellen eines neuen virtuellen Computers.</span><span class="sxs-lookup"><span data-stu-id="c886a-147">An example of this scenario is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="c886a-148">Sie möchten die Reservierung der Adresse oder die Erstellung des Datenträgers nicht überprüfen, sondern lediglich sicherstellen, dass der virtuelle Computer bei der Erstellung über diese Ressourcen verfügt.</span><span class="sxs-lookup"><span data-stu-id="c886a-148">You don't want to verify reserving the address or the creating the disk, you just want to ensure the virtual machine has those resources when it is created.</span></span>

<span data-ttu-id="c886a-149">Mit `Creatable<T>`-Objekten können Sie Azure-Ressourcen für die Verwendung in Ihrem Code definieren, ohne zu warten, bis sie in Ihrem Abonnement erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="c886a-149">`Creatable<T>` objects let you define Azure resources for use in your code without waiting around for them to be created in your subscription.</span></span> <span data-ttu-id="c886a-150">Die Verwaltungsbibliotheken stellen die Erstellung von `Creatable<T>`-Objekten zurück, bis sie benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="c886a-150">The management libraries defer creating  `Creatable<T>` objects until they are needed.</span></span>

<span data-ttu-id="c886a-151">Verwenden Sie das Verb `define()`, um `Creatable<T>`-Objekte für Azure-Ressourcen zu generieren:</span><span class="sxs-lookup"><span data-stu-id="c886a-151">Generate `Creatable<T>` objects for Azure resources through the `define()` verb:</span></span>

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

<span data-ttu-id="c886a-152">Die in diesem Beispiel durch `Creatable<PublicIPAddress>` definierte Azure-Ressource ist bei der Codeausführung noch nicht in Ihrem Abonnement vorhanden.</span><span class="sxs-lookup"><span data-stu-id="c886a-152">The Azure resource defined by the `Creatable<PublicIPAddress>` in this example does not yet exist in your subscription when this code executes.</span></span>  <span data-ttu-id="c886a-153">Verwenden Sie das Objekt `publicIPAddressCreatable`, um weitere Azure-Ressourcen mit dieser IP-Adresse zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c886a-153">Use the `publicIPAddressCreatable` object to create other Azure resources with this IP address.</span></span> 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

<span data-ttu-id="c886a-154">Die `Creatable<T>`-Ressourcen werden in Ihrem Abonnement generiert, wenn in Azure eine mithilfe des Objekts definierte Ressource unter Verwendung von `create()` erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="c886a-154">The `Creatable<T>` resources are generated in your subscription when any resource that is defined using the object is built in Azure using `create()`.</span></span> <span data-ttu-id="c886a-155">Fortsetzung des Beispiels mit der IP-Adresse und dem virtuellen Computer:</span><span class="sxs-lookup"><span data-stu-id="c886a-155">Continuing the IP address and virtual machine example:</span></span>

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

<span data-ttu-id="c886a-156">Durch die Übergabe von `Creatable<T>` an Aufrufe von `create()` wird anstelle eines einzelnen Ressourcenobjekts ein `CreatedResources`-Objekt zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="c886a-156">Passing the `Creatable<T>` to `create()` calls returns a `CreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="c886a-157">Das `CreatedResources<T>`-Objekt ermöglicht den Zugriff auf alle Ressourcen, die durch den Aufruf `create()` erstellt wurden (nicht nur auf die typisierte Ressource aus dem Aufruf).</span><span class="sxs-lookup"><span data-stu-id="c886a-157">The `CreatedResources<T>` object lets you access all resources created by the `create()` call, not just the typed resource in the call.</span></span> <span data-ttu-id="c886a-158">So greifen Sie auf die in Azure erstellte öffentliche IP-Adresse für den virtuellen Computer zu, der im obigen Beispiel erstellt wurde:</span><span class="sxs-lookup"><span data-stu-id="c886a-158">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a><span data-ttu-id="c886a-159">Ausnahmebehandlung</span><span class="sxs-lookup"><span data-stu-id="c886a-159">Exception handling</span></span>

<span data-ttu-id="c886a-160">Die Ausnahmeklassen der Verwaltungsbibliotheken erweitern `com.microsoft.rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="c886a-160">The management libraries' Exception classes extend `com.microsoft.rest.RestException`.</span></span> <span data-ttu-id="c886a-161">Fangen Sie von den Verwaltungsbibliotheken generierte Ausnahmen mit einem `catch (RestException exception)`-Block nach der entsprechenden `try`-Anweisung ab.</span><span class="sxs-lookup"><span data-stu-id="c886a-161">Catch exceptions generated by the management libraries with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-trace"></a><span data-ttu-id="c886a-162">Protokolle und Ablaufverfolgung</span><span class="sxs-lookup"><span data-stu-id="c886a-162">Logs and trace</span></span>

<span data-ttu-id="c886a-163">Konfigurieren Sie den Protokollierungsgrad der Verwaltungsbibliothek mithilfe von `withLogLevel()`, wenn Sie das Einstiegspunktobjekt `Azure` erstellen.</span><span class="sxs-lookup"><span data-stu-id="c886a-163">Configure the amount of logging from the management library when you build the entry point `Azure` object using `withLogLevel()`.</span></span> <span data-ttu-id="c886a-164">Folgende Ablaufverfolgungsebenen stehen zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="c886a-164">The following trace levels exist:</span></span>

| <span data-ttu-id="c886a-165">Ablaufverfolgungsebene</span><span class="sxs-lookup"><span data-stu-id="c886a-165">Trace level</span></span> | <span data-ttu-id="c886a-166">Protokollierung aktiviert</span><span class="sxs-lookup"><span data-stu-id="c886a-166">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="c886a-167">com.microsoft.rest.LogLevel.NONE</span><span class="sxs-lookup"><span data-stu-id="c886a-167">com.microsoft.rest.LogLevel.NONE</span></span> | <span data-ttu-id="c886a-168">Keine Ausgabe</span><span class="sxs-lookup"><span data-stu-id="c886a-168">No output</span></span>
| <span data-ttu-id="c886a-169">com.microsoft.rest.LogLevel.BASIC</span><span class="sxs-lookup"><span data-stu-id="c886a-169">com.microsoft.rest.LogLevel.BASIC</span></span> | <span data-ttu-id="c886a-170">Protokolliert die URLs für zugrunde liegende REST-Aufrufe, Antwortcodes und Zeiten</span><span class="sxs-lookup"><span data-stu-id="c886a-170">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="c886a-171">com.microsoft.rest.LogLevel.BODY</span><span class="sxs-lookup"><span data-stu-id="c886a-171">com.microsoft.rest.LogLevel.BODY</span></span> | <span data-ttu-id="c886a-172">Alles aus BASIC plus Abfrage- und Antworttext für die REST-Aufrufe</span><span class="sxs-lookup"><span data-stu-id="c886a-172">Everything in BASIC plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="c886a-173">com.microsoft.rest.LogLevel.HEADERS</span><span class="sxs-lookup"><span data-stu-id="c886a-173">com.microsoft.rest.LogLevel.HEADERS</span></span> | <span data-ttu-id="c886a-174">Alles aus BASIC plus Abfrage- und Antwortheader der REST-Aufrufe</span><span class="sxs-lookup"><span data-stu-id="c886a-174">Everything in BASIC plus the request and response headers REST calls</span></span>
| <span data-ttu-id="c886a-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span><span class="sxs-lookup"><span data-stu-id="c886a-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span></span> | <span data-ttu-id="c886a-176">Alles aus den Protokollierungsebenen „BODY“ und „HEADERS“</span><span class="sxs-lookup"><span data-stu-id="c886a-176">Everything in both BODY and HEADERS log level</span></span>

<span data-ttu-id="c886a-177">Falls Sie Ausgaben in einem Protokollierungsframework wie [Log4J 2](https://logging.apache.org/log4j/2.x/) protokollieren müssen, können Sie eine [SLF4J-Protokollierungsimplementierung](https://www.slf4j.org/manual.html) einbinden.</span><span class="sxs-lookup"><span data-stu-id="c886a-177">Bind a [SLF4J logging implementation](https://www.slf4j.org/manual.html) if you need to log output to a logging framework like [Log4J 2](https://logging.apache.org/log4j/2.x/).</span></span>