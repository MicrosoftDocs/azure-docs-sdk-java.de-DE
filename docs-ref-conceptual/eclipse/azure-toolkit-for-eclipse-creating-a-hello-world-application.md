---
title: "Erstellen eines Hello World Cloud-Diensts für Azure in Eclipse"
description: "Informationen Sie zum Erstellen einer einfachen Hello World-Anwendung mit dem Azure-Toolkit für Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 9b31f0faeb6ee7b5e7b8fe3a1f2827133d6188e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Erstellen eines Hello World Cloud-Diensts für Azure in Eclipse
Die folgenden Schritte veranschaulichen, wie zum Erstellen und Bereitstellen einer einfachen JSP-Anwendung in Azure mit dem Azure-Toolkit für Eclipse. Ein JSP-Beispiel wird aus Gründen der Einfachheit angezeigt, aber sehr ähnliche Schritte erforderlich wäre ein Java-Servlet angebracht, soweit Azure-Bereitstellung ist.

Die Anwendung sieht etwa wie folgt aus:

![][ic600360]

## <a name="prerequisites"></a>Voraussetzungen
* Ein Java Developer Kit (JDK), Version 1.7 oder höher.
* Eclipse IDE für Java EE-Entwickler, Indigo oder höher. Dies kann von heruntergeladen werden <http://www.eclipse.org/downloads/>.
* Eine Distribution eines Java-basierten Webservers oder Anwendungsservers wie Apache Tomcat, GlassFish, JBoss-Anwendungsserver, Jetty oder IBM® WebSphere® Application Server Liberty Core.
* Ein Azure-Abonnement, das erworben werden kann <http://azure.microsoft.com/pricing/purchase-options/>.
* Das Azure-Toolkit für Eclipse. Weitere Informationen finden Sie unter [Azure-Toolkit für Eclipse installieren][Installing the Azure Toolkit for Eclipse].

## <a name="to-create-a-hello-world-application"></a>Erstellen eine Hello World-Anwendung
Zunächst beginnen wir mit dem Erstellen einer Java-Projekt.

1. Starten Sie Eclipse, und klicken Sie auf das Menü auf **Datei**, klicken Sie auf **neu**, und klicken Sie dann auf **Dynamic Web Project**. (Wenn Sie nicht sehen **Dynamic Web Project** als verfügbares Projekt aufgeführt, nach dem Klicken auf **Datei**, **neu**, gehen Sie folgendermaßen vor: Klicken Sie auf **Datei**, klicken Sie auf **neu**, klicken Sie auf **Projekt...** , erweitern Sie **Web**, klicken Sie auf **Dynamic Web Project**, und klicken Sie auf **Weiter**.)

1. Für die Zwecke dieses Lernprogramms, nennen Sie das Projekt **"myhelloworld"**. (Stellen Sie sicher verwenden Sie diesen Namen, die nachfolgenden Schritte in diesem Lernprogramm erwarten, dass Ihre WAR-Datei "myhelloworld" heißen). Ihr Bildschirm wird ähnlich der folgenden aussehen:

   ![][ic589576]

1. Klicken Sie auf **Fertig stellen**.

1. Erweitern Sie in Eclipse-Projekt-Explorer-Ansicht **"myhelloworld"**. Mit der rechten Maustaste **WebContent**, klicken Sie auf **neu**, und klicken Sie dann auf **JSP-Datei**.

1. In der **neue JSP-Datei** Dialogfeld, benennen Sie die Datei **"Index.jsp"**. Behalten Sie den übergeordneten Ordner als **MyHelloWorld/WebContent**, wie im folgenden gezeigt:

   ![][ic659262]

1. In der **Select JSP Template** Dialogfeld für die Zwecke dieses Lernprogrammen wählen **neue JSP-Datei (html)** , und klicken Sie auf **Fertig stellen**.

1. Wenn die Datei "Index.jsp" in Eclipse geöffnet wird, dynamisch für anzuzeigenden Text hinzufügen **Hello World!** innerhalb des vorhandenen `<body>` Element. Der aktualisierte `<body>` Inhalt sollte wie folgt aussehen:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Speichern Sie die Datei "Index.jsp".

## <a name="to-deploy-your-application-to-azure-the-quick-and-simple-way"></a>Ihre Anwendung in Azure schnell und auf einfache Weise bereitstellen
Sobald Sie über eine Java-Webanwendung testbereit verfügen, können Sie die folgende verkürzte verwenden, direkt auf der Azure-Cloud auszuprobieren.

1. Klicken Sie im Projektexplorer von Eclipse auf **"myhelloworld"**.

