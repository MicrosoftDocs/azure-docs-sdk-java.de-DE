---
title: "Entwicklerhandbuch für die Azure-Verwaltungsbibliotheken für Java"
description: "Muster und Konzepte für die Verwendung der Java-Verwaltungsbibliotheken zum Verwalten von Cloudressourcen in Azure."
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
ms.openlocfilehash: 8b52981ddfaadb7227cea4c7df014011196339cb
ms.sourcegitcommit: 1f6a80e067a8bdbbb4b2da2e2145fda73d5fe65a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="patterns-and-best-practices-for-development-with-the-azure-libraries-for-java"></a>Muster und bewährte Methoden für die Entwicklung mit den Azure-Bibliotheken für Java 

In diesem Artikel sind verschiedene Muster und bewährte Methoden für die Verwendung der Azure-Bibliotheken für Java in Ihren Projekten aufgeführt. Verwenden Sie bei der Entwicklung diese Muster und Richtlinien, um die zu verwaltende Codemenge zu reduzieren und das Hinzufügen oder Konfigurieren zusätzlicher Ressourcen in künftigen Aktualisierungen der Verwaltungsbibliotheken zu vereinfachen.

## <a name="build-resources-through-a-fluent-interface"></a>Erstellen von Ressourcen über eine Fluent-Schnittstelle

Eine Fluent-Schnittstelle ist ein Muster, das Objekte mithilfe einer Methodenkette erstellt, die die Attribute des Objekts korrekt konfiguriert – beispielsweise, um ein neues Azure Storage-Konto zu erstellen.

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

Beim Durchlaufen der Methodenkette schlägt die IDE den nächsten Methodenaufruf in der Fluent-Konversation vor.   

![GIF der IntelliJ-Befehlsvervollständigung im Rahmen einer Fluent-Kette](media/intelliJFluent.gif)

Verketten Sie die von der IDE vorgeschlagenen Methoden, solange diese für die zu definierende Azure-Ressource sinnvoll sind. Sollte in der Kette eine erforderliche Methode fehlen, wird dies durch die IDE mit einem Fehler gekennzeichnet.

## <a name="resource-collections"></a>Ressourcensammlungen

Die Verwaltungsbibliothek besitzt für die Erstellung und Aktualisierung von Ressourcen einen einzelnen Zugangspunkt über das Objekt `com.microsoft.azure.management.Azure` der obersten Ebene. Wählen Sie mithilfe der im Objekt `Azure` definierten Ressourcensammlungsmethoden aus, mit welcher Art von Ressourcen Sie arbeiten möchten. Beispiel für SQL-Datenbank:

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a>Listen und Iterationen

Jede Ressourcensammlung verfügt über eine `list()`-Methode, um jede Instanz der Ressource in Ihrem aktuellen Abonnement zurückzugeben. `azure.sqlServers().list()` gibt beispielsweise alle SQL-Datenbanken im Abonnement zurück.

Verwenden Sie die Methode `listByResourceGroup(String groupname)`, um die zurückgegebene Liste auf eine bestimmte [Azure-Ressourcengruppe](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) einzugrenzen.  

Die zurückgegebene `PagedList<T>`-Sammlung kann genau wie ein normales `List<T>`-Element durchsucht und durchlaufen werden:

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a>Von Abfragen zurückgegebene Sammlungen

Die Verwaltungsbibliotheken geben aus Abfragen bestimmte Sammlungstypen zurück (abhängig von der Struktur der Ergebnisse).

- `List<T>`: Unsortierte Daten, die sich einfach durchsuchen und durchlaufen lassen.
- `Map<T>`: Zuordnungen sind Schlüssel-Wert-Paare mit eindeutigen Schlüsseln und nicht unbedingt eindeutigen Werten. Ein Beispiel für eine Zuordnung sind App-Einstellungen für eine App Service-Web-App.
- `Set<T>`: Sätze verfügen über eindeutige Schlüssel und Werte. Ein Beispiel für einen Satz sind an einen virtuellen Computer angefügte Netzwerke, die sowohl einen eindeutigen Bezeichner (Schlüssel) als auch eine eindeutige Netzwerkkonfiguration (Wert) besitzen.

## <a name="actionable-verbs"></a>Handlungsrelevante Verben

Methoden, deren Name ein Verb enthält, haben das sofortige Ausführen einer Aktion in Azure zur Folge. Diese Methoden werden synchron ausgeführt und blockieren bis zu ihrem Abschluss die Ausführung im aktuellen Thread. 

| Verb   |  Beispielverwendung |
|--------|---------------|
| create | `azure.virtualMachines().create(listOfVMCreatables)` |
| apply  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| delete | `azure.disks().deleteById(id)` | 
| list   | `azure.sqlServers().list()` | 
| get    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> `define()` und `update()` sind zwar Verben, blockieren den Ablauf aber nur, wenn im Anschluss `create()` oder `apply()` folgt.
 
