---
title: Erstellen einer „Hello World“-Web-App für Azure mit dem Legacytoolkit für IntelliJ
description: In diesem Tutorial erfahren Sie, wie Sie mit Version 3.0.6 (oder einer älteren Version) des Azure-Toolkits für IntelliJ eine „Hello World“-Web-App für Azure erstellen.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: efc1dffa248987772827bbe7bc0caa9f10a0b4ef
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090783"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a>Erstellen einer „Hello World“-Web-App für Azure mit dem Legacytoolkit für IntelliJ

Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe von Version 3.0.6 (oder einer älteren Version) des [Azure-Toolkit für IntelliJ].

> [!NOTE]
>
> Eine Version dieses Artikels, in dem das [Azure-Toolkit für Eclipse] verwendet wird, finden Sie unter [Erstellen einer einfachen Azure-Web-App mit Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> Das Azure-Toolkit für IntelliJ wurde im August 2017 mit einem anderen Workflow aktualisiert. In diesem Artikel wird das Erstellen einer „Hello World“-Web-App mithilfe der Version 3.0.6 (oder einer älteren Version) des Azure-Toolkits für IntelliJ veranschaulicht. Wenn Sie die Version 3.0.7 (oder eine höhere Version) des Toolkits verwenden, müssen Sie die Schritte unter [Erstellen einer einfachen Azure-Web-App in IntelliJ][Updated Version] ausführen.
>

Wenn Sie dieses Tutorial abgeschlossen haben, entspricht Ihre Anwendung bei der Anzeige in einem Webbrowser etwa der folgenden Abbildung:

![Vorschau der Hello World-App][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Erstellen eines neuen Web-App-Projekts

1. Starten Sie IntelliJ, und melden Sie sich beim Azure-Konto gemäß den Anweisungen im Artikel [Anleitung zur Anmeldung für das Azure-Toolkit für IntelliJ][intelliJ-sign-in-instructions] an.

1. Klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.
   
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

## <a name="deploy-your-web-app-to-azure"></a>Bereitstellen der Web-App in Azure

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

## <a name="browsing-to-your-web-app-on-azure"></a>Navigieren zur Web-App in Azure

Um in Azure zu Ihrer Web-App zu navigieren, können Sie die Ansicht **Azure Explorer** verwenden.

Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in IntelliJ auf das Menü **Ansicht**, auf **Toolfenster** und dann auf **Service Explorer** klicken. Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.

Wenn die Ansicht **Azure Explorer** angezeigt wird, führen Sie folgende Schritte aus, um zu Ihrer Web-App zu navigieren: 

1. Erweitern Sie den Knoten **Azure** .
2. Erweitern Sie den Knoten **Web Apps** (Web-Apps). 
3. Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.
4. Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Im Browser öffnen**.
   
   ![Durchsuchen von Web-App][17]

## <a name="updating-your-web-app"></a>Aktualisieren Ihrer Web-App

Das Aktualisieren einer vorhandenen, ausgeführten Azure-Web-App ist ein schneller und einfacher Prozess, und Ihnen stehen zwei Optionen für die Aktualisierung zur Verfügung:

* Sie können die Bereitstellung einer vorhandenen Java-Web-App aktualisieren.
* Sie können eine weitere Java-Anwendung in dem gleichen Web-App-Container veröffentlichen.

In beiden Fällen ist der Prozess identisch und dauert nur wenige Sekunden:

1. Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf die Java-Anwendung, die Sie aktualisieren oder einem vorhandenen Web-App-Container hinzufügen möchten.
2. Wählen Sie im Kontextmenü **Azure** und dann **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen) aus.
3. Da Sie sich bereits zuvor angemeldet haben, sehen Sie eine Liste Ihrer vorhandenen Web-App-Container. Wählen Sie den Container aus, in dem Sie Ihre Java-Anwendung veröffentlichen oder erneut veröffentlichen möchten, und klicken Sie auf **OK**.

Wenige Sekunden später wird Ihre aktualisierte Bereitstellung in der Ansicht **Azure Activity Log** (Azure-Aktivitätsprotokoll) als **Published** (Veröffentlicht) angezeigt, und Sie können die aktualisierte Anwendung in einem Webbrowser überprüfen.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Starten, Beenden oder Neustarten einer vorhandenen Web-App

Um einen vorhandenen Azure-Web-App-Container zu starten oder zu beenden (einschließlich aller darin bereitgestellten Java-Anwendungen), können Sie die Ansicht **Azure Explorer** verwenden.

Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in IntelliJ auf das Menü **Ansicht**, auf **Toolfenster** und dann auf **Service Explorer** klicken. Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.

Wenn die Ansicht **Azure Explorer** angezeigt wird, starten oder beenden Sie Ihre Web-App mit folgenden Schritten: 

1. Erweitern Sie den Knoten **Azure** .
2. Erweitern Sie den Knoten **Web Apps** (Web-Apps). 
3. Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.
4. Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Starten**, **Beenden** oder **Neu starten**. Beachten Sie, dass die Menüoptionen kontextabhängig sind. Sie können nur eine ausgeführte Web-App beenden oder eine Web-App starten, die zurzeit nicht ausgeführt wird.
   
   ![Beenden von Web-App][18]

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
[Updated Version]: azure-toolkit-for-intellij-create-hello-world-web-app.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/18-Stop-Web-App.png
