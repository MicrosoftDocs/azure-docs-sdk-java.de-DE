---
title: Erstellen einer einfachen Azure-Web-App mit Eclipse
description: "In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für Eclipse eine „Hello World“-Web-App für Azure erstellen."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: dcab31ad99fb79a91374d95c2b8b0d9d10346f5f
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Erstellen einer einfachen Azure-Web-App mit Eclipse
Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe des [Azure-Toolkits für Eclipse]. Zur Vereinfachung wird ein grundlegendes JSP-Beispiel verwendet, aber mit einer ähnlichen Vorgehensweise können Sie auch ein Java-Servlet in Azure bereitstellen.

Wenn Sie dieses Tutorial abgeschlossen haben, entspricht Ihre Anwendung bei der Anzeige in einem Webbrowser etwa der folgenden Abbildung:

![Vorschau der Hello World-App][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-create-a-hello-world-application"></a>So erstellen Sie eine Hello World-Anwendung
Zunächst beginnen wir mit der Erstellung eines Java-Projekts.

1. Starten Sie Eclipse, klicken Sie im Menü auf **File** (Datei), auf **New** (Neu) und anschließend auf **Dynamic Web Project** (Dynamisches Webprojekt). (Wenn **Dynamic Web Project** (Dynamisches Webprojekt) nach dem Klicken auf **File** (Datei) und **New** (Neu) nicht als verfügbares Projekt aufgeführt ist, gehen Sie wie folgt vor: Klicken Sie auf **File** (Datei), anschließend auf **New** (Neu) und dann auf **Project...** (Projekt...). Erweitern Sie die Option **Web**, klicken Sie auf **Dynamic Web Project** (Dynamisches Webprojekt) und dann auf **Next** (Weiter).)

2. Nennen Sie das Projekt für die Zwecke dieses Tutorials **MyWebApp**. Ihr Bildschirm sieht dann in etwa wie folgt aus:
   
   ![Erstellen eines neuen dynamischen Webprojekts][02]

3. Klicken Sie auf **Fertig stellen**.

4. Erweitern Sie in der Project Explorer-Ansicht von Eclipse die Option **MyWebApp**. Klicken Sie mit der rechten Maustaste auf **WebContent**, und klicken Sie dann auf **Neu** sowie auf **JSP-Datei**.

5. Geben Sie im Dialogfeld **New JSP File** (Neue JSP-Datei) den Namen **index.jsp** für die Datei ein. Behalten Sie den übergeordneten Ordner als **MyWebApp/WebContent** bei, und klicken Sie auf **Next** (Weiter).

6. Wählen Sie im Dialogfeld **Select JSP Template** (JSP-Vorlage auswählen) im Rahmen dieses Tutorials **New JSP File (html)** (Neue JSP-Datei (HTML)) aus, und klicken Sie dann auf **Finish** (Fertig stellen).

7. Wenn in Eclipse die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein, damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird. Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Speichern Sie die Datei „index.jsp“.

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>So stellen Sie Ihre Anwendung in einem Azure-Web-App-Container bereit
Es gibt mehrere Möglichkeiten, eine Java-Webanwendung in Azure bereitzustellen. In diesem Tutorial wird eine der einfachsten beschrieben: Ihre Anwendung wird in einem Azure-Web-App-Container bereitgestellt – weder ein spezieller Projekttyp noch zusätzliche Tools sind erforderlich. Das JDK und die Webcontainersoftware werden von Azure für Sie bereitgestellt, sodass Sie weder ein eigenes JDK noch eigene Webcontainersoftware hochladen müssen; Sie benötigen lediglich Ihre Java Web-App. Darum dauert der Veröffentlichungsprozess für Ihre Anwendung nur Sekunden, nicht Minuten.

1. Klicken Sie in Eclipse Project Explorer mit der rechten Maustaste auf **MyWebApp**.

2. Wählen Sie im Kontextmenü **Azure** aus, und klicken Sie dann auf **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen...).
   
   ![Veröffentlichen als Azure-Web-App][03]
   
   Alternativ können Sie auch das Webanwendungsprojekt im Projekt-Explorer auswählen und auf der Symbolleiste auf die Dropdownschaltfläche **Publish** (Veröffentlichen) klicken. Wählen Sie anschließend **Publish as Azure Web App** (Als Azure-Web-App veröffentlichen) aus:
   
   ![Veröffentlichen als Azure-Web-App][14]

