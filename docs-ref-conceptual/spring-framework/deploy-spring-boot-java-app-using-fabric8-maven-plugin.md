---
title: Bereitstellen einer Spring Boot-App unter Verwendung des Fabric8 Maven-Plug-Ins
description: In diesem Tutorial werden die Schritte zum Bereitstellen einer Spring Boot-Anwendung in Microsoft Azure mit dem Fabric8-Plug-In für Apache Maven erläutert.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: yuwzho;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: f05dca50f84b27f157892d63cda02286c6755795
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090813"
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a>Bereitstellen einer Spring Boot-App unter Verwendung des Fabric8 Maven-Plug-Ins

**[Fabric8]**  ist eine Open-Source-Lösung, die auf **[Kubernetes]** basiert und Entwicklern beim Erstellen von Anwendungen in Linux-Containern hilft.

In diesem Tutorial wird die Verwendung des Fabric8-Plug-Ins für Maven zur Entwicklung und Bereitstellung einer Anwendung auf einem Linux-Host in [Azure Container Service (AKS)] erläutert.

## <a name="prerequisites"></a>Voraussetzungen

Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
* Die [Azure-Befehlszeilenschnittstelle (CLI)]
* Ein aktuelles [Java Developer Kit (JDK)]
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
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   – oder –
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. Klonen Sie das Beispielprojekt [Spring Boot on Docker Getting Started] in das Verzeichnis.
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   – oder –
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. Verwenden Sie Maven zum Erstellen und Ausführen der Beispiel-App.
   ```shell
   mvn clean package spring-boot:run
   ```

