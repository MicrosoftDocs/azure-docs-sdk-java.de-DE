---
title: Bereitstellen einer Spring Boot-App in Azure Container Registry in Azure App Service mithilfe des Maven-Plug-Ins für Azure-Web-Apps
description: In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung in Azure Container Registry in Azure App Service mithilfe eines Maven-Plug-Ins erläutert.
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: e84960ebf79b89b2430924016a429518a935d086
ms.sourcegitcommit: 9d9e2fa97ebd95a699adcb58e82c3fc0882f0a24
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/15/2018
ms.locfileid: "49315934"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="c0c0e-103">Bereitstellen einer Spring Boot-App in Azure Container Registry in Azure App Service mithilfe des Maven-Plug-Ins für Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="c0c0e-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="c0c0e-104">In diesem Artikel wird veranschaulicht, wie Sie eine [Spring Boot]-Beispielanwendung in Azure Container Registry und dann mithilfe des Maven-Plug-Ins für Azure-Web-Apps in Azure App Services bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-104">This article demonstrates how to deploy a sample [Spring Boot] application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c0c0e-105">Das Maven-Plug-In für Azure-Web-Apps für [Apache Maven](http://maven.apache.org/) ermöglicht die nahtlose Integration von Azure App Service in Maven-Projekte und optimiert für Entwickler den Bereitstellungsprozess für Web-Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="c0c0e-106">Das Maven-Plug-In für Azure-Web-Apps ist derzeit als Vorschauversion verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="c0c0e-107">Zur Zeit wird nur FTP-Veröffentlichung unterstützt. Für die Zukunft sind jedoch weitere Features geplant.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="c0c0e-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c0c0e-108">Prerequisites</span></span>

<span data-ttu-id="c0c0e-109">Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="c0c0e-110">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="c0c0e-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c0c0e-111">Die [Azure CLI (Command-Line Interface, Befehlszeilenschnittstelle)]</span><span class="sxs-lookup"><span data-stu-id="c0c0e-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c0c0e-112">Ein aktuelles [Java Development Kit (JDK)], Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="c0c0e-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="c0c0e-113">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="c0c0e-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c0c0e-114">Einen [Git]</span><span class="sxs-lookup"><span data-stu-id="c0c0e-114">A [Git] client.</span></span>
* <span data-ttu-id="c0c0e-115">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="c0c0e-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c0c0e-116">Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="c0c0e-117">Klonen der Beispiel-Web-App für Spring Boot in Docker</span><span class="sxs-lookup"><span data-stu-id="c0c0e-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="c0c0e-118">In diesem Abschnitt klonen Sie eine containerbasierte Spring Boot-Anwendung und testen sie lokal.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="c0c0e-119">Öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Spring Boot-Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c0c0e-120">– oder –</span><span class="sxs-lookup"><span data-stu-id="c0c0e-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c0c0e-121">Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. <span data-ttu-id="c0c0e-122">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="c0c0e-123">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c0c0e-124">Starten Sie die Web-App nach der Erstellung mithilfe von Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c0c0e-125">Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="c0c0e-126">Sie können beispielsweise den folgenden Befehl verwenden, wenn curl verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c0c0e-127">Es sollte die folgende Meldung angezeigt werden: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-127">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Lokales Durchsuchen von Beispiel-Apps][SB01]

> [!NOTE]
>
> <span data-ttu-id="c0c0e-129">Wenn Sie Docker lokal verwenden, wird unter Umständen ein Fehler mit dem Hinweis angezeigt, dass Sie keine Verbindung mit Localhost an Port 2375 herstellen können.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-129">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="c0c0e-130">In diesem Fall müssen Sie möglicherweise die lokale Verwendung von Docker ohne TLS aktivieren.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-130">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="c0c0e-131">Öffnen Sie dazu die Docker-Einstellungen, und aktivieren Sie die Option **Expose daemon on TCP://localhost:2375 without TLS** (Daemon unter TCP://localhost:2375 ohne TLS verfügbar machen).</span><span class="sxs-lookup"><span data-stu-id="c0c0e-131">To do so, open your Docker settings and check the option to **Expose daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![Docker-Daemon am lokalen TCP-Port 2375 verfügbar machen][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="c0c0e-133">Erstellen eines Azure-Dienstprinzipals</span><span class="sxs-lookup"><span data-stu-id="c0c0e-133">Create an Azure service principal</span></span>

<span data-ttu-id="c0c0e-134">In diesem Abschnitt erstellen Sie einen Azure-Dienstprinzipal, den das Maven-Plug-In beim Bereitstellen des Containers in Azure verwendet.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-134">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="c0c0e-135">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-135">Open a command prompt.</span></span>

2. <span data-ttu-id="c0c0e-136">Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-136">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="c0c0e-137">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-137">Follow the instructions to complete the sign-in process.</span></span>

3. <span data-ttu-id="c0c0e-138">Erstellen Sie einen Azure-Dienstprinzipal:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-138">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="c0c0e-139">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-139">Where:</span></span>

   | <span data-ttu-id="c0c0e-140">Parameter</span><span class="sxs-lookup"><span data-stu-id="c0c0e-140">Parameter</span></span>  |                    <span data-ttu-id="c0c0e-141">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0c0e-141">Description</span></span>                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | <span data-ttu-id="c0c0e-142">Gibt den Benutzernamen für den Dienstprinzipal an.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-142">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="c0c0e-143">Gibt das Kennwort für den Dienstprinzipal an.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-143">Specifies the password for the service principal.</span></span>  |


4. <span data-ttu-id="c0c0e-144">Azure antwortet mit JSON-Code, der etwa wie folgendes Beispiel aussieht:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-144">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="c0c0e-145">Sie verwenden die Werte aus dieser JSON-Antwort, wenn Sie das Maven-Plug-In für die Bereitstellung des Containers in Azure konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-145">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="c0c0e-146">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` und `tttttttt` sind Platzhalterwerte. Sie werden in diesem Beispiel dazu verwendet, die Zuordnung der Werte zu ihren entsprechenden Elementen zu vereinfachen, wenn Sie die Maven-Datei `settings.xml` im nächsten Abschnitt konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-146">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="c0c0e-147">Erstellen einer Azure Container Registry-Instanz über die Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="c0c0e-147">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="c0c0e-148">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-148">Open a command prompt.</span></span>

1. <span data-ttu-id="c0c0e-149">Melden Sie sich bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-149">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="c0c0e-150">Erstellen Sie eine Ressourcengruppe für die in diesem Artikel verwendeten Azure-Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-150">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="c0c0e-151">Ersetzen Sie `wingtiptoysresources` in diesem Beispiel durch einen eindeutigen Namen für Ihre Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-151">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="c0c0e-152">Erstellen Sie eine private Azure-Containerregistrierung in der Ressourcengruppe für Ihre Spring Boot-App:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-152">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="c0c0e-153">Ersetzen Sie `wingtiptoysregistry` in diesem Beispiel durch einen eindeutigen Namen für Ihre Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-153">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="c0c0e-154">Rufen Sie das Kennwort für Ihre Containerregistrierung ab:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-154">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="c0c0e-155">Azure antwortet mit Ihrem Kennwort. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-155">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="c0c0e-156">Hinzufügen der Azure-Containerregistrierung und des Azure-Dienstprinzipals zu den Maven-Einstellungen</span><span class="sxs-lookup"><span data-stu-id="c0c0e-156">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="c0c0e-157">Öffnen Sie die Maven-Datei `settings.xml` in einem Text-Editor. Diese Datei kann sich beispielsweise in einem der folgenden Pfade befinden:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-157">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. <span data-ttu-id="c0c0e-158">Fügen Sie Ihre Zugriffseinstellungen für Azure Container Registry aus dem vorherigen Abschnitt dieses Artikels zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-158">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="c0c0e-159">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-159">Where:</span></span>

   |   <span data-ttu-id="c0c0e-160">Element</span><span class="sxs-lookup"><span data-stu-id="c0c0e-160">Element</span></span>    |                                 <span data-ttu-id="c0c0e-161">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0c0e-161">Description</span></span>                                  |
   |--------------|------------------------------------------------------------------------------|
   |    `<id>`    |         <span data-ttu-id="c0c0e-162">Enthält den Namen Ihrer privaten Azure-Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-162">Contains the name of your private Azure container registry.</span></span>          |
   | `<username>` |         <span data-ttu-id="c0c0e-163">Enthält den Namen Ihrer privaten Azure-Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-163">Contains the name of your private Azure container registry.</span></span>          |
   | `<password>` | <span data-ttu-id="c0c0e-164">Enthält das Kennwort, das Sie im vorherigen Abschnitt dieses Artikels abgerufen haben.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-164">Contains the password you retrieved in the previous section of this article.</span></span> |


3. <span data-ttu-id="c0c0e-165">Fügen Sie Ihre Azure-Dienstprinzipaleinstellungen aus einem vorherigen Abschnitt dieses Artikels zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-165">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="c0c0e-166">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-166">Where:</span></span>

   |     <span data-ttu-id="c0c0e-167">Element</span><span class="sxs-lookup"><span data-stu-id="c0c0e-167">Element</span></span>     |                                                                                   <span data-ttu-id="c0c0e-168">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0c0e-168">Description</span></span>                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                <span data-ttu-id="c0c0e-169">Gibt einen eindeutigen Namen an, mit dem Maven Ihre Sicherheitseinstellungen abruft, wenn Sie die Web-App in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-169">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>                                |
   |   `<client>`    |                                                             <span data-ttu-id="c0c0e-170">Enthält den Wert `appId` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-170">Contains the `appId` value from your service principal.</span></span>                                                             |
   |   `<tenant>`    |                                                            <span data-ttu-id="c0c0e-171">Enthält den Wert `tenant` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-171">Contains the `tenant` value from your service principal.</span></span>                                                             |
   |     `<key>`     |                                                           <span data-ttu-id="c0c0e-172">Enthält den Wert `password` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-172">Contains the `password` value from your service principal.</span></span>                                                            |
   | `<environment>` | <span data-ttu-id="c0c0e-173">Definiert die Azure-Zielcloudumgebung (in diesem Beispiel: `AZURE`).</span><span class="sxs-lookup"><span data-stu-id="c0c0e-173">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="c0c0e-174">(Eine vollständige Liste der Umgebungen finden Sie in der Dokumentation zum [Maven Plugin for Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="c0c0e-174">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |


4. <span data-ttu-id="c0c0e-175">Speichern und schließen Sie die Datei *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-175">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="c0c0e-176">Erstellen des Docker-Containerimages und Übertragen des Images an die Azure-Containerregistrierung</span><span class="sxs-lookup"><span data-stu-id="c0c0e-176">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="c0c0e-177">Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung (z.B. „*C:\SpringBoot\gs-spring-boot-docker\complete*“ oder „*/users/robert/SpringBoot/gs-spring-boot-docker/complete*“), und öffnen Sie die Datei *pom.xml* mit einem Texteditor.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-177">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

2. <span data-ttu-id="c0c0e-178">Aktualisieren Sie die Auflistung `<properties>` in der Datei *pom.xml* mit dem Wert des Anmeldeservers für Ihre Azure-Containerregistrierung aus dem vorherigen Abschnitt dieses Tutorials. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-178">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="c0c0e-179">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-179">Where:</span></span>

   |           <span data-ttu-id="c0c0e-180">Element</span><span class="sxs-lookup"><span data-stu-id="c0c0e-180">Element</span></span>           |                                                                       <span data-ttu-id="c0c0e-181">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0c0e-181">Description</span></span>                                                                       |
   |-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
   | `<azure.containerRegistry>` |                                              <span data-ttu-id="c0c0e-182">Gibt den Namen Ihrer privaten Azure-Containerregistrierung an.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-182">Specifies the name of your private Azure container registry.</span></span>                                               |
   |   `<docker.image.prefix>`   | <span data-ttu-id="c0c0e-183">Gibt die URL Ihrer privaten Azure-Containerregistrierung an. Sie wird durch Anfügen von „.azurecr.io“ an den Namen der privaten Containerregistrierung abgeleitet.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-183">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span> |


3. <span data-ttu-id="c0c0e-184">Vergewissern Sie sich, dass `<plugin>` für das Docker-Plug-In in der Datei *pom.xml* die richtigen Eigenschaften für Anmeldeserveradresse und Registrierungsname aus dem vorherigen Schritt in diesem Tutorial enthält.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-184">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="c0c0e-185">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="c0c0e-185">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="c0c0e-186">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-186">Where:</span></span>

   |     <span data-ttu-id="c0c0e-187">Element</span><span class="sxs-lookup"><span data-stu-id="c0c0e-187">Element</span></span>     |                                       <span data-ttu-id="c0c0e-188">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0c0e-188">Description</span></span>                                       |
   |-----------------|-----------------------------------------------------------------------------------------|
   |  `<serverId>`   |  <span data-ttu-id="c0c0e-189">Gibt die Eigenschaft an, die den Namen Ihrer privaten Azure-Containerregistrierung enthält.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-189">Specifies the property which contains name of your private Azure container registry.</span></span>   |
   | `<registryUrl>` | <span data-ttu-id="c0c0e-190">Gibt die Eigenschaft an, die die URL Ihrer privaten Azure-Containerregistrierung enthält.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-190">Specifies the property which contains the URL of your private Azure container registry.</span></span> |


4. <span data-ttu-id="c0c0e-191">Navigieren Sie zu dem abgeschlossenen Projektverzeichnis für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Befehl aus, um die Anwendung erneut zu erstellen und den Container per Push in die Azure-Containerregistrierung zu übertragen:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-191">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

5. <span data-ttu-id="c0c0e-192">OPTIONAL: Navigieren Sie zum [Azure-Portal], und vergewissern Sie sich, dass Ihre Containerregistrierung das Docker-Containerimage **gs-spring-boot-docker** enthält.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-192">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Überprüfen des Containers im Azure-Portal][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="c0c0e-194">Anpassen der Datei „pom.xml“ und anschließendes Erstellen und Bereitstellen des Containers in Azure</span><span class="sxs-lookup"><span data-stu-id="c0c0e-194">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="c0c0e-195">Öffnen Sie die Datei `pom.xml` für Ihre Spring Boot-Anwendung in einem Text-Editor, und suchen Sie das Element `<plugin>` für `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-195">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="c0c0e-196">Dieses Element sollte etwa wie folgendes Beispiel aussehen:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-196">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="c0c0e-197">Für das Maven-Plug-In können mehrere Werte angepasst werden. Eine ausführliche Beschreibung der einzelnen Elemente finden Sie in der Dokumentation zum [Maven Plugin for Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="c0c0e-197">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="c0c0e-198">Für diesen Artikel sind jedoch besonders folgende Werte hervorzuheben:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-198">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="c0c0e-199">Element</span><span class="sxs-lookup"><span data-stu-id="c0c0e-199">Element</span></span> | <span data-ttu-id="c0c0e-200">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0c0e-200">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="c0c0e-201">Gibt die Version des [Maven Plugin for Azure Web Apps] an.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-201">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="c0c0e-202">Überprüfen Sie die im [zentralen Maven-Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) angegebene Version, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-202">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="c0c0e-203">Gibt die Authentifizierungsinformationen für Azure an, die in diesem Beispiel ein `<serverId>`-Element enthalten, das `azure-auth` enthält. Maven nutzt diesen Wert, um die Azure-Dienstprinzipalwerte in Ihrer Maven-Datei *settings.xml* abzurufen, die Sie weiter oben in diesem Artikel festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-203">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="c0c0e-204">Gibt die Zielressourcengruppe an (in diesem Beispiel: `wingtiptoysresources`).</span><span class="sxs-lookup"><span data-stu-id="c0c0e-204">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="c0c0e-205">Wenn die Ressourcengruppe nicht bereits vorhanden ist, wird sie während der Bereitstellung erstellt.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-205">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="c0c0e-206">Gibt den Zielnamen für Ihre Web-App an.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-206">Specifies the target name for your web app.</span></span> <span data-ttu-id="c0c0e-207">In diesem Beispiel lautet der Zielname `maven-linux-app-${maven.build.timestamp}`. Dabei wird das Suffix `${maven.build.timestamp}` angehängt, um Konflikte zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-207">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="c0c0e-208">(Der Zeitstempel ist optional. Sie können eine beliebige eindeutige Zeichenfolge für den App-Namen angeben.)</span><span class="sxs-lookup"><span data-stu-id="c0c0e-208">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="c0c0e-209">Gibt die Zielregion an (in diesem Beispiel: `westus`).</span><span class="sxs-lookup"><span data-stu-id="c0c0e-209">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="c0c0e-210">(Eine vollständige Liste finden Sie in der Dokumentation zum [Maven Plugin for Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="c0c0e-210">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<containerSettings>` | <span data-ttu-id="c0c0e-211">Gibt die Eigenschaften an, die den Namen und die URL des Containers enthalten.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-211">Specifies the properties which contain the name and URL of your container.</span></span> |
| `<appSettings>` | <span data-ttu-id="c0c0e-212">Gibt eindeutige Einstellungen für Maven an, die beim Bereitstellen der Web-App in Azure verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-212">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="c0c0e-213">In diesem Beispiel enthält ein `<property>`-Element ein Name/Wert-Paar untergeordneter Elemente, die den Port für Ihre App angeben.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-213">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="c0c0e-214">Die Einstellungen zum Ändern der Portnummer in diesem Beispiel sind nur erforderlich, wenn Sie nicht die Standardeinstellung für den Port verwenden.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-214">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="c0c0e-215">Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-215">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c0c0e-216">Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-216">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="c0c0e-217">Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App noch nicht vorhanden ist, wird sie erstellt.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-217">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c0c0e-218">Falls in der Region, die Sie im `<region>`-Element der Datei *pom.xml* angeben, beim Starten der Bereitstellung nicht genügend Server verfügbar sind, wird unter Umständen ein Fehler wie im folgenden Beispiel angezeigt:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-218">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="c0c0e-219">In diesem Fall können Sie eine andere Region angeben und den Maven-Befehl zum Bereitstellen Ihrer Anwendung erneut ausführen.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-219">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="c0c0e-220">Wenn Ihre Web-App bereitgestellt wurde, können Sie sie mit dem [Azure-Portal] verwalten.</span><span class="sxs-lookup"><span data-stu-id="c0c0e-220">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="c0c0e-221">Ihre Web-App wird unter **App Services** aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-221">Your web app will be listed in **App Services**:</span></span>

   ![Im Azure-Portal unter „App Services“ aufgeführte Web-App][AP01]

* <span data-ttu-id="c0c0e-223">Die URL für Ihre Web-App wird in der **Übersicht** für Ihre Web-App aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-223">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Festlegen der URL für Ihre Web-App][AP02]

## <a name="next-steps"></a><span data-ttu-id="c0c0e-225">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c0c0e-225">Next steps</span></span>

<span data-ttu-id="c0c0e-226">Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="c0c0e-226">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="c0c0e-227">[Maven Plugin for Azure Web Apps] (Maven-Plug-In für Azure-Web-Apps)</span><span class="sxs-lookup"><span data-stu-id="c0c0e-227">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="c0c0e-228">Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)</span><span class="sxs-lookup"><span data-stu-id="c0c0e-228">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="c0c0e-229">Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c0c0e-229">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* <span data-ttu-id="c0c0e-230">[Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)</span><span class="sxs-lookup"><span data-stu-id="c0c0e-230">[Maven Settings Reference](https://maven.apache.org/settings.html)</span></span>

* <span data-ttu-id="c0c0e-231">[Docker plugin for Maven] (Docker-Plug-In für Maven)</span><span class="sxs-lookup"><span data-stu-id="c0c0e-231">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure CLI (Command-Line Interface, Befehlszeilenschnittstelle)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin (Maven-Plug-In für Azure-Web-Apps)
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin (Docker-Plug-In für Maven)
[Kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