3. Wenn Sie sich noch nicht von Eclipse aus bei Azure angemeldet haben, werden Sie aufgefordert, sich bei Ihrem Azure-Konto anzumelden:
   
   ![Azure-Anmeldedialogfeld][04]
   
   Wenn Sie über mehrere Azure-Konten verfügen, können einige der Eingabeaufforderungen während des Anmeldeprozesses mehrmals angezeigt werden, auch wenn sie scheinbar identisch sind. Befolgen Sie in diesem Fall weiterhin die Anweisungen zur Anmeldung.

4. Nachdem Sie sich erfolgreich bei Ihrem Azure-Konto angemeldet haben, wird im Dialogfeld **Manage Subscriptions** (Abonnements verwalten) eine Liste der Abonnements angezeigt, die mit Ihren Anmeldeinformationen verknüpft sind. Wenn mehrere Abonnements aufgeführt sind und Sie nur mit einer bestimmten Teilmenge davon arbeiten möchten, können Sie optional die Abonnements deaktivieren, die Sie nicht verwenden möchten. Wenn Sie Ihre Abonnements ausgewählt haben, klicken Sie auf **Schließen**.
   
   ![Dialogfeld zum Verwalten von Abonnements][05]

5. Wenn das Dialogfeld **Deploy to Azure Web App Container** (In Azure-Web-App-Container bereitstellen) angezeigt wird, werden alle Web-App-Container angezeigt, die Sie zuvor erstellt haben. Wenn Sie keine Container erstellt haben, ist die Liste leer.
   
   ![Dialogfeld zum Bereitstellen im Azure-Web-App-Container][06]

