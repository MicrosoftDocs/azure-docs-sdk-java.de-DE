---
title: Verwenden von Spring und Azure Cosmos DB mit App Service für Linux
description: In diesem Artikel erfahren Sie Schritt für Schritt, wie Sie Java-Web-Apps in Azure App Service für Linux erstellen, konfigurieren, bereitstellen, skalieren und Probleme behandeln.
documentationcenter: java
author: bmitchell287
ms.author: brendm; joshuapa
ms.date: 4/24/2019
ms.devlang: java
ms.service: app-service, cosmos-db
ms.topic: article
ms.openlocfilehash: 5d209c0670d6f4265b1237e7b8cff45faa9bb5d8
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568633"
---
# <a name="how-to-use-spring-and-cosmos-db-with-app-service-on-linux"></a><span data-ttu-id="7f70c-103">Verwenden von Spring und Azure Cosmos DB mit App Service für Linux</span><span class="sxs-lookup"><span data-stu-id="7f70c-103">How to use Spring and Cosmos DB with App Service on Linux</span></span>

## <a name="overview"></a><span data-ttu-id="7f70c-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="7f70c-104">Overview</span></span>

<span data-ttu-id="7f70c-105">In diesem Artikel erfahren Sie Schritt für Schritt, wie Sie Java-Web-Apps in Azure App Service für Linux erstellen, konfigurieren, bereitstellen, skalieren und Probleme behandeln.</span><span class="sxs-lookup"><span data-stu-id="7f70c-105">This article will walk you through the process of building, configuring, deploying, troubleshooting, and scaling Java Web apps in Azure App Service on Linux.</span></span>

<span data-ttu-id="7f70c-106">Dabei wird die Verwendung folgender Komponenten veranschaulicht:</span><span class="sxs-lookup"><span data-stu-id="7f70c-106">It will demonstrate the usage of the following components:</span></span>

