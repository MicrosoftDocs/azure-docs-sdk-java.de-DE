---
title: Java Flight Recorder und Mission Control
description: Leitfaden zum Sammeln und Überprüfen von App-Daten mithilfe von Java Flight Recorder und Mission Control.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: b27e0f741f1322b7e8e1df363dbb2f40a3d34d53
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568563"
---
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a><span data-ttu-id="aac9d-103">Verwenden von Java Flight Recorder (JFR) und Mission Control</span><span class="sxs-lookup"><span data-stu-id="aac9d-103">Using Java Flight Recorder (JFR) and Mission Control</span></span>

<span data-ttu-id="aac9d-104">Zulu Mission Control ist ein umfassend getesteter Build von JDK Mission Control, der 2018 von Oracle als Open Source-Komponente veröffentlicht wurde und als Projekt im Rahmen von OpenJDK verwaltet wird.</span><span class="sxs-lookup"><span data-stu-id="aac9d-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="aac9d-105">Zusammen mit Flight Recorder bietet Mission Control praktische interaktive Überwachungs- und Verwaltungsfunktionen für Java-Workloads.</span><span class="sxs-lookup"><span data-stu-id="aac9d-105">Coupled with Flight Recorder, Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="aac9d-106">Zulu Mission Control ist mit folgenden JDKs/JREs kompatibel:</span><span class="sxs-lookup"><span data-stu-id="aac9d-106">Zulu Mission Control is compatible with the following JDKs/JREs:</span></span>

* <span data-ttu-id="aac9d-107">Zulu 12.1 und höher</span><span class="sxs-lookup"><span data-stu-id="aac9d-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="aac9d-108">Zulu 11.0 und höher</span><span class="sxs-lookup"><span data-stu-id="aac9d-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="aac9d-109">Zulu 8u202 (8.36) und höher</span><span class="sxs-lookup"><span data-stu-id="aac9d-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="aac9d-110">Oracle OpenJDK 11+15 und höher</span><span class="sxs-lookup"><span data-stu-id="aac9d-110">Oracle OpenJDK 11+15 and later</span></span>
* <span data-ttu-id="aac9d-111">Oracle Java 11.0 und höher</span><span class="sxs-lookup"><span data-stu-id="aac9d-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="aac9d-112">Oracle Java 8.0 und höher</span><span class="sxs-lookup"><span data-stu-id="aac9d-112">Oracle Java 8.0 and later</span></span>

<span data-ttu-id="aac9d-113">Gehen Sie wie folgt vor, um Zulu Mission Control zu installieren, eine Verbindung mit einer JVM-Instanz (Java Virtual Machine) herzustellen und Echtzeitinformationen zu sämtlichen Aspekten einer ausgeführten Anwendung zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="aac9d-113">Follow the steps below to install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application.</span></span>

1.  <span data-ttu-id="aac9d-114">[Installieren Sie eine mit Zulu Mission Control kompatible JDK-/JRE-Instanz.](java-jdk-install.md)</span><span class="sxs-lookup"><span data-stu-id="aac9d-114">[Install a Zulu Mission Control compatible JDK/JRE](java-jdk-install.md).</span></span>

