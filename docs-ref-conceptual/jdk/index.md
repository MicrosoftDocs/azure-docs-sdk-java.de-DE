---
title: Java-JDKs und LTS (Long-Term Support) für Azure-Entwicklung
description: In diesem Artikel werden Downloadlinks und eine Erklärung des Azure-Supports für das Entwickeln und Ausführen von Java-Anwendungen vorgestellt.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 1bb93f775686b5b0f127c586dda802f4eb5f775d
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533636"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a>Langfristiger Java-Support für Azure und Azure Stack

Als Java-Entwickler für Microsoft Azure und Azure Stack können Sie Java-Produktionsanwendungen mithilfe von [Azul Zulu Enterprise für Azure](https://www.azul.com/downloads/azure-only/zulu/) erstellen und ausführen, ohne dass zusätzliche Supportkosten anfallen. Sie können in Azure eine beliebige Java-Runtime verwenden. Wenn Sie aber Zulu verwenden, erhalten Sie kostenlose Wartungsupdates, und Sie können Supportprobleme mit Microsoft lösen.

> [!div class="nextstepaction"]
> [Java herunterladen und installieren](java-jdk-install.md)

## <a name="long-term-support"></a>Langfristiger Support

* [Java 11](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [Java 7](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a>Technische Vorschauversion

* [Java 12](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a>Was ist Zulu OpenJDK für Azure?

Bei Azul Zulu Enterprise-Builds von OpenJDK handelt es sich um eine kostenlose, plattformübergreifende und produktionsbereite Distribution von OpenJDK für Azure und Azure Stack, die von Microsoft und Azul Systems unterstützt wird. Merkmale dieser Distributionen:

* Hundertprozentige Open-Source-Builds von OpenJDK, die als JDKs (Java Development Kits), JREs (Java Runtime Environments) und steuerungslose (headless) JREs verpackt sind. Bei diesen Binärdateien handelt es sich um vollständig kompatible und konforme kommerzielle Builds von Java Standard Edition (SE), die mit Java-Anwendungen oder -Komponenten in Azure und Azure Stack verwendet werden können.
* Bereitgestellt mit langfristigem Support (Long-Term Support, LTS), der Fehlerbehebungen, Leistungsoptimierungen und Sicherheitspatches umfasst.
* Verfügbar für die Entwicklung und Ausführung von Java-Anwendungen unter Windows, Linux und macOS.
* Verfügbar als Containerimages in Docker Hub sowie als virtuelle Computer (Windows und Linux) im Azure Marketplace.
* Sie werden von Azure für verschiedenste Azure-Dienste genutzt. Beispiele:
  * Azure App Service (Windows)
  * Azure App Service (Linux)
  * Azure-Funktionen
  * Azure Service Fabric
  * Azure HDInsight
  * Azure Search
  * Azure DevOps
  * Azure Cloud Shell  

## <a name="supported-java-versions-and-update-schedule"></a>Unterstützte Java-Versionen und Zeitplan für Updates

Azul Systems stellt vollständig unterstützte [Zulu Enterprise-Builds von OpenJDK für Azure](https://www.azul.com/downloads/azure-only/zulu/) für alle LTS-Versionen von Java ab Java SE 7, 8 und 11 bereit. Weitere Informationen finden Sie in der [Azul-Pressemitteilung](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).

|Java SE mit LTS  |Support bis  |
|---------|----------|
|[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7) |Juli 2023 |
|[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8) |März 2025|
|[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11) |September 2026|
|[![Java 12](../media/jdk/java-12.png)]() |**Vorschau**|

Für diese JDK-Releases werden vierteljährliche Sicherheitsupdates, Fehlerbehebungen sowie wichtige Out-of-band-Updates und -Patches nach Bedarf bereitgestellt. Dieser Support umfasst Zurückportierungen von Sicherheitsupdates sowie die Behebung von Fehlern für Java 7 und 8, die in neueren Versionen von Java (etwa in Java 11) gemeldet wurden. Der Support gewährleistet die kontinuierliche Stabilität und Sicherheit von älteren Java-Versionen. Azure-Kunden können diese Sicherheitsupdates und Fehlerbehebungen für Plattformen beziehen, ohne dass ungeplante Gebühren für Java SE-Abonnements anfallen.

Azul Systems verwaltet eine [Java SE-Roadmap](https://www.azul.com/products/azul_support_roadmap/) für diese Releases.

## <a name="benefits-for-developers"></a>Vorteile für Entwickler

Die Azul Zulu JDK-Releases bieten folgende Vorteile:

* Unterstützt von Microsoft und Azul Systems.

   * Zulu-Binärdateien sind produktionsbereit und werden von Microsoft und Azul Systems unterstützt.
   * Zulu wird mit kostenfreiem LTS für Java 7, 8 und 11 bereitgestellt (LTS wird auch für Java 17 bereitgestellt). Java-Versionen müssen nur bei Bedarf aktualisiert werden.
   * Java 7 wird bis Juli 2023 unterstützt. Support für Java 8 und 11 wird über 2024 hinaus bereitgestellt.
   * Microsoft ist bestrebt, Zulu intern auf Computern auszuführen, die vielen Azure-Diensten zugrunde liegen.

* Bereit für die Produktion.

   * 100-prozentige Open-Source für Builds von OpenJDK.
   * Direkter Ersatz für zahlreiche Java SE-Distributionen
   * JDK, JRE und JRE steuerungslos (headless).
   * Java 7, 8 und 11.
   * Überprüfte Konformität mit den Java SE-Spezifikationen, für die die OpenJDK Community Technology Compatibility Kits (TCK) verwendet wird.
   * Als Entwickler erhalten Sie weiterhin Produktionsupdates für Java SE, einschließlich Fehlerbehebungen, Leistungsverbesserungen und Sicherheitspatches für Java SE 7, 8 und 11.

* Unterstützung mehrerer Plattformen Zulu unterstützt Binärdateien für mehrere Plattformen und Versionen:

   * Windows-Client
     * 10
     * 8.1
     * 8, 7
   * Windows Server
     * 2016 R2
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
   * macOS X
   * Bereitstellung in mehreren Pakettypen:
     * MSI, ZIP, TAR, DEB, RPM und DMG

    Bei Docker stehen zertifizierte Docker-Containerimages für Zulu JDK, JRE und JRE (monitorlos) für mehrere Betriebssystem-Basisimages zur Verfügung.

    Hub:

    * [JDK](https://hub.docker.com/_/microsoft-java-jdk)
    * [JRE](https://hub.docker.com/_/microsoft-java-jre)
    * [JRE (monitorlos)](https://hub.docker.com/_/microsoft-java-jre-headless)

* Keine Kosten.

   * Microsoft stellt Ihnen kostenlos alles zur Verfügung, was Sie zum Erstellen und Skalieren von Java-Apps in Azure benötigen. Über Zulu erhalten Sie kostenlose Sicherheitsupdates und plattformspezifische Fehlerbehebungen für Java-Apps.
   * [Java Flight Recorder und Mission Control](java-jdk-flight-recorder-and-mission-control.md) stehen in Zulu Java 8, 11 und 12 (Vorschauversion) zur Verfügung.

* Verfügbar als technische Vorschauversion von Versionen ohne LTS.

   * Mit technischen Vorschauversionen können Sie neues Features schrittweise testen, während diese in kurzfristigen Versionen bereitgestellt werden, die letztendlich zu Java 17 LTS weiterentwickelt werden.

* Änderungen an OpenJDK werden in Upstreamrichtung gesendet.

   * Azul Systems-Committers pushen Zulu-Änderungen an OpenJDK, wodurch ein umfassendes und gesamtheitliches Upstreamrepository entsteht.

Wie immer können Sie als Java-Entwickler Ihren eigenen Java-Runtimes in Azure einbeziehen, einschließlich des Oracle-JDKs und des Red Hat-JDKs. Sie können auch die sichere Infrastruktur und die funktionsreichen Dienste verwenden. Die Produktionsedition von Oracle Java SE ist für Sie verfügbar, um Java-Workloads auf virtuellen Windows- oder Linux-Computern in Azure ausführen zu können.

## <a name="use-java-jdks-for-local-development"></a>Verwenden von Java-JDKs für die lokale Entwicklung 

Sie können [Java-JDKs für Azure und Azure Stack](https://www.azul.com/downloads/azure-only/zulu/) zur Verwendung in Ihrer lokalen Entwicklungsumgebungen herunterladen. Downloads sind für Windows, Linux und MacOS verfügbar. Wenn Sie mit Linux arbeiten, können Sie Pakete auch über die Paket-Manager [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) und [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) abrufen.

Weitere Informationen finden Sie unter [Docker-Images für Azure](java-jdk-docker-images.md).
