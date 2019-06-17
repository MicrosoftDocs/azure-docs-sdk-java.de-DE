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
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a>Verwenden von Java Flight Recorder (JFR) und Mission Control

Zulu Mission Control ist ein umfassend getesteter Build von JDK Mission Control, der 2018 von Oracle als Open Source-Komponente veröffentlicht wurde und als Projekt im Rahmen von OpenJDK verwaltet wird. Zusammen mit Flight Recorder bietet Mission Control praktische interaktive Überwachungs- und Verwaltungsfunktionen für Java-Workloads.

Zulu Mission Control ist mit folgenden JDKs/JREs kompatibel:

* Zulu 12.1 und höher
* Zulu 11.0 und höher
* Zulu 8u202 (8.36) und höher
* Oracle OpenJDK 11+15 und höher
* Oracle Java 11.0 und höher
* Oracle Java 8.0 und höher

Gehen Sie wie folgt vor, um Zulu Mission Control zu installieren, eine Verbindung mit einer JVM-Instanz (Java Virtual Machine) herzustellen und Echtzeitinformationen zu sämtlichen Aspekten einer ausgeführten Anwendung zu erhalten:

1.  [Installieren Sie eine mit Zulu Mission Control kompatible JDK-/JRE-Instanz.](java-jdk-install.md)

2.  Laden Sie Zulu Mission Control über die [Azul-Downloadwebsite](https://www.azul.com/products/zulu-mission-control/) herunter, wählen Sie die passende Version für Ihr System aus, speichern Sie sie lokal, und navigieren Sie zum entsprechenden Verzeichnis.

3.  Erweitern Sie die heruntergeladene Datei.

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

4.  Starten Sie Ihre Java-Anwendung mit einem der kompatiblen JDKs. Beispiel:

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  Starten Sie Zulu Mission Control:

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

6.  Optional: Ändern Sie die JVM-Installation für Mission Control.

    Unter Windows verwendet *zmc.exe* die in der Registrierung konfigurierte JVM-Standardinstallation. Zulu Mission Control muss über ein vollwertiges JDK gestartet werden, um die automatische Erkennung lokaler JVM-Instanzen zu ermöglichen. Bei Verwendung einer JRE wird die folgende Warnung angezeigt:

    > [!div class="mx-imgBorder"]
    ![Warnung, bei JRE-basierter JDK-Installation](../media/jdk/azul-jfr-1.png)

    Gehen Sie wie folgt vor, um die von Mission Control verwendete JVM-Instanz zu ändern: 
    1.  Öffnen Sie die Konfigurationsdatei *zmc.ini*. Diese befindet sich im gleichen Verzeichnis wie *zmc.exe*.
    2.  Fügen Sie vor der Zeile `-vmargs` zwei Zeilen hinzu:
        * Schreiben Sie `–vm` in die erste Zeile.
        * Schreiben Sie den Pfad Ihrer JDK-Installation in die zweite Zeile. (Beispiel: `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`)

7.  Suchen Sie die JVM-Instanz, von der Ihre Anwendung ausgeführt wird.
    1.  Klicken Sie links oben im Zulu Mission Control-Fenster auf die Registerkarte **JVM Browser** (JVM-Browser).
    2.  Wählen Sie links oben das Listenelement für die JVM-Instanz aus, von der Ihre Anwendung ausgeführt wird, und erweitern Sie es.

    > [!div class="mx-imgBorder"]
    ![Erweitern des Listenelements für Ihre JVM-Instanz in der linken oberen Ecke](../media/jdk/azul-jfr-2.png)


8.  Starten Sie bei Bedarf eine Flight Recorder-Aufzeichnung.
    1.  Sollte von Flight Recorder angezeigt werden, dass keine Aufzeichnungen vorliegen, starten Sie eine Aufzeichnung. Klicken Sie hierzu auf der Registerkarte des JVM-Browsers mit der rechten Maustaste auf die Flight Recorder-Zeile, und wählen Sie die Option zum Starten einer **Flight Recorder-Aufzeichnung** aus.
    2.  Wählen Sie entweder eine Aufzeichnung mit fester Dauer oder eine kontinuierliche Aufzeichnung und entweder eine Profilerstellungskonfiguration (differenziert) oder eine kontinuierliche Konfiguration (weniger Aufwand) aus, und klicken Sie auf **Fertig stellen**.

    > [!div class="mx-imgBorder"]
    ![Starten einer Flight Recorder-Aufzeichnung](../media/jdk/azul-jfr-3.png)

9.  Speichern Sie die Flight Recorder-Aufzeichnung.
    1.  Eine Flight Recorder-Aufzeichnung sollte im JVM-Browser unter der Flight Recorder-Zeile angezeigt werden. Klicken Sie mit der rechten Maustaste auf die Zeile der Flight Recorder-Aufzeichnung, und wählen Sie **Dump whole recording** (Gesamte Aufzeichnung speichern) aus.
    2.  Im großen Bereich auf der rechten Seite des Zulu Mission Control-Fensters wird eine neue Registerkarte angezeigt. Dieser Bereich stellt die Flight Recorder-Aufzeichnung dar, die soeben von der JVM-Instanz gespeichert wurde, von der Ihre Anwendung ausgeführt wird.

10. Untersuchen Sie die Flight Recorder-Aufzeichnung mithilfe von Zulu Mission Control.
    1.  Wählen Sie im linken Bereich des Zulu Mission Control-Fensters die Registerkarte **Outline** (Gliederung) aus, sofern sie noch nicht aktiviert ist. Diese Registerkarte enthält verschiedene Ansichten der Daten, die in der Flight Recorder-Aufzeichnung gesammelt wurden.
 
    > [!div class="mx-imgBorder"]
    ![Überprüfen der Flight Recorder-Aufzeichnung](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>Ressourcen

Wir haben auch ein [Demovideo](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) mit Simon Ritter (stellvertretender CTO von Azul Systems) vorbereitet. In diesem Video werden die Konfigurations- und Installationsschritte für Flight Recorder und Zulu Mission Control erläutert. Die Besprechung von Flight Recorder beginnt bei 31:30.

