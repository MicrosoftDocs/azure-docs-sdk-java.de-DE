---
title: Bereitstellen einer Spring Boot-App unter Kubernetes in Azure Kubernetes Service
description: In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Microsoft Azure erläutert.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 42bb030a916cc5aaf1e20242518a0a400b8baa88
ms.sourcegitcommit: 3b10fe30dcc83e4c2e4c94d5b55e37ddbaa23c7a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2019
ms.locfileid: "59071009"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a><span data-ttu-id="15598-103">Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="15598-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Kubernetes Service</span></span>

<span data-ttu-id="15598-104">**[Kubernetes]** und **[Docker]** sind Open Source-Lösungen, mit denen Entwickler die Bereitstellung, Skalierung und Verwaltung ihrer in Containern ausgeführten Anwendungen automatisieren können.</span><span class="sxs-lookup"><span data-stu-id="15598-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications running in containers.</span></span>

<span data-ttu-id="15598-105">In diesem Tutorial wird die Kombination dieser beiden gängigen Open Source-Technologien zum Entwickeln und Bereitstellen einer Spring Boot-Anwendung in Microsoft Azure erläutert.</span><span class="sxs-lookup"><span data-stu-id="15598-105">This tutorial walks you through combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="15598-106">Genauer gesagt verwenden Sie *[Spring Boot]* für die Anwendungsentwicklung, *[Kubernetes]* für die Containerbereitstellung und [Azure Kubernetes Service (AKS)] zum Hosten der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="15598-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Kubernetes Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="15598-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="15598-107">Prerequisites</span></span>