Für einige dieser Methoden sind asynchrone Versionen mit dem Suffix `Async` vorhanden, die [reaktive Erweiterungen](https://github.com/ReactiveX/RxJava) verwenden. 

Einige Objekte verfügen über andere Methoden, die den Zustand der Ressource in Azure ändern. Beispielsweise `restart()` für ein `VirtualMachine`-Element.

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
Diese Methoden verfügen nicht immer über asynchrone Versionen und blockieren bis zu ihrem Abschluss die Ausführung in ihrem Thread.

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a>Verzögerte Ressourcenerstellung

Eine Herausforderung beim Erstellen von Azure-Ressourcen ergibt sich, wenn eine neue Ressource von einer anderen Ressource abhängt, die noch nicht vorhanden ist. Ein Beispiel für dieses Szenario ist das Reservieren einer öffentlichen IP-Adresse und das Einrichten eines Datenträgers beim Erstellen eines neuen virtuellen Computers. Sie möchten die Reservierung der Adresse oder die Erstellung des Datenträgers nicht überprüfen, sondern lediglich sicherstellen, dass der virtuelle Computer bei der Erstellung über diese Ressourcen verfügt.

Mit `Creatable<T>`-Objekten können Sie Azure-Ressourcen für die Verwendung in Ihrem Code definieren, ohne zu warten, bis sie in Ihrem Abonnement erstellt wurden. Die Verwaltungsbibliotheken stellen die Erstellung von `Creatable<T>`-Objekten zurück, bis sie benötigt werden.

Verwenden Sie das Verb `define()`, um `Creatable<T>`-Objekte für Azure-Ressourcen zu generieren:

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

Die in diesem Beispiel durch `Creatable<PublicIPAddress>` definierte Azure-Ressource ist bei der Codeausführung noch nicht in Ihrem Abonnement vorhanden.  Verwenden Sie das Objekt `publicIPAddressCreatable`, um weitere Azure-Ressourcen mit dieser IP-Adresse zu erstellen. 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

Die `Creatable<T>`-Ressourcen werden in Ihrem Abonnement generiert, wenn in Azure eine mithilfe des Objekts definierte Ressource unter Verwendung von `create()` erstellt wird. Fortsetzung des Beispiels mit der IP-Adresse und dem virtuellen Computer:

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

Durch die Übergabe von `Creatable<T>` an Aufrufe von `create()` wird anstelle eines einzelnen Ressourcenobjekts ein `CreatedResources`-Objekt zurückgegeben.  Das `CreatedResources<T>`-Objekt ermöglicht den Zugriff auf alle Ressourcen, die durch den Aufruf `create()` erstellt wurden (nicht nur auf die typisierte Ressource aus dem Aufruf). So greifen Sie auf die in Azure erstellte öffentliche IP-Adresse für den virtuellen Computer zu, der im obigen Beispiel erstellt wurde:

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a>Ausnahmebehandlung

Die Ausnahmeklassen der Verwaltungsbibliotheken erweitern `com.microsoft.rest.RestException`. Fangen Sie von den Verwaltungsbibliotheken generierte Ausnahmen mit einem `catch (RestException exception)`-Block nach der entsprechenden `try`-Anweisung ab.

## <a name="logs-and-trace"></a>Protokolle und Ablaufverfolgung

Konfigurieren Sie den Protokollierungsgrad der Verwaltungsbibliothek mithilfe von `withLogLevel()`, wenn Sie das Einstiegspunktobjekt `Azure` erstellen. Folgende Ablaufverfolgungsebenen stehen zur Verfügung:

| Ablaufverfolgungsebene | Protokollierung aktiviert 
| ------------ | ---------------
| com.microsoft.rest.LogLevel.NONE | Keine Ausgabe
| com.microsoft.rest.LogLevel.BASIC | Protokolliert die URLs für zugrunde liegende REST-Aufrufe, Antwortcodes und Zeiten
| com.microsoft.rest.LogLevel.BODY | Alles aus BASIC plus Abfrage- und Antworttext für die REST-Aufrufe
| com.microsoft.rest.LogLevel.HEADERS | Alles aus BASIC plus Abfrage- und Antwortheader der REST-Aufrufe
| com.microsoft.rest.LogLevel.BODY_AND_HEADERS | Alles aus den Protokollierungsebenen „BODY“ und „HEADERS“

Falls Sie Ausgaben in einem Protokollierungsframework wie [Log4J 2](https://logging.apache.org/log4j/2.x/) protokollieren müssen, können Sie eine [SLF4J-Protokollierungsimplementierung](https://www.slf4j.org/manual.html) einbinden.