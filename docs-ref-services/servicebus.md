---
title: "Service Bus-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Clientbibliotheken und -Verwaltungsbibliotheken für Service Bus"
keywords: Azure, Java, SDK, API, Nessaging, AMQP, Qpid, JMS, PubSub, Pub-Sub, Nachrichtenbroker
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: service-bus
ms.openlocfilehash: 6fccbc76a3600e2bbe43e4332c6146d2be81b6c9
ms.sourcegitcommit: fcf1189ede712ae30f8c7626bde50c9b8bb561bc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="service-bus-libraries-for-java"></a><span data-ttu-id="6f95f-104">Service Bus-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="6f95f-104">Service Bus libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="6f95f-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="6f95f-105">Overview</span></span>

<span data-ttu-id="6f95f-106">Service Bus ist ein professioneller Plattformdienst für transaktionales Messaging, der äußerst zuverlässige Warteschlangen und Veröffentlichungs-/Abonnementthemen mit umfassenden Features wie geordneter Übermittlung, Sitzungen, Partitionierung, Planung, komplexen Abonnements sowie Handhabung von Workflows und Transaktionen kombiniert.</span><span class="sxs-lookup"><span data-stu-id="6f95f-106">Service Bus is an enterprise-class, transactional messaging platform service that provides highly reliable queues and publish/subscribe topics with deep feature capabilities such as ordered delivery, sessions, partitioning, scheduling, complex subscriptions, as well as workflow and transaction handling.</span></span>

<span data-ttu-id="6f95f-107">Die Funktionen des Service Bus-Features sind vergleichbar mit den Funktionen lokaler High-End-Legacy-Nachrichtenbroker und übertreffen diese häufig sogar.</span><span class="sxs-lookup"><span data-stu-id="6f95f-107">The Service Bus feature capabilities are comparable and often exceed those of high-end, on-premises legacy message brokers.</span></span> <span data-ttu-id="6f95f-108">Service Bus-Features werden über standardbasierte Protokolle wie AMQP 1.0 und HTTPS bereitgestellt, und sämtliche Protokollgesten sind vollständig dokumentiert, um eine umfassende Interoperabilität zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="6f95f-108">The Service Bus features are available via standards-based protocols like AMQP 1.0 and HTTPS and all protocol gestures are fully documented, allowing for broad interoperability.</span></span> 

<span data-ttu-id="6f95f-109">Service Bus Premium bietet hochverfügbares und robustes Messaging sowie eine wettbewerbsfähige Durchsatzleistung (sogar im Vergleich mit umfangreichen lokalen Datencenterbereitstellungen) ohne Entscheidungs- und Anschaffungsprozesse für Hardware, Bereitstellungsplanung und -durchführung oder endlose Leistungsoptimierungen.</span><span class="sxs-lookup"><span data-stu-id="6f95f-109">Focusing on highly available and reliable durable messaging, the Service Bus Premium provides competitive throughput performance even with substantial local datacenter deployments, but without hardware selection and acquisition processes, deployment planning and execution, and endless performance optimization sessions.</span></span> 

<span data-ttu-id="6f95f-110">Service Bus Premium ist ein vollständig verwaltetes Angebot mit dedizierter, für die einzelnen Mandanten reservierter Kapazität und zeichnet sich durch planbare Leistung sowie durch ein einfaches, kapazitätsorientiertes Preismodell und erheblich geringere Gesamtkosten aus als kommerzielle lokale Broker.</span><span class="sxs-lookup"><span data-stu-id="6f95f-110">Service Bus Premium is a fully managed offering with dedicated capacity reserved for each tenant that yields predictable performance with a simple, capacity-oriented pricing model and at extremely lower overall cost than commercial on-premises brokers.</span></span> <span data-ttu-id="6f95f-111">Für viele Kunden kann Service Bus Premium schon heute dedizierte lokale Messagingcluster ersetzen – selbst wenn die damit verbundenen Workloads nicht in der Cloud ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="6f95f-111">For many customers, Service Bus Premium can replace dedicated on-premises messaging clusters today, even if the attached workloads do not run in the cloud.</span></span> 

