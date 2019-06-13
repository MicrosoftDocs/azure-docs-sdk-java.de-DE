---
title: Verwenden von Docker-Images mit einem JDK für die Azure Java-Entwicklung
description: ''
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: ee8df2a08b23d090965cb42e2c15b934d4785e7c
ms.sourcegitcommit: 03379369346974c6e80f86e7129b885112b5c1a9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910228"
---
# <a name="use-docker-with-a-jdk-for-azure"></a><span data-ttu-id="6cfd5-102">Verwenden von Docker mit einem JDK für Azure</span><span class="sxs-lookup"><span data-stu-id="6cfd5-102">Use Docker with a JDK for Azure</span></span> 

<span data-ttu-id="6cfd5-103">Vorgefertigte Docker-Images für Java 7, 8 und 11 sind über [Docker Hub](https://hub.docker.com/_/microsoft-java-se) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="6cfd5-103">Pre-built Docker images for Java 7, 8, and 11 are available through [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span></span>

<span data-ttu-id="6cfd5-104">Auf Docker Hub stehen zertifizierte Docker-Containerimages für das Zulu JDK, die JRE und die monitorlose JRE für mehrere Basisbetriebssystem-Images zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="6cfd5-104">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker Hub:</span></span>

* [<span data-ttu-id="6cfd5-105">JDK</span><span class="sxs-lookup"><span data-stu-id="6cfd5-105">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
* [<span data-ttu-id="6cfd5-106">JRE</span><span class="sxs-lookup"><span data-stu-id="6cfd5-106">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
* [<span data-ttu-id="6cfd5-107">Monitorlose JRE</span><span class="sxs-lookup"><span data-stu-id="6cfd5-107">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

## <a name="running-a-docker-image"></a><span data-ttu-id="6cfd5-108">Ausführen eines Docker-Images</span><span class="sxs-lookup"><span data-stu-id="6cfd5-108">Running a Docker image</span></span>

<span data-ttu-id="6cfd5-109">Docker-Images können wie im folgenden Beispiel gezeigt mit der Syntax `$ docker run mcr.microsoft.com/java/jdk:tag java` ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="6cfd5-109">Docker images can be run using the syntax `$ docker run mcr.microsoft.com/java/jdk:tag java` as shown in the following example.</span></span>

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a><span data-ttu-id="6cfd5-110">Erstellen eines Docker-Images</span><span class="sxs-lookup"><span data-stu-id="6cfd5-110">Creating a Docker image</span></span>

<span data-ttu-id="6cfd5-111">Sie können wie in den folgenden Beispielen gezeigt unter Verwendung der offiziellen Docker Hub-Images von Microsoft ein Image erstellen:</span><span class="sxs-lookup"><span data-stu-id="6cfd5-111">You can create an image using Microsoft's official Docker Hub images as shown in the following examples.</span></span>

### <a name="create-a-docker-file"></a><span data-ttu-id="6cfd5-112">Erstellen einer Docker-Datei</span><span class="sxs-lookup"><span data-stu-id="6cfd5-112">Create a Docker file</span></span>

```cli
FROM mcr.microsoft.com/java/jdk:8u212-zulu-alpine 
  
RUN echo $' \
  
public class HelloWorld { \
   public static void main(String[] args) { \
      // Prints "Hello, World" in the terminal window. \
      System.out.println("Hello, World - From Microsoft Azure !!!"); \
   } \
}' > HelloWorld.java
  
RUN javac HelloWorld.java
  
CMD ["java", "HelloWorld"]
```

### <a name="build-a-docker-image"></a><span data-ttu-id="6cfd5-113">Erstellen eines Docker-Images</span><span class="sxs-lookup"><span data-stu-id="6cfd5-113">Build a Docker image</span></span>

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a><span data-ttu-id="6cfd5-114">Ausführen des neuen Images</span><span class="sxs-lookup"><span data-stu-id="6cfd5-114">Run the new image</span></span>

```cli
docker run hello-world
```

<span data-ttu-id="6cfd5-115">Die folgende Ausgabe wird angezeigt:</span><span class="sxs-lookup"><span data-stu-id="6cfd5-115">You will see the following output:</span></span>

```output
Hello World - From Microsoft Azure !!!
```