- [<span data-ttu-id="7f70c-107">Spring Boot Starter mit der SQL-API von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7f70c-107">Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>](configure-spring-boot-starter-java-app-with-cosmos-db.md)
- [<span data-ttu-id="7f70c-108">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7f70c-108">Azure Cosmos DB</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-introduction)
- [<span data-ttu-id="7f70c-109">App Service (Linux)</span><span class="sxs-lookup"><span data-stu-id="7f70c-109">App Service Linux</span></span>](https://docs.microsoft.com/en-us/azure/app-service/containers/app-service-linux-intro)

## <a name="prerequisites"></a><span data-ttu-id="7f70c-110">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="7f70c-110">Prerequisites</span></span>

<span data-ttu-id="7f70c-111">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="7f70c-111">The following prerequisites are required in order to follow the steps in this article:</span></span>

- <span data-ttu-id="7f70c-112">Sie benötigen ein Azure-Abonnement, um eine Java-Web-App in der Cloud bereitstellen zu können.</span><span class="sxs-lookup"><span data-stu-id="7f70c-112">In order to deploy a Java Web app to cloud, you need an Azure subscription.</span></span> <span data-ttu-id="7f70c-113">Falls Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) aktivieren oder sich für ein [kostenloses Azure-Konto]((https://azure.microsoft.com/pricing/free-trial/)) registrieren.</span><span class="sxs-lookup"><span data-stu-id="7f70c-113">If you do not already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account]((https://azure.microsoft.com/pricing/free-trial/)).</span></span>
- [<span data-ttu-id="7f70c-114">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7f70c-114">Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
- [<span data-ttu-id="7f70c-115">Java 8 JDK</span><span class="sxs-lookup"><span data-stu-id="7f70c-115">Java 8 JDK</span></span>](https://docs.microsoft.com/java/azure/jdk/java-jdk-install)
- [<span data-ttu-id="7f70c-116">Maven 3</span><span class="sxs-lookup"><span data-stu-id="7f70c-116">Maven 3</span></span>](http://maven.apache.org/)

## <a name="clone-the-sample-java-web-app-repository"></a><span data-ttu-id="7f70c-117">Klonen des Repositorys für die exemplarische Java-Web-App</span><span class="sxs-lookup"><span data-stu-id="7f70c-117">Clone the Sample Java Web App Repository</span></span>
<span data-ttu-id="7f70c-118">In dieser Übung wird die Spring-Todo-App verwendet. Hierbei handelt es sich um eine Java-Anwendung, die mit [Spring Boot](https://spring.io/projects/spring-boot), [Spring Data für Cosmos DB](https://docs.microsoft.com/en-us/java/azure/spring-framework/configure-spring-boot-starter-java-app-with-cosmos-db?view=azure-java-stable) und [Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-introduction) erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7f70c-118">For this exercise you'll be using the Spring Todo app, which is a Java application built using [Spring Boot](https://spring.io/projects/spring-boot), [Spring Data for Cosmos DB](https://docs.microsoft.com/en-us/java/azure/spring-framework/configure-spring-boot-starter-java-app-with-cosmos-db?view=azure-java-stable) and [Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-introduction).</span></span>
1. <span data-ttu-id="7f70c-119">Klonen Sie die Spring-Todo-App, und kopieren Sie den Inhalt des Ordners **.prep**, um das Projekt zu initialisieren:</span><span class="sxs-lookup"><span data-stu-id="7f70c-119">Clone the Spring Todo app and copy the contents of the **.prep** folder to initialize the project:</span></span>

    <span data-ttu-id="7f70c-120">Bash:</span><span class="sxs-lookup"><span data-stu-id="7f70c-120">For bash:</span></span>
    ```bash
    git clone --recurse-submodules https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2.git
    yes | cp -rf .prep/* .
    ```

    <span data-ttu-id="7f70c-121">Windows:</span><span class="sxs-lookup"><span data-stu-id="7f70c-121">For Windows:</span></span>
    ```cmd
    git clone --recurse-submodules https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2.git
    cd e2e-java-experience-in-app-service-linux-part-2
    xcopy .prep /f /s /e /y
    ```

2. <span data-ttu-id="7f70c-122">Ändern Sie das Verzeichnis in den folgenden Ordner des geklonten Repositorys:</span><span class="sxs-lookup"><span data-stu-id="7f70c-122">Change the directory to the following folder in the cloned repo:</span></span>

   ```bash
   cd initial\spring-todo-app
   ``` 
## <a name="create-an-azure-cosmos-db-from-azure-cli"></a><span data-ttu-id="7f70c-123">Erstellen einer Azure Cosmos DB-Instanz über die Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="7f70c-123">Create an Azure Cosmos DB from Azure CLI</span></span>

1. <span data-ttu-id="7f70c-124">Melden Sie sich bei Ihrer Azure-Befehlszeilenschnittstelle an, und legen Sie Ihre Abonnement-ID fest.</span><span class="sxs-lookup"><span data-stu-id="7f70c-124">Login to your Azure CLI, and set your subscription id.</span></span>

    ```bash
    az login
    ```

2. <span data-ttu-id="7f70c-125">Legen Sie bei Bedarf die Abonnement-ID fest.</span><span class="sxs-lookup"><span data-stu-id="7f70c-125">Set the subscription id if needed.</span></span>
    ```bash
    az account set -s <your-subscription-id>
    ```

3. <span data-ttu-id="7f70c-126">Erstellen Sie eine Azure-Ressourcengruppe, und notieren Sie sich den Namen der Ressourcengruppe für später.</span><span class="sxs-lookup"><span data-stu-id="7f70c-126">Create an Azure resource group, and write down the resource group name for later use.</span></span>

    ```bash
    az group create -n <your-azure-group-name> \
    -l <your-resource-group-region>
    ```

4. <span data-ttu-id="7f70c-127">Erstellen Sie die Cosmos DB-Instanz, und geben Sie als Typ „GlobalDocumentDB“ an.</span><span class="sxs-lookup"><span data-stu-id="7f70c-127">Create the Cosmos DB and specify the type as GlobalDocumentDB.</span></span>
<span data-ttu-id="7f70c-128">Der Name der Cosmos DB-Instanz darf nur Kleinbuchstaben enthalten.</span><span class="sxs-lookup"><span data-stu-id="7f70c-128">The name of the Cosmos DB must use only lower case letters.</span></span> <span data-ttu-id="7f70c-129">Notieren Sie sich den Wert des Felds `documentEndpoint` aus der Antwort.</span><span class="sxs-lookup"><span data-stu-id="7f70c-129">Make sure to note the `documentEndpoint` field in the response.</span></span> <span data-ttu-id="7f70c-130">Er wird später noch benötigt.</span><span class="sxs-lookup"><span data-stu-id="7f70c-130">You'll need this later.</span></span>

    ```bash
    az cosmosdb create --kind GlobalDocumentDB \
        -g <your-azure-group-name> \
        -n <your-azure-COSMOS-DB-name-in-lower-case-letters>
     ```

4. <span data-ttu-id="7f70c-131">Rufen Sie Ihre Azure Cosmos DB-Schlüssel ab, und notieren Sie sich den Wert `primaryMasterKey` für später.</span><span class="sxs-lookup"><span data-stu-id="7f70c-131">Get your Azure Cosmos DB keys, record the `primaryMasterKey` value for later use.</span></span>

    ```bash
    az cosmosdb list-keys -g <your-azure-group-name> -n <your-azure-COSMOSDB-name>
    ```

## <a name="build-and-run-the-app-locally"></a><span data-ttu-id="7f70c-132">Lokales Erstellen und Ausführen der App</span><span class="sxs-lookup"><span data-stu-id="7f70c-132">Build and Run the App Locally</span></span>

1. <span data-ttu-id="7f70c-133">Konfigurieren Sie innerhalb Ihrer bevorzugten Konsole die Umgebungsvariablen aus den folgenden Codeabschnitten mit den Azure- und Cosmos DB-Verbindungsinformationen, die Sie weiter oben in diesem Artikel gesammelt haben.</span><span class="sxs-lookup"><span data-stu-id="7f70c-133">Within your console of choice configure the environment variables shown in the following code sections with the Azure and Cosmos DB connection information you gathered previously in this article.</span></span> <span data-ttu-id="7f70c-134">Geben Sie einen eindeutigen Namen für **WEBAPP_NAME** und einen Wert für **REGION** an.</span><span class="sxs-lookup"><span data-stu-id="7f70c-134">You'll need to provide a unique name for **WEBAPP_NAME** and value for the **REGION** variables.</span></span>

<span data-ttu-id="7f70c-135">Linux (Bash):</span><span class="sxs-lookup"><span data-stu-id="7f70c-135">For Linux (Bash):</span></span>

```bash
export COSMOSDB_URI=<put-your-COSMOS-DB-documentEndpoint-URI-here>
export COSMOSDB_KEY=<put-your-COSMOS-DB-primaryMasterKey-here>
export COSMOSDB_DBNAME=<put-your-COSMOS-DB-name-here>
export RESOURCEGROUP_NAME=<put-your-resource-group-name-here>
export WEBAPP_NAME=<put-your-Webapp-name-here>
export REGION=<put-your-REGION-here>
```

<span data-ttu-id="7f70c-136">Windows (Eingabeaufforderung):</span><span class="sxs-lookup"><span data-stu-id="7f70c-136">For Windows (Command Prompt):</span></span>
```cmd
set COSMOSDB_URI=<put-your-COSMOS-DB-documentEndpoint-URI-here>
set COSMOSDB_KEY=<put-your-COSMOS-DB-primaryMasterKey-here>
set COSMOSDB_DBNAME=<put-your-COSMOS-DB-name-here>
set RESOURCEGROUP_NAME=<put-your-resource-group-name-here>
set WEBAPP_NAME=<put-your-Webapp-name-here>
set REGION=<put-your-REGION-here>
```

> [!NOTE]
> <span data-ttu-id="7f70c-137">Falls Sie diese Variablen mit einem Skript bereitstellen möchten, finden Sie im Verzeichnis „.prep“ eine Vorlage für Bash, die Sie kopieren und als Grundlage verwenden können.</span><span class="sxs-lookup"><span data-stu-id="7f70c-137">If you'd like to provision these variables with a script, there is a template for Bash in the .prep directory that you can copy and use as a starting point.</span></span>

2. <span data-ttu-id="7f70c-138">Ändern Sie das Verzeichnis wie folgt:</span><span class="sxs-lookup"><span data-stu-id="7f70c-138">Change the directory to the following:</span></span>

    ```bash
    cd initial/spring-todo-app
    ``` 
 
3. <span data-ttu-id="7f70c-139">Führen Sie die Spring-Todo-App mithilfe des folgenden Befehls lokal aus:</span><span class="sxs-lookup"><span data-stu-id="7f70c-139">Run the Spring Todo app locally with the following command:</span></span>

    ```bash
    mvn package spring-boot:run
    ```

4. <span data-ttu-id="7f70c-140">Nachdem die Anwendung gestartet wurde, können Sie die Bereitstellung überprüfen, indem Sie unter [http://localhost:8080/](http://localhost:8080/) auf die Spring-Todo-App zugreifen.</span><span class="sxs-lookup"><span data-stu-id="7f70c-140">Once the application has started,you can validate the deployment by accessing the Spring Todo app here: [http://localhost:8080/](http://localhost:8080/).</span></span>

 ![Lokal ausgeführte Spring-App][SCDB01]

## <a name="deploy-to-app-service-linux"></a><span data-ttu-id="7f70c-142">Bereitstellen für App Service (Linux)</span><span class="sxs-lookup"><span data-stu-id="7f70c-142">Deploy to App Service Linux</span></span>

1. <span data-ttu-id="7f70c-143">Öffnen Sie die Datei „pom.xml“, die Sie zuvor in das Verzeichnis **initial/spring-todo-app** des Repositorys kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="7f70c-143">Open the pom.xml file that you previously copied to the **initial/spring-todo-app** directory of the repository.</span></span> <span data-ttu-id="7f70c-144">Vergewissern Sie sich, dass das [Maven-Plug-In für Azure App Service](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-webapp-maven-plugin/README.md) enthalten ist, wie weiter unten in der Datei „pom.xml“ zu sehen.</span><span class="sxs-lookup"><span data-stu-id="7f70c-144">Ensure that the [Maven Plugin for Azure App Service](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-webapp-maven-plugin/README.md) is included as seen in the pom.xml file below.</span></span> <span data-ttu-id="7f70c-145">Sollte die Version nicht auf **1.6.0** festgelegt sein, aktualisieren Sie den Wert.</span><span class="sxs-lookup"><span data-stu-id="7f70c-145">If the version is not set to **1.6.0** then update the value.</span></span>

```xml
<plugins> 

    <!--*************************************************-->
    <!-- Deploy to Java SE in App Service Linux           -->
    <!--*************************************************-->
       
    <plugin>
        <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-webapp-maven-plugin</artifactId>
            <version>1.6.0</version>
            <configuration>
            <deploymentType>jar</deploymentType>
            
            <!-- Web App information -->
            <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
            <appName>${WEBAPP_NAME}</appName>
            <region>${REGION}</region>
            
            <!-- Java Runtime Stack for Web App on Linux-->
            <linuxRuntime>jre8</linuxRuntime>
            
            <appSettings>
                <property>
                    <name>COSMOSDB_URI</name>
                    <value>${COSMOSDB_URI}</value>
                </property>
                <property>
                    <name>COSMOSDB_KEY</name>
                    <value>${COSMOSDB_KEY}</value>
                </property>
                <property>
                    <name>COSMOSDB_DBNAME</name>
                    <value>${COSMOSDB_DBNAME}</value>
                </property>
                <property>
                    <name>JAVA_OPTS</name>
                    <value>-Dserver.port=80</value>
                </property>
            </appSettings>
            
        </configuration>
    </plugin>            
    ...
</plugins>
```

2. <span data-ttu-id="7f70c-146">Führen Sie die Bereitstellung für Java SE in App Service (Linux) durch.</span><span class="sxs-lookup"><span data-stu-id="7f70c-146">Deploy to Java SE in App Service Linux</span></span>

    ```bash
    mvn azure-webapp:deploy
    ```

```bash
// Deploy
bash-3.2$ mvn azure-webapp:deploy
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-todo-app 2.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- azure-webapp-maven-plugin:1.6.0:deploy (default-cli) @ spring-todo-app ---
[INFO] Authenticate with Azure CLI 2.0
[INFO] Target Web App doesnt exist. Creating a new one...
[INFO] Creating App Service Plan 'ServicePlan11111111-1111-1111'...
[INFO] Successfully created App Service Plan.
[INFO] Successfully created Web App.
[INFO] Trying to deploy artifact to spring-todo-app...
[INFO] Successfully deployed the artifact to https://spring-todo-app.azurewebsites.net
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 02:19 min
[INFO] Finished at: 2018-10-28T15:32:03-07:00
[INFO] Final Memory: 50M/574M
[INFO] ------------------------------------------------------------------------
```

3. <span data-ttu-id="7f70c-147">Navigieren Sie zu Ihrer Web-App, die unter Java SE in App Service (Linux) ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="7f70c-147">Browse to your web app running on Java SE in App Service Linux:</span></span>

    ```bash
    https://<WEBAPP_NAME>.azurewebsites.net
    ```

![In App Service unter Linux ausgeführte Spring-App][SCDB02]

## <a name="troubleshoot-spring-todo-app-on-azure-by-viewing-logs"></a><span data-ttu-id="7f70c-149">Behandeln von Problemen mit der Spring-Todo-App in Azure anhand von Protokollen</span><span class="sxs-lookup"><span data-stu-id="7f70c-149">Troubleshoot Spring Todo App on Azure by Viewing Logs</span></span>

1. <span data-ttu-id="7f70c-150">Konfigurieren Sie Protokolle für die bereitgestellte Java-Web-App in Azure App Service unter Linux:</span><span class="sxs-lookup"><span data-stu-id="7f70c-150">Configure logs for the deployed Java Web app in Azure App Service in Linux:</span></span>

    ```bash
    az webapp log config --name ${WEBAPP_NAME} \
     --resource-group ${RESOURCEGROUP_NAME} \
     --web-server-logging filesystem
    ```
2. <span data-ttu-id="7f70c-151">Öffnen Sie den Remoteprotokollstream der Java-Web-App von einem lokalen Computer aus:</span><span class="sxs-lookup"><span data-stu-id="7f70c-151">Open Java Web app remote log stream from a local machine:</span></span>

    ```bash
    az webapp log tail --name ${WEBAPP_NAME} \
     --resource-group ${RESOURCEGROUP_NAME}
     ```

```bash
bash-3.2$ az webapp log tail --name ${WEBAPP_NAME}  --resource-group ${RESOURCEGROUP_NAME}
2018-10-28T22:50:17  Welcome, you are now connected to log-streaming service.
2018-10-28T22:44:56.265890407Z   _____                               
2018-10-28T22:44:56.265930308Z   /  _  \ __________ _________   ____  
2018-10-28T22:44:56.265936008Z  /  /_\  \___   /  |  \_  __ \_/ __ \ 
2018-10-28T22:44:56.265940308Z /    |    \/    /|  |  /|  | \/\  ___/ 
2018-10-28T22:44:56.265944408Z \____|__  /_____ \____/ |__|    \___  >
2018-10-28T22:44:56.265948508Z         \/      \/                  \/ 
2018-10-28T22:44:56.265952508Z A P P   S E R V I C E   O N   L I N U X
2018-10-28T22:44:56.265956408Z Documentation: http://aka.ms/webapp-linux
2018-10-28T22:44:56.266260910Z Setup openrc ...
2018-10-28T22:44:57.396926506Z Service `hwdrivers needs non existent service dev
2018-10-28T22:44:57.397294409Z  * Caching service dependencies ... [ ok ]
2018-10-28T22:44:57.474152273Z Starting ssh service...
...
...
2018-10-28T22:46:13.432160734Z [INFO] AnnotationMBeanExporter - Registering beans for JMX exposure on startup
2018-10-28T22:46:13.744859424Z [INFO] TomcatWebServer - Tomcat started on port(s): 80 (http) with context path ''
2018-10-28T22:46:13.783230205Z [INFO] TodoApplication - Started TodoApplication in 57.209 seconds (JVM running for 70.815)
2018-10-28T22:46:14.887366993Z 2018-10-28 22:46:14.887  INFO 198 --- [p-nio-80-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring FrameworkServlet 'dispatcherServlet'
2018-10-28T22:46:14.887637695Z [INFO] DispatcherServlet - FrameworkServlet 'dispatcherServlet': initialization started
2018-10-28T22:46:14.998479907Z [INFO] DispatcherServlet - FrameworkServlet 'dispatcherServlet': initialization completed in 111 ms

2018-10-28T22:49:20.572059062Z Sun Oct 28 22:49:20 GMT 2018 GET ======= /api/todolist =======
2018-10-28T22:49:25.850543080Z Sun Oct 28 22:49:25 GMT 2018 DELETE ======= /api/todolist/{4f41ab03-1b12-4131-a920-fe5dfec106ca} ======= 
2018-10-28T22:49:26.047126614Z Sun Oct 28 22:49:26 GMT 2018 GET ======= /api/todolist =======
2018-10-28T22:49:30.201740227Z Sun Oct 28 22:49:30 GMT 2018 POST ======= /api/todolist ======= Milk
2018-10-28T22:49:30.413468872Z Sun Oct 28 22:49:30 GMT 2018 GET ======= /api/todolist =======


```

3. <span data-ttu-id="7f70c-152">Anschließend können Sie Ihre Ergebnisse anhand des Codes in [e2e-java-experience-in-app-service-linux-part-2/complete](https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2/tree/master/complete) überprüfen.</span><span class="sxs-lookup"><span data-stu-id="7f70c-152">When you are finished, you can check your results against the code in [e2e-java-experience-in-app-service-linux-part-2/complete](https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2/tree/master/complete).</span></span>


## <a name="scale-out-the-spring-todo-app"></a><span data-ttu-id="7f70c-153">Erweitern der Spring-Todo-App</span><span class="sxs-lookup"><span data-stu-id="7f70c-153">Scale out the Spring Todo App</span></span>

1. <span data-ttu-id="7f70c-154">Erweitern Sie die Java-Web-App über die Azure-Befehlszeilenschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="7f70c-154">Scale out Java Web app using Azure CLI:</span></span>

    ```bash
    az appservice plan update --number-of-workers 2 \
      --name ${WEBAPP_PLAN_NAME} \
      --resource-group ${RESOURCEGROUP_NAME}
    ```

## <a name="next-steps"></a><span data-ttu-id="7f70c-155">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="7f70c-155">Next steps</span></span>

- [<span data-ttu-id="7f70c-156">Java-Entwicklerleitfaden für App Service unter Linux</span><span class="sxs-lookup"><span data-stu-id="7f70c-156">Java in App Service Linux dev guide</span></span>](https://docs.microsoft.com/en-us/azure/app-service/containers/app-service-linux-java)
- <span data-ttu-id="7f70c-157">[Azure für Java-Entwickler](https://docs.microsoft.com/en-us/java/azure/): Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="7f70c-157">[Azure for Java Developers](https://docs.microsoft.com/en-us/java/azure/) To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f70c-158">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="7f70c-158">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="7f70c-159">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7f70c-159">Additional Resources</span></span>

<span data-ttu-id="7f70c-160">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="7f70c-160">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="7f70c-161">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7f70c-161">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="7f70c-162">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7f70c-162">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="7f70c-163">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="7f70c-163">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="7f70c-164">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="7f70c-164">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="7f70c-165">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="7f70c-165">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="7f70c-166">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="7f70c-166">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="7f70c-167">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="7f70c-167">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure für Java-Entwickler]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot Document DB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: https://azure.microsoft.com/services/devops/java/ (Arbeiten mit Azure DevOps und Java)
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SCDB01]: ./media/configure-spring-app-with-cosmos-db-on-app-service-linux/SCDB01.png
[SCDB02]: ./media/configure-spring-app-with-cosmos-db-on-app-service-linux/SCDB02.png
