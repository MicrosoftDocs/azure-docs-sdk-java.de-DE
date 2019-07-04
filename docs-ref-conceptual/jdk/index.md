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
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="81e1e-103">Langfristiger Java-Support für Azure und Azure Stack</span><span class="sxs-lookup"><span data-stu-id="81e1e-103">Java long-term support for Azure and Azure Stack</span></span>

<span data-ttu-id="81e1e-104">Als Java-Entwickler für Microsoft Azure und Azure Stack können Sie Java-Produktionsanwendungen mithilfe von [Azul Zulu Enterprise für Azure](https://www.azul.com/downloads/azure-only/zulu/) erstellen und ausführen, ohne dass zusätzliche Supportkosten anfallen.</span><span class="sxs-lookup"><span data-stu-id="81e1e-104">As a Java developer on Microsoft Azure and Azure Stack, you can build and run production Java applications by using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="81e1e-105">Sie können in Azure eine beliebige Java-Runtime verwenden. Wenn Sie aber Zulu verwenden, erhalten Sie kostenlose Wartungsupdates, und Sie können Supportprobleme mit Microsoft lösen.</span><span class="sxs-lookup"><span data-stu-id="81e1e-105">You can use any Java runtime you want on Azure, but when you use Zulu, you get free maintenance updates and you can resolve support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81e1e-106">Java herunterladen und installieren</span><span class="sxs-lookup"><span data-stu-id="81e1e-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support"></a><span data-ttu-id="81e1e-107">Langfristiger Support</span><span class="sxs-lookup"><span data-stu-id="81e1e-107">Long-term support</span></span>

* [<span data-ttu-id="81e1e-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="81e1e-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [<span data-ttu-id="81e1e-109">Java 8</span><span class="sxs-lookup"><span data-stu-id="81e1e-109">Java 8</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [<span data-ttu-id="81e1e-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="81e1e-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="81e1e-111">Technische Vorschauversion</span><span class="sxs-lookup"><span data-stu-id="81e1e-111">Technical preview</span></span>

* [<span data-ttu-id="81e1e-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="81e1e-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="81e1e-113">Was ist Zulu OpenJDK für Azure?</span><span class="sxs-lookup"><span data-stu-id="81e1e-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="81e1e-114">Bei Azul Zulu Enterprise-Builds von OpenJDK handelt es sich um eine kostenlose, plattformübergreifende und produktionsbereite Distribution von OpenJDK für Azure und Azure Stack, die von Microsoft und Azul Systems unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="81e1e-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack that's backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="81e1e-115">Merkmale dieser Distributionen:</span><span class="sxs-lookup"><span data-stu-id="81e1e-115">These distributions are:</span></span>

* <span data-ttu-id="81e1e-116">Hundertprozentige Open-Source-Builds von OpenJDK, die als JDKs (Java Development Kits), JREs (Java Runtime Environments) und steuerungslose (headless) JREs verpackt sind.</span><span class="sxs-lookup"><span data-stu-id="81e1e-116">100 percent open-source builds of OpenJDK that are packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="81e1e-117">Bei diesen Binärdateien handelt es sich um vollständig kompatible und konforme kommerzielle Builds von Java Standard Edition (SE), die mit Java-Anwendungen oder -Komponenten in Azure und Azure Stack verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="81e1e-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="81e1e-118">Bereitgestellt mit langfristigem Support (Long-Term Support, LTS), der Fehlerbehebungen, Leistungsoptimierungen und Sicherheitspatches umfasst.</span><span class="sxs-lookup"><span data-stu-id="81e1e-118">Provided with long-term support (LTS), which includes bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="81e1e-119">Verfügbar für die Entwicklung und Ausführung von Java-Anwendungen unter Windows, Linux und macOS.</span><span class="sxs-lookup"><span data-stu-id="81e1e-119">Available for developing and running Java applications on Windows, Linux, and macOS.</span></span>
* <span data-ttu-id="81e1e-120">Verfügbar als Containerimages in Docker Hub sowie als virtuelle Computer (Windows und Linux) im Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="81e1e-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) in the Azure Marketplace.</span></span>
* <span data-ttu-id="81e1e-121">Sie werden von Azure für verschiedenste Azure-Dienste genutzt. Beispiele:</span><span class="sxs-lookup"><span data-stu-id="81e1e-121">Used by Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="81e1e-122">Azure App Service (Windows)</span><span class="sxs-lookup"><span data-stu-id="81e1e-122">Azure App Service (Windows)</span></span>
  * <span data-ttu-id="81e1e-123">Azure App Service (Linux)</span><span class="sxs-lookup"><span data-stu-id="81e1e-123">Azure App Service (Linux)</span></span>
  * <span data-ttu-id="81e1e-124">Azure-Funktionen</span><span class="sxs-lookup"><span data-stu-id="81e1e-124">Azure Functions</span></span>
  * <span data-ttu-id="81e1e-125">Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="81e1e-125">Azure Service Fabric</span></span>
  * <span data-ttu-id="81e1e-126">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="81e1e-126">Azure HDInsight</span></span>
  * <span data-ttu-id="81e1e-127">Azure Search</span><span class="sxs-lookup"><span data-stu-id="81e1e-127">Azure Search</span></span>
  * <span data-ttu-id="81e1e-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="81e1e-128">Azure DevOps</span></span>
  * <span data-ttu-id="81e1e-129">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="81e1e-129">Azure Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="81e1e-130">Unterstützte Java-Versionen und Zeitplan für Updates</span><span class="sxs-lookup"><span data-stu-id="81e1e-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="81e1e-131">Azul Systems stellt vollständig unterstützte [Zulu Enterprise-Builds von OpenJDK für Azure](https://www.azul.com/downloads/azure-only/zulu/) für alle LTS-Versionen von Java ab Java SE 7, 8 und 11 bereit.</span><span class="sxs-lookup"><span data-stu-id="81e1e-131">Azul Systems provides fully supported [Zulu Enterprise builds of OpenJDK for Azure](https://www.azul.com/downloads/azure-only/zulu/) for all LTS versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="81e1e-132">Weitere Informationen finden Sie in der [Azul-Pressemitteilung](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="81e1e-132">For more information, see the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="81e1e-133">Java SE mit LTS</span><span class="sxs-lookup"><span data-stu-id="81e1e-133">Java SE LTS</span></span>  |<span data-ttu-id="81e1e-134">Support bis</span><span class="sxs-lookup"><span data-stu-id="81e1e-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="81e1e-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="81e1e-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="81e1e-136">Juli 2023</span><span class="sxs-lookup"><span data-stu-id="81e1e-136">July 2023</span></span> |
|<span data-ttu-id="81e1e-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="81e1e-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="81e1e-138">März 2025</span><span class="sxs-lookup"><span data-stu-id="81e1e-138">March 2025</span></span>|
|<span data-ttu-id="81e1e-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="81e1e-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="81e1e-140">September 2026</span><span class="sxs-lookup"><span data-stu-id="81e1e-140">September 2026</span></span>|
|<span data-ttu-id="81e1e-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="81e1e-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="81e1e-142">**Vorschau**</span><span class="sxs-lookup"><span data-stu-id="81e1e-142">**Preview**</span></span>|

<span data-ttu-id="81e1e-143">Für diese JDK-Releases werden vierteljährliche Sicherheitsupdates, Fehlerbehebungen sowie wichtige Out-of-band-Updates und -Patches nach Bedarf bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="81e1e-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span> <span data-ttu-id="81e1e-144">Dieser Support umfasst Zurückportierungen von Sicherheitsupdates sowie die Behebung von Fehlern für Java 7 und 8, die in neueren Versionen von Java (etwa in Java 11) gemeldet wurden.</span><span class="sxs-lookup"><span data-stu-id="81e1e-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 that are reported in newer versions of Java, such as Java 11.</span></span> <span data-ttu-id="81e1e-145">Der Support gewährleistet die kontinuierliche Stabilität und Sicherheit von älteren Java-Versionen.</span><span class="sxs-lookup"><span data-stu-id="81e1e-145">The support ensures the continued stability and security of older versions of Java.</span></span> <span data-ttu-id="81e1e-146">Azure-Kunden können diese Sicherheitsupdates und Fehlerbehebungen für Plattformen beziehen, ohne dass ungeplante Gebühren für Java SE-Abonnements anfallen.</span><span class="sxs-lookup"><span data-stu-id="81e1e-146">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="81e1e-147">Azul Systems verwaltet eine [Java SE-Roadmap](https://www.azul.com/products/azul_support_roadmap/) für diese Releases.</span><span class="sxs-lookup"><span data-stu-id="81e1e-147">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="81e1e-148">Vorteile für Entwickler</span><span class="sxs-lookup"><span data-stu-id="81e1e-148">Benefits for developers</span></span>

<span data-ttu-id="81e1e-149">Die Azul Zulu JDK-Releases bieten folgende Vorteile:</span><span class="sxs-lookup"><span data-stu-id="81e1e-149">The Azul Zulu JDK releases are:</span></span>

* <span data-ttu-id="81e1e-150">Unterstützt von Microsoft und Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="81e1e-150">Backed and supported by both Microsoft and Azul Systems.</span></span>

   * <span data-ttu-id="81e1e-151">Zulu-Binärdateien sind produktionsbereit und werden von Microsoft und Azul Systems unterstützt.</span><span class="sxs-lookup"><span data-stu-id="81e1e-151">Zulu binaries are production ready and backed by Microsoft and Azul Systems.</span></span>
   * <span data-ttu-id="81e1e-152">Zulu wird mit kostenfreiem LTS für Java 7, 8 und 11 bereitgestellt (LTS wird auch für Java 17 bereitgestellt).</span><span class="sxs-lookup"><span data-stu-id="81e1e-152">Zulu comes with zero-cost LTS for Java 7, 8, and 11 (LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="81e1e-153">Java-Versionen müssen nur bei Bedarf aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="81e1e-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="81e1e-154">Java 7 wird bis Juli 2023 unterstützt.</span><span class="sxs-lookup"><span data-stu-id="81e1e-154">Java 7 is supported until July 2023.</span></span> <span data-ttu-id="81e1e-155">Support für Java 8 und 11 wird über 2024 hinaus bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="81e1e-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="81e1e-156">Microsoft ist bestrebt, Zulu intern auf Computern auszuführen, die vielen Azure-Diensten zugrunde liegen.</span><span class="sxs-lookup"><span data-stu-id="81e1e-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

* <span data-ttu-id="81e1e-157">Bereit für die Produktion.</span><span class="sxs-lookup"><span data-stu-id="81e1e-157">Production-ready.</span></span>

   * <span data-ttu-id="81e1e-158">100-prozentige Open-Source für Builds von OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="81e1e-158">100 percent open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="81e1e-159">Direkter Ersatz für zahlreiche Java SE-Distributionen</span><span class="sxs-lookup"><span data-stu-id="81e1e-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="81e1e-160">JDK, JRE und JRE steuerungslos (headless).</span><span class="sxs-lookup"><span data-stu-id="81e1e-160">JDK, JRE, and JRE-headless.</span></span>
   * <span data-ttu-id="81e1e-161">Java 7, 8 und 11.</span><span class="sxs-lookup"><span data-stu-id="81e1e-161">Java 7, 8, and 11.</span></span>
   * <span data-ttu-id="81e1e-162">Überprüfte Konformität mit den Java SE-Spezifikationen, für die die OpenJDK Community Technology Compatibility Kits (TCK) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="81e1e-162">Verified compliant with the Java SE specifications that use the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="81e1e-163">Als Entwickler erhalten Sie weiterhin Produktionsupdates für Java SE, einschließlich Fehlerbehebungen, Leistungsverbesserungen und Sicherheitspatches für Java SE 7, 8 und 11.</span><span class="sxs-lookup"><span data-stu-id="81e1e-163">As a developer, you continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

* <span data-ttu-id="81e1e-164">Unterstützung mehrerer Plattformen</span><span class="sxs-lookup"><span data-stu-id="81e1e-164">Supported for multi-platform.</span></span> <span data-ttu-id="81e1e-165">Zulu unterstützt Binärdateien für mehrere Plattformen und Versionen:</span><span class="sxs-lookup"><span data-stu-id="81e1e-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="81e1e-166">Windows-Client</span><span class="sxs-lookup"><span data-stu-id="81e1e-166">Windows client</span></span>
     * <span data-ttu-id="81e1e-167">10</span><span class="sxs-lookup"><span data-stu-id="81e1e-167">10</span></span>
     * <span data-ttu-id="81e1e-168">8.1</span><span class="sxs-lookup"><span data-stu-id="81e1e-168">8.1</span></span>
     * <span data-ttu-id="81e1e-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="81e1e-169">8, 7</span></span>
   * <span data-ttu-id="81e1e-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="81e1e-170">Windows Server</span></span>
     * <span data-ttu-id="81e1e-171">2016 R2</span><span class="sxs-lookup"><span data-stu-id="81e1e-171">2016 R2</span></span>
     * <span data-ttu-id="81e1e-172">2016</span><span class="sxs-lookup"><span data-stu-id="81e1e-172">2016</span></span>
     * <span data-ttu-id="81e1e-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="81e1e-173">2012 R2</span></span>
     * <span data-ttu-id="81e1e-174">2012</span><span class="sxs-lookup"><span data-stu-id="81e1e-174">2012</span></span>
     * <span data-ttu-id="81e1e-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="81e1e-175">2008 R2</span></span>
   * <span data-ttu-id="81e1e-176">Linux, einschließlich</span><span class="sxs-lookup"><span data-stu-id="81e1e-176">Linux, including</span></span>
     * <span data-ttu-id="81e1e-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="81e1e-177">RHEL</span></span>
     * <span data-ttu-id="81e1e-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="81e1e-178">CentOS</span></span>
     * <span data-ttu-id="81e1e-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="81e1e-179">Ubuntu</span></span>
     * <span data-ttu-id="81e1e-180">SLES</span><span class="sxs-lookup"><span data-stu-id="81e1e-180">SLES</span></span>
     * <span data-ttu-id="81e1e-181">Debian</span><span class="sxs-lookup"><span data-stu-id="81e1e-181">Debian</span></span>
     * <span data-ttu-id="81e1e-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="81e1e-182">Oracle Linux</span></span>
   * <span data-ttu-id="81e1e-183">macOS X</span><span class="sxs-lookup"><span data-stu-id="81e1e-183">macOS X</span></span>
   * <span data-ttu-id="81e1e-184">Bereitstellung in mehreren Pakettypen:</span><span class="sxs-lookup"><span data-stu-id="81e1e-184">Delivery in multiple package types:</span></span>
     * <span data-ttu-id="81e1e-185">MSI, ZIP, TAR, DEB, RPM und DMG</span><span class="sxs-lookup"><span data-stu-id="81e1e-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="81e1e-186">Bei Docker stehen zertifizierte Docker-Containerimages für Zulu JDK, JRE und JRE (monitorlos) für mehrere Betriebssystem-Basisimages zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="81e1e-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="81e1e-187">Hub:</span><span class="sxs-lookup"><span data-stu-id="81e1e-187">Hub:</span></span>

    * [<span data-ttu-id="81e1e-188">JDK</span><span class="sxs-lookup"><span data-stu-id="81e1e-188">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
    * [<span data-ttu-id="81e1e-189">JRE</span><span class="sxs-lookup"><span data-stu-id="81e1e-189">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
    * [<span data-ttu-id="81e1e-190">JRE (monitorlos)</span><span class="sxs-lookup"><span data-stu-id="81e1e-190">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

* <span data-ttu-id="81e1e-191">Keine Kosten.</span><span class="sxs-lookup"><span data-stu-id="81e1e-191">No cost.</span></span>

   * <span data-ttu-id="81e1e-192">Microsoft stellt Ihnen kostenlos alles zur Verfügung, was Sie zum Erstellen und Skalieren von Java-Apps in Azure benötigen.</span><span class="sxs-lookup"><span data-stu-id="81e1e-192">Microsoft provides everything you need to build and scale Java apps on Azure, at no cost to you.</span></span> <span data-ttu-id="81e1e-193">Über Zulu erhalten Sie kostenlose Sicherheitsupdates und plattformspezifische Fehlerbehebungen für Java-Apps.</span><span class="sxs-lookup"><span data-stu-id="81e1e-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="81e1e-194">[Java Flight Recorder und Mission Control](java-jdk-flight-recorder-and-mission-control.md) stehen in Zulu Java 8, 11 und 12 (Vorschauversion) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="81e1e-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

* <span data-ttu-id="81e1e-195">Verfügbar als technische Vorschauversion von Versionen ohne LTS.</span><span class="sxs-lookup"><span data-stu-id="81e1e-195">Available as tech preview of non-LTS versions.</span></span>

   * <span data-ttu-id="81e1e-196">Mit technischen Vorschauversionen können Sie neues Features schrittweise testen, während diese in kurzfristigen Versionen bereitgestellt werden, die letztendlich zu Java 17 LTS weiterentwickelt werden.</span><span class="sxs-lookup"><span data-stu-id="81e1e-196">With tech previews, you can progressively test new features as they're delivered, in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

* <span data-ttu-id="81e1e-197">Änderungen an OpenJDK werden in Upstreamrichtung gesendet.</span><span class="sxs-lookup"><span data-stu-id="81e1e-197">Changes to OpenJDK are sent upstream.</span></span>

   * <span data-ttu-id="81e1e-198">Azul Systems-Committers pushen Zulu-Änderungen an OpenJDK, wodurch ein umfassendes und gesamtheitliches Upstreamrepository entsteht.</span><span class="sxs-lookup"><span data-stu-id="81e1e-198">Azul Systems committers push Zulu changes to OpenJDK, which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="81e1e-199">Wie immer können Sie als Java-Entwickler Ihren eigenen Java-Runtimes in Azure einbeziehen, einschließlich des Oracle-JDKs und des Red Hat-JDKs.</span><span class="sxs-lookup"><span data-stu-id="81e1e-199">As always, as a Java developer, you can bring to Azure your own Java runtimes, including the Oracle JDK and the Red Hat JDK.</span></span> <span data-ttu-id="81e1e-200">Sie können auch die sichere Infrastruktur und die funktionsreichen Dienste verwenden.</span><span class="sxs-lookup"><span data-stu-id="81e1e-200">You can also use the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="81e1e-201">Die Produktionsedition von Oracle Java SE ist für Sie verfügbar, um Java-Workloads auf virtuellen Windows- oder Linux-Computern in Azure ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="81e1e-201">The production edition of Oracle Java SE is available to you for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-java-jdks-for-local-development"></a><span data-ttu-id="81e1e-202">Verwenden von Java-JDKs für die lokale Entwicklung</span><span class="sxs-lookup"><span data-stu-id="81e1e-202">Use Java JDKs for local development</span></span> 

<span data-ttu-id="81e1e-203">Sie können [Java-JDKs für Azure und Azure Stack](https://www.azul.com/downloads/azure-only/zulu/) zur Verwendung in Ihrer lokalen Entwicklungsumgebungen herunterladen.</span><span class="sxs-lookup"><span data-stu-id="81e1e-203">You can [download Java JDKs for Azure and Azure Stack](https://www.azul.com/downloads/azure-only/zulu/) for use in your local development environments.</span></span> <span data-ttu-id="81e1e-204">Downloads sind für Windows, Linux und MacOS verfügbar.</span><span class="sxs-lookup"><span data-stu-id="81e1e-204">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="81e1e-205">Wenn Sie mit Linux arbeiten, können Sie Pakete auch über die Paket-Manager [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) und [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) abrufen.</span><span class="sxs-lookup"><span data-stu-id="81e1e-205">If you're working on Linux, you can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="81e1e-206">Weitere Informationen finden Sie unter [Docker-Images für Azure](java-jdk-docker-images.md).</span><span class="sxs-lookup"><span data-stu-id="81e1e-206">For additional guidance, see [Docker images for Azure](java-jdk-docker-images.md).</span></span>
