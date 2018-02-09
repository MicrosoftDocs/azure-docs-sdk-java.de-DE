---
title: "Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps"
description: "Erfahren Sie, wie Sie eine Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps bereitstellen."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 515cf350f32fc8252644e7022846cc2c9d264ed0
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="d9309-103">Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="d9309-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="d9309-104">In diesem Artikel wird veranschaulicht, wie Sie mithilfe des [Maven-Plug-Ins für Azure-Web-Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) eine Spring Boot-Beispielanwendung in einem Docker-Container in Azure App Services bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="d9309-104">This article demonstrates using the [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="d9309-105">Das Maven-Plug-In für Azure-Web-Apps für [Apache Maven](http://maven.apache.org/) ermöglicht die nahtlose Integration von Azure App Service in Maven-Projekte und optimiert für Entwickler den Bereitstellungsprozess für Web-Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d9309-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="d9309-106">Das Maven-Plug-In für Azure-Web-Apps ist derzeit als Vorschauversion verfügbar.</span><span class="sxs-lookup"><span data-stu-id="d9309-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="d9309-107">Zur Zeit wird nur FTP-Veröffentlichung unterstützt. Für die Zukunft sind jedoch weitere Features geplant.</span><span class="sxs-lookup"><span data-stu-id="d9309-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="d9309-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="d9309-108">Prerequisites</span></span>

<span data-ttu-id="d9309-109">Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="d9309-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="d9309-110">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="d9309-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d9309-111">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="d9309-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="d9309-112">Ein aktuelles [Java Development Kit (JDK)], Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="d9309-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="d9309-113">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="d9309-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="d9309-114">Einen [Git-Client]</span><span class="sxs-lookup"><span data-stu-id="d9309-114">A [Git] client.</span></span>
* <span data-ttu-id="d9309-115">Einen [Docker]-Client</span><span class="sxs-lookup"><span data-stu-id="d9309-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d9309-116">Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="d9309-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="d9309-117">Klonen der Beispiel-Web-App für Spring Boot in Docker</span><span class="sxs-lookup"><span data-stu-id="d9309-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="d9309-118">In diesem Abschnitt klonen Sie eine containerbasierte Spring Boot-Anwendung und testen sie lokal.</span><span class="sxs-lookup"><span data-stu-id="d9309-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="d9309-119">Öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Spring Boot-Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d9309-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="d9309-120">– oder –</span><span class="sxs-lookup"><span data-stu-id="d9309-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="d9309-121">Klonen Sie das Beispielprojekt [Erste Schritte mit Spring Boot in Docker] in das Verzeichnis, das Sie gerade erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d9309-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="d9309-122">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d9309-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="d9309-123">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d9309-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="d9309-124">Starten Sie die Web-App nach der Erstellung mithilfe von Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d9309-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="d9309-125">Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="d9309-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="d9309-126">Sie können beispielsweise den folgenden Befehl verwenden, wenn curl verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="d9309-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="d9309-127">Es sollte die folgende Meldung angezeigt werden: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="d9309-127">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="d9309-128">Erstellen eines Azure-Dienstprinzipals</span><span class="sxs-lookup"><span data-stu-id="d9309-128">Create an Azure service principal</span></span>

<span data-ttu-id="d9309-129">In diesem Abschnitt erstellen Sie einen Azure-Dienstprinzipal, den das Maven-Plug-In beim Bereitstellen des Containers in Azure verwendet.</span><span class="sxs-lookup"><span data-stu-id="d9309-129">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="d9309-130">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="d9309-130">Open a command prompt.</span></span>

1. <span data-ttu-id="d9309-131">Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="d9309-131">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="d9309-132">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="d9309-132">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="d9309-133">Erstellen Sie einen Azure-Dienstprinzipal:</span><span class="sxs-lookup"><span data-stu-id="d9309-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="d9309-134">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="d9309-134">Where:</span></span>
   | <span data-ttu-id="d9309-135">Parameter</span><span class="sxs-lookup"><span data-stu-id="d9309-135">Parameter</span></span> | <span data-ttu-id="d9309-136">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="d9309-136">Description</span></span> |
   |---|---|
   | `uuuuuuuu` | <span data-ttu-id="d9309-137">Gibt den Benutzernamen für den Dienstprinzipal an.</span><span class="sxs-lookup"><span data-stu-id="d9309-137">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="d9309-138">Gibt das Kennwort für den Dienstprinzipal an.</span><span class="sxs-lookup"><span data-stu-id="d9309-138">Specifies the password for the service principal.</span></span> |

