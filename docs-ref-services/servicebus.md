---
title: Service Bus-Bibliotheken für Java
description: Referenzdokumentation für die Java-Clientbibliotheken und -Verwaltungsbibliotheken für Service Bus
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
ms.openlocfilehash: ed830b4f7ffa104174205f75ea2923235029ea80
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/08/2018
ms.locfileid: "33887760"
---
# <a name="service-bus-libraries-for-java"></a>Service Bus-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Service Bus ist ein professioneller Plattformdienst für transaktionales Messaging, der äußerst zuverlässige Warteschlangen und Veröffentlichungs-/Abonnementthemen mit umfassenden Features wie geordneter Übermittlung, Sitzungen, Partitionierung, Planung, komplexen Abonnements sowie Handhabung von Workflows und Transaktionen kombiniert.

Die Funktionen des Service Bus-Features sind vergleichbar mit den Funktionen lokaler High-End-Legacy-Nachrichtenbroker und übertreffen diese häufig sogar. Service Bus-Features werden über standardbasierte Protokolle wie AMQP 1.0 und HTTPS bereitgestellt, und sämtliche Protokollgesten sind vollständig dokumentiert, um eine umfassende Interoperabilität zu gewährleisten. 

Service Bus Premium bietet hochverfügbares und robustes Messaging sowie eine wettbewerbsfähige Durchsatzleistung (sogar im Vergleich mit umfangreichen lokalen Datencenterbereitstellungen) ohne Entscheidungs- und Anschaffungsprozesse für Hardware, Bereitstellungsplanung und -durchführung oder endlose Leistungsoptimierungen. 

Service Bus Premium ist ein vollständig verwaltetes Angebot mit dedizierter, für die einzelnen Mandanten reservierter Kapazität und zeichnet sich durch planbare Leistung sowie durch ein einfaches, kapazitätsorientiertes Preismodell und erheblich geringere Gesamtkosten aus als kommerzielle lokale Broker. Für viele Kunden kann Service Bus Premium schon heute dedizierte lokale Messagingcluster ersetzen – selbst wenn die damit verbundenen Workloads nicht in der Cloud ausgeführt werden. 

Weitere Informationen zu Service Bus-Konzepten finden Sie in der [Service Bus-Messaging-Dokumentation](https://docs.microsoft.com/azure/service-bus-messaging/). 

Für Java-Entwickler bietet Service Bus eine von Microsoft unterstützte native API. Darüber hinaus kann Service Bus auch mit AMQP 1.0-kompatiblen Bibliotheken wie dem JMS-Anbieter von Apache Qpid Proton verwendet werden.

## <a name="client-library"></a>Clientbibliothek

Der offizielle Service Bus-Client steht als [Quellcode auf GitHub](https://github.com/azure/azure-service-bus-java) und in Form von Binärdateien und gepackten Quellen bei [Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22) zur Verfügung.

**Das [Beispielcoderepository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) enthält Beispiele für:**
* die Verwendung von [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java).
* die Verwendung von [„TopicClient“ und „SubscriptionClient“](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java).
* die Verwendung der Nachrichten vom Typ [„MessageSender“ und „MessageReceiver“](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) von Service Bus.

Fügen Sie der Datei `pom.xml` Ihres Maven-Projekts eine Abhängigkeit hinzu, um die Bibliothek in Ihrem eigenen Projekt zu verwenden. Geben Sie die gewünschte Version an.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

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
> [Untersuchen der Client-APIs](/java/api/overview/azure/servicebus/client)
> [Weitere Beispiele (ausführlichere Informationen siehe oben)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)

## <a name="management-api"></a>Verwaltungs-API

Die Verwaltungs-API dient zum Erstellen und Verwalten von Namespaces, Themen, Warteschlangen und Abonnements.

**Hier finden Sie einige Beispiele:**
* [Verwalten von Service Bus-Warteschlangen](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
* [Erstellen und Abonnieren von Service Bus-Themen](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)

**Verwenden Sie die Verwaltungs-API in Ihrem Projekt:**
\
Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/servicebus/management)

Sehen Sie sich weitere [Java-Codebeispiele für Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) an, die Sie in Ihren Apps verwenden können.
