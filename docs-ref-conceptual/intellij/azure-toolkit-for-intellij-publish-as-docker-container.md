---
title: "Veröffentlichen eines Docker-Containers mit dem Azure-Toolkit für IntelliJ"
description: "Erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine Web-App in Microsoft Azure als Docker-Container veröffentlichen."
services: 
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
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 2d94dfa4467bc79d6155321a9966358b79e9e960
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für IntelliJ

Docker-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen. Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen. Mit dem Azure-Toolkit für IntelliJ wird dieser Prozess für Java-Entwickler vereinfacht, indem Features vom Typ *Als Docker-Container veröffentlichen* für die Bereitstellung in Microsoft Azure hinzugefügt werden. In diesem Artikel werden die Schritte beschrieben, die zum Veröffentlichen Ihrer Anwendungen in Azure als Docker-Container erforderlich sind.

> [!NOTE]
>
> Weitere Informationen zu Docker finden Sie auf der [Docker-Website].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Veröffentlichen Ihrer Web-App in Azure mithilfe eines Docker-Containers

> [!NOTE]
> * Zum Veröffentlichen Ihrer Web-App müssen Sie ein Artefakt erstellen, das für die Bereitstellung bereit ist. Weitere Informationen finden Sie im Abschnitt [Zusätzliche Informationen zum Erstellen von Artefakten](#artifacts).
>
> * Nachdem Sie den Bereitstellungs-Assistenten mindestens einmal ausgeführt haben, sind die meisten Einstellungen bereits als Standardwerte vorhanden, wenn Sie den Assistenten erneut ausführen.
>

1. Öffnen Sie Ihr Web-App-Projekt in IntelliJ.

2. Wählen Sie eine der Optionen, um den Assistenten **Publish as Docker Container** (Als Docker-Container veröffentlichen) zu starten:

   * Klicken Sie im Fenster des Tools **Projekt** mit der rechten Maustaste auf Ihr Projekt, und klicken Sie dann auf **Azure** und **Publish as Docker Container** (Als Docker-Container veröffentlichen):

      ![Befehl „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PUB01]

   * Klicken Sie auf der IntelliJ-Symbolleiste auf die Schaltfläche **Publish Group** (Gruppe veröffentlichen) und anschließend auf **Publish as Docker Container** (Als Docker-Container veröffentlichen):

      ![Befehl „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PUB02]  
    Der Assistent **Deploy Docker Container on Azure** (Docker-Container in Azure bereitstellen) wird geöffnet.

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB03]

3. Gehen Sie im Fenster **Type an image name, select the artifact's path and check a Docker host to be used** (Geben Sie einen Imagenamen ein, wählen Sie den Pfad des Artefakts aus, und aktivieren Sie den gewünschten Docker-Host) wie folgt vor: 

   a. Geben Sie im Feld **Docker image name** (Docker-Imagename) einen eindeutigen Namen für Ihren Docker-Host ein. (Der Assistent gibt automatisch einen Namen vor, aber Sie können den Namen ändern.) 

   b. Im Bereich **Hosts** werden die Docker-Hosts angezeigt, die Sie bereits erstellt haben. Führen Sie einen der folgenden Schritte aus: 
      * Wenn Sie über einen vorhandenen Docker-Host verfügen, können Sie Ihre Web-App darauf bereitstellen.
      * Klicken Sie zum Erstellen eines Docker-Hosts auf das grüne Pluszeichen (**+**).  
       Das Dialogfeld **Create Docker Host** (Docker-Host erstellen) wird geöffnet. 

      ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB04a]

