---
title: Azure IoT Hub-Bibliotheken für Java
description: Referenzdokumentation für die Java-IoT Hub-Bibliotheken
keywords: Azure, Java, SDK, API, Ereignisse, IoT, Streams, Geräte, IoT Hub
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: 497b2a72d851b8e43a48384c6f1a160e8a38cbe6
ms.sourcegitcommit: bb7286fad75a2bb43e6ce1a8f1b09e701147c9f9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047147"
---
# <a name="azure-iot-libraries-for-java"></a>Azure IoT-Bibliotheken für Java

Verbinden, überwachen und kontrollieren Sie IoT-Assets (Internet of Things, Internet der Dinge) mithilfe von [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).

Informationen zu den ersten Schritten mit Azure IoT Hub finden Sie unter [Herstellen einer Verbindung zwischen Ihrem Gerät und Ihrem IoT Hub mit Java](/azure/iot-hub/iot-hub-java-java-getstarted).

## <a name="iot-service-library"></a>IoT-Dienstbibliothek

Mit der IoT-Dienstbibliothek können Sie Geräte registrieren und Nachrichten von der Cloud an registrierte Geräte senden.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a>IOT-Gerätebibliothek

Mit der IoT-Gerätebibliothek können Sie Nachrichten an die Cloud senden und Nachrichten auf Geräten empfangen.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/java/api/overview/azure/iot/client)   

## <a name="example"></a>Beispiel

Senden Sie eine Nachricht von Azure IoT Hub an ein Gerät:

```java
Message messageToSend = new Message(messageText);
messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
messageToSend.setMessageId(java.util.UUID.randomUUID().toString());

// set message properties
Map<String, String> propertiesToSend = new HashMap<String, String>();
propertiesToSend.put(messagePropertyKey,messagePropertyKey);
messageToSend.setProperties(propertiesToSend);

CompletableFuture<Void> future = serviceClient.sendAsync(deviceId, messageToSend);
try {
    future.get();
}
catch (ExecutionException e) {
    System.out.println("Exception : " + e.getMessage());
}
```


## <a name="samples"></a>Beispiele

[IoT-Gerätebeispiele](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)     
[IoT-Dienstbeispiele](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

Sehen Sie sich weitere [Java-Codebeispiele für Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) an, die Sie in Ihren Apps verwenden können.
