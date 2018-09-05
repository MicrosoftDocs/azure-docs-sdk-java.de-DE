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
ms.openlocfilehash: 323ae247c3df8c7d7b180d9d60b9014e4e2d7382
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240960"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a>Bereitstellen eines Java-basierten MicroProfile-Diensts in Azure-Web-App für Container

MicroProfile eignet sich sehr gut, um besonders kleine Java-Anwendungen zu erstellen, die schnell und einfach in Diensten wie [Azure-Web-App für Container](https://azure.microsoft.com/services/app-service/containers/) bereitgestellt werden können. In diesem Tutorial erstellen wir einen einfachen MicroProfile-basierten Microservice, der dann in einen Docker-Container gepackt, in einer [Azure Container Registry-Instanz](https://azure.microsoft.com/services/container-registry/) bereitgestellt und anschließend mithilfe von Azure-Web-App für Container gehostet wird.

> [!NOTE]
>
> Dieses Verfahren kann für jede Implementierung von „MicroProfile.io“ verwendet werden, solange das Docker-Containerimage selbstausführbar ist (sprich: die Runtime enthält).

In diesem Beispiel werden [Payara Micro](https://www.payara.fish/payara_micro) und [MicroProfile 1.3](https://microprofile.io/) verwendet, um eine kleine Java-WAR-Datei (5.085 Bytes auf dem Erstellercomputer) zu erstellen. Diese wird dann in ein Docker-Image (mit einer Größe von etwa 174 MB) verpackt. Dieses Docker-Image enthält alles, was für eine vollständige Containerbereitstellung dieser Web-App benötigt wird.

Aufgrund der Funktionsweise von Docker muss häufig nicht das gesamte 174 MB große Docker-Image erneut bereitgestellt werden, wenn der Quellcode der Anwendung geändert wird, da Docker lediglich die (deutlich kleineren) Unterschiede hochlädt. Der Prozess zum Ausführen einer neuen MicroProfile-Anwendungsversion über eine CI/CD-Pipeline wird so äußerst effizient und schnell. Darüber hinaus wird der Prozess dadurch reibungsloser und ermöglicht eine schnelle Entwicklungsiteration.

In diesem Tutorial erstellen wir zunächst den Code und führen ihn lokal aus. Danach führen wir die Bereitstellung als Web-App in Azure durch. In beiden Fällen nutzen wir Docker zur Vereinfachung und Standardisierung. Bevor wir beginnen, erstellen wir eine Azure Container Registry-Instanz, in der wir unsere Docker-Container speichern können.

## <a name="creating-an-azure-container-registry"></a>Erstellen einer Azure Container Registry-Instanz

Wir erstellen die Azure Container Registry-Instanz über das [Azure-Portal](http://portal.azure.com). Für die Erstellung kann aber beispielsweise auch die Azure-Befehlszeilenschnittstelle verwendet werden. Führen Sie die folgenden Schritte aus, um eine neue Azure Container Registry-Instanz zu erstellen:

1. Melden Sie sich beim [Azure-Portal](http://portal.azure.com) an, und erstellen Sie eine neue Azure Container Registry-Ressource. Geben Sie einen Registrierungsnamen an. (Hinweis: Dieser Name muss als `docker.registry`-Eigenschaft in `pom.xml` festgelegt werden.) Ändern Sie die Standardeinstellungen nach Belieben, und klicken Sie anschließend auf „Erstellen“.

1. Wenn die Containerregistrierung aktiv ist (ungefähr 30 Sekunden nach dem Klicken auf „Erstellen“), klicken Sie auf die Containerregistrierung und anschließend im linken Menübereich auf „Zugriffsschlüssel“. Hier müssen Sie die Einstellung „Administratorbenutzer“ aktivieren, damit von unseren Computern aus auf diese Containerregistrierung zugegriffen werden kann (um Docker-Container per Push hinzuzufügen) und um den Zugriff über die Instanz von Azure-Web-App für Container zu ermöglichen, die wir in Kürze einrichten.

1. Notieren Sie sich die Werte `username` und `password`, während Sie sich im Bereich „Zugriffsschlüssel“ befinden. Diese Werte fügen wir später in unsere globale Maven-Datei `settings.xml` ein. (Weitere Informationen zu Maven-Einstellungen finden Sie in auf der [Website des Apache Maven-Projekts](https://maven.apache.org/settings.html).) Zu Referenzzwecken sehen Sie hier eine verschleierte Version der Datei `${user.home}/.m2/settings.xml` vom Erstellersystem:

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

Kommen wir nun zum Erstellen und lokalen Ausführen der MicroProfile-Anwendung.

## <a name="creating-our-microprofile-application"></a>Erstellen der MicroProfile-Anwendung

Dieses Beispiel basiert auf einer auf GitHub verfügbaren Beispielanwendung, deren Code wir hier klonen und Schritt für Schritt durchgehen. Gehen Sie wie folgt vor, um den Code auf Ihrem Computer zu klonen:

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

In diesem Verzeichnis befindet sich eine Datei namens `pom.xml`, die dazu dient, das Projekt im vom Maven-Erstellungstool verwendeten Format anzugeben. Diese Datei kann bearbeitet und an Ihre Anforderungen angepasst werden. Insbesondere die Eigenschaften `docker.registry` und `docker.name` müssen auf die Werte von `docker.registry` und `docker.name` festgelegt werden, die beim Einrichten der Azure Container Registry-Instanz erstellt wurden.

Eine andere wichtige Datei in diesem Verzeichnis ist die Dockerfile, die wie folgt aussieht:

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

Diese Dockerfile erstellt einfach einen neuen Docker-Container auf der Grundlage des Payara Micro-Docker-Containers und kopiert die WAR-Datei hinein, die im Rahmen unseres Buildprozesses erstellt wird. Außerdem macht sie den Port 8080 verfügbar, damit wir auf den Dienst zugreifen können, wenn er innerhalb eines Docker-Containers ausgeführt wird.

Im Verzeichnis `src` befindet sich unter anderem auch die Klasse `Application`:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

Die Anmerkung `@ApplicationPath("/api")` gibt den Basisendpunkt für diesen Microservice an. Das bedeutet, dass bei allen Endpunkten dem restlichen Teil der URL, die für den Zugriff auf einen bestimmen REST-Endpunkt benötigt wird, `/api` vorangestellt wird.

Das Paket `api` enthält eine Klasse namens `API` mit folgendem Code:

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

Die Anmerkung `@Path("/helloworld")` macht deutlich, dass dieser REST-Endpunkt in Kombination mit der Angabe von `/api` aus der Klasse `Application` wie folgt lautet: `/api/helloworld`. Wenn dieser Endpunkt mithilfe einer HTTP GET-Anforderung aufgerufen wird, wird durch die Methode Text/HTML (die hartcodierte Zeichenfolge „Hello, world!“) erzeugt.

Damit kennen Sie den gesamten Code, der zum Erstellen eines Microservice mit MicroProfile benötigt wird. Wir können nun Maven verwenden, um ihn zu erstellen, in einen Docker-Container zu packen und lokal auszuführen. Gehen Sie dazu wie folgt vor:

1. Führen Sie `mvn clean package` aus, und warten Sie, bis der Vorgang erfolgreich abgeschlossen wurde.

1. Führen Sie `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest` aus. (Beispiel: `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, wenn `docker.registry` auf `jogilescr.azurecr.io` und `docker.name` auf `samples/docker-helloworld` festgelegt ist.)

1. Greifen Sie in Ihrem Webbrowser auf [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) und [http://localhost:8080/health](http://localhost:8080/health) zu. Wenn Sie die erwartete Antwort „Hello, world!“ (und integritätsbezogene Informationen für den Endpunkt [/health](http://localhost:8080/health)) sehen, haben Sie die MicroProfile-Anwendung erfolgreich auf Ihrem lokalen Computer bereitgestellt.

## <a name="pushing-to-the-azure-container-registry"></a>Ausführen von Pushvorgängen an die Azure Container Registry-Instanz

Wir haben nun unsere MicroProfile-Anwendung erstellt und auf unserem lokalen Computer ausgeführt. Als Nächstes pushen wir den Container in unsere Containerregistrierung. In diesem Tutorial verwenden wir Azure Container Registry. Es kann aber auch eine beliebige andere Containerregistrierung verwendet werden (vorausgesetzt, die Datei `pom.xml` wird bearbeitet, um auf den entsprechenden Ort zu verweisen).

1. Führen Sie `mvn clean package` aus, um ein lokales Docker-Image zu bereinigen, zu kompilieren und zu erstellen.
2. Führen Sie `mvn dockerfile:push` aus, um einen Pushvorgang an die Azure Container Repository-Instanz auszuführen.

Sie haben nun Ihr Docker-Containerimage in die Azure Container Registry-Instanz hochgeladen, es wird jedoch noch nicht ausgeführt, da es noch in einer Instanz von Azure-Web-App für Container bereitgestellt werden muss. Diesen Schritt führen wir als Nächstes aus.

## <a name="creating-an-azure-web-app-for-containers-instance"></a>Erstellen einer Instanz von Azure-Web-App für Container

1. Kehren Sie zum [Azure-Portal](http://portal.azure.com) zurück, und erstellen Sie eine neue Instanz von Web-App für Container (unter der Überschrift „Web + Mobil“ im Menü). Ein paar Hinweise:

   1. Der hier angegebene Name ist die öffentliche URL der Web-App (auch wenn später bei Bedarf eine benutzerdefinierte Domäne hinzugefügt werden kann). Es empfiehlt sich daher, einen leicht zu merkenden Namen zu verwenden.

   1. Im Abschnitt „Container konfigurieren“ können Sie als Imagequelle „Azure Container Registry“ und anschließend das korrekte Image aus den Dropdownlisten auswählen.

   1. Im Feld „Startdatei“ muss kein Wert angegeben werden.

1. Warten Sie, bis die Instanz erstellt wurde (was nicht lange dauert), klicken Sie auf die Instanz, und klicken Sie anschließend auf das Menüelement „Anwendungseinstellungen“. Hier müssen Sie eine neue Anwendungseinstellung mit dem Schlüssel `WEBSITES_PORT` und dem Wert `8080` hinzufügen. So teilen Sie Azure mit, welchen Port Sie im Container verfügbar machen möchten, und er wird extern dem Port 80 zugeordnet.

1. Klicken Sie optional auf den Link „Docker-Container“, und aktivieren Sie „Continuous Deployment“. Dadurch erfolgt nach jeder Aktualisierung des Azure Container Registry-Images automatisch eine Aktualisierung in der Instanz von Azure-Web-App für Container.

1. Sie sollten auf die von Azure gehosteten Instanzen unter `http://<appname>.azurewebsites.net/microprofile/api/helloworld` und `http://<appname>.azurewebsites.net/health` zugreifen können.

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial sind wir Schritt für Schritt die Erstellung eines einfachen MicroProfile-basierten Microservice durchgegangen, haben ihn in einen Docker-Container gepackt und ihn lokal ausgeführt und in Azure veröffentlicht. In diesem Tutorial wird nicht auf die Erweiterung des Microservice mit nützlicheren Funktionen eingegangen. Im Internet stehen jedoch zahlreiche MicroProfile-Tutorials und -Tipps zur Verfügung – unter anderem unter [MicroProfile.io](https://microprofile.io/).