1. <span data-ttu-id="d9309-139">Azure antwortet mit JSON-Code, der etwa wie folgendes Beispiel aussieht:</span><span class="sxs-lookup"><span data-stu-id="d9309-139">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="d9309-140">Sie verwenden die Werte aus dieser JSON-Antwort, wenn Sie das Maven-Plug-In für die Bereitstellung des Containers in Azure konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d9309-140">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="d9309-141">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` und `tttttttt` sind Platzhalterwerte. Sie werden in diesem Beispiel dazu verwendet, die Zuordnung der Werte zu ihren entsprechenden Elementen zu vereinfachen, wenn Sie die Maven-Datei `settings.xml` im nächsten Abschnitt konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d9309-141">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="d9309-142">Konfigurieren von Maven zur Verwendung des Azure-Dienstprinzipals</span><span class="sxs-lookup"><span data-stu-id="d9309-142">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="d9309-143">In diesem Abschnitt verwenden Sie die Werte Ihres Azure-Dienstprinzipals zum Konfigurieren der Authentifizierung, die Maven bei der Bereitstellung Ihres Containers in Azure verwendet.</span><span class="sxs-lookup"><span data-stu-id="d9309-143">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="d9309-144">Öffnen Sie die Maven-Datei `settings.xml` in einem Text-Editor. Diese Datei kann sich beispielsweise in einem der folgenden Pfade befinden:</span><span class="sxs-lookup"><span data-stu-id="d9309-144">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="d9309-145">Fügen Sie Ihre Azure-Dienstprinzipaleinstellungen aus dem vorherigen Abschnitt dieses Tutorials zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d9309-145">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="d9309-146">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="d9309-146">Where:</span></span>
   | <span data-ttu-id="d9309-147">Element</span><span class="sxs-lookup"><span data-stu-id="d9309-147">Element</span></span> | <span data-ttu-id="d9309-148">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="d9309-148">Description</span></span> |
   |---|---|
   | `<id>` | <span data-ttu-id="d9309-149">Gibt einen eindeutigen Namen an, mit dem Maven Ihre Sicherheitseinstellungen abruft, wenn Sie die Web-App in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="d9309-149">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span> |
   | `<client>` | <span data-ttu-id="d9309-150">Enthält den Wert `appId` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="d9309-150">Contains the `appId` value from your service principal.</span></span> |
   | `<tenant>` | <span data-ttu-id="d9309-151">Enthält den Wert `tenant` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="d9309-151">Contains the `tenant` value from your service principal.</span></span> |
   | `<key>` | <span data-ttu-id="d9309-152">Enthält den Wert `password` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="d9309-152">Contains the `password` value from your service principal.</span></span> |
   | `<environment>` | <span data-ttu-id="d9309-153">Definiert die Azure-Zielcloudumgebung (in diesem Beispiel: `AZURE`).</span><span class="sxs-lookup"><span data-stu-id="d9309-153">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="d9309-154">(Eine vollständige Liste der Umgebungen finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)</span><span class="sxs-lookup"><span data-stu-id="d9309-154">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |

1. <span data-ttu-id="d9309-155">Speichern und schließen Sie die Datei *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="d9309-155">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="d9309-156">OPTIONAL: Bereitstellen der lokalen Docker-Datei auf Docker Hub</span><span class="sxs-lookup"><span data-stu-id="d9309-156">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="d9309-157">Wenn Sie ein Docker-Konto besitzen, können Sie das Docker-Containerimage lokal erstellen und per Push an Docker Hub übertragen.</span><span class="sxs-lookup"><span data-stu-id="d9309-157">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="d9309-158">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="d9309-158">To do so, use the following steps.</span></span>

