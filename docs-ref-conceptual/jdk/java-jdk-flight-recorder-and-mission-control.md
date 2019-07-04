---
title: Java Flight Recorder und Mission Control
description: Leitfaden zum Sammeln und Überprüfen von App-Daten mithilfe von Java Flight Recorder und Mission Control.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 64f64f2e5891fccf9d62510f39bd99d73457d590
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533624"
---
# <a name="use-java-flight-recorder-and-mission-control"></a><span data-ttu-id="f72a2-103">Verwenden von Java Flight Recorder und Mission Control</span><span class="sxs-lookup"><span data-stu-id="f72a2-103">Use Java Flight Recorder and Mission Control</span></span>

<span data-ttu-id="f72a2-104">Zulu Mission Control ist ein umfassend getesteter Build von JDK Mission Control, der 2018 von Oracle als Open Source-Komponente veröffentlicht wurde und als Projekt im Rahmen von OpenJDK verwaltet wird.</span><span class="sxs-lookup"><span data-stu-id="f72a2-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open-sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="f72a2-105">Zusammen mit Java Flight Recorder (JFR) bietet Mission Control praktische interaktive Überwachungs- und Verwaltungsfunktionen für Java-Workloads.</span><span class="sxs-lookup"><span data-stu-id="f72a2-105">Coupled with Java Flight Recorder (JFR), Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="f72a2-106">Zulu Mission Control ist kompatibel mit den folgenden Java Development Kits (JDKs) und Java Runtime Environments (JREs):</span><span class="sxs-lookup"><span data-stu-id="f72a2-106">Zulu Mission Control is compatible with the following Java Development Kits (JDKs) and Java Runtime Environments (JREs):</span></span>

* <span data-ttu-id="f72a2-107">Zulu 12.1 und höher</span><span class="sxs-lookup"><span data-stu-id="f72a2-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="f72a2-108">Zulu 11.0 und höher</span><span class="sxs-lookup"><span data-stu-id="f72a2-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="f72a2-109">Zulu 8u202 (8.36) und höher</span><span class="sxs-lookup"><span data-stu-id="f72a2-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="f72a2-110">Oracle OpenJDK 11 und 15 und höher</span><span class="sxs-lookup"><span data-stu-id="f72a2-110">Oracle OpenJDK 11 and 15 and later</span></span>
* <span data-ttu-id="f72a2-111">Oracle Java 11.0 und höher</span><span class="sxs-lookup"><span data-stu-id="f72a2-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="f72a2-112">Oracle Java 8.0 und höher</span><span class="sxs-lookup"><span data-stu-id="f72a2-112">Oracle Java 8.0 and later</span></span>

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a><span data-ttu-id="f72a2-113">Installieren von Zulu Mission Control und Herstellen einer Verbindung mit einer JVM</span><span class="sxs-lookup"><span data-stu-id="f72a2-113">Install Zulu Mission Control and connect to a JVM</span></span>

<span data-ttu-id="f72a2-114">Um Zulu Mission Control zu installieren, eine Verbindung mit einer JVM-Instanz (Java Virtual Machine) herzustellen und Echtzeitinformationen zu sämtlichen Aspekten einer aktiven Anwendung zu erhalten, gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="f72a2-114">To install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application, do the following:</span></span>

