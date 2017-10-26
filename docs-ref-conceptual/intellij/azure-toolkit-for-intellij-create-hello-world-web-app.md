---
title: Erstellen einer einfachen Azure-Web-App in IntelliJ
description: "In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine „Hello World“-Web-App für Azure erstellen."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 323ce74f2d4dad10460a0c2bc0fb59f2bbdbbf3c
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Erstellen einer einfachen Azure-Web-App in IntelliJ

Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe des [Azure-Toolkits für IntelliJ].

> [!NOTE]
> 
> Das Azure-Toolkit für IntelliJ wurde im August 2017 mit einem anderen Workflow aktualisiert. Aus diesem Grund enthält dieser Artikel zwei verschiedene Abschnitte:
>
> * Im ersten Abschnitt wird das Erstellen einer „Hello World“-Web-App mithilfe der Version des Azure-Toolkits für IntelliJ von August 2017 (oder später) veranschaulicht.
>
> * Im zweiten Abschnitt dieses Artikels wird das Erstellen einer „Hello World“-Web-App mit der Version des Toolkits von April 2017 (oder früher) veranschaulicht.
> 

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-hello-world-web-app-by-using-the-version-307-or-later-toolkit"></a>Erstellen einer „Hello World“-Web-App mit Version 3.0.7 oder höher des Toolkits

### <a name="create-a-new-web-app-project"></a>Erstellen eines neuen Web-App-Projekts

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

1. Erweitern Sie in der Projektexplorer-Ansicht von IntelliJ **src**, dann **main**, dann **webapp**, und doppelklicken Sie dann auf **index.jsp**.
   
   ![Öffnen der Indexseite][open-index-page]

1. Wenn in IntelliJ die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein, damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird. Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Bearbeiten der Indexseite][edit-index-page]

1. Speichern Sie die Datei „index.jsp“.

### <a name="deploy-your-web-app-to-azure"></a>Bereitstellen der Web-App in Azure

1. Klicken Sie in der Projekt-Explorer-Ansicht von IntelliJ mit der rechten Maustaste auf das Projekt, wählen Sie **Azure** aus, und wählen Sie dann **Run on Web App** (In Web-App ausführen) aus.
   
   ![Menü „Run on web app“ (In Web-App ausführen)][run-on-web-app-menu]

1. Im Dialogfeld „Run on Web App“ (In Web-App ausführen) können Sie eine der folgenden Optionen auswählen:

   * Wählen Sie eine vorhandene Web-App aus (sofern vorhanden), und klicken Sie dann auf **Run** (Ausführen).

      ![Dialogfeld „Run on Web App“ (In Web-App ausführen)][run-on-web-app-dialog]

   * Klicken Sie auf **Create New Web App** (Neue Web-App erstellen). Wenn Sie eine neue Web-App erstellen, geben Sie die erforderlichen Informationen für Ihre Web-App an, und klicken Sie dann auf **Run** (Ausführen).

      ![Create new web app (Neue Web-App erstellen)][create-new-web-app-dialog]

1. Im Toolkit wird eine Statusmeldung angezeigt, sobald Ihre Web-App bereitgestellt wurde. Dies schließt auch die URL Ihrer bereitgestellten Web-App ein.

   ![Erfolgreiche Bereitstellung][successfully-deployed]

1. Sie können über den Link in der Statusmeldung zu Ihrer Web-App navigieren.

   ![Navigieren zur Web-App][browse-web-app]

1. Nachdem Sie Ihre Web-App veröffentlicht haben, werden die Einstellungen als Standard gespeichert. Sie können Ihre Anwendung in Azure ausführen, indem Sie auf der Symbolleiste auf den grünen Pfeil klicken. Sie können die Einstellungen ändern, indem Sie auf das Dropdownmenü für Ihre Web-App und dann auf **Konfigurationen bearbeiten** klicken.

   ![Bearbeitungsmenü für die Konfiguration][edit-configuration-menu]