6. Wenn Sie zuvor keinen Azure-Web-App-Container erstellt haben, oder Sie Ihre Anwendung in einem neuen Container veröffentlichen möchten, führen Sie die folgenden Schritte aus. Wählen Sie andernfalls einen vorhandenen Web-App-Container, und fahren Sie mit Schritt 7 fort.
   
   a. Klicken Sie auf **New...**
      
      ![Dialogfeld zum Bereitstellen im Azure-Web-App-Container][15]

   b. Das Dialogfeld **New Web App Container** (Neuer Web-App-Container) wird angezeigt:
      
      ![Dialogfeld für neuen Web-App-Container][07a]

   c. Geben Sie eine **DNS-Bezeichnung** für Ihren Web-App-Container ein; dies ist die Blatt-DNS-Bezeichnung der Host-URL für Ihre Webanwendung in Azure. (Hinweis: Der Name muss verfügbar sein und den Azure-Web-App-Namenskonventionen entsprechen.)

   d. Wählen Sie im Dropdownmenü **Web Container** (Webcontainer) die passende Software für Ihre Anwendung aus.
      
      Aktuell können Sie zwischen Tomcat 8, Tomcat 7 und Jetty 9 wählen. Azure stellt eine aktuelle Distribution der gewählten Software bereit und diese wird auf einer aktuellen Distribution von JDK 8 ausgeführt, die von Oracle erstellt und von Azure bereitgestellt wird.

   e. Wählen Sie im Dropdownmenü **Subscription** (Abonnement) das Abonnement aus, das Sie für diese Bereitstellung verwenden möchten.

   f. Wählen Sie im Dropdownmenü **Resource Group** (Ressourcengruppe) die Ressourcengruppe aus, der Sie Ihre Web-App zuordnen möchten. (Mithilfe von Azure-Ressourcengruppen können Sie verwandte Ressourcen gruppieren, um diese z.B. gemeinsam löschen zu können.)
      
      Sie können eine vorhandene Ressourcengruppe auswählen (sofern vorhanden) und direkt mit Schritt g unten fortfahren oder die folgenden Schritte ausführen, um eine neue Ressourcengruppe zu erstellen:
      
      * Klicken Sie auf **New...**
      * Das Dialogfeld **New Resource Group** (Neue Ressourcengruppe) wird angezeigt:
        
          ![Dialogfeld für neue Ressourcengruppe][08]
      * Geben Sie im Textfeld **Name** einen Namen für die neue Ressourcengruppe ein.
      * Wählen Sie im Dropdownmenü **Region** den entsprechenden Azure-Rechenzentrumsstandort für Ihre Ressourcengruppe aus.
      * OPTIONAL: Standardmäßig stellt Azure automatisch eine aktuelle Distribution von Java 8 in Ihrem Web-App-Container als JVM bereit. Sie können jedoch eine andere JVM-Version und -Distribution angeben, wenn Ihre Web-App dies erfordert. Um das JDK für Ihre Web-App anzugeben, klicken Sie auf die Registerkarte **JDK** , und wählen Sie eine der folgenden Optionen aus:
         * **Deploy the default JDK offered by Azure Web Apps service**(Das vom Azure-Web-Apps-Dienst angebotene Standard-JDK bereitstellen): Diese Option stellt eine aktuelle Distribution von Java 8 bereit.
         * **Deploy a 3rd party JDK available on Azure**(Ein in Azure verfügbares JDK eines Drittanbieters bereitstellen): Mit dieser Option können Sie aus einer Liste der von Microsoft Azure angebotenen JDKs auswählen.
         * **Deploy my own JDK from this download location**(Eigenes JDK von diesem Downloadspeicherort bereitstellen): Mit dieser Option können Sie Ihre eigene JDK-Distribution angeben, die als ZIP-Datei gepackt und entweder in einen öffentlich verfügbaren Speicherort oder in ein Azure-Speicherkonto hochgeladen sein muss, auf das Sie Zugriff haben.
          
         ![Dialogfeld für neuen Web-App-Container][07b]

   g. Klicken Sie auf **OK**.

   h. Im Dropdownmenü **App Service Plan** (App Service-Plan) werden die App Service-Pläne aufgelistet, die der ausgewählten Ressourcengruppe zugeordnet sind. (App Service-Pläne enthalten verschiedene Informationen wie z.B. den Speicherort Ihrer Web-App, den Tarif und die Größe der Compute-Instanz. Da ein App Service-Plan für mehrere Web-Apps verwendet werden kann, wird er getrennt von einer bestimmten Web-App-Bereitstellung verwaltet.)
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * Klicken Sie auf **New...**
      * Das Dialogfeld **New App Service Plan** (Neuer App Service-Plan) wird angezeigt:
        
          ![Dialogfeld für neuen App Service-Plan][09]
      * Geben Sie im Textfeld **Name** einen Namen für den neuen App Service-Plan ein.
      * Wählen Sie im Dropdownmenü **Location** (Standort) den entsprechenden Azure-Rechenzentrumsstandort für den Plan aus.
      * Wählen Sie im Dropdownmenü **Pricing Tier** (Tarif) die entsprechenden Preise für den Plan aus. Zu Testzwecken können Sie **Free**(Kostenlos) auswählen.
      * Wählen Sie im Dropdownmenü **Instance Size** (Instanzgröße) die entsprechende Instanzgröße für den Plan aus. Zu Testzwecken können Sie **Small**(Klein) wählen.

   i. Wenn Sie alle oben genannten Schritte abgeschlossen haben, sollte das Dialogfeld „New Web App Container“ (Neuer Web-App-Container) folgender Abbildung ähneln:
      
      ![Dialogfeld für neuen Web-App-Container][10]

   j. Klicken Sie auf **OK** , um die Erstellung Ihres neuen Web-App-Containers abzuschließen.
       
      Warten Sie einige Sekunden, bis die Liste der Web-App-Container aktualisiert wurde. Ihr neu erstellter Web-App-Container sollte nun in der Liste angezeigt werden und markiert sein.

