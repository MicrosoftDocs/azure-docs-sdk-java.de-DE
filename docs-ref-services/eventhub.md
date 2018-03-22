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
ms.openlocfilehash: 076906ff3cafcb4eba97b0a022e5214d7834517c
ms.sourcegitcommit: 02b70b9f5d34415c337601f0b818f7e0985fd884
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="829db-104">Azure Event Hub-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="829db-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="829db-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="829db-105">Overview</span></span>

<span data-ttu-id="829db-106">Sammeln und verwalten Sie mithilfe von [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs) pro Sekunde Millionen von Ereignissen von verbundenen IoT-Geräten und -Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="829db-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="829db-107">Informationen zu den ersten Schritten mit Azure Event Hubs finden Sie unter [Empfangen von Ereignissen von Azure Event Hubs mithilfe von Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="829db-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="829db-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="829db-108">Client library</span></span>

<span data-ttu-id="829db-109">Mit der Event Hubs-Bibliothek können Sie Ereignisse an Azure Event Hub senden und Ereignisse von einem Event Hub nutzen und verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="829db-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="829db-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="829db-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="829db-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="829db-111">Example</span></span>

<span data-ttu-id="829db-112">Senden Sie Ereignissen an einen Event Hub:</span><span class="sxs-lookup"><span data-stu-id="829db-112">Send an event to an event hub.</span></span>

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="829db-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="829db-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhub/client)


## <a name="samples"></a><span data-ttu-id="829db-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="829db-114">Samples</span></span>

<span data-ttu-id="829db-115">[Schreiben in Event Hub über JMS und Lesen aus Apache Storm][1]
[Lesen und Schreiben in EventHubs mit einer .NET-/Java-Hybridtopologie][2]</span><span class="sxs-lookup"><span data-stu-id="829db-115">[Write to Event Hub via JMS and read from Apache Storm][1]
[Read and write from EventHubs using a hybrid .NET/Java topology][2]</span></span> 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="829db-116">Sehen Sie sich weitere [Java-Codebeispiele für Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="829db-116">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

