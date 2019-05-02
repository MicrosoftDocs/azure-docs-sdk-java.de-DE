---
title: Veröffentlichen eines Docker-Containers mithilfe des Azure-Toolkits für Eclipse
description: Erfahren Sie, wie Sie mit dem Azure-Toolkit für Eclipse eine Web-App in Microsoft Azure als Docker-Container veröffentlichen.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4eb159bef52b384de32ada18937b0b9a47a93afc
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61590793"
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für Eclipse

Docker-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen. Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen. Mit dem Azure-Toolkit für Eclipse wird dieser Prozess für Java-Entwickler vereinfacht, indem Features vom Typ *Als Docker-Container veröffentlichen* für die Bereitstellung in Microsoft Azure hinzugefügt werden. In diesem Artikel werden die Schritte beschrieben, die zum Veröffentlichen Ihrer Anwendungen in Azure als Docker-Container erforderlich sind.

> [!NOTE]
> Weitere Informationen zu Docker finden Sie auf der [Docker-Website].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Veröffentlichen Ihrer Web-App in Azure mithilfe eines Docker-Containers

1. Öffnen Sie Ihr Web-App-Projekt in Eclipse.

2. Wählen Sie eine der Optionen, um den Assistenten **Publish as Docker Container** (Als Docker-Container veröffentlichen) zu starten:

   * Klicken Sie in der Ansicht **Navigator** mit der rechten Maustaste auf Ihr Projekt, und klicken Sie dann auf **Azure** und **Publish as Docker Container** (Als Docker-Container veröffentlichen).

      ![Navigator-Ansicht „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PUB01]

   * Klicken Sie auf der Eclipse-Symbolleiste auf die Schaltfläche **Publish** (Veröffentlichen) und anschließend auf **Publish as Docker Container** (Als Docker-Container veröffentlichen).

      ![Eclipse-Symbolleiste „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PUB02]
      
   Der Assistent **Deploy Docker Container on Azure** (Docker-Container in Azure bereitstellen) wird geöffnet.

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB03]

3. Gehen Sie im Fenster **Type an image name, select the artifact's path and check a Docker host to be used** (Geben Sie einen Imagenamen ein, wählen Sie den Pfad des Artefakts aus, und aktivieren Sie den gewünschten Docker-Host) wie folgt vor:

   a. Geben Sie im Feld **Docker image name** (Docker-Imagename) einen eindeutigen Namen für Ihren Docker-Host ein. (Der Assistent gibt automatisch einen Namen vor, aber Sie können den Namen ändern.)

   b. Im Bereich **Hosts** werden die Docker-Hosts angezeigt, die Sie bereits erstellt haben. Führen Sie einen der folgenden Schritte aus:

   * Wenn Sie über einen vorhandenen Docker-Host verfügen, können Sie Ihre Web-App darauf bereitstellen.
   * Um einen neuen Docker-Host zu erstellen, klicken Sie auf **Add** (Hinzufügen).  
      
      Das Dialogfeld **Create Docker Host** (Docker-Host erstellen) wird geöffnet.

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB04a]

