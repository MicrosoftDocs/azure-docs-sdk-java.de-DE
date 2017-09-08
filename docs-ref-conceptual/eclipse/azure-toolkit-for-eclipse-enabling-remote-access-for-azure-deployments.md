---
title: "Aktivieren des Remotezugriffs für Azure-Bereitstellungen in Eclipse"
description: "Informationen Sie zum Aktivieren des Remotezugriffs für Azure-Bereitstellungen mit dem Azure-Toolkit für Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Aktivieren des Remotezugriffs für Azure-Bereitstellungen in Eclipse
Um Ihre Bereitstellungen zu beheben, können Sie aktivieren und Remotezugriff für die Verbindung mit dem virtuellen Computer hostet Ihre Bereitstellung verwenden. Der RAS-Funktionen basiert auf dem Remote Desktop Protocol (RDP). Sie können Remotezugriff für Ihre Bereitstellung konfigurieren, nachdem Sie in Azure veröffentlicht haben, oder wenn Sie Eclipse mit einem Windows-Betriebssystem verwenden, Sie Remote Access konfigurieren können, bevor Sie in Azure veröffentlichen. Beachten Sie, dass Sie einen Remotedesktopclient, der mit Ihrem Betriebssystem kompatibel ist erforderlich ist, um mit der Bereitstellung virtuellen Computer in Azure zu verbinden.

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a>Gewusst wie: Aktivieren des Remotezugriffs vor der Bereitstellung in Azure
> [!NOTE]
> Um den Remotezugriff aktivieren, bevor Sie Ihre Anwendung in Azure bereitstellen, müssen Sie Eclipse unter Windows ausgeführt werden.
> 
> 

Die folgende Abbildung zeigt die **Remotezugriff** Eigenschaftendialogfeld verwendet, um den Remotezugriff zu ermöglichen.

![][ic719494]

Es gibt zwei Möglichkeiten zum Anzeigen der **Remotezugriff** Dialogfeld "Eigenschaften":

* Klicken Sie auf die **erweitert** link die **Remotezugriff** Teil der **Publish to Azure** Dialogfeld.

* Öffnen der **Eigenschaften** Dialogfeld des Azure-Projekts.

Wenn Sie ein neues Azure-Bereitstellungsprojekt erstellen, müssen das Projekt nicht Remote Access standardmäßig aktiviert. Allerdings können Sie Remotezugriff problemlos aktivieren, indem Sie den Benutzernamen und Kennwort in die **Publish to Azure** Dialogfeld. Der RAS-Kennwort wird mithilfe von x. 509-Zertifikaten verschlüsselt. Wenn Sie nicht verwenden, geben Sie Ihr eigenes Zertifikat die Verschlüsselung ein selbst signiertes Zertifikat, das im Lieferumfang der Azure-Plug-In für Eclipse verwendet. Dieses selbstsignierte Zertifikat befindet sich in der **Cert** Ordner des Azure-Projekts, sowohl als öffentliche Zertifikatdatei (SampleRemoteAccessPublic.cer) als ein Personal Information Exchange (PFX)-Zertifikatdatei (SampleRemoteAccessPrivate.pfx) gespeichert. Die letztere Datei enthält den privaten Schlüssel für das Zertifikat, und es wurde ein Standardkennwort **Password1**. Da dieses Kennwort öffentlich bekannt ist, sollte jedoch das Standardzertifikat verwendet werden lediglich zu Schulungszwecken nicht für eine produktionsbereitstellung. Außer zu Lernzwecken beim Aktivieren von Remotesitzungen für Ihre Bereitstellungen werden sollen. Klicken Sie auf die **erweitert** wiederherstellungsverknüpfung in der **Publish to Azure** Dialogfeld, um Ihr eigenes Zertifikat anzugeben. Beachten Sie, müssen Sie die PFX-Version des Zertifikats in den gehosteten Dienst im Azure-Verwaltungsportal hochladen, damit das Kennwort des Benutzers, die Azure entschlüsselt werden kann.

