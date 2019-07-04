---
title: Bereitstellen eines Java-basierten MicroProfile-Diensts in Azure-Web-App für Container
description: Hier erfahren Sie, wie Sie einen MicroProfile-Dienst unter Verwendung von Docker und Azure-Web-App für Container bereitstellen.
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533591"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="60ccf-103">Bereitstellen eines Java-basierten MicroProfile-Diensts in Azure-Web-App für Container</span><span class="sxs-lookup"><span data-stu-id="60ccf-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="60ccf-104">MicroProfile eignet sich sehr gut, um besonders kleine Java-Anwendungen zu erstellen, die Sie schnell und einfach in Diensten wie [Azure-Web-App für Container](https://azure.microsoft.com/services/app-service/containers/) bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="60ccf-104">MicroProfile is a great way to build exceedingly small Java applications that you can quickly and easily deploy to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="60ccf-105">In diesem Tutorial erstellen Sie einen einfachen MicroProfile-basierten Microservice, den Sie dann in einen Docker-Container packen, in einer [Azure Container Registry-Instanz](https://azure.microsoft.com/services/container-registry/) bereitstellen und anschließend über Azure Web-App für Container hosten.</span><span class="sxs-lookup"><span data-stu-id="60ccf-105">In this tutorial, you create a simple, MicroProfile-based microservice that you containerize into a Docker container, deploy to an [Azure container registry instance](https://azure.microsoft.com/services/container-registry/), and then host by using Azure Web App for Containers.</span></span>

> [!NOTE]
> <span data-ttu-id="60ccf-106">Dieses Verfahren kann für jede Implementierung von „MicroProfile.io“ verwendet werden, solange das Docker-Containerimage selbstausführbar ist (d. h., das Image enthält die Runtime).</span><span class="sxs-lookup"><span data-stu-id="60ccf-106">This procedure works with any implementation of MicroProfile.io, as long the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

<span data-ttu-id="60ccf-107">In diesem Beispiel verwenden Sie [Payara Micro](https://www.payara.fish/payara_micro) und [MicroProfile 1.3](https://microprofile.io/), um eine kleine (ungefähr 5.000 Byte) Java-WAR-Datei (Web Application Requirement) zu erstellen und diese dann in ein Docker-Image von etwa 174 Megabyte (MB) zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="60ccf-107">In this sample, you use [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a small (approximately 5,000 bytes) Java web application requirement (WAR) file, and then package it into a Docker image of approximately 174 megabytes (MB).</span></span> <span data-ttu-id="60ccf-108">Das Docker-Image enthält alles, was für eine vollständige Containerbereitstellung der Web-App benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="60ccf-108">The Docker image contains everything necessary for a fully containerized deployment of the web app.</span></span>

<span data-ttu-id="60ccf-109">Wenn sich der Quellcode der Anwendung geändert hat, muss nicht das gesamte 174-MB-Docker-Image erneut bereitgestellt werden, weil Docker nur die Unterschiede hochlädt (die deutlich kleiner sind).</span><span class="sxs-lookup"><span data-stu-id="60ccf-109">An entire 174 MB Docker image doesn't need to be redeployed whenever the application source code is changed, because Docker uploads only the differences (which are significantly smaller).</span></span> <span data-ttu-id="60ccf-110">Daher ist der Prozess zum Ausführen einer neuen MicroProfile-Anwendungsversion über eine CI/CD-Pipeline äußerst effizient und schnell, wodurch die Reibungsverluste verringert werden und eine schnelle Entwicklungsiteration ermöglicht wird.</span><span class="sxs-lookup"><span data-stu-id="60ccf-110">Consequently, the process of executing a new release of a MicroProfile application via a CI/CD pipeline is extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="60ccf-111">Sie arbeiten dieses Tutorial durch, indem Sie zuerst den Code lokal erstellen und ausführen und ihn dann als Web-App in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="60ccf-111">You'll work through this tutorial by first creating and running the code locally and then deploying it as a web app on Azure.</span></span> <span data-ttu-id="60ccf-112">In beiden Phasen können Sie Docker nutzen, um Ihre Aktivitäten zu vereinfachen und zu standardisieren.</span><span class="sxs-lookup"><span data-stu-id="60ccf-112">In both phases, you can depend on Docker to simplify and standardize your efforts.</span></span> <span data-ttu-id="60ccf-113">Bevor Sie beginnen, erstellen Sie eine Azure Container Registry-Instanz, in der Sie Ihre Docker-Container speichern können.</span><span class="sxs-lookup"><span data-stu-id="60ccf-113">Before you begin, you'll create an Azure container registry instance for storing your Docker containers.</span></span>

## <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="60ccf-114">Erstellen einer Azure Container Registry-Instanz</span><span class="sxs-lookup"><span data-stu-id="60ccf-114">Create an Azure container registry instance</span></span>

<span data-ttu-id="60ccf-115">Sie können das [Azure-Portal](http://portal.azure.com) verwenden, um die Azure Container Registry-Instanz zu erstellen, es gibt aber auch andere Optionen, etwa die Azure-Befehlszeilenschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="60ccf-115">You can use the [Azure portal](http://portal.azure.com) to create the Azure container registry instance, but there are other choices also, such as the Azure CLI.</span></span> <span data-ttu-id="60ccf-116">Um eine neue Azure Container Registry-Instanz zu erstellen, gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="60ccf-116">To create a new Azure container registry instance, do the following:</span></span>

1. <span data-ttu-id="60ccf-117">Melden Sie sich beim [Azure-Portal](http://portal.azure.com) an, und erstellen Sie eine neue Azure Container Registry-Ressource.</span><span class="sxs-lookup"><span data-stu-id="60ccf-117">Sign in to the [Azure portal](http://portal.azure.com) and create a new Azure container registry resource.</span></span> <span data-ttu-id="60ccf-118">Geben Sie einen Registrierungsnamen an (dieser Name muss als `docker.registry`-Eigenschaft in der *pom.xml*-Datei festgelegt werden).</span><span class="sxs-lookup"><span data-stu-id="60ccf-118">Provide a registry name (this name should be set as the `docker.registry` property in the *pom.xml* file).</span></span> <span data-ttu-id="60ccf-119">Ändern Sie die Standardeinstellungen nach Bedarf, und wählen Sie anschließend **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="60ccf-119">Change the defaults as you want, and then select **Create**.</span></span>

1. <span data-ttu-id="60ccf-120">Nach etwa 30 Sekunden, wenn die Container Registry-Instanz aktiv ist, wählen Sie die Container Registry-Instanz aus, und wählen Sie dann im linken Bereich den Link **Zugriffsschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="60ccf-120">In about 30 seconds, when the container registry instance is live, select the container registry instance and then, in the left pane, select the **Access keys** link.</span></span> 

    <span data-ttu-id="60ccf-121">Aktivieren Sie die Einstellung *Administratorbenutzer*, damit Sie von Ihren Computern Zugriff auf diese Container Registry-Instanz haben und Docker-Container in die Instanz pushen können.</span><span class="sxs-lookup"><span data-stu-id="60ccf-121">Be sure to enable the *admin user* setting, so that you can access this container registry instance from your machines and push Docker containers into it.</span></span> <span data-ttu-id="60ccf-122">Dadurch wird auch Zugriff aus der Azure Web-App für Container-Instanz aktiviert, die Sie bald schnell einrichten werden.</span><span class="sxs-lookup"><span data-stu-id="60ccf-122">Doing so also enables access from the Azure Web App for Containers instance that you'll set up soon.</span></span>

1. <span data-ttu-id="60ccf-123">Kopieren Sie im Bereich **Zugriffsschlüssel** die Werte von **username** und **password**, und fügen Sie diese Werte in Ihre globale *settings.xml*-Maven-Datei ein.</span><span class="sxs-lookup"><span data-stu-id="60ccf-123">In the **Access keys** pane, copy the **username** and **password** values and paste them into your global Maven *settings.xml* file.</span></span> <span data-ttu-id="60ccf-124">Weitere Informationen zu Maven-Einstellungen finden Sie auf der [Apache Maven Project](https://maven.apache.org/settings.html)-Website.</span><span class="sxs-lookup"><span data-stu-id="60ccf-124">For more information about Maven settings, go to the [Apache Maven Project](https://maven.apache.org/settings.html) website.</span></span> 

   <span data-ttu-id="60ccf-125">Zu Referenzzwecken ist hier ein Beispiel der *${user.home}/.m2/settings.xml*-Datei aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="60ccf-125">For your reference, here's an example of the *${user.home}/.m2/settings.xml* file:</span></span>

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

<span data-ttu-id="60ccf-126">Nachdem Sie Ihre Container-Registry-Instanz erstellt haben, können Sie nun Ihre MicroProfile-Anwendung lokal erstellen und ausführen.</span><span class="sxs-lookup"><span data-stu-id="60ccf-126">Now that you've created your container registry instance, you can move on to building and running your MicroProfile application locally.</span></span>

## <a name="create-your-microprofile-application"></a><span data-ttu-id="60ccf-127">Erstellen Ihrer MicroProfile-Anwendung</span><span class="sxs-lookup"><span data-stu-id="60ccf-127">Create your MicroProfile application</span></span>

<span data-ttu-id="60ccf-128">Dieser Beispielcode basiert auf einer Beispielanwendung, die auf GitHub verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="60ccf-128">This example code is based on a sample application that's available on GitHub.</span></span> <span data-ttu-id="60ccf-129">Um den Code auf Ihrem Computer zu klonen, geben Sie die folgenden Befehle ein:</span><span class="sxs-lookup"><span data-stu-id="60ccf-129">To clone the code onto your machine, enter the following commands:</span></span>

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

<span data-ttu-id="60ccf-130">Dieses Verzeichnis enthält eine *pom.xml*-Datei, die Sie dazu verwenden können, das Projekt in dem Format anzugeben, das vom Maven-Erstellungstool verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="60ccf-130">This directory contains a *pom.xml* file that you use to specify the project in the format that's used by the Maven build tool.</span></span> <span data-ttu-id="60ccf-131">Sie können die Datei bearbeiten, damit sie Ihren Anforderungen entspricht.</span><span class="sxs-lookup"><span data-stu-id="60ccf-131">You can edit the file to suit your own needs.</span></span> <span data-ttu-id="60ccf-132">Insbesondere müssen die Eigenschaften `docker.registry` und `docker.name` entsprechend der `docker.registry`- und der `docker.name`-Eigenschaft geändert werden, die erstellt wurden, als Sie die Azure Container Registry-Instanz eingerichtet haben.</span><span class="sxs-lookup"><span data-stu-id="60ccf-132">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` properties that were created when you set up the Azure container registry instance.</span></span>

<span data-ttu-id="60ccf-133">Eine andere wichtige Datei in diesem Verzeichnis ist die Dockerfile, die wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="60ccf-133">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="60ccf-134">Das Dockerfile erstellt einen neuen Docker-Container, der auf dem Payara Micro-Docker-Container basiert.</span><span class="sxs-lookup"><span data-stu-id="60ccf-134">The Dockerfile creates a new Docker container that's based on the Payara Micro Docker Container.</span></span> <span data-ttu-id="60ccf-135">Es kopiert in die WAR-Datei, die als Teil Ihres Buildprozesses erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="60ccf-135">It copies in the WAR file that was created as part of your build process.</span></span> <span data-ttu-id="60ccf-136">Es macht den Port 8080 verfügbar, sodass Sie auf den Dienst zugreifen können, nachdem er in einem Docker-Container aktiviert ist und ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="60ccf-136">It also exposes port 8080 so that you can access the service after it's up and running within a Docker container.</span></span>

<span data-ttu-id="60ccf-137">Wenn Sie das Verzeichnis *src* öffnen, finden Sie schließlich die `Application`-Klasse, die hier reproduziert ist:</span><span class="sxs-lookup"><span data-stu-id="60ccf-137">When you open the *src* directory, you'll eventually discover the `Application` class that's reproduced here:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="60ccf-138">Die *@ApplicationPath("/api")* -Annotation gibt den Basisendpunkt für diesen Microservice an.</span><span class="sxs-lookup"><span data-stu-id="60ccf-138">The *@ApplicationPath("/api")* annotation specifies the base endpoint for this microservice.</span></span> <span data-ttu-id="60ccf-139">Das heißt, für alle Endpunkte wird */api* dem Rest der URL vorangestellt, die erforderlich ist, um auf einen bestimmten REST-Endpunkt zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="60ccf-139">That is, for all endpoints, */api* precedes the rest of the URL that's required to access any specific REST endpoint.</span></span>

<span data-ttu-id="60ccf-140">Das Paket *api* enthält eine Klasse namens `API` mit folgendem Code:</span><span class="sxs-lookup"><span data-stu-id="60ccf-140">Inside the *api* package is a class named `API`, which contains the following code:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

<span data-ttu-id="60ccf-141">Durch Verwenden der *@Path("/helloworld")* -Annotation können Sie sehen, dass dieser REST-Endpunkt, wenn er mit der */api* kombiniert wird, die in der `Application`-Klasse angegeben ist, gleich */api/helloworld* ist.</span><span class="sxs-lookup"><span data-stu-id="60ccf-141">Through the use of the *@Path("/helloworld")* annotation, you can see that this REST endpoint, when it's combined with the */api* that's specified in the `Application` class, will be */api/helloworld*.</span></span> <span data-ttu-id="60ccf-142">Wenn Sie diesen Endpunkt über eine HTTP GET-Anforderung aufrufen, können Sie sehen, dass durch die Methode Text/HTML erzeugt wird, und dies ist tatsächlich einfach die hartcodierte Zeichenfolge „Hello, world!“.</span><span class="sxs-lookup"><span data-stu-id="60ccf-142">When you call this endpoint by using an HTTP GET request, you can see that the method produces text/html and, in fact, it's simply a hard-coded string, "Hello, world!"</span></span>

<span data-ttu-id="60ccf-143">Bisher ist in diesem Artikel der gesamten Code angegeben, der für die Erstellung eines Microservice mithilfe von MicroProfile erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="60ccf-143">So far, this article has covered all the code that's required for you to create a microservice by using MicroProfile.</span></span> <span data-ttu-id="60ccf-144">Sie können nun Maven verwenden, um den Code zu erstellen, ihn in einen Docker-Container zu packen und ihn lokal auszuführen. Gehen Sie dazu wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="60ccf-144">You can now use Maven to build it, containerize it into a Docker container, and run it locally by doing the following:</span></span>

1. <span data-ttu-id="60ccf-145">Führen Sie `mvn clean package` aus, und warten Sie, bis der Befehl abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="60ccf-145">Run `mvn clean package`, and wait until it is complete.</span></span>

1. <span data-ttu-id="60ccf-146">Führen Sie `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest` aus.</span><span class="sxs-lookup"><span data-stu-id="60ccf-146">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span></span> <span data-ttu-id="60ccf-147">Zum Beispiel *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, wobei *\<docker.registry>* gleich *jogilescr.azurecr.io* and *\<docker.name>* gleich *samples/docker-helloworld* ist.</span><span class="sxs-lookup"><span data-stu-id="60ccf-147">For example, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, where *\<docker.registry>* is *jogilescr.azurecr.io* and *\<docker.name>* is *samples/docker-helloworld*.</span></span>

1. <span data-ttu-id="60ccf-148">Greifen Sie in Ihrem Webbrowser auf [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) und [http://localhost:8080/health](http://localhost:8080/health) zu.</span><span class="sxs-lookup"><span data-stu-id="60ccf-148">Try to access [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="60ccf-149">Wenn Sie die erwartete Antwort „Hello, world!“</span><span class="sxs-lookup"><span data-stu-id="60ccf-149">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="60ccf-150">(und integritätsbezogene Informationen für den Endpunkt [/health](http://localhost:8080/health)) sehen, haben Sie die MicroProfile-Anwendung erfolgreich auf Ihrem lokalen Computer bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="60ccf-150">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you've successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="push-the-container-to-the-azure-container-registry-instance"></a><span data-ttu-id="60ccf-151">Pushen des Containers in die Azure Container Registry-Instanz</span><span class="sxs-lookup"><span data-stu-id="60ccf-151">Push the container to the Azure container registry instance</span></span>

<span data-ttu-id="60ccf-152">Nachdem Sie Ihre MicroProfile-Anwendung erfolgreich auf Ihrem lokalen Computer erstellt und ausgeführt haben, pushen Sie den Container in Ihre Container Registry-Instanz.</span><span class="sxs-lookup"><span data-stu-id="60ccf-152">Now that you've successfully built and run your MicroProfile application on your local machine, push this container to your container registry instance.</span></span> 

> [!NOTE]
> <span data-ttu-id="60ccf-153">Obwohl in diesem Artikel eine Azure Container Registry-Instanz verwendet wird, sollte jede Container Registry-Instanz funktionieren, sofern die *pom.xml*-Datei bearbeitet wurde, sodass in ihr auf den entsprechenden Speicherort verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="60ccf-153">Although this article uses an Azure container registry instance, any container registry instance should work, as long as the *pom.xml* file is edited to point to the relevant location.</span></span>

1. <span data-ttu-id="60ccf-154">Um ein lokales Docker-Image zu bereinigen, zu kompilieren und zu erstellen, führen Sie `mvn clean package` aus.</span><span class="sxs-lookup"><span data-stu-id="60ccf-154">To clean, compile, and create a local Docker image, run `mvn clean package`.</span></span>
2. <span data-ttu-id="60ccf-155">Um den Container in die Azure Container Registry-Instanz zu pushen, führen Sie `mvn dockerfile:push` aus.</span><span class="sxs-lookup"><span data-stu-id="60ccf-155">To push the container to the Azure container registry instance, run `mvn dockerfile:push`.</span></span>

<span data-ttu-id="60ccf-156">Sie haben jetzt Ihr Docker-Containerimage in die Azure Container Registry-Instanz hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="60ccf-156">You now have your Docker container image uploaded to the Azure container registry instance.</span></span> <span data-ttu-id="60ccf-157">Das Image wird aber noch nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="60ccf-157">However, it's not yet running.</span></span> <span data-ttu-id="60ccf-158">Sie müssen es in einer Azure-Web-App für Container-Instanz bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="60ccf-158">You now have to deploy it to an Azure Web App for Containers instance.</span></span> 

## <a name="create-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="60ccf-159">Erstellen einer Azure-Web-App für Container-Instanz</span><span class="sxs-lookup"><span data-stu-id="60ccf-159">Create an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="60ccf-160">Wählen Sie im [Azure-Portal](http://portal.azure.com) im linken Bereich den Eintrag **Web + Mobil** aus, und gehen Sie dann wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="60ccf-160">In the [Azure portal](http://portal.azure.com), in the left pane, select **Web + Mobile**, and then do the following:</span></span>

   <span data-ttu-id="60ccf-161">a.</span><span class="sxs-lookup"><span data-stu-id="60ccf-161">a.</span></span> <span data-ttu-id="60ccf-162">Geben Sie einen Namen an.</span><span class="sxs-lookup"><span data-stu-id="60ccf-162">Specify a name.</span></span> <span data-ttu-id="60ccf-163">Der Name wird die öffentliche URL der Web-App, daher ist es eine gute Idee, einen Namen auszuwählen, den Sie sich leicht merken können.</span><span class="sxs-lookup"><span data-stu-id="60ccf-163">The name will become the public URL of the web app, so it's a good idea to pick a name that you can easily remember.</span></span> <span data-ttu-id="60ccf-164">Bei Bedarf können Sie später einen benutzerdefinierten Domänennamen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="60ccf-164">You can add a custom domain name later, if you want.</span></span>

   <span data-ttu-id="60ccf-165">b.</span><span class="sxs-lookup"><span data-stu-id="60ccf-165">b.</span></span> <span data-ttu-id="60ccf-166">Wählen Sie im Abschnitt **Container konfigurieren** unter **Imagequelle** die Option **Azure Container Registry** aus, und wählen Sie anschließend in der Dropdownliste das richtige Image aus.</span><span class="sxs-lookup"><span data-stu-id="60ccf-166">In the **Configure container** section, under **Image source**, select **Azure Container Registry** and then, in the drop-down list, select the correct image.</span></span>

   <span data-ttu-id="60ccf-167">c.</span><span class="sxs-lookup"><span data-stu-id="60ccf-167">c.</span></span> <span data-ttu-id="60ccf-168">Sie müssen keinen Wert im Feld **Startdatei** angeben.</span><span class="sxs-lookup"><span data-stu-id="60ccf-168">You don't need to specify a value in the **Startup File** field.</span></span>

1. <span data-ttu-id="60ccf-169">Nachdem Sie die Instanz erstellt haben, wählen Sie diese aus, und wählen Sie dann **Anwendungseinstellungen** aus.</span><span class="sxs-lookup"><span data-stu-id="60ccf-169">After you've created the instance, select it, and then select **Application Settings**.</span></span> <span data-ttu-id="60ccf-170">Geben Sie für **Schlüssel** die Einstellung **WEBSITES_PORT** und für **Wert** die Einstellung **8080** ein.</span><span class="sxs-lookup"><span data-stu-id="60ccf-170">For **Key**, enter **WEBSITES_PORT**, and for **Value**, enter **8080**.</span></span> <span data-ttu-id="60ccf-171">Diese Einstellungen geben für Azure an, welcher Port im Container verfügbar zu machen ist, und dass er extern Port 80 zugeordnet werden soll.</span><span class="sxs-lookup"><span data-stu-id="60ccf-171">These settings tell Azure which port to expose in the container and to map it to port 80 externally.</span></span>

1. <span data-ttu-id="60ccf-172">(Optional) Wählen Sie den Link **Docker-Container** aus, und aktivieren Sie dann die Option **Continuous Deployment**.</span><span class="sxs-lookup"><span data-stu-id="60ccf-172">(Optional) Select the **Docker Container** link, and then enable **Continuous Deployment**.</span></span> <span data-ttu-id="60ccf-173">Dies bewirkt, dass das Image nach jeder Aktualisierung, die Sie an ihm in der Azure Container Registry-Instanz vorgenommen haben, automatisch in der Azure-Web-App für Container-Instanz aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="60ccf-173">By doing so, whenever you update the Azure container registry instance image, it's automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="60ccf-174">Sie sollten nun auf die von Azure gehosteten Instanzen unter `http://<appname>.azurewebsites.net/microprofile/api/helloworld` und `http://<appname>.azurewebsites.net/health` zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="60ccf-174">You should now be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="60ccf-175">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="60ccf-175">Summary</span></span>

<span data-ttu-id="60ccf-176">In diesem Tutorial haben Sie Schritt für Schritt die Erstellung eines einfachen MicroProfile-basierten Microservice durchlaufen, haben ihn in einen Docker-Container gepackt, haben ihn lokal ausgeführt und haben ihn in Azure veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="60ccf-176">In this tutorial, you've stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, run it locally, and published it to Azure.</span></span> <span data-ttu-id="60ccf-177">Sie können Ihren Microservice erweitern, um weitere nützliche Funktionen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="60ccf-177">You can extend your microservice to provide additional useful functionality.</span></span> <span data-ttu-id="60ccf-178">Weitere Informationen finden Sie auf [MicroProfile.io](https://microprofile.io/).</span><span class="sxs-lookup"><span data-stu-id="60ccf-178">For more information, go to [MicroProfile.io](https://microprofile.io/).</span></span>