2.  <span data-ttu-id="aac9d-115">Laden Sie Zulu Mission Control über die [Azul-Downloadwebsite](https://www.azul.com/products/zulu-mission-control/) herunter, wählen Sie die passende Version für Ihr System aus, speichern Sie sie lokal, und navigieren Sie zum entsprechenden Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="aac9d-115">Download Zulu Mission Control from [the Azul download site](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

3.  <span data-ttu-id="aac9d-116">Erweitern Sie die heruntergeladene Datei.</span><span class="sxs-lookup"><span data-stu-id="aac9d-116">Expand the downloaded file.</span></span>

    <span data-ttu-id="aac9d-117">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="aac9d-117">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="aac9d-118">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="aac9d-118">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="aac9d-119">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="aac9d-119">**MacOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

4.  <span data-ttu-id="aac9d-120">Starten Sie Ihre Java-Anwendung mit einem der kompatiblen JDKs.</span><span class="sxs-lookup"><span data-stu-id="aac9d-120">Start your Java application using one of the compatible JDKs.</span></span> <span data-ttu-id="aac9d-121">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="aac9d-121">E.g.:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  <span data-ttu-id="aac9d-122">Starten Sie Zulu Mission Control:</span><span class="sxs-lookup"><span data-stu-id="aac9d-122">Start Zulu Mission Control</span></span>

    <span data-ttu-id="aac9d-123">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="aac9d-123">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="aac9d-124">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="aac9d-124">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="aac9d-125">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="aac9d-125">**MacOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

6.  <span data-ttu-id="aac9d-126">Optional: Ändern Sie die JVM-Installation für Mission Control.</span><span class="sxs-lookup"><span data-stu-id="aac9d-126">Switch the JVM installation for Mission Control (Optional)</span></span>

    <span data-ttu-id="aac9d-127">Unter Windows verwendet *zmc.exe* die in der Registrierung konfigurierte JVM-Standardinstallation.</span><span class="sxs-lookup"><span data-stu-id="aac9d-127">On Windows, *zmc.exe* will use the default JVM installation configured in the registry.</span></span> <span data-ttu-id="aac9d-128">Zulu Mission Control muss über ein vollwertiges JDK gestartet werden, um die automatische Erkennung lokaler JVM-Instanzen zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="aac9d-128">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="aac9d-129">Bei Verwendung einer JRE wird die folgende Warnung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="aac9d-129">If this is a JRE, you will see the warning below:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="aac9d-130">![Warnung, bei JRE-basierter JDK-Installation](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="aac9d-130">![Warning if JDK install is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="aac9d-131">Gehen Sie wie folgt vor, um die von Mission Control verwendete JVM-Instanz zu ändern:</span><span class="sxs-lookup"><span data-stu-id="aac9d-131">To change the JVM used by Mission Control, follow these steps:</span></span> 
    1.  <span data-ttu-id="aac9d-132">Öffnen Sie die Konfigurationsdatei *zmc.ini*. Diese befindet sich im gleichen Verzeichnis wie *zmc.exe*.</span><span class="sxs-lookup"><span data-stu-id="aac9d-132">Open *zmc.ini* configuration file, located in the same directory as the *zmc.exe*</span></span>
    2.  <span data-ttu-id="aac9d-133">Fügen Sie vor der Zeile `-vmargs` zwei Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="aac9d-133">Before the line `-vmargs`, add two lines:</span></span>
        * <span data-ttu-id="aac9d-134">Schreiben Sie `–vm` in die erste Zeile.</span><span class="sxs-lookup"><span data-stu-id="aac9d-134">On the first line, write `–vm`</span></span>
        * <span data-ttu-id="aac9d-135">Schreiben Sie den Pfad Ihrer JDK-Installation in die zweite Zeile.</span><span class="sxs-lookup"><span data-stu-id="aac9d-135">On the second line, write the path to your JDK installation.</span></span> <span data-ttu-id="aac9d-136">(Beispiel: `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`)</span><span class="sxs-lookup"><span data-stu-id="aac9d-136">(For example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

7.  <span data-ttu-id="aac9d-137">Suchen Sie die JVM-Instanz, von der Ihre Anwendung ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="aac9d-137">Locate the JVM running your application</span></span>
    1.  <span data-ttu-id="aac9d-138">Klicken Sie links oben im Zulu Mission Control-Fenster auf die Registerkarte **JVM Browser** (JVM-Browser).</span><span class="sxs-lookup"><span data-stu-id="aac9d-138">In the upper left pane of the Zulu Mission Control window click on the tab labelled **JVM Browser**.</span></span>
    2.  <span data-ttu-id="aac9d-139">Wählen Sie links oben das Listenelement für die JVM-Instanz aus, von der Ihre Anwendung ausgeführt wird, und erweitern Sie es.</span><span class="sxs-lookup"><span data-stu-id="aac9d-139">Select and expand the list item in the upper left for your the JVM instance running your application.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="aac9d-140">![Erweitern des Listenelements für Ihre JVM-Instanz in der linken oberen Ecke](../media/jdk/azul-jfr-2.png)</span><span class="sxs-lookup"><span data-stu-id="aac9d-140">![Expand the list item in the upper-left for your JVM instance](../media/jdk/azul-jfr-2.png)</span></span>


8.  <span data-ttu-id="aac9d-141">Starten Sie bei Bedarf eine Flight Recorder-Aufzeichnung.</span><span class="sxs-lookup"><span data-stu-id="aac9d-141">Start a Flight Recording, if necessary</span></span>
    1.  <span data-ttu-id="aac9d-142">Sollte von Flight Recorder angezeigt werden, dass keine Aufzeichnungen vorliegen, starten Sie eine Aufzeichnung. Klicken Sie hierzu auf der Registerkarte des JVM-Browsers mit der rechten Maustaste auf die Flight Recorder-Zeile, und wählen Sie die Option zum Starten einer **Flight Recorder-Aufzeichnung** aus.</span><span class="sxs-lookup"><span data-stu-id="aac9d-142">If the Flight Recorder displays "No Recordings", start one by right-clicking on the Flight Recorder line in the JVM Browser tab and selecting **Start Flight Recording...**</span></span>
    2.  <span data-ttu-id="aac9d-143">Wählen Sie entweder eine Aufzeichnung mit fester Dauer oder eine kontinuierliche Aufzeichnung und entweder eine Profilerstellungskonfiguration (differenziert) oder eine kontinuierliche Konfiguration (weniger Aufwand) aus, und klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="aac9d-143">Select either a fixed duration recording or a continuous recording, and either a Profiling configuration (fine-grained) or a Continuous configuration (lower overhead), then click **Finish**.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="aac9d-144">![Starten einer Flight Recorder-Aufzeichnung](../media/jdk/azul-jfr-3.png)</span><span class="sxs-lookup"><span data-stu-id="aac9d-144">![Start a Flight Recording](../media/jdk/azul-jfr-3.png)</span></span>

9.  <span data-ttu-id="aac9d-145">Speichern Sie die Flight Recorder-Aufzeichnung.</span><span class="sxs-lookup"><span data-stu-id="aac9d-145">Dump the Flight Recording</span></span>
    1.  <span data-ttu-id="aac9d-146">Eine Flight Recorder-Aufzeichnung sollte im JVM-Browser unter der Flight Recorder-Zeile angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="aac9d-146">A Flight Recording should appear below the Flight Recorder line in the JVM Browser.</span></span> <span data-ttu-id="aac9d-147">Klicken Sie mit der rechten Maustaste auf die Zeile der Flight Recorder-Aufzeichnung, und wählen Sie **Dump whole recording** (Gesamte Aufzeichnung speichern) aus.</span><span class="sxs-lookup"><span data-stu-id="aac9d-147">Right-click on the line representing the Flight Recording and select **Dump whole recording**.</span></span>
    2.  <span data-ttu-id="aac9d-148">Im großen Bereich auf der rechten Seite des Zulu Mission Control-Fensters wird eine neue Registerkarte angezeigt.</span><span class="sxs-lookup"><span data-stu-id="aac9d-148">A new tab will appear in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="aac9d-149">Dieser Bereich stellt die Flight Recorder-Aufzeichnung dar, die soeben von der JVM-Instanz gespeichert wurde, von der Ihre Anwendung ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="aac9d-149">This pane represents the Flight Recording just dumped from the JVM running your application.</span></span>

10. <span data-ttu-id="aac9d-150">Untersuchen Sie die Flight Recorder-Aufzeichnung mithilfe von Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="aac9d-150">Examine the Flight Recording using Zulu Mission Control</span></span>
    1.  <span data-ttu-id="aac9d-151">Wählen Sie im linken Bereich des Zulu Mission Control-Fensters die Registerkarte **Outline** (Gliederung) aus, sofern sie noch nicht aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="aac9d-151">If not already activated, select the tab labelled **Outline** in the left pane of the Zulu Mission Control Window.</span></span> <span data-ttu-id="aac9d-152">Diese Registerkarte enthält verschiedene Ansichten der Daten, die in der Flight Recorder-Aufzeichnung gesammelt wurden.</span><span class="sxs-lookup"><span data-stu-id="aac9d-152">This tab contains different views of the data collected in the Flight Recording.</span></span>
 
    > [!div class="mx-imgBorder"]
    <span data-ttu-id="aac9d-153">![Überprüfen der Flight Recorder-Aufzeichnung](../media/jdk/azul-jfr-4.png)</span><span class="sxs-lookup"><span data-stu-id="aac9d-153">![Review the Fliight Recording](../media/jdk/azul-jfr-4.png)</span></span>

## <a name="resources"></a><span data-ttu-id="aac9d-154">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="aac9d-154">Resources</span></span>

<span data-ttu-id="aac9d-155">Wir haben auch ein [Demovideo](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) mit Simon Ritter (stellvertretender CTO von Azul Systems) vorbereitet.</span><span class="sxs-lookup"><span data-stu-id="aac9d-155">We have also prepared a [demonstration video](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="aac9d-156">In diesem Video werden die Konfigurations- und Installationsschritte für Flight Recorder und Zulu Mission Control erläutert.</span><span class="sxs-lookup"><span data-stu-id="aac9d-156">The video walks you through the configuration and setup of both Flight Recorder and Zulu Mission Control.</span></span> <span data-ttu-id="aac9d-157">Die Besprechung von Flight Recorder beginnt bei 31:30.</span><span class="sxs-lookup"><span data-stu-id="aac9d-157">The Flight Recorder discussion starts at 31:30.</span></span>