1. Wenn das Dialogfeld für die **Ausführungs-/Debugkonfigurationen** angezeigt wird, können Sie beliebige Standardeinstellungen ändern. Klicken Sie anschließend auf **OK**.

   ![Bearbeitungsdialogfeld für die Konfiguration][edit-configuration-dialog]

<hr />

## <a name="create-a-hello-world-web-app-by-using-the-version-306-or-earlier-toolkit"></a>Erstellen einer „Hello World“-Web-App mit Version 3.0.6 oder niedriger des Toolkits

### <a name="create-a-new-web-app-project"></a>Erstellen eines neuen Web-App-Projekts

1. Starten Sie IntelliJ, klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.
   
   ![Datei Neu Projekt][02]

2. Wählen Sie im Dialogfeld **Neues Projekt** die Option **Java** und dann **Webanwendung** aus, und klicken Sie dann auf **Neu**, um ein Projekt-SDK hinzuzufügen.
   
   ![Dialogfeld "Neues Projekt"][03a]
   
3. Wählen Sie im Dialogfeld für die Auswahl des Stammverzeichnisses für JDK den Ordner aus, in dem Ihr JDK installiert ist, und klicken Sie dann auf **OK**. Klicken Sie im Dialogfeld „Neues Projekt“ auf **Weiter**, um fortzufahren.
   
   ![Festlegen des JDK-Stammverzeichnisses][03b]

4. Für die Zwecke dieses Tutorials benennen Sie das Projekt mit **Java-Web-App-On-Azure**, und klicken Sie dann auf **Fertig stellen**.
   
   ![Dialogfeld "Neues Projekt"][04]

5. Erweitern Sie in der Projektexplorer-Ansicht von IntelliJ **Java-Web-App-On-Azure**, erweitern Sie anschließend **web**, und doppelklicken Sie dann auf **index.jsp**.
   
   ![Öffnen der Indexseite][05c]

6. Wenn in IntelliJ die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein, damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird. Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. Speichern Sie die Datei „index.jsp“.

### <a name="deploy-your-web-app-to-azure"></a>Bereitstellen der Web-App in Azure
Es gibt mehrere Möglichkeiten, eine Java-Web-App in Azure bereitzustellen. In diesem Tutorial wird eine der einfachsten beschrieben: Ihre Anwendung wird in einem Azure-Web-App-Container bereitgestellt – weder ein spezieller Projekttyp noch zusätzliche Tools sind erforderlich. Das JDK und die Webcontainersoftware werden von Azure für Sie bereitgestellt, sodass Sie weder ein eigenes JDK noch eigene Webcontainersoftware hochladen müssen; Sie benötigen lediglich Ihre Java Web-App. Darum dauert der Veröffentlichungsprozess für Ihre Anwendung nur Sekunden, nicht Minuten.

Vor der Veröffentlichung Ihrer Anwendung müssen Sie zuerst die Moduleinstellungen konfigurieren. Führen Sie dazu die folgenden Schritte aus:

1. Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf das Projekt **Java-Web-App-On-Azure** . Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Moduleinstellungen öffnen**.

   ![Öffnen der Moduleinstellungen][05a]

2. Wenn das Dialogfeld „Projektstruktur“ angezeigt wird:

   a. Klicken Sie in der Liste der **Projekteinstellungen** auf **Artefakte**.

   b. Ändern Sie den Artefaktnamen im Feld **Name** so, dass er keine Leerzeichen oder Sonderzeichen enthält; dies ist erforderlich, da der Name im Uniform Resource Identifier (URI) verwendet wird.

   c. Ändern Sie den **Typ** in **Webanwendung: Archiv**.

   d. Klicken Sie auf **OK**, um das Dialogfeld mit der Projektstruktur zu schließen.

   ![Öffnen der Moduleinstellungen][05b]

Nachdem Sie die Moduleinstellungen konfiguriert haben, können Sie Ihre Anwendung mithilfe der folgenden Schritte in Azure veröffentlichen:

1. Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf das Projekt **Java-Web-App-On-Azure** . Wählen Sie im Kontextmenü **Azure** aus, und klicken Sie dann auf **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen).
   
   ![Kontextmenü zur Azure-Veröffentlichung][06]

