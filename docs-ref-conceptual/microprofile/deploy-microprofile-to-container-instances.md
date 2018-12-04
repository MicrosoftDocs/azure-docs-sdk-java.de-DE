---
title: Bereitstellen einer MicroProfile-App in der Cloud mit Docker und Azure
description: Hier erfahren Sie, wie Sie eine MicroProfile-App unter Verwendung von Docker und Azure Container Instances in der Cloud bereitstellen.
services: container-instances;container-retistry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 22870b7ba32f115e7270c63d1bf42cbfc6531d7e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338784"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a>Bereitstellen einer MicroProfile-Anwendung in der Cloud mit Docker und Azure

In diesem Artikel wird gezeigt, wie Sie eine Anwendung vom Typ [MicroProfile.io] in einen Docker-Container packen und in Azure Container Instances ausführen.

> [!NOTE]
>
> Dieses Verfahren kann für jede Implementierung von „MicroProfile.io“ verwendet werden, solange das Docker-Containerimage selbstausführbar ist (sprich: die Runtime enthält).

## <a name="prerequisites"></a>Voraussetzungen

Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:

* Ein Azure-Abonnement. Sollten Sie noch nicht über ein Azure-Abonnement verfügen, können Sie sich für ein [kostenloses Azure-Konto] registrieren.
* Die [Azure-Befehlszeilenschnittstelle (CLI)]
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* Das Erstellungstool [Maven] von Apache (ab Version 3)
* Einen [Git]

## <a name="microprofile-hello-azure-sample"></a>Beispiel „MicroProfile Hello Azure“

In diesem Artikel verwenden wir das Beispiel [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure):

### <a name="clone-build-and-run-locally"></a>Klonen, Erstellen und lokales Ausführen

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

Sie können die Anwendung testen, indem Sie `curl` aufrufen oder sie über einen [Browser](http://localhost:8080/api/hello) öffnen:

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a>Bereitstellen in Azure

Als Nächstes bringen wir die Anwendung mithilfe der Dienste [Azure Container Instances] und [Azure Container Registry] in die Cloud.

### <a name="build-a-docker-image"></a>Erstellen eines Docker-Images

Das Beispielprojekt stellt bereits eine Dockerfile bereit, die Sie verwenden können. Docker muss jedoch nicht installiert sein, da wir das Azure Container Registry Build-Feature verwenden, um das Image in der Cloud zu erstellen.

Führen Sie die folgenden Schritte aus, um das Image zu erstellen und für die Ausführung in Azure vorzubereiten:

1. Installieren und Anmelden mit der Azure-Befehlszeilenschnittstelle
1. Erstellen einer Azure-Ressourcengruppe
1. Erstellen einer ACR-Instanz (Azure Container Registry)
1. Erstellen des Docker-Images
1. Veröffentlichen des Docker-Images in der zuvor erstellten ACR-Instanz
1. (Optional) Erstellen und Veröffentlichen in ACR mit nur einem Befehl


#### <a name="set-up-azure-cli"></a>Einrichten der Azure-Befehlszeilenschnittstelle

Stellen Sie sicher, dass Sie über ein Azure-Abonnement verfügen, dass die [Azure-Befehlszeilenschnittstelle installiert](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) ist und dass Sie bei Ihrem Konto authentifiziert sind:

```bash
az login
```

#### <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a>Erstellen einer Azure Container Registry-Instanz

Dieser Befehl erstellt eine (hoffentlich) global eindeutige Containerregistrierung mit einem einfachen Namen und einer Zufallszahl.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Erstellen des Docker-Images

Sie können das Docker-Image zwar ganz einfach mithilfe von Docker lokal erstellen, es gibt jedoch einige Gründe, die für eine Erstellung in der Cloud sprechen:

1. Keine lokale Docker-Installation erforderlich
1. Viel schneller, da der Buildvorgang anderswo ausgeführt wird (mit Ausnahme der Uploadzeit für den Kontext)
1. Schnellere Downloads, da der Prozess in der Cloud Zugriff auf eine schnellere Internetverbindung hat
1. Direktes Hinzufügen von Images zu Container Registry

Aus diesen Gründen erstellen wir das Image mithilfe des Features [Azure Container Registry Build]:

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a>Bereitstellen des Docker-Images über Azure Container Registry in Container Instances (ACI)

Das Image ist nun in Ihrer ACR-Instanz verfügbar ist. Als Nächstes übertragen wir eine Containerinstanz per Push an ACI und instanziieren sie. Zuvor müssen wir jedoch sicherstellen, dass die Authentifizierung in ACR möglich ist:

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Testen der bereitgestellten MicroProfile-Anwendung

Ihre Anwendung sollte nun betriebsbereit sein. Führen Sie an der Befehlszeile den folgenden Befehl aus, um sie zu testen:

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Glückwunsch! Sie haben erfolgreich eine MicroProfile-Anwendung erstellt und als Docker-Container in Microsoft Azure bereitgestellt.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:

* [Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry