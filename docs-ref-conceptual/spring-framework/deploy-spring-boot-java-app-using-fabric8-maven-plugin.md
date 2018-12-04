---
title: Bereitstellen einer Spring Boot-App unter Verwendung des Fabric8 Maven-Plug-Ins
description: In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung in Microsoft Azure mit dem Fabric8-Plug-In für Apache Maven erläutert.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: ab3babf358cf4899709a9a9d2d7917cb2c6d220e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338834"
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a><span data-ttu-id="53b7b-103">Bereitstellen einer Spring Boot-App unter Verwendung des Fabric8 Maven-Plug-Ins</span><span class="sxs-lookup"><span data-stu-id="53b7b-103">Deploy a Spring Boot app using the Fabric8 Maven Plugin</span></span>

<span data-ttu-id="53b7b-104">**[Fabric8]**  ist eine Open-Source-Lösung, die auf **[Kubernetes]** basiert und Entwicklern beim Erstellen von Anwendungen in Linux-Containern hilft.</span><span class="sxs-lookup"><span data-stu-id="53b7b-104">**[Fabric8]** is an open-source solution that is built on **[Kubernetes]**, which helps developers create applications in Linux containers.</span></span>

<span data-ttu-id="53b7b-105">In diesem Tutorial wird die Verwendung des Fabric8-Plug-Ins für Maven zur Entwicklung und Bereitstellung einer Anwendung auf einem Linux-Host in [Azure Container Service (AKS)] erläutert.</span><span class="sxs-lookup"><span data-stu-id="53b7b-105">This tutorial walks you through using the Fabric8 plugin for Maven to develop to deploy an application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53b7b-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="53b7b-106">Prerequisites</span></span>

<span data-ttu-id="53b7b-107">Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="53b7b-107">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="53b7b-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="53b7b-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="53b7b-109">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="53b7b-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="53b7b-110">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="53b7b-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="53b7b-111">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="53b7b-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="53b7b-112">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="53b7b-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="53b7b-113">Einen [Git-Client]</span><span class="sxs-lookup"><span data-stu-id="53b7b-113">A [Git] client.</span></span>
* <span data-ttu-id="53b7b-114">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="53b7b-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="53b7b-115">Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="53b7b-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="53b7b-116">Erstellen der Web-App für erste Schritte mit Spring Boot in Docker</span><span class="sxs-lookup"><span data-stu-id="53b7b-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="53b7b-117">Im Folgenden werden die Schritte zum Erstellen einer Spring Boot-Webanwendung und zum lokalen Testen dieser Anwendung beschrieben.</span><span class="sxs-lookup"><span data-stu-id="53b7b-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="53b7b-118">Öffnen Sie eine Eingabeaufforderung, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   <span data-ttu-id="53b7b-119">– oder –</span><span class="sxs-lookup"><span data-stu-id="53b7b-119">-- or --</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. <span data-ttu-id="53b7b-120">Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="53b7b-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="53b7b-121">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-121">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   <span data-ttu-id="53b7b-122">– oder –</span><span class="sxs-lookup"><span data-stu-id="53b7b-122">-- or --</span></span>
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. <span data-ttu-id="53b7b-123">Verwenden Sie Maven zum Erstellen und Ausführen der Beispiel-App.</span><span class="sxs-lookup"><span data-stu-id="53b7b-123">Use Maven to build and run the sample app.</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

1. <span data-ttu-id="53b7b-124">Testen Sie die Web-App durch Navigieren zu http://localhost:8080 oder mit dem folgenden `curl`-Befehl:</span><span class="sxs-lookup"><span data-stu-id="53b7b-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="53b7b-125">Es sollte die Meldung **Hello Docker World** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="53b7b-125">You should see a **Hello Docker World** message displayed.</span></span>

   ![Lokales Durchsuchen der Beispielanwendung][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a><span data-ttu-id="53b7b-127">Installieren der Kubernetes-Befehlszeilenschnittstelle und Erstellen einer Azure-Ressourcengruppe mithilfe der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53b7b-127">Install the Kubernetes command-line interface and create an Azure resource group using the Azure CLI</span></span>

1. <span data-ttu-id="53b7b-128">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="53b7b-128">Open a command prompt.</span></span>

1. <span data-ttu-id="53b7b-129">Melden Sie sich mithilfe des folgenden Befehls bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="53b7b-129">Type the following command to log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="53b7b-130">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="53b7b-130">Follow the instructions to complete the login process</span></span>

   <span data-ttu-id="53b7b-131">Die Azure CLI zeigt eine Liste Ihrer Konten an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-131">The Azure CLI will display a list of your accounts; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="53b7b-132">Wenn Sie die Kubernetes-Befehlszeilenschnittstelle (`kubectl`) noch nicht installiert haben, können Sie sie mithilfe der Azure CLI installieren, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-132">If you do not already have the Kubernetes command-line interface (`kubectl`) installed, you can install using the Azure CLI; for example:</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="53b7b-133">Linux-Benutzer müssen diesem Befehl möglicherweise das Präfix `sudo` voranstellen, da er die Kubernetes-Befehlszeilenschnittstelle in `/usr/local/bin` bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="53b7b-133">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   >
   > <span data-ttu-id="53b7b-134">Falls Sie `kubectl` bereits installiert haben und Ihre Version von `kubectl` zu alt ist, wird möglicherweise eine Fehlermeldung wie die im folgenden Beispiel angezeigt, wenn Sie versuchen, die weiter unten in diesem Artikel beschriebenen Schritte auszuführen:</span><span class="sxs-lookup"><span data-stu-id="53b7b-134">If you already have `kubectl`) installed and your version of `kubectl` is too old, you may see an error message similar to the following example when you attempt to complete the steps listed later in this article:</span></span>
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > <span data-ttu-id="53b7b-135">In diesem Fall müssen Sie `kubectl` erneut installieren, um Ihre Version zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="53b7b-135">If this happens, you will need to reinstall `kubectl` to update your version.</span></span>
   >

1. <span data-ttu-id="53b7b-136">Erstellen Sie eine Ressourcengruppe für die Azure-Ressourcen, die Sie in diesem Tutorial verwenden, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-136">Create a resource group for the Azure resources that you will use in this tutorial; for example:</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   <span data-ttu-id="53b7b-137">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="53b7b-137">Where:</span></span>  
      * <span data-ttu-id="53b7b-138">*wingtiptoys-kubernetes* ist ein eindeutiger Name für Ihre Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="53b7b-138">*wingtiptoys-kubernetes* is a unique name for your resource group</span></span>  
      * <span data-ttu-id="53b7b-139">*westeurope* ist ein geeigneter geografischer Ort für Ihre Anwendung.</span><span class="sxs-lookup"><span data-stu-id="53b7b-139">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="53b7b-140">Die Azure CLI zeigt die Ergebnisse der Erstellung Ihrer Ressourcengruppe an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-140">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a><span data-ttu-id="53b7b-141">Erstellen eines Kubernetes-Clusters mit der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53b7b-141">Create a Kubernetes cluster using the Azure CLI</span></span>

1. <span data-ttu-id="53b7b-142">Erstellen Sie einen Kubernetes-Cluster in Ihrer neuen Ressourcengruppe, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-142">Create a Kubernetes cluster in your new resource group; for example:</span></span>  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   <span data-ttu-id="53b7b-143">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="53b7b-143">Where:</span></span>  
      * <span data-ttu-id="53b7b-144">*wingtiptoys-kubernetes* ist der Name Ihrer Ressourcengruppe von weiter oben in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="53b7b-144">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="53b7b-145">*wingtiptoys-cluster* ist ein eindeutiger Name für Ihren Kubernetes-Cluster.</span><span class="sxs-lookup"><span data-stu-id="53b7b-145">*wingtiptoys-cluster* is a unique name for your Kubernetes cluster</span></span>
      * <span data-ttu-id="53b7b-146">*wingtiptoys* ist ein eindeutiger DNS-Name für Ihre Anwendung.</span><span class="sxs-lookup"><span data-stu-id="53b7b-146">*wingtiptoys* is a unique name DNS name for your application</span></span>

   <span data-ttu-id="53b7b-147">Die Azure CLI zeigt die Ergebnisse der Erstellung Ihres Clusters an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-147">The Azure CLI will display the results of your cluster creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. <span data-ttu-id="53b7b-148">Laden Sie Ihre Anmeldeinformationen für den neuen Kubernetes-Cluster herunter, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-148">Download your credentials for your new Kubernetes cluster; for example:</span></span>  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. <span data-ttu-id="53b7b-149">Überprüfen Sie die Verbindung mit dem folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="53b7b-149">Verify your connection with the following command:</span></span>
   ```shell 
   kubectl get nodes
   ```

   <span data-ttu-id="53b7b-150">Daraufhin sollte eine Liste von Knoten und Statusangaben angezeigt werden, wie im folgenden Beispiel dargestellt:</span><span class="sxs-lookup"><span data-stu-id="53b7b-150">You should see a list of nodes and statuses like the following example:</span></span>

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="53b7b-151">Erstellen einer privaten Azure-Containerregistrierung mit der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53b7b-151">Create a private Azure container registry using the Azure CLI</span></span>

1. <span data-ttu-id="53b7b-152">Erstellen Sie eine private Azure-Containerregistrierung in der Ressourcengruppe, um Ihr Docker-Image zu hosten, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-152">Create a private Azure container registry in your resource group to host your Docker image; for example:</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="53b7b-153">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="53b7b-153">Where:</span></span>

   | <span data-ttu-id="53b7b-154">Parameter</span><span class="sxs-lookup"><span data-stu-id="53b7b-154">Parameter</span></span> | <span data-ttu-id="53b7b-155">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="53b7b-155">Description</span></span> |
   |---|---|
   | `wingtiptoys-kubernetes` | <span data-ttu-id="53b7b-156">Gibt den Namen Ihrer Ressourcengruppe von weiter oben in diesem Artikel an.</span><span class="sxs-lookup"><span data-stu-id="53b7b-156">Specifies the name of your resource group from earlier in this article.</span></span> |
   | `wingtiptoysregistry` | <span data-ttu-id="53b7b-157">Gibt einen eindeutigen Namen für die private Registrierung an.</span><span class="sxs-lookup"><span data-stu-id="53b7b-157">Specifies a unique name for your private registry.</span></span> |
   | `westeurope` | <span data-ttu-id="53b7b-158">Gibt einen geeigneten geografischen Ort für Ihre Anwendung an.</span><span class="sxs-lookup"><span data-stu-id="53b7b-158">Specifies an appropriate geographic location for your application.</span></span> |

   <span data-ttu-id="53b7b-159">Die Azure CLI zeigt die Ergebnisse der Erstellung Ihrer Registrierung an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-159">The Azure CLI will display the results of your registry creation; for example:</span></span>  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

2. <span data-ttu-id="53b7b-160">Rufen Sie das Kennwort für Ihre Containerregistrierung über die Azure-Befehlszeilenschnittstelle ab.</span><span class="sxs-lookup"><span data-stu-id="53b7b-160">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   <span data-ttu-id="53b7b-161">Die Azure CLI zeigt das Kennwort Ihrer Registrierung an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-161">The Azure CLI will display the password for your registry; for example:</span></span>  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

3. <span data-ttu-id="53b7b-162">Navigieren Sie zu dem Konfigurationsverzeichnis Ihrer Maven-Installation (Standard: „~/.m2/“ oder „C:\Users\username\.m2“), und öffnen Sie die Datei *settings.xml* mit einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="53b7b-162">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

4. <span data-ttu-id="53b7b-163">Fügen Sie die URL, den Benutzernamen und das Kennwort für Azure Container Registry einer neuen `<server>`-Sammlung in der Datei *settings.xml* hinzu.</span><span class="sxs-lookup"><span data-stu-id="53b7b-163">Add your Azure Container Registry URL, username and password to a new `<server>` collection in the *settings.xml* file.</span></span>
   <span data-ttu-id="53b7b-164">`id` und `username` bilden den Namen der Registrierung.</span><span class="sxs-lookup"><span data-stu-id="53b7b-164">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="53b7b-165">Verwenden Sie den `password`-Wert des vorherigen Befehls (ohne Anführungszeichen).</span><span class="sxs-lookup"><span data-stu-id="53b7b-165">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

5. <span data-ttu-id="53b7b-166">Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung (z.B. *C:\SpringBoot\gs-spring-boot-docker\complete* oder */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*), und öffnen Sie die Datei *pom.xml* mit einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="53b7b-166">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

6. <span data-ttu-id="53b7b-167">Aktualisieren Sie die `<properties>`-Sammlung in der Datei *pom.xml* mit dem Wert des Anmeldeservers für Ihre Azure Container Registry-Instanz.</span><span class="sxs-lookup"><span data-stu-id="53b7b-167">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

7. <span data-ttu-id="53b7b-168">Aktualisieren Sie die `<plugins>`-Sammlung in der Datei *pom.xml* so, dass `<plugin>` die Adresse des Anmeldeservers und den Registrierungsnamen für Ihre Azure Container Registry-Instanz enthält.</span><span class="sxs-lookup"><span data-stu-id="53b7b-168">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
     <groupId>com.spotify</groupId>
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

8. <span data-ttu-id="53b7b-169">Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Maven-Befehl aus, um den Docker-Container zu erstellen und das Image per Push in die Registrierung zu übertragen:</span><span class="sxs-lookup"><span data-stu-id="53b7b-169">Navigate to the completed project directory for your Spring Boot application, and run the following Maven command to build the Docker container and push the image to your registry:</span></span>

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   <span data-ttu-id="53b7b-170">Maven zeigt die Ergebnisse des Builds an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-170">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a><span data-ttu-id="53b7b-171">Konfigurieren der Spring Boot-App für die Verwendung des Fabric8 Maven-Plug-Ins</span><span class="sxs-lookup"><span data-stu-id="53b7b-171">Configure your Spring Boot app to use the Fabric8 Maven plugin</span></span>

1. <span data-ttu-id="53b7b-172">Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung (z.B. *C:\SpringBoot\gs-spring-boot-docker\complete* oder */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*), und öffnen Sie die Datei *pom.xml* mit einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="53b7b-172">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="53b7b-173">Aktualisieren Sie die `<plugins>`-Sammlung in der Datei *pom.xml*, um das Fabric8 Maven-Plug-In hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="53b7b-173">Update the `<plugins>` collection in the *pom.xml* file to add the Fabric8 Maven plugin:</span></span>

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="53b7b-174">Navigieren Sie zum Hauptquellverzeichnis für Ihre Spring Boot-Anwendung (z.B. *C:\SpringBoot\gs-spring-boot-docker\complete\src\main* oder */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*), und erstellen Sie einen neuen Ordner namens *fabric8*.</span><span class="sxs-lookup"><span data-stu-id="53b7b-174">Navigate to the main source directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*"), and create a new folder named "*fabric8*".</span></span>

1. <span data-ttu-id="53b7b-175">Erstellen Sie drei YAML-Fragmentdateien im neuen Ordner *fabric8*:</span><span class="sxs-lookup"><span data-stu-id="53b7b-175">Create three YAML fragment files in the new *fabric8* folder:</span></span>

   <span data-ttu-id="53b7b-176">a.</span><span class="sxs-lookup"><span data-stu-id="53b7b-176">a.</span></span> <span data-ttu-id="53b7b-177">Erstellen Sie eine Datei namens **deployment.yml** mit folgendem Inhalt:</span><span class="sxs-lookup"><span data-stu-id="53b7b-177">Create a file named **deployment.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   <span data-ttu-id="53b7b-178">b.</span><span class="sxs-lookup"><span data-stu-id="53b7b-178">b.</span></span> <span data-ttu-id="53b7b-179">Erstellen Sie eine Datei namens **secrets.yml** mit folgendem Inhalt:</span><span class="sxs-lookup"><span data-stu-id="53b7b-179">Create a file named **secrets.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   <span data-ttu-id="53b7b-180">c.</span><span class="sxs-lookup"><span data-stu-id="53b7b-180">c.</span></span> <span data-ttu-id="53b7b-181">Erstellen Sie eine Datei namens **service.yml** mit folgendem Inhalt:</span><span class="sxs-lookup"><span data-stu-id="53b7b-181">Create a file named **service.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. <span data-ttu-id="53b7b-182">Führen Sie den folgenden Maven-Befehl aus, um die Kubernetes-Ressourcenlistendatei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="53b7b-182">Run the following Maven command to build the Kubernetes resource list file:</span></span>

   ```shell
   mvn fabric8:resource
   ```

   <span data-ttu-id="53b7b-183">Dieser Befehl führt alle Kubernetes-YAML-Ressourcendateien im Ordner *src/main/fabric8* in einer YAML-Datei zusammen, die eine Kubernetes-Ressourcenliste enthält, die direkt auf einen Kubernetes-Cluster angewendet oder in ein Helm-Diagramm exportiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="53b7b-183">This command merges all Kubernetes resource yaml files under the *src/main/fabric8* folder to a YAML file that contains a Kubernetes resource list, which can be applied to Kubernetes cluster directly or export to a helm chart.</span></span>

   <span data-ttu-id="53b7b-184">Maven zeigt die Ergebnisse des Builds an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-184">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="53b7b-185">Führen Sie den folgenden Maven-Befehl aus, um die Ressourcenlistendatei auf den Kubernetes-Cluster anzuwenden:</span><span class="sxs-lookup"><span data-stu-id="53b7b-185">Run the following Maven command to apply the resource list file to your Kubernetes cluster:</span></span>

   ```shell
   mvn fabric8:apply
   ```

   <span data-ttu-id="53b7b-186">Maven zeigt die Ergebnisse des Builds an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-186">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="53b7b-187">Nachdem die App im Cluster bereitgestellt wurde, fragen Sie die externe IP-Adresse mit der `kubectl`-Anwendung ab, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-187">Once the app is deployed to the cluster, query the external IP address using the `kubectl` application; for example:</span></span>
   ```shell
   kubectl get svc -w
   ```

   <span data-ttu-id="53b7b-188">`kubectl` zeigt die internen und externen IP-Adressen an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-188">`kubectl` will display your internal and external IP addresses; for example:</span></span>

   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```

   <span data-ttu-id="53b7b-189">Sie können die externe IP-Adresse verwenden, um Ihre Anwendung in einem Webbrowser zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="53b7b-189">You can use the external IP address to open your application in a web browser.</span></span>

   ![Externes Durchsuchen der Beispielanwendung][SB02]

## <a name="delete-your-kubernetes-cluster"></a><span data-ttu-id="53b7b-191">Löschen Ihres Kubernetes-Clusters</span><span class="sxs-lookup"><span data-stu-id="53b7b-191">Delete your Kubernetes cluster</span></span>

<span data-ttu-id="53b7b-192">Wenn der Kubernetes-Cluster nicht mehr benötigt wird, können Sie den Befehl `az group delete` verwenden, um die Ressourcengruppe zu entfernen. Dadurch werden auch alle zugehörigen Ressourcen entfernt, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53b7b-192">When your Kubernetes cluster is no longer needed, you can use the `az group delete` command to remove the resource group, which will remove all of its related resources; for example:</span></span>

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a><span data-ttu-id="53b7b-193">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="53b7b-193">Next steps</span></span>

<span data-ttu-id="53b7b-194">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="53b7b-194">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="53b7b-195">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="53b7b-195">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="53b7b-196">Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="53b7b-196">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)
* <span data-ttu-id="53b7b-197">[Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md) (Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service)</span><span class="sxs-lookup"><span data-stu-id="53b7b-197">[Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)</span></span>

<span data-ttu-id="53b7b-198">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="53b7b-198">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="53b7b-199">Weitere Informationen zum Spring Boot-Beispielprojekt in Docker finden Sie unter [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="53b7b-199">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="53b7b-200">Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie bei **Spring Initializr** unter <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="53b7b-200">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at <https://start.spring.io/>.</span></span>

<span data-ttu-id="53b7b-201">Weitere Informationen zu den ersten Schritten beim Erstellen einer einfachen Spring Boot-Anwendung finden Sie bei Spring Initializr unter <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="53b7b-201">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at <https://start.spring.io/>.</span></span>

<span data-ttu-id="53b7b-202">Weitere Beispiele zur Vorgehensweise bei der Verwendung benutzerdefinierter Docker-Images mit Azure finden Sie unter [Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux].</span><span class="sxs-lookup"><span data-stu-id="53b7b-202">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Git]: https://github.com/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
