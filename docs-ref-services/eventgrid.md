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
# <a name="azure-event-grid-libraries-for-java"></a>Azure Event Grid-Bibliotheken für Java

Buildereignisgesteuerte Anwendungen, die mit einfacher HTTP-basierter Ereignisbehandlung und Azure Event Grid auf Ereignisse von Azure-Diensten und benutzerdefinierten Quellen lauschen und reagieren

[Weitere Informationen](/azure/event-grid/overview) zu Azure Event Grid und erste Schritte mit dem [Tutorial zu Azure Blob Storage-Ereignissen](/azure/storage/blobs/storage-blob-event-quickstart) 

## <a name="client-sdk"></a>Client-SDK

Mit dem Client-SDK von Azure Event Grid können Sie Ereignisse erstellen, die Authentifizierung durchführen und Beiträge in Themen posten.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a>Veröffentlichen von Ereignissen

Der folgende Code authentifiziert sich mit Azure und veröffentlicht `List` von `EventGridEvent`-Ereignissen eines benutzerdefinierten Typs (in diesem Beispiel `Contoso.Items.ItemsReceived`) in einem Thema. Der Schlüssel und die Endpunktadresse für das Thema, die im Beispiel verwendet werden, können über die Azure-Befehlszeilenschnittstelle abgerufen werden:

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
> [Informationen zu den Event Grid-Client-APIs](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>Verwaltungs-SDK

Das Event Grid-Verwaltungs-SDK ermöglicht Ihnen das Erstellen, Aktualisieren und Löschen von Event Grid-Instanzen, -Themen und -Abonnements.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

Im folgenden Beispiel aus den [EventGrid-Java-Beispielen](https://github.com/Azure-Samples/event-grid-java-publish-consume-events) wird ein Event Grid-Abonnement erstellt.

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
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/eventgrid/management)