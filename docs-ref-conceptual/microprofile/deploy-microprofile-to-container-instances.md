---
title: Bereitstellen einer MicroProfile-App in der Cloud über Docker und Azure
description: Hier erfahren Sie, wie Sie eine MicroProfile-App in der Cloud bereitstellen, indem Sie Docker und Azure Container Instances verwenden.
services: container-instances;container-registry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533602"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a><span data-ttu-id="743d0-103">Bereitstellen einer MicroProfile-App in der Cloud über Docker und Azure</span><span class="sxs-lookup"><span data-stu-id="743d0-103">Deploy a MicroProfile app to the cloud by using Docker and Azure</span></span>

<span data-ttu-id="743d0-104">In diesem Artikel wird gezeigt, wie Sie eine Anwendung vom Typ [MicroProfile.io] in einen Docker-Container packen und in Azure Container Instances ausführen.</span><span class="sxs-lookup"><span data-stu-id="743d0-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
> <span data-ttu-id="743d0-105">Dieses Verfahren kann für jede Implementierung von „MicroProfile.io“ verwendet werden, solange das Docker-Containerimage selbstausführbar ist (d. h., das Image enthält die Runtime).</span><span class="sxs-lookup"><span data-stu-id="743d0-105">This procedure works with any implementation of MicroProfile.io, as long as the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="743d0-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="743d0-106">Prerequisites</span></span>