2. Wenn Sie sich noch nicht über IntelliJ bei Azure angemeldet haben, werden Sie aufgefordert, sich bei Ihrem Azure-Konto anzumelden. (Wenn Sie über mehrere Azure-Konten verfügen, können einige der Eingabeaufforderungen während des Anmeldeprozesses mehrmals angezeigt werden, auch wenn sie scheinbar identisch sind. Befolgen Sie in diesem Fall weiterhin die Anweisungen zur Anmeldung.)
   
   ![Anmeldedialogfeld von Azure][07]

3. Nachdem Sie sich erfolgreich bei Ihrem Azure-Konto angemeldet haben, wird im Dialogfeld **Manage Subscriptions** (Abonnements verwalten) eine Liste der Abonnements angezeigt, die mit Ihren Anmeldeinformationen verknüpft sind. (Wenn mehrere Abonnements aufgeführt sind und Sie nur mit einer bestimmten Teilmenge davon arbeiten möchten, können Sie optional die Abonnements deaktivieren, die Sie nicht verwenden möchten.) Wenn Sie Ihre Abonnements ausgewählt haben, klicken Sie auf **Schließen**.
   
   ![Verwalten von Abonnements][08]

4. Wenn das Dialogfeld **Deploy to Azure Web App Container** (In Azure-Web-App-Container bereitstellen) angezeigt wird, werden alle Web-App-Container angezeigt, die Sie zuvor erstellt haben. Wenn Sie keine Container erstellt haben, ist die Liste leer.
   
   ![App-Container][09]

