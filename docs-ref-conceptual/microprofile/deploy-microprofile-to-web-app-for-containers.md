---
title: Bereitstellen eines Java-basierten MicroProfile-Diensts in Azure-Web-App für Container
description: Hier erfahren Sie, wie Sie einen MicroProfile-Dienst unter Verwendung von Docker und Azure-Web-App für Container bereitstellen.
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533591"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a>Bereitstellen eines Java-basierten MicroProfile-Diensts in Azure-Web-App für Container

MicroProfile eignet sich sehr gut, um besonders kleine Java-Anwendungen zu erstellen, die Sie schnell und einfach in Diensten wie [Azure-Web-App für Container](https://azure.microsoft.com/services/app-service/containers/) bereitstellen können. In diesem Tutorial erstellen Sie einen einfachen MicroProfile-basierten Microservice, den Sie dann in einen Docker-Container packen, in einer [Azure Container Registry-Instanz](https://azure.microsoft.com/services/container-registry/) bereitstellen und anschließend über Azure Web-App für Container hosten.

> [!NOTE]
> Dieses Verfahren kann für jede Implementierung von „MicroProfile.io“ verwendet werden, solange das Docker-Containerimage selbstausführbar ist (d. h., das Image enthält die Runtime).

In diesem Beispiel verwenden Sie [Payara Micro](https://www.payara.fish/payara_micro) und [MicroProfile 1.3](https://microprofile.io/), um eine kleine (ungefähr 5.000 Byte) Java-WAR-Datei (Web Application Requirement) zu erstellen und diese dann in ein Docker-Image von etwa 174 Megabyte (MB) zu verpacken. Das Docker-Image enthält alles, was für eine vollständige Containerbereitstellung der Web-App benötigt wird.

Wenn sich der Quellcode der Anwendung geändert hat, muss nicht das gesamte 174-MB-Docker-Image erneut bereitgestellt werden, weil Docker nur die Unterschiede hochlädt (die deutlich kleiner sind). Daher ist der Prozess zum Ausführen einer neuen MicroProfile-Anwendungsversion über eine CI/CD-Pipeline äußerst effizient und schnell, wodurch die Reibungsverluste verringert werden und eine schnelle Entwicklungsiteration ermöglicht wird.

Sie arbeiten dieses Tutorial durch, indem Sie zuerst den Code lokal erstellen und ausführen und ihn dann als Web-App in Azure bereitstellen. In beiden Phasen können Sie Docker nutzen, um Ihre Aktivitäten zu vereinfachen und zu standardisieren. Bevor Sie beginnen, erstellen Sie eine Azure Container Registry-Instanz, in der Sie Ihre Docker-Container speichern können.

## <a name="create-an-azure-container-registry-instance"></a>Erstellen einer Azure Container Registry-Instanz

Sie können das [Azure-Portal](http://portal.azure.com) verwenden, um die Azure Container Registry-Instanz zu erstellen, es gibt aber auch andere Optionen, etwa die Azure-Befehlszeilenschnittstelle. Um eine neue Azure Container Registry-Instanz zu erstellen, gehen Sie wie folgt vor:

1. Melden Sie sich beim [Azure-Portal](http://portal.azure.com) an, und erstellen Sie eine neue Azure Container Registry-Ressource. Geben Sie einen Registrierungsnamen an (dieser Name muss als `docker.registry`-Eigenschaft in der *pom.xml*-Datei festgelegt werden). Ändern Sie die Standardeinstellungen nach Bedarf, und wählen Sie anschließend **Erstellen** aus.

1. Nach etwa 30 Sekunden, wenn die Container Registry-Instanz aktiv ist, wählen Sie die Container Registry-Instanz aus, und wählen Sie dann im linken Bereich den Link **Zugriffsschlüssel** aus. 

    Aktivieren Sie die Einstellung *Administratorbenutzer*, damit Sie von Ihren Computern Zugriff auf diese Container Registry-Instanz haben und Docker-Container in die Instanz pushen können. Dadurch wird auch Zugriff aus der Azure Web-App für Container-Instanz aktiviert, die Sie bald schnell einrichten werden.

1. Kopieren Sie im Bereich **Zugriffsschlüssel** die Werte von **username** und **password**, und fügen Sie diese Werte in Ihre globale *settings.xml*-Maven-Datei ein. Weitere Informationen zu Maven-Einstellungen finden Sie auf der [Apache Maven Project](https://maven.apache.org/settings.html)-Website. 

   Zu Referenzzwecken ist hier ein Beispiel der *${user.home}/.m2/settings.xml*-Datei aufgeführt:

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

Nachdem Sie Ihre Container-Registry-Instanz erstellt haben, können Sie nun Ihre MicroProfile-Anwendung lokal erstellen und ausführen.

## <a name="create-your-microprofile-application"></a>Erstellen Ihrer MicroProfile-Anwendung

Dieser Beispielcode basiert auf einer Beispielanwendung, die auf GitHub verfügbar ist. Um den Code auf Ihrem Computer zu klonen, geben Sie die folgenden Befehle ein:

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

Dieses Verzeichnis enthält eine *pom.xml*-Datei, die Sie dazu verwenden können, das Projekt in dem Format anzugeben, das vom Maven-Erstellungstool verwendet wird. Sie können die Datei bearbeiten, damit sie Ihren Anforderungen entspricht. Insbesondere müssen die Eigenschaften `docker.registry` und `docker.name` entsprechend der `docker.registry`- und der `docker.name`-Eigenschaft geändert werden, die erstellt wurden, als Sie die Azure Container Registry-Instanz eingerichtet haben.

Eine andere wichtige Datei in diesem Verzeichnis ist die Dockerfile, die wie folgt aussieht:

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

Das Dockerfile erstellt einen neuen Docker-Container, der auf dem Payara Micro-Docker-Container basiert. Es kopiert in die WAR-Datei, die als Teil Ihres Buildprozesses erstellt wurde. Es macht den Port 8080 verfügbar, sodass Sie auf den Dienst zugreifen können, nachdem er in einem Docker-Container aktiviert ist und ausgeführt wird.

Wenn Sie das Verzeichnis *src* öffnen, finden Sie schließlich die `Application`-Klasse, die hier reproduziert ist:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

Die *@ApplicationPath("/api")* -Annotation gibt den Basisendpunkt für diesen Microservice an. Das heißt, für alle Endpunkte wird */api* dem Rest der URL vorangestellt, die erforderlich ist, um auf einen bestimmten REST-Endpunkt zuzugreifen.

Das Paket *api* enthält eine Klasse namens `API` mit folgendem Code:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

Durch Verwenden der *@Path("/helloworld")* -Annotation können Sie sehen, dass dieser REST-Endpunkt, wenn er mit der */api* kombiniert wird, die in der `Application`-Klasse angegeben ist, gleich */api/helloworld* ist. Wenn Sie diesen Endpunkt über eine HTTP GET-Anforderung aufrufen, können Sie sehen, dass durch die Methode Text/HTML erzeugt wird, und dies ist tatsächlich einfach die hartcodierte Zeichenfolge „Hello, world!“.

Bisher ist in diesem Artikel der gesamten Code angegeben, der für die Erstellung eines Microservice mithilfe von MicroProfile erforderlich ist. Sie können nun Maven verwenden, um den Code zu erstellen, ihn in einen Docker-Container zu packen und ihn lokal auszuführen. Gehen Sie dazu wie folgt vor:

1. Führen Sie `mvn clean package` aus, und warten Sie, bis der Befehl abgeschlossen ist.

1. Führen Sie `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest` aus. Zum Beispiel *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, wobei *\<docker.registry>* gleich *jogilescr.azurecr.io* and *\<docker.name>* gleich *samples/docker-helloworld* ist.

1. Greifen Sie in Ihrem Webbrowser auf [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) und [http://localhost:8080/health](http://localhost:8080/health) zu. Wenn Sie die erwartete Antwort „Hello, world!“ (und integritätsbezogene Informationen für den Endpunkt [/health](http://localhost:8080/health)) sehen, haben Sie die MicroProfile-Anwendung erfolgreich auf Ihrem lokalen Computer bereitgestellt.

## <a name="push-the-container-to-the-azure-container-registry-instance"></a>Pushen des Containers in die Azure Container Registry-Instanz

Nachdem Sie Ihre MicroProfile-Anwendung erfolgreich auf Ihrem lokalen Computer erstellt und ausgeführt haben, pushen Sie den Container in Ihre Container Registry-Instanz. 

> [!NOTE]
> Obwohl in diesem Artikel eine Azure Container Registry-Instanz verwendet wird, sollte jede Container Registry-Instanz funktionieren, sofern die *pom.xml*-Datei bearbeitet wurde, sodass in ihr auf den entsprechenden Speicherort verwiesen wird.

1. Um ein lokales Docker-Image zu bereinigen, zu kompilieren und zu erstellen, führen Sie `mvn clean package` aus.
2. Um den Container in die Azure Container Registry-Instanz zu pushen, führen Sie `mvn dockerfile:push` aus.

Sie haben jetzt Ihr Docker-Containerimage in die Azure Container Registry-Instanz hochgeladen. Das Image wird aber noch nicht ausgeführt. Sie müssen es in einer Azure-Web-App für Container-Instanz bereitstellen. 

## <a name="create-an-azure-web-app-for-containers-instance"></a>Erstellen einer Azure-Web-App für Container-Instanz

1. Wählen Sie im [Azure-Portal](http://portal.azure.com) im linken Bereich den Eintrag **Web + Mobil** aus, und gehen Sie dann wie folgt vor:

   a. Geben Sie einen Namen an. Der Name wird die öffentliche URL der Web-App, daher ist es eine gute Idee, einen Namen auszuwählen, den Sie sich leicht merken können. Bei Bedarf können Sie später einen benutzerdefinierten Domänennamen hinzufügen.

   b. Wählen Sie im Abschnitt **Container konfigurieren** unter **Imagequelle** die Option **Azure Container Registry** aus, und wählen Sie anschließend in der Dropdownliste das richtige Image aus.

   c. Sie müssen keinen Wert im Feld **Startdatei** angeben.

1. Nachdem Sie die Instanz erstellt haben, wählen Sie diese aus, und wählen Sie dann **Anwendungseinstellungen** aus. Geben Sie für **Schlüssel** die Einstellung **WEBSITES_PORT** und für **Wert** die Einstellung **8080** ein. Diese Einstellungen geben für Azure an, welcher Port im Container verfügbar zu machen ist, und dass er extern Port 80 zugeordnet werden soll.

1. (Optional) Wählen Sie den Link **Docker-Container** aus, und aktivieren Sie dann die Option **Continuous Deployment**. Dies bewirkt, dass das Image nach jeder Aktualisierung, die Sie an ihm in der Azure Container Registry-Instanz vorgenommen haben, automatisch in der Azure-Web-App für Container-Instanz aktualisiert wird.

1. Sie sollten nun auf die von Azure gehosteten Instanzen unter `http://<appname>.azurewebsites.net/microprofile/api/helloworld` und `http://<appname>.azurewebsites.net/health` zugreifen können.

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie Schritt für Schritt die Erstellung eines einfachen MicroProfile-basierten Microservice durchlaufen, haben ihn in einen Docker-Container gepackt, haben ihn lokal ausgeführt und haben ihn in Azure veröffentlicht. Sie können Ihren Microservice erweitern, um weitere nützliche Funktionen bereitzustellen. Weitere Informationen finden Sie auf [MicroProfile.io](https://microprofile.io/).
