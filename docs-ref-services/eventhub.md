---
title: Azure Event Hub-Bibliotheken für Java
description: Referenzdokumentation für die Java-Event Hub-Bibliotheken
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
ms.openlocfilehash: b6646ef27edace4247090e749c9a52cd6a33a82c
ms.sourcegitcommit: 3d3460289ab6b9165c2cf6a3dd56eafd0692501e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/17/2018
ms.locfileid: "34283024"
---
# <a name="azure-event-hub-libraries-for-java"></a>Azure Event Hub-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Sammeln und verwalten Sie mithilfe von [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs) pro Sekunde Millionen von Ereignissen von verbundenen IoT-Geräten und -Anwendungen.

Informationen zu den ersten Schritten mit Azure Event Hubs finden Sie unter [Empfangen von Ereignissen von Azure Event Hubs mithilfe von Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Clientbibliothek

Mit der Event Hubs-Bibliothek können Sie Ereignisse an Azure Event Hub senden und Ereignisse von einem Event Hub nutzen und verarbeiten.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die [Clientbibliothek](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) in Ihrem Projekt zu verwenden.
 

## <a name="example"></a>Beispiel

Senden Sie Ereignissen an einen Event Hub:

```java
final ConnectionStringBuilder connStr = new ConnectionStringBuilder()
                                            .setNamespaceName(namespaceName)
                                            .setEventHubName(eventHubName)
                                            .setSasKeyName(sasKeyName)
                                            .setSasKey(sasKey);
final EventHubClient ehClient = EventHubClient.createSync(connStr.toString());

final byte[] payloadBytes = "Test AMQP message".getBytes("UTF-8");
final EventData sendEvent = new EventData(payloadBytes);

ehClient.sendSync(sendEvent);
```


> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a>Beispiele

[Untersuchen der Datenebenen-API von Event Hub anhand von Beispielen][1]

[Schreiben in Event Hub über JMS und Lesen aus Apache Storm][2]

[Lesen und Schreiben aus EventHubs mit einer .NET-/Java-Hybridtopologie][3] 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Sehen Sie sich weitere [Java-Codebeispiele für Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) an, die Sie in Ihren Apps verwenden können.

