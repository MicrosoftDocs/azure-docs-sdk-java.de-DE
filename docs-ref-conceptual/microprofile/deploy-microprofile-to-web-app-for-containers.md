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
ms.openlocfilehash: 1eb0e7d7a718a1c106adebbf89011f6e3fa1504e
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040248"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="8f8e9-103">Bereitstellen eines Java-basierten MicroProfile-Diensts in Azure-Web-App für Container</span><span class="sxs-lookup"><span data-stu-id="8f8e9-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="8f8e9-104">MicroProfile eignet sich sehr gut, um besonders kleine Java-Anwendungen zu erstellen, die schnell und einfach in Diensten wie [Azure-Web-App für Container](https://azure.microsoft.com/services/app-service/containers/) bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-104">MicroProfile is a great way to build exceedingly tiny Java applications that can be quickly and easily deployed to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="8f8e9-105">In diesem Tutorial erstellen wir einen einfachen MicroProfile-basierten Microservice, der dann in einen Docker-Container gepackt, in einer [Azure Container Registry-Instanz](https://azure.microsoft.com/services/container-registry/) bereitgestellt und anschließend mithilfe von Azure-Web-App für Container gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-105">In this tutorial we will create a simple MicroProfile-based microservice that is then containerized into a Docker container, deployed into an [Azure Container Registry](https://azure.microsoft.com/services/container-registry/), and then hosted using Azure Web App for Containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8f8e9-106">Dieses Verfahren kann für jede Implementierung von „MicroProfile.io“ verwendet werden, solange das Docker-Containerimage selbstausführbar ist (sprich: die Runtime enthält).</span><span class="sxs-lookup"><span data-stu-id="8f8e9-106">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

<span data-ttu-id="8f8e9-107">In diesem Beispiel werden [Payara Micro](https://www.payara.fish/payara_micro) und [MicroProfile 1.3](https://microprofile.io/) verwendet, um eine kleine Java-WAR-Datei (5.085 Bytes auf dem Erstellercomputer) zu erstellen. Diese wird dann in ein Docker-Image (mit einer Größe von etwa 174 MB) verpackt.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-107">More concretely, this sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a tiny Java war file (5,085 bytes on the authors machine), and then packages it up into a Docker image (which is approximately 174 megabytes).</span></span> <span data-ttu-id="8f8e9-108">Dieses Docker-Image enthält alles, was für eine vollständige Containerbereitstellung dieser Web-App benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-108">This Docker image contains everything necessary for a fully-containerised deployment of this webapp.</span></span>

<span data-ttu-id="8f8e9-109">Aufgrund der Funktionsweise von Docker muss häufig nicht das gesamte 174 MB große Docker-Image erneut bereitgestellt werden, wenn der Quellcode der Anwendung geändert wird, da Docker lediglich die (deutlich kleineren) Unterschiede hochlädt.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-109">Because of the way Docker works, it is often the case that the entire 174 megabyte Docker image does not need to be redeployed whenever the application source code is changed, as Docker will only upload the differences (which is significantly smaller).</span></span> <span data-ttu-id="8f8e9-110">Der Prozess zum Ausführen einer neuen MicroProfile-Anwendungsversion über eine CI/CD-Pipeline wird so äußerst effizient und schnell. Darüber hinaus wird der Prozess dadurch reibungsloser und ermöglicht eine schnelle Entwicklungsiteration.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-110">This makes the process of executing a new release of a MicroProfile application via a CI/CD pipeline extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="8f8e9-111">In diesem Tutorial erstellen wir zunächst den Code und führen ihn lokal aus. Danach führen wir die Bereitstellung als Web-App in Azure durch.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-111">We will work through this tutorial firstly by creating and running the code locally, and then we will deploy this as a web app on Azure.</span></span> <span data-ttu-id="8f8e9-112">In beiden Fällen nutzen wir Docker zur Vereinfachung und Standardisierung.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-112">In both cases we will depend on Docker to simplify and standardize our efforts.</span></span> <span data-ttu-id="8f8e9-113">Bevor wir beginnen, erstellen wir eine Azure Container Registry-Instanz, in der wir unsere Docker-Container speichern können.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-113">Before we begin, we will create an Azure Container Registry to store our Docker containers in.</span></span>

## <a name="creating-an-azure-container-registry"></a><span data-ttu-id="8f8e9-114">Erstellen einer Azure Container Registry-Instanz</span><span class="sxs-lookup"><span data-stu-id="8f8e9-114">Creating an Azure Container Registry</span></span>

<span data-ttu-id="8f8e9-115">Wir erstellen die Azure Container Registry-Instanz über das [Azure-Portal](http://portal.azure.com). Für die Erstellung kann aber beispielsweise auch die Azure-Befehlszeilenschnittstelle verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-115">We will use the [Azure Portal](http://portal.azure.com) for creating the Azure Container Registry, but note that there are alternate choices such as the Azure CLI.</span></span> <span data-ttu-id="8f8e9-116">Führen Sie die folgenden Schritte aus, um eine neue Azure Container Registry-Instanz zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="8f8e9-116">Follow the steps below to create a new Azure Container Registry:</span></span>

1. <span data-ttu-id="8f8e9-117">Melden Sie sich beim [Azure-Portal](http://portal.azure.com) an, und erstellen Sie eine neue Azure Container Registry-Ressource.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-117">Log in to the [Azure Portal](http://portal.azure.com) and create a new Azure Container Registry resource.</span></span> <span data-ttu-id="8f8e9-118">Geben Sie einen Registrierungsnamen an. (Hinweis: Dieser Name muss als `docker.registry`-Eigenschaft in `pom.xml` festgelegt werden.)</span><span class="sxs-lookup"><span data-stu-id="8f8e9-118">Provide a registry name (note that this is the name that should be set as the `docker.registry` property in `pom.xml`).</span></span> <span data-ttu-id="8f8e9-119">Ändern Sie die Standardeinstellungen nach Belieben, und klicken Sie anschließend auf „Erstellen“.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-119">Change the defaults as you wish, and then click 'create'.</span></span>

1. <span data-ttu-id="8f8e9-120">Wenn die Containerregistrierung aktiv ist (ungefähr 30 Sekunden nach dem Klicken auf „Erstellen“), klicken Sie auf die Containerregistrierung und anschließend im linken Menübereich auf „Zugriffsschlüssel“.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-120">Once the container registry is live (which is about 30 seconds after clicking 'create'), click on the container registry, and click on the 'Access keys' link in the left-menu area.</span></span> <span data-ttu-id="8f8e9-121">Hier müssen Sie die Einstellung „Administratorbenutzer“ aktivieren, damit von unseren Computern aus auf diese Containerregistrierung zugegriffen werden kann (um Docker-Container per Push hinzuzufügen) und um den Zugriff über die Instanz von Azure-Web-App für Container zu ermöglichen, die wir in Kürze einrichten.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-121">In here, you need to enable the 'admin user' setting, so that this container registry can be accessed from our machines (to push docker containers into), and also to enable access from the Azure Web Apps for Containers instance we will setup soon.</span></span>

1. <span data-ttu-id="8f8e9-122">Notieren Sie sich die Werte `username` und `password`, während Sie sich im Bereich „Zugriffsschlüssel“ befinden.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-122">Whilst you are in the 'Access keys' area, note the `username` and `password` values.</span></span> <span data-ttu-id="8f8e9-123">Diese Werte fügen wir später in unsere globale Maven-Datei `settings.xml` ein. (Weitere Informationen zu Maven-Einstellungen finden Sie in auf der [Website des Apache Maven-Projekts](https://maven.apache.org/settings.html).)</span><span class="sxs-lookup"><span data-stu-id="8f8e9-123">We will copy / paste these into our global Maven `settings.xml` file  (for more information on Maven settings, refer to the [Apache Maven Project](https://maven.apache.org/settings.html) website).</span></span> <span data-ttu-id="8f8e9-124">Zu Referenzzwecken sehen Sie hier eine verschleierte Version der Datei `${user.home}/.m2/settings.xml` vom Erstellersystem:</span><span class="sxs-lookup"><span data-stu-id="8f8e9-124">For reference, here is an obfuscated version of the `${user.home}/.m2/settings.xml` file on the authors system:</span></span>

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

<span data-ttu-id="8f8e9-125">Kommen wir nun zum Erstellen und lokalen Ausführen der MicroProfile-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-125">Now that this is complete, we can move on with building and running our MicroProfile application locally.</span></span>

## <a name="creating-our-microprofile-application"></a><span data-ttu-id="8f8e9-126">Erstellen der MicroProfile-Anwendung</span><span class="sxs-lookup"><span data-stu-id="8f8e9-126">Creating our MicroProfile application</span></span>

<span data-ttu-id="8f8e9-127">Dieses Beispiel basiert auf einer auf GitHub verfügbaren Beispielanwendung, deren Code wir hier klonen und Schritt für Schritt durchgehen.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-127">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="8f8e9-128">Gehen Sie wie folgt vor, um den Code auf Ihrem Computer zu klonen:</span><span class="sxs-lookup"><span data-stu-id="8f8e9-128">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

<span data-ttu-id="8f8e9-129">In diesem Verzeichnis befindet sich eine Datei namens `pom.xml`, die dazu dient, das Projekt im vom Maven-Erstellungstool verwendeten Format anzugeben.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-129">In this directory there is a `pom.xml` file that is used to specify the project in the format used by the Maven build tool.</span></span> <span data-ttu-id="8f8e9-130">Diese Datei kann bearbeitet und an Ihre Anforderungen angepasst werden.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-130">This file can be edited to suit your own needs.</span></span> <span data-ttu-id="8f8e9-131">Insbesondere die Eigenschaften `docker.registry` und `docker.name` müssen auf die Werte von `docker.registry` und `docker.name` festgelegt werden, die beim Einrichten der Azure Container Registry-Instanz erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-131">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` created when the Azure Container Registry was setup.</span></span>

<span data-ttu-id="8f8e9-132">Eine andere wichtige Datei in diesem Verzeichnis ist die Dockerfile, die wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="8f8e9-132">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="8f8e9-133">Diese Dockerfile erstellt einfach einen neuen Docker-Container auf der Grundlage des Payara Micro-Docker-Containers und kopiert die WAR-Datei hinein, die im Rahmen unseres Buildprozesses erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-133">This Dockerfile simply creates a new Docker container based on the Payara Micro Docker Container, and copies in the .war file that is created as part of our build process.</span></span> <span data-ttu-id="8f8e9-134">Außerdem macht sie den Port 8080 verfügbar, damit wir auf den Dienst zugreifen können, wenn er innerhalb eines Docker-Containers ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-134">It also exposes port 8080 so that we may access the service once it is up and running within a Docker container.</span></span>

<span data-ttu-id="8f8e9-135">Im Verzeichnis `src` befindet sich unter anderem auch die Klasse `Application`:</span><span class="sxs-lookup"><span data-stu-id="8f8e9-135">Diving into the `src` directory, we will eventually discover the `Application` class reproduced below:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="8f8e9-136">Die Anmerkung `@ApplicationPath("/api")` gibt den Basisendpunkt für diesen Microservice an. Das bedeutet, dass bei allen Endpunkten dem restlichen Teil der URL, die für den Zugriff auf einen bestimmen REST-Endpunkt benötigt wird, `/api` vorangestellt wird.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-136">The `@ApplicationPath("/api")` annotation specifies the base endpoint for this microservice - that is, that all endpoints will have `/api` preceed the rest of the URL required to access any specific REST endpoint.</span></span>

<span data-ttu-id="8f8e9-137">Das Paket `api` enthält eine Klasse namens `API` mit folgendem Code:</span><span class="sxs-lookup"><span data-stu-id="8f8e9-137">Inside the `api` package is a class named `API`, which contains the following code:</span></span>

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

<span data-ttu-id="8f8e9-138">Die Anmerkung `@Path("/helloworld")` macht deutlich, dass dieser REST-Endpunkt in Kombination mit der Angabe von `/api` aus der Klasse `Application` wie folgt lautet: `/api/helloworld`.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-138">Through the use of the `@Path("/helloworld")` annotation, we can see that this REST endpoint, when combined with the `/api` specified in the `Application` class, will be `/api/helloworld`.</span></span> <span data-ttu-id="8f8e9-139">Wenn dieser Endpunkt mithilfe einer HTTP GET-Anforderung aufgerufen wird, wird durch die Methode Text/HTML (die hartcodierte Zeichenfolge „Hello, world!“) erzeugt.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-139">When this endpoint is called using an HTTP GET request, we can see that the method will produce text/html, and in fact it is simply a hard-coded string "Hello, world!".</span></span>

<span data-ttu-id="8f8e9-140">Damit kennen Sie den gesamten Code, der zum Erstellen eines Microservice mit MicroProfile benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-140">We have now covered all the code required to create a microservice using MicroProfile.</span></span> <span data-ttu-id="8f8e9-141">Wir können nun Maven verwenden, um ihn zu erstellen, in einen Docker-Container zu packen und lokal auszuführen.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-141">We can now use Maven to build it, containerize it into a Docker container, and run it locally.</span></span> <span data-ttu-id="8f8e9-142">Gehen Sie dazu wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="8f8e9-142">We can do that with the following steps:</span></span>

1. <span data-ttu-id="8f8e9-143">Führen Sie `mvn clean package` aus, und warten Sie, bis der Vorgang erfolgreich abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-143">Run `mvn clean package` and wait until it successfully completes.</span></span>

1. <span data-ttu-id="8f8e9-144">Führen Sie `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest` aus. (Beispiel: `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, wenn `docker.registry` auf `jogilescr.azurecr.io` und `docker.name` auf `samples/docker-helloworld` festgelegt ist.)</span><span class="sxs-lookup"><span data-stu-id="8f8e9-144">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, for example, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, if your `docker.registry` is `jogilescr.azurecr.io` and `docker.name` is `samples/docker-helloworld`.</span></span>

1. <span data-ttu-id="8f8e9-145">Greifen Sie in Ihrem Webbrowser auf [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) und [http://localhost:8080/health](http://localhost:8080/health) zu.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-145">Try accessing [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="8f8e9-146">Wenn Sie die erwartete Antwort „Hello, world!“</span><span class="sxs-lookup"><span data-stu-id="8f8e9-146">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="8f8e9-147">(und integritätsbezogene Informationen für den Endpunkt [/health](http://localhost:8080/health)) sehen, haben Sie die MicroProfile-Anwendung erfolgreich auf Ihrem lokalen Computer bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-147">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you have successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="pushing-to-the-azure-container-registry"></a><span data-ttu-id="8f8e9-148">Ausführen von Pushvorgängen an die Azure Container Registry-Instanz</span><span class="sxs-lookup"><span data-stu-id="8f8e9-148">Pushing to the Azure Container Registry</span></span>

<span data-ttu-id="8f8e9-149">Wir haben nun unsere MicroProfile-Anwendung erstellt und auf unserem lokalen Computer ausgeführt. Als Nächstes pushen wir den Container in unsere Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-149">Now that we have successfully built and run our MicroProfile application on our local machine, the next step is to push this container into our container registry.</span></span> <span data-ttu-id="8f8e9-150">In diesem Tutorial verwenden wir Azure Container Registry. Es kann aber auch eine beliebige andere Containerregistrierung verwendet werden (vorausgesetzt, die Datei `pom.xml` wird bearbeitet, um auf den entsprechenden Ort zu verweisen).</span><span class="sxs-lookup"><span data-stu-id="8f8e9-150">In this tutorial we are using the Azure Container Registry, but any container registry will work (as long as the `pom.xml` file is edited to point to the relevant location).</span></span>

1. <span data-ttu-id="8f8e9-151">Führen Sie `mvn clean package` aus, um ein lokales Docker-Image zu bereinigen, zu kompilieren und zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-151">Run `mvn clean package` to clean, compile, and create a local docker image.</span></span>
2. <span data-ttu-id="8f8e9-152">Führen Sie für die Übertragung an Azure Container Registry per Push `mvn dockerfile:push` aus.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-152">Run `mvn dockerfile:push` to push to the Azure Container Registry.</span></span>

<span data-ttu-id="8f8e9-153">Sie haben nun Ihr Docker-Containerimage in die Azure Container Registry-Instanz hochgeladen, es wird jedoch noch nicht ausgeführt, da es noch in einer Instanz von Azure-Web-App für Container bereitgestellt werden muss.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-153">At this stage you now have your docker container image uploaded to the Azure Container Registry, but it is not yet running as we now have to deploy it into an Azure Web App for Containers instance.</span></span> <span data-ttu-id="8f8e9-154">Diesen Schritt führen wir als Nächstes aus.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-154">We will now do that.</span></span>

## <a name="creating-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="8f8e9-155">Erstellen einer Instanz von Azure-Web-App für Container</span><span class="sxs-lookup"><span data-stu-id="8f8e9-155">Creating an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="8f8e9-156">Kehren Sie zum [Azure-Portal](http://portal.azure.com) zurück, und erstellen Sie eine neue Instanz von Web-App für Container (unter der Überschrift „Web + Mobil“ im Menü).</span><span class="sxs-lookup"><span data-stu-id="8f8e9-156">Return to the [Azure Portal](http://portal.azure.com) and create a new Web App for Containers instance (located under the 'Web + Mobile' heading in the menu).</span></span> <span data-ttu-id="8f8e9-157">Ein paar Hinweise:</span><span class="sxs-lookup"><span data-stu-id="8f8e9-157">A few pointers:</span></span>

   1. <span data-ttu-id="8f8e9-158">Der hier angegebene Name ist die öffentliche URL der Web-App (auch wenn später bei Bedarf eine benutzerdefinierte Domäne hinzugefügt werden kann). Es empfiehlt sich daher, einen leicht zu merkenden Namen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-158">The name you specify here will be the public URL of the web app (although a custom domain can be added later if desired), so it is a good idea to pick a name that you can easily remember.</span></span>

   1. <span data-ttu-id="8f8e9-159">Im Abschnitt „Container konfigurieren“ können Sie als Imagequelle „Azure Container Registry“ und anschließend das korrekte Image aus den Dropdownlisten auswählen.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-159">When you get to the 'Configure container' section, you can select 'Azure Container Registry' for the 'Image source', and then select the correct image from the drop-down lists.</span></span>

   1. <span data-ttu-id="8f8e9-160">Im Feld „Startdatei“ muss kein Wert angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-160">You do not need to specify any value in the 'Startup File' field.</span></span>

1. <span data-ttu-id="8f8e9-161">Warten Sie, bis die Instanz erstellt wurde (was nicht lange dauert), klicken Sie auf die Instanz, und klicken Sie anschließend auf das Menüelement „Anwendungseinstellungen“.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-161">Once the instance is created (again, it is very quick), click on it and then click on the 'Application Settings' menu item.</span></span> <span data-ttu-id="8f8e9-162">Hier müssen Sie eine neue Anwendungseinstellung mit dem Schlüssel `WEBSITES_PORT` und dem Wert `8080` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-162">In here you need to add a new application setting, where the key is `WEBSITES_PORT` and the value is `8080`.</span></span> <span data-ttu-id="8f8e9-163">So teilen Sie Azure mit, welchen Port Sie im Container verfügbar machen möchten, und er wird extern dem Port 80 zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-163">This tells Azure which port you want to expose in the container, and it will be mapped to port 80 externally.</span></span>

1. <span data-ttu-id="8f8e9-164">Klicken Sie optional auf den Link „Docker-Container“, und aktivieren Sie „Continuous Deployment“. Dadurch erfolgt nach jeder Aktualisierung des Azure Container Registry-Images automatisch eine Aktualisierung in der Instanz von Azure-Web-App für Container.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-164">Optionally, click on the 'Docker Container' link, and enable 'Continuous Deployment', so that whenever you update the Azure Container Registry image it is automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="8f8e9-165">Sie sollten auf die von Azure gehosteten Instanzen unter `http://<appname>.azurewebsites.net/microprofile/api/helloworld` und `http://<appname>.azurewebsites.net/health` zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-165">You should be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="8f8e9-166">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="8f8e9-166">Summary</span></span>

<span data-ttu-id="8f8e9-167">In diesem Tutorial sind wir Schritt für Schritt die Erstellung eines einfachen MicroProfile-basierten Microservice durchgegangen, haben ihn in einen Docker-Container gepackt und ihn lokal ausgeführt und in Azure veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="8f8e9-167">Through this tutorial we have stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, and we have run it locally and published it to Azure.</span></span> <span data-ttu-id="8f8e9-168">In diesem Tutorial wird nicht auf die Erweiterung des Microservice mit nützlicheren Funktionen eingegangen. Im Internet stehen jedoch zahlreiche MicroProfile-Tutorials und -Tipps zur Verfügung – unter anderem unter [MicroProfile.io](https://microprofile.io/).</span><span class="sxs-lookup"><span data-stu-id="8f8e9-168">Extending our microservice to provide more useful functionality is outside the scope of this tutorial, but there is a wealth of tutorials and advice on MicroProfile on the internet, and readers are encouraged to review [MicroProfile.io](https://microprofile.io/) for more content.</span></span>
