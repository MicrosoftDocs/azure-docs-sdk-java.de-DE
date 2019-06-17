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
# <a name="how-to-use-spring-and-cosmos-db-with-app-service-on-linux"></a>Verwenden von Spring und Azure Cosmos DB mit App Service für Linux

## <a name="overview"></a>Übersicht

In diesem Artikel erfahren Sie Schritt für Schritt, wie Sie Java-Web-Apps in Azure App Service für Linux erstellen, konfigurieren, bereitstellen, skalieren und Probleme behandeln.

Dabei wird die Verwendung folgender Komponenten veranschaulicht:

- [Spring Boot Starter mit der SQL-API von Azure Cosmos DB](configure-spring-boot-starter-java-app-with-cosmos-db.md)
- [Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-introduction)
- [App Service (Linux)](https://docs.microsoft.com/en-us/azure/app-service/containers/app-service-linux-intro)

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

- Sie benötigen ein Azure-Abonnement, um eine Java-Web-App in der Cloud bereitstellen zu können. Falls Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) aktivieren oder sich für ein [kostenloses Azure-Konto]((https://azure.microsoft.com/pricing/free-trial/)) registrieren.
- [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
- [Java 8 JDK](https://docs.microsoft.com/java/azure/jdk/java-jdk-install)
- [Maven 3](http://maven.apache.org/)

## <a name="clone-the-sample-java-web-app-repository"></a>Klonen des Repositorys für die exemplarische Java-Web-App
In dieser Übung wird die Spring-Todo-App verwendet. Hierbei handelt es sich um eine Java-Anwendung, die mit [Spring Boot](https://spring.io/projects/spring-boot), [Spring Data für Cosmos DB](https://docs.microsoft.com/en-us/java/azure/spring-framework/configure-spring-boot-starter-java-app-with-cosmos-db?view=azure-java-stable) und [Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-introduction) erstellt wurde.
1. Klonen Sie die Spring-Todo-App, und kopieren Sie den Inhalt des Ordners **.prep**, um das Projekt zu initialisieren:

    Bash:
    ```bash
    git clone --recurse-submodules https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2.git
    yes | cp -rf .prep/* .
    ```

    Windows:
    ```cmd
    git clone --recurse-submodules https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2.git
    cd e2e-java-experience-in-app-service-linux-part-2
    xcopy .prep /f /s /e /y
    ```

2. Ändern Sie das Verzeichnis in den folgenden Ordner des geklonten Repositorys:

   ```bash
   cd initial\spring-todo-app
   ``` 
## <a name="create-an-azure-cosmos-db-from-azure-cli"></a>Erstellen einer Azure Cosmos DB-Instanz über die Azure-Befehlszeilenschnittstelle

1. Melden Sie sich bei Ihrer Azure-Befehlszeilenschnittstelle an, und legen Sie Ihre Abonnement-ID fest.

    ```bash
    az login
    ```

2. Legen Sie bei Bedarf die Abonnement-ID fest.
    ```bash
    az account set -s <your-subscription-id>
    ```

3. Erstellen Sie eine Azure-Ressourcengruppe, und notieren Sie sich den Namen der Ressourcengruppe für später.

    ```bash
    az group create -n <your-azure-group-name> \
    -l <your-resource-group-region>
    ```

4. Erstellen Sie die Cosmos DB-Instanz, und geben Sie als Typ „GlobalDocumentDB“ an.
Der Name der Cosmos DB-Instanz darf nur Kleinbuchstaben enthalten. Notieren Sie sich den Wert des Felds `documentEndpoint` aus der Antwort. Er wird später noch benötigt.

    ```bash
    az cosmosdb create --kind GlobalDocumentDB \
        -g <your-azure-group-name> \
        -n <your-azure-COSMOS-DB-name-in-lower-case-letters>
     ```

4. Rufen Sie Ihre Azure Cosmos DB-Schlüssel ab, und notieren Sie sich den Wert `primaryMasterKey` für später.

    ```bash
    az cosmosdb list-keys -g <your-azure-group-name> -n <your-azure-COSMOSDB-name>
    ```

## <a name="build-and-run-the-app-locally"></a>Lokales Erstellen und Ausführen der App

1. Konfigurieren Sie innerhalb Ihrer bevorzugten Konsole die Umgebungsvariablen aus den folgenden Codeabschnitten mit den Azure- und Cosmos DB-Verbindungsinformationen, die Sie weiter oben in diesem Artikel gesammelt haben. Geben Sie einen eindeutigen Namen für **WEBAPP_NAME** und einen Wert für **REGION** an.

Linux (Bash):

```bash
export COSMOSDB_URI=<put-your-COSMOS-DB-documentEndpoint-URI-here>
export COSMOSDB_KEY=<put-your-COSMOS-DB-primaryMasterKey-here>
export COSMOSDB_DBNAME=<put-your-COSMOS-DB-name-here>
export RESOURCEGROUP_NAME=<put-your-resource-group-name-here>
export WEBAPP_NAME=<put-your-Webapp-name-here>
export REGION=<put-your-REGION-here>
```

Windows (Eingabeaufforderung):
```cmd
set COSMOSDB_URI=<put-your-COSMOS-DB-documentEndpoint-URI-here>
set COSMOSDB_KEY=<put-your-COSMOS-DB-primaryMasterKey-here>
set COSMOSDB_DBNAME=<put-your-COSMOS-DB-name-here>
set RESOURCEGROUP_NAME=<put-your-resource-group-name-here>
set WEBAPP_NAME=<put-your-Webapp-name-here>
set REGION=<put-your-REGION-here>
```

> [!NOTE]
> Falls Sie diese Variablen mit einem Skript bereitstellen möchten, finden Sie im Verzeichnis „.prep“ eine Vorlage für Bash, die Sie kopieren und als Grundlage verwenden können.

2. Ändern Sie das Verzeichnis wie folgt:

    ```bash
    cd initial/spring-todo-app
    ``` 
 
3. Führen Sie die Spring-Todo-App mithilfe des folgenden Befehls lokal aus:

    ```bash
    mvn package spring-boot:run
    ```

4. Nachdem die Anwendung gestartet wurde, können Sie die Bereitstellung überprüfen, indem Sie unter [http://localhost:8080/](http://localhost:8080/) auf die Spring-Todo-App zugreifen.

 ![Lokal ausgeführte Spring-App][SCDB01]

## <a name="deploy-to-app-service-linux"></a>Bereitstellen für App Service (Linux)

1. Öffnen Sie die Datei „pom.xml“, die Sie zuvor in das Verzeichnis **initial/spring-todo-app** des Repositorys kopiert haben. Vergewissern Sie sich, dass das [Maven-Plug-In für Azure App Service](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-webapp-maven-plugin/README.md) enthalten ist, wie weiter unten in der Datei „pom.xml“ zu sehen. Sollte die Version nicht auf **1.6.0** festgelegt sein, aktualisieren Sie den Wert.

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

2. Führen Sie die Bereitstellung für Java SE in App Service (Linux) durch.

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

3. Navigieren Sie zu Ihrer Web-App, die unter Java SE in App Service (Linux) ausgeführt wird:

    ```bash
    https://<WEBAPP_NAME>.azurewebsites.net
    ```

![In App Service unter Linux ausgeführte Spring-App][SCDB02]

## <a name="troubleshoot-spring-todo-app-on-azure-by-viewing-logs"></a>Behandeln von Problemen mit der Spring-Todo-App in Azure anhand von Protokollen

1. Konfigurieren Sie Protokolle für die bereitgestellte Java-Web-App in Azure App Service unter Linux:

    ```bash
    az webapp log config --name ${WEBAPP_NAME} \
     --resource-group ${RESOURCEGROUP_NAME} \
     --web-server-logging filesystem
    ```
2. Öffnen Sie den Remoteprotokollstream der Java-Web-App von einem lokalen Computer aus:

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

3. Anschließend können Sie Ihre Ergebnisse anhand des Codes in [e2e-java-experience-in-app-service-linux-part-2/complete](https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2/tree/master/complete) überprüfen.


## <a name="scale-out-the-spring-todo-app"></a>Erweitern der Spring-Todo-App

1. Erweitern Sie die Java-Web-App über die Azure-Befehlszeilenschnittstelle:

    ```bash
    az appservice plan update --number-of-workers 2 \
      --name ${WEBAPP_PLAN_NAME} \
      --resource-group ${RESOURCEGROUP_NAME}
    ```

## <a name="next-steps"></a>Nächste Schritte

- [Java-Entwicklerleitfaden für App Service unter Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/app-service-linux-java)
- [Azure für Java-Entwickler](https://docs.microsoft.com/en-us/java/azure/): Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.

> [!div class="nextstepaction"]
> [Spring Framework in Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Weitere Ressourcen

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).

**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen. Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt. Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.

<!-- URL List -->

[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure für Java-Entwickler]: /java/azure/
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
