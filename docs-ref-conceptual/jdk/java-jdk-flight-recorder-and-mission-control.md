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
# <a name="use-java-flight-recorder-and-mission-control"></a>Verwenden von Java Flight Recorder und Mission Control

Zulu Mission Control ist ein umfassend getesteter Build von JDK Mission Control, der 2018 von Oracle als Open Source-Komponente veröffentlicht wurde und als Projekt im Rahmen von OpenJDK verwaltet wird. Zusammen mit Java Flight Recorder (JFR) bietet Mission Control praktische interaktive Überwachungs- und Verwaltungsfunktionen für Java-Workloads.

Zulu Mission Control ist kompatibel mit den folgenden Java Development Kits (JDKs) und Java Runtime Environments (JREs):

* Zulu 12.1 und höher
* Zulu 11.0 und höher
* Zulu 8u202 (8.36) und höher
* Oracle OpenJDK 11 und 15 und höher
* Oracle Java 11.0 und höher
* Oracle Java 8.0 und höher

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a>Installieren von Zulu Mission Control und Herstellen einer Verbindung mit einer JVM

Um Zulu Mission Control zu installieren, eine Verbindung mit einer JVM-Instanz (Java Virtual Machine) herzustellen und Echtzeitinformationen zu sämtlichen Aspekten einer aktiven Anwendung zu erhalten, gehen Sie wie folgt vor:

1.  [Installieren Sie ein JDK und eine JRE, die mit Zulu Mission Control kompatibel sind](java-jdk-install.md).

1.  [Laden Sie Zulu Mission Control herunter](https://www.azul.com/products/zulu-mission-control/), wählen Sie die passende Version für Ihr System aus, speichern Sie diese lokal, und navigieren Sie zu diesem Verzeichnis.

1.  Erweitern Sie die heruntergeladene Datei.

    **Linux:**

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    **Windows:**

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    **macOS:**

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  Starten Sie Ihre Java-Anwendung, indem Sie eines der kompatiblen JDKs verwenden. Beispiel:

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  Starten Sie Zulu Mission Control.

    **Linux:**

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    **Windows:**

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    **macOS:**

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  (Optional) Wechseln Sie die JVM-Installation für Mission Control.

    Auf Windows-Geräten wird von *zmc.exe* die JVM-Standardinstallation verwendet, die in der Registrierung konfiguriert ist. Zulu Mission Control muss über ein vollwertiges JDK gestartet werden, um die automatische Erkennung lokaler JVM-Instanzen zu ermöglichen. Ist die Installation eine JRE, wird keine JVM erkannt, und Sie erhalten die folgende Warnung:

    > [!div class="mx-imgBorder"]
    ![Warnung, wenn die JDK-Installation nur als JRE vorliegt](../media/jdk/azul-jfr-1.png)

    Um die JVM zu wechseln, die von Mission Control verwendet wird, gehen Sie wie folgt vor: 

    a. Öffnen Sie die Konfigurationsdatei *zmc.ini*, die sich im selben Verzeichnis wie die Datei *zmc.exe* befindet.

    b. Fügen Sie vor der Zeile `-vmargs` zwei Zeilen hinzu:  

       * Geben Sie `–vm` in die erste Zeile ein.  
       * Geben Sie in die zweite Zeile den Pfad zu Ihrer JDK-Installation ein (beispielsweise `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).

1.  Suchen Sie nach der JVM, von der Ihre Anwendung ausgeführt wird, indem Sie wie folgt vorgehen:

    a. Wählen Sie im linken Bereich des Fensters „Zulu Mission Control“ die Registerkarte **JVM Browser** aus.

    b. Wählen Sie in der Liste die JVM-Instanz aus, von der Ihre Anwendung ausgeführt wird, und erweitern Sie die Instanz.

    ![Die JVM-Instanz in der erweiterten Liste](../media/jdk/azul-jfr-2.png)


1.  Starten Sie bei Bedarf eine Flight Recorder-Aufzeichnung.

    a. Starten Sie im linken Bereich unter **Flight Recorder**, sofern eine *No Recordings*-Meldung angezeigt wird, eine Aufzeichnung, indem Sie mit der rechten Maustaste auf **Flight Recorder** klicken und dann **Start Flight Recording** auswählen.

    b. Aktivieren Sie entweder **Time fixed recording** oder **Continuous recording**, und wählen Sie entweder eine **Profiling**-Konfiguration (differenziert) oder eine **Continuous**-Konfiguration (weniger Overhead) aus, und wählen Sie dann **Finish** aus.

    ![Starten einer Flight Recorder-Aufzeichnung](../media/jdk/azul-jfr-3.png)

    Eine Flight Recorder-Aufzeichnung sollte im JVM-Browser unter der **Flight Recorder**-Zeile angezeigt werden.

1. Speichern Sie die Flight Recorder-Aufzeichnung. Klicken Sie dazu mit der rechten Maustaste auf die Zeile, die der Flight Recorder-Aufzeichnung entspricht, und wählen Sie dann **Dump whole recording** aus.

    Im großen Bereich auf der rechten Seite des Fensters „Zulu Mission Control“ wird eine neue Registerkarte angezeigt. Dieser Bereich stellt die Flight Recorder-Aufzeichnung dar, die soeben aus der JVM-Instanz gespeichert wurde, von der Ihre Anwendung ausgeführt wird.

1. Werten Sie die Flight Recorder-Aufzeichnung aus, indem Sie Zulu Mission Control verwenden. Wählen Sie dazu im linken Bereich des Fensters „Zulu Mission Control“ die Registerkarte **Outline** aus. Auf dieser Registerkarte werden verschiedene Ansichten der Daten angezeigt, die in der Flight Recorder-Aufzeichnung gesammelt wurden.
 
    ![Überprüfen der Flight Recorder-Aufzeichnung](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>Ressourcen

Wenn Sie weitere Informationen wünschen, navigieren Sie zur Azul Systems-Website, und zeigen Sie [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) an. Der Text des Videos wird von Simon Ritter gesprochen, der stellvertretender technischer Direktor bei Azul Systems ist. Die Besprechung von Flight Recorder beginnt bei 31:30.