7. Sie können jetzt die erste Bereitstellung Ihrer Web-App in Azure abschließen:
   
   ![Dialogfeld zum Bereitstellen im Azure-Web-App-Container][11]
   
   Klicken Sie auf **OK** , um Ihre Java-Anwendung im ausgewählten Web-App-Container bereitzustellen.
   
   Standardmäßig wird die Anwendung als Unterverzeichnis des Anwendungsservers bereitgestellt. Wenn sie als Stammanwendung bereitgestellt werden soll, aktivieren Sie das Kontrollkästchen **Deploy to root** (In Stamm bereitstellen), bevor Sie auf **OK** klicken.

8. Als Nächstes sollte das **Azure-Aktivitätsprotokoll** mit dem Bereitstellungsstatus der Web-App angezeigt werden.
   
   ![Azure-Aktivitätsprotokoll][12]
   
   Die Bereitstellung Ihrer Web-App in Azure sollte nur einige Sekunden dauern. Wenn Ihre Anwendung bereit ist, wird in der Spalte **Veröffentlicht** in the **Veröffentlicht** angezeigt. Wenn Sie auf den Link klicken, gelangen Sie zur Startseite Ihrer bereitgestellten Web-App.

## <a name="updating-your-web-app"></a>Aktualisieren Ihrer Web-App
Das Aktualisieren einer vorhandenen, ausgeführten Azure-Web-App ist ein schneller und einfacher Prozess, und Ihnen stehen zwei Optionen für die Aktualisierung zur Verfügung:

* Sie können die Bereitstellung einer vorhandenen Java-Web-App aktualisieren.
* Sie können eine weitere Java-Anwendung in dem gleichen Web-App-Container veröffentlichen.

In beiden Fällen ist der Prozess identisch und dauert nur wenige Sekunden:

1. Klicken Sie im Projektexplorer von Eclipse mit der rechten Maustaste auf die Java-Anwendung, die Sie aktualisieren oder einem vorhandenen Web-App-Container hinzufügen möchten.

2. Wählen Sie im Kontextmenü **Azure** und dann **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen) aus.

3. Da Sie sich bereits zuvor angemeldet haben, sehen Sie eine Liste Ihrer vorhandenen Web-App-Container. Wählen Sie den Container aus, in dem Sie Ihre Java-Anwendung veröffentlichen oder erneut veröffentlichen möchten, und klicken Sie auf **OK**.

Wenige Sekunden später wird Ihre aktualisierte Bereitstellung in der Ansicht **Azure Activity Log** (Azure-Aktivitätsprotokoll) als **Published** (Veröffentlicht) angezeigt, und Sie können die aktualisierte Anwendung in einem Webbrowser überprüfen.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Starten, Beenden oder Neustarten einer vorhandenen Web-App
Um einen vorhandenen Azure-Web-App-Container zu starten oder zu beenden (einschließlich aller darin bereitgestellten Java-Anwendungen), können Sie die Ansicht **Azure Explorer** verwenden.

Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in Eclipse auf das Menü **Window** (Fenster) und dann auf **Show View** (Ansicht anzeigen), **Other...** (Andere...), **Azure** und **Azure Explorer** klicken. Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.

Wenn die Ansicht **Azure Explorer** angezeigt wird, starten oder beenden Sie Ihre Web-App mit folgenden Schritten: 

1. Erweitern Sie den Knoten **Azure** .

2. Erweitern Sie den Knoten **Web Apps** (Web-Apps). 

3. Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.

4. Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Starten**, **Beenden** oder **Neu starten**. Beachten Sie, dass die Menüoptionen kontextabhängig sind. Sie können nur eine ausgeführte Web-App beenden oder eine Web-App starten, die zurzeit nicht ausgeführt wird.
   
   ![Beenden einer vorhandenen Web-App][13]

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].

<!-- URL List -->

[Azure-Toolkits für Eclipse]: azure-toolkit-for-eclipse.md
[Web-Apps – Übersicht]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