1. <span data-ttu-id="d9309-159">Öffnen Sie die Datei `pom.xml` für Ihre Spring Boot-Anwendung in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="d9309-159">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="d9309-160">Suchen Sie das untergeordnete Element `<imageName>` des `<containerSettings>`-Elements.</span><span class="sxs-lookup"><span data-stu-id="d9309-160">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="d9309-161">Aktualisieren Sie den Wert `${docker.image.prefix}` mit dem Namen Ihres Docker-Kontos:</span><span class="sxs-lookup"><span data-stu-id="d9309-161">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="d9309-162">Wählen Sie eine der folgenden Bereitstellungsmethoden aus:</span><span class="sxs-lookup"><span data-stu-id="d9309-162">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="d9309-163">Erstellen Sie Ihr Containerimage lokal mit Maven, und übertragen Sie den Container anschließend mithilfe von Docker per Push an Docker Hub:</span><span class="sxs-lookup"><span data-stu-id="d9309-163">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="d9309-164">Falls das [Docker-Plug-In für Maven] installiert ist, können Sie das Containerimage mithilfe des `-DpushImage`-Parameters automatisch erstellen und per Push an Docker Hub übertragen:</span><span class="sxs-lookup"><span data-stu-id="d9309-164">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="d9309-165">OPTIONAL: Anpassen der Datei „pom.xml“ vor der Bereitstellung des Containers in Azure</span><span class="sxs-lookup"><span data-stu-id="d9309-165">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="d9309-166">Öffnen Sie die Datei `pom.xml` für Ihre Spring Boot-Anwendung in einem Text-Editor, und suchen Sie das Element `<plugin>` für `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="d9309-166">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="d9309-167">Dieses Element sollte etwa wie folgendes Beispiel aussehen:</span><span class="sxs-lookup"><span data-stu-id="d9309-167">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
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

<span data-ttu-id="d9309-168">Für das Maven-Plug-In können mehrere Werte angepasst werden. Eine ausführliche Beschreibung der einzelnen Elemente finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].</span><span class="sxs-lookup"><span data-stu-id="d9309-168">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="d9309-169">Für diesen Artikel sind jedoch besonders folgende Werte hervorzuheben:</span><span class="sxs-lookup"><span data-stu-id="d9309-169">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="d9309-170">Element</span><span class="sxs-lookup"><span data-stu-id="d9309-170">Element</span></span> | <span data-ttu-id="d9309-171">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="d9309-171">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="d9309-172">Gibt die Version des [Maven-Plug-In für Azure-Web-Apps] an.</span><span class="sxs-lookup"><span data-stu-id="d9309-172">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="d9309-173">Überprüfen Sie die im [zentralen Maven-Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) angegebene Version, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="d9309-173">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="d9309-174">Gibt die Authentifizierungsinformationen für Azure an, die in diesem Beispiel ein `<serverId>`-Element enthalten, das `azure-auth` enthält. Maven nutzt diesen Wert, um die Azure-Dienstprinzipalwerte in Ihrer Maven-Datei *settings.xml* abzurufen, die Sie weiter oben in diesem Artikel festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="d9309-174">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="d9309-175">Gibt die Zielressourcengruppe an (in diesem Beispiel: `maven-plugin`).</span><span class="sxs-lookup"><span data-stu-id="d9309-175">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="d9309-176">Wenn die Ressourcengruppe nicht bereits vorhanden ist, wird sie während der Bereitstellung erstellt.</span><span class="sxs-lookup"><span data-stu-id="d9309-176">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="d9309-177">Gibt den Zielnamen für Ihre Web-App an.</span><span class="sxs-lookup"><span data-stu-id="d9309-177">Specifies the target name for your web app.</span></span> <span data-ttu-id="d9309-178">In diesem Beispiel lautet der Zielname `maven-linux-app-${maven.build.timestamp}`. Dabei wird das Suffix `${maven.build.timestamp}` angehängt, um Konflikte zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="d9309-178">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="d9309-179">(Der Zeitstempel ist optional. Sie können eine beliebige eindeutige Zeichenfolge für den App-Namen angeben.)</span><span class="sxs-lookup"><span data-stu-id="d9309-179">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="d9309-180">Gibt die Zielregion an (in diesem Beispiel: `westus`).</span><span class="sxs-lookup"><span data-stu-id="d9309-180">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="d9309-181">(Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)</span><span class="sxs-lookup"><span data-stu-id="d9309-181">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<appSettings>` | <span data-ttu-id="d9309-182">Gibt eindeutige Einstellungen für Maven an, die beim Bereitstellen der Web-App in Azure verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="d9309-182">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="d9309-183">In diesem Beispiel enthält ein `<property>`-Element ein Name/Wert-Paar untergeordneter Elemente, die den Port für Ihre App angeben.</span><span class="sxs-lookup"><span data-stu-id="d9309-183">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="d9309-184">Die Einstellungen zum Ändern der Portnummer in diesem Beispiel sind nur erforderlich, wenn Sie nicht die Standardeinstellung für den Port verwenden.</span><span class="sxs-lookup"><span data-stu-id="d9309-184">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="d9309-185">Erstellen und Bereitstellen Ihres Containers in Azure</span><span class="sxs-lookup"><span data-stu-id="d9309-185">Build and deploy your container to Azure</span></span>