2. Klicken Sie in der Eclipse-Symbolleiste auf die **veröffentlichen** Dropdown-Schaltfläche, und klicken Sie dann auf **veröffentlichen als Azure Cloud-Dienst**

   ![][publishDropdownButton]

3. Wenn Sie diese Anwendung in Azure zum ersten Mal veröffentlichen, und ein Azure-Bereitstellungsprojekt für diese Anwendung nicht erstellt haben, eine Azure-Bereitstellungsprojekt für Sie automatisch erstellt. Daraufhin sollte die folgende Meldung angezeigt, die auch das JDK-Paket werden aufgelistet und Anwendungsserver, die zum Ausführen der Anwendungsstatus automatisch bereitgestellt werden.

   ![][ic789598]
   
   Dieser verkürzte Ansatz ermöglicht eine schnelle und einfache Möglichkeit zum Testen Ihrer Anwendung in Azure ohne so konfigurieren Sie einen bestimmten Server oder JDK, die von den Standardwerten abweicht. Wenn Sie mit den Standardwerten zufrieden sind, können Sie klicken **OK** mit den folgenden Schritten fort.
   Jedoch wenn Sie das JDK ändern möchten oder Anwendungsservers zur für Ihre Anwendung verwenden Sie können dies später durch Bearbeiten der Azure-Bereitstellungsprojekt, die automatisch für Sie erstellt wurde, oder klicken Sie auf **"Abbrechen"** sofort aus, und lesen die **Informationen zu Azure-Bereitstellungsprojekte Abschnitt** dieses Lernprogramm.

