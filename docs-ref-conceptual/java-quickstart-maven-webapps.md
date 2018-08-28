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
ms.openlocfilehash: 70b508118c50b75693e2d746dc1e2919c827cb29
ms.sourcegitcommit: 0f38ef9ad64cffdb7b2e9e966224dfd0af251b0f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703543"
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a>Erstellen und Bereitstellen einer Java-App in Azure mit Maven

In dieser Schnellstartanleitung erfahren Sie, wie Sie mithilfe von [Apache Maven](http://maven.apache.org) und der Azure-Befehlszeilenschnittstelle in wenigen Minuten eine einfache Java-Web-App erstellen und in [Azure App Service](/azure/app-service/app-service-value-prop-what-is) bereitstellen.

## <a name="before-you-begin"></a>Voraussetzungen

Richten Sie zunächst Folgendes ein:

- [Git-Client](https://git-scm.com/)
- [Java 8](https://www.azul.com/downloads/zulu/)
- [Maven 3](http://maven.apache.org/download.cgi)
- [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

## <a name="get-the-sample-code"></a>Laden Sie den Beispielcode herunter

Klonen Sie das Beispiel-App-Repository auf Ihrem lokalen Computer. Bei dem Beispiel handelt es sich um eine einfache JSP-Anwendung mit zusätzlicher Maven-Konfiguration im Projekt `pom.xml`, um die App lokal zu testen und die Bereitstellung des Beispiels in Azure App Service zu vereinfachen.

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a>Lokales Ausführen der App

Öffnen Sie eine Eingabeaufforderung, und verwenden Sie Maven, um die App zu erstellen und in einem lokalen [Tomcat](https://tomcat.apache.org)-Webcontainer auszuführen. 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

Öffnen Sie einen Webbrowser, und navigieren Sie zu http://localhost:8080, um eine Vorschau auf die App anzuzeigen:

  ![Ausgabe „Hello World“ der Java-Beispielanwendung](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a>Anmelden an Azure

Melden Sie sich mit `az login` bei der Azure-Befehlszeilenschnittstelle an. Die Azure-Ressourcen, die zum Hosten der App erforderlich sind, werden in dieser Schnellstartanleitung über die Befehlszeilenschnittstelle abgefragt und erstellt.
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe   

Erstellen Sie mit [az group create](/cli/azure/group#create) eine Ressourcengruppe. Eine Azure-Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen bereitgestellt und verwaltet werden.

```azurecli
az group create --location "East US" --name myResourceGroup
```

Weitere mögliche Werte für `---location` können Sie mithilfe von [az appservice list-locations](/cli/azure/appservice#list-locations) anzeigen.

## <a name="create-an-app-service-plan"></a>Wie erstelle ich einen Plan?

Erstellen Sie mithilfe von [az appservice plan create](/cli/azure/appservice/plan#create) einen [App Service-Plan](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) vom Typ **FREE**. App Service-Pläne ordnen gemeinsam genutzte Ressourcen für sämtliche Web-Apps zu, die im Rahmen des Plans ausgeführt werden.


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

Wenn der App Service-Plan bereit ist, zeigt die Azure-Befehlszeilenschnittstelle Informationen wie im folgenden Beispiel an:

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


## <a name="create-a-web-app"></a>Erstellen einer Web-App

Erstellen Sie über die Azure-Befehlszeilenschnittstelle mithilfe des Befehls [az webapp create](/cli/azure/appservice/web#create) eine Web-App, die die Ressourcen des Plans verwendet. Die Web-App-Definition bietet Platz für die Bereitstellung des Codes sowie eine URL für den Zugriff auf die ausgeführte App.

Ersetzen Sie im unten stehenden Befehl den Platzhalter <appname> durch Ihren eigenen eindeutigen App-Namen. <appname> wird im Standardhostnamen für die Web-App verwendet. Ist <appname> nicht eindeutig, wird die Fehlermeldung „Eine Website mit dem angegebenen Namen ist bereits vorhanden.“ angezeigt.

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

Nach Erstellung der Web-App zeigt die Azure-Befehlszeilenschnittstelle Informationen wie im folgenden Beispiel an:

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

## <a name="configure-java-and-tomcat"></a>Konfigurieren von Java und Tomcat

Konfigurieren Sie die Web-App über die Azure-Befehlszeilenschnittstelle mithilfe des Befehls [az webapp config](/cli/azure/appservice/web#config) für die Verwendung von Java und Tomcat. Im folgenden Beispiel wird App Service für die Ausführung von Java 8 und [Apache Tomcat 8.5](http://tomcat.apache.org/) konfiguriert, um die App auszuführen.

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a>Konfigurieren von Maven 

Die Maven-Datei `pom.xml` des Beispiels enthält die Konfiguration für FTP-Übermittlung des Beispiels an Azure, diese muss jedoch für die Bereitstellung in ihrer eigenen Web-App angepasst werden. Rufen Sie mithilfe von [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles) Ihre App Service-Anmeldeinformationen ab:

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

Ersetzen Sie die Platzhalter in der Datei `az-settings.xml` durch das Kennwort, den Benutzernamen und den FTP-Hostnamen aus der Ausgabe. Achten Sie darauf, dass der Benutzername nur ein einzelnes `\`-Zeichen enthält (im Gegensatz zu dem Wert mit Escapezeichen aus der Ausgabe der Befehlszeilenschnittstelle).
   
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

## <a name="deploy-the-sample-application"></a>Bereitstellen der Beispielanwendung

Stellen Sie das Beispiel in Azure bereit. Verwenden Sie dabei den Maven-Parameter `-s`, um die Konfiguration aus der Datei `az-settings.xml` zu verwenden.

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a>Navigieren zur Web-App

Sehen Sie sich das in Azure ausgeführte Beispiel an:

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a>Aktualisieren der App

Öffnen Sie `src/main/webapp/index.jsp` in einem Text-Editor, und ersetzen Sie den vorhandenen JSP-Code durch Folgendes:

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

Stellen Sie die Aktualisierung mit Maven bereit:

```
mvn clean package
mvn install -s az-settings.xml
```

Aktualisieren Sie Ihren Browser, nachdem die App erneut bereitgestellt wurde, um Ihre Änderungen anzuzeigen.

## <a name="manage-your-new-azure-app"></a>Verwalten Ihrer neuen Azure-App

Sehen Sie sich die soeben erstellte Web-App im Azure-Portal an.

Melden Sie sich dazu bei [https://portal.azure.com](https://portal.azure.com) an.

Klicken Sie im linken Menü auf **App Service** und anschließend auf den Namen Ihrer Azure-Web-App.

 ![Auswählen Ihrer App aus der Web-App-Liste im Portal](media/azure-app-service-portal.png)

Testen Sie die Überwachung, indem sie `curl` für die App ausführen, um Datenverkehr zu übermitteln.

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

Nach wenigen Minuten erscheint die Anforderungsaktivität in der Überwachung.

 ![Überwachen im Azure-Portal](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Führen Sie den folgenden Befehl aus, um alle in diesem Leitfaden erstellten Ressourcen zu entfernen:

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a>Nächste Schritte

Sehen Sie sich die vollständige Liste der [Azure-Java-Beispiele](https://azure.microsoft.com/resources/samples/?term=java) an.
