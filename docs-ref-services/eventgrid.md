---
title: Azure Event Grid-Bibliotheken für Java
description: Referenzdokumentation für die Azure Event Grid-Java-Bibliotheken
keywords: Azure, Java, SDK, API, Event Grid, Messaging, ereignisgesteuert
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 07/11/2017
ms.topic: managed-reference
ms.devlang: java
ms.service: event-grid
ms.openlocfilehash: 35acbdeede2fbc541128029ad43f149209a057c4
ms.sourcegitcommit: db36eeb667a0bfe6d113953bb0583240db61b0f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/26/2018
ms.locfileid: "50134628"
---
# <a name="azure-event-grid-libraries-for-java"></a><span data-ttu-id="afd9b-104">Azure Event Grid-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="afd9b-104">Azure Event Grid libraries for Java</span></span>

<span data-ttu-id="afd9b-105">Buildereignisgesteuerte Anwendungen, die mit einfacher HTTP-basierter Ereignisbehandlung und Azure Event Grid auf Ereignisse von Azure-Diensten und benutzerdefinierten Quellen lauschen und reagieren</span><span class="sxs-lookup"><span data-stu-id="afd9b-105">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="afd9b-106">[Weitere Informationen](/azure/event-grid/overview) zu Azure Event Grid und erste Schritte mit dem [Tutorial zu Azure Blob Storage-Ereignissen](/azure/storage/blobs/storage-blob-event-quickstart)</span><span class="sxs-lookup"><span data-stu-id="afd9b-106">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="afd9b-107">Client-SDK</span><span class="sxs-lookup"><span data-stu-id="afd9b-107">Client SDK</span></span>

<span data-ttu-id="afd9b-108">Mit dem Client-SDK von Azure Event Grid können Sie Ereignisse erstellen, die Authentifizierung durchführen und Beiträge in Themen posten.</span><span class="sxs-lookup"><span data-stu-id="afd9b-108">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="afd9b-109">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="afd9b-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a><span data-ttu-id="afd9b-110">Veröffentlichen von Ereignissen</span><span class="sxs-lookup"><span data-stu-id="afd9b-110">Publish events</span></span>

<span data-ttu-id="afd9b-111">Der folgende Code authentifiziert sich mit Azure und veröffentlicht `List` von `EventGridEvent`-Ereignissen eines benutzerdefinierten Typs (in diesem Beispiel `Contoso.Items.ItemsReceived`) in einem Thema.</span><span class="sxs-lookup"><span data-stu-id="afd9b-111">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceived` ) to a topic.</span></span> <span data-ttu-id="afd9b-112">Der Schlüssel und die Endpunktadresse für das Thema, die im Beispiel verwendet werden, können über die Azure-Befehlszeilenschnittstelle abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="afd9b-112">The topic key and endpoint address used in the sample can be retrieved from the Azure CLI:</span></span>

```azurecli-interactive
az eventgrid topic show -g gridResourceGroup -n topicName
az eventgrid topic key list -g gridResourceGroup -n topicName
```

```java
// Create an event grid client.
TopicCredentials topicCredentials = new TopicCredentials(System.getenv("EVENTGRID_TOPIC_KEY"));
EventGridClient client = new EventGridClientImpl(topicCredentials);

// Publish custom events to the EventGrid.
System.out.println("Publish custom events to the EventGrid");
List<EventGridEvent> eventsList = new ArrayList<>();
for (int i = 0; i < 5; i++) {
    eventsList.add(new EventGridEvent(
        UUID.randomUUID().toString(),
        String.format("Door%d", i),
        new ContosoItemReceivedEventData("Contoso Item SKU #1"),
        "Contoso.Items.ItemReceived",
        DateTime.now(),
        "2.0"
    ));
}

String eventGridEndpoint = String.format("https://%s/", new URI(System.getenv("EVENTGRID_TOPIC_ENDPOINT")).getHost());

client.publishEvents(eventGridEndpoint, eventsList);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="afd9b-113">Informationen zu den Event Grid-Client-APIs</span><span class="sxs-lookup"><span data-stu-id="afd9b-113">Explore the Event Grid Client APIs</span></span>](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="afd9b-114">Verwaltungs-SDK</span><span class="sxs-lookup"><span data-stu-id="afd9b-114">Management SDK</span></span>

<span data-ttu-id="afd9b-115">Das Event Grid-Verwaltungs-SDK ermöglicht Ihnen das Erstellen, Aktualisieren und Löschen von Event Grid-Instanzen, -Themen und -Abonnements.</span><span class="sxs-lookup"><span data-stu-id="afd9b-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the Event Grid management SDK.</span></span>

<span data-ttu-id="afd9b-116">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="afd9b-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

<span data-ttu-id="afd9b-117">Im folgenden Beispiel aus den [EventGrid-Java-Beispielen](https://github.com/Azure-Samples/event-grid-java-publish-consume-events) wird ein Event Grid-Abonnement erstellt.</span><span class="sxs-lookup"><span data-stu-id="afd9b-117">The following example creates an Event Grid subscription, taken from the [EventGrid Java samples](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span></span>

```java
// Create an event grid subscription.
//
System.out.println("Creating an Azure EventGrid Subscription");

EventSubscription eventSubscription = eventGridManager.eventSubscriptions().define(eventSubscriptionName)
    .withScope(eventGridTopic.id())
    .withDestination(new EventHubEventSubscriptionDestination()
        .withResourceId(eventHub.id()))
    .withFilter(new EventSubscriptionFilter()
        .withIsSubjectCaseSensitive(false)
        .withSubjectBeginsWith("")
        .withSubjectEndsWith(""))
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="afd9b-118">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="afd9b-118">Explore the management APIs</span></span>](/java/api/overview/azure/eventgrid/management)