<span data-ttu-id="d9309-186">Nachdem Sie alle Einstellungen in den vorhergehenden Abschnitten in diesem Artikel konfiguriert haben, können Sie Ihren Container in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="d9309-186">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="d9309-187">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="d9309-187">To do so, use the following steps:</span></span>

1. <span data-ttu-id="d9309-188">Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d9309-188">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="d9309-189">Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d9309-189">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="d9309-190">Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App noch nicht vorhanden ist, wird sie erstellt.</span><span class="sxs-lookup"><span data-stu-id="d9309-190">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d9309-191">Falls in der Region, die Sie im `<region>`-Element der Datei *pom.xml* angeben, beim Starten der Bereitstellung nicht genügend Server verfügbar sind, wird unter Umständen ein Fehler wie im folgenden Beispiel angezeigt:</span><span class="sxs-lookup"><span data-stu-id="d9309-191">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="d9309-192">In diesem Fall können Sie eine andere Region angeben und den Maven-Befehl zum Bereitstellen Ihrer Anwendung erneut ausführen.</span><span class="sxs-lookup"><span data-stu-id="d9309-192">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="d9309-193">Wenn Ihre Web-App bereitgestellt wurde, können Sie sie mit dem [Azure-Portal] verwalten.</span><span class="sxs-lookup"><span data-stu-id="d9309-193">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="d9309-194">Ihre Web-App wird unter **App Services** aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="d9309-194">Your web app will be listed in **App Services**:</span></span>

   ![Im Azure-Portal unter „App Services“ aufgeführte Web-App][AP01]

* <span data-ttu-id="d9309-196">Die URL für Ihre Web-App wird in der **Übersicht** für Ihre Web-App aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="d9309-196">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Festlegen der URL für Ihre Web-App][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="d9309-198">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="d9309-198">Next steps</span></span>

<span data-ttu-id="d9309-199">Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="d9309-199">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="d9309-200">[Maven-Plug-In für Azure-Web-Apps] (Maven-Plug-In für Azure-Web-Apps)</span><span class="sxs-lookup"><span data-stu-id="d9309-200">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="d9309-201">Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)</span><span class="sxs-lookup"><span data-stu-id="d9309-201">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* <span data-ttu-id="d9309-202">[How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service ](deploy-spring-boot-java-app-with-maven-plugin.md) (Bereitstellen einer Spring Boot-App in Azure App Service mithilfe des Maven-Plug-Ins für Azure-Web-Apps)</span><span class="sxs-lookup"><span data-stu-id="d9309-202">[How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service ](deploy-spring-boot-java-app-with-maven-plugin.md)</span></span>

* [<span data-ttu-id="d9309-203">Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d9309-203">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* <span data-ttu-id="d9309-204">[Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)</span><span class="sxs-lookup"><span data-stu-id="d9309-204">[Maven Settings Reference](https://maven.apache.org/settings.html)</span></span>

* <span data-ttu-id="d9309-205">[Docker-Plug-In für Maven] (Docker-Plug-In für Maven)</span><span class="sxs-lookup"><span data-stu-id="d9309-205">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Docker-Plug-In für Maven]: https://github.com/spotify/docker-maven-plugin (Docker-Plug-In für Maven)
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Erste Schritte mit Spring Boot in Docker]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/
[Maven-Plug-In für Azure-Web-Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin (Maven-Plug-In für Azure-Web-Apps)

<!-- IMG List -->

[AP01]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP02.png