1.  <span data-ttu-id="f72a2-115">[Installieren Sie ein JDK und eine JRE, die mit Zulu Mission Control kompatibel sind](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="f72a2-115">[Install a Zulu Mission Control-compatible JDK and JRE](java-jdk-install.md).</span></span>

1.  <span data-ttu-id="f72a2-116">[Laden Sie Zulu Mission Control herunter](https://www.azul.com/products/zulu-mission-control/), wählen Sie die passende Version für Ihr System aus, speichern Sie diese lokal, und navigieren Sie zu diesem Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="f72a2-116">[Download Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

1.  <span data-ttu-id="f72a2-117">Erweitern Sie die heruntergeladene Datei.</span><span class="sxs-lookup"><span data-stu-id="f72a2-117">Expand the downloaded file.</span></span>

    <span data-ttu-id="f72a2-118">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="f72a2-118">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="f72a2-119">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="f72a2-119">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="f72a2-120">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="f72a2-120">**macOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  <span data-ttu-id="f72a2-121">Starten Sie Ihre Java-Anwendung, indem Sie eines der kompatiblen JDKs verwenden.</span><span class="sxs-lookup"><span data-stu-id="f72a2-121">Start your Java application by using one of the compatible JDKs.</span></span> <span data-ttu-id="f72a2-122">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f72a2-122">For example:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  <span data-ttu-id="f72a2-123">Starten Sie Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="f72a2-123">Start Zulu Mission Control.</span></span>

    <span data-ttu-id="f72a2-124">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="f72a2-124">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="f72a2-125">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="f72a2-125">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="f72a2-126">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="f72a2-126">**macOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  <span data-ttu-id="f72a2-127">(Optional) Wechseln Sie die JVM-Installation für Mission Control.</span><span class="sxs-lookup"><span data-stu-id="f72a2-127">(Optional) Switch the JVM installation for Mission Control.</span></span>

    <span data-ttu-id="f72a2-128">Auf Windows-Geräten wird von *zmc.exe* die JVM-Standardinstallation verwendet, die in der Registrierung konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="f72a2-128">On Windows devices, *zmc.exe* uses the default JVM installation that's configured in the registry.</span></span> <span data-ttu-id="f72a2-129">Zulu Mission Control muss über ein vollwertiges JDK gestartet werden, um die automatische Erkennung lokaler JVM-Instanzen zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="f72a2-129">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="f72a2-130">Ist die Installation eine JRE, wird keine JVM erkannt, und Sie erhalten die folgende Warnung:</span><span class="sxs-lookup"><span data-stu-id="f72a2-130">If the installation is a JRE, no JVM will be detected, and you will receive the following warning:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f72a2-131">![Warnung, wenn die JDK-Installation nur als JRE vorliegt](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="f72a2-131">![Warning if JDK installation is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="f72a2-132">Um die JVM zu wechseln, die von Mission Control verwendet wird, gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="f72a2-132">To change the JVM that's used by Mission Control, do the following:</span></span> 

    <span data-ttu-id="f72a2-133">a.</span><span class="sxs-lookup"><span data-stu-id="f72a2-133">a.</span></span> <span data-ttu-id="f72a2-134">Öffnen Sie die Konfigurationsdatei *zmc.ini*, die sich im selben Verzeichnis wie die Datei *zmc.exe* befindet.</span><span class="sxs-lookup"><span data-stu-id="f72a2-134">Open the *zmc.ini* configuration file, which is in the same directory as the *zmc.exe* file.</span></span>

    <span data-ttu-id="f72a2-135">b.</span><span class="sxs-lookup"><span data-stu-id="f72a2-135">b.</span></span> <span data-ttu-id="f72a2-136">Fügen Sie vor der Zeile `-vmargs` zwei Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="f72a2-136">Before the line `-vmargs`, add two lines:</span></span>  

       * <span data-ttu-id="f72a2-137">Geben Sie `–vm` in die erste Zeile ein.</span><span class="sxs-lookup"><span data-stu-id="f72a2-137">On the first line, enter `–vm`.</span></span>  
       * <span data-ttu-id="f72a2-138">Geben Sie in die zweite Zeile den Pfad zu Ihrer JDK-Installation ein (beispielsweise `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="f72a2-138">On the second line, enter the path to your JDK installation (for example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

1.  <span data-ttu-id="f72a2-139">Suchen Sie nach der JVM, von der Ihre Anwendung ausgeführt wird, indem Sie wie folgt vorgehen:</span><span class="sxs-lookup"><span data-stu-id="f72a2-139">Locate the JVM that's running your application by doing the following:</span></span>

    <span data-ttu-id="f72a2-140">a.</span><span class="sxs-lookup"><span data-stu-id="f72a2-140">a.</span></span> <span data-ttu-id="f72a2-141">Wählen Sie im linken Bereich des Fensters „Zulu Mission Control“ die Registerkarte **JVM Browser** aus.</span><span class="sxs-lookup"><span data-stu-id="f72a2-141">In the left pane of the Zulu Mission Control window, select the **JVM Browser** tab.</span></span>

    <span data-ttu-id="f72a2-142">b.</span><span class="sxs-lookup"><span data-stu-id="f72a2-142">b.</span></span> <span data-ttu-id="f72a2-143">Wählen Sie in der Liste die JVM-Instanz aus, von der Ihre Anwendung ausgeführt wird, und erweitern Sie die Instanz.</span><span class="sxs-lookup"><span data-stu-id="f72a2-143">In the list, select and expand the JVM instance that's running your application.</span></span>

    ![Die JVM-Instanz in der erweiterten Liste](../media/jdk/azul-jfr-2.png)


1.  <span data-ttu-id="f72a2-145">Starten Sie bei Bedarf eine Flight Recorder-Aufzeichnung.</span><span class="sxs-lookup"><span data-stu-id="f72a2-145">Start a flight recording, if necessary.</span></span>

    <span data-ttu-id="f72a2-146">a.</span><span class="sxs-lookup"><span data-stu-id="f72a2-146">a.</span></span> <span data-ttu-id="f72a2-147">Starten Sie im linken Bereich unter **Flight Recorder**, sofern eine *No Recordings*-Meldung angezeigt wird, eine Aufzeichnung, indem Sie mit der rechten Maustaste auf **Flight Recorder** klicken und dann **Start Flight Recording** auswählen.</span><span class="sxs-lookup"><span data-stu-id="f72a2-147">In the left pane, under **Flight Recorder**, if a *No Recordings* message is displayed, start a recording by right-clicking **Flight Recorder** and then selecting **Start Flight Recording**.</span></span>

    <span data-ttu-id="f72a2-148">b.</span><span class="sxs-lookup"><span data-stu-id="f72a2-148">b.</span></span> <span data-ttu-id="f72a2-149">Aktivieren Sie entweder **Time fixed recording** oder **Continuous recording**, und wählen Sie entweder eine **Profiling**-Konfiguration (differenziert) oder eine **Continuous**-Konfiguration (weniger Overhead) aus, und wählen Sie dann **Finish** aus.</span><span class="sxs-lookup"><span data-stu-id="f72a2-149">Select either **Time fixed recording** or **Continuous recording**, and either a **Profiling** configuration (fine-grained) or a **Continuous** configuration (lower overhead), and then select **Finish**.</span></span>

    ![Starten einer Flight Recorder-Aufzeichnung](../media/jdk/azul-jfr-3.png)

    <span data-ttu-id="f72a2-151">Eine Flight Recorder-Aufzeichnung sollte im JVM-Browser unter der **Flight Recorder**-Zeile angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="f72a2-151">A flight recording should appear below the **Flight Recorder** line in the JVM browser.</span></span>

1. <span data-ttu-id="f72a2-152">Speichern Sie die Flight Recorder-Aufzeichnung.</span><span class="sxs-lookup"><span data-stu-id="f72a2-152">Dump the flight recording.</span></span> <span data-ttu-id="f72a2-153">Klicken Sie dazu mit der rechten Maustaste auf die Zeile, die der Flight Recorder-Aufzeichnung entspricht, und wählen Sie dann **Dump whole recording** aus.</span><span class="sxs-lookup"><span data-stu-id="f72a2-153">To do so, right-click the line that represents the flight recording, and then select **Dump whole recording**.</span></span>

    <span data-ttu-id="f72a2-154">Im großen Bereich auf der rechten Seite des Fensters „Zulu Mission Control“ wird eine neue Registerkarte angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f72a2-154">A new tab appears in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="f72a2-155">Dieser Bereich stellt die Flight Recorder-Aufzeichnung dar, die soeben aus der JVM-Instanz gespeichert wurde, von der Ihre Anwendung ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f72a2-155">This pane represents the flight recording that was just dumped from the JVM that's running your application.</span></span>

1. <span data-ttu-id="f72a2-156">Werten Sie die Flight Recorder-Aufzeichnung aus, indem Sie Zulu Mission Control verwenden.</span><span class="sxs-lookup"><span data-stu-id="f72a2-156">Examine the flight recording by using Zulu Mission Control.</span></span> <span data-ttu-id="f72a2-157">Wählen Sie dazu im linken Bereich des Fensters „Zulu Mission Control“ die Registerkarte **Outline** aus.</span><span class="sxs-lookup"><span data-stu-id="f72a2-157">To do so, select the **Outline** tab in the left pane of the Zulu Mission Control window.</span></span> <span data-ttu-id="f72a2-158">Auf dieser Registerkarte werden verschiedene Ansichten der Daten angezeigt, die in der Flight Recorder-Aufzeichnung gesammelt wurden.</span><span class="sxs-lookup"><span data-stu-id="f72a2-158">This tab displays various views of the data that's collected in the flight recording.</span></span>
 
    ![Überprüfen der Flight Recorder-Aufzeichnung](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a><span data-ttu-id="f72a2-160">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f72a2-160">Resources</span></span>

<span data-ttu-id="f72a2-161">Wenn Sie weitere Informationen wünschen, navigieren Sie zur Azul Systems-Website, und zeigen Sie [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) an.</span><span class="sxs-lookup"><span data-stu-id="f72a2-161">To learn more, go to the Azul Systems site and view [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/).</span></span> <span data-ttu-id="f72a2-162">Der Text des Videos wird von Simon Ritter gesprochen, der stellvertretender technischer Direktor bei Azul Systems ist.</span><span class="sxs-lookup"><span data-stu-id="f72a2-162">The video is narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="f72a2-163">Die Besprechung von Flight Recorder beginnt bei 31:30.</span><span class="sxs-lookup"><span data-stu-id="f72a2-163">The Flight Recorder discussion starts at 31:30.</span></span>

