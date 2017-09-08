---
title: "Azure-Verwaltungsbibliotheken für Java – Konzepte und Muster für die Verwendung"
description: 
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
ms.openlocfilehash: 052c4de1e8f9ff0ece5f36d1c3514bad8c04cfec
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-library-concepts"></a><span data-ttu-id="6cba9-103">Azure-Verwaltungsbibliotheken für Java – Konzepte</span><span class="sxs-lookup"><span data-stu-id="6cba9-103">Azure management library concepts</span></span>

## <a name="build-resources-through-a-fluent-interface"></a><span data-ttu-id="6cba9-104">Erstellen von Ressourcen über eine Fluent-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="6cba9-104">Build resources through a fluent interface</span></span>

<span data-ttu-id="6cba9-105">Eine Fluent-Schnittstelle ist ein Muster, das Objekte mithilfe einer Methodenkette erstellt, die die Attribute des Objekts korrekt konfiguriert –</span><span class="sxs-lookup"><span data-stu-id="6cba9-105">A fluent interface is a pattern that creates objects using a method chain that correctly configures the object's attributes.</span></span> <span data-ttu-id="6cba9-106">beispielsweise, um ein neues Azure Storage-Konto zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6cba9-106">For example, to create a new Azure Storage account</span></span>

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

<span data-ttu-id="6cba9-107">Beim Durchlaufen der Methodenkette schlägt die IDE den nächsten Methodenaufruf in der Fluent-Konversation vor.</span><span class="sxs-lookup"><span data-stu-id="6cba9-107">As you go through the method chain, your IDE suggests the next method to call in the fluent conversation.</span></span>   

![GIF der IntelliJ-Befehlsvervollständigung im Rahmen einer Fluent-Kette](media/intelliJFluent.gif)

<span data-ttu-id="6cba9-109">Verketten Sie die von der IDE vorgeschlagenen Methoden, solange diese für die zu definierende Azure-Ressource sinnvoll sind.</span><span class="sxs-lookup"><span data-stu-id="6cba9-109">Chain the methods suggested by the IDE as long as they make sense for the Azure resource being defined.</span></span> <span data-ttu-id="6cba9-110">Sollte in der Kette eine erforderliche Methode fehlen, wird dies durch die IDE mit einem Fehler gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="6cba9-110">If you are missing a required method in the chain your IDE will highlight it with an error.</span></span>

## <a name="resource-collections"></a><span data-ttu-id="6cba9-111">Ressourcensammlungen</span><span class="sxs-lookup"><span data-stu-id="6cba9-111">Resource collections</span></span>

<span data-ttu-id="6cba9-112">Die Verwaltungsbibliothek besitzt für die Erstellung und Aktualisierung von Ressourcen einen einzelnen Zugangspunkt über das Objekt `com.microsoft.azure.management.Azure` der obersten Ebene.</span><span class="sxs-lookup"><span data-stu-id="6cba9-112">The management library has a single point of entry through the top-level `com.microsoft.azure.management.Azure` object to create and update resources.</span></span> <span data-ttu-id="6cba9-113">Wählen Sie mithilfe der im Objekt `Azure` definierten Ressourcensammlungsmethoden aus, mit welcher Art von Ressourcen Sie arbeiten möchten.</span><span class="sxs-lookup"><span data-stu-id="6cba9-113">Select which type of resources to work with using the resource collection methods defined in the `Azure` object.</span></span> <span data-ttu-id="6cba9-114">Beispiel für SQL-Datenbank:</span><span class="sxs-lookup"><span data-stu-id="6cba9-114">For example, SQL Database:</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a><span data-ttu-id="6cba9-115">Listen und Iterationen</span><span class="sxs-lookup"><span data-stu-id="6cba9-115">Lists and iterations</span></span>

