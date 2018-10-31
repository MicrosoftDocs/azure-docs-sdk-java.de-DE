---
title: CI/CD für MicroProfile-Anwendungen mit Azure DevOps
description: Erfahren Sie, wie Sie mithilfe von Azure DevOps einen CI/CD-Releasezyklus zum Bereitstellen einer MicroProfile-Anwendung in einer Azure-Web-App für Container-Instanz einrichten.
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: 818e37291fa47f99cb161c63a86062bddbf6248c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799936"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a>CI/CD für MicroProfile-Anwendungen mit Azure DevOps

In diesem Tutorial wird beschrieben, wie Java EE-Entwickler mithilfe von Azure DevOps (früher bekannt als VSTS) mühelos einen CI/CD-Releasezyklus zum Bereitstellen ihrer [MicroProfile](http://microprofile.io)-Anwendungen in einer Azure-Web-App für Container-Instanz einrichten können.  In diesem Beispiel verwenden wir eine MicroProfile-Anwendung, die [Payara Micro](https://www.payara.fish/payara_micro) als Basisimage nutzt.   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
Wir beginnen mit dem Azure DevOps-Containerisierungsprozess, indem wir ein Docker-Image erstellen und das Containerimage in eine Azure Container Registry-Instanz pushen.  Anschließend stellen wir das Containerimage mithilfe einer Azure DevOps-Releasepipeline in einer Web-App bereit.

## <a name="prerequisites"></a>Voraussetzungen
- Kopieren und speichern Sie die Git-URL aus [GitHub](https://github.com/Azure-Samples/microprofile-hello-azure).
- Registrieren Sie sich für ein [Azure DevOps](https://dev.azure.com)-Konto, oder melden Sie sich mit Ihrem Azure DevOps-Konto an.
- Erstellen Sie ein neues [Azure DevOps-Projekt](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav), und verwenden Sie die oben genannte Git-URL zum **Importieren eines Repositorys**.
- Erstellen Sie eine [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry)-Instanz (ACR).
- Erstellen Sie eine Azure-Web-App für Container-Instanz.
  > [!NOTE]
  >
  > Wählen Sie beim Bereitstellen der Web-App-Instanz die Option „Schnellstart“ in den Containereinstellungen aus.


## <a name="create-a-build-definition"></a>Erstellen einer Builddefinition

Jedes Mal, wenn in der Java EE-Quellanwendung Commit ausgeführt wird, führt die Builddefinition in Azure DevOps automatisch alle Aufgaben im Build aus.  In diesem Beispiel verwendet Azure DevOps Maven zum Erstellen des Java-MicroProfile-Projekts.

1. Klicken Sie oben auf der Azure DevOps-Projektseite auf die Registerkarte „Build und Release“.  Klicken Sie dann auf den Link **Builds**. 

<img src="media/VSTS/Buid-and-Release1.png">

2. Klicken Sie auf die Schaltfläche **Neue Pipeline** und dann auf **Weiter**, um mit der Definition Ihrer Buildaufgaben zu beginnen.
3. Wählen Sie in der Vorlagenliste die Option „Maven“ aus, und klicken Sie auf die Schaltfläche **Anwenden**, um Ihr Java-Projekt zu erstellen.
4. Wählen Sie im Dropdownmenü des Felds „Agentpool“ die Option **Gehostete Linux-Vorschau** aus.
   > [!NOTE]
   >
   > Dadurch wird Azure DevOps der zu verwendende Server mitgeteilt.  Sie können Ihren privaten angepassten Buildserver verwenden.

5. Um Ihren Build für Continuous Integration zu konfigurieren, klicken Sie auf die Registerkarte **Trigger**, und aktivieren Sie das Kontrollkästchen **Continuous Integration aktivieren**.  

<img src="media/VSTS/Build-Triggers2.png"> 

6. Klicken Sie auf die Registerkarte <strong>Aufgaben</strong>, um zur Hauptseite für die Buildpipeline zurückzukehren.
7. Wählen Sie im Dropdownmenü <strong>Speichern und in Warteschlange einreihen&amp; die Option <strong>Speichern</strong> aus.


## <a name="create-a-docker-build-image"></a>Erstellen eines Docker-Buildimages

In dieser Aufgabe erstellt Azure DevOps anhand einer Dockerfile-Datei mit einem Basisimage von Payara Micro ein Docker-Image.  

1. Klicken Sie auf die Registerkarte **Aufgaben**, um zur Hauptseite für die Buildpipeline zurückzukehren.
2. Klicken Sie auf das Symbol **+**, um der Builddefinition eine neue Aufgabe hinzuzufügen.

<img src="media/VSTS/Tasks-add4.png">

3. Wählen Sie in der Vorlagenliste die Option &quot;Docker&quot; aus, und klicken Sie dann auf die Schaltfläche <strong>Hinzufügen</strong>.
4. Geben Sie einen beschreibenden Namen in das Feld <strong>Anzeigename</strong> ein.
5. Vergewissern Sie sich, dass im Dropdownmenü <strong>Containerregistrierungstyp</strong> die Option <strong>Azure Container Registry</strong> ausgewählt ist.
&gt; [!NOTE]
&gt; &gt;  Wenn Sie Docker-Hub oder eine andere Registrierung verwenden, wählen Sie stattdessen &quot;Containerregistrierung&quot; aus.  Klicken Sie dann auf die Schaltfläche &quot;+ Neu&quot;, um die zugehörigen Anmelde- und Verbindungsinformationen anzugeben. Wechseln Sie anschließend zum Abschnitt „Befehle“, um fortzufahren.

6. Wählen Sie im Dropdownmenü **Azure-Abonnement** Ihre Azure-Abonnement-ID aus.  Klicken Sie auf die Schaltfläche **Autorisieren**.
7. Wählen Sie im Dropdownmenü **Azure Container Registry** den Namen der Registrierung aus, die Sie in Azure erstellt haben.
8. Vergewissern Sie sich, dass im Dropdownmenü **Befehl** die Option **Erstellen** ausgewählt ist.
9. Klicken Sie für die **Dockerfile** auf das Pfadnavigationssymbol neben dem Textfeld, um die Dockerfile-Datei aus dem GitHub-Projekt auszuwählen.  Klicken Sie anschließend auf **OK**.

<img src="media/VSTS/Dockerfile5.png">

10. Aktivieren Sie unter **Imagename** das Kontrollkästchen **Aktuelles Tag einschließen**. 
11. Wählen Sie im Dropdownmenü **Speichern und in Warteschlange einreihen** die Option **Speichern** aus.

## <a name="push-docker-image-to-acr"></a>Pushen des Docker-Images in ACR

In dieser Aufgabe pusht Azure DevOps das Docker-Image in Ihre Azure Container Registry-Instanz.  Dieses Image wird verwendet, um die MicroProfile-API-Anwendung als Java-Container-Web-App auszuführen.

1. Da wir Docker in Azure DevOps verwenden, erstellen Sie eine neue Docker-Vorlage, indem Sie die Schritte 1 bis 7 im obigen Abschnitt **Erstellen eines Docker-Buildimages** wiederholen.
2. Wählen Sie im Dropdownmenü **Befehl** die Option **Push** aus.
3. Klicken Sie auf die Registerkarte **Speichern und in Warteschlange einreihen**, und wählen Sie dann **Speichern und in Warteschlange einreihen** aus.
4. Vergewissern Sie sich im Popupfenster, dass **Gehostete Linux-Vorschau** für den Agentpool ausgewählt ist.  Klicken Sie dann auf die Schaltfläche **Speichern und in Warteschlange einreihen**.
5. Klicken Sie auf die Buildnummer, um zu überprüfen, ob die Buildpipeline für das Java-Projekt erfolgreich abgeschlossen wurde.

<img src="media/VSTS/Build-Number6.png">


## <a name="create-a-release-definition-for-a-java-app"></a>Erstellen einer Releasedefinition für eine Java-App

Die Releasepipeline in Azure DevOps löst die Bereitstellung von Buildartefakten in einer Zielumgebung wie Azure automatisch aus, sobald der Buildprozess erfolgreich abgeschlossen wurde.   Die Releasepipeline kann für Entwicklungs-, Test-, Staging- oder Produktionsumgebungen erstellt werden.

1. Klicken Sie oben auf der Azure DevOps-Projektseite auf die Registerkarte „Build und Release“.  Klicken Sie dann auf den Link **Releases**.

<img src="media/VSTS/Release-new-pipeline7.png">

2. Klicken Sie auf die Schaltfläche &quot;Neue Pipeline**.
3. Wählen Sie in der Vorlagenliste die Option <strong>Java-App in Azure App Service bereitstellen</strong> aus, und klicken Sie dann auf die Schaltfläche <strong>Anwenden</strong>.

<img src="media/VSTS/deploy-java-template8.png">

4. Legen Sie einen <strong>Stufennamen</strong> fest (z. B. „Entwicklung“, „Test“, „Staging“ oder „Produktion“).  Klicken Sie dann auf die Schaltfläche mit dem <strong>X</strong>, um das Popupfenster zu schließen.
5. Klicken Sie im Abschnitt „Artefakte“ auf die Schaltfläche <strong>+ Hinzufügen</strong>.  Dadurch werden Artefakte aus der Builddefinition mit dieser Releasedefinition verknüpft.<br/>6. Wählen Sie im Dropdownmenü <strong>Source (build pipeline)</strong> (Quelle (Buildpipeline)) Ihre Builddefinition aus. Klicken Sie dann auf die Schaltfläche <strong>Hinzufügen</strong>, um fortzufahren.

<img src="media/VSTS/add-artifact9.png">

7. Klicken Sie auf die Registerkarte <strong>Aufgaben</strong> für die Pipeline.  Wählen Sie dann Ihren Stufennamen aus.

<img src="media/VSTS/release-stage10.png">

8. Wählen Sie im Dropdownmenü **Azure-Abonnement** Ihre Azure-Abonnement-ID aus.
9. Wählen Sie im Dropdownmenü **App-Typ** die Option **Linux-App** aus.
10. Wählen Sie im Dropdownmenü **App Service-Name** den Namen der Web-App für Container-Instanz aus, die Sie soeben erstellt haben.
11. Geben Sie den Namen Ihrer Azure Container Registry-Instanz in das Feld **Registrierung oder Namespace** ein,  beispielsweise **myregistry.azure.io**.
12. Geben Sie den Namen der Registrierung in das Feld **Repository** ein.
13. Klicken Sie auf **Azure App Service bereitstellen**.  Geben Sie das Tag für das Containerimage in das Textfeld **Tag** ein. 
14. Klicken Sie auf **Auf Agent ausführen**.  Wählen Sie im Dropdownmenü „Agentpool“ die Option **Gehostete Linux-Vorschau** aus 

## <a name="setup-environment-variables"></a>Einrichten von Umgebungsvariablen

1. Klicken Sie auf die Registerkarte **Variablen**.  Klicken Sie dann auf die Schaltfläche **+ Hinzufügen**, um Ihre Umgebungsvariablen zu definieren.
2. Fügen Sie die Variablennamen und -werte für die Containerregistrierungs-URL, den Benutzernamen und das Kennwort hinzu.   Klicken Sie aus Sicherheitsgründen auf das Schlosssymbol, um den Kennwortwert auszublenden.

Beispiel: 
- registry.password
- registry.url
- registry.username

<img src="media/VSTS/environment-variables12.png">

3. Klicken Sie auf die Registerkarte **Aufgaben**, um zur Hauptseite für die Definition der Releasepipeline zurückkehren.
4. Klicken Sie auf **Azure App Service bereitstellen**. 
5. Erweitern Sie den Abschnitt **Anwendungs- und Konfigurationseinstellungen**, und klicken Sie dann auf den Navigationspfad für das Feld **App-Einstellungen**, um Umgebungsvariablen hinzuzufügen, damit während der Bereitstellung eine Verbindung mit der Containerregistrierung hergestellt wird.
6. Klicken Sie auf die Schaltfläche „+ Hinzufügen“, um die folgenden App-Einstellungen zu definieren und die Umgebungsvariablen zuzuweisen.
7. DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)
8. DOCKER_REGISTRY_SERVER_URL = $(registry.url)
9. DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)

<img src="media/VSTS/environment-variables14.png">

7. Klicken Sie auf <strong>OK</strong>, um fortzufahren.

## <a name="setup-continious-deployment--deploy-java-application"></a>Einrichten von Continuous Deployment und Bereitstellen der Java-Anwendung

1. Klicken Sie zum Aktivieren von Continuous Deployment auf die Registerkarte **Pipelines**.
2. Klicken Sie im Abschnitt „Artefakte“ auf das Blitzsymbol.  Legen Sie dann **Continuous Deployment-Trigger** auf „Aktiviert“ fest.

<img src="media/VSTS/release-enable-CD.png">

3. Klicken Sie auf die Schaltfläche <strong>Speichern</strong> und dann auf <strong>OK</strong>. 
4. Klicken Sie auf das Dropdownmenü <strong>+ Freigabe</strong>, und wählen Sie dann <strong>Create a release</strong> (Release erstellen) aus.
5. Aktivieren Sie im Dropdownmenü <strong>Stages for a trigger change from automated to manual</strong> (Stufen für einen Trigger werden von automatisiert in manuell geändert) das Kontrollkästchen für Ihren Stufennamen.
6. Klicken Sie auf die Schaltfläche <strong>Erstellen</strong>, um fortzufahren.
7. Klicken Sie auf die Releasenummer.  Zeigen Sie anschließend mit dem Mauscursor auf den Stufennamen, und klicken Sie auf die Schaltfläche <strong>Bereitstellen</strong>.
8. Klicken Sie im Popupfenster auf die Schaltfläche <strong>Bereitstellen</strong>, um den Prozess der Bereitstellung in Azure zu starten.


## <a name="test-the-java-web-application"></a>Testen der Java-Webanwendung
1. Geben Sie die Web-App-URL im Webbrowser ein:  
   https://{Ihr-App-Service-Name}.azurewebsites.net/api/hello


<img src="media/VSTS/web-app16.png">

2. Auf der Webseite sollte **Hello Azure!** angezeigt werden.

<img src="media/VSTS/web-api17.png">
