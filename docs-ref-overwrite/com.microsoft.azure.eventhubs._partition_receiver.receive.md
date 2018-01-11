---
uid: com.microsoft.azure.eventhubs._partition_receiver.receive(final int)
summary: 'Receives a batch of [EventData](/java/api/com.microsoft.azure.eventhubs._event_data) objects from an Event Hubs partition.'
remarks: *content
---

<span data-ttu-id="5c55f-101">Im folgenden Beispielcode wird die synchrone Version der API verwendet, aber die Konzepte sind identisch:</span><span class="sxs-lookup"><span data-stu-id="5c55f-101">The following sample code uses the synchronous version of the API, but the concepts are the same:</span></span>

```java
EventHubClient client = createFromConnectionStringSync(final String connectionString)("connection");
PartitionReceiver receiver = client.createPartitionReceiverSync("ConsumerGroup1", "1"); 
Iterable{<}EventData{>} receivedEvents = receiver.receiveSync();

while (true) 
{ 
    int batchSize = 0; 
    if (receivedEvents != null) 
    { 
        for(EventData receivedEvent: receivedEvents) 
        { 
            System.out.println(String.format("Message Payload: %s", new String(receivedEvent.getBytes(), Charset.defaultCharset()))); 
            System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s", receivedEvent.getSystemProperties().getOffset(), receivedEvent.getSystemProperties().getSequenceNumber(), receivedEvent.getSystemProperties().getEnqueuedTime())); 
            batchSize++; 
        } 
    } 

    System.out.println(String.format("ReceivedBatch Size: %s", batchSize)); 
    receivedEvents = receiver.receiveSync(); 
} 
```