<span data-ttu-id="743d0-107">Zum Durchführen dieses Tutorials benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="743d0-107">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="743d0-108">Ein Azure-Abonnement.</span><span class="sxs-lookup"><span data-stu-id="743d0-108">An Azure subscription.</span></span> <span data-ttu-id="743d0-109">Wenn Sie noch kein Azure-Abonnement haben, können Sie sich für ein [kostenloses Azure-Konto] anmelden.</span><span class="sxs-lookup"><span data-stu-id="743d0-109">If you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="743d0-110">Die [Azure-Befehlszeilenschnittstelle] muss installiert sein.</span><span class="sxs-lookup"><span data-stu-id="743d0-110">The [Azure CLI], installed.</span></span>
* <span data-ttu-id="743d0-111">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="743d0-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="743d0-112">Weitere Informationen zu den JDKs, die verfügbar sind, wenn Sie in Azure entwickeln, finden Sie unter [Langfristiger Java-Support für Azure und Azure Stack](https://aka.ms/azure-jdks).</span><span class="sxs-lookup"><span data-stu-id="743d0-112">For more information about the JDKs that are available to use when you develop on Azure, see [Java long-term support for Azure and Azure Stack](https://aka.ms/azure-jdks).</span></span>
* <span data-ttu-id="743d0-113">Das [Apache Maven]-Buildtool (Version 3 oder höher).</span><span class="sxs-lookup"><span data-stu-id="743d0-113">The [Apache Maven] build tool (version 3 or later).</span></span>
* <span data-ttu-id="743d0-114">Einen [Git-Client]</span><span class="sxs-lookup"><span data-stu-id="743d0-114">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="743d0-115">Beispiel „MicroProfile Hello Azure“</span><span class="sxs-lookup"><span data-stu-id="743d0-115">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="743d0-116">In diesem Artikel verwenden Sie das Beispiel [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="743d0-116">In this article, you use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample.</span></span> <span data-ttu-id="743d0-117">Verwenden Sie die folgenden Befehle, um das Beispiel lokal zu klonen, zu erstellen und auszuführen:</span><span class="sxs-lookup"><span data-stu-id="743d0-117">Clone, build, and run it locally by using the following commands:</span></span>

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

<span data-ttu-id="743d0-118">Sie können die Anwendung testen, indem Sie `curl` aufrufen oder einen [Browser](http://localhost:8080/api/hello) verwenden:</span><span class="sxs-lookup"><span data-stu-id="743d0-118">You can test the application by calling `curl` or by using a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="743d0-119">Bereitstellen der Anwendung in Azure</span><span class="sxs-lookup"><span data-stu-id="743d0-119">Deploy the app to Azure</span></span>

<span data-ttu-id="743d0-120">Platzieren Sie die Anwendung nun in Azure, indem Sie die Dienste [Azure Container Instances] und [Azure Container Registry] verwenden.</span><span class="sxs-lookup"><span data-stu-id="743d0-120">Now bring this application to Azure by using the [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="743d0-121">Erstellen eines Docker-Images</span><span class="sxs-lookup"><span data-stu-id="743d0-121">Build a Docker image</span></span>

<span data-ttu-id="743d0-122">Das Beispielprojekt stellt ein Dockerfile bereit, das Sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="743d0-122">The sample project provides a Dockerfile that you can use.</span></span> <span data-ttu-id="743d0-123">Docker muss jedoch nicht installiert sein, weil Sie das Azure Container Registry Build-Feature verwenden, um das Image in der Cloud zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="743d0-123">You don't need to have Docker installed, though, because you'll use the Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="743d0-124">Gehen Sie wie folgt vor, um das Image zu erstellen und so vorzubereiten, dass es in Azure ausgeführt werden kann:</span><span class="sxs-lookup"><span data-stu-id="743d0-124">To build the image and prepare to run it on Azure, do the following:</span></span>

1. <span data-ttu-id="743d0-125">Installieren Sie die Azure CLI, und melden Sie sich bei der Azure CLI an.</span><span class="sxs-lookup"><span data-stu-id="743d0-125">Install and sign in to the Azure CLI.</span></span>
1. <span data-ttu-id="743d0-126">Erstellen einer Azure-Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="743d0-126">Create an Azure resource group.</span></span>
1. <span data-ttu-id="743d0-127">Erstellen Sie eine Azure Container Registry-Instanz.</span><span class="sxs-lookup"><span data-stu-id="743d0-127">Create an Azure container registry instance.</span></span>
1. <span data-ttu-id="743d0-128">Erstellen Sie ein Docker-Image.</span><span class="sxs-lookup"><span data-stu-id="743d0-128">Build a Docker image.</span></span>
1. <span data-ttu-id="743d0-129">Veröffentlichen Sie das Docker-Image in der zuvor erstellten Container Registry-Instanz.</span><span class="sxs-lookup"><span data-stu-id="743d0-129">Publish the Docker image to the previously created container registry instance.</span></span>
1. <span data-ttu-id="743d0-130">(Optional) Erstellen und veröffentlichen Sie das Image in der Container-Registry-Instanz in einem einzigen Befehl.</span><span class="sxs-lookup"><span data-stu-id="743d0-130">(Optional) Build and publish the image to the container registry instance in one command.</span></span>


#### <a name="set-up-the-azure-cli"></a><span data-ttu-id="743d0-131">Einrichten der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="743d0-131">Set up the Azure CLI</span></span>

<span data-ttu-id="743d0-132">Stellen Sie sicher, dass Sie ein Azure-Abonnement haben, dass Sie [die Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) installiert haben und dass Sie bei Ihrem Konto authentifiziert sind:</span><span class="sxs-lookup"><span data-stu-id="743d0-132">Make sure that you have an Azure subscription, that you've installed [the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you're authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="743d0-133">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="743d0-133">Create a resource group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a><span data-ttu-id="743d0-134">Erstellen einer Container Registry-Instanz</span><span class="sxs-lookup"><span data-stu-id="743d0-134">Create a container registry instance</span></span>

<span data-ttu-id="743d0-135">Dieser Befehl sollte eine global eindeutige Container Registry-Instanz mit einem Basisnamen und einer Zufallszahl erstellen.</span><span class="sxs-lookup"><span data-stu-id="743d0-135">This command should create a globally unique container registry instance with a basic name and a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="743d0-136">Erstellen des Docker-Images</span><span class="sxs-lookup"><span data-stu-id="743d0-136">Build the Docker image</span></span>

<span data-ttu-id="743d0-137">Obwohl Sie das Docker-Image ganz einfach lokal erstellen können, indem Sie Docker selbst verwenden, gibt es einige Gründe, die für eine Erstellung des Images in der Cloud sprechen:</span><span class="sxs-lookup"><span data-stu-id="743d0-137">Although you can easily build the Docker image locally by using Docker itself, you might consider building it in the cloud for few reasons:</span></span>

* <span data-ttu-id="743d0-138">Sie müssen Docker nicht lokal installieren.</span><span class="sxs-lookup"><span data-stu-id="743d0-138">You don't have to install Docker locally.</span></span>
* <span data-ttu-id="743d0-139">Es ist viel schneller, weil der Buildvorgang anderswo ausgeführt wird (mit Ausnahme der Uploadzeit für den Kontext).</span><span class="sxs-lookup"><span data-stu-id="743d0-139">It's much faster, because the build happens elsewhere (except for context upload time).</span></span>
* <span data-ttu-id="743d0-140">Der Prozess in der Cloud hat schnelleren Zugriff auf das Internet und somit schnellere Downloads.</span><span class="sxs-lookup"><span data-stu-id="743d0-140">The process in the cloud has faster access to the internet and, therefore, faster downloads.</span></span>
* <span data-ttu-id="743d0-141">Das Image wird direkt in der Container Registry-Instanz hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="743d0-141">The image goes directly into the container registry instance.</span></span>

<span data-ttu-id="743d0-142">Aus diesen Gründen erstellen Sie das Image über das Feature [Azure Container Registry Build]:</span><span class="sxs-lookup"><span data-stu-id="743d0-142">For these reasons, you build the image by using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a><span data-ttu-id="743d0-143">Bereitstellen des Docker-Images aus der Azure Container Registry-Instanz in Container Instances</span><span class="sxs-lookup"><span data-stu-id="743d0-143">Deploy the Docker image from the Azure container registry instance to Container Instances</span></span>

<span data-ttu-id="743d0-144">Nachdem das Image nun in Ihrer Container-Registry-Instanz verfügbar ist, senden Sie eine Containerinstanz an Container Instances, und instanziieren Sie die Instanz dort.</span><span class="sxs-lookup"><span data-stu-id="743d0-144">Now that the image is available on your container registry instance, push and instantiate a container instance on Container Instances.</span></span> <span data-ttu-id="743d0-145">Zunächst müssen Sie aber sicherstellen, dass Sie sich für die Container Registry-Instanz authentifizieren können:</span><span class="sxs-lookup"><span data-stu-id="743d0-145">But first, make sure that you can authenticate into the container registry instance:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="743d0-146">Testen Ihrer bereitgestellten MicroProfile-Anwendung</span><span class="sxs-lookup"><span data-stu-id="743d0-146">Test your deployed MicroProfile application</span></span>

<span data-ttu-id="743d0-147">Ihre Anwendung sollte nun betriebsbereit sein.</span><span class="sxs-lookup"><span data-stu-id="743d0-147">Your application should now be up and running.</span></span> <span data-ttu-id="743d0-148">Um sie aus der Befehlszeilenschnittstelle zu testen, verwenden Sie den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="743d0-148">To test it from the command-line interface, use the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="743d0-149">Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="743d0-149">Congratulations!</span></span> <span data-ttu-id="743d0-150">Sie haben erfolgreich eine MicroProfile-Anwendung als Docker-Container erstellt und in Azure bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="743d0-150">You've successfully built a MicroProfile application as a Docker container and deployed it to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="743d0-151">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="743d0-151">Next steps</span></span>

<span data-ttu-id="743d0-152">Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="743d0-152">For more information about the various technologies discussed in this article, see:</span></span>

* [<span data-ttu-id="743d0-153">Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)</span><span class="sxs-lookup"><span data-stu-id="743d0-153">Sign in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure-Befehlszeilenschnittstelle]: /cli/azure/overview
[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
