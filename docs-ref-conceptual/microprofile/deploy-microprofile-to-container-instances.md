---
title: Bereitstellen einer MicroProfile-App in der Cloud über Docker und Azure
description: Hier erfahren Sie, wie Sie eine MicroProfile-App in der Cloud bereitstellen, indem Sie Docker und Azure Container Instances verwenden.
services: container-instances;container-registry
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
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533602"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a>Bereitstellen einer MicroProfile-App in der Cloud über Docker und Azure

In diesem Artikel wird gezeigt, wie Sie eine Anwendung vom Typ [MicroProfile.io] in einen Docker-Container packen und in Azure Container Instances ausführen.

> [!NOTE]
> Dieses Verfahren kann für jede Implementierung von „MicroProfile.io“ verwendet werden, solange das Docker-Containerimage selbstausführbar ist (d. h., das Image enthält die Runtime).

## <a name="prerequisites"></a>Voraussetzungen

Zum Durchführen dieses Tutorials benötigen Sie Folgendes:

* Ein Azure-Abonnement. Wenn Sie noch kein Azure-Abonnement haben, können Sie sich für ein [kostenloses Azure-Konto] anmelden.
* Die [Azure-Befehlszeilenschnittstelle] muss installiert sein.
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den JDKs, die verfügbar sind, wenn Sie in Azure entwickeln, finden Sie unter [Langfristiger Java-Support für Azure und Azure Stack](https://aka.ms/azure-jdks).
* Das [Apache Maven]-Buildtool (Version 3 oder höher).
* Einen [Git-Client]

## <a name="microprofile-hello-azure-sample"></a>Beispiel „MicroProfile Hello Azure“

In diesem Artikel verwenden Sie das Beispiel [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure). Verwenden Sie die folgenden Befehle, um das Beispiel lokal zu klonen, zu erstellen und auszuführen:

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

Sie können die Anwendung testen, indem Sie `curl` aufrufen oder einen [Browser](http://localhost:8080/api/hello) verwenden:

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a>Bereitstellen der Anwendung in Azure

Platzieren Sie die Anwendung nun in Azure, indem Sie die Dienste [Azure Container Instances] und [Azure Container Registry] verwenden.

### <a name="build-a-docker-image"></a>Erstellen eines Docker-Images

Das Beispielprojekt stellt ein Dockerfile bereit, das Sie verwenden können. Docker muss jedoch nicht installiert sein, weil Sie das Azure Container Registry Build-Feature verwenden, um das Image in der Cloud zu erstellen.

Gehen Sie wie folgt vor, um das Image zu erstellen und so vorzubereiten, dass es in Azure ausgeführt werden kann:

1. Installieren Sie die Azure CLI, und melden Sie sich bei der Azure CLI an.
1. Erstellen einer Azure-Ressourcengruppe.
1. Erstellen Sie eine Azure Container Registry-Instanz.
1. Erstellen Sie ein Docker-Image.
1. Veröffentlichen Sie das Docker-Image in der zuvor erstellten Container Registry-Instanz.
1. (Optional) Erstellen und veröffentlichen Sie das Image in der Container-Registry-Instanz in einem einzigen Befehl.


#### <a name="set-up-the-azure-cli"></a>Einrichten der Azure CLI

Stellen Sie sicher, dass Sie ein Azure-Abonnement haben, dass Sie [die Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) installiert haben und dass Sie bei Ihrem Konto authentifiziert sind:

```bash
az login
```

#### <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a>Erstellen einer Container Registry-Instanz

Dieser Befehl sollte eine global eindeutige Container Registry-Instanz mit einem Basisnamen und einer Zufallszahl erstellen.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Erstellen des Docker-Images

Obwohl Sie das Docker-Image ganz einfach lokal erstellen können, indem Sie Docker selbst verwenden, gibt es einige Gründe, die für eine Erstellung des Images in der Cloud sprechen:

* Sie müssen Docker nicht lokal installieren.
* Es ist viel schneller, weil der Buildvorgang anderswo ausgeführt wird (mit Ausnahme der Uploadzeit für den Kontext).
* Der Prozess in der Cloud hat schnelleren Zugriff auf das Internet und somit schnellere Downloads.
* Das Image wird direkt in der Container Registry-Instanz hinzugefügt.

Aus diesen Gründen erstellen Sie das Image über das Feature [Azure Container Registry Build]:

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a>Bereitstellen des Docker-Images aus der Azure Container Registry-Instanz in Container Instances

Nachdem das Image nun in Ihrer Container-Registry-Instanz verfügbar ist, senden Sie eine Containerinstanz an Container Instances, und instanziieren Sie die Instanz dort. Zunächst müssen Sie aber sicherstellen, dass Sie sich für die Container Registry-Instanz authentifizieren können:

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Testen Ihrer bereitgestellten MicroProfile-Anwendung

Ihre Anwendung sollte nun betriebsbereit sein. Um sie aus der Befehlszeilenschnittstelle zu testen, verwenden Sie den folgenden Befehl:

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Glückwunsch! Sie haben erfolgreich eine MicroProfile-Anwendung als Docker-Container erstellt und in Azure bereitgestellt.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie hier:

* [Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure-Befehlszeilenschnittstelle]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Git-Client]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
