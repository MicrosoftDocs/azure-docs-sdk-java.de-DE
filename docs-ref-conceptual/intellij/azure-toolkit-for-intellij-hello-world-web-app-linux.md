---
title: "Bereitstellen der in einem Linux-Container in der Cloud ausgeführten Web-App „Hallo Welt“ mit dem Azure-Toolkit für IntelliJ"
description: "Führen Sie eine einfache Web-App vom Typ „Hallo Welt“ in einem Linux-Container aus, und stellen Sie sie mithilfe des Azure-Toolkits für IntelliJ in der Cloud bereit."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: fdf41d6e8b23a6b7d6217ec626480e6c72e13969
ms.sourcegitcommit: 9c354a65b0f8ad49a528f40ddee647b091f7d246
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/04/2018
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a>Bereitstellen einer Web-App vom Typ „Hallo Welt“ in einem Linux-Container in der Cloud mit dem Azure-Toolkit für IntelliJ

[Docker]-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen. Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen. Mit dem Azure-Toolkit für IntelliJ wird dieser Prozess für Java-Entwickler vereinfacht, indem Features für die Bereitstellung als Container in Microsoft Azure hinzugefügt werden.

In diesem Artikel werden die Schritte zum Erstellen einer einfachen „Hello World“-Web-App beschrieben. Außerdem erfahren Sie, wie Sie Ihre Web-App mithilfe des Azure-Toolkits für IntelliJ in einem Linux-Container in Azure veröffentlichen.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* Einen [Docker]-Client

> [!NOTE]
>
> Sie müssen für die Schritte in diesem Tutorial [Docker] so konfigurieren, dass der Daemon ohne TLS an Port 2375 verfügbar gemacht wird. Sie können diese Einstellung beim Installieren von Docker oder über das Docker-Einstellungsmenü konfigurieren.
>
> ![Docker-Einstellungsmenü][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Erstellen eines neuen Web-App-Projekts

1. Starten Sie IntelliJ, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ] an.

1. Klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.
   
   ![Erstellen eines neuen Projekts][file-new-project]

1. Wählen Sie im Dialogfeld **Neues Projekt** die Option **Maven** und abschließend **maven-archetype-webapp** aus, und klicken Sie dann auf **Weiter**.
   
   ![Auswählen der Maven-archetype-Web-App][maven-archetype-webapp]
   
1. Geben Sie die **GroupId** und **ArtifactId** für Ihre Web-App an, und klicken Sie dann auf **Weiter**.
   
   ![Eingeben von GroupId und ArtifactId][groupid-and-artifactid]

1. Passen Sie alle gewünschten Maven-Einstellungen an, oder übernehmen Sie die Standardeinstellungen, und klicken Sie dann auf **Weiter**.
   
   ![Angeben von Maven-Einstellungen][maven-options]

1. Geben Sie den Projektnamen und einen Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.
   
   ![Angeben des Projektnamens][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Erstellen einer Azure-Containerregistrierung, die als private Docker-Registrierung verwendet werden soll

Die folgende Anleitung führt Sie durch die Verwendung des Azure-Portals zur Erstellung einer Azure-Containerregistrierung.

> [!NOTE]
>
> Wenn Sie statt des Azure-Portals die Azure CLI verwenden möchten, führen Sie die Schritte unter [Erstellen einer privaten Docker-Containerregistrierung mit der Azure CLI 2.0][Create Docker Registry using Azure CLI] aus.
>

1. Navigieren Sie zum [Azure-Portal], und melden Sie sich an.

   Nachdem Sie sich im Azure-Portal bei Ihrem Konto angemeldet haben, können Sie die Schritte im Artikel [Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal] ausführen, die im Folgenden aus Gründen der Zweckmäßigkeit umschrieben werden.

1. Klicken Sie auf das Menüsymbol für **+ Neu**, auf **Container** und anschließend auf **Azure-Containerregistrierung**.
   
   ![Erstellen einer neuen Azure-Containerregistrierung][AR01]

1. Wenn die Informationsseite für die Vorlage der Azure-Containerregistrierung angezeigt wird, klicken Sie auf **Erstellen**. 

   ![Erstellen einer neuen Azure-Containerregistrierung][AR02]

1. Wenn die Seite **Containerregistrierung erstellen** angezeigt wird, geben Sie Ihren **Registrierungsnamen** und die **Ressourcengruppe** ein, wählen Sie bei dem **Administratorbenutzer** die Option **Aktivieren** aus, und klicken Sie anschließend auf **Erstellen**.

   ![Konfigurieren der Einstellungen für die Azure-Containerregistrierung][AR03]

1. Navigieren Sie nach der Erstellung der Containerregistrierung im Azure-Portal zu Ihrer Containerregistrierung, und klicken Sie anschließend auf **Zugriffsschlüssel**. Notieren Sie sich den Benutzernamen und das Kennwort für die nächsten Schritte.

   ![Zugriffsschlüssel für die Azure-Containerregistrierung][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Bereitstellen Ihrer Web-App in einem Docker-Container

1. Klicken Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie **Azure** aus, und klicken Sie dann auf **Docker-Unterstützung hinzufügen**.

   Damit wird automatisch eine Docker-Datei mit einer Standardkonfiguration erstellt.

   ![Hinzufügen der Docker-Unterstützung][add-docker-support]

1. Nachdem Sie die Docker-Unterstützung hinzugefügt haben, klicken Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie **Azure** aus, und klicken Sie dann auf **Run on Web App (Linux)** (In Web-App ausführen (Linux)) aus.

   ![In Web-App ausführen (Linux)][run-on-web-app-linux]

1. Wenn das Dialogfeld **Run on Web App (Linux)** (In Web-App ausführen (Linux)) angezeigt wird, geben Sie die erforderlichen Informationen ein:

   * **Name:** gibt den Anzeigenamen im Azure-Toolkit an. 

   * **Server-URL:** gibt die URL für Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels an; dabei wird in der Regel die folgende Syntax verwendet: „*Registrierung*.azurecr.io“. 

   * **Benutzername** und **Kennwort**: geben die Zugriffsschlüssel für Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels an. 

   * **Image und Tag:** gibt den Namen des Containerimages an; dabei wird in der Regel die folgende Syntax verwendet: „*Registrierung*.azurecr.io/*App-Name*:latest“; dabei gilt Folgendes: 
      * *Registrierung* ist Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels. 
      * *App-Name* ist der Name Ihrer Web-App. 

   * **Use Existing Web App** (Vorhandene Web-App verwenden) oder **Create New Web App** (Neue Web-App erstellen): gibt an, ob Sie den Container in einer vorhandenen Web-App bereitstellen oder eine neue Web-App erstellen. 

   * **Ressourcengruppe:** gibt an, ob Sie eine vorhandene Ressourcengruppe verwenden oder eine neue erstellen möchten. 

   * **App Service-Plan:** gibt an, ob Sie einen vorhandenen App Service-Plan verwenden oder einen neuen erstellen möchten. 

1. Wenn Sie mit dem Konfigurieren der oben aufgeführten Einstellungen fertig sind, klicken Sie auf **Ausführen**.

   ![Web-App erstellen][create-web-app]

1. Nachdem Sie Ihre Web-App veröffentlicht haben, werden die Einstellungen als Standard gespeichert. Sie können Ihre Anwendung in Azure ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken. Sie können diese Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

## <a name="next-steps"></a>Nächste Schritte

Weitere Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website][Docker].

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure-Portal]: https://portal.azure.com/
[Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
