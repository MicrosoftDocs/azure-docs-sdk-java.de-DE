---
title: Erstellen einer „Hello World“-Web-App für Azure mit IntelliJ
description: In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine „Hello World“-Web-App für Azure erstellen.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 7055751d1b1c37e019ef4ed59f1710ce6905e9f8
ms.sourcegitcommit: a108a82414bd35be896e3c4e7047f5eb7b1518cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2019
ms.locfileid: "58489638"
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a>Erstellen einer „Hello World“-Web-App für Azure mit IntelliJ

Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe des [Azure-Toolkit für IntelliJ].

> [!NOTE]
>
> Eine Version dieses Artikels, in dem das [Azure-Toolkit für Eclipse] verwendet wird, finden Sie unter [Erstellen einer einfachen Azure-Web-App mit Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> Das Azure-Toolkit für IntelliJ wurde im August 2017 mit einem anderen Workflow aktualisiert. In diesem Artikel wird das Erstellen einer „Hello World“-Web-App mithilfe der Version 3.0.7 (oder höher) des Azure-Toolkits für IntelliJ veranschaulicht. Wenn Sie die Version 3.0.6 (oder eine ältere Version) des Toolkits verwenden, müssen Sie die Schritte unter [Create a Hello World web app for Azure using the legacy toolkit for IntelliJ][Legacy Version] (Erstellen einer „Hello World“-Web-App für Azure mit dem Legacytoolkit für IntelliJ) ausführen.
> 

Wenn Sie dieses Tutorial abgeschlossen haben, entspricht Ihre Anwendung bei der Anzeige in einem Webbrowser etwa der folgenden Abbildung:

![Vorschau der Hello World-App][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Erstellen eines neuen Web-App-Projekts

1. Starten Sie IntelliJ, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ][intelliJ-sign-in-instructions] an.

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

1. Erweitern Sie in der Projektexplorer-Ansicht von IntelliJ **src**, dann **main**, dann **webapp**, und doppelklicken Sie dann auf **index.jsp**.
   
   ![Öffnen der Indexseite][open-index-page]

1. Wenn in IntelliJ die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein, damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird. Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Bearbeiten der Indexseite][edit-index-page]

1. Speichern Sie die Datei „index.jsp“.

## <a name="deploy-your-web-app-to-azure"></a>Bereitstellen der Web-App in Azure

1. Klicken Sie in der Projekt-Explorer-Ansicht von IntelliJ mit der rechten Maustaste auf das Projekt, wählen Sie **Azure** aus, und wählen Sie dann **Run on Web App** (In Web-App ausführen) aus.
   
   ![Menü „Run on web app“ (In Web-App ausführen)][run-on-web-app-menu]

1. Im Dialogfeld „Run on Web App“ (In Web-App ausführen) können Sie eine der folgenden Optionen auswählen:

   * Wählen Sie eine vorhandene Web-App aus (sofern vorhanden), und klicken Sie dann auf **Run** (Ausführen).

      ![Dialogfeld „Run on Web App“ (In Web-App ausführen)][run-on-web-app-dialog]

   * Klicken Sie im WebApp-Dropdownmenü auf **Neue Web-App erstellen**. Wenn Sie eine neue Web-App erstellen, geben Sie die erforderlichen Informationen für Ihre Web-App an, und klicken Sie nach ihrer Erstellung auf **Run** (Ausführen).

      ![Create new web app (Neue Web-App erstellen)][create-new-web-app-dialog]

1. Im Toolkit wird eine Statusmeldung angezeigt, sobald Ihre Web-App bereitgestellt wurde. Dies schließt auch die URL Ihrer bereitgestellten Web-App ein.

   ![Erfolgreiche Bereitstellung][successfully-deployed]

1. Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.

   ![Navigieren zur Web-App][browse-web-app]

1. Nachdem Sie Ihre Web-App veröffentlicht haben, werden die Einstellungen als Standard gespeichert. Sie können Ihre Anwendung in Azure ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken. Sie können die Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].

<!-- URL List -->

[Azure-Toolkit für IntelliJ]: azure-toolkit-for-intellij.md
[Azure-Toolkit für Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
