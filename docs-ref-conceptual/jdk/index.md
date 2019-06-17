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
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="80766-103">Langfristiger Java-Support für Azure und Azure Stack</span><span class="sxs-lookup"><span data-stu-id="80766-103">Java Long-Term Support for Azure and Azure Stack</span></span>

<span data-ttu-id="80766-104">Java-Entwickler, die mit Azure und Azure Stack arbeiten, können Java-Produktionsanwendungen mithilfe von [Azul Zulu Enterprise für Azure](https://www.azul.com/downloads/azure-only/zulu/) erstellen und ausführen, ohne dass zusätzliche Supportkosten anfallen.</span><span class="sxs-lookup"><span data-stu-id="80766-104">Java developers on Azure and Azure Stack can build and run production Java applications using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="80766-105">Sie können in Azure eine beliebige Java-Runtime verwenden. Bei Verwendung von Zulu erhalten Sie jedoch kostenlose Wartungsupdates und können Supportprobleme bei Microsoft erstellen.</span><span class="sxs-lookup"><span data-stu-id="80766-105">You can use any Java runtime you want on Azure, but when you use Zulu you get free maintenance updates and can create support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="80766-106">Java herunterladen und installieren</span><span class="sxs-lookup"><span data-stu-id="80766-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support-lts"></a><span data-ttu-id="80766-107">Langfristiger Support (Long-Term Support, LTS)</span><span class="sxs-lookup"><span data-stu-id="80766-107">Long-term support (LTS)</span></span>

* [<span data-ttu-id="80766-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="80766-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [<span data-ttu-id="80766-109">Java 8</span><span class="sxs-lookup"><span data-stu-id="80766-109">Java 8</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [<span data-ttu-id="80766-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="80766-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="80766-111">Technische Vorschauversion</span><span class="sxs-lookup"><span data-stu-id="80766-111">Technical preview</span></span>

* [<span data-ttu-id="80766-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="80766-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="80766-113">Was ist Zulu OpenJDK für Azure?</span><span class="sxs-lookup"><span data-stu-id="80766-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="80766-114">Bei Azul Zulu Enterprise-Builds von OpenJDK handelt es sich um eine kostenlose, plattformübergreifende und produktionsbereite Distribution von OpenJDK für Azure und Azure Stack, die von Microsoft und Azul Systems unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="80766-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="80766-115">Merkmale dieser Distributionen:</span><span class="sxs-lookup"><span data-stu-id="80766-115">These distributions are:</span></span>

* <span data-ttu-id="80766-116">Hundertprozentige Open-Source-Builds von OpenJDK, verpackt als JDKs (Java Development Kits), JREs (Java Runtime Environments) und monitorlose JREs.</span><span class="sxs-lookup"><span data-stu-id="80766-116">100% open source builds of OpenJDK packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="80766-117">Bei diesen Binärdateien handelt es sich um vollständig kompatible und konforme kommerzielle Builds von Java Standard Edition (SE), die mit Java-Anwendungen oder -Komponenten in Azure und Azure Stack verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="80766-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="80766-118">Langfristiger Support – einschließlich Fehlerbehebungen, Leistungsoptimierungen und Sicherheitspatches</span><span class="sxs-lookup"><span data-stu-id="80766-118">Provided with long-term support including bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="80766-119">Verfügbar für die Entwicklung und Ausführung von Java-Anwendungen unter Windows, Linux und macOS</span><span class="sxs-lookup"><span data-stu-id="80766-119">Available for developing and running Java applications on Windows, Linux, and MacOS.</span></span>
* <span data-ttu-id="80766-120">Verfügbar als Containerimages in Docker Hub sowie als virtuelle Computer (Windows und Linux) im Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="80766-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) on Azure Marketplace.</span></span>
* <span data-ttu-id="80766-121">Sie werden von Microsoft Azure für verschiedenste Azure-Dienste genutzt. Beispiele:</span><span class="sxs-lookup"><span data-stu-id="80766-121">Used by Microsoft Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="80766-122">App Service (Windows)</span><span class="sxs-lookup"><span data-stu-id="80766-122">App Service Windows</span></span>
  * <span data-ttu-id="80766-123">App Service (Linux)</span><span class="sxs-lookup"><span data-stu-id="80766-123">App Service Linux</span></span>
  * <span data-ttu-id="80766-124">Functions</span><span class="sxs-lookup"><span data-stu-id="80766-124">Functions</span></span>
  * <span data-ttu-id="80766-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="80766-125">Service Fabric</span></span>
  * <span data-ttu-id="80766-126">HDInsight</span><span class="sxs-lookup"><span data-stu-id="80766-126">HDInsight</span></span>
  * <span data-ttu-id="80766-127">Suchen,</span><span class="sxs-lookup"><span data-stu-id="80766-127">Search</span></span>
  * <span data-ttu-id="80766-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="80766-128">Azure DevOps</span></span>
  * <span data-ttu-id="80766-129">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="80766-129">Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="80766-130">Unterstützte Java-Versionen und Zeitplan für Updates</span><span class="sxs-lookup"><span data-stu-id="80766-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="80766-131">Azul Systems stellt vollständig unterstützte [Zulu Enterprise-Builds von OpenJDK für Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) bereit, der mit allen LTS-Versionen von Java (ab Java SE 7, 8 und 11) verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="80766-131">Azul Systems provides fully-supported [Zulu Enterprise builds of OpenJDK for Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) for all long-term support (LTS) versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="80766-132">Weitere Informationen finden Sie in der [Pressemitteilung von Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="80766-132">More information can be found in the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="80766-133">Java SE mit LTS</span><span class="sxs-lookup"><span data-stu-id="80766-133">Java SE LTS</span></span>  |<span data-ttu-id="80766-134">Support bis</span><span class="sxs-lookup"><span data-stu-id="80766-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="80766-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="80766-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="80766-136">Juli 2023</span><span class="sxs-lookup"><span data-stu-id="80766-136">July 2023</span></span> |
|<span data-ttu-id="80766-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="80766-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="80766-138">März 2025</span><span class="sxs-lookup"><span data-stu-id="80766-138">March 2025</span></span>|
|<span data-ttu-id="80766-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="80766-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="80766-140">September 2026</span><span class="sxs-lookup"><span data-stu-id="80766-140">Sept. 2026</span></span>|
|<span data-ttu-id="80766-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="80766-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="80766-142">**VORSCHAUVERSION**</span><span class="sxs-lookup"><span data-stu-id="80766-142">**PREVIEW**</span></span>|

<span data-ttu-id="80766-143">Für diese JDK-Releases werden vierteljährliche Sicherheitsupdates, Fehlerbehebungen sowie wichtige Out-of-band-Updates und -Patches nach Bedarf bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="80766-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span>  <span data-ttu-id="80766-144">Dieser Support umfasst die Zurückportierung von Sicherheitsupdates sowie die Behebung von Fehlern für Java 7 und 8, die in neueren Versionen von Java (etwa in Java 11) gemeldet wurden, um die kontinuierliche Stabilität und Sicherheit von älteren Java-Versionen zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="80766-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 reported in newer versions of Java such as Java 11, which ensures the continued stability and security of older versions of Java.</span></span>  <span data-ttu-id="80766-145">Azure-Kunden können diese Sicherheitsupdates und Fehlerbehebungen für Plattformen beziehen, ohne dass ungeplante Gebühren für Java SE-Abonnements anfallen.</span><span class="sxs-lookup"><span data-stu-id="80766-145">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="80766-146">Azul Systems verwaltet eine [Java SE-Roadmap](https://www.azul.com/products/azul_support_roadmap/) für diese Releases.</span><span class="sxs-lookup"><span data-stu-id="80766-146">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="80766-147">Vorteile für Entwickler</span><span class="sxs-lookup"><span data-stu-id="80766-147">Benefits for developers</span></span>

<span data-ttu-id="80766-148">Die Azul Zulu JDK-Releases bieten folgende Vorteile:</span><span class="sxs-lookup"><span data-stu-id="80766-148">The Azul Zulu JDK releases are:</span></span>

1. <span data-ttu-id="80766-149">Unterstützt von Microsoft und Azul Systems</span><span class="sxs-lookup"><span data-stu-id="80766-149">Backed and supported by both Microsoft and Azul Systems</span></span>

   * <span data-ttu-id="80766-150">Zulu-Binärdateien sind produktionsbereit und werden von Microsoft und Azul Systems unterstützt.</span><span class="sxs-lookup"><span data-stu-id="80766-150">Zulu binaries are production-ready and backed by Microsoft and Azul Systems</span></span>
   * <span data-ttu-id="80766-151">Zulu bietet kostenlosen langfristigen Support (Long-Term Support, LTS) für Java 7, 8 und 11.</span><span class="sxs-lookup"><span data-stu-id="80766-151">Zulu comes with zero-cost long-term support (LTS) for Java 7, 8, and 11.</span></span> <span data-ttu-id="80766-152">(LTS wird auch für Java 17 bereitgestellt.)</span><span class="sxs-lookup"><span data-stu-id="80766-152">(LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="80766-153">Java-Versionen müssen nur bei Bedarf aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="80766-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="80766-154">Support für Java 7 wird bis Juli 2023 bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="80766-154">Java 7 supported until July 2023.</span></span> <span data-ttu-id="80766-155">Support für Java 8 und 11 wird über 2024 hinaus bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="80766-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="80766-156">Microsoft ist bestrebt, Zulu intern auf Computern auszuführen, die vielen Azure-Diensten zugrunde liegen.</span><span class="sxs-lookup"><span data-stu-id="80766-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

2. <span data-ttu-id="80766-157">Bereit für die Produktion</span><span class="sxs-lookup"><span data-stu-id="80766-157">Production-ready</span></span>

   * <span data-ttu-id="80766-158">100-prozentige Open-Source-Builds von OpenJDK</span><span class="sxs-lookup"><span data-stu-id="80766-158">100% open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="80766-159">Direkter Ersatz für zahlreiche Java SE-Distributionen</span><span class="sxs-lookup"><span data-stu-id="80766-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="80766-160">JDK, JRE und JRE (monitorlos)</span><span class="sxs-lookup"><span data-stu-id="80766-160">JDK, JRE, and JRE-headless</span></span>
   * <span data-ttu-id="80766-161">Java 7, 8 und 11</span><span class="sxs-lookup"><span data-stu-id="80766-161">Java 7, 8, and 11</span></span>
   * <span data-ttu-id="80766-162">Konformität mit den Java SE-Spezifikationen unter Verwendung des OpenJDK Community Technology Compatibility Kits (TCK) geprüft</span><span class="sxs-lookup"><span data-stu-id="80766-162">Verified compliant with the Java SE  specifications using the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="80766-163">Entwickler erhalten weiterhin Produktionsupdates für Java SE – einschließlich Fehlerbehebungen, Leistungsverbesserungen und Sicherheitspatches für Java SE 7, 8 und 11.</span><span class="sxs-lookup"><span data-stu-id="80766-163">Developers will continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

3. <span data-ttu-id="80766-164">Unterstützung mehrerer Plattformen</span><span class="sxs-lookup"><span data-stu-id="80766-164">Supported for multi-platform.</span></span> <span data-ttu-id="80766-165">Zulu unterstützt Binärdateien für mehrere Plattformen und Versionen:</span><span class="sxs-lookup"><span data-stu-id="80766-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="80766-166">Windows-Client</span><span class="sxs-lookup"><span data-stu-id="80766-166">Windows Client</span></span>
     * <span data-ttu-id="80766-167">10</span><span class="sxs-lookup"><span data-stu-id="80766-167">10</span></span>
     * <span data-ttu-id="80766-168">8.1</span><span class="sxs-lookup"><span data-stu-id="80766-168">8.1</span></span>
     * <span data-ttu-id="80766-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="80766-169">8, 7</span></span>
   * <span data-ttu-id="80766-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="80766-170">Windows Server</span></span>
     * <span data-ttu-id="80766-171">2016 R2</span><span class="sxs-lookup"><span data-stu-id="80766-171">2016R2</span></span>
     * <span data-ttu-id="80766-172">2016</span><span class="sxs-lookup"><span data-stu-id="80766-172">2016</span></span>
     * <span data-ttu-id="80766-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="80766-173">2012 R2</span></span>
     * <span data-ttu-id="80766-174">2012</span><span class="sxs-lookup"><span data-stu-id="80766-174">2012</span></span>
     * <span data-ttu-id="80766-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="80766-175">2008 R2</span></span>
   * <span data-ttu-id="80766-176">Linux, einschließlich</span><span class="sxs-lookup"><span data-stu-id="80766-176">Linux, including</span></span>
     * <span data-ttu-id="80766-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="80766-177">RHEL</span></span>
     * <span data-ttu-id="80766-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="80766-178">CentOS</span></span>
     * <span data-ttu-id="80766-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="80766-179">Ubuntu</span></span>
     * <span data-ttu-id="80766-180">SLES</span><span class="sxs-lookup"><span data-stu-id="80766-180">SLES</span></span>
     * <span data-ttu-id="80766-181">Debian</span><span class="sxs-lookup"><span data-stu-id="80766-181">Debian</span></span>
     * <span data-ttu-id="80766-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="80766-182">Oracle Linux</span></span>
   * <span data-ttu-id="80766-183">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="80766-183">Mac OS X</span></span>
   * <span data-ttu-id="80766-184">Bereitgestellt in mehreren Pakettypen:</span><span class="sxs-lookup"><span data-stu-id="80766-184">delivered in multiple package types:</span></span>
     * <span data-ttu-id="80766-185">MSI, ZIP, TAR, DEB, RPM und DMG</span><span class="sxs-lookup"><span data-stu-id="80766-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="80766-186">Bei Docker stehen zertifizierte Docker-Containerimages für Zulu JDK, JRE und JRE (monitorlos) für mehrere Betriebssystem-Basisimages zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="80766-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="80766-187">Hub:</span><span class="sxs-lookup"><span data-stu-id="80766-187">Hub:</span></span>

    * [<span data-ttu-id="80766-188">JDK</span><span class="sxs-lookup"><span data-stu-id="80766-188">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
    * [<span data-ttu-id="80766-189">JRE</span><span class="sxs-lookup"><span data-stu-id="80766-189">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
    * [<span data-ttu-id="80766-190">JRE (monitorlos)</span><span class="sxs-lookup"><span data-stu-id="80766-190">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

4. <span data-ttu-id="80766-191">Kostenlos</span><span class="sxs-lookup"><span data-stu-id="80766-191">No cost</span></span>

   * <span data-ttu-id="80766-192">Microsoft stellt Ihnen kostenlos alles zur Verfügung, was Sie zum Erstellen und Skalieren von Java-Apps in Azure benötigen.</span><span class="sxs-lookup"><span data-stu-id="80766-192">Microsoft provides everything you need to build and scale Java apps on Azure at no cost to you.</span></span> <span data-ttu-id="80766-193">Über Zulu erhalten Sie kostenlose Sicherheitsupdates und plattformspezifische Fehlerbehebungen für Java-Apps.</span><span class="sxs-lookup"><span data-stu-id="80766-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="80766-194">[Java Flight Recorder und Mission Control](java-jdk-flight-recorder-and-mission-control.md) stehen in Zulu Java 8, 11 und 12 (Vorschauversion) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="80766-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

5. <span data-ttu-id="80766-195">Technische Vorschauversion von Versionen ohne LTS</span><span class="sxs-lookup"><span data-stu-id="80766-195">Tech Preview of Non-LTS versions</span></span>

   * <span data-ttu-id="80766-196">Mit technischen Vorschauversionen können Sie nach und nach neue Features testen, die im Rahmen kurzfristiger Versionen bereitgestellt und letztendlich zu Java 17 LTS weiterentwickelt werden.</span><span class="sxs-lookup"><span data-stu-id="80766-196">Tech previews provide you with opportunities to progressively test new features as they are delivered in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

6. <span data-ttu-id="80766-197">Upstreaming von OpenJDK-Änderungen</span><span class="sxs-lookup"><span data-stu-id="80766-197">Changes to OpenJDK are up-streamed</span></span>

   * <span data-ttu-id="80766-198">Azul Systems-Committers pushen Zulu-Änderungen an OpenJDK, wodurch ein umfassendes und gesamtheitliches Upstreamrepository entsteht.</span><span class="sxs-lookup"><span data-stu-id="80766-198">Azul Systems committers push Zulu changes to OpenJDK which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="80766-199">Java-Entwickler können wie gewohnt ihre eigenen Java-Runtimes (einschließlich Oracle JDK und Red Hat JDK) in Azure verwenden und dabei die sichere Infrastruktur und die umfangreichen Dienste nutzen.</span><span class="sxs-lookup"><span data-stu-id="80766-199">As always, Java developers can bring their own Java run-times, including Oracle JDK and Red Hat JDK, to Azure and use  the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="80766-200">Die Produktionsedition von Oracle Java SE ist ebenfalls für Java-Entwickler verfügbar, um Java-Workloads auf virtuellen Windows- oder Linux-Computern in Azure ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="80766-200">The production edition of Oracle Java SE is also available to Java developers for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-for-local-development"></a><span data-ttu-id="80766-201">Verwendung für lokale Entwicklung</span><span class="sxs-lookup"><span data-stu-id="80766-201">Use for local development</span></span> 

<span data-ttu-id="80766-202">Entwickler können Java-JDKs für Azure und Azure Stack zur Verwendung in lokalen Entwicklungsumgebungen [herunterladen](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="80766-202">Developers can [download](https://www.azul.com/downloads/azure-only/zulu/) Java JDKs for Azure and Azure Stack for use in local development environments.</span></span> <span data-ttu-id="80766-203">Downloads sind für Windows, Linux und MacOS verfügbar.</span><span class="sxs-lookup"><span data-stu-id="80766-203">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="80766-204">Unter Linux können Entwickler Pakete auch über die Paket-Manager [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) und [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) abrufen.</span><span class="sxs-lookup"><span data-stu-id="80766-204">Developers working on Linux can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="80766-205">Weitere Informationen finden Sie unter [Docker-Images für Azure](java-jdk-docker-images.md).</span><span class="sxs-lookup"><span data-stu-id="80766-205">For additional guidance see [Docker images for Azure](java-jdk-docker-images.md).</span></span>