---
title: Erstellen einer Java-Web-App in Azure in fünf Minuten mit Maven | Microsoft-Dokumentation
description: Erstellen und Bereitstellen einer mit Maven erstellten Java-App in Azure
services: app-service\web
documentationcenter: ''
author: rloutlaw
manager: douge
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: routlaw
ms.openlocfilehash: 1adc0a104ba22bcd353664e68323165890e46c64
ms.sourcegitcommit: 30d502b3150fa14bcc1251f5f88c7c0dd83e531e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/12/2017
ms.locfileid: "22033632"
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a><span data-ttu-id="05faa-103">Erstellen und Bereitstellen einer Java-App in Azure mit Maven</span><span class="sxs-lookup"><span data-stu-id="05faa-103">Create and deploy a Java app to Azure with Maven</span></span>

<span data-ttu-id="05faa-104">In dieser Schnellstartanleitung erfahren Sie, wie Sie mithilfe von [Apache Maven](http://maven.apache.org) und der Azure-Befehlszeilenschnittstelle in wenigen Minuten eine einfache Java-Web-App erstellen und in [Azure App Service](/azure/app-service/app-service-value-prop-what-is) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="05faa-104">This quickstart helps you create and deploy a simple Java web app to [Azure App Service](/azure/app-service/app-service-value-prop-what-is) in just a few minutes using [Apache Maven](http://maven.apache.org) and the Azure CLI.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="05faa-105">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="05faa-105">Before you begin</span></span>

<span data-ttu-id="05faa-106">Richten Sie zunächst Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="05faa-106">Before you start, set up the following:</span></span>

- [<span data-ttu-id="05faa-107">Git</span><span class="sxs-lookup"><span data-stu-id="05faa-107">Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="05faa-108">Java 8</span><span class="sxs-lookup"><span data-stu-id="05faa-108">Java 8</span></span>](https://www.azul.com/downloads/zulu/)
- [<span data-ttu-id="05faa-109">Maven 3</span><span class="sxs-lookup"><span data-stu-id="05faa-109">Maven 3</span></span>](http://maven.apache.org/download.cgi)
- [<span data-ttu-id="05faa-110">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="05faa-110">Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-az-cli2)

<span data-ttu-id="05faa-111">Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.</span><span class="sxs-lookup"><span data-stu-id="05faa-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="05faa-112">Laden Sie den Beispielcode herunter</span><span class="sxs-lookup"><span data-stu-id="05faa-112">Get the sample code</span></span>

<span data-ttu-id="05faa-113">Klonen Sie das Beispiel-App-Repository auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="05faa-113">Clone the sample app repository to your local machine.</span></span> <span data-ttu-id="05faa-114">Bei dem Beispiel handelt es sich um eine einfache JSP-Anwendung mit zusätzlicher Maven-Konfiguration im Projekt `pom.xml`, um die App lokal zu testen und die Bereitstellung des Beispiels in Azure App Service zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="05faa-114">The sample is a simple JSP application with additional Maven configuration in the project `pom.xml` to test the app locally and help deploy the sample to Azure App Service.</span></span>

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a><span data-ttu-id="05faa-115">Lokales Ausführen der App</span><span class="sxs-lookup"><span data-stu-id="05faa-115">Run the app locally</span></span>

<span data-ttu-id="05faa-116">Öffnen Sie eine Eingabeaufforderung, und verwenden Sie Maven, um die App zu erstellen und in einem lokalen [Tomcat](https://tomcat.apache.org)-Webcontainer auszuführen.</span><span class="sxs-lookup"><span data-stu-id="05faa-116">Open a command prompt and use Maven to build the app and run it in a local [Tomcat](https://tomcat.apache.org) web container.</span></span> 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

<span data-ttu-id="05faa-117">Navigieren Sie in einem Webbrowser zu http://localhost:8080, um eine Vorschau der App anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="05faa-117">Open a web browser and navigate to http://localhost:8080 to preview the app:</span></span>

  ![Ausgabe „Hello World“ der Java-Beispielanwendung](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="05faa-119">Anmelden an Azure</span><span class="sxs-lookup"><span data-stu-id="05faa-119">Log in to Azure</span></span>

<span data-ttu-id="05faa-120">Melden Sie sich mit `az login` bei der Azure-Befehlszeilenschnittstelle an.</span><span class="sxs-lookup"><span data-stu-id="05faa-120">Log in to the Azure CLI with `az login`.</span></span> <span data-ttu-id="05faa-121">Die Azure-Ressourcen, die zum Hosten der App erforderlich sind, werden in dieser Schnellstartanleitung über die Befehlszeilenschnittstelle abgefragt und erstellt.</span><span class="sxs-lookup"><span data-stu-id="05faa-121">This quickstart uses the CLI to query and create the Azure resources needed to host the app.</span></span>
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="05faa-122">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="05faa-122">Create a resource group</span></span>   

<span data-ttu-id="05faa-123">Erstellen Sie mit [az group create](/cli/azure/group#create) eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="05faa-123">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="05faa-124">Eine Azure-Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen bereitgestellt und verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="05faa-124">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

```azurecli
az group create --location "East US" --name myResourceGroup
```

<span data-ttu-id="05faa-125">Weitere mögliche Werte für `---location` können Sie mithilfe von [az appservice list-locations](/cli/azure/appservice#list-locations) anzeigen.</span><span class="sxs-lookup"><span data-stu-id="05faa-125">To see other possible values you can use for `---location`, use [az appservice list-locations](/cli/azure/appservice#list-locations)</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="05faa-126">Wie erstelle ich einen Plan?</span><span class="sxs-lookup"><span data-stu-id="05faa-126">Create an App Service plan</span></span>

<span data-ttu-id="05faa-127">Erstellen Sie mithilfe von [az appservice plan create](/cli/azure/appservice/plan#create) einen [App Service-Plan](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) vom Typ **FREE**.</span><span class="sxs-lookup"><span data-stu-id="05faa-127">Create a **FREE** [App Service plan](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) using [az appservice plan create](/cli/azure/appservice/plan#create).</span></span> <span data-ttu-id="05faa-128">App Service-Pläne ordnen gemeinsam genutzte Ressourcen für sämtliche Web-Apps zu, die im Rahmen des Plans ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="05faa-128">App Service plans allocate resources shared across all web apps running in the plan.</span></span>


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="05faa-129">Wenn der App Service-Plan bereit ist, zeigt die Azure-Befehlszeilenschnittstelle Informationen wie im folgenden Beispiel an:</span><span class="sxs-lookup"><span data-stu-id="05faa-129">When the App Service Plan is ready, the Azure CLI shows information similar to the following example:</span></span>

```json
{
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "location": "East US",
    "sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "tier": "Standard"
    },
    "status": "Ready",
    "type": "Microsoft.Web/serverfarms"
}
```


## <a name="create-a-web-app"></a><span data-ttu-id="05faa-130">Erstellen einer Web-App</span><span class="sxs-lookup"><span data-stu-id="05faa-130">Create a web app</span></span>

<span data-ttu-id="05faa-131">Erstellen Sie über die Azure-Befehlszeilenschnittstelle mithilfe des Befehls [az webapp create](/cli/azure/appservice/web#create) eine Web-App, die die Ressourcen des Plans verwendet.</span><span class="sxs-lookup"><span data-stu-id="05faa-131">Create a web app that uses the plan's resources using the Azure CLI [az webapp create](/cli/azure/appservice/web#create) command.</span></span> <span data-ttu-id="05faa-132">Die Web-App-Definition bietet Platz für die Bereitstellung des Codes sowie eine URL für den Zugriff auf die ausgeführte App.</span><span class="sxs-lookup"><span data-stu-id="05faa-132">The web app definition provides a space to deploy the code to and a URL to access the app once it's running.</span></span>

<span data-ttu-id="05faa-133">Ersetzen Sie im unten stehenden Befehl den Platzhalter <appname> durch Ihren eigenen eindeutigen App-Namen.</span><span class="sxs-lookup"><span data-stu-id="05faa-133">In the command below substitute your own unique app name where you see the <appname> placeholder.</span></span> <span data-ttu-id="05faa-134"><appname> wird im Standardhostnamen für die Web-App verwendet.</span><span class="sxs-lookup"><span data-stu-id="05faa-134">The <appname> is used in the default hostname for the web app.</span></span> <span data-ttu-id="05faa-135">Ist <appname> nicht eindeutig, wird die Fehlermeldung „Eine Website mit dem angegebenen Namen ist bereits vorhanden.“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="05faa-135">If <appname> is not unique, you get the friendly error message "Website with given name already exists."</span></span>

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

<span data-ttu-id="05faa-136">Nach Erstellung der Web-App zeigt die Azure-Befehlszeilenschnittstelle Informationen wie im folgenden Beispiel an:</span><span class="sxs-lookup"><span data-stu-id="05faa-136">When the Web App has been created, the Azure CLI shows information similar to the following example.1</span></span>

```json
{
    "clientAffinityEnabled": true,
    "defaultHostName": "<appname>.azurewebsites.net",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<appname>",
    "isDefaultContainer": null,
    "kind": "app",
    "location": "East US",
    "name": "<app_name>",
    "repositorySiteName": "<app_name>",
    "reserved": true,
    "resourceGroup": "myResourceGroup",
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "state": "Running",
    "type": "Microsoft.Web/sites",
}
```

## <a name="configure-java-and-tomcat"></a><span data-ttu-id="05faa-137">Konfigurieren von Java und Tomcat</span><span class="sxs-lookup"><span data-stu-id="05faa-137">Configure Java and Tomcat</span></span>

<span data-ttu-id="05faa-138">Konfigurieren Sie die Web-App über die Azure-Befehlszeilenschnittstelle mithilfe des Befehls [az webapp config](/cli/azure/appservice/web#config) für die Verwendung von Java und Tomcat.</span><span class="sxs-lookup"><span data-stu-id="05faa-138">Configure the web app to use Java and Tomcat using the Azure CLI's [az webapp config](/cli/azure/appservice/web#config) command.</span></span> <span data-ttu-id="05faa-139">Im folgenden Beispiel wird App Service für die Ausführung von Java 8 und [Apache Tomcat 8.5](http://tomcat.apache.org/) konfiguriert, um die App auszuführen.</span><span class="sxs-lookup"><span data-stu-id="05faa-139">The example below configures App Service to run Java 8 and [Apache Tomcat 8.5](http://tomcat.apache.org/) to run the app.</span></span>

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a><span data-ttu-id="05faa-140">Konfigurieren von Maven</span><span class="sxs-lookup"><span data-stu-id="05faa-140">Configure Maven</span></span> 

<span data-ttu-id="05faa-141">Die Maven-Datei `pom.xml` des Beispiels enthält die Konfiguration für FTP-Übermittlung des Beispiels an Azure, diese muss jedoch für die Bereitstellung in ihrer eigenen Web-App angepasst werden.</span><span class="sxs-lookup"><span data-stu-id="05faa-141">The sample's Maven `pom.xml` includes configuration to FTP the sample into Azure, but you'll need to customize it to deploy to your own web app.</span></span> <span data-ttu-id="05faa-142">Rufen Sie mithilfe von [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles) Ihre App Service-Anmeldeinformationen ab:</span><span class="sxs-lookup"><span data-stu-id="05faa-142">Retreive your App Seevice credentials with [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span></span>

```azurecli
az webapp deployment list-publishing-profiles  \
--name appname \ 
--resource-group myResourceGroup  \
--query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" 
```

```json
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "appname\\$appname"
  }
]
```

<span data-ttu-id="05faa-143">Ersetzen Sie die Platzhalter in der Datei `az-settings.xml` durch das Kennwort, den Benutzernamen und den FTP-Hostnamen aus der Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="05faa-143">Replace the placeholders in the `az-settings.xml` file with password, username, and FTP hostname from the output.</span></span> <span data-ttu-id="05faa-144">Achten Sie darauf, dass der Benutzername nur ein einzelnes `\`-Zeichen enthält (im Gegensatz zu dem Wert mit Escapezeichen aus der Ausgabe der Befehlszeilenschnittstelle).</span><span class="sxs-lookup"><span data-stu-id="05faa-144">Make sure to only use one `\` character in the username instead of the escaped value from the CLI output.</span></span>
   
```XML
...
    <server>
      <id>azure-hello-world</id>
      <username>appname\$appname</username>
      <password>aBcDeFgHiJkLmNoPqRsTuVwXyZ</password>
    </server>
...
   <configuration>
     <fromFile>${basedir}/target/AzureAppDemo-0.0.1-SNAPSHOT.war</fromFile>
     <url>ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot</url>
     <toFile>webapps/ROOT.war</toFile>
     <serverId>azure-hello-world</serverId>
   </configuration>
...
```

## <a name="deploy-the-sample-application"></a><span data-ttu-id="05faa-145">Bereitstellen der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="05faa-145">Deploy the sample application</span></span>

<span data-ttu-id="05faa-146">Stellen Sie das Beispiel in Azure bereit. Verwenden Sie dabei den Maven-Parameter `-s`, um die Konfiguration aus der Datei `az-settings.xml` zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="05faa-146">Deploy with sample to Azure, using Maven's `-s` parameter to use the configuration in the `az-settings.xml` file.</span></span>

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a><span data-ttu-id="05faa-147">Navigieren zur Web-App</span><span class="sxs-lookup"><span data-stu-id="05faa-147">Browse to web app</span></span>

<span data-ttu-id="05faa-148">Sehen Sie sich das in Azure ausgeführte Beispiel an:</span><span class="sxs-lookup"><span data-stu-id="05faa-148">View the sample running in Azure:</span></span>

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a><span data-ttu-id="05faa-149">Aktualisieren der App</span><span class="sxs-lookup"><span data-stu-id="05faa-149">Update the app</span></span>

<span data-ttu-id="05faa-150">Öffnen Sie `src/main/webapp/index.jsp` in einem Text-Editor, und ersetzen Sie den vorhandenen JSP-Code durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="05faa-150">Using a text editor, open `src/main/webapp/index.jsp`, and replace the existing JSP with the one below.</span></span>

```html
<%--
  Copyright (c) Microsoft Corporation. All rights reserved.
  Licensed under the MIT License. See License.txt in the project root for
  license information.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"  import="java.util.Date" %>
<html>
<head>
  <title>Azure Samples Hello World</title>
</head>
<body>
  <H1>Hello Azure!</H1>
   Current time is: <%= new Date() %>
</body>
</html>
```

<span data-ttu-id="05faa-151">Stellen Sie die Aktualisierung mit Maven bereit:</span><span class="sxs-lookup"><span data-stu-id="05faa-151">Deploy the update with Maven:</span></span>

```
mvn clean package
mvn install -s az-settings.xml
```

<span data-ttu-id="05faa-152">Aktualisieren Sie Ihren Browser, nachdem die App erneut bereitgestellt wurde, um Ihre Änderungen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="05faa-152">Refresh your browser after the app redeploys to view your changes.</span></span>

## <a name="manage-your-new-azure-app"></a><span data-ttu-id="05faa-153">Verwalten Ihrer neuen Azure-App</span><span class="sxs-lookup"><span data-stu-id="05faa-153">Manage your new Azure app</span></span>

<span data-ttu-id="05faa-154">Sehen Sie sich die soeben erstellte Web-App im Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="05faa-154">Go to the Azure portal to take a look at the web app you just created.</span></span>

<span data-ttu-id="05faa-155">Melden Sie sich hierzu bei [https://portal.azure.com](https://portal.azure.com) an.</span><span class="sxs-lookup"><span data-stu-id="05faa-155">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="05faa-156">Klicken Sie im linken Menü auf **App Service** und anschließend auf den Namen Ihrer Azure-Web-App.</span><span class="sxs-lookup"><span data-stu-id="05faa-156">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

 ![Auswählen Ihrer App aus der Web-App-Liste im Portal](media/azure-app-service-portal.png)

<span data-ttu-id="05faa-158">Testen Sie die Überwachung, indem sie `curl` für die App ausführen, um Datenverkehr zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="05faa-158">Test the monitoring by running `curl` against the app to send some traffic.</span></span>

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

<span data-ttu-id="05faa-159">Nach wenigen Minuten erscheint die Anforderungsaktivität in der Überwachung.</span><span class="sxs-lookup"><span data-stu-id="05faa-159">You'll see the request activity in the monitoring after a couple of minutes.</span></span>

 ![Überwachen im Azure-Portal](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a><span data-ttu-id="05faa-161">Bereinigen von Ressourcen</span><span class="sxs-lookup"><span data-stu-id="05faa-161">Clean up resources</span></span>

<span data-ttu-id="05faa-162">Führen Sie den folgenden Befehl aus, um alle in diesem Leitfaden erstellten Ressourcen zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="05faa-162">To remove all the resources created in this guide, run the following command:</span></span>

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a><span data-ttu-id="05faa-163">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="05faa-163">Next steps</span></span>

<span data-ttu-id="05faa-164">Sehen Sie sich die vollständige Liste der [Azure-Java-Beispiele](https://azure.microsoft.com/resources/samples/?term=java) an.</span><span class="sxs-lookup"><span data-stu-id="05faa-164">Browse the full list of [Azure Java samples](https://azure.microsoft.com/resources/samples/?term=java).</span></span>