5. Wenn Sie zuvor keinen Azure-Web-App-Container erstellt haben, oder Sie Ihre Anwendung in einem neuen Container veröffentlichen möchten, führen Sie die folgenden Schritte aus. Wählen Sie andernfalls einen vorhandenen Web-App-Container aus, und fahren Sie mit Schritt 6 fort.
   
   a. Klicken Sie auf das Symbol **+**.
      
      ![App-Container hinzufügen][10]

   b. Das Dialogfeld **New Web App Container** (Neuer Web-App-Container) wird angezeigt, in dem Sie die nächsten Schritte ausführen.
      
      ![Neuer App-Container][11a]
   
   c. Geben Sie eine **DNS-Bezeichnung** für Ihren Web-App-Container ein; dies ist die Blatt-DNS-Bezeichnung der Host-URL für Ihre Webanwendung in Azure. Hinweis: Der Name muss verfügbar sein und den Azure-Web-App-Namenskonventionen entsprechen.

   d. Wählen Sie im Dropdownmenü **Web Container** (Webcontainer) die passende Software für Ihre Anwendung aus.
      
      Aktuell können Sie zwischen Tomcat 8, Tomcat 7 und Jetty 9 wählen. Azure stellt eine aktuelle Distribution der gewählten Software bereit und diese wird auf einer aktuellen Distribution von JDK 8 ausgeführt, die von Oracle erstellt und von Azure bereitgestellt wird.

   e. Wählen Sie im Dropdownmenü **Subscription** (Abonnement) das Abonnement aus, das Sie für diese Bereitstellung verwenden möchten.

   f. Wählen Sie im Dropdownmenü **Resource Group** (Ressourcengruppe) die Ressourcengruppe aus, der Sie Ihre Web-App zuordnen möchten. (Mithilfe von Azure-Ressourcengruppen können Sie verwandte Ressourcen gruppieren, um diese z.B. gemeinsam löschen zu können.)
      
      (Sie können eine vorhandene Ressourcengruppe auswählen (sofern vorhanden) und direkt mit Schritt g unten fortfahren oder die Schritte zum Erstellen einer neuen Ressourcengruppe ausführen:
      
      * Wählen Sie im Dropdownmenü **Ressourcengruppe** die Option **&lt;&lt;Neue Ressourcengruppe erstellen&gt;&gt;**.
      * Das Dialogfeld **New Resource Group** (Neue Ressourcengruppe) wird angezeigt:
        
         ![Neue Ressourcengruppe][12]

      * Geben Sie im Textfeld **Name** einen Namen für die neue Ressourcengruppe ein.
      * Wählen Sie im Dropdownmenü **Region** den entsprechenden Azure-Rechenzentrumsstandort für Ihre Ressourcengruppe aus.
      * Klicken Sie auf **OK**.

   g. Im Dropdownmenü **App Service Plan** (App Service-Plan) werden die App Service-Pläne aufgelistet, die der ausgewählten Ressourcengruppe zugeordnet sind. Ein App Service-Plan enthält verschiedene Informationen wie z.B. den Speicherort Ihrer Web-App, den Tarif und die Größe der Compute-Instanz. Da ein App Service-Plan für mehrere Web-Apps verwendet werden kann, wird er getrennt von einer bestimmten Web-App-Bereitstellung verwaltet.)
      
      Sie können einen vorhandenen App Service-Plan auswählen (sofern vorhanden) und direkt mit Schritt h unten fortfahren oder die folgenden Schritte ausführen, um einen neuen App Service-Plan zu erstellen:
      
      * Wählen Sie in der Dropdownliste **App Service-Plan** die Option **&lt;&lt;Neuen App Service-Plan erstellen&gt;&gt;**.
      * Das Dialogfeld **New App Service Plan** (Neuer App Service-Plan) wird angezeigt:
        
         ![Neuer App Service-Plan][13]

      * Geben Sie im Textfeld **Name** einen Namen für den neuen App Service-Plan ein.
      * Wählen Sie im Dropdownmenü **Location** (Standort) den entsprechenden Azure-Rechenzentrumsstandort für den Plan aus.
      * Wählen Sie im Dropdownmenü **Pricing Tier** (Tarif) die entsprechenden Preise für den Plan aus. Zu Testzwecken können Sie **Free**(Kostenlos) auswählen.
      * Wählen Sie im Dropdownmenü **Instance Size** (Instanzgröße) die entsprechende Instanzgröße für den Plan aus. Zu Testzwecken können Sie **Small**(Klein) wählen.
      * Klicken Sie auf **OK**.

   h. (Optional) Azure stellt standardmäßig automatisch eine aktuelle Distribution von Java 8 in Ihrem Web-App-Container als JVM bereit. Sie können jedoch eine andere JVM-Version und -Distribution auswählen. Führen Sie dazu die folgenden Schritte aus:
      
      * Klicken Sie im Dialogfeld **New Web App Container** (Neuer Web-App-Container) auf die Registerkarte **JDK**.
      * Folgende Optionen stehen zur Auswahl:
        
         * Bereitstellen des Standard-JDKs von Azure
         * Bereitstellen eines Drittanbieter-JDKs aus einer Dropdownliste mit zusätzlichen JDKs, die in Azure verfügbar sind
         * Bereitstellen eines benutzerdefinierten JDKs, das als ZIP-Datei verpackt und entweder öffentlich verfügbar sein oder sich in Ihrem Azure-Speicherkonto befinden muss
        
      ![New App Container (Neuer App-Container) Registerkarte „JDK“][11b]

   i. Wenn Sie alle oben genannten Schritte abgeschlossen haben, sollte das Dialogfeld „New Web App Container“ (Neuer Web-App-Container) folgender Abbildung ähneln:
      
      ![Neuer App-Container][14]
   
   j. Klicken Sie auf **OK** , um die Erstellung Ihres neuen Web-App-Containers abzuschließen.
       
      Warten Sie einige Sekunden, bis die Liste der Web-App-Container aktualisiert wurde. Ihr neu erstellter Web-App-Container sollte nun in der Liste angezeigt werden und markiert sein.

6. Sie sind nun bereit für die erste Bereitstellung der Web-App in Azure. Klicken Sie auf **OK**, um Ihre Java-Anwendung im ausgewählten Web-App-Container bereitzustellen. Standardmäßig wird die Anwendung als Unterverzeichnis des Anwendungsservers bereitgestellt. Wenn sie als Stammanwendung bereitgestellt werden soll, aktivieren Sie das Kontrollkästchen **Deploy to root** (In Stamm bereitstellen), bevor Sie auf **OK** klicken.
   
   ![In Azure bereitstellen][15]