<span data-ttu-id="6cba9-116">Jede Ressourcensammlung verfügt über eine Methode vom Typ `list()`, um jede Instanz der Ressource in Ihrem aktuellen Abonnement zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="6cba9-116">Each resource collection has a `list()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="6cba9-117">`azure.sqlServers().list()` gibt beispielsweise alle SQL-Datenbanken im Abonnement zurück.</span><span class="sxs-lookup"><span data-stu-id="6cba9-117">For example, `azure.sqlServers().list()` returns all SQL databases in the subscription.</span></span>

<span data-ttu-id="6cba9-118">Verwenden Sie die Methode `listByResourceGroup(String groupname)`, um die zurückgegebene Liste auf eine bestimmte [Azure-Ressourcengruppe](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) einzugrenzen.</span><span class="sxs-lookup"><span data-stu-id="6cba9-118">Use the `listByResourceGroup(String groupname)` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="6cba9-119">Die zurückgegebene Sammlung vom Typ `PagedList<T>` kann genau wie ein normales Element vom Typ `List<T>` durchsucht und durchlaufen werden:</span><span class="sxs-lookup"><span data-stu-id="6cba9-119">Search and iterate over the returned `PagedList<T>` collection just as you would a normal `List<T>`:</span></span>

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a><span data-ttu-id="6cba9-120">Von Abfragen zurückgegebene Sammlungen</span><span class="sxs-lookup"><span data-stu-id="6cba9-120">Collections returned from queries</span></span>

<span data-ttu-id="6cba9-121">Die Verwaltungsbibliotheken geben aus Abfragen bestimmte Sammlungstypen zurück (abhängig von der Struktur der Ergebnisse).</span><span class="sxs-lookup"><span data-stu-id="6cba9-121">The management libraries return specific collection types from queries based on the structure of the results.</span></span>

- <span data-ttu-id="6cba9-122">`List<T>`: Unsortierte Daten, die sich einfach durchsuchen und durchlaufen lassen.</span><span class="sxs-lookup"><span data-stu-id="6cba9-122">`List<T>`: Unordered data that is easy to search and iterate over.</span></span>
- <span data-ttu-id="6cba9-123">`Map<T>`: Zuordnungen sind Schlüssel-Wert-Paare mit eindeutigen Schlüsseln und nicht unbedingt eindeutigen Werten.</span><span class="sxs-lookup"><span data-stu-id="6cba9-123">`Map<T>`: Maps are key/value pairs with unique keys, but not necessarily unique values.</span></span> <span data-ttu-id="6cba9-124">Ein Beispiel für eine Zuordnung sind App-Einstellungen für eine App Service-Web-App.</span><span class="sxs-lookup"><span data-stu-id="6cba9-124">An example of a Map would be app settings for an App Service Web App.</span></span>
- <span data-ttu-id="6cba9-125">`Set<T>`: Sätze verfügen über eindeutige Schlüssel und Werte.</span><span class="sxs-lookup"><span data-stu-id="6cba9-125">`Set<T>`: Sets have unique keys and values.</span></span> <span data-ttu-id="6cba9-126">Ein Beispiel für einen Satz sind an einen virtuellen Computer angefügte Netzwerke, die sowohl einen eindeutigen Bezeichner (Schlüssel) als auch eine eindeutige Netzwerkkonfiguration (Wert) besitzen.</span><span class="sxs-lookup"><span data-stu-id="6cba9-126">An example of a Set would be networks attached to a virtual machine, which would have both an unique identifier (the key) and a unique network configuration (the value).</span></span>

## <a name="actionable-verbs"></a><span data-ttu-id="6cba9-127">Handlungsrelevante Verben</span><span class="sxs-lookup"><span data-stu-id="6cba9-127">Actionable verbs</span></span>

<span data-ttu-id="6cba9-128">Methoden, deren Name ein Verb enthält, haben eine umgehende Aktion in Azure zur Folge.</span><span class="sxs-lookup"><span data-stu-id="6cba9-128">Methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="6cba9-129">Diese Methoden werden synchron ausgeführt und blockieren bis zu ihrem Abschluss die Ausführung im aktuellen Thread.</span><span class="sxs-lookup"><span data-stu-id="6cba9-129">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="6cba9-130">Verb</span><span class="sxs-lookup"><span data-stu-id="6cba9-130">Verb</span></span>   |  <span data-ttu-id="6cba9-131">Beispielverwendung</span><span class="sxs-lookup"><span data-stu-id="6cba9-131">Sample Usage</span></span> |
|--------|---------------|
| <span data-ttu-id="6cba9-132">create</span><span class="sxs-lookup"><span data-stu-id="6cba9-132">create</span></span> | `azure.virtualMachines().create(listOfVMCreatables)` |
| <span data-ttu-id="6cba9-133">apply</span><span class="sxs-lookup"><span data-stu-id="6cba9-133">apply</span></span>  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| <span data-ttu-id="6cba9-134">delete</span><span class="sxs-lookup"><span data-stu-id="6cba9-134">delete</span></span> | `azure.disks().deleteById(id)` | 
| <span data-ttu-id="6cba9-135">list</span><span class="sxs-lookup"><span data-stu-id="6cba9-135">list</span></span>   | `azure.sqlServers().list()` | 
| <span data-ttu-id="6cba9-136">get</span><span class="sxs-lookup"><span data-stu-id="6cba9-136">get</span></span>    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="6cba9-137">`define()` und `update()` sind zwar Verben, blockieren den Ablauf aber nur, wenn im Anschluss `create()` oder `apply()` folgt.</span><span class="sxs-lookup"><span data-stu-id="6cba9-137">`define()` and `update()` are verbs but do not block unless followed by a `create()` or `apply()`.</span></span>
 
<span data-ttu-id="6cba9-138">Für einige dieser Methoden sind asynchrone Versionen mit dem Suffix `Async` vorhanden, die [reaktive Erweiterungen](https://github.com/ReactiveX/RxJava) verwenden.</span><span class="sxs-lookup"><span data-stu-id="6cba9-138">Asynchronous versions of some of these  methods exist with the `Async` suffix using [Reactive extensions](https://github.com/ReactiveX/RxJava).</span></span> 

<span data-ttu-id="6cba9-139">Einige Objekte verfügen über andere Methoden, die den Zustand der Ressource in Azure ändern.</span><span class="sxs-lookup"><span data-stu-id="6cba9-139">Some objects have other methods with that change the state of the resource in Azure.</span></span> <span data-ttu-id="6cba9-140">Beispielsweise `restart()` für ein Element vom Typ `VirtualMachine`.</span><span class="sxs-lookup"><span data-stu-id="6cba9-140">For example, `restart()` on a `VirtualMachine`.</span></span>

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
<span data-ttu-id="6cba9-141">Diese Methoden verfügen nicht immer über asynchrone Versionen und blockieren bis zu ihrem Abschluss die Ausführung in ihrem Thread.</span><span class="sxs-lookup"><span data-stu-id="6cba9-141">These methods do not always have asynchronous versions and will block execution on their thread until they complete.</span></span>

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a><span data-ttu-id="6cba9-142">Verzögerte Ressourcenerstellung</span><span class="sxs-lookup"><span data-stu-id="6cba9-142">Lazy resource creation</span></span>

<span data-ttu-id="6cba9-143">Eine Herausforderung beim Erstellen von Azure-Ressourcen ergibt sich, wenn eine neue Ressource von einer anderen Ressource abhängt, die noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6cba9-143">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="6cba9-144">Ein Beispiel für dieses Szenario ist das Reservieren einer öffentlichen IP-Adresse und das Einrichten eines Datenträgers beim Erstellen eines neuen virtuellen Computers.</span><span class="sxs-lookup"><span data-stu-id="6cba9-144">An example of this scenario is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="6cba9-145">Sie möchten die Reservierung der Adresse oder die Erstellung des Datenträgers nicht überprüfen, sondern lediglich sicherstellen, dass der virtuelle Computer bei der Erstellung über diese Ressourcen verfügt.</span><span class="sxs-lookup"><span data-stu-id="6cba9-145">You don't want to verify reserving the address or the creating the disk, you just want to ensure the virtual machine has those resources when it is created.</span></span>

<span data-ttu-id="6cba9-146">Mit Objekten vom Typ `Creatable<T>` können Sie Azure-Ressourcen für die Verwendung in Ihrem Code definieren, ohne zu warten, bis sie in Ihrem Abonnement erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="6cba9-146">`Creatable<T>` objects let you define Azure resources for use in your code without waiting around for them to be created in your subscription.</span></span> <span data-ttu-id="6cba9-147">Die Verwaltungsbibliotheken stellen die Erstellung von Objekten vom Typ `Creatable<T>` zurück, bis sie benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="6cba9-147">The management libraries defer creating  `Creatable<T>` objects until they are needed.</span></span>

<span data-ttu-id="6cba9-148">Verwenden Sie das Verb `define()`, um Objekte vom Typ `Creatable<T>` für Azure-Ressourcen zu generieren:</span><span class="sxs-lookup"><span data-stu-id="6cba9-148">Generate `Creatable<T>` objects for Azure resources through the `define()` verb:</span></span>

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

<span data-ttu-id="6cba9-149">Die in diesem Beispiel durch `Creatable<PublicIPAddress>` definierte Azure-Ressource ist bei der Codeausführung noch nicht in Ihrem Abonnement vorhanden.</span><span class="sxs-lookup"><span data-stu-id="6cba9-149">The Azure resource defined by the `Creatable<PublicIPAddress>` in this example does not yet exist in your subscription when this code executes.</span></span>  <span data-ttu-id="6cba9-150">Verwenden Sie das Objekt `publicIPAddressCreatable`, um weitere Azure-Ressourcen mit dieser IP-Adresse zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6cba9-150">Use the `publicIPAddressCreatable` object to create other Azure resources with this IP address.</span></span> 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

<span data-ttu-id="6cba9-151">Die Ressourcen vom Typ `Creatable<T>` werden in Ihrem Abonnement generiert, wenn in Azure eine mithilfe des Objekts definierte Ressource unter Verwendung von `create()` erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="6cba9-151">The `Creatable<T>` resources are generated in your subscription when any resource that is defined using the object is built in Azure using `create()`.</span></span> <span data-ttu-id="6cba9-152">Fortsetzung des Beispiels mit der IP-Adresse und dem virtuellen Computer:</span><span class="sxs-lookup"><span data-stu-id="6cba9-152">Continuing the IP address and virtual machine example:</span></span>

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

<span data-ttu-id="6cba9-153">Durch die Übergabe von `Creatable<T>` an Aufrufe von `create()` wird anstelle eines einzelnen Ressourcenobjekts ein Objekt vom Typ `CreatedResources` zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="6cba9-153">Passing the `Creatable<T>` to `create()` calls returns a `CreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="6cba9-154">Das Objekt vom Typ `CreatedResources<T>` ermöglicht den Zugriff auf alle Ressourcen, die durch den Aufruf `create()` erstellt wurden (nicht nur auf die typisierte Ressource aus dem Aufruf).</span><span class="sxs-lookup"><span data-stu-id="6cba9-154">The `CreatedResources<T>` object lets you access all resources created by the `create()` call, not just the typed resource in the call.</span></span> <span data-ttu-id="6cba9-155">So greifen Sie auf die in Azure erstellte öffentliche IP-Adresse für den virtuellen Computer zu, der im obigen Beispiel erstellt wurde:</span><span class="sxs-lookup"><span data-stu-id="6cba9-155">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a><span data-ttu-id="6cba9-156">Ausnahmebehandlung</span><span class="sxs-lookup"><span data-stu-id="6cba9-156">Exception handling</span></span>

