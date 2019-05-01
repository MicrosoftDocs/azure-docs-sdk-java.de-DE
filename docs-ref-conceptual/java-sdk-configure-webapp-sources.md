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
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a>Konfigurieren von Azure App Service-Bereitstellungsquellen über Ihre Java-Anwendungen

[Dieses Beispiel](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) stellt Code für vier Anwendungen in einem einzelnen [Azure App Service](https://docs.microsoft.com/azure/app-service/)-Plan bereit, die jeweils eine andere Bereitstellungsquelle verwenden.

## <a name="run-the-sample"></a>Ausführen des Beispiels

Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest. Führen Sie anschließend Folgendes aus:

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

Sehen Sie sich den [vollständigen Beispielcode auf GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java) an.

## <a name="authenticate-with-azure"></a>Authentifizieren über Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a>Erstellen einer App Service-App, die Apache Tomcat ausführt

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

`withJavaVersion()` und `withWebContainer()` konfigurieren App Service für die Bereitstellung von HTTP-Anforderungen unter Verwendung von Tomcat 8.

## <a name="deploy-a-java-application-using-ftp"></a>Bereitstellen einer Java-Anwendung unter Verwendung von FTP
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

Dieser Code lädt eine WAR-Datei in das Verzeichnis `/site/wwwroot/webapps` hoch. Tomcat stellt WAR-Dateien aus diesem Verzeichnis standardmäßig in App Service bereit.

## <a name="deploy-a-java-application-from-a-local-git-repo"></a>Bereitstellen einer Java-Anwendung aus einem lokalen Git-Repository

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

Dieser Code erstellt unter Verwendung der Bibliotheken vom Typ [JGit](https://eclipse.org/jgit/) ein neues Git-Repository im Ordner `src/main/resources/azure-samples-appservice-helloworld`. Anschließend fügt das Beispiel alle Dateien aus dem Ordner einem anfänglichen Commit hinzu und pusht das Commit unter Verwendung von Git-Bereitstellungsinformationen aus dem Web-App-Element `PublishingProfile` an Azure. 

>[!NOTE]
> Das Layout der Dateien im Repository muss exakt der gewünschten Bereitstellung der Dateien unter dem Verzeichnis `/site/wwwroot/` in Azure App Service entsprechen.

## <a name="deploy-an-application-from-a-public-git-repo"></a>Bereitstellen einer Anwendung über ein öffentliches Git-Repository

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

 Das .NET-Projekt wird von der App Service-Laufzeit unter Verwendung des neuesten Codes aus der Verzweigung `master` des Repositorys automatisch erstellt und bereitgestellt.

## <a name="continuous-deployment-from-a-github-repo"></a>Continuous Deployment über ein GitHub-Repository

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

Die Werte `username` und `reponame` werden in GitHub verwendet. [Erstellen Sie ein persönliches GitHub-Zugriffstoken](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) mit Repository-Leseberechtigungen, und übergeben Sie es an `withGitHubAccessToken`. 


## <a name="sample-explanation"></a>Erläuterung des Beispiels

Das Beispiel erstellt die erste Anwendung unter Verwendung von Java 8 und Tomcat 8, die im Rahmen eines neu erstellten App Service-Plans vom Typ [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) ausgeführt werden. Anschließend wird eine WAR-Datei per FTP und unter Verwendung der Informationen im Objekt `PublishingProfile` übertragen und von Tomcat bereitgestellt.

Die zweite Anwendung verwendet den gleichen Plan wie die erste und wird ebenfalls als Java 8/Tomcat 8-Anwendung konfiguriert. Die JGit-Bibliotheken erstellen ein neues Git-Repository in einem Ordner, der eine entpackte Java-Webanwendung in einer auf App Service abgestimmten Verzeichnisstruktur enthält. Ein neuer Commit fügt die Dateien aus dem Ordner dem neuen Git-Repository hinzu, und Git pusht den Commit an Azure – mit einer Remote-URL und einem Benutzernamen/Kennwort aus dem Element `PublishingProfile` der Web-App.

Die dritte Anwendung ist nicht für Java und Tomcat konfiguriert. Stattdessen wird ein .NET-Beispiel aus einem öffentlichen GitHub-Repository direkt über die Quelle bereitgestellt.

Die vierte Anwendung stellt den Code immer dann in Ihrer Hauptverzweigung bereit, wenn Sie Änderungen pushen oder einen Pull Request in der Hauptverzweigung des GitHub-Repositorys zusammenführen.

| Im Beispiel verwendete Klasse | Notizen
|-------|-------|
| [WebApp](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | Erstellt mithilfe der Fluent-Kette `azure.webApps().define()....create()`. Erstellt eine App Service-Web-App und alle erforderlichen Ressourcen. Die meisten Methoden fragen Konfigurationsdetails vom Objekt ab. Verbmethoden wie `restart()` ändern hingegen den Zustand der Web-App.
| [WebContainer](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | Klasse mit statischen öffentlichen Feldern, die beim Definieren einer in einem Java-Webcontainer ausgeführten Web-App als Parameter für `withWebContainer()` verwendet werden. Verfügt über Optionen für Tomcat- und Jetty-Versionen.
| [PublishingProfile](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | Wird über ein WebApp-Objekt mithilfe der Methode `getPublishingProfile()` abgerufen. Enthält FTP- und Git-Bereitstellungsinformationen – einschließlich Benutzername und Kennwort für die Bereitstellung (unabhängig von den Anmeldeinformationen für das Azure-Konto oder für den Dienstprinzipal).
| [AppServicePlan](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | Wird von `azure.appServices().appServicePlans().getByResourceGroup()` zurückgegeben. Mit den verfügbaren Methoden können Sie die Kapazität, den Tarif und die Anzahl von Web-Apps überprüfen, die unter dem Plan ausgeführt werden.
| [AppServicePricingTier](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | Klasse mit statischen öffentlichen Feldern, die App Service-Ebenen darstellen. Dient zum Definieren eines Plantarifs – entweder inline im Zuge der App-Erstellung mit `withPricingTier()` oder direkt beim Definieren eines Plans über `azure.appServices().appServicePlans().define()`.
| [JavaVersion](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | Klasse mit statischen öffentlichen Feldern, die von App Service unterstützte Java-Versionen darstellen. Wird beim Erstellen einer neuen Web-App im Rahmen der Kette `define()...create()` mit `withJavaVersion()` verwendet.

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [next-steps](includes/java-next-steps.md)]