4. Geben Sie im Fenster **Configure the new virtual machine** (Neuen virtuellen Computer konfigurieren) die folgenden Optionen für Ihren Docker-Host an. (Der Assistent generiert die meisten Optionen für Sie automatisch, aber Sie können sie ändern.)

   a. **Name**: Geben Sie einen eindeutigen Name für den Docker-Host ein. (Dieser ist nicht mit dem Namen des Docker-Image identisch, den Sie zuvor angegeben haben.)

   b. **Abonnement**: Geben Sie das Azure-Abonnement ein, das Sie für Ihren Host verwenden.

   c. **Region**: Geben Sie die geografische Region ein, in der sich Ihr Host befindet.

   d. Auf der Registerkarte **Host-BS und Größe**: 
   * **Host OS** (Hostbetriebssystem): Geben Sie das Betriebssystem für den virtuellen Computer ein, der Ihren Host enthält.
   * **Größe**: Geben Sie die Größe des virtuellen Computers für Ihren Host ein.

   e. Auf der Registerkarte **Ressourcengruppe**: 
   * **Neue Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe für Ihren Host.
   * **Vorhandene Ressourcengruppe**: Geben Sie eine vorhandene Ressourcengruppe Ihres Azure-Kontos ein.

   f. Auf der Registerkarte **Netzwerk**: 
   * **Neues virtuelles Netzwerk**: Erstellen Sie ein neues virtuelles Netzwerk für Ihren Host.
   * **Existing virtual network** (Vorhandenes virtuelles Netzwerk): Geben Sie ein vorhandenes virtuelles Netzwerk Ihres Azure-Kontos ein.

   g. Auf der Registerkarte **Storage**: 
   * **Neues Speicherkonto**: Erstellen Sie ein neues Speicherkonto für Ihren Host.
   * **Vorhandenes Speicherkonto**: Geben Sie ein vorhandenes Speicherkonto Ihres Azure-Kontos ein.

5. Klicken Sie auf **Weiter**.

6. Wählen Sie im Fenster **Configure log in credentials and port settings** (Anmeldeinformationen und Porteinstellungen konfigurieren) eine der folgenden Optionen aus:

   * **Import credentials from Azure Key Vault** (Anmeldeinformationen aus Azure Key Vault importieren): Gibt zuvor gespeicherte Anmeldeinformationen an, die in Ihrem Azure-Abonnement gespeichert sind. 

   >[!NOTE]
   >Auf einem Azure Key Vault-Tresor, der in einem bestimmten Konto oder Dienstprinzipal erstellt wird, kann kein anderes Konto und kein anderer Dienstprinzipal desselben Abonnements automatisch zugreifen. Damit ein anderes Konto oder ein anderer Dienstprinzipal den Key Vault-Schlüsseltresor verwenden kann, müssen Sie im Azure-Portal das Konto oder den Dienstprinzipal hinzufügen.
   >

   * **New log in credentials** (Neue Anmeldeinformationen): Erstellt neue Anmeldeinformationen. Gehen Sie bei Auswahl dieser Option wie folgt vor: 
    
     * Wählen Sie auf der Registerkarte **VM-Anmeldeinformationen** eine der folgenden Optionen für die Anmeldung beim virtuellen Computer Ihres Docker-Hosts: 

       * **Benutzername**: Geben Sie den Benutzernamen für die Anmeldeinformationen Ihres virtuellen Computers an. 
       * **Kennwort** und **Bestätigen**: Geben Sie das Kennwort für die Anmeldeinformationen Ihres virtuellen Computers an. 
       * **SSH**: Geben Sie die SSH-Einstellungen (Secure Shell) für Ihren Docker-Host ein. Sie können zwischen folgenden Optionen wählen: 
          * **Keine:** Gibt an, dass Ihr virtueller Computer keine SSH-Verbindungen zulässt. 
          * **Automatisch generieren**: Mit dieser Option werden die erforderlichen Einstellungen zum Herstellen einer Verbindung über SSH automatisch erstellt. 
          * **Import from directory** (Aus Verzeichnis importieren): Gibt ein Verzeichnis an, das zuvor gespeicherte SSH-Einstellungen enthält. Das Verzeichnis muss die folgenden beiden Dateien enthalten: 
             * *id_rsa*: Enthält die RSA-Kennung eines Benutzers. 
             * *id_rsa.pub*: Enthält den öffentlichen RSA-Schlüssel, der für die Authentifizierung verwendet wird. 
        
         ![Erstellen eines Docker-Hosts][PUB05]

     * Geben Sie auf der Registerkarte **Docker-Daemon-Anmeldeinformationen** die folgenden Optionen an: 

       * **Docker-Daemon-Port**: Geben Sie den eindeutigen TCP-Port für den Docker-Host an. 
       * **TLS-Sicherheit**: Geben Sie die Transport Layer Security-Einstellungen für Ihren Docker-Host an. Sie können zwischen folgenden Optionen wählen: 
          * **Keine:** Gibt an, dass Ihr virtueller Computer keine TLS-Verbindungen zulässt. 
          * **Automatisch generieren**: Mit dieser Option werden die erforderlichen Einstellungen zum Herstellen einer Verbindung über TLS automatisch erstellt. 
          * **Import from directory** (Aus Verzeichnis importieren): Gibt ein Verzeichnis an, das zuvor gespeicherte TLS-Einstellungen enthält. Genauer gesagt muss das Verzeichnis die folgenden sechs Dateien enthalten: 
             * *ca.pem* und *ca-key.pem*: Enthalten das Zertifikat und den öffentlichen Schlüssel für die TLS-Zertifizierungsstelle. 
             * *cert.pem* und *key.pem*: Enthalten das Clientzertifikat und den öffentlichen Schlüssel für die TLS-Authentifizierung. 
             * *server.pem* und *server-key.pem*: Enthalten das Serverzertifikat und den öffentlichen Schlüssel für den Host. 

         ![Erstellen eines Docker-Hosts][PUB06]

