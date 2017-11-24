---
title: "Azure Event Hub-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Event Hub-Bibliotheken"
keywords: Azure, Java, SDK, API, Event Hub, IoT, Streamverarbeitung
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: event-hub
ms.openlocfilehash: 8e5b032624862ffbef18c718abf4fa29359b3e67
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-event-hub-libraries-for-java"></a>Azure Event Hub-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Sammeln und verwalten Sie mithilfe von [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs) pro Sekunde Millionen von Ereignissen von verbundenen IoT-Geräten und -Anwendungen.

Informationen zu den ersten Schritten mit Azure Event Hubs finden Sie unter [Empfangen von Ereignissen von Azure Event Hubs mithilfe von Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Clientbibliothek

Mit der Event Hubs-Bibliothek können Sie Ereignisse an Azure Event Hub senden und Ereignisse von einem Event Hub nutzen und verarbeiten.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a>Beispiel

Senden Sie Ereignissen an einen Event Hub:

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/java/api/overview/azure/eventhub/clientlibrary)


## <a name="samples"></a>Beispiele

[Schreiben in Event Hub über JMS und Lesen aus Apache Storm][1]
[Lesen und Schreiben in EventHubs mit einer .NET-/Java-Hybridtopologie][2] 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Sehen Sie sich weitere [Java-Codebeispiele für Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) an, die Sie in Ihren Apps verwenden können.