<span data-ttu-id="6cba9-157">Die Ausnahmeklassen der Verwaltungsbibliotheken erweitern `com.microsoft.rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="6cba9-157">The management libraries' Exception classes extend `com.microsoft.rest.RestException`.</span></span> <span data-ttu-id="6cba9-158">Fangen Sie von den Verwaltungsbibliotheken generierte Ausnahmen mit einem Block vom Typ `catch (RestException exception)` nach der entsprechenden Anweisung vom Typ `try` ab.</span><span class="sxs-lookup"><span data-stu-id="6cba9-158">Catch exceptions generated by the management libraries with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-trace"></a><span data-ttu-id="6cba9-159">Protokolle und Ablaufverfolgung</span><span class="sxs-lookup"><span data-stu-id="6cba9-159">Logs and trace</span></span>

<span data-ttu-id="6cba9-160">Konfigurieren Sie den Protokollierungsgrad der Verwaltungsbibliothek mithilfe von `withLogLevel()`, wenn Sie das Einstiegspunktobjekt `Azure` erstellen.</span><span class="sxs-lookup"><span data-stu-id="6cba9-160">Configure the amount of logging from the management library when you build the entry point `Azure` object using `withLogLevel()`.</span></span> <span data-ttu-id="6cba9-161">Folgende Ablaufverfolgungsebenen stehen zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="6cba9-161">The following trace levels exist:</span></span>

| <span data-ttu-id="6cba9-162">Ablaufverfolgungsebene</span><span class="sxs-lookup"><span data-stu-id="6cba9-162">Trace level</span></span> | <span data-ttu-id="6cba9-163">Protokollierung aktiviert</span><span class="sxs-lookup"><span data-stu-id="6cba9-163">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="6cba9-164">com.microsoft.rest.LogLevel.NONE</span><span class="sxs-lookup"><span data-stu-id="6cba9-164">com.microsoft.rest.LogLevel.NONE</span></span> | <span data-ttu-id="6cba9-165">Keine Ausgabe</span><span class="sxs-lookup"><span data-stu-id="6cba9-165">No output</span></span>
| <span data-ttu-id="6cba9-166">com.microsoft.rest.LogLevel.BASIC</span><span class="sxs-lookup"><span data-stu-id="6cba9-166">com.microsoft.rest.LogLevel.BASIC</span></span> | <span data-ttu-id="6cba9-167">Protokolliert die URLs für zugrunde liegende REST-Aufrufe, Antwortcodes und Zeiten</span><span class="sxs-lookup"><span data-stu-id="6cba9-167">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="6cba9-168">com.microsoft.rest.LogLevel.BODY</span><span class="sxs-lookup"><span data-stu-id="6cba9-168">com.microsoft.rest.LogLevel.BODY</span></span> | <span data-ttu-id="6cba9-169">Alles aus BASIC plus Abfrage- und Antworttext für die REST-Aufrufe</span><span class="sxs-lookup"><span data-stu-id="6cba9-169">Everything in BASIC plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="6cba9-170">com.microsoft.rest.LogLevel.HEADERS</span><span class="sxs-lookup"><span data-stu-id="6cba9-170">com.microsoft.rest.LogLevel.HEADERS</span></span> | <span data-ttu-id="6cba9-171">Alles aus BASIC plus Abfrage- und Antwortheader der REST-Aufrufe</span><span class="sxs-lookup"><span data-stu-id="6cba9-171">Everything in BASIC plus the request and response headers REST calls</span></span>
| <span data-ttu-id="6cba9-172">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span><span class="sxs-lookup"><span data-stu-id="6cba9-172">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span></span> | <span data-ttu-id="6cba9-173">Alles aus den Protokollierungsebenen „BODY“ und „HEADERS“</span><span class="sxs-lookup"><span data-stu-id="6cba9-173">Everything in both BODY and HEADERS log level</span></span>

<span data-ttu-id="6cba9-174">Falls Sie Ausgaben in einem Protokollierungsframework wie [Log4J 2](https://logging.apache.org/log4j/2.x/) protokollieren müssen, können Sie eine [SLF4J-Protokollierungsimplementierung](https://www.slf4j.org/manual.html) einbinden.</span><span class="sxs-lookup"><span data-stu-id="6cba9-174">Bind a [SLF4J logging implementation](https://www.slf4j.org/manual.html) if you need to log output to a logging framework like [Log4J 2](https://logging.apache.org/log4j/2.x/).</span></span>