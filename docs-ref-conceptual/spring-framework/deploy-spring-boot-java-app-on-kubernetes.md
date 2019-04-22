---
title: Bereitstellen einer Spring Boot-App unter Kubernetes in Azure Kubernetes Service
description: In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Microsoft Azure erläutert.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 42bb030a916cc5aaf1e20242518a0a400b8baa88
ms.sourcegitcommit: f33befab25a66a252b4c91c7aeb1b77cb32821bb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2019
ms.locfileid: "59745158"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a>Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Kubernetes Service

**[Kubernetes]** und **[Docker]** sind Open Source-Lösungen, mit denen Entwickler die Bereitstellung, Skalierung und Verwaltung ihrer in Containern ausgeführten Anwendungen automatisieren können.

In diesem Tutorial wird die Kombination dieser beiden gängigen Open Source-Technologien zum Entwickeln und Bereitstellen einer Spring Boot-Anwendung in Microsoft Azure erläutert. Genauer gesagt verwenden Sie *[Spring Boot]* für die Anwendungsentwicklung, *[Kubernetes]* für die Containerbereitstellung und [Azure Kubernetes Service (AKS)] zum Hosten der Anwendung.

### <a name="prerequisites"></a>Voraussetzungen

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
* Die [Azure-Befehlszeilenschnittstelle (CLI)]
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* Das Erstellungstool Apache [Maven] (Version 3)
* Einen [Git-Client]
* Einen [Docker]-Client

> [!NOTE]
>
> Aufgrund der Virtualisierungsanforderungen dieses Tutorials können Sie die Schritte in diesem Artikel nicht auf einem virtuellen Computer ausführen; Sie müssen einen physischen Computer mit aktivierten Virtualisierungsfunktionen verwenden.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Erstellen der Web-App für erste Schritte mit Spring Boot in Docker

Im Folgenden werden die Schritte zum Erstellen einer Spring Boot-Webanwendung und zum lokalen Testen dieser Anwendung beschrieben.

1. Öffnen Sie eine Eingabeaufforderung, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   – oder –
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Verwenden Sie Maven zum Erstellen und Ausführen der Beispiel-App.
   ```
   mvn package spring-boot:run
   ```

1. Testen Sie die Web-App durch Navigieren zu `http://localhost:8080` oder mit dem folgenden `curl`-Befehl:
   ```
   curl http://localhost:8080
   ```

