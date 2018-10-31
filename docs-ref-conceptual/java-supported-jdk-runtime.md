---
title: Java-JDKs und LTS (Long-Term Support) für Azure-Entwicklung
description: Downloads und Anweisung des Azure-Supports für die Entwicklung und Ausführung von Java-Anwendungen.
author: rloutlaw
manager: angerobe
ms.devlang: java
ms.topic: article
ms.date: 10/15/2017
ms.author: routlaw
ms.openlocfilehash: 2865219f350990e8b07f7d2cd99f536168a6b8d4
ms.sourcegitcommit: 7df2d442ad7cbdb235e5dd35302a9b73379c23d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/25/2018
ms.locfileid: "50026996"
---
# <a name="get-java-jdk-downloads-and-support-when-developing-for-azure"></a>Java-JDK-Downloads und Support beim Entwickeln für Azure

Java-Entwickler, die mit Azure und Azure Stack arbeiten, können Java-Produktionsanwendungen mithilfe von [Zulu Enterprise, einem OpenJDK-Build von Azul Systems](https://www.azul.com/downloads/azure-only/zulu/), erstellen und ausführen, ohne dabei zusätzliche Supportkosten zu erzeugen. Sie können eine beliebige Java-Laufzeit in Azure verwenden, bei der Verwendung von Zulu erhalten Sie jedoch kostenlose Wartungsupdates und können mit einem [qualifizierten Azure-Supportplan](https://azure.microsoft.com/support/plans/) Supportprobleme bei Microsoft erstellen.

## <a name="supported-java-versions-and-update-schedule"></a>Unterstützte Java-Versionen und Zeitplan für Updates

Azul Systems stellt mit [Zulu Enterprise einen vollständig unterstützten OpenJDK-Build für Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) zur Verfügung, der mit allen LTS-Versionen von Java (ab Java SE 7, 8 und 11) verwendet werden kann. Weitere Informationen finden Sie in der [Pressemitteilung von Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).


Für diese JDK-Releases gibt es vierteljährliche Sicherheitsupdates und Fehlerbehebungen sowie wichtige Out-of-band-Updates und Patches je nach Bedarf.  Dieser Support umfasst die rückwirkende Portierung von Sicherheitsupdates und Fehlerbehebungen in Java 7 und 8, die in neueren Versionen von Java, z.B. Java 11, gemeldet wurden, und stellt die kontinuierliche Stabilität und Sicherheit von älteren Java-Versionen sicher.  Azure-Kunden können diese Sicherheitsupdates und Fehlerbehebungen für Plattformen nutzen, ohne dabei ungeplante Gebühren für Java SE-Abonnements zu verursachen. Die Supportdaten für die einzelnen Java SE-Versionen sind in der folgenden Abbildung hervorgehoben.

![JDK-Supportzeitachse für Azure](media/azure-jdk-support.png)

Azul Systems verwaltet eine [Java SE-Roadmap](https://www.azul.com/products/azul_support_roadmap/) für diese Releases.

## <a name="use-for-local-development"></a>Verwendung für lokale Entwicklung 

Entwickler können Java-JDKs für Azure und Azure Stack von der [Azul Systems-Website](https://www.azul.com/downloads/azure-only/zulu/) herunterladen. Downloads sind für Windows, Linux und MacOS verfügbar. Entwickler, die unter Linux arbeiten, können Pakete auch über die Paket-Manager [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) und [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) abrufen.

Produktsupport für das von Azure unterstützte Azul Zulu JDK ist bei der Entwicklung für Azure oder Azure Stack mit einem [qualifizierten Azure-Supportplan](https://azure.microsoft.com/support/plans/) erhältlich.

## <a name="use-in-docker-containers"></a>Verwendung in Docker-Containern

Sie können mithilfe der Zulu Enterprise-Builds von OpenJDK beliebig viele Docker-Images für die Distributionen Ihrer Wahl erstellen. Zulu-Docker-Images, die auf Azul Zulu Enterprise für Azure-JDKs basieren, sind im [öffentlichen Docker-Repository von Microsoft](https://hub.docker.com/r/microsoft/java-jdk/) verfügbar. Die zum Erstellen dieser Images verwendeten Dockerfiles sind im [Java-GitHub-Repository von Microsoft](https://github.com/Microsoft/java/tree/master/docker) verfügbar.

Zum Containerisieren Ihrer Apps mithilfe dieser Images müssen Sie eine `FROM`-Anweisung in Ihrem Dockerfile festlegen und dann den Container mit den Abhängigkeiten Ihrer Anwendung konfigurieren. Beispiel für die Ausführung einer Java SE-Anwendung, die in eine JAR-Datei gepackt ist und an Port 8080 bindet:

```Dockerfile
FROM  microsoft/java-jdk:<tag>
EXPOSE 8080
ADD target/hello.jar hello.jar
ENTRYPOINT ["java", "-jar","/hello.jar"]
```

## <a name="azure-service-runtime-support"></a>Laufzeitunterstützung für Azure-Dienst

Azure-Plattformdienste wie [App Service](/azure/app-service/containers/), [Functions](/azure/azure-functions/functions-create-first-java-maven), [Service Fabric](/azure/service-fabric/) und [HDInsight](/azure/hdinsight/) verwenden Zulu Enterprise-Builds von OpenJDK mit integriertem automatischem Patching für Nebenversionen von Java, die Sicherheitsupdates und Fehlerbehebungen umfassen.