7. Klicken Sie nach dem Eingeben aller erforderlichen Informationen auf **Fertig stellen**.

8. Klicken Sie im Assistenten **Deploy Docker Container on Azure** (Docker-Container in Azure bereitstellen) auf **Weiter**.

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB07]

9. Im Fenster **Configure the Docker container to be created** (Zu erstellenden Docker-Container konfigurieren) tun Sie Folgendes:

   a. Geben Sie im Feld **Docker container name** (Name des Docker-Containers) einen eindeutigen Namen für Ihren Docker-Container ein.

   b. Wählen Sie eines der folgenden Docker-Images aus: 

   * **Predefined Docker image** (Vordefiniertes Docker-Image): Gibt ein bereits in Azure vorhandenes Docker-Image an. 

     >[!NOTE]
     >Die Liste mit den Docker-Images in diesem Feld enthält mehrere Images, für deren Patching das Azure-Toolkit konfiguriert ist, damit Ihr Artefakt automatisch bereitgestellt wird.
     >

   * **Custom Dockerfile** (Benutzerdefinierte Dockerfile): Gibt eine zuvor auf Ihrem lokalen Computer gespeicherte Dockerfile an.

     >[!NOTE]
     >Dies ist eine komplexere Funktion für Entwickler, die ihre eigene Dockerfile bereitstellen möchten. Es ist jedoch Aufgabe von Entwickler, die diese Option wählen, dafür zu sorgen, dass ihre Dockerfile ordnungsgemäß erstellt wurde. Das Azure-Toolkit überprüft nicht den Inhalt einer benutzerdefinierten Dockerfile, sodass die Bereitstellung möglicherweise fehlschlägt, wenn die Dockerfile Probleme verursacht. Weil vom Azure-Toolkit erwartet wird, dass die benutzerdefinierte Dockerfile ein Web-App-Artefakt enthält, wird außerdem versucht, eine HTTP-Verbindung zu öffnen. Wenn Entwickler eine andere Art von Artefakt veröffentlichen, können nach der Bereitstellung womöglich harmlose Fehler auftreten.
     >

   c. **Porteinstellungen**: Geben Sie die eindeutige TCP-Portbindung für Ihren Docker-Container ein.

      ![Fenster „Configure the Docker container to be created“ (Zu erstellenden Docker-Container konfigurieren)][PUB08]

10. Nachdem Sie alle obigen Schritte abgeschlossen haben, können Sie auf **Fertig stellen** klicken.

Das Azure-Toolkit beginnt damit, Ihre Web-App in einem Docker-Container in Azure bereitzustellen. 

## <a name="next-steps"></a>Nächste Schritte

Zusätzliche Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website].

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Docker-Website]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png