<span data-ttu-id="6f95f-112">Weitere Informationen zu Service Bus-Konzepten finden Sie in der [Service Bus-Messaging-Dokumentation](https://docs.microsoft.com/azure/service-bus-messaging/).</span><span class="sxs-lookup"><span data-stu-id="6f95f-112">Learn more about Service Bus concepts [in the messaging documentation section](https://docs.microsoft.com/azure/service-bus-messaging/)</span></span> 

<span data-ttu-id="6f95f-113">Für Java-Entwickler bietet Service Bus eine von Microsoft unterstützte native API. Darüber hinaus kann Service Bus auch mit AMQP 1.0-kompatiblen Bibliotheken wie dem JMS-Anbieter von Apache Qpid Proton verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6f95f-113">For Java developers, Service Bus provides a Microsoft supported native API and Service Bus can also be used with AMQP 1.0 compliant libraries such as Apache Qpid Proton's JMS provider.</span></span>

<span data-ttu-id="6f95f-114">Der offizielle Service Bus-Client steht als [Quellcode auf GitHub](https://github.com/azure/azure-service-bus-java) und in Form von Binärdateien und gepackten Quellen bei [Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="6f95f-114">The official Service Bus client is available in [source code form on GitHub](https://github.com/azure/azure-service-bus-java) and binaries and packaged sources [are available on Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span></span> 


## <a name="client-library"></a><span data-ttu-id="6f95f-115">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="6f95f-115">Client library</span></span>


<span data-ttu-id="6f95f-116">Fügen Sie der Datei `pom.xml` Ihres Maven-Projekts eine Abhängigkeit hinzu, um die Bibliothek in Ihrem eigenen Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="6f95f-116">Add a dependency to your Maven project's `pom.xml` file to use the library in your own project.</span></span> <span data-ttu-id="6f95f-117">Geben Sie die gewünschte Version an.</span><span class="sxs-lookup"><span data-stu-id="6f95f-117">Specify the version as desired.</span></span>

<span data-ttu-id="6f95f-118">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="6f95f-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="examples"></a><span data-ttu-id="6f95f-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="6f95f-119">Examples</span></span>

<span data-ttu-id="6f95f-120">Das [Beispielcoderepository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) enthält Beispiele für die Verwendung von Nachrichten vom Typ [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java), [TopicClient und SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java) und [MessageSender und MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) aus Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6f95f-120">The [sample code repository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contains samples for how to [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java) and [TopicClient and SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java) and [MessageSender and MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) messages from Service Bus.</span></span>


```java
public class BasicSendReceiveWithQueueClient {
    // Connection String for the namespace can be obtained from the Azure portal under the
    // 'Shared Access policies' section.
    private static final String connectionString = "{connection string}";
    private static final String queueName = "{queue name}";
    private static IQueueClient queueClient;
    private static int totalSend = 100;
    private static int totalReceived = 0;

    public static void main(String[] args) throws Exception {

        Log.log("Starting BasicSendReceiveWithQueueClient sample");

        // create client
        Log.log("Create queue client.");
        queueClient = new QueueClient(new ConnectionStringBuilder(connectionString, queueName), ReceiveMode.PeekLock);

        // send and receive
        queueClient.registerMessageHandler(new MessageHandler(queueClient), new MessageHandlerOptions(1, false, Duration.ofMinutes(1)));
        for (int i = 0; i < totalSend; i++) {
            int j = i;
            Log.log("Sending message #%d.", j);
            queueClient.sendAsync(new Message("" + i)).thenRunAsync(() -> { Log.log("Sent message #%d.", j);});
        }

        while(totalReceived != totalSend) {
            Thread.sleep(1000);
        }

        Log.log("Received all messages, exiting the sample.");
        Log.log("Closing queue client.");
        queueClient.close();
    }

    static class MessageHandler implements IMessageHandler {
        private IQueueClient client;

        public MessageHandler(IQueueClient client) {
            this.client = client;
        }

        @Override
        public CompletableFuture<Void> onMessageAsync(IMessage iMessage) {
            Log.log("Received message with sq#: %d and lock token: %s.", iMessage.getSequenceNumber(), iMessage.getLockToken());
            return this.client.completeAsync(iMessage.getLockToken()).thenRunAsync(() -> {
                Log.log("Completed message sq#: %d and locktoken: %s", iMessage.getSequenceNumber(), iMessage.getLockToken());
                totalReceived++;
            });
        }

        @Override
        public void notifyException(Throwable throwable, ExceptionPhase exceptionPhase) {
            Log.log(exceptionPhase + "-" + throwable.getMessage());
        }
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f95f-121">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="6f95f-121">Explore the Client APIs</span></span>](/java/api/overview/azure/servicebus/clientlibrary)

## <a name="management-api"></a><span data-ttu-id="6f95f-122">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="6f95f-122">Management API</span></span>

<span data-ttu-id="6f95f-123">Die Verwaltungs-API dient zum Erstellen und Verwalten von Namespaces, Themen, Warteschlangen und Abonnements.</span><span class="sxs-lookup"><span data-stu-id="6f95f-123">Create and manage namespaces, topics, queues, and subscriptions with the management API.</span></span>

<span data-ttu-id="6f95f-124">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="6f95f-124">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f95f-125">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="6f95f-125">Explore the Management APIs</span></span>](/java/api/overview/azure/servicebus/managementapi)


## <a name="examples"></a><span data-ttu-id="6f95f-126">Beispiele</span><span class="sxs-lookup"><span data-stu-id="6f95f-126">Examples</span></span>

<span data-ttu-id="6f95f-127">[Verwalten von Service Bus-Warteschlangen](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Erstellen und Abonnieren von Service Bus-Themen](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span><span class="sxs-lookup"><span data-stu-id="6f95f-127">[Manage Service Bus queues](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Create and subscribe to Service Bus topics](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span></span>

<span data-ttu-id="6f95f-128">Sehen Sie sich weitere [Java-Codebeispiele für Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="6f95f-128">Explore more [sample Java code for Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) you can use in your apps.</span></span>