Der Rest des Lernprogramms wird gezeigt, wie Remotezugriff für ein Azure-Bereitstellungsprojekt zu aktivieren, die ursprünglich mit deaktiviertem Remotezugriff erstellt wurde. Für die Zwecke dieses Lernprogramms wir erstellen ein neues selbstsigniertes Zertifikat, und die PFX-Datei hat ein Kennwort Ihrer Wahl. Sie haben auch die Möglichkeit, ein von einer Zertifizierungsstelle ausgestelltes Zertifikat verwenden.

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a>Gewusst wie: Aktivieren des Remotezugriffs nach der Bereitstellung in Azure
Um den Remotezugriff aktivieren, nachdem Sie in Azure bereitgestellt haben, verwenden Sie die folgenden Schritte aus:

1. Melden Sie sich bei Azure-Verwaltungsportal mit Ihrem Azure-Konto

2. In der Liste der **Clouddienste**, wählen Sie Ihren bereitgestellten Cloud-Dienst

3. Klicken Sie auf der Webseite des Cloud-Dienst auf dem **konfigurieren** Link

4. Am unteren Rand der Seite "Konfiguration", klicken Sie auf die **Remote** Link

5. Wenn das Popupdialogfeld angezeigt wird:
   
   * Geben Sie die Rolle, die Sie zum gewünschten Remotezugriff zu ermöglichen

   * Klicken Sie auf die **Remotedesktop aktivieren** Kontrollkästchen
   
   * Geben Sie einen Benutzernamen und Kennwort, die Sie für den Remotezugriff verwenden möchten.
   
   * Wählen Sie das zu verwendende Zertifikat

6. Klicken Sie auf **OK**. 

Sie sehen eine Meldung, die besagt, dass Ihre konfigurationsänderung ausgeführt wird, wird die kann einen Moment dauern. Nachdem die konfigurationsänderung abgeschlossen ist, führen Sie die Schritte in der **zur Remoteanmeldung** Abschnitt weiter unten in diesem Artikel.

## <a name="how-to-enable-remote-access-in-your-package"></a>Gewusst wie: Aktivieren des Remotezugriffs in Ihrem Paket
1. Im Projektexplorer von Eclipse, Maustaste das Azure-Projekt, und klicken Sie auf **Eigenschaften**.

2. In der **Eigenschaften** Dialogfeld erweitern Sie **Azure** im linken Bereich, und klicken Sie auf **Remotezugriff**.

3. In der **Remotezugriff** Dialogfeld, stellen Sie sicher **Remotedesktopverbindungen mit diesen Anmeldeinformationen akzeptiert alle Rollen aktivieren** aktiviert ist.

4. Geben Sie einen Benutzernamen für die Remotedesktopverbindung.

5. Geben Sie an, und bestätigen Sie das Kennwort für den Benutzer. Die Benutzer und Kennwort Werte in diesem Dialogfeld festgelegten werden verwendet werden, wenn Sie eine Remotedesktopverbindung vornehmen. (Beachten Sie, dass dieses Kennwort vom PFX-Kennwort ist.)

6. Geben Sie das Ablaufdatum für das Benutzerkonto ein.

7. Klicken Sie auf **neu** ein neues selbstsigniertes Zertifikat erstellen. (Alternativ können Sie ein Zertifikat auswählen, aus Ihrem Arbeitsbereich oder Dateisystem über die **Arbeitsbereich** oder **FileSystem** Schaltflächen, aber für die Zwecke dieses Lernprogramms erstellen wir ein neues Zertifikat.)

   * In der **neues Zertifikat** Dialogfeld, geben Sie ein, und bestätigen Sie das Kennwort, das Sie für die PFX-Datei verwenden.

   * Übernehmen Sie den vorgesehenen Wert **Name (CN)**, oder verwenden Sie einen benutzerdefinierten Namen.

   * Geben Sie den Pfad und Dateinamen ein, die, in dem das neue Zertifikat, im CER-Format gespeichert wird. Für diesen Schritt und den nächsten Schritt können Sie die **Cert** Ordner Azure-Projekt, aber Sie können auch einen anderen Speicherort auszuwählen. Für dieses Lernprogramm verwenden wir **c:\mycert\mycert.cer**. (Erstellen der **c:\mycert** Ordner, bevor Sie den Vorgang fortsetzen, oder verwenden Sie einen vorhandenen Ordner aus, falls gewünscht.)

   * Geben Sie den Pfad und Dateinamen ein, die, in dem das neue Zertifikat und seinen privaten Schlüssel im PFX-Format gespeichert werden. Für dieses Lernprogramm verwenden wir **c:\mycert\mycert.pfx**. Ihre **neues Zertifikat** Dialogfeld sollte etwa wie folgt aussehen (Aktualisieren Sie die Ordnerpfade, wenn Sie nicht verwendet haben **c:\mycert**):
     
      ![][ic712275]

   * Klicken Sie auf **OK** schließen die **neues Zertifikat** Dialogfeld.

8. Ihre **Remotezugriff** Dialogfeld sollte etwa wie folgt aussehen:</p>
   
   ![][ic719495]

9. Klicken Sie auf **OK** schließen die **Remotezugriff** Dialogfeld.

Erstellen Sie Ihre Anwendung mit dem Build, legen Sie für die Bereitstellung in der cloud neu.

## <a name="to-log-in-remotely"></a>Zur Remoteanmeldung
Sobald Ihre Rolleninstanz bereit ist, können Sie Remote mit dem virtuellen Computer anmelden, die Ihre Anwendung gehostet wird.

* Wenn Sie Eclipse unter Windows und ausgewählten verwenden die **Starten von Remotedesktop auf bereitstellen** Option während der Bereitstellung in Azure, Sie werden erhält den Anmeldebildschirm für die Remotedesktopverbindung beim Starten der Bereitstellung. Wenn Sie für den Benutzernamen und Kennwort aufgefordert werden, geben Sie die Werte, die Sie für den Remotebenutzer angegeben und wird in der Lage, melden Sie sich.

* Eine weitere Möglichkeit zur Remoteanmeldung ist über die <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure-Verwaltungsportal</a>:
  
  * Innerhalb der **Clouddienste** des Azure-Verwaltungsportals anzuzeigen, klicken Sie auf den Cloud-Dienst, klicken Sie auf **Instanzen**, klicken Sie auf eine bestimmte Instanz, und klicken Sie dann auf die **verbinden** Schaltfläche. Die **verbinden** Schaltfläche wird wie folgt auf der Befehlsleiste angezeigt:
    
      ![][ic659273]

  * Nach dem Klicken auf die **verbinden** Schaltfläche, werden Sie aufgefordert, um eine RDP-Datei zu öffnen. Öffnen Sie die Datei, und befolgen Sie die Anweisungen. (Sie könnten diese Datei auch auf dem lokalen Computer speichern und führen Sie die Datei durch Doppelklicken zur Remoteanmeldung auf dem virtuellen Computer ohne zuerst Verwaltungsportal wechseln.)

  * Wenn Sie für den Benutzernamen und Kennwort aufgefordert werden, geben Sie die Werte, die Sie für den Remotebenutzer angegeben und wird in der Lage, melden Sie sich.

> [!NOTE]
> Wenn Sie eine nicht-Windows-Betriebssystem arbeiten, müssen Sie einen Remotedesktop-Client, der mit Ihrem Betriebssystem kompatibel ist, und führen die Schritte zum Konfigurieren von diesem Clients mit den Einstellungen in der RDP-Datei, die Sie heruntergeladen haben.
> 
> 

## <a name="see-also"></a>Siehe auch
[Azure-Toolkit für Eclipse][Azure Toolkit for Eclipse]

[Erstellen einer Hello World-Anwendung für Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Installieren des Azure-Toolkits für Eclipse][Installing the Azure Toolkit for Eclipse] 

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter der [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
