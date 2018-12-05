---
title: Veröffentlichen einer Spring Boot-App als Docker-Container mit dem Azure-Toolkit für IntelliJ
description: Erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine Web-App in Microsoft Azure als Docker-Container veröffentlichen.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4b8527ced4aa8010a26b6d1f99f76943a875e66e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338704"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Veröffentlichen einer Spring Boot-App als Docker-Container mit dem Azure-Toolkit für IntelliJ

[Spring Framework] ist eine Open Source-Lösung, die Java-Entwickler bei der Erstellung professioneller Anwendungen unterstützt. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.

[Docker] ist eine Open Source-Lösung, die Entwickler beim Automatisieren der Bereitstellung, Skalierung und Verwaltung ihrer in Containern ausgeführten Anwendungen unterstützt.

In diesem Tutorial erfahren Sie, wie Sie mithilfe des Azure-Toolkits für IntelliJ eine Spring Boot-Anwendung als Docker-Container in Microsoft Azure bereitstellen.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>Klonen des standardmäßigen Spring Boot-Docker-Repositorys

Mit den folgenden Schritten wird das Spring Boot-Docker-Repository mithilfe von IntelliJ geklont. Informationen zur Verwendung einer Befehlszeile finden unter [Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].

1. Öffnen Sie IntelliJ.

1. Wählen Sie auf der Willkommensseite in der Liste **Check out from version control** (Von Versionskontrolle auschecken) die Option **GitHub** aus.

   ![GitHub-Option für die Versionskontrolle][CL01]

1. Geben Sie Ihre Anmeldeinformationen ein, wenn Sie dazu aufgefordert werden.

   * GitHub-Anmeldung unter Verwendung von Benutzername und Kennwort: 

      ![Dialogfeld für die Eingabe von Benutzername und Kennwort für GitHub][CL02a]

   * Tokenbasierte GitHub-Anmeldung: 

      ![Dialogfeld für die Eingabe eines GitHub-Tokens][CL02b]

1. Geben Sie **https://github.com/spring-guides/gs-spring-boot-docker.git** als URL des Repositorys ein, geben Sie Ihren lokalen Pfad und Ordnerinformationen an, und klicken Sie dann auf **Klonen**.

   ![Dialogfeld „Repository klonen“][CL03]

1. Wenn Sie zum Erstellen eines IntelliJ-Projekts aufgefordert werden, wählen Sie **Nein** aus.

   ![Ablehnen der Erstellung eines IntelliJ-Projekts][CL04]

1. Klicken Sie auf der Willkommensseite auf **Projekt importieren**.

   ![Klicken auf „Projekt importieren“][CL05]

1. Suchen Sie den Pfad, an dem Sie das Spring Boot-Repository geklont haben, wählen Sie den **gesamten** Ordner unter dem Stammverzeichnis aus, und klicken Sie auf **OK**.

   ![Auswählen eines zu importierenden Ordners][CL06]

1. Wählen Sie **Create project from existing sources** (Projekt aus vorhandenen Quellen erstellen) aus, wenn Sie dazu aufgefordert werden.

   ![Option zum Erstellen eines Projekts auf der Grundlage vorhandener Quellen][CL07]

1. Geben Sie einen Projektnamen ein, oder übernehmen Sie den Standardnamen, überprüfen Sie den Pfad für den **gesamten** Ordner, und klicken Sie auf **Weiter**.

   ![Angeben des Projektnamens][CL08]

1. Passen Sie Verzeichnisse für den Import an, und klicken Sie auf **Weiter**.

   ![Auswahl von Verzeichnissen][CL09]

1. Überprüfen Sie die zu importierenden Bibliotheken, und klicken Sie dann auf **Weiter**.

   ![Überprüfen der Projektbibliotheken][CL10]

1. Überprüfen Sie die Modulstruktur, und klicken Sie dann auf **Weiter**.

   ![Überprüfen der Modulstruktur][CL11]