1. Testen Sie die Web-App durch Navigieren zu http://localhost:8080 oder mit dem folgenden `curl`-Befehl:
   ```shell
   curl http://localhost:8080
   ```

   Es sollte die Meldung **Hello Docker World** angezeigt werden.

   ![Lokales Durchsuchen der Beispielanwendung][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a>Installieren der Kubernetes-Befehlszeilenschnittstelle und Erstellen einer Azure-Ressourcengruppe mithilfe der Azure CLI

1. Öffnen Sie eine Eingabeaufforderung.

1. Melden Sie sich mithilfe des folgenden Befehls bei Ihrem Azure-Konto an:
   ```azurecli
   az login
   ```
   Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.

   Die Azure CLI zeigt eine Liste Ihrer Konten an, Beispiel:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. Wenn Sie die Kubernetes-Befehlszeilenschnittstelle (`kubectl`) noch nicht installiert haben, können Sie sie mithilfe der Azure CLI installieren, Beispiel:
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > Linux-Benutzer müssen diesem Befehl möglicherweise das Präfix `sudo` voranstellen, da er die Kubernetes-Befehlszeilenschnittstelle in `/usr/local/bin` bereitstellt.
   >
   > Falls Sie `kubectl` bereits installiert haben und Ihre Version von `kubectl` zu alt ist, wird möglicherweise eine Fehlermeldung wie die im folgenden Beispiel angezeigt, wenn Sie versuchen, die weiter unten in diesem Artikel beschriebenen Schritte auszuführen:
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > In diesem Fall müssen Sie `kubectl` erneut installieren, um Ihre Version zu aktualisieren.
   >

1. Erstellen Sie eine Ressourcengruppe für die Azure-Ressourcen, die Sie in diesem Tutorial verwenden, Beispiel:
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   Hinweis:  
      * *wingtiptoys-kubernetes* ist ein eindeutiger Name für Ihre Ressourcengruppe.  
      * *westeurope* ist ein geeigneter geografischer Ort für Ihre Anwendung.  

   Die Azure CLI zeigt die Ergebnisse der Erstellung Ihrer Ressourcengruppe an, Beispiel:  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a>Erstellen eines Kubernetes-Clusters mit der Azure CLI

1. Erstellen Sie einen Kubernetes-Cluster in Ihrer neuen Ressourcengruppe, Beispiel:  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   Hinweis:  
      * *wingtiptoys-kubernetes* ist der Name Ihrer Ressourcengruppe von weiter oben in diesem Artikel.  
      * *wingtiptoys-cluster* ist ein eindeutiger Name für Ihren Kubernetes-Cluster.
      * *wingtiptoys* ist ein eindeutiger DNS-Name für Ihre Anwendung.

   Die Azure CLI zeigt die Ergebnisse der Erstellung Ihres Clusters an, Beispiel:  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. Laden Sie Ihre Anmeldeinformationen für den neuen Kubernetes-Cluster herunter, Beispiel:  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. Überprüfen Sie die Verbindung mit dem folgenden Befehl:
   ```shell 
   kubectl get nodes
   ```

   Daraufhin sollte eine Liste von Knoten und Statusangaben angezeigt werden, wie im folgenden Beispiel dargestellt:

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a>Erstellen einer privaten Azure-Containerregistrierung mit der Azure CLI

1. Erstellen Sie eine private Azure-Containerregistrierung in der Ressourcengruppe, um Ihr Docker-Image zu hosten, Beispiel:
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `wingtiptoys-kubernetes` | Gibt den Namen Ihrer Ressourcengruppe von weiter oben in diesem Artikel an. |
   | `wingtiptoysregistry` | Gibt einen eindeutigen Namen für die private Registrierung an. |
   | `westeurope` | Gibt einen geeigneten geografischen Ort für Ihre Anwendung an. |

   Die Azure CLI zeigt die Ergebnisse der Erstellung Ihrer Registrierung an, Beispiel:  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

2. Rufen Sie das Kennwort für Ihre Containerregistrierung über die Azure-Befehlszeilenschnittstelle ab.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   Die Azure CLI zeigt das Kennwort Ihrer Registrierung an, Beispiel:  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

3. Navigieren Sie zu dem Konfigurationsverzeichnis Ihrer Maven-Installation (Standard: „~/.m2/“ oder „C:\Users\username\.m2“), und öffnen Sie die Datei *settings.xml* mit einem Text-Editor.

4. Fügen Sie die URL, den Benutzernamen und das Kennwort für Azure Container Registry einer neuen `<server>`-Sammlung in der Datei *settings.xml* hinzu.
   `id` und `username` bilden den Namen der Registrierung. Verwenden Sie den `password`-Wert des vorherigen Befehls (ohne Anführungszeichen).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

5. Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung (z.B. *C:\SpringBoot\gs-spring-boot-docker\complete* oder */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*), und öffnen Sie die Datei *pom.xml* mit einem Text-Editor.

6. Aktualisieren Sie die `<properties>`-Sammlung in der Datei *pom.xml* mit dem Wert des Anmeldeservers für Ihre Azure Container Registry-Instanz.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

7. Aktualisieren Sie die `<plugins>`-Sammlung in der Datei *pom.xml* so, dass `<plugin>` die Adresse des Anmeldeservers und den Registrierungsnamen für Ihre Azure Container Registry-Instanz enthält.

   ```xml
   <plugin>
     <groupId>com.spotify</groupId>
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

8. Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung, und führen Sie den folgenden Maven-Befehl aus, um den Docker-Container zu erstellen und das Image per Push in die Registrierung zu übertragen:

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   Maven zeigt die Ergebnisse des Builds an, Beispiel:  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a>Konfigurieren der Spring Boot-App für die Verwendung des Fabric8 Maven-Plug-Ins

1. Navigieren Sie zum Verzeichnis des abgeschlossenen Projekts für Ihre Spring Boot-Anwendung (z.B. *C:\SpringBoot\gs-spring-boot-docker\complete* oder */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*), und öffnen Sie die Datei *pom.xml* mit einem Text-Editor.

1. Aktualisieren Sie die `<plugins>`-Sammlung in der Datei *pom.xml*, um das Fabric8 Maven-Plug-In hinzuzufügen:

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. Navigieren Sie zum Hauptquellverzeichnis für Ihre Spring Boot-Anwendung (z.B. *C:\SpringBoot\gs-spring-boot-docker\complete\src\main* oder */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*), und erstellen Sie einen neuen Ordner namens *fabric8*.

1. Erstellen Sie drei YAML-Fragmentdateien im neuen Ordner *fabric8*:

   a. Erstellen Sie eine Datei namens **deployment.yml** mit folgendem Inhalt:
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   b. Erstellen Sie eine Datei namens **secrets.yml** mit folgendem Inhalt:
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   c. Erstellen Sie eine Datei namens **service.yml** mit folgendem Inhalt:
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. Führen Sie den folgenden Maven-Befehl aus, um die Kubernetes-Ressourcenlistendatei zu erstellen:

   ```shell
   mvn fabric8:resource
   ```

   Dieser Befehl führt alle Kubernetes-YAML-Ressourcendateien im Ordner *src/main/fabric8* in einer YAML-Datei zusammen, die eine Kubernetes-Ressourcenliste enthält, die direkt auf einen Kubernetes-Cluster angewendet oder in ein Helm-Diagramm exportiert werden kann.

   Maven zeigt die Ergebnisse des Builds an, Beispiel:  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. Führen Sie den folgenden Maven-Befehl aus, um die Ressourcenlistendatei auf den Kubernetes-Cluster anzuwenden:

   ```shell
   mvn fabric8:apply
   ```

   Maven zeigt die Ergebnisse des Builds an, Beispiel:  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. Nachdem die App im Cluster bereitgestellt wurde, fragen Sie die externe IP-Adresse mit der `kubectl`-Anwendung ab, Beispiel:
   ```shell
   kubectl get svc -w
   ```

   `kubectl` zeigt die internen und externen IP-Adressen an, Beispiel:

   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```

   Sie können die externe IP-Adresse verwenden, um Ihre Anwendung in einem Webbrowser zu öffnen.

   ![Externes Durchsuchen der Beispielanwendung][SB02]

## <a name="delete-your-kubernetes-cluster"></a>Löschen Ihres Kubernetes-Clusters

Wenn der Kubernetes-Cluster nicht mehr benötigt wird, können Sie den Befehl `az group delete` verwenden, um die Ressourcengruppe zu entfernen. Dadurch werden auch alle zugehörigen Ressourcen entfernt, Beispiel:

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)
* [Bereitstellen einer Spring Boot-Anwendung unter Linux in Azure Container Service](deploy-spring-boot-java-app-on-linux.md)
* [Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md) (Bereitstellen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service)

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

Weitere Informationen zum Spring Boot-Beispielprojekt in Docker finden Sie unter [Spring Boot on Docker Getting Started].

Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie bei **Spring Initializr** unter <https://start.spring.io/>.

Weitere Informationen zu den ersten Schritten beim Erstellen einer einfachen Spring Boot-Anwendung finden Sie bei Spring Initializr unter <https://start.spring.io/>.

Weitere Beispiele zur Vorgehensweise bei der Verwendung benutzerdefinierter Docker-Images mit Azure finden Sie unter [Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux].

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Verwenden eines benutzerdefinierten Docker-Images für Azure-Web-Apps unter Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Erste Schritte mit Spring Boot in Docker)
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
