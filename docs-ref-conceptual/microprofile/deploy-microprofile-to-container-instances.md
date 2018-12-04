---
title: Bereitstellen einer MicroProfile-App in der Cloud mit Docker und Azure
description: Hier erfahren Sie, wie Sie eine MicroProfile-App unter Verwendung von Docker und Azure Container Instances in der Cloud bereitstellen.
services: container-instances;container-retistry
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
ms.openlocfilehash: 22870b7ba32f115e7270c63d1bf42cbfc6531d7e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338784"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a><span data-ttu-id="c91eb-103">Bereitstellen einer MicroProfile-Anwendung in der Cloud mit Docker und Azure</span><span class="sxs-lookup"><span data-stu-id="c91eb-103">Deploy a MicroProfile application to the cloud with Docker and Azure</span></span>

<span data-ttu-id="c91eb-104">In diesem Artikel wird gezeigt, wie Sie eine Anwendung vom Typ [MicroProfile.io] in einen Docker-Container packen und in Azure Container Instances ausführen.</span><span class="sxs-lookup"><span data-stu-id="c91eb-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c91eb-105">Dieses Verfahren kann für jede Implementierung von „MicroProfile.io“ verwendet werden, solange das Docker-Containerimage selbstausführbar ist (sprich: die Runtime enthält).</span><span class="sxs-lookup"><span data-stu-id="c91eb-105">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c91eb-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c91eb-106">Prerequisites</span></span>

<span data-ttu-id="c91eb-107">Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c91eb-107">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="c91eb-108">Ein Azure-Abonnement. Sollten Sie noch nicht über ein Azure-Abonnement verfügen, können Sie sich für ein [kostenloses Azure-Konto] registrieren.</span><span class="sxs-lookup"><span data-stu-id="c91eb-108">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c91eb-109">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="c91eb-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c91eb-110">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="c91eb-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c91eb-111">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c91eb-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c91eb-112">Das Erstellungstool [Maven] von Apache (ab Version 3)</span><span class="sxs-lookup"><span data-stu-id="c91eb-112">Apache's [Maven] build tool (version 3+).</span></span>
* <span data-ttu-id="c91eb-113">Einen [Git]</span><span class="sxs-lookup"><span data-stu-id="c91eb-113">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="c91eb-114">Beispiel „MicroProfile Hello Azure“</span><span class="sxs-lookup"><span data-stu-id="c91eb-114">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="c91eb-115">In diesem Artikel verwenden wir das Beispiel [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure):</span><span class="sxs-lookup"><span data-stu-id="c91eb-115">For this article, we will use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample:</span></span>

### <a name="clone-build-and-run-locally"></a><span data-ttu-id="c91eb-116">Klonen, Erstellen und lokales Ausführen</span><span class="sxs-lookup"><span data-stu-id="c91eb-116">Clone, build, and run locally</span></span>

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

<span data-ttu-id="c91eb-117">Sie können die Anwendung testen, indem Sie `curl` aufrufen oder sie über einen [Browser](http://localhost:8080/api/hello) öffnen:</span><span class="sxs-lookup"><span data-stu-id="c91eb-117">You can test the application by calling `curl` or visiting through a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a><span data-ttu-id="c91eb-118">Bereitstellen in Azure</span><span class="sxs-lookup"><span data-stu-id="c91eb-118">Deploy to Azure</span></span>

<span data-ttu-id="c91eb-119">Als Nächstes bringen wir die Anwendung mithilfe der Dienste [Azure Container Instances] und [Azure Container Registry] in die Cloud.</span><span class="sxs-lookup"><span data-stu-id="c91eb-119">Now let's bring this application to the cloud using [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="c91eb-120">Erstellen eines Docker-Images</span><span class="sxs-lookup"><span data-stu-id="c91eb-120">Build a Docker image</span></span>

<span data-ttu-id="c91eb-121">Das Beispielprojekt stellt bereits eine Dockerfile bereit, die Sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c91eb-121">The sample project already provides a Dockerfile you can use.</span></span> <span data-ttu-id="c91eb-122">Docker muss jedoch nicht installiert sein, da wir das Azure Container Registry Build-Feature verwenden, um das Image in der Cloud zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c91eb-122">You don't need Docker installed though, as we will use Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="c91eb-123">Führen Sie die folgenden Schritte aus, um das Image zu erstellen und für die Ausführung in Azure vorzubereiten:</span><span class="sxs-lookup"><span data-stu-id="c91eb-123">To build the image and be ready to run on Azure, you will have to follow these steps:</span></span>

1. <span data-ttu-id="c91eb-124">Installieren und Anmelden mit der Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="c91eb-124">Install and log in with Azure CLI</span></span>
1. <span data-ttu-id="c91eb-125">Erstellen einer Azure-Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="c91eb-125">Create an Azure Resource Group</span></span>
1. <span data-ttu-id="c91eb-126">Erstellen einer ACR-Instanz (Azure Container Registry)</span><span class="sxs-lookup"><span data-stu-id="c91eb-126">Create an Azure Container Registry (ACR)</span></span>
1. <span data-ttu-id="c91eb-127">Erstellen des Docker-Images</span><span class="sxs-lookup"><span data-stu-id="c91eb-127">Build the Docker image</span></span>
1. <span data-ttu-id="c91eb-128">Veröffentlichen des Docker-Images in der zuvor erstellten ACR-Instanz</span><span class="sxs-lookup"><span data-stu-id="c91eb-128">Publish the Docker image to the ACR created before</span></span>
1. <span data-ttu-id="c91eb-129">(Optional) Erstellen und Veröffentlichen in ACR mit nur einem Befehl</span><span class="sxs-lookup"><span data-stu-id="c91eb-129">(Optionally) Build and publish to ACR in one command</span></span>


#### <a name="set-up-azure-cli"></a><span data-ttu-id="c91eb-130">Einrichten der Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="c91eb-130">Set up Azure CLI</span></span>

<span data-ttu-id="c91eb-131">Stellen Sie sicher, dass Sie über ein Azure-Abonnement verfügen, dass die [Azure-Befehlszeilenschnittstelle installiert](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) ist und dass Sie bei Ihrem Konto authentifiziert sind:</span><span class="sxs-lookup"><span data-stu-id="c91eb-131">Make sure you have an Azure subscription, [Azure CLI installed](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you are authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="c91eb-132">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="c91eb-132">Create a Resource Group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="c91eb-133">Erstellen einer Azure Container Registry-Instanz</span><span class="sxs-lookup"><span data-stu-id="c91eb-133">Create an Azure Container Registry instance</span></span>

<span data-ttu-id="c91eb-134">Dieser Befehl erstellt eine (hoffentlich) global eindeutige Containerregistrierung mit einem einfachen Namen und einer Zufallszahl.</span><span class="sxs-lookup"><span data-stu-id="c91eb-134">This command will create a globally unique (hopefully) container registry using a basic name with a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="c91eb-135">Erstellen des Docker-Images</span><span class="sxs-lookup"><span data-stu-id="c91eb-135">Build the Docker image</span></span>

<span data-ttu-id="c91eb-136">Sie können das Docker-Image zwar ganz einfach mithilfe von Docker lokal erstellen, es gibt jedoch einige Gründe, die für eine Erstellung in der Cloud sprechen:</span><span class="sxs-lookup"><span data-stu-id="c91eb-136">While you can easily build the Docker image locally using Docker itself, you may want to consider building it in the Cloud for few reasons:</span></span>

1. <span data-ttu-id="c91eb-137">Keine lokale Docker-Installation erforderlich</span><span class="sxs-lookup"><span data-stu-id="c91eb-137">No need to install Docker locally</span></span>
1. <span data-ttu-id="c91eb-138">Viel schneller, da der Buildvorgang anderswo ausgeführt wird (mit Ausnahme der Uploadzeit für den Kontext)</span><span class="sxs-lookup"><span data-stu-id="c91eb-138">Much faster since build will happen elsewhere (except for context upload time)</span></span>
1. <span data-ttu-id="c91eb-139">Schnellere Downloads, da der Prozess in der Cloud Zugriff auf eine schnellere Internetverbindung hat</span><span class="sxs-lookup"><span data-stu-id="c91eb-139">Process in the Cloud has access to faster Internet, therefore faster downloads</span></span>
1. <span data-ttu-id="c91eb-140">Direktes Hinzufügen von Images zu Container Registry</span><span class="sxs-lookup"><span data-stu-id="c91eb-140">Image goes directly into the Container Registry</span></span>

<span data-ttu-id="c91eb-141">Aus diesen Gründen erstellen wir das Image mithilfe des Features [Azure Container Registry Build]:</span><span class="sxs-lookup"><span data-stu-id="c91eb-141">Because of these reasons, we will build the image using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a><span data-ttu-id="c91eb-142">Bereitstellen des Docker-Images über Azure Container Registry in Container Instances (ACI)</span><span class="sxs-lookup"><span data-stu-id="c91eb-142">Deploy Docker Image from Azure Container Registry (ACR) into Container Instances (ACI)</span></span>

<span data-ttu-id="c91eb-143">Das Image ist nun in Ihrer ACR-Instanz verfügbar ist. Als Nächstes übertragen wir eine Containerinstanz per Push an ACI und instanziieren sie.</span><span class="sxs-lookup"><span data-stu-id="c91eb-143">Now that the image is available on your ACR, let's push and instanciate a container instance on ACI.</span></span> <span data-ttu-id="c91eb-144">Zuvor müssen wir jedoch sicherstellen, dass die Authentifizierung in ACR möglich ist:</span><span class="sxs-lookup"><span data-stu-id="c91eb-144">But first, we need to make sure we can authenticate into the ACR:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="c91eb-145">Testen der bereitgestellten MicroProfile-Anwendung</span><span class="sxs-lookup"><span data-stu-id="c91eb-145">Test Your Deployed MicroProfile Application</span></span>

<span data-ttu-id="c91eb-146">Ihre Anwendung sollte nun betriebsbereit sein.</span><span class="sxs-lookup"><span data-stu-id="c91eb-146">Your application should now be up and running.</span></span> <span data-ttu-id="c91eb-147">Führen Sie an der Befehlszeile den folgenden Befehl aus, um sie zu testen:</span><span class="sxs-lookup"><span data-stu-id="c91eb-147">To test it from the command-line, try the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="c91eb-148">Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="c91eb-148">Congratulations!</span></span> <span data-ttu-id="c91eb-149">Sie haben erfolgreich eine MicroProfile-Anwendung erstellt und als Docker-Container in Microsoft Azure bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="c91eb-149">You have successfuly built and deployed a MicroProfile application as a Docker container onto Microsoft Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c91eb-150">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c91eb-150">Next steps</span></span>

<span data-ttu-id="c91eb-151">Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="c91eb-151">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* [<span data-ttu-id="c91eb-152">Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)</span><span class="sxs-lookup"><span data-stu-id="c91eb-152">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry