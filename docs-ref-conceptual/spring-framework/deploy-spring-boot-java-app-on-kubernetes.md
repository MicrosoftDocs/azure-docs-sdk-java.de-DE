---
title: Bereitstellen einer Spring Boot-App unter Kubernetes in Azure Container Service
description: "In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Microsoft Azure erläutert."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: ee8d5fecc31df427645c1552e27996592eaf27af
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="58e9d-103">Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="58e9d-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="58e9d-104">**[Kubernetes]** und **[Docker]** sind Open-Source-Lösungen, mit denen Entwickler die Bereitstellung, Skalierung und Verwaltung ihrer in Containern ausgeführten Anwendungen automatisieren können.</span><span class="sxs-lookup"><span data-stu-id="58e9d-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="58e9d-105">In diesem Tutorial wird die Kombination dieser beiden gängigen Open-Source-Technologien zum Entwickeln und Bereitstellen einer Spring Boot-Anwendung in Microsoft Azure erläutert.</span><span class="sxs-lookup"><span data-stu-id="58e9d-105">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="58e9d-106">Genauer gesagt verwenden Sie *[Spring Boot]* für die Anwendungsentwicklung, *[Kubernetes]* für die Containerbereitstellung und [Azure Container Service (AKS)] zum Hosten der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="58e9d-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="58e9d-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="58e9d-107">Prerequisites</span></span>

* <span data-ttu-id="58e9d-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="58e9d-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="58e9d-109">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="58e9d-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="58e9d-110">Ein aktuelles [Java Developer Kit (JDK)]</span><span class="sxs-lookup"><span data-stu-id="58e9d-110">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="58e9d-111">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="58e9d-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="58e9d-112">Einen [Git-Client]</span><span class="sxs-lookup"><span data-stu-id="58e9d-112">A [Git] client.</span></span>
* <span data-ttu-id="58e9d-113">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="58e9d-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="58e9d-114">Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="58e9d-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="58e9d-115">Erstellen der Web-App für erste Schritte mit Spring Boot in Docker</span><span class="sxs-lookup"><span data-stu-id="58e9d-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="58e9d-116">Im Folgenden werden die Schritte zum Erstellen einer Spring Boot-Webanwendung und zum lokalen Testen dieser Anwendung beschrieben.</span><span class="sxs-lookup"><span data-stu-id="58e9d-116">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="58e9d-117">Öffnen Sie eine Eingabeaufforderung, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="58e9d-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="58e9d-118">– oder –</span><span class="sxs-lookup"><span data-stu-id="58e9d-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="58e9d-119">Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="58e9d-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="58e9d-120">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt.</span><span class="sxs-lookup"><span data-stu-id="58e9d-120">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="58e9d-121">Verwenden Sie Maven zum Erstellen und Ausführen der Beispiel-App.</span><span class="sxs-lookup"><span data-stu-id="58e9d-121">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="58e9d-122">Testen Sie die Web-App durch Navigieren zu http://localhost:8080 oder mit dem folgenden `curl`-Befehl:</span><span class="sxs-lookup"><span data-stu-id="58e9d-122">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="58e9d-123">Es sollte die folgende Meldung angezeigt werden: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="58e9d-123">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Lokales Navigieren zur Beispiel-App][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="58e9d-125">Erstellen einer Azure Container Registry-Instanz über die Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="58e9d-125">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="58e9d-126">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="58e9d-126">Open a command prompt.</span></span>

1. <span data-ttu-id="58e9d-127">Melden Sie sich bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="58e9d-127">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="58e9d-128">Erstellen Sie eine Ressourcengruppe für die in diesem Tutorial verwendeten Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="58e9d-128">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="58e9d-129">Erstellen Sie eine private Azure Container Registry-Instanz in der Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="58e9d-129">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="58e9d-130">Die Beispiel-App wird in diesem Tutorial in späteren Schritten als Docker-Image per Push in diese Registrierung übertragen.</span><span class="sxs-lookup"><span data-stu-id="58e9d-130">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="58e9d-131">Ersetzen Sie `wingtiptoysregistry` durch einen eindeutigen Namen für die Registrierung.</span><span class="sxs-lookup"><span data-stu-id="58e9d-131">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="58e9d-132">Übertragen der App in die Containerregistrierung per Push</span><span class="sxs-lookup"><span data-stu-id="58e9d-132">Push your app to the container registry</span></span>

1. <span data-ttu-id="58e9d-133">Navigieren Sie zu dem Konfigurationsverzeichnis Ihrer Maven-Installation (Standard: „~/.m2/“ oder „C:\Users\username\.m2“), und öffnen Sie die Datei *settings.xml* mit einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="58e9d-133">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="58e9d-134">Rufen Sie das Kennwort für Ihre Containerregistrierung über die Azure-Befehlszeilenschnittstelle ab.</span><span class="sxs-lookup"><span data-stu-id="58e9d-134">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="58e9d-135">Fügen Sie die ID und das Kennwort für Azure Container Registry einer neuen `<server>`-Sammlung in der Datei *Settings.xml* hinzu.</span><span class="sxs-lookup"><span data-stu-id="58e9d-135">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="58e9d-136">`id` und `username` bilden den Namen der Registrierung.</span><span class="sxs-lookup"><span data-stu-id="58e9d-136">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="58e9d-137">Verwenden Sie den `password`-Wert des vorherigen Befehls (ohne Anführungszeichen).</span><span class="sxs-lookup"><span data-stu-id="58e9d-137">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="58e9d-138">Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung (z.B.„*C:\SpringBoot\gs-spring-boot-docker\complete*“ oder „*/users/robert/SpringBoot/gs-spring-boot-docker/complete*“), und öffnen Sie die Datei *pom.xml* mit einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="58e9d-138">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="58e9d-139">Aktualisieren Sie die `<properties>`-Sammlung in der Datei *pom.xml* mit dem Wert des Anmeldeservers für Ihre Azure Container Registry-Instanz.</span><span class="sxs-lookup"><span data-stu-id="58e9d-139">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="58e9d-140">Aktualisieren Sie die `<plugins>`-Sammlung in der Datei *pom.xml* so, dass `<plugin>` die Adresse des Anmeldeservers und den Registrierungsnamen für Ihre Azure Container Registry-Instanz enthält.</span><span class="sxs-lookup"><span data-stu-id="58e9d-140">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="58e9d-141">Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Befehl aus, um den Docker-Container zu erstellen und das Image per Push in die Registrierung zu übertragen:</span><span class="sxs-lookup"><span data-stu-id="58e9d-141">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="58e9d-142">Möglicherweise wird eine Fehlermeldung ähnlich einer der folgenden Meldungen angezeigt, wenn Maven das Image per Push in Azure überträgt:</span><span class="sxs-lookup"><span data-stu-id="58e9d-142">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="58e9d-143">Wenn dieser Fehler angezeigt wird, melden Sie sich über die Docker-Befehlszeile bei Azure an.</span><span class="sxs-lookup"><span data-stu-id="58e9d-143">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="58e9d-144">Übertragen Sie dann den Container per Push:</span><span class="sxs-lookup"><span data-stu-id="58e9d-144">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="58e9d-145">Erstellen eines Kubernetes-Clusters in AKS über die Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="58e9d-145">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="58e9d-146">Erstellen Sie einen Kubernetes-Cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="58e9d-146">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="58e9d-147">Mit dem folgenden Befehl wird ein *Kubernetes*-Cluster in der Ressourcengruppe *wingtiptoys-kubernetes* mit *wingtiptoys-containerservice* als Clustername und *wingtiptoys-kubernetes* als DNS-Präfix erstellt:</span><span class="sxs-lookup"><span data-stu-id="58e9d-147">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="58e9d-148">Die Ausführung des Befehls kann eine Weile dauern.</span><span class="sxs-lookup"><span data-stu-id="58e9d-148">This command may take a while to complete.</span></span>

1. <span data-ttu-id="58e9d-149">Installieren Sie `kubectl` über die Azure-Befehlszeilenschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="58e9d-149">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="58e9d-150">Linux-Benutzer müssen diesem Befehl möglicherweise das Präfix `sudo` voranstellen, da er die Kubernetes-Befehlszeilenschnittstelle in `/usr/local/bin` bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="58e9d-150">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="58e9d-151">Laden Sie die Konfigurationsinformationen des Clusters herunter, damit Sie den Cluster über die Kubernetes-Weboberfläche und `kubectl` verwalten können.</span><span class="sxs-lookup"><span data-stu-id="58e9d-151">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="58e9d-152">Bereitstellen des Images in Ihrem Kubernetes-Cluster</span><span class="sxs-lookup"><span data-stu-id="58e9d-152">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="58e9d-153">In diesem Tutorial wird die App mit `kubectl` bereitgestellt, dann können Sie die Bereitstellung über die Kubernetes-Weboberfläche erkunden.</span><span class="sxs-lookup"><span data-stu-id="58e9d-153">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="58e9d-154">Bereitstellen über die Kubernetes-Weboberfläche</span><span class="sxs-lookup"><span data-stu-id="58e9d-154">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="58e9d-155">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="58e9d-155">Open a command prompt.</span></span>

1. <span data-ttu-id="58e9d-156">Öffnen Sie die Konfigurationswebsite für Ihren Kubernetes-Cluster im Standardbrowser:</span><span class="sxs-lookup"><span data-stu-id="58e9d-156">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="58e9d-157">Nachdem die Kubernetes-Konfigurationswebsite im Browser geöffnet wurde, klicken Sie auf den Link zum **Bereitstellen einer Container-App**:</span><span class="sxs-lookup"><span data-stu-id="58e9d-157">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Kubernetes-Konfigurationswebsite][KB01]

1. <span data-ttu-id="58e9d-159">Geben Sie auf der angezeigten Seite **Deploy a Containerized App** (Container-App bereitstellen) die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="58e9d-159">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="58e9d-160">a.</span><span class="sxs-lookup"><span data-stu-id="58e9d-160">a.</span></span> <span data-ttu-id="58e9d-161">Wählen Sie **Specify app details below** (App-Details unten angeben) aus.</span><span class="sxs-lookup"><span data-stu-id="58e9d-161">Select **Specify app details below**.</span></span>

   <span data-ttu-id="58e9d-162">b.</span><span class="sxs-lookup"><span data-stu-id="58e9d-162">b.</span></span> <span data-ttu-id="58e9d-163">Geben Sie unter **App name** (App-Name) den Namen der Spring Boot-Anwendung ein, z.B. *gs-spring-boot-docker*.</span><span class="sxs-lookup"><span data-stu-id="58e9d-163">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="58e9d-164">c.</span><span class="sxs-lookup"><span data-stu-id="58e9d-164">c.</span></span> <span data-ttu-id="58e9d-165">Geben Sie unter **Container image** (Containerimage) die weiter oben verwendeten Werte für den Anmeldeserver und das Containerimage ein, z.B. *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*.</span><span class="sxs-lookup"><span data-stu-id="58e9d-165">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="58e9d-166">d.</span><span class="sxs-lookup"><span data-stu-id="58e9d-166">d.</span></span> <span data-ttu-id="58e9d-167">Wählen Sie **External** (Extern) für **Service** (Dienst) aus.</span><span class="sxs-lookup"><span data-stu-id="58e9d-167">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="58e9d-168">e.</span><span class="sxs-lookup"><span data-stu-id="58e9d-168">e.</span></span> <span data-ttu-id="58e9d-169">Geben Sie in den Textfeldern **Port** und **Target port** (Zielport) den externen und internen Port an.</span><span class="sxs-lookup"><span data-stu-id="58e9d-169">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes-Konfigurationswebsite][KB02]


1. <span data-ttu-id="58e9d-171">Klicken Sie auf **Deploy** (Bereitstellen), um den Container bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="58e9d-171">Click **Deploy** to deploy the container.</span></span>

   ![Bereitstellen des Containers][KB05]

1. <span data-ttu-id="58e9d-173">Nach erfolgter Bereitstellung wird die Spring Boot-Anwendung unter **Services** (Dienste) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="58e9d-173">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes-Dienste][KB06]

1. <span data-ttu-id="58e9d-175">Wenn Sie auf den Link für **External endpoints** (Externe Endpunkte) klicken, können Sie die in Azure ausgeführte Spring Boot-Anwendung sehen.</span><span class="sxs-lookup"><span data-stu-id="58e9d-175">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes-Dienste][KB07]

   ![Navigieren zur Beispiel-App in Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="58e9d-178">Bereitstellen mit kubectl</span><span class="sxs-lookup"><span data-stu-id="58e9d-178">Deploy with kubectl</span></span>

1. <span data-ttu-id="58e9d-179">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="58e9d-179">Open a command prompt.</span></span>

1. <span data-ttu-id="58e9d-180">Führen Sie den Container im Kubernetes-Cluster mit dem Befehl `kubectl run` aus.</span><span class="sxs-lookup"><span data-stu-id="58e9d-180">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="58e9d-181">Geben Sie einen Dienstnamen für die App in Kubernetes und den vollständigen Imagenamen an.</span><span class="sxs-lookup"><span data-stu-id="58e9d-181">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="58e9d-182">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="58e9d-182">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="58e9d-183">In diesem Befehl:</span><span class="sxs-lookup"><span data-stu-id="58e9d-183">In this command:</span></span>

   * <span data-ttu-id="58e9d-184">Der Containername `gs-spring-boot-docker` wird direkt nach dem Befehl `run` angegeben.</span><span class="sxs-lookup"><span data-stu-id="58e9d-184">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="58e9d-185">Der Parameter `--image` gibt die Kombination aus Anmeldeserver und Imagename als `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest` an.</span><span class="sxs-lookup"><span data-stu-id="58e9d-185">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="58e9d-186">Machen Sie den Kubernetes-Cluster mit dem Befehl `kubectl expose` extern verfügbar.</span><span class="sxs-lookup"><span data-stu-id="58e9d-186">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="58e9d-187">Geben Sie den Dienstnamen, den öffentlichen TCP-Port für den Zugriff auf die App und den internen Zielport, auf dem die App lauscht, an.</span><span class="sxs-lookup"><span data-stu-id="58e9d-187">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="58e9d-188">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="58e9d-188">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="58e9d-189">In diesem Befehl:</span><span class="sxs-lookup"><span data-stu-id="58e9d-189">In this command:</span></span>

   * <span data-ttu-id="58e9d-190">Der Containername `gs-spring-boot-docker` wird direkt nach dem Befehl `expose deployment` angegeben.</span><span class="sxs-lookup"><span data-stu-id="58e9d-190">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="58e9d-191">Der Parameter `--type` gibt an, dass der Cluster einen Lastenausgleich verwendet.</span><span class="sxs-lookup"><span data-stu-id="58e9d-191">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="58e9d-192">Der Parameter `--port` gibt den öffentlichen TCP-Port 80 an.</span><span class="sxs-lookup"><span data-stu-id="58e9d-192">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="58e9d-193">Sie greifen über diesen Port auf die App zu.</span><span class="sxs-lookup"><span data-stu-id="58e9d-193">You access the app on this port.</span></span>

   * <span data-ttu-id="58e9d-194">Der Parameter `--target-port` gibt den internen TCP-Port 8080 an.</span><span class="sxs-lookup"><span data-stu-id="58e9d-194">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="58e9d-195">Der Load Balancer leitet über diesen Port Anforderungen an die App weiter.</span><span class="sxs-lookup"><span data-stu-id="58e9d-195">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="58e9d-196">Nachdem die App im Cluster bereitgestellt wurde, fragen Sie die externe IP-Adresse ab, und öffnen Sie sie im Webbrowser:</span><span class="sxs-lookup"><span data-stu-id="58e9d-196">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Navigieren zur Beispiel-App in Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="58e9d-198">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="58e9d-198">Next steps</span></span>

<span data-ttu-id="58e9d-199">Weitere Informationen zur Verwendung von Spring Boot in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="58e9d-199">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="58e9d-200">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="58e9d-200">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="58e9d-201">Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="58e9d-201">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

<span data-ttu-id="58e9d-202">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="58e9d-202">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="58e9d-203">Weitere Informationen zum Spring Boot-Beispielprojekt in Docker finden Sie unter [Spring Boot on Docker Getting Started] (Erste Schritte mit Spring Boot in Docker).</span><span class="sxs-lookup"><span data-stu-id="58e9d-203">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="58e9d-204">Über die folgenden Links erhalten Sie weitere Informationen zur Erstellung von Spring Boot-Anwendungen:</span><span class="sxs-lookup"><span data-stu-id="58e9d-204">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="58e9d-205">Weitere Informationen zum Erstellen einer einfachen Spring Boot-Anwendung finden Sie im Spring Initializr unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="58e9d-205">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="58e9d-206">Über die folgenden Links erhalten Sie weitere Informationen zur Verwendung von Kubernetes mit Azure:</span><span class="sxs-lookup"><span data-stu-id="58e9d-206">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="58e9d-207">Erste Schritte mit einem Kubernetes-Cluster in Container Service</span><span class="sxs-lookup"><span data-stu-id="58e9d-207">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="58e9d-208">Verwenden der Webbenutzeroberfläche von Kubernetes mit Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="58e9d-208">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="58e9d-209">Weitere Informationen zur Verwendung der Kubernetes-Befehlszeilenschnittstelle stehen im Benutzerhandbuch für **kubectl** unter <https://kubernetes.io/docs/user-guide/kubectl/> zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="58e9d-209">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="58e9d-210">Die Kubernetes-Website umfasst mehrere Artikel zur Verwendung von Images in privaten Registrierungen:</span><span class="sxs-lookup"><span data-stu-id="58e9d-210">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="58e9d-211">[Configuring Service Accounts for Pods] (Konfigurieren von Dienstkonten für Pods)</span><span class="sxs-lookup"><span data-stu-id="58e9d-211">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="58e9d-212">[Namespaces]</span><span class="sxs-lookup"><span data-stu-id="58e9d-212">[Namespaces]</span></span>
* <span data-ttu-id="58e9d-213">[Pulling an Image from a Private Registry] (Übertragen eines Images aus einer privaten Registrierung per Pull)</span><span class="sxs-lookup"><span data-stu-id="58e9d-213">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="58e9d-214">Weitere Beispiele zur Verwendung benutzerdefinierter Docker-Images mit Azure finden Sie unter [Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux].</span><span class="sxs-lookup"><span data-stu-id="58e9d-214">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Konfigurieren von Dienstkonten für Pods)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Übertragen eines Images aus einer privaten Registrierung per Pull)

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
