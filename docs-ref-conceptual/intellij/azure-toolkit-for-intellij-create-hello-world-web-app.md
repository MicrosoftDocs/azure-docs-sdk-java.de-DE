---
title: Erstellen einer „Hello World“-Web-App für Azure App Service mit IntelliJ
description: In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine „Hello World“-Web-App für Azure erstellen.
services: app-service
keywords: Java, IntelliJ, Web-App, Azure App Service, Hallo Welt, Hello World, Schnellstart
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
ms.openlocfilehash: ae0749ce1ddab971f1a83e2e5e58492fd8ccb287
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626118"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a>Erstellen einer „Hello World“-Web-App für Azure App Service mit IntelliJ

Mithilfe des Open-Source-Plug-Ins [Azure-Toolkit für IntelliJ](https://plugins.jetbrains.com/plugin/8053) können Sie innerhalb weniger Minuten eine einfache „Hello World“-Anwendung erstellen und als Web-App in Azure App Service bereitstellen.

> [!NOTE]
>
> Ein ähnliches Tutorial für Eclipse finden Sie [hier][eclipse-hello-world].
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> Denken Sie daran, die Ressourcen nach Abschluss dieses Tutorials zu bereinigen. In diesem Fall wird Ihr kostenloses Kontokontingent im Rahmen dieses Leitfadens nicht überschritten.
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a>Installation und Anmeldung

1. Wählen Sie im Dialogfeld mit den Einstellungen/Voreinstellungen von IntelliJ IDEA (STRG+ALT+S) die Option **Plugins** (Plug-Ins) aus. Suchen Sie anschließend unter **Marketplace** nach **Azure Toolkit for IntelliJ** (Azure-Toolkit für IntelliJ), und klicken Sie auf **Install** (Installieren). Klicken Sie nach Abschluss der Installation auf **Restart** (Neu starten), um das Plug-In zu aktivieren. 

   ![Plug-In „Azure-Toolkit für IntelliJ“ im Marketplace][marketplace]

2. Melden Sie sich bei Ihrem Azure-Konto an. Öffnen Sie hierzu über die Seitenleiste den **** Azure-Explorer, und klicken Sie anschließend auf der Leiste am oberen Rand auf das Symbol **** für die Azure-Anmeldung, oder navigieren Sie im IDEA-Menü zu **Tools > Azure >Azure Sign in** (Extras > Azure > Azure-Anmeldung).

   ![IntelliJ-Befehl für Azure-Anmeldung][I01]

3. Wählen Sie im Fenster für die Azure-Anmeldung **** die Option **Device Login** (Geräteanmeldung) aus, und klicken Sie anschließend auf **Sign in** (Anmelden). Weitere Anmeldeoptionen finden Sie [hier](azure-toolkit-for-intellij-sign-in-instructions.md).

   ![Fenster für die Azure-Anmeldung mit ausgewählter Geräteanmeldung][I02]

4. Klicken Sie im Dialogfeld **Azure Device Login** (Azure-Geräteanmeldung) auf **Copy&Open** (Kopieren und öffnen).

   ![Dialogfeld für Azure-Anmeldung][I03]

5. Fügen Sie im Browser Ihren Gerätecode ein, den Sie im vorherigen Schritt durch Klicken auf **Copy&Open** (Kopieren und öffnen) kopiert haben, und klicken Sie anschließend auf **Next** (Weiter).

   ![Der Browser für die Geräteanmeldung][I04]

6. Wenn das Dialogfeld **Select Subscriptions** (Abonnements auswählen) angezeigt wird, wählen Sie die Abonnements aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

   ![Dialogfeld zum Auswählen von Abonnements][I05]

## <a name="creating-web-app-project"></a>Erstellen des Web-App-Projekts

1. Klicken Sie in IntelliJ im Menü **File** (Datei) auf **New** (Neu) und anschließend auf **Project** (Projekt).

   ![Erstellen eines neuen Projekts][file-new-project]

2. Wählen Sie im Dialogfeld **Neues Projekt** die Option **Maven** und abschließend **maven-archetype-webapp** aus, und klicken Sie dann auf **Weiter**.

   ![Auswählen von „maven-archetype-webapp“][maven-archetype-webapp]

3. Geben Sie die **GroupId** und **ArtifactId** für Ihre Web-App an, und klicken Sie dann auf **Weiter**.

   ![Eingeben von GroupId und ArtifactId][groupid-and-artifactid]

4. Passen Sie alle gewünschten Maven-Einstellungen an, oder übernehmen Sie die Standardeinstellungen, und klicken Sie dann auf **Weiter**.

   ![Angeben von Maven-Einstellungen][maven-options]

5. Geben Sie den Projektnamen und einen Speicherort an, und klicken Sie anschließend auf **Fertig stellen**.

   ![Angeben des Projektnamens][project-name]

6. Öffnen Sie die Datei **src/main/webapp/index.jsp** im Projektexplorer, bearbeiten Sie sie wie folgt, und **speichern Sie die Änderungen**:

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Bearbeiten der Indexseite][edit-index-page]

