---
title: Veröffentlichen einer Spring Boot-App als Docker-Container mit dem Azure-Toolkit für Eclipse
description: Erfahren Sie, wie Sie mit dem Azure-Toolkit für Eclipse eine Web-App in Microsoft Azure als Docker-Container veröffentlichen.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: c116e0712afd8e48983f946f43eddfd0c79c0ba8
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2018
ms.locfileid: "38075472"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Veröffentlichen einer Spring Boot-App als Docker-Container mit dem Azure-Toolkit für Eclipse

[Spring-Framework] ist eine Open Source-Lösung, die Java-Entwickler bei der Erstellung professioneller Anwendungen unterstützt. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.

[Docker] ist eine Open Source-Lösung, die Entwickler beim Automatisieren der Bereitstellung, Skalierung und Verwaltung ihrer in Containern ausgeführten Anwendungen unterstützt.

In diesem Tutorial erfahren Sie, wie Sie mithilfe des Azure-Toolkits für Eclipse eine Spring Boot-Anwendung als Docker-Container in Microsoft Azure bereitstellen.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a>Klonen des standardmäßigen Spring Boot-Docker-Repositorys

### <a name="import-the-public-repository"></a>Importieren des öffentlichen Repositorys

Mit den folgenden Schritte wird das Spring Boot-Docker-Repository auf Ihrem lokalen Computer mithilfe von IntelliJ geklont. Informationen zur Verwendung einer Befehlszeile finden Sie unter [Deploy a Spring Boot application on Linux in the Azure Container Service][Deploy Spring Boot on Linux in AKS] (Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service).

1. Öffnen Sie Eclipse.

1. Klicken Sie auf **Datei** > **Importieren**.

   ![Menü „Datei importieren“][CL01]

1. Wenn das Dialogfeld **Importieren** geöffnet wird:

   a. Erweitern Sie **Git**.

   b. Wählen Sie **Projekte aus Git**.
   
   c. Klicken Sie auf **Weiter**.

   ![Dialogfeld „Importieren“][CL02]

1. Auf der Seite **Repositoryquelle auswählen**:

   a. Wählen Sie **URI klonen** aus.
   
   b. Klicken Sie auf **Weiter**.

   ![Seite „Repositoryquelle auswählen“][CL03]

1. Auf der Seite **Quelle Git-Repository**:

   a. Geben Sie `https://github.com/spring-guides/gs-spring-boot-docker.git` für den **URI** ein. Dadurch sollten die Felder **Host** und **Repositorypfad** automatisch mit den korrekten Werten aufgefüllt werden.
   
   b. Da das Spring Boot-Repository öffentlich ist, müssen Sie nicht Ihren Git-Benutzernamen und das Kennwort eingeben.
   
   c. Klicken Sie auf **Weiter**.

   ![Seite „Quelle Git-Repository“][CL04]

1. Klicken Sie auf der Seite **Verzweigungsauswahl** auf **Weiter**.

   ![Seite „Verzweigungsauswahl“][CL05]

1. Auf der Seite **Lokales Ziel**:

   a. Geben Sie den lokalen Ordner an, in dem Ihr lokales Repository angelegt werden soll.
   
   b. Klicken Sie auf **Weiter**.

   ![Seite „Lokales Ziel“][CL06]

1. Auf der Seite **Assistent zum Importieren von Projekten auswählen**:

   a. Wählen Sie **Als allgemeines Projekt importieren** aus.
   
   b. Klicken Sie auf **Weiter**.

   ![Seite „Assistent zum Importieren von Projekten auswählen“][CL07]

1. Auf der Seite **Projekte importieren**:

   a. Geben Sie Ihren Projektnamen an.
   
   b. Klicken Sie auf **Fertig stellen**.

   ![Seite „Projekte importieren“][CL08]

