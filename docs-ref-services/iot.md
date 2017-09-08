---
title: "Azure IoT Hub-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-IoT Hub-Bibliotheken"
keywords: "Azure, Java, SDK, API, Ereignisse, IoT, Streams, Geräte, IoT Hub"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: b386612741e222fcaeb7b6c38753d0cb7d616239
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-iot-libraries-for-java"></a><span data-ttu-id="61947-104">Azure IoT-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="61947-104">Azure IoT libraries for Java</span></span>

<span data-ttu-id="61947-105">Verbinden, überwachen und kontrollieren Sie IoT-Assets (Internet of Things, Internet der Dinge) mithilfe von [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-what-is-iot-hub).</span><span class="sxs-lookup"><span data-stu-id="61947-105">Connect, monitor, and control Internet of Things assets with [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-what-is-iot-hub).</span></span>

<span data-ttu-id="61947-106">Informationen zu den ersten Schritten mit Azure IoT Hub finden Sie unter [Herstellen einer Verbindung zwischen Ihrem Gerät und Ihrem IoT Hub mit Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span><span class="sxs-lookup"><span data-stu-id="61947-106">To get started with Azure IoT Hub, see [Connect your device to your IoT hub using Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span></span>

## <a name="iot-service-library"></a><span data-ttu-id="61947-107">IoT-Dienstbibliothek</span><span class="sxs-lookup"><span data-stu-id="61947-107">IoT Service library</span></span>

<span data-ttu-id="61947-108">Mit der IoT-Dienstbibliothek können Sie Geräte registrieren und Nachrichten von der Cloud an registrierte Geräte senden.</span><span class="sxs-lookup"><span data-stu-id="61947-108">Register devices and send messages from the cloud to registered devices using the IoT Service library.</span></span>

<span data-ttu-id="61947-109">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="61947-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a><span data-ttu-id="61947-110">IOT-Gerätebibliothek</span><span class="sxs-lookup"><span data-stu-id="61947-110">Iot Device library</span></span>

<span data-ttu-id="61947-111">Mit der IoT-Gerätebibliothek können Sie Nachrichten an die Cloud senden und Nachrichten auf Geräten empfangen.</span><span class="sxs-lookup"><span data-stu-id="61947-111">Send messages to the cloud and receive messages on devices using the IoT Device library.</span></span>

<span data-ttu-id="61947-112">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="61947-112">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="61947-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="61947-113">Explore the Client APIs</span></span>](/java/api/overview/azure/iot/clientlibrary)   

## <a name="example"></a><span data-ttu-id="61947-114">Beispiel</span><span class="sxs-lookup"><span data-stu-id="61947-114">Example</span></span>

<span data-ttu-id="61947-115">Senden Sie eine Nachricht von Azure IoT Hub an ein Gerät:</span><span class="sxs-lookup"><span data-stu-id="61947-115">Send a message from Azure IoT Hub to a device.</span></span>

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


## <a name="samples"></a><span data-ttu-id="61947-116">Beispiele</span><span class="sxs-lookup"><span data-stu-id="61947-116">Samples</span></span>

<span data-ttu-id="61947-117">[IoT-Gerätebeispiele](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span><span class="sxs-lookup"><span data-stu-id="61947-117">[IoT Device samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span></span>  
[<span data-ttu-id="61947-118">IoT-Dienstbeispiele</span><span class="sxs-lookup"><span data-stu-id="61947-118">IoT Service samples</span></span>](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

<span data-ttu-id="61947-119">Sehen Sie sich weitere [Java-Codebeispiele für Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="61947-119">Explore more [sample Java code for Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) you can use in your apps.</span></span>