7. Als Nächstes sollte das **Azure-Aktivitätsprotokoll** mit dem Bereitstellungsstatus der Web-App angezeigt werden.
   
   ![Statusanzeige][16]
   
   Die Bereitstellung Ihrer Web-App in Azure sollte nur einige Sekunden dauern. Wenn Ihre Anwendung bereit ist, wird in der Spalte **Status** der Link **Veröffentlicht** angezeigt. Wenn Sie auf den Link klicken, gelangen Sie zur Startseite der bereitgestellten Web-App. Sie können auch anhand der Schritte im folgenden Abschnitt zu Ihrer Web-App navigieren.

### <a name="browsing-to-your-web-app-on-azure"></a>Navigieren zur Web-App in Azure
Um in Azure zu Ihrer Web-App zu navigieren, können Sie die Ansicht **Azure Explorer** verwenden.

Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in IntelliJ auf das Menü **Ansicht**, auf **Toolfenster** und dann auf **Service Explorer** klicken. Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.

Wenn die Ansicht **Azure Explorer** angezeigt wird, führen Sie folgende Schritte aus, um zu Ihrer Web-App zu navigieren: 

1. Erweitern Sie den Knoten **Azure** .
2. Erweitern Sie den Knoten **Web Apps** (Web-Apps). 
3. Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.
4. Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Im Browser öffnen**.
   
   ![Durchsuchen von Web-App][17]

### <a name="updating-your-web-app"></a>Aktualisieren Ihrer Web-App
Das Aktualisieren einer vorhandenen, ausgeführten Azure-Web-App ist ein schneller und einfacher Prozess, und Ihnen stehen zwei Optionen für die Aktualisierung zur Verfügung:

* Sie können die Bereitstellung einer vorhandenen Java-Web-App aktualisieren.
* Sie können eine weitere Java-Anwendung in dem gleichen Web-App-Container veröffentlichen.

In beiden Fällen ist der Prozess identisch und dauert nur wenige Sekunden:

1. Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf die Java-Anwendung, die Sie aktualisieren oder einem vorhandenen Web-App-Container hinzufügen möchten.
2. Wählen Sie im Kontextmenü **Azure** und dann **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen) aus.
3. Da Sie sich bereits zuvor angemeldet haben, sehen Sie eine Liste Ihrer vorhandenen Web-App-Container. Wählen Sie den Container aus, in dem Sie Ihre Java-Anwendung veröffentlichen oder erneut veröffentlichen möchten, und klicken Sie auf **OK**.

Wenige Sekunden später wird Ihre aktualisierte Bereitstellung in der Ansicht **Azure Activity Log** (Azure-Aktivitätsprotokoll) als **Published** (Veröffentlicht) angezeigt, und Sie können die aktualisierte Anwendung in einem Webbrowser überprüfen.

### <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Starten, Beenden oder Neustarten einer vorhandenen Web-App
Um einen vorhandenen Azure-Web-App-Container zu starten oder zu beenden (einschließlich aller darin bereitgestellten Java-Anwendungen), können Sie die Ansicht **Azure Explorer** verwenden.

Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in IntelliJ auf das Menü **Ansicht**, auf **Toolfenster** und dann auf **Service Explorer** klicken. Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.

Wenn die Ansicht **Azure Explorer** angezeigt wird, starten oder beenden Sie Ihre Web-App mit folgenden Schritten: 

1. Erweitern Sie den Knoten **Azure** .
2. Erweitern Sie den Knoten **Web Apps** (Web-Apps). 
3. Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.
4. Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Starten**, **Beenden** oder **Neu starten**. Beachten Sie, dass die Menüoptionen kontextabhängig sind. Sie können nur eine ausgeführte Web-App beenden oder eine Web-App starten, die zurzeit nicht ausgeführt wird.
   
   ![Beenden von Web-App][18]

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].

<!-- URL List -->

[Azure-Toolkits für IntelliJ]: azure-toolkit-for-intellij.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/18-Stop-Web-App.png

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