4. Geben Sie im Fenster **Configure the new virtual machine** (Neuen virtuellen Computer konfigurieren) die folgenden Informationen zu Ihrem Docker-Host ein. (Der Assistent generiert die meisten Informationen für Sie automatisch, aber Sie können sie ändern.) 

   a. Geben Sie im Feld **Name** einen eindeutigen Namen für den Docker-Host ein. (Dieser ist nicht mit dem Namen des Docker-Image identisch, den Sie zuvor angegeben haben.) 
    
   b. Geben Sie im Feld **Abonnement** das Azure-Abonnement ein, das Sie für Ihren Host verwenden. 
      
   c. Geben Sie im Feld **Region** die geografische Region ein, in der sich Ihr Host befindet.
      
   d. Gehen Sie auf der Registerkarte **OS and Size** (Betriebssystem und Größe) wie folgt vor:      
      * **Host OS** (Hostbetriebssystem): Geben Sie das Betriebssystem für den virtuellen Computer ein, der Ihren Host enthält. 
      * **Größe**: Geben Sie die Größe des virtuellen Computers für Ihren Host ein.   
       
   e. Wählen Sie auf der Registerkarte **Ressourcengruppe** eine der folgenden Optionen:      
      * **Neue Ressourcengruppe**: Erstellen Sie eine Ressourcengruppe für Ihren Host.
      * **Vorhandene Ressourcengruppe**: Geben Sie eine vorhandene Ressourcengruppe Ihres Azure-Kontos an. 
       
   f. Wählen Sie auf der Registerkarte **Netzwerk** eine der folgenden Optionen:      
      * **Neues virtuelles Netzwerk**: Erstellen Sie ein virtuelles Netzwerk für Ihren Host.
      * **Existing virtual network** (Vorhandenes virtuelles Netzwerk): Geben Sie ein vorhandenes virtuelles Netzwerk Ihres Azure-Kontos an. 
       
   g. Wählen Sie auf der Registerkarte **Speicher** eine der folgenden Optionen:      
      * **Neues Speicherkonto**: Erstellen Sie ein Speicherkonto für Ihren Host.
      * **Vorhandenes Speicherkonto**: Geben Sie ein vorhandenes Speicherkonto Ihres Azure-Kontos an.
       
5. Klicken Sie auf **Weiter**.
     
  Das Fenster **Configure log in credentials and port settings** (Anmeldeinformationen und Porteinstellungen konfigurieren) wird geöffnet.

      ![Fenster „Configure log in credentials and port settings“ (Anmeldeinformationen und Porteinstellungen konfigurieren)][PUB05]

6. Wählen Sie eine der folgenden Optionen:

      * **Import credentials from Azure Key Vault** (Anmeldeinformationen aus Azure Key Vault importieren): Geben Sie zuvor gespeicherte Anmeldeinformationen an, die in Ihrem Azure-Abonnement gespeichert sind.

          > [!NOTE]
          > Auf einen Azure-Schlüsseltresor, der in einem bestimmten Konto oder Dienstprinzipal erstellt wird, kann kein anderes Konto und kein anderer Dienstprinzipal desselben Abonnements automatisch zugreifen. Damit ein anderes Konto oder ein anderer Dienstprinzipal den Schlüsseltresor verwenden kann, müssen Sie im Azure-Portal das Konto oder den Dienstprinzipal hinzufügen.

      * **New log in credentials** (Neue Anmeldeinformationen): Erstellen Sie neue Anmeldeinformationen. Gehen Sie bei Auswahl dieser Option wie folgt vor:

        a. Geben Sie auf der Registerkarte **VM Credentials** (VM-Anmeldeinformationen) die folgenden Angaben für die VM-Anmeldeinformationen Ihres Docker-Hosts an: * **Benutzername**: Geben Sie den Benutzernamen für Ihre VM-Anmeldeinformationen ein.
             * **Kennwort** und **Bestätigen**: Geben Sie das Kennwort für Ihre VM-Anmeldeinformationen ein.
             * **SSH**: Geben Sie die SSH-Einstellungen (Secure Shell) für Ihren Docker-Host ein. Sie können eine der folgenden Optionen auswählen: * **Keine**: Gibt an, dass für Ihren virtuellen Computer keine SSH-Verbindungen zulässig sind.
                * **Automatisch generieren**: Mit dieser Option werden die erforderlichen Einstellungen zum Herstellen einer Verbindung über SSH automatisch erstellt.
                * **Import from directory** (Aus Verzeichnis importieren): Ermöglicht das Angeben eines Verzeichnisses, das zuvor gespeicherte SSH-Einstellungen enthält. Das Verzeichnis muss die folgenden beiden Dateien enthalten:
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        b. Geben Sie auf der Registerkarte **Docker Daemon Access** (Docker-Daemon-Zugriff) die folgenden Informationen an:

          ![Erstellen eines Docker-Hosts][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. Klicken Sie nach dem Eingeben der erforderlichen Informationen auf **Fertig stellen**.  
    Der Assistent **Deploy Docker Container on Azure** (Docker-Container in Azure bereitstellen) wird wieder angezeigt.

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB07]

8. Klicken Sie auf **Weiter**.  
    Das Fenster **Configure the Docker container to be created** (Zu erstellenden Docker-Container konfigurieren) wird geöffnet.

   ![Fenster „Configure the Docker container to be created“ (Zu erstellenden Docker-Container konfigurieren)][PUB08]

9. Geben Sie im Fenster **Configure the Docker container to be created** (Zu erstellenden Docker-Container konfigurieren) die folgenden Informationen an: 

   a. Geben Sie im Feld **Docker container name** (Name des Docker-Containers) einen eindeutigen Namen für Ihren Docker-Container ein.

   b. Wählen Sie eines der folgenden Docker-Images aus: 

      * **Predefined Docker image** (Vordefiniertes Docker-Image): Geben Sie ein bereits in Azure vorhandenes Docker-Image an. 

        > [!NOTE]
        > Die Liste mit den Docker-Images in diesem Feld enthält mehrere Images, für deren Patching das Azure-Toolkit konfiguriert ist, damit Ihr Artefakt automatisch bereitgestellt wird. 

      * **Custom Dockerfile** (Benutzerdefinierte Dockerfile): Geben Sie eine zuvor auf Ihrem lokalen Computer gespeicherte Dockerfile an.

        > [!NOTE]
        > Dies ist eine komplexere Funktion für Entwickler, die ihre eigene Dockerfile bereitstellen möchten. Es ist jedoch Aufgabe von Entwickler, die diese Option wählen, dafür zu sorgen, dass ihre Dockerfile ordnungsgemäß erstellt wurde. Da das Azure-Toolkit den Inhalt einer benutzerdefinierten Dockerfile nicht überprüft, kann die Bereitstellung unter Umständen fehlschlagen, wenn die Dockerfile Probleme verursacht. Weil vom Azure-Toolkit erwartet wird, dass die benutzerdefinierte Dockerfile ein Web-App-Artefakt enthält, wird außerdem versucht, eine HTTP-Verbindung zu öffnen. Wenn Entwickler eine andere Art von Artefakt veröffentlichen, können nach der Bereitstellung ggf. harmlose Fehler auftreten.

   c. Geben Sie im Feld **Porteinstellungen** die eindeutige TCP-Portbindung für Ihren Docker-Container ein. 

10. Nachdem Sie die obigen Schritte abgeschlossen haben, können Sie auf **Fertig stellen** klicken. 

Das Azure-Toolkit beginnt damit, Ihre Web-App in einem Docker-Container in Azure bereitzustellen. Sofern Sie für IntelliJ nicht die Bereitstellung im Hintergrund konfiguriert haben, wird die Statusanzeige **Deploying to Azure** (Wird in Azure bereitgestellt) angezeigt. 

![Statusanzeige für Bereitstellung][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Zusätzliche Informationen zum Erstellen von Artefakten

Gehen Sie wie folgt vor, um ein bereitstellungsfähiges Artefakt zu erstellen:

1. Öffnen Sie Ihr Web-App-Projekt in IntelliJ.

2. Klicken Sie auf **Datei** und dann auf **Projektstruktur**.

   ![Befehl „Projektstruktur“][ART01]

3. Klicken Sie zum Hinzufügen eines Artefakts auf das grüne Pluszeichen (**+**) und dann auf **Webanwendung: Archiv**.

   ![Befehl „Webanwendung: Archiv“][ART02]

4. Geben Sie im Feld **Name** einen Namen für Ihr Artefakt ein (ohne die Erweiterung *.war*), und klicken Sie dann auf **OK**.

   ![Feld „Name“ für Artefakt][ART03]

Weitere Informationen zum Erstellen von Artefakten in IntelliJ finden Sie auf der JetBrains-Website unter [Konfigurieren von Artefakten].

## <a name="next-steps"></a>Nächste Schritte

Zusätzliche Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website].

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Docker-Website]: https://www.docker.com/
[Konfigurieren von Artefakten]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
