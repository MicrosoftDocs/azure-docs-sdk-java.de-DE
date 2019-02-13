---
title: Bereitstellen der in einem Linux-Container in der Cloud ausgeführten Web-App „Hallo Welt“ mit dem Azure-Toolkit für Eclipse
description: Führen Sie eine einfache Web-App vom Typ „Hallo Welt“ in einem Linux-Container aus, und stellen Sie sie mithilfe des Azure-Toolkits für Eclipse in der Cloud bereit.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 799f21a282956f9a88aa35743157fc1292197569
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2019
ms.locfileid: "55649246"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-eclipse"></a>Bereitstellen einer Web-App vom Typ „Hallo Welt“ in einem Linux-Container in der Cloud mit dem Azure-Toolkit für Eclipse

[Docker]-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen. Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen. Mit dem Azure-Toolkit für Eclipse wird dieser Prozess für Java-Entwickler vereinfacht, indem Features für die Bereitstellung von Containern in Microsoft Azure hinzugefügt werden.

In diesem Artikel werden die Schritte zum Erstellen einer einfachen „Hallo Welt“-Web-App beschrieben. Außerdem erfahren Sie, wie Sie Ihre Web-App mithilfe des Azure-Toolkits für Eclipse in einem Linux-Container in Azure veröffentlichen.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]
* Einen [Docker]-Client

> [!NOTE]
>
> Sie müssen für die Schritte in diesem Tutorial [Docker] so konfigurieren, dass der Daemon ohne TLS an Port 2375 verfügbar gemacht wird. Sie können diese Einstellung beim Installieren von Docker oder über das Docker-Einstellungsmenü konfigurieren.
>
> ![Docker-Einstellungsmenü][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Erstellen eines neuen Web-App-Projekts

1. Starten Sie Eclipse, und melden Sie sich beim Azure-Konto an, indem Sie die Schritte im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) befolgen.

1. Klicken Sie auf das Menü **Datei** und dann auf **Neu** und **Dynamisches Webprojekt**.
   
   ![Erstellen eines neuen Projekts][file-new-project]

1. Geben Sie im Dialogfeld **Neues dynamisches Webprojekt** Ihren Projektnamen und den Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.
   
   ![Angeben des Projektnamens][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Erstellen einer Azure-Containerregistrierung, die als private Docker-Registrierung verwendet werden soll

Die folgende Anleitung führt Sie durch die Verwendung des Azure-Portals zur Erstellung einer Azure-Containerregistrierung.

> [!NOTE]
>
> Wenn Sie statt des Azure-Portals die Azure CLI verwenden möchten, führen Sie die Schritte unter [Erstellen einer privaten Docker-Containerregistrierung mit der Azure CLI 2.0][Create Docker Registry using Azure CLI] aus.
>

1. Navigieren Sie zum [Azure-Portal], und melden Sie sich an.

   Nachdem Sie sich im Azure-Portal bei Ihrem Konto angemeldet haben, können Sie die Schritte im Artikel [Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal] ausführen, die im Folgenden aus Gründen der Zweckmäßigkeit umschrieben werden.

1. Klicken Sie auf das Menüsymbol für **+ Ressource erstellen** und dann auf **Container** und **Containerregistrierung**.
   
   ![Erstellen einer neuen Azure-Containerregistrierung][create-container-registry-01]

1. Wenn die Seite **Containerregistrierung erstellen** angezeigt wird, geben Sie Ihren **Registrierungsnamen** und die **Ressourcengruppe** ein, wählen Sie bei dem **Administratorbenutzer** die Option **Aktivieren** aus, und klicken Sie anschließend auf **Erstellen**.

   ![Konfigurieren der Einstellungen für die Azure-Containerregistrierung][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Bereitstellen Ihrer Web-App in einem Docker-Container

1. Klicken Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie **Azure** aus, und klicken Sie dann auf **Docker-Unterstützung hinzufügen**.

   Damit wird automatisch eine Docker-Datei mit einer Standardkonfiguration erstellt.

   ![Hinzufügen der Docker-Unterstützung][add-docker-support]

1. Nachdem Sie die Docker-Unterstützung hinzugefügt haben, können Sie im Projekt-Explorer mit der rechten Maustaste auf Ihr Projekt klicken, die Option **Azure** wählen und dann auf **Publish to Web App for Containers** (In Web-App für Container veröffentlichen) klicken.

   ![Veröffentlichen in Web-App für Container][run-on-web-app-for-containers]

1. Geben Sie die erforderlichen Informationen ein, wenn das Dialogfeld **Run on Web App for Containers** (In Web-App für Container ausführen) angezeigt wird:

   * **Docker-Datei**: Hiermit wird der Pfad zu der Docker-Datei angegeben, die erstellt wurde, als Sie Ihrem Projekt die Docker-Unterstützung hinzugefügt haben. 

   * **Containerregistrierung**: Wählen Sie im Dropdownmenü die Containerregistrierung aus, die Sie im vorherigen Abschnitt dieses Artikels erstellt haben. Die Felder für **Server-URL**, **Benutzername** und **Kennwort** werden automatisch ausgefüllt.

   * **Image und Tag**: Gibt den Namen des Containerimages an, wobei in der Regel die folgende Syntax verwendet wird: „*Registrierung*.azurecr.io/*App-Name*:latest“. Hierbei gilt Folgendes: 
      * *Registrierung* ist Ihre Containerregistrierung aus dem vorherigen Abschnitt dieses Artikels. 
      * *App-Name* ist der Name Ihrer Web-App. 

   * **Web-App für Container**: Wählen Sie **Vorhandene verwenden** oder **Neu erstellen**, um anzugeben, ob Sie den Container in einer vorhandenen Web-App bereitstellen oder eine neue Web-App erstellen.  Mit dem von Ihnen angegebenen **App-Namen** wird die URL für Ihre Web-App erstellt, z. B. *wingtiptoys.azurewebsites.net*.

   * **Ressourcengruppe**: Gibt an, ob Sie eine vorhandene Ressourcengruppe verwenden oder eine neue erstellen möchten. 

   * **App Service-Plan**: Gibt an, ob Sie einen vorhandenen App Service-Plan verwenden oder einen neuen erstellen möchten. 

   ![Ausführen von Web-App für Container][run-on-web-app-linux]

1. Wenn Sie das Konfigurieren der oben aufgeführten Einstellungen abgeschlossen haben, können Sie auf **OK** klicken, um Ihre Web-App in Azure zu veröffentlichen.

1. Nach der Veröffentlichung Ihrer Web-App können Sie zu der URL navigieren, die für Ihre Web-App zuvor angegeben wurde, z. B. *wingtiptoys.azurewebsites.net*.

   ![Navigieren zu Ihrer Web-App][browsing-to-web-app]

## <a name="next-steps"></a>Nächste Schritte

Weitere Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website][Docker].

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure-Portal]: https://portal.azure.com/
[Erstellen einer privaten Docker-Containerregistrierung im Azure-Portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-eclipse-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/file-new-project.png
[project-name]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-linux.png