## <a name="deploying-web-app-to-azure"></a>Bereitstellen der Web-App in Azure

1. Klicken Sie im Projektexplorer mit der rechten Maustaste auf Ihr Projekt, erweitern Sie **Azure**, und klicken Sie anschließend auf **Deploy to Azure** (In Azure bereitstellen).

   ![Menüoption zum Bereitstellen in Azure][deploy-to-azure-menu]

1. Im Dialogfeld für die Bereitstellung in Azure können Sie die Anwendung direkt für eine vorhandene Tomcat-Web-App bereitstellen, sofern Sie bereits über eine solche Web-App verfügen. Andernfalls müssen Sie zunächst eine neue Web-App erstellen.
   1. Klicken Sie auf den Link **No available webapp, click to create a new one** (Keine Web-App verfügbar. Klicken Sie hier, um eine neue zu erstellen.), um eine neue Web-App zu erstellen. Falls in Ihrem Abonnement bereits Web-Apps vorhanden sind, können Sie in der Web-App-Dropdownliste die Option **Create New WebApp** (Neue Web-App erstellen) auswählen.

      ![Dialogfeld zum Bereitstellen in Azure][deploy-to-azure-dialog]

   1. Wählen Sie im Popupdialogfeld die Option **TOMCAT 8.5-jre8** als Webcontainer aus, und geben Sie die übrigen erforderlichen Informationen an. Klicken Sie abschließend auf **OK**, um die Web-App zu erstellen.

      ![Create new web app (Neue Web-App erstellen)][create-new-web-app-dialog]

   1. Wählen Sie in der Web-App-Dropdownliste die Web-App aus, und klicken Sie anschließend auf **Run** (Ausführen). (Wenn Sie die Bereitstellung für eine bereits vorhandene Web-App ausführen möchten, können Sie an dieser Stelle beginnen.)

      ![Bereitstellen für eine vorhandene Web-App][deploy-to-existing-webapp]

1. Nachdem Ihre Web-App bereitgestellt wurde, wird im Toolkit eine Statusmeldung angezeigt. Diese enthält auch die URL Ihrer bereitgestellten Web-App, sofern die Bereitstellung erfolgreich war.

   ![Erfolgreiche Bereitstellung][successfully-deployed]

1. Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.

   ![Navigieren zur Web-App][browse-web-app]

## <a name="managing-deploy-configurations"></a>Verwalten von Bereitstellungskonfigurationen

1. Nachdem Sie Ihre Web-App veröffentlicht haben, werden Ihre Einstellungen als Standard gespeichert, und Sie können die Bereitstellung ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken. Sie können die Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a>Bereinigen der Ressourcen

1. Löschen von Web-Apps im Azure-Explorer

     ![Ressourcenbereinigung][clean-resources]

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->
[marketplace]:./media/azure-toolkit-for-intellij-create-hello-world-web-app/marketplace.png
[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[deploy-to-azure-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[deploy-to-azure-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[deploy-to-existing-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/deploy-to-existing-webapp.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
[clean-resources]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/clean-resource.png
[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-intellij-sign-in-instructions/I05.png