1. Die folgende Meldung sollte angezeigt werden: **Hello Docker World!**

   ![Lokales Durchsuchen von Beispiel-Apps][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Erstellen einer Azure Container Registry-Instanz über die Azure-Befehlszeilenschnittstelle

1. Öffnen Sie eine Eingabeaufforderung.

1. Melden Sie sich bei Ihrem Azure-Konto an:
   ```azurecli
   az login
   ```

1. Wählen Sie Ihr Azure-Abonnement aus:
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. Erstellen Sie eine Ressourcengruppe für die in diesem Tutorial verwendeten Azure-Ressourcen.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Erstellen Sie eine private Azure Container Registry-Instanz in der Ressourcengruppe. Die Beispiel-App wird in diesem Tutorial in späteren Schritten als Docker-Image per Push in diese Registrierung übertragen. Ersetzen Sie `wingtiptoysregistry` durch einen eindeutigen Namen für die Registrierung.
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a>Pushen der App in die Containerregistrierung über Jib

1. Melden Sie sich über die Azure-Befehlszeilenschnittstelle bei Ihrer Azure Container Registry-Instanz an.
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung (z.B.„*C:\SpringBoot\gs-spring-boot-docker\complete*“ oder „*/users/robert/SpringBoot/gs-spring-boot-docker/complete*“), und öffnen Sie die Datei *pom.xml* mit einem Text-Editor.

1. Aktualisieren Sie die Sammlung `<properties>` in der Datei *pom.xml* mit dem Registrierungsnamen für Ihre Azure Container Registry-Instanz und der aktuellen Version von [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.0.2</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Aktualisieren Sie die Sammlung `<plugins>` in der Datei *pom.xml* so, dass `<plugin>` das Element `jib-maven-plugin` enthält.

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>              
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>                
            <image>${docker.image.prefix}/${project.artifactId}</image>
        </to>
     </configuration>
   </plugin>
   ```

1. Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Befehl aus, um das Image zu erstellen und per Push in die Registrierung zu übertragen:

   ```
   mvn compile jib:build
   ```

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a>Erstellen eines Kubernetes-Clusters in AKS über die Azure-Befehlszeilenschnittstelle

1. Erstellen Sie einen Kubernetes-Cluster in Azure Kubernetes Service. Mit dem folgenden Befehl wird ein *Kubernetes*-Cluster in der Ressourcengruppe *wingtiptoys-kubernetes* mit *wingtiptoys-akscluster* als Clustername und *wingtiptoys-kubernetes* als DNS-Präfix erstellt:
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   Die Ausführung des Befehls kann eine Weile dauern.

1. Wenn Sie Azure Container Registry (ACR) zusammen mit Azure Kubernetes Service (AKS) verwenden, müssen Sie Azure Kubernetes Service Pullzugriff auf Azure Container Registry gewähren. Azure generiert beim Erstellen einer Azure Kubernetes Service-Instanz einen Standarddienstprinzipal. Führen Sie die folgenden Skripts in Bash oder Powershell aus, um AKS Zugriff auf ACR zu gewähren. Ausführlichere Informationen finden Sie unter [Authentifizieren per Azure Container Registry über Azure Kubernetes Service].

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  – oder –

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. Installieren Sie `kubectl` über die Azure-Befehlszeilenschnittstelle. Linux-Benutzer müssen diesem Befehl möglicherweise das Präfix `sudo` voranstellen, da er die Kubernetes-Befehlszeilenschnittstelle in `/usr/local/bin` bereitstellt.
   ```azurecli
   az aks install-cli
   ```

1. Laden Sie die Konfigurationsinformationen des Clusters herunter, damit Sie den Cluster über die Kubernetes-Weboberfläche und `kubectl` verwalten können. 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a>Bereitstellen des Images in Ihrem Kubernetes-Cluster

In diesem Tutorial wird die App mit `kubectl` bereitgestellt, dann können Sie die Bereitstellung über die Kubernetes-Weboberfläche erkunden.

### <a name="deploy-with-kubectl"></a>Bereitstellen mit kubectl

1. Öffnen Sie eine Eingabeaufforderung.

1. Führen Sie den Container im Kubernetes-Cluster mit dem Befehl `kubectl run` aus. Geben Sie einen Dienstnamen für die App in Kubernetes und den vollständigen Imagenamen an. Beispiel: 
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   In diesem Befehl:

   * Der Containername `gs-spring-boot-docker` wird direkt nach dem Befehl `run` angegeben.

   * Der Parameter `--image` gibt die Kombination aus Anmeldeserver und Imagename als `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest` an.

1. Machen Sie den Kubernetes-Cluster mit dem Befehl `kubectl expose` extern verfügbar. Geben Sie den Dienstnamen, den öffentlichen TCP-Port für den Zugriff auf die App und den internen Zielport, auf dem die App lauscht, an. Beispiel: 
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   In diesem Befehl:

   * Der Containername `gs-spring-boot-docker` wird direkt nach dem Befehl `expose deployment` angegeben.

   * Der Parameter `--type` gibt an, dass der Cluster einen Lastenausgleich verwendet.

   * Der Parameter `--port` gibt den öffentlichen TCP-Port 80 an. Sie greifen über diesen Port auf die App zu.

   * Der Parameter `--target-port` gibt den internen TCP-Port 8080 an. Der Load Balancer leitet über diesen Port Anforderungen an die App weiter.

1. Nachdem die App im Cluster bereitgestellt wurde, fragen Sie die externe IP-Adresse ab, und öffnen Sie sie im Webbrowser:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Navigieren zur Beispiel-App in Azure][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a>Bereitstellen über die Kubernetes-Weboberfläche

1. Öffnen Sie eine Eingabeaufforderung.

1. Öffnen Sie die Konfigurationswebsite für Ihren Kubernetes-Cluster im Standardbrowser:
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. Nachdem die Kubernetes-Konfigurationswebsite im Browser geöffnet wurde, klicken Sie auf den Link zum **Bereitstellen einer Container-App**:

   ![Kubernetes-Konfigurationswebsite][KB01]

1. Geben Sie auf der angezeigten Seite für die **Ressourcenerstellung** die folgenden Optionen an:

   a. Wählen Sie **APP ERSTELLEN** aus.

   b. Geben Sie unter **App name** (App-Name) den Namen der Spring Boot-Anwendung ein, z.B. *gs-spring-boot-docker*.

   c. Geben Sie unter **Container image** (Containerimage) die weiter oben verwendeten Werte für den Anmeldeserver und das Containerimage ein, z.B. *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*.

   d. Wählen Sie **External** (Extern) für **Service** (Dienst) aus.

   e. Geben Sie in den Textfeldern **Port** und **Target port** (Zielport) den externen und internen Port an.

   ![Kubernetes-Konfigurationswebsite][KB02]


1. Klicken Sie auf **Deploy** (Bereitstellen), um den Container bereitzustellen.

   ![Kubernetes-Schaltfläche „Deploy“][KB05]

1. Nach erfolgter Bereitstellung wird die Spring Boot-Anwendung unter **Services** (Dienste) angezeigt.

   ![Kubernetes-Dienste][KB06]

1. Wenn Sie auf den Link für **External endpoints** (Externe Endpunkte) klicken, können Sie die in Azure ausgeführte Spring Boot-Anwendung sehen.

   ![Kubernetes-Dienste][KB07]

   ![Navigieren zur Beispiel-App in Azure][SB02]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.

> [!div class="nextstepaction"]
> [Spring Framework in Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Weitere Ressourcen

Weitere Informationen zur Verwendung von Spring Boot in Azure finden Sie im folgenden Artikel:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).

Weitere Informationen zum Bereitstellen einer Java-Anwendung in Kubernetes mit Visual Studio Code finden Sie in den [Visual Studio Code-Tutorials für Java].

Weitere Informationen zum Spring Boot-Beispielprojekt in Docker finden Sie unter [Spring Boot on Docker Getting Started] (Erste Schritte mit Spring Boot in Docker).

Über die folgenden Links erhalten Sie weitere Informationen zur Erstellung von Spring Boot-Anwendungen:

* Weitere Informationen zum Erstellen einer einfachen Spring Boot-Anwendung finden Sie im Spring Initializr unter https://start.spring.io/.

Über die folgenden Links erhalten Sie weitere Informationen zur Verwendung von Kubernetes mit Azure:

* [Erste Schritte mit einem Kubernetes-Cluster in Azure Kubernetes Service](/azure/aks/intro-kubernetes)

Weitere Informationen zur Verwendung der Kubernetes-Befehlszeilenschnittstelle stehen im Benutzerhandbuch für **kubectl** unter <https://kubernetes.io/docs/user-guide/kubectl/> zur Verfügung.

Die Kubernetes-Website umfasst mehrere Artikel zur Verwendung von Images in privaten Registrierungen:

* [Configuring Service Accounts for Pods] (Konfigurieren von Dienstkonten für Pods)
* [Namespaces]
* [Pulling an Image from a Private Registry] (Übertragen eines Images aus einer privaten Registrierung per Pull)

Weitere Beispiele zur Vorgehensweise bei der Verwendung benutzerdefinierter Docker-Images mit Azure finden Sie unter [Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux].

Weitere Informationen zum iterativen Ausführen und Debuggen von Containern mit Azure Dev Spaces direkt in Azure Kubernetes Service (AKS) finden Sie unter [Erste Schritte in Azure Dev Spaces mit Java].

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure für Java-Entwickler]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Arbeiten mit Azure DevOps und Java)
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Konfigurieren von Dienstkonten für Pods)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Übertragen eines Images aus einer privaten Registrierung per Pull)

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[Authentifizieren per Azure Container Registry über Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Visual Studio Code-Tutorials für Java]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Erste Schritte in Azure Dev Spaces mit Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