1. Geben Sie Ihr JDK, an und klicken Sie dann auf **Weiter**.

   ![Angeben eines JDKs][CL12]

1. Klicken Sie auf **Fertig stellen**.

   ![Schaltfläche „Fertig stellen“][CL13]

IntelliJ importiert die Spring Boot-App als Projekt und zeigt nach Abschluss des Importvorgangs die Struktur an.

![Spring Boot-App in IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Erstellen Ihrer Spring Boot-App

### <a name="build-the-app-by-using-the-maven-pom"></a>Erstellen der App mithilfe des Maven-POMs

1. Öffnen Sie das Maven-Toolfenster, sofern es nicht bereits geöffnet ist. Klicken Sie auf **Ansicht** > **Toolfenster** > **Maven-Projekte**.

   ![Befehle „Toolfenster“ und „Maven-Projekte“][BU01]

1. Klicken Sie im Maven-Toolfenster mit der rechten Maustaste auf **Paket**, und wählen Sie **Run Maven Build** (Maven-Build ausführen) aus. (Sollte Ihr Maven-Projekt nicht automatisch angezeigt werden, klicken Sie auf der Maven-Symbolleiste auf das Symbol **Reimport** (Erneut importieren).)

   ![Befehl zum Ausführen des Maven-Builds][BU02]

1. Wenn Ihre Spring Boot-App erfolgreich erstellt wurde, zeigt IntelliJ eine entsprechende **Meldung** an.

   ![Meldung nach erfolgreicher Erstellung][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Erstellen eines bereitstellungsfähigen Artefakts

Zum Veröffentlichen Ihrer Spring Boot-App müssen Sie ein bereitstellungsfähiges Artefakt erstellen. Führen Sie die folgenden Schritte aus:

1. Öffnen Sie Ihr Web-App-Projekt in IntelliJ.

1. Klicken Sie auf **Datei** und dann auf **Projektstruktur**.

   ![Befehl „Projektstruktur“][ART01]

1. Klicken Sie auf das grüne Plussymbol (**+**), um ein Artefakt hinzuzufügen. Klicken Sie anschließend auf **JAR** und dann auf **Leer**.

   ![Hinzufügen eines Artefakts][ART02]

1. Benennen Sie Ihr Artefakt und stellen Sie dabei sicher, dass Sie nicht die Erweiterung „.jar“ anfügen. Geben Sie anschließend den Zielordner für die Maven-Ausgabe an.

   ![Angeben der Eigenschaften des Artefakts][ART03]

1. Erstellen Sie ein Manifest für Ihr Artefakt (optional):

   a. Klicken Sie auf **Create Manifest** (Manifest erstellen).

      ![Klicken auf die Schaltfläche „Create Manifest“ (Manifest erstellen)][ART04a]

   b. Wählen Sie den Standardpfad für das Artefakt aus, und klicken Sie dann auf **OK**.

      ![Angeben des Artefaktpfads][ART04b]

   c. Klicken Sie auf die Auslassungspunkte (**...**), um die Hauptklasse zu suchen.

      ![Suchen der Hauptklasse][ART04c]

   d. Wählen Sie die Hauptklasse aus, und klicken Sie anschließend auf **OK**.

      ![Angeben der Hauptklasse][ART04d]

1. Klicken Sie auf **OK**.

   ![Schließen des Dialogfelds mit der Projektstruktur][ART05]

> [!NOTE]
> Weitere Informationen zum Erstellen von Artefakten in IntelliJ finden Sie auf der JetBrains-Website unter [Konfigurieren von Artefakten].
>

### <a name="build-the-artifact-for-deployment"></a>Erstellen des Artefakts für die Bereitstellung

1. Klicken Sie auf **Erstellen** und anschließend auf **Artefakte**.

   ![Befehl zum Erstellen von Artefakten][BU04]

1. Klicken Sie auf **Erstellen**, wenn das Kontextmenü **Build Artifact** (Artefakt erstellen) angezeigt wird.

   ![Kontextmenü für die Artefakterstellung][BU05]

IntelliJ zeigt das vollständige Artefakt für Ihre Spring Boot-App im Projekt-Toolfenster an.

   ![Erstelltes Artefakt][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Veröffentlichen Ihrer Web-App in Azure mithilfe eines Docker-Containers

1. Melden Sie sich gemäß der [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ][Azure Sign In for IntelliJ] bei Ihrem Azure-Konto an, sofern noch nicht geschehen.

1. Klicken Sie im Toolfenster „Project Explorer“ mit der rechten Maustaste auf das Projekt, und wählen Sie dann **Azure** > **Publish as Docker Container** (Als Docker-Container veröffentlichen) aus.

   ![Befehl zum Veröffentlichen als Docker-Container][PU01]

1. Wenn das Dialogfeld **Deploy Docker Container on Azure** (Bereitstellen des Docker-Containers in Azure) erscheint, werden alle vorhandenen Docker-Hosts angezeigt. Wenn Sie in einem vorhandenen Host bereitstellen möchten, fahren Sie mit Schritt 4 fort. Führen Sie andernfalls die folgenden Schritte aus, um einen Host zu erstellen:

   a. Klicken Sie auf das grüne Plussymbol (**+**).

      ![Hinzufügen eines neuen Docker-Hosts][PU02]

   b. Wenn das Dialogfeld **Create Docker Host** (Docker-Host erstellen) angezeigt wird, können Sie wahlweise die Standardeinstellungen übernehmen oder beliebige benutzerdefinierte Einstellungen für den neuen Docker-Host angeben. (Ausführliche Beschreibungen der verschiedenen Einstellungen finden Sie unter [Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für IntelliJ][Publish Container with Azure Toolkit].) Klicken Sie auf **Weiter**, nachdem Sie die gewünschten Einstellungen eingegeben haben.

      ![Angeben von Docker-Hostoptionen][PU03a]

   c. Sie können wahlweise vorhandene Anmeldeinformationen aus einem Azure-Schlüsseltresor verwenden oder neue Docker-Anmeldeinformationen eingeben. Klicken Sie auf **Fertig stellen**, nachdem Sie Ihre Optionen angegeben haben.

      ![Angeben von Docker-Hostanmeldeinformationen][PU03b]

1. Wählen Sie Ihren Docker-Host aus, und klicken Sie dann auf **Weiter**.

   ![Auswählen des zu verwendenden Docker-Hosts][PU04]

1. Geben Sie auf der letzten Seite des Dialogfelds **Deploy Docker Container on Azure** (Bereitstellen des Docker-Containers in Azure) folgende Optionen an:

   a. Sie können entweder einen benutzerdefinierten Namen für den Container angeben, der Ihren Docker-Container hostet, oder die Standardeinstellung übernehmen.

   b. Geben Sie die TCP-Ports für Ihren Docker-Host mit folgender Syntax ein: *[externer Port]*:*[interner Port]*. **80:8080** gibt beispielsweise den externen Port 80 und den internen Spring Boot-Standardport 8080 an.
   
      Wenn Sie den internen Port angepasst haben (beispielsweise durch Bearbeiten der Datei „application.yml“), müssen Sie diese Portnummer angeben, damit das Routing in Azure ordnungsgemäß funktioniert.

   c. Klicken Sie nach dem Konfigurieren dieser Optionen auf **Fertig stellen**.

   ![Bereitstellen eines Docker-Containers in Azure][PU05]

1. Nachdem die Veröffentlichung des Azure-Toolkits abgeschlossen ist, zeigt das Azure-Aktivitätsprotokoll den Status **Veröffentlicht** an.

   ![Docker-Host erfolgreich bereitgestellt][PU06]

## <a name="next-steps"></a>Nächste Schritte

Informationen zu weiteren Spring Boot-App-Erstellungsmethoden mit IntelliJ finden Sie auf der JetBrains-Website unter [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) (Erstellen von Spring Boot-Projekten).

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Konfigurieren von Artefakten]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