1. Nachdem das Repository erfolgreich geklont wurde, wird eine Liste aller Dateien in Eclipse angezeigt.

   ![Lokales Repository][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Erstellen eines Maven-Projekts aus dem lokalen Repository

Das Docker-Repository von Spring Boot enthält ein abgeschlossenes Maven-Projekt, das Sie für dieses Tutorial verwenden können. 

1. Klicken Sie auf **Datei** > **Importieren**.

   ![Befehl zum Importieren im Menü „Datei“][CL01]

1. Wenn das Dialogfeld **Importieren** geöffnet wird:

   a. Erweitern Sie **Maven**.
   
   b. Wählen Sie **Vorhandene Maven-Projekte**.
   
   c. Klicken Sie auf **Weiter**.

   ![Dialogfeld „Importieren“][MV01]

1. Auf der Seite **Maven-Projekte**:

   a. Geben Sie unter **Stammverzeichnis** den **vollständigen** Ordner in Ihrem lokalen Repository an.
   
   b. Erweitern Sie den Abschnitt **Erweitert**, und geben Sie einen benutzerdefinierten Namen für **Namensvorlage** ein.
   
   c. Aktivieren Sie das Kontrollkästchen für die Datei **pom.xml** im Projekt.
   
   d. Klicken Sie auf **Fertig stellen**.

   ![Seite „Maven-Projekte“][MV02]

1. Nachdem das Maven-Projekt erfolgreich geöffnet wurde, wird ein zweites Projekt in Eclipse aufgelistet.

   ![Lokales Maven-Projekt][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Erstellen der Spring Boot-App mithilfe von Maven

1. Wählen Sie im Projekt-Explorer von Eclipse das Maven-Projekt aus.

1. Klicken Sie auf **Ausführen** > **Ausführen als** > **Maven-Build**.

   ![Befehle zum Ausführen als Maven-Build][BU01]

1. Nachdem die Anwendung erfolgreich erstellt wurde, wird im Konsolenfenster der Status angezeigt.

   ![Erfolgreicher Maven-Build][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Veröffentlichen Ihrer Web-App in Azure mithilfe eines Docker-Containers

1. Wählen Sie im Projekt-Explorer von Eclipse das Maven-Projekt aus.

1. Klicken Sie auf das Azure-Menü **Veröffentlichen** und anschließend auf **Publish as Docker Container** (Als Docker-Container veröffentlichen).

   ![Befehl „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PU01]

1. Wenn das Dialogfeld **Deploying Docker Container on Azure** (Docker-Container wird in Azure bereitgestellt) angezeigt wird:

   a. Geben Sie einen benutzerdefinierten Docker-Imagenamen ein.
   
   b. Geben Sie für **Artifact to deploy** (Bereitzustellendes Artefakt) den Pfad zur Datei **gs-spring-boot-docker-0.1.0.jar** an, die Sie soeben erstellt haben.

   ![Angeben von Docker-Optionen][PU02]

   Alle vorhandenen Docker-Hosts werden angezeigt. 

1. Fahren Sie für die Bereitstellung in einem vorhandenen Host mit Schritt 5 fort. Führen Sie andernfalls die folgenden Schritte aus, um einen Host zu erstellen:

   a. Klicken Sie auf **Hinzufügen**.

      ![Hinzufügen eines neuen Docker-Hosts][PU03]

   b. Wenn das Dialogfeld **Create Docker Host** (Docker-Host erstellen) angezeigt wird, können Sie wahlweise die Standardeinstellungen übernehmen oder beliebige benutzerdefinierte Einstellungen für den neuen Docker-Host angeben. (Ausführliche Beschreibungen der verschiedenen Einstellungen finden Sie unter [Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für IntelliJ][Publish Container with Azure Toolkit].) Klicken Sie auf **Weiter**, nachdem Sie die gewünschten Einstellungen eingegeben haben.

      ![Angeben von Docker-Hostoptionen][PU04]

   c. Sie können wahlweise vorhandene Anmeldeinformationen aus einem Azure-Schlüsseltresor verwenden oder neue Docker-Anmeldeinformationen eingeben. Klicken Sie auf **Fertig stellen**, nachdem Sie Ihre Optionen angegeben haben.

      ![Angeben von Docker-Hostanmeldeinformationen][PU05]

1. Wählen Sie Ihren Docker-Host aus, und klicken Sie dann auf **Weiter**.

   ![Auswählen des Docker-Hosts, der verwendet werden soll][PU06]

1. Geben Sie auf der letzten Seite des Dialogfelds **Deploying Docker Container on Azure** (Docker-Container wird in Azure bereitgestellt) folgende Optionen an:

   a. Sie können entweder einen benutzerdefinierten Namen für den Container angeben, der Ihren Docker-Container hostet, oder die Standardeinstellung übernehmen.

   b. Geben Sie die TCP-Ports für Ihren Docker-Host mit folgender Syntax ein: *[externer Port]*:*[interner Port]*. **80:8080** gibt beispielsweise den externen Port 80 und den internen Spring Boot-Standardport 8080 an.
   
      Wenn Sie den internen Port angepasst haben (beispielsweise durch Bearbeiten der Datei „application.yml“), müssen Sie diese Portnummer angeben, damit das Routing in Azure ordnungsgemäß funktioniert.

   c. Klicken Sie nach dem Konfigurieren dieser Optionen auf **Fertig stellen**.

   ![Bereitstellen eines Docker-Containers in Azure][PU07]

1. Nachdem die Veröffentlichung des Azure-Toolkits abgeschlossen ist, zeigt das Azure-Aktivitätsprotokoll den Status **Veröffentlicht** an.

   ![Docker-Host erfolgreich bereitgestellt][PU08]

## <a name="next-steps"></a>Nächste Schritte

Zusätzliche Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website](https://www.docker.com/).

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: azure-toolkit-for-eclipse-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring-Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
