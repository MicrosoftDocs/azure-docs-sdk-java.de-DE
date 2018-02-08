---
title: "Erstellen einer „Hello World“-Web-App für Azure mit Eclipse"
description: "In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für Eclipse eine „Hello World“-Web-App für Azure erstellen."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: bec94e65951330c933e0173fd580c3578e759c18
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a>Erstellen einer „Hello World“-Web-App für Azure mit Eclipse

Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe des [Azure-Toolkits für Eclipse].

> [!NOTE]
>
> Eine Version dieses Artikels, in dem das [Azure-Toolkit für IntelliJ] verwendet wird, finden Sie unter [Erstellen einer einfachen Azure-Web-App in IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> Das Azure-Toolkit für Eclipse wurde im August 2017 mit einem anderen Workflow aktualisiert. In diesem Artikel wird das Erstellen einer „Hello World“-Web-App mithilfe der Version 3.0.7 (oder höher) des Azure-Toolkits für Eclipse veranschaulicht. Wenn Sie die Version 3.0.6 (oder eine ältere Version) des Toolkits verwenden, müssen Sie die Schritte unter [Create a Hello World web app for Azure using the legacy toolkit for Eclipse][Legacy Version] (Erstellen einer „Hello World“-Web-App für Azure mit dem Legacytoolkit für Eclipse) ausführen.
> 

Wenn Sie dieses Tutorial abgeschlossen haben, entspricht Ihre Anwendung bei der Anzeige in einem Webbrowser etwa der folgenden Abbildung:

![Vorschau der Hello World-App][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Erstellen eines neuen Web-App-Projekts

1. Starten Sie Eclipse, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse][eclipse-sign-in-instructions] an.

1. Klicken Sie auf **Datei**, dann auf **Neu** und schließlich auf **Dynamisches Webprojekt**. (Wenn **Dynamic Web Project** (Dynamisches Webprojekt) nach dem Klicken auf **File** (Datei) und **New** (Neu) nicht als verfügbares Projekt aufgeführt ist, gehen Sie wie folgt vor: Klicken Sie auf **File** (Datei), anschließend auf **New** (Neu) und dann auf **Project...** (Projekt...). Erweitern Sie die Option **Web**, klicken Sie auf **Dynamic Web Project** (Dynamisches Webprojekt) und dann auf **Next** (Weiter).)

   ![Erstellen eines neuen dynamischen Webprojekts][file-new-dynamic-web-project]

2. Nennen Sie das Projekt für die Zwecke dieses Tutorials **MyWebApp**. Ihr Bildschirm sieht dann in etwa wie folgt aus:
   
   ![Eigenschaften des neuen dynamischen Webprojekts][dynamic-web-project-properties]

3. Klicken Sie auf **Fertig stellen**.

4. Erweitern Sie in der Project Explorer-Ansicht von Eclipse die Option **MyWebApp**. Klicken Sie mit der rechten Maustaste auf **WebContent**, und klicken Sie dann auf **Neu** sowie auf **JSP-Datei**.

   ![Erstellen einer neuen JSP-Datei][create-new-jsp-file]

5. Geben Sie im Dialogfeld **New JSP File** (Neue JSP-Datei) den Namen **index.jsp** für die Datei ein. Behalten Sie den übergeordneten Ordner als **MyWebApp/WebContent** bei, und klicken Sie auf **Next** (Weiter).

   ![Dialogfeld „New JSP File“ (Neue JSP-Datei)][new-jsp-file-dialog]

6. Wählen Sie im Dialogfeld **Select JSP Template** (JSP-Vorlage auswählen) im Rahmen dieses Tutorials **New JSP File (html)** (Neue JSP-Datei (HTML)) aus, und klicken Sie dann auf **Finish** (Fertig stellen).

   ![Auswählen einer JSP-Vorlage][select-jsp-template]

7. Wenn in Eclipse die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein, damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird. Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Speichern Sie die Datei „index.jsp“.

## <a name="deploy-your-web-app-to-azure"></a>Bereitstellen der Web-App in Azure

1. Klicken Sie in der Projekt-Explorer-Ansicht von Eclipse mit der rechten Maustaste auf das Projekt, wählen Sie **Azure** aus, und wählen Sie dann **Publish as Azure Web App** (Als Azure-Web-App veröffentlichen) aus.
   
   ![Veröffentlichen als Azure-Web-App][publish-as-azure-web-app]

1. Im Dialogfeld **Web-App bereitstellen** können Sie eine der folgenden Optionen auswählen:

   * Wählen Sie eine vorhandene Web-App aus, sofern vorhanden.

      ![Auswählen eines App-Diensts][select-app-service]

   * Klicken Sie auf **Create New Web App** (Neue Web-App erstellen).

      ![Erstellen eines App Service][create-app-service]

      Geben Sie die erforderlichen Informationen für Ihre Web-App im Dialogfeld **App Service erstellen** an, und klicken Sie dann auf **Erstellen**.

      ![Dialogfeld „App Service erstellen“][create-app-service-dialog]

1. Wählen Sie Ihre Web-App aus, und klicken Sie dann auf **Bereitstellen**.

   ![Bereitstellen eines App-Diensts][deploy-app-service]

1. Im Toolkit wird ein **Azure-Aktivitätsprotokoll** mit dem Status **Veröffentlicht** angezeigt, wenn die Web-App bereitgestellt wurde. Der Status ist als Link für die URL der bereitgestellten Web-App formatiert.

   ![Veröffentlichungsstatus][publish-status]

1. Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.

   ![Navigieren zur Web-App][browse-web-app]

1. Nachdem Sie Ihre Web-App in Azure veröffentlicht haben, können Sie die App verwalten, indem Sie mit der rechten Maustaste darauf klicken und eine der Optionen im Kontextmenü auswählen. Sie können für die Web-App beispielsweise die Option zum **Starten**, **Beenden** oder **Löschen** auswählen.

   ![Verwalten des App-Diensts][manage-app-service]

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].

<!-- URL List -->

[Azure-Toolkits für Eclipse]: azure-toolkit-for-eclipse.md
[Azure-Toolkit für IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