4. In der **Publish to Azure** Dialogfeld:

   1. Wenn es keine Abonnements, wählen Sie in der **Abonnement** Liste noch, befolgen Sie diese Schritte aus, um Ihre Abonnementinformationen zu importieren:
      1. Klicken Sie auf **Import from PUBLISH-SETTINGS File**.
      2. In der **Import Subscription Information** Dialogfeld klicken Sie auf **Download PUBLISH-SETTINGS File**. Wenn Sie noch nicht in Ihrem Azure-Konto angemeldet sind, werden Sie aufgefordert, um sich anzumelden. Klicken Sie dann werden Sie aufgefordert, speichern Sie eine Azure Einstellungsdatei veröffentlichen. Speichern Sie es auf Ihrem lokalen Computer.
      3. Immer noch in der **Import Subscription Information** Dialogfeld klicken Sie auf die **Durchsuchen** Schaltfläche, wählen Sie die im vorherigen Schritt lokal gespeicherte Datei mit den veröffentlichungseinstellungen, und klicken Sie dann auf **öffnen**. Ihr Bildschirm sollte etwa wie folgt aussehen:![][ic644267]
      4. Klicken Sie auf **OK**.
   2. Für **Abonnement**, wählen Sie das Abonnement, die Sie für Ihre Bereitstellung verwenden möchten.
   3. Für **Speicherkonto**, wählen Sie das Speicherkonto, das Sie verwenden möchten, verwenden, oder klicken Sie auf **neu** um ein neues Speicherkonto zu erstellen.
   4. Für **Dienstname**, wählen Sie den Clouddienst, den Sie verwenden möchten, verwenden, oder klicken Sie auf **neu** um einen neuen Clouddienst zu erstellen.
   5. Für **Target OS**, wählen Sie die Version des Betriebssystems, die Sie für Ihre Bereitstellung verwenden möchten.
   6. Für **zielumgebung**, für die Zwecke dieses Lernprogramms wählen **Staging**. (Wenn Sie bereit sind, Ihre Produktionswebsite bereitzustellen sind, ändern Sie diese Option, um **Produktion**.)
   7. Optional: Sicherstellen, dass **Überschreiben einer vorherigen Bereitstellung** ist aktiviert, wenn Sie Ihre neue Bereitstellung die vorherige Bereitstellung automatisch überschrieben werden soll. Wenn Sie diese Option aktivieren, werden Sie nicht Erfahrung "409 Conflict"-Probleme beim an demselben Speicherort veröffentlichen.
      Beachten Sie, dass die **Publish to Azure** Dialogfeld enthält einen Abschnitt für **Remotezugriff**. Standardmäßig Remotezugriff nicht aktiviert ist, und wir werden Sie nicht in diesem Beispiel aktivieren. Um den Remotezugriff zu aktivieren, geben Sie einen Benutzernamen und ein Kennwort zu verwendende Remote anmelden. Weitere Informationen zum Remotezugriff finden Sie unter [Remotezugriff aktivieren, für die Azure-Bereitstellungen in Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      Ihre **Publish to Azure** Dialogfeld sieht in etwa wie folgt:![][ic719488]

5. Klicken Sie auf **veröffentlichen** um in die Stagingumgebung zu veröffentlichen.

   Wenn Sie aufgefordert, einen vollständigen Build durchzuführen, klicken Sie auf **Ja**. Dies kann beim ersten Build mehrere Minuten dauern.
   Ein **Azure-Aktivitätsprotokoll** wird im Ansichtenabschnitt im Registerkartenformat Eclipse angezeigt.
   ![][ic719489]Sie können dieses Protokoll verwenden, sowie die **Konsole** Ansicht, um den Status Ihrer Bereitstellung anzuzeigen. Eine Alternative besteht darin, melden Sie sich die [Azure-Verwaltungsportal][Azure Management Portal], und verwenden Sie die **Clouddienste** Abschnitt aus, um den Status zu überwachen.

6. Wenn Ihre Bereitstellung erfolgreich bereitgestellt wird, die **Azure-Aktivitätsprotokoll** den Status des **veröffentlichte**. Klicken Sie auf **veröffentlichte**, wie in der folgenden Abbildung dargestellt, und öffnen Sie Ihren Browser wird eine Instanz Ihrer Bereitstellung.

   ![][ic719490]

Da dies eine Bereitstellung in einer Stagingumgebung gehandelt, werden die DNS-Namen im Format http://&lt;*Guid*&gt;. cloudapp.net und die URL wird der DNS-Name und ein Suffix für die Anwendung enthalten. Beispielsweise http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (Die **"myhelloworld"** Teil Groß-/Kleinschreibung beachtet wird.) Wenn Sie den Namen der Bereitstellung in der Azure Platform-Verwaltungsportal (innerhalb der Cloud-Dienste Teil des Verwaltungsportals) klicken, können Sie auch den DNS-Namen finden Sie unter.

Obwohl diese exemplarische Vorgehensweise für eine Bereitstellung in der Stagingumgebung wurde, eine Bereitstellung bis hin zur Produktion mit denselben Schritten, mit Ausnahme von innerhalb der **Publish to Azure** wählen Sie im Dialogfeld **Produktion** anstelle von **Staging** für die **zielumgebung**. Eine Bereitstellung bis hin zur Produktion führt zu einer URL basierend auf dem DNS-Namen Ihrer Wahl, anstatt eine GUID, wie für das Staging.

> [!WARNING]
> An diesem Punkt haben Sie die Azure-Anwendung in der Cloud bereitgestellt. Jedoch, bevor Sie fortfahren, beachten Sie, dass eine bereitgestellte Anwendung, auch wenn er nicht ausgeführt wird, weiterhin fakturierbare Zeit für Ihr Abonnement entstehen. Aus diesem Grund ist es äußerst wichtig, nicht gewünschte Bereitstellungen aus Ihrem Azure-Abonnement zu löschen.
> 
> 

## <a name="about-azure-deployment-projects"></a>Informationen zu Azure-Bereitstellungsprojekten
Um eine oder mehrere Java-Anwendungen in Azure bereitstellen, wird ein Azure-Bereitstellungsprojekt benötigt. Es spielt die Rolle des "Pakets", die Ihre Anwendungen verpackt werden um in Azure veröffentlicht werden müssen.

Neben den Informationen zu Ihren Anwendungen, Azure-Bereitstellungsprojekt enthält auch Informationen über andere Hauptkomponenten Ihrer Bereitstellung, hierbei am wichtigsten: der anwendungsservercontainer Ihre Web-app ausführen und die Java-Laufzeit, in denen auf. Azure unterstützt eine große Auswahl von Java-Laufzeiten und Java-Anwendungsservern, denen Sie auswählen können.

Obwohl es sich bei das hier verwendete Beispiel zu Lernzwecken erheblich vereinfacht wird, kann ein Azure-Bereitstellungsprojekt auch andere wichtige Konfigurationsinformationen enthalten, die Ihnen ermöglicht, nahezu beliebig komplexe, skalierbare, hochverfügbare, Multi-Tier-Cloud-Dienste mit Ihren Anwendungen zu erstellen. Sie können **sitzungsaffinität ("persistente Sitzungen")**, **schnelles caching**, **SSL-Abladung**, **Firewall-/portrouting**, **Remotezugriff**, und eine Reihe von anderen leistungsstarken Funktionen.

Wenn Sie im vorherigen Abschnitt dieses Lernprogramms ("zum Bereitstellen der Anwendung in Azure schnellen und auf einfache Weise") abgeschlossen haben, sehen Sie jetzt ein neues Azure-Bereitstellungsprojekt im Projekt-Explorer automatisch für Sie generiert und mit dem Namen "**MyHelloWorld_onAzure**".

Sie können auch in diesem Lernprogramm gestartet haben indem zuerst ein leeres Azure-Bereitstellungsprojekt selbst erstellen und dann Ihre Anwendung(en) hinzuzufügen. Dies ist ein längerer Prozess, verleiht Ihnen aber mehr Kontrolle über die Erstkonfiguration von Anfang.

Um ein neues Azure-Bereitstellungsprojekt von Grund auf neu zu erstellen, klicken Sie auf die **New Azure Deployment Project** Schaltfläche ![][ic710876].

Unabhängig davon, ob sind Sie mit einem bereits vorhandenen Azure-Bereitstellungsprojekt arbeiten oder eins von Grund auf neu erstellen, werden Sie so ändern Sie seine Konfigurationseinstellungen und Komponenten, z. B. das JDK oder den Anwendungsserver ausgeführt, ebenso können jederzeit einfach.

So ändern Sie das JDK oder den Anwendungsserver ausgeführt oder die Liste der Anwendungen in einem vorhandenen Azure-Bereitstellungsprojekt:

1. Erweitern Sie den Projektknoten (z. B. **MyHelloWorld_onAzure**) im Projekt-Explorer

2. Mit der rechten Maustaste **WorkerRole1**

3. Erweitern Sie die **Azure** Untermenü im Kontextmenü

4. Klicken Sie auf **Serverkonfiguration**

Unabhängig von, ob Sie diese Serverkonfigurationsschritte von gestartet bearbeiten ein vorhandenen Azure-Bereitstellungsprojekt, wie oben gezeigt, oder erstellen eine neue von Grund auf neu, sehen Sie die gleiche Art von Dialogfeldern, damit Sie Ihr JDK-, Server- und Anwendungskomponenten konfigurieren. Weitere Informationen zum Ändern der Einstellungen in diesen Dialogfeldern, z. B. das Ändern des JDK, den Anwendungsserver ausgeführt und hinzufügen oder Entfernen von Anwendungen in einer Bereitstellung finden Sie unter der [serverkonfigurationseigenschaften] [ Server configuration properties] Artikel.

## <a name="windows-only-to-deploy-your-application-to-the-compute-emulator"></a>Nur Windows: zum Bereitstellen der Anwendung im Serveremulator

> [!NOTE]
> Azure-Emulator ist nur unter Windows verfügbar. Überspringen Sie diesen Abschnitt, wenn Sie ein älteres Betriebssystem als Windows verwenden.
> 
> 

Wenn Sie ein neue Azure-Bereitstellungsprojekt befolgen die zuvor beschriebenen Schritten, also implizit, erstellt haben veröffentlichen Sie Ihre Anwendung in Azure, das JDK und den Application wurden Server für die Cloud, jedoch nicht für lokale Emulation konfiguriert. Um das Projekt testen im lokalen Emulator vorzubereiten, gehen Sie folgendermaßen vor:

1. Klicken Sie im Projektexplorer von Eclipse auf **MyHelloWorld_onAzure**.

2. Mit der rechten Maustaste auf **WorkerRole1**.

3. Erweitern Sie die **Azure** Untermenü im Kontextmenü.

4. Klicken Sie auf **Serverkonfiguration**.

5. Auf der **JDK** Registerkarte, überprüfen Sie, ob das Toolkit den Standardwert vorkonfiguriert hat local JDK für Sie. Wenn nicht oder wenn Sie die angenommenen Standardeinstellungen ändern möchten, sicher, dass die **JDK aus diesen Dateipfad für die Tests lokal verwenden** aktiviert ist und der JDK-Installationsspeicherort, den Sie verwenden möchten, wird angegeben. Wenn Sie sie ändern möchten, klicken Sie auf die **Durchsuchen** und verwenden Sie die Steuerelemente an, wählen Sie das Verzeichnis des JDK zu verwenden.

6. Klicken Sie auf die **Server** Registerkarte.

7. In der **lokaler Serverpfad** Textfeld unten auf der das Dialogfeld, geben Sie den Pfad von einer lokal installierten Servers ein, der den Typ und die Hauptversionsnummer des Servers unter oben im Dialogfeld ausgewählten entspricht der **Bereitstellen eines Servers dieses Typs** Kontrollkästchen. Wenn Sie einen anderen Typ oder die Hauptversion des Anwendungsservers verwenden möchten, müssen Sie zuerst ändern Sie die Auswahl unter diesem Kontrollkästchen.

8. Klicken Sie auf **OK**.

9. Klicken Sie in der Eclipse-Symbolleiste auf die **Run in Azure Emulator** Schaltfläche ![][ic710879]. Wenn die **Run in Azure Emulator** Schaltfläche nicht aktiviert ist, stellen Sie sicher, die **MyHelloWorld_onAzure** im Projektexplorer von Eclipse ausgewählt ist, und stellen Sie sicher, dass Projektexplorer von Eclipse im aktuellen Fenster den Fokus besitzt. Zuerst wird einen vollständigen Build Ihres Projekts gestartet und dann Ihre Java-Anwendung im Serveremulator zu starten. (Beachten Sie, dass je nach Leistungsmerkmale des Computers, der erste Build zwischen ein paar Sekunden einige Minuten dauern, aber nachfolgende builds schneller erhalten.) Nachdem der erste Buildschritt abgeschlossen wurde, werden Sie durch Benutzerkontensteuerung (UAC) Windows aufgefordert, diesen Befehl, um Änderungen an Ihrem Computer zu ermöglichen. Klicken Sie auf **Ja**.

> [!IMPORTANT]
> Wenn Sie nicht die UAC-Eingabeaufforderung angezeigt werden, überprüfen Sie die Windows-Taskleiste auf das Symbol "Benutzerkontensteuerung", und klicken Sie darauf zuerst. Manchmal wird die UAC Eingabeaufforderung wird nicht als oberstes Fenster angezeigt, aber nur als Taskleistensymbol sichtbar ist.
> 
> 

1. Überprüfen Sie die Ausgabe der Serveremulator-Benutzeroberfläche, um festzustellen, ob alle Probleme in Ihrem Projekt vorliegen. Je nach den Inhalten der Bereitstellungskonfiguration dauert es ein paar Minuten für Ihre Anwendung im Serveremulator vollständig gestartet werden soll.

2. Starten Sie den Browser, und verwenden Sie die URL `http://localhost:8080/MyHelloWorld` als Adresse (die `MyHelloWorld` Teil der URL wird Groß-/Kleinschreibung). Daraufhin sollte die Anwendung "myhelloworld" (die Ausgabe von "Index.jsp"), wie in der folgenden Abbildung:

   ![][ic589579]

Wenn Sie bereit für das Beenden der Anwendung im Serveremulator, in der Eclipse-Symbolleiste sind klicken Sie auf die **Reset Azure Emulator** Schaltfläche ![][ic710880].

## <a name="to-delete-your-deployment"></a>So löschen Sie die Bereitstellung
Zum Löschen Ihrer Bereitstellung im Azure-Toolkit für Eclipse stellen sicher, dass **MyHelloWorld_onAzure** wird im Projektexplorer von Eclipse ausgewählt ist, stellen Sie sicher im Projekt-Explorer von Eclipse verfügt das aktuelle Fenster zu konzentrieren, und klicken Sie dann auf die **Unpublish** Schaltfläche ![][ic710883], in der Eclipse-Symbolleiste. (Sie könnten denselben Vorgang tun, mit der rechten Maustaste **MyHelloWorld_onAzure** im Projektexplorer von Eclipse, klicken auf **Azure** und dann auf **Undeploy from Azure Cloud**.) Dies zeigt die **Unpublish Azure Project** Dialogfeld.

![][ic719491]

Wählen Sie das Abonnement und Cloud-Dienst, der die Bereitstellung enthält, wählen Sie die Bereitstellung, die Sie löschen möchten, und klicken Sie dann auf **Unpublish**.

(Eine Alternative zum Löschen der Bereitstellung mithilfe des Toolkits ist die Verwendung der **Clouddienste** Abschnitt des Azure-Verwaltungsportals: Navigieren Sie zu Ihrer Bereitstellung, wählen Sie ihn, und klicken Sie dann auf die **löschen** Schaltfläche. Dies beendet, und klicken Sie dann die Bereitstellung löschen. Wenn Sie nur die Bereitstellung beenden möchten und nicht löschen, klicken Sie auf die **beenden** anstelle der Schaltfläche den **löschen** Schaltfläche, jedoch als oben genannten, wenn Sie die Bereitstellung nicht löschen, weiterhin weitere Kosten für Ihre Bereitstellung entstehen, selbst wenn er beendet ist).

## <a name="see-also"></a>Siehe auch
[Azure-Toolkit für Eclipse][Azure Toolkit for Eclipse]

[Installieren des Azure-Toolkits für Eclipse][Installing the Azure Toolkit for Eclipse] 

[Neuigkeiten im Azure-Toolkit für Eclipse][What's New in the Azure Toolkit for Eclipse]

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter der [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
