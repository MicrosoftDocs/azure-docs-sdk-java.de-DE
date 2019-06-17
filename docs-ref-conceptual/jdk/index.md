---
title: Java-JDKs und LTS (Long-Term Support) für Azure-Entwicklung
description: Downloads und Anweisung des Azure-Supports für die Entwicklung und Ausführung von Java-Anwendungen.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 340f6149ffe39ccbb2d7de534ed63b8784d1f63a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270881"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a>Langfristiger Java-Support für Azure und Azure Stack

Java-Entwickler, die mit Azure und Azure Stack arbeiten, können Java-Produktionsanwendungen mithilfe von [Azul Zulu Enterprise für Azure](https://www.azul.com/downloads/azure-only/zulu/) erstellen und ausführen, ohne dass zusätzliche Supportkosten anfallen. Sie können in Azure eine beliebige Java-Runtime verwenden. Bei Verwendung von Zulu erhalten Sie jedoch kostenlose Wartungsupdates und können Supportprobleme bei Microsoft erstellen.

> [!div class="nextstepaction"]
> [Java herunterladen und installieren](java-jdk-install.md)

## <a name="long-term-support-lts"></a>Langfristiger Support (Long-Term Support, LTS)

* [Java 11](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [Java 7](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a>Technische Vorschauversion

* [Java 12](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a>Was ist Zulu OpenJDK für Azure?

Bei Azul Zulu Enterprise-Builds von OpenJDK handelt es sich um eine kostenlose, plattformübergreifende und produktionsbereite Distribution von OpenJDK für Azure und Azure Stack, die von Microsoft und Azul Systems unterstützt wird. Merkmale dieser Distributionen:

* Hundertprozentige Open-Source-Builds von OpenJDK, verpackt als JDKs (Java Development Kits), JREs (Java Runtime Environments) und monitorlose JREs. Bei diesen Binärdateien handelt es sich um vollständig kompatible und konforme kommerzielle Builds von Java Standard Edition (SE), die mit Java-Anwendungen oder -Komponenten in Azure und Azure Stack verwendet werden können.
* Langfristiger Support – einschließlich Fehlerbehebungen, Leistungsoptimierungen und Sicherheitspatches
* Verfügbar für die Entwicklung und Ausführung von Java-Anwendungen unter Windows, Linux und macOS
* Verfügbar als Containerimages in Docker Hub sowie als virtuelle Computer (Windows und Linux) im Azure Marketplace
* Sie werden von Microsoft Azure für verschiedenste Azure-Dienste genutzt. Beispiele:
  * App Service (Windows)
  * App Service (Linux)
  * Functions
  * Service Fabric
  * HDInsight
  * Suchen,
  * Azure DevOps
  * Cloud Shell  

## <a name="supported-java-versions-and-update-schedule"></a>Unterstützte Java-Versionen und Zeitplan für Updates

Azul Systems stellt vollständig unterstützte [Zulu Enterprise-Builds von OpenJDK für Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) bereit, der mit allen LTS-Versionen von Java (ab Java SE 7, 8 und 11) verwendet werden können. Weitere Informationen finden Sie in der [Pressemitteilung von Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).

|Java SE mit LTS  |Support bis  |
|---------|----------|
|[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7) |Juli 2023 |
|[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8) |März 2025|
|[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11) |September 2026|
|[![Java 12](../media/jdk/java-12.png)]() |**VORSCHAUVERSION**|

Für diese JDK-Releases werden vierteljährliche Sicherheitsupdates, Fehlerbehebungen sowie wichtige Out-of-band-Updates und -Patches nach Bedarf bereitgestellt.  Dieser Support umfasst die Zurückportierung von Sicherheitsupdates sowie die Behebung von Fehlern für Java 7 und 8, die in neueren Versionen von Java (etwa in Java 11) gemeldet wurden, um die kontinuierliche Stabilität und Sicherheit von älteren Java-Versionen zu gewährleisten.  Azure-Kunden können diese Sicherheitsupdates und Fehlerbehebungen für Plattformen beziehen, ohne dass ungeplante Gebühren für Java SE-Abonnements anfallen.

Azul Systems verwaltet eine [Java SE-Roadmap](https://www.azul.com/products/azul_support_roadmap/) für diese Releases.

## <a name="benefits-for-developers"></a>Vorteile für Entwickler

Die Azul Zulu JDK-Releases bieten folgende Vorteile:

1. Unterstützt von Microsoft und Azul Systems

   * Zulu-Binärdateien sind produktionsbereit und werden von Microsoft und Azul Systems unterstützt.
   * Zulu bietet kostenlosen langfristigen Support (Long-Term Support, LTS) für Java 7, 8 und 11. (LTS wird auch für Java 17 bereitgestellt.) Java-Versionen müssen nur bei Bedarf aktualisiert werden.
   * Support für Java 7 wird bis Juli 2023 bereitgestellt. Support für Java 8 und 11 wird über 2024 hinaus bereitgestellt.
   * Microsoft ist bestrebt, Zulu intern auf Computern auszuführen, die vielen Azure-Diensten zugrunde liegen.

2. Bereit für die Produktion

   * 100-prozentige Open-Source-Builds von OpenJDK
   * Direkter Ersatz für zahlreiche Java SE-Distributionen
   * JDK, JRE und JRE (monitorlos)
   * Java 7, 8 und 11
   * Konformität mit den Java SE-Spezifikationen unter Verwendung des OpenJDK Community Technology Compatibility Kits (TCK) geprüft
   * Entwickler erhalten weiterhin Produktionsupdates für Java SE – einschließlich Fehlerbehebungen, Leistungsverbesserungen und Sicherheitspatches für Java SE 7, 8 und 11.

3. Unterstützung mehrerer Plattformen Zulu unterstützt Binärdateien für mehrere Plattformen und Versionen:

   * Windows-Client
     * 10
     * 8.1
     * 8, 7
   * Windows Server
     * 2016 R2
     * 2016
     * 2012 R2
     * 2012
     * 2008 R2
   * Linux, einschließlich
     * RHEL
     * CentOS
     * Ubuntu
     * SLES
     * Debian
     * Oracle Linux
   * Mac OS X
   * Bereitgestellt in mehreren Pakettypen:
     * MSI, ZIP, TAR, DEB, RPM und DMG

    Bei Docker stehen zertifizierte Docker-Containerimages für Zulu JDK, JRE und JRE (monitorlos) für mehrere Betriebssystem-Basisimages zur Verfügung.

    Hub:

    * [JDK](https://hub.docker.com/_/microsoft-java-jdk)
    * [JRE](https://hub.docker.com/_/microsoft-java-jre)
    * [JRE (monitorlos)](https://hub.docker.com/_/microsoft-java-jre-headless)

4. Kostenlos

   * Microsoft stellt Ihnen kostenlos alles zur Verfügung, was Sie zum Erstellen und Skalieren von Java-Apps in Azure benötigen. Über Zulu erhalten Sie kostenlose Sicherheitsupdates und plattformspezifische Fehlerbehebungen für Java-Apps.
   * [Java Flight Recorder und Mission Control](java-jdk-flight-recorder-and-mission-control.md) stehen in Zulu Java 8, 11 und 12 (Vorschauversion) zur Verfügung.

5. Technische Vorschauversion von Versionen ohne LTS

   * Mit technischen Vorschauversionen können Sie nach und nach neue Features testen, die im Rahmen kurzfristiger Versionen bereitgestellt und letztendlich zu Java 17 LTS weiterentwickelt werden.

6. Upstreaming von OpenJDK-Änderungen

   * Azul Systems-Committers pushen Zulu-Änderungen an OpenJDK, wodurch ein umfassendes und gesamtheitliches Upstreamrepository entsteht.

Java-Entwickler können wie gewohnt ihre eigenen Java-Runtimes (einschließlich Oracle JDK und Red Hat JDK) in Azure verwenden und dabei die sichere Infrastruktur und die umfangreichen Dienste nutzen. Die Produktionsedition von Oracle Java SE ist ebenfalls für Java-Entwickler verfügbar, um Java-Workloads auf virtuellen Windows- oder Linux-Computern in Azure ausführen zu können.

## <a name="use-for-local-development"></a>Verwendung für lokale Entwicklung 

Entwickler können Java-JDKs für Azure und Azure Stack zur Verwendung in lokalen Entwicklungsumgebungen [herunterladen](https://www.azul.com/downloads/azure-only/zulu/). Downloads sind für Windows, Linux und MacOS verfügbar. Unter Linux können Entwickler Pakete auch über die Paket-Manager [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) und [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) abrufen.

Weitere Informationen finden Sie unter [Docker-Images für Azure](java-jdk-docker-images.md).