* <span data-ttu-id="15598-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="15598-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="15598-109">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="15598-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="15598-110">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="15598-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="15598-111">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="15598-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="15598-112">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="15598-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="15598-113">Einen [Git-Client]</span><span class="sxs-lookup"><span data-stu-id="15598-113">A [Git] client.</span></span>
* <span data-ttu-id="15598-114">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="15598-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="15598-115">Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="15598-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="15598-116">Erstellen der Web-App für erste Schritte mit Spring Boot in Docker</span><span class="sxs-lookup"><span data-stu-id="15598-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="15598-117">Im Folgenden werden die Schritte zum Erstellen einer Spring Boot-Webanwendung und zum lokalen Testen dieser Anwendung beschrieben.</span><span class="sxs-lookup"><span data-stu-id="15598-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="15598-118">Öffnen Sie eine Eingabeaufforderung, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="15598-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="15598-119">– oder –</span><span class="sxs-lookup"><span data-stu-id="15598-119">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="15598-120">Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="15598-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="15598-121">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt.</span><span class="sxs-lookup"><span data-stu-id="15598-121">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="15598-122">Verwenden Sie Maven zum Erstellen und Ausführen der Beispiel-App.</span><span class="sxs-lookup"><span data-stu-id="15598-122">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="15598-123">Testen Sie die Web-App durch Navigieren zu `http://localhost:8080` oder mit dem folgenden `curl`-Befehl:</span><span class="sxs-lookup"><span data-stu-id="15598-123">Test the web app by browsing to `http://localhost:8080`, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="15598-124">Die folgende Meldung sollte angezeigt werden: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="15598-124">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Lokales Durchsuchen von Beispiel-Apps][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="15598-126">Erstellen einer Azure Container Registry-Instanz über die Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="15598-126">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="15598-127">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="15598-127">Open a command prompt.</span></span>

1. <span data-ttu-id="15598-128">Melden Sie sich bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="15598-128">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="15598-129">Wählen Sie Ihr Azure-Abonnement aus:</span><span class="sxs-lookup"><span data-stu-id="15598-129">Choose your Azure Subscription:</span></span>
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. <span data-ttu-id="15598-130">Erstellen Sie eine Ressourcengruppe für die in diesem Tutorial verwendeten Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="15598-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="15598-131">Erstellen Sie eine private Azure Container Registry-Instanz in der Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="15598-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="15598-132">Die Beispiel-App wird in diesem Tutorial in späteren Schritten als Docker-Image per Push in diese Registrierung übertragen.</span><span class="sxs-lookup"><span data-stu-id="15598-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="15598-133">Ersetzen Sie `wingtiptoysregistry` durch einen eindeutigen Namen für die Registrierung.</span><span class="sxs-lookup"><span data-stu-id="15598-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a><span data-ttu-id="15598-134">Pushen der App in die Containerregistrierung über Jib</span><span class="sxs-lookup"><span data-stu-id="15598-134">Push your app to the container registry via Jib</span></span>

1. <span data-ttu-id="15598-135">Melden Sie sich über die Azure-Befehlszeilenschnittstelle bei Ihrer Azure Container Registry-Instanz an.</span><span class="sxs-lookup"><span data-stu-id="15598-135">Log in to your Azure Container Registry from the Azure CLI.</span></span>
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. <span data-ttu-id="15598-136">Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung (z.B.„*C:\SpringBoot\gs-spring-boot-docker\complete*“ oder „*/users/robert/SpringBoot/gs-spring-boot-docker/complete*“), und öffnen Sie die Datei *pom.xml* mit einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="15598-136">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="15598-137">Aktualisieren Sie die Sammlung `<properties>` in der Datei *pom.xml* mit dem Registrierungsnamen für Ihre Azure Container Registry-Instanz und der aktuellen Version von [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="15598-137">Update the `<properties>` collection in the *pom.xml* file with the registry name for your Azure Container Registry and the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.0.2</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="15598-138">Aktualisieren Sie die Sammlung `<plugins>` in der Datei *pom.xml* so, dass `<plugin>` das Element `jib-maven-plugin` enthält.</span><span class="sxs-lookup"><span data-stu-id="15598-138">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the `jib-maven-plugin`.</span></span>

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>              
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>                
            <image>${docker.image.prefix}/${project.artifactId}</image>
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="15598-139">Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Befehl aus, um das Image zu erstellen und per Push in die Registrierung zu übertragen:</span><span class="sxs-lookup"><span data-stu-id="15598-139">Navigate to the completed project directory for your Spring Boot application and run the following command to build the image and push the image to the registry:</span></span>

   ```
   mvn compile jib:build
   ```

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="15598-140">Erstellen eines Kubernetes-Clusters in AKS über die Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="15598-140">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="15598-141">Erstellen Sie einen Kubernetes-Cluster in Azure Kubernetes Service.</span><span class="sxs-lookup"><span data-stu-id="15598-141">Create a Kubernetes cluster in Azure Kubernetes Service.</span></span> <span data-ttu-id="15598-142">Mit dem folgenden Befehl wird ein *Kubernetes*-Cluster in der Ressourcengruppe *wingtiptoys-kubernetes* mit *wingtiptoys-akscluster* als Clustername und *wingtiptoys-kubernetes* als DNS-Präfix erstellt:</span><span class="sxs-lookup"><span data-stu-id="15598-142">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-akscluster* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   <span data-ttu-id="15598-143">Die Ausführung des Befehls kann eine Weile dauern.</span><span class="sxs-lookup"><span data-stu-id="15598-143">This command may take a while to complete.</span></span>

1. <span data-ttu-id="15598-144">Wenn Sie Azure Container Registry (ACR) zusammen mit Azure Kubernetes Service (AKS) verwenden, müssen Sie Azure Kubernetes Service Pullzugriff auf Azure Container Registry gewähren.</span><span class="sxs-lookup"><span data-stu-id="15598-144">When you're using Azure Container Registry (ACR) with Azure Kubernetes Service (AKS), you need to grant Azure Kubernetes Service pull access to Azure Container Registry.</span></span> <span data-ttu-id="15598-145">Azure generiert beim Erstellen einer Azure Kubernetes Service-Instanz einen Standarddienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="15598-145">Azure creates a default service principal when you are creating Azure Kubernetes Service.</span></span> <span data-ttu-id="15598-146">Führen Sie die folgenden Skripts in Bash oder Powershell aus, um AKS Zugriff auf ACR zu gewähren. Ausführlichere Informationen finden Sie unter [Authentifizieren per Azure Container Registry über Azure Kubernetes Service].</span><span class="sxs-lookup"><span data-stu-id="15598-146">Please run the following scripts in bash or Powershell to grant AKS access to ACR, see more details at [Authenticate with Azure Container Registry from Azure Kubernetes Service].</span></span>

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  <span data-ttu-id="15598-147">– oder –</span><span class="sxs-lookup"><span data-stu-id="15598-147">-- or --</span></span>

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. <span data-ttu-id="15598-148">Installieren Sie `kubectl` über die Azure-Befehlszeilenschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="15598-148">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="15598-149">Linux-Benutzer müssen diesem Befehl möglicherweise das Präfix `sudo` voranstellen, da er die Kubernetes-Befehlszeilenschnittstelle in `/usr/local/bin` bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="15598-149">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az aks install-cli
   ```

1. <span data-ttu-id="15598-150">Laden Sie die Konfigurationsinformationen des Clusters herunter, damit Sie den Cluster über die Kubernetes-Weboberfläche und `kubectl` verwalten können.</span><span class="sxs-lookup"><span data-stu-id="15598-150">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="15598-151">Bereitstellen des Images in Ihrem Kubernetes-Cluster</span><span class="sxs-lookup"><span data-stu-id="15598-151">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="15598-152">In diesem Tutorial wird die App mit `kubectl` bereitgestellt, dann können Sie die Bereitstellung über die Kubernetes-Weboberfläche erkunden.</span><span class="sxs-lookup"><span data-stu-id="15598-152">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-kubectl"></a><span data-ttu-id="15598-153">Bereitstellen mit kubectl</span><span class="sxs-lookup"><span data-stu-id="15598-153">Deploy with kubectl</span></span>

1. <span data-ttu-id="15598-154">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="15598-154">Open a command prompt.</span></span>

1. <span data-ttu-id="15598-155">Führen Sie den Container im Kubernetes-Cluster mit dem Befehl `kubectl run` aus.</span><span class="sxs-lookup"><span data-stu-id="15598-155">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="15598-156">Geben Sie einen Dienstnamen für die App in Kubernetes und den vollständigen Imagenamen an.</span><span class="sxs-lookup"><span data-stu-id="15598-156">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="15598-157">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="15598-157">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="15598-158">In diesem Befehl:</span><span class="sxs-lookup"><span data-stu-id="15598-158">In this command:</span></span>

   * <span data-ttu-id="15598-159">Der Containername `gs-spring-boot-docker` wird direkt nach dem Befehl `run` angegeben.</span><span class="sxs-lookup"><span data-stu-id="15598-159">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="15598-160">Der Parameter `--image` gibt die Kombination aus Anmeldeserver und Imagename als `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest` an.</span><span class="sxs-lookup"><span data-stu-id="15598-160">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="15598-161">Machen Sie den Kubernetes-Cluster mit dem Befehl `kubectl expose` extern verfügbar.</span><span class="sxs-lookup"><span data-stu-id="15598-161">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="15598-162">Geben Sie den Dienstnamen, den öffentlichen TCP-Port für den Zugriff auf die App und den internen Zielport, auf dem die App lauscht, an.</span><span class="sxs-lookup"><span data-stu-id="15598-162">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="15598-163">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="15598-163">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="15598-164">In diesem Befehl:</span><span class="sxs-lookup"><span data-stu-id="15598-164">In this command:</span></span>

   * <span data-ttu-id="15598-165">Der Containername `gs-spring-boot-docker` wird direkt nach dem Befehl `expose deployment` angegeben.</span><span class="sxs-lookup"><span data-stu-id="15598-165">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="15598-166">Der Parameter `--type` gibt an, dass der Cluster einen Lastenausgleich verwendet.</span><span class="sxs-lookup"><span data-stu-id="15598-166">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="15598-167">Der Parameter `--port` gibt den öffentlichen TCP-Port 80 an.</span><span class="sxs-lookup"><span data-stu-id="15598-167">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="15598-168">Sie greifen über diesen Port auf die App zu.</span><span class="sxs-lookup"><span data-stu-id="15598-168">You access the app on this port.</span></span>

   * <span data-ttu-id="15598-169">Der Parameter `--target-port` gibt den internen TCP-Port 8080 an.</span><span class="sxs-lookup"><span data-stu-id="15598-169">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="15598-170">Der Load Balancer leitet über diesen Port Anforderungen an die App weiter.</span><span class="sxs-lookup"><span data-stu-id="15598-170">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="15598-171">Nachdem die App im Cluster bereitgestellt wurde, fragen Sie die externe IP-Adresse ab, und öffnen Sie sie im Webbrowser:</span><span class="sxs-lookup"><span data-stu-id="15598-171">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Navigieren zur Beispiel-App in Azure][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="15598-173">Bereitstellen über die Kubernetes-Weboberfläche</span><span class="sxs-lookup"><span data-stu-id="15598-173">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="15598-174">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="15598-174">Open a command prompt.</span></span>

1. <span data-ttu-id="15598-175">Öffnen Sie die Konfigurationswebsite für Ihren Kubernetes-Cluster im Standardbrowser:</span><span class="sxs-lookup"><span data-stu-id="15598-175">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. <span data-ttu-id="15598-176">Nachdem die Kubernetes-Konfigurationswebsite im Browser geöffnet wurde, klicken Sie auf den Link zum **Bereitstellen einer Container-App**:</span><span class="sxs-lookup"><span data-stu-id="15598-176">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Kubernetes-Konfigurationswebsite][KB01]

1. <span data-ttu-id="15598-178">Geben Sie auf der angezeigten Seite für die **Ressourcenerstellung** die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="15598-178">When the **Resource Creation** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="15598-179">a.</span><span class="sxs-lookup"><span data-stu-id="15598-179">a.</span></span> <span data-ttu-id="15598-180">Wählen Sie **APP ERSTELLEN** aus.</span><span class="sxs-lookup"><span data-stu-id="15598-180">Select **CREATE AN APP**.</span></span>

   <span data-ttu-id="15598-181">b.</span><span class="sxs-lookup"><span data-stu-id="15598-181">b.</span></span> <span data-ttu-id="15598-182">Geben Sie unter **App name** (App-Name) den Namen der Spring Boot-Anwendung ein, z.B. *gs-spring-boot-docker*.</span><span class="sxs-lookup"><span data-stu-id="15598-182">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="15598-183">c.</span><span class="sxs-lookup"><span data-stu-id="15598-183">c.</span></span> <span data-ttu-id="15598-184">Geben Sie unter **Container image** (Containerimage) die weiter oben verwendeten Werte für den Anmeldeserver und das Containerimage ein, z.B. *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*.</span><span class="sxs-lookup"><span data-stu-id="15598-184">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="15598-185">d.</span><span class="sxs-lookup"><span data-stu-id="15598-185">d.</span></span> <span data-ttu-id="15598-186">Wählen Sie **External** (Extern) für **Service** (Dienst) aus.</span><span class="sxs-lookup"><span data-stu-id="15598-186">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="15598-187">e.</span><span class="sxs-lookup"><span data-stu-id="15598-187">e.</span></span> <span data-ttu-id="15598-188">Geben Sie in den Textfeldern **Port** und **Target port** (Zielport) den externen und internen Port an.</span><span class="sxs-lookup"><span data-stu-id="15598-188">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes-Konfigurationswebsite][KB02]


1. <span data-ttu-id="15598-190">Klicken Sie auf **Deploy** (Bereitstellen), um den Container bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="15598-190">Click **Deploy** to deploy the container.</span></span>

   ![Kubernetes-Schaltfläche „Deploy“][KB05]

1. <span data-ttu-id="15598-192">Nach erfolgter Bereitstellung wird die Spring Boot-Anwendung unter **Services** (Dienste) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="15598-192">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes-Dienste][KB06]

1. <span data-ttu-id="15598-194">Wenn Sie auf den Link für **External endpoints** (Externe Endpunkte) klicken, können Sie die in Azure ausgeführte Spring Boot-Anwendung sehen.</span><span class="sxs-lookup"><span data-stu-id="15598-194">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes-Dienste][KB07]

   ![Navigieren zur Beispiel-App in Azure][SB02]

## <a name="next-steps"></a><span data-ttu-id="15598-197">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="15598-197">Next steps</span></span>

<span data-ttu-id="15598-198">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="15598-198">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="15598-199">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="15598-199">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="15598-200">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="15598-200">Additional Resources</span></span>

<span data-ttu-id="15598-201">Weitere Informationen zur Verwendung von Spring Boot in Azure finden Sie im folgenden Artikel:</span><span class="sxs-lookup"><span data-stu-id="15598-201">For more information about using Spring Boot on Azure, see the following article:</span></span>

* [<span data-ttu-id="15598-202">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="15598-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

<span data-ttu-id="15598-203">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="15598-203">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="15598-204">Weitere Informationen zum Bereitstellen einer Java-Anwendung in Kubernetes mit Visual Studio Code finden Sie in den [Visual Studio Code-Tutorials für Java].</span><span class="sxs-lookup"><span data-stu-id="15598-204">For more information about deploying a Java application to Kubernetes with Visual Studio Code, see [Visual Studio Code Java Tutorials].</span></span>

<span data-ttu-id="15598-205">Weitere Informationen zum Spring Boot-Beispielprojekt in Docker finden Sie unter [Spring Boot on Docker Getting Started] (Erste Schritte mit Spring Boot in Docker).</span><span class="sxs-lookup"><span data-stu-id="15598-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="15598-206">Über die folgenden Links erhalten Sie weitere Informationen zur Erstellung von Spring Boot-Anwendungen:</span><span class="sxs-lookup"><span data-stu-id="15598-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="15598-207">Weitere Informationen zum Erstellen einer einfachen Spring Boot-Anwendung finden Sie im Spring Initializr unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="15598-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="15598-208">Über die folgenden Links erhalten Sie weitere Informationen zur Verwendung von Kubernetes mit Azure:</span><span class="sxs-lookup"><span data-stu-id="15598-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="15598-209">Erste Schritte mit einem Kubernetes-Cluster in Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="15598-209">Get started with a Kubernetes cluster in Azure Kubernetes Service</span></span>](/azure/aks/intro-kubernetes)

<span data-ttu-id="15598-210">Weitere Informationen zur Verwendung der Kubernetes-Befehlszeilenschnittstelle stehen im Benutzerhandbuch für **kubectl** unter <https://kubernetes.io/docs/user-guide/kubectl/> zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="15598-210">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="15598-211">Die Kubernetes-Website umfasst mehrere Artikel zur Verwendung von Images in privaten Registrierungen:</span><span class="sxs-lookup"><span data-stu-id="15598-211">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="15598-212">[Configuring Service Accounts for Pods] (Konfigurieren von Dienstkonten für Pods)</span><span class="sxs-lookup"><span data-stu-id="15598-212">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="15598-213">[Namespaces]</span><span class="sxs-lookup"><span data-stu-id="15598-213">[Namespaces]</span></span>
* <span data-ttu-id="15598-214">[Pulling an Image from a Private Registry] (Übertragen eines Images aus einer privaten Registrierung per Pull)</span><span class="sxs-lookup"><span data-stu-id="15598-214">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="15598-215">Weitere Beispiele zur Vorgehensweise bei der Verwendung benutzerdefinierter Docker-Images mit Azure finden Sie unter [Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux].</span><span class="sxs-lookup"><span data-stu-id="15598-215">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<span data-ttu-id="15598-216">Weitere Informationen zum iterativen Ausführen und Debuggen von Containern mit Azure Dev Spaces direkt in Azure Kubernetes Service (AKS) finden Sie unter [Erste Schritte in Azure Dev Spaces mit Java].</span><span class="sxs-lookup"><span data-stu-id="15598-216">For more information about iteratively running and debugging containers directly in Azure Kubernetes Service (AKS) with Azure Dev Spaces, see [Get started on Azure Dev Spaces with Java]</span></span>

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure für Java-Entwickler]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Arbeiten mit Azure DevOps und Java)
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Konfigurieren von Dienstkonten für Pods)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Übertragen eines Images aus einer privaten Registrierung per Pull)

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[Authentifizieren per Azure Container Registry über Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Authenticate with Azure Container Registry from Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Visual Studio Code-Tutorials für Java]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Visual Studio Code Java Tutorials]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Erste Schritte in Azure Dev Spaces mit Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
[Get started on Azure Dev Spaces with Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
