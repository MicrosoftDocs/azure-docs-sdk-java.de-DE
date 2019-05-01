---
title: Konfigurieren von Web-App-Bereitstellungen mithilfe von Java | Microsoft-Dokumentation
description: Java-Beispielcode zum Konfigurieren der Git- oder FTP-basierten Azure App Service-Bereitstellungen mithilfe des Azure SDKs für Java
author: rloutlaw
manager: douge
ms.assetid: 833e9c78-1e50-4c23-a611-f73a2f0c2983
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: c416cb871ac8264cd6da2045d1ffdd50607fb092
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592625"
---
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a><span data-ttu-id="64401-103">Konfigurieren von Azure App Service-Bereitstellungsquellen über Ihre Java-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="64401-103">Configure Azure App Service deployment sources from your Java applications</span></span>

<span data-ttu-id="64401-104">[Dieses Beispiel](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) stellt Code für vier Anwendungen in einem einzelnen [Azure App Service](https://docs.microsoft.com/azure/app-service/)-Plan bereit, die jeweils eine andere Bereitstellungsquelle verwenden.</span><span class="sxs-lookup"><span data-stu-id="64401-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) deploys code to four applications in a single [Azure App Service](https://docs.microsoft.com/azure/app-service/) plan, each using a different deployment source.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="64401-105">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="64401-105">Run the sample</span></span>

<span data-ttu-id="64401-106">Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest.</span><span class="sxs-lookup"><span data-stu-id="64401-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="64401-107">Führen Sie anschließend Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="64401-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

<span data-ttu-id="64401-108">Sehen Sie sich den [vollständigen Beispielcode auf GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java) an.</span><span class="sxs-lookup"><span data-stu-id="64401-108">View the [complete sample code on GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="64401-109">Authentifizieren über Azure</span><span class="sxs-lookup"><span data-stu-id="64401-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a><span data-ttu-id="64401-110">Erstellen einer App Service-App, die Apache Tomcat ausführt</span><span class="sxs-lookup"><span data-stu-id="64401-110">Create a App Service app running Apache Tomcat</span></span>

```java
// create a new Standard app service plan and create a single Java 8/Tomcat 8 app in it
WebApp app1 = azure.webApps().define(app1Name)
             .withNewResourceGroup(rgName)
             .withNewAppServicePlan(planName)
             .withRegion(Region.US_WEST)
             .withPricingTier(AppServicePricingTier.STANDARD_S1)
             .withJavaVersion(JavaVersion.JAVA_8_NEWEST)
             .withWebContainer(WebContainer.TOMCAT_8_0_NEWEST)
             .create();
```

<span data-ttu-id="64401-111">`withJavaVersion()` und `withWebContainer()` konfigurieren App Service für die Bereitstellung von HTTP-Anforderungen unter Verwendung von Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="64401-111">`withJavaVersion()` and `withWebContainer()` configure App Service to serve HTTP requests using Tomcat 8.</span></span>

## <a name="deploy-a-java-application-using-ftp"></a><span data-ttu-id="64401-112">Bereitstellen einer Java-Anwendung unter Verwendung von FTP</span><span class="sxs-lookup"><span data-stu-id="64401-112">Deploy a Java application using FTP</span></span>
```java
// pass the PublishingProfile that contains FTP information to a helper method 
uploadFileToFtp(app1.getPublishingProfile(), "helloworld.war", 
      ManageWebAppSourceControl.class.getResourceAsStream("/helloworld.war"));

// Use the FTP classes in the Apache Commons library to connect to Azure using 
// the information from the PublishingProfile
private static void uploadFileToFtp(PublishingProfile profile, String fileName, InputStream file) throws Exception {
        FTPClient ftpClient = new FTPClient();
        String[] ftpUrlSegments = profile.ftpUrl().split("/", 2);
        String server = ftpUrlSegments[0];
        // Tomcat will deploy WAR files uploaded to this directory.
        String path = "./site/wwwroot/webapps"; 

        // FTP the build WAR to Azure
        ftpClient.connect(server);
        ftpClient.login(profile.ftpUsername(), profile.ftpPassword());
        ftpClient.setFileType(FTP.BINARY_FILE_TYPE);
        ftpClient.changeWorkingDirectory(path);
        ftpClient.storeFile(fileName, file);
        ftpClient.disconnect();
}
```

<span data-ttu-id="64401-113">Dieser Code lädt eine WAR-Datei in das Verzeichnis `/site/wwwroot/webapps` hoch.</span><span class="sxs-lookup"><span data-stu-id="64401-113">This code uploads a WAR file to the `/site/wwwroot/webapps` directory.</span></span> <span data-ttu-id="64401-114">Tomcat stellt WAR-Dateien aus diesem Verzeichnis standardmäßig in App Service bereit.</span><span class="sxs-lookup"><span data-stu-id="64401-114">Tomcat deploys WAR files placed in this directory by default in App Service.</span></span>

## <a name="deploy-a-java-application-from-a-local-git-repo"></a><span data-ttu-id="64401-115">Bereitstellen einer Java-Anwendung aus einem lokalen Git-Repository</span><span class="sxs-lookup"><span data-stu-id="64401-115">Deploy a Java application from a local Git repo</span></span>

```java
// get the publishing profile from the App Service webapp
PublishingProfile profile = app2.getPublishingProfile();

// create a new Git repo in the sample directory under src/main/resources 
Git git = Git
    .init()
    .setDirectory(new File(ManageWebAppSourceControl.class.getResource("/azure-samples-appservice-helloworld/").getPath()))
    .call();
git.add().addFilepattern(".").call();
// add the files in the sample app to an initial commit
git.commit().setMessage("Initial commit").call(); 

// push the commit using the Azure Git remote URL and credentials in the publishing profile
PushCommand command = git.push();
command.setRemote(profile.gitUrl()); 
command.setCredentialsProvider(new UsernamePasswordCredentialsProvider(profile.gitUsername(), profile.gitPassword()));
command.setRefSpecs(new RefSpec("master:master")); 
command.setForce(true);
command.call();
```      

<span data-ttu-id="64401-116">Dieser Code erstellt unter Verwendung der Bibliotheken vom Typ [JGit](https://eclipse.org/jgit/) ein neues Git-Repository im Ordner `src/main/resources/azure-samples-appservice-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="64401-116">This code uses the [JGit](https://eclipse.org/jgit/) libraries to create a new Git repo in the `src/main/resources/azure-samples-appservice-helloworld` folder.</span></span> <span data-ttu-id="64401-117">Anschließend fügt das Beispiel alle Dateien aus dem Ordner einem anfänglichen Commit hinzu und pusht das Commit unter Verwendung von Git-Bereitstellungsinformationen aus dem Web-App-Element `PublishingProfile` an Azure.</span><span class="sxs-lookup"><span data-stu-id="64401-117">The sample then adds all files in the folder to an initial commit and pushes the commit to Azure using Git deployment information from the webapp's `PublishingProfile`.</span></span> 

>[!NOTE]
> <span data-ttu-id="64401-118">Das Layout der Dateien im Repository muss exakt der gewünschten Bereitstellung der Dateien unter dem Verzeichnis `/site/wwwroot/` in Azure App Service entsprechen.</span><span class="sxs-lookup"><span data-stu-id="64401-118">The layout of the files in the repo must match exactly how you want the files deployed under the `/site/wwwroot/` directory in Azure App Service.</span></span>

## <a name="deploy-an-application-from-a-public-git-repo"></a><span data-ttu-id="64401-119">Bereitstellen einer Anwendung über ein öffentliches Git-Repository</span><span class="sxs-lookup"><span data-stu-id="64401-119">Deploy an application from a public Git repo</span></span>

```java
// deploy a .NET sample app from a public GitHub repo into a new webapp
WebApp app3 = azure.webApps().define(app3Name)
                .withNewResourceGroup(rgName)
                .withExistingAppServicePlan(plan)
                .defineSourceControl()
                .withPublicGitRepository(
                   "https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
                .withBranch("master")
                .attach()
                .create();
 ```

 <span data-ttu-id="64401-120">Das .NET-Projekt wird von der App Service-Laufzeit unter Verwendung des neuesten Codes aus der Verzweigung `master` des Repositorys automatisch erstellt und bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="64401-120">The App Service runtime automatically builds and deploys the .NET project using the latest code on the `master` branch of the repo.</span></span>

## <a name="continuous-deployment-from-a-github-repo"></a><span data-ttu-id="64401-121">Continuous Deployment über ein GitHub-Repository</span><span class="sxs-lookup"><span data-stu-id="64401-121">Continuous deployment from a GitHub repo</span></span>

```java
// deploy the application whenever you push a new commit or merge a pull request into your master branch
WebApp app4 = azure.webApps()
                    .define(app4Name)
                    .withExistingResourceGroup(rgName)
                    .withExistingAppServicePlan(plan)
                    // Uncomment the following lines to turn on continuous deployment scenario
                    //.defineSourceControl()
                    //    .withContinuouslyIntegratedGitHubRepository("username", "reponame")
                    //    .withBranch("master")
                    //    .withGitHubAccessToken("YOUR GITHUB PERSONAL TOKEN")
                    //    .attach()
                    .create();
```  

<span data-ttu-id="64401-122">Die Werte `username` und `reponame` werden in GitHub verwendet.</span><span class="sxs-lookup"><span data-stu-id="64401-122">The `username` and `reponame` values are the ones used in GitHub.</span></span> <span data-ttu-id="64401-123">[Erstellen Sie ein persönliches GitHub-Zugriffstoken](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) mit Repository-Leseberechtigungen, und übergeben Sie es an `withGitHubAccessToken`.</span><span class="sxs-lookup"><span data-stu-id="64401-123">[Create a GitHub personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) with repo read permissions and pass it to `withGitHubAccessToken`.</span></span> 


## <a name="sample-explanation"></a><span data-ttu-id="64401-124">Erläuterung des Beispiels</span><span class="sxs-lookup"><span data-stu-id="64401-124">Sample explanation</span></span>

<span data-ttu-id="64401-125">Das Beispiel erstellt die erste Anwendung unter Verwendung von Java 8 und Tomcat 8, die im Rahmen eines neu erstellten App Service-Plans vom Typ [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="64401-125">The sample creates the first application using Java 8 and Tomcat 8 running in a newly created [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service plan.</span></span> <span data-ttu-id="64401-126">Anschließend wird eine WAR-Datei per FTP und unter Verwendung der Informationen im Objekt `PublishingProfile` übertragen und von Tomcat bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="64401-126">The code then FTPs a WAR file using the information in the `PublishingProfile` object and Tomcat deploys it.</span></span>

<span data-ttu-id="64401-127">Die zweite Anwendung verwendet den gleichen Plan wie die erste und wird ebenfalls als Java 8/Tomcat 8-Anwendung konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="64401-127">The second application uses in the same plan as the first and is also configured as a Java 8/Tomcat 8 application.</span></span> <span data-ttu-id="64401-128">Die JGit-Bibliotheken erstellen ein neues Git-Repository in einem Ordner, der eine entpackte Java-Webanwendung in einer auf App Service abgestimmten Verzeichnisstruktur enthält.</span><span class="sxs-lookup"><span data-stu-id="64401-128">The JGit libraries create a new Git repository in a folder that contains an unpacked Java web application in a directory structure that maps to App Service.</span></span> <span data-ttu-id="64401-129">Ein neuer Commit fügt die Dateien aus dem Ordner dem neuen Git-Repository hinzu, und Git pusht den Commit an Azure – mit einer Remote-URL und einem Benutzernamen/Kennwort aus dem Element `PublishingProfile` der Web-App.</span><span class="sxs-lookup"><span data-stu-id="64401-129">A new commit adds the files in the folder to the new Git repo, and Git pushes the commit to Azure with a remote URL and username/password provided by the webapp's `PublishingProfile`.</span></span>

<span data-ttu-id="64401-130">Die dritte Anwendung ist nicht für Java und Tomcat konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="64401-130">The third application is not configured for Java and Tomcat.</span></span> <span data-ttu-id="64401-131">Stattdessen wird ein .NET-Beispiel aus einem öffentlichen GitHub-Repository direkt über die Quelle bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="64401-131">Instead, a .NET sample in a public GitHub repo is deployed directly from source.</span></span>

<span data-ttu-id="64401-132">Die vierte Anwendung stellt den Code immer dann in Ihrer Hauptverzweigung bereit, wenn Sie Änderungen pushen oder einen Pull Request in der Hauptverzweigung des GitHub-Repositorys zusammenführen.</span><span class="sxs-lookup"><span data-stu-id="64401-132">The fourth application deploys the code in your master branch every time you push changes or merge a pull request into the GitHub repo's master branch.</span></span>

| <span data-ttu-id="64401-133">Im Beispiel verwendete Klasse</span><span class="sxs-lookup"><span data-stu-id="64401-133">Class used in sample</span></span> | <span data-ttu-id="64401-134">Notizen</span><span class="sxs-lookup"><span data-stu-id="64401-134">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="64401-135">WebApp</span><span class="sxs-lookup"><span data-stu-id="64401-135">WebApp</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | <span data-ttu-id="64401-136">Erstellt mithilfe der Fluent-Kette `azure.webApps().define()....create()`.</span><span class="sxs-lookup"><span data-stu-id="64401-136">Created from the `azure.webApps().define()....create()` fluent chain.</span></span> <span data-ttu-id="64401-137">Erstellt eine App Service-Web-App und alle erforderlichen Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="64401-137">Creates a App Service web app and any resources needed for the app.</span></span> <span data-ttu-id="64401-138">Die meisten Methoden fragen Konfigurationsdetails vom Objekt ab. Verbmethoden wie `restart()` ändern hingegen den Zustand der Web-App.</span><span class="sxs-lookup"><span data-stu-id="64401-138">Most methods query the object for configuration details, but verb methods like `restart()` change the state of the webapp.</span></span>
| [<span data-ttu-id="64401-139">WebContainer</span><span class="sxs-lookup"><span data-stu-id="64401-139">WebContainer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | <span data-ttu-id="64401-140">Klasse mit statischen öffentlichen Feldern, die beim Definieren einer in einem Java-Webcontainer ausgeführten Web-App als Parameter für `withWebContainer()` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="64401-140">Class with static public fields used as paramters to `withWebContainer()` when defining a WebApp running a Java webcontainer.</span></span> <span data-ttu-id="64401-141">Verfügt über Optionen für Tomcat- und Jetty-Versionen.</span><span class="sxs-lookup"><span data-stu-id="64401-141">Has choices for both Jetty and Tomcat versions.</span></span>
| [<span data-ttu-id="64401-142">PublishingProfile</span><span class="sxs-lookup"><span data-stu-id="64401-142">PublishingProfile</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | <span data-ttu-id="64401-143">Wird über ein WebApp-Objekt mithilfe der Methode `getPublishingProfile()` abgerufen.</span><span class="sxs-lookup"><span data-stu-id="64401-143">Obtained through a WebApp object using the `getPublishingProfile()` method.</span></span> <span data-ttu-id="64401-144">Enthält FTP- und Git-Bereitstellungsinformationen – einschließlich Benutzername und Kennwort für die Bereitstellung (unabhängig von den Anmeldeinformationen für das Azure-Konto oder für den Dienstprinzipal).</span><span class="sxs-lookup"><span data-stu-id="64401-144">Contains FTP and Git deployment information, including deployment username and password (which is separate from Azure account or service principal credentials).</span></span>
| [<span data-ttu-id="64401-145">AppServicePlan</span><span class="sxs-lookup"><span data-stu-id="64401-145">AppServicePlan</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | <span data-ttu-id="64401-146">Wird von `azure.appServices().appServicePlans().getByResourceGroup()` zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="64401-146">Returned by `azure.appServices().appServicePlans().getByResourceGroup()`.</span></span> <span data-ttu-id="64401-147">Mit den verfügbaren Methoden können Sie die Kapazität, den Tarif und die Anzahl von Web-Apps überprüfen, die unter dem Plan ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="64401-147">Methods are availble to check the capacity, tier, and number of web apps running in the plan.</span></span>
| [<span data-ttu-id="64401-148">AppServicePricingTier</span><span class="sxs-lookup"><span data-stu-id="64401-148">AppServicePricingTier</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | <span data-ttu-id="64401-149">Klasse mit statischen öffentlichen Feldern, die App Service-Ebenen darstellen.</span><span class="sxs-lookup"><span data-stu-id="64401-149">Class with static public fields representing App Service tiers.</span></span> <span data-ttu-id="64401-150">Dient zum Definieren eines Plantarifs – entweder inline im Zuge der App-Erstellung mit `withPricingTier()` oder direkt beim Definieren eines Plans über `azure.appServices().appServicePlans().define()`.</span><span class="sxs-lookup"><span data-stu-id="64401-150">Used to define a plan tier in-line during app creation with `withPricingTier()` or directly when defining a plan via `azure.appServices().appServicePlans().define()`</span></span>
| [<span data-ttu-id="64401-151">JavaVersion</span><span class="sxs-lookup"><span data-stu-id="64401-151">JavaVersion</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | <span data-ttu-id="64401-152">Klasse mit statischen öffentlichen Feldern, die von App Service unterstützte Java-Versionen darstellen.</span><span class="sxs-lookup"><span data-stu-id="64401-152">Class with static public fields representing Java versions supported by App Service.</span></span> <span data-ttu-id="64401-153">Wird beim Erstellen einer neuen Web-App im Rahmen der Kette `define()...create()` mit `withJavaVersion()` verwendet.</span><span class="sxs-lookup"><span data-stu-id="64401-153">Used with `withJavaVersion()` during the `define()...create()` chain when creating a new webapp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64401-154">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="64401-154">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]