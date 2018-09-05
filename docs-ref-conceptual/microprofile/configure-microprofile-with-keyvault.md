---
title: Konfigurieren von MicroProfile mit Azure Key Vault
description: Hier erfahren Sie, wie Sie Geheimnisse in einen MicroProfile-Webdienst mit Azure Key Vault einfügen.
services: key-vault
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: fa93788f9b600d963f35ea599a58d309d3a3ee52
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240823"
---
# <a name="configure-microprofile-with-azure-key-vault"></a>Konfigurieren von MicroProfile mit Azure Key Vault

Dieses Tutorial zeigt, wie Sie eine [MicroProfile](http://microprofile.io)-Anwendung für den Abruf von Geheimnissen aus [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) konfigurieren und dabei die [MicroProfile-Konfigurations-APIs](https://microprofile.io/project/eclipse/microprofile-config) verwenden, um eine direkte Verbindung mit Azure Key Vault herzustellen. Die MicroProfile-Konfigurations-APIs bieten Entwicklern eine Standard-API zum Abrufen und Einfügen von Konfigurationsdaten für ihre Microservices.

Bevor wir in die Details gehen, sehen wir uns zunächst kurz an, was wir in unserem Code schreiben können, wenn wir Azure Key Vault und die MicroProfile-Konfigurations-API miteinander kombinieren. Hier sehen Sie einen Codeausschnitt für ein Feld in einer Klasse mit den Anmerkungen `@Inject` und `@ConfigProperty`. Der in den Anmerkungen angegebene Name (`name`) ist der Name der Eigenschaft, die in Azure Key Vault gesucht werden soll, und `defaultValue` ist der Wert, der festgelegt wird, wenn der Schlüssel nicht ermittelt werden kann. Dadurch wird zur Laufzeit entweder der in Azure Key Vault gespeicherte Wert oder der Standardwert automatisch in das Feld eingefügt. Entwickler müssen somit keine Werte mehr in Konstruktoren und Setter-Methoden übergeben, sondern können die Behandlung MicroProfile überlassen.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

Auf die MicroProfile-Konfiguration kann auch direkt zugegriffen werden, um Geheimnisse nach Bedarf anzufordern. Beispiel:

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

In diesem Beispiel wird unter Verwendung von [Payara Micro](https://www.payara.fish/payara_micro) und [MicroProfile](https://microprofile.io/) eine kleine Java-WAR-Datei erstellt, die lokal auf Ihrem Computer ausgeführt werden kann. Es zeigt nicht, wie der Code in Docker verpackt oder an Azure gepusht wird. Am Ende dieses Tutorials befindet sich jedoch ein Abschnitt mit Links zu weiteren hilfreichen Tutorials, in denen dieser Punkt erläutert wird.

In diesem Beispiel wird eine kostenlose Open-Source-Bibliothek verwendet, die (unter Verwendung der MicroProfile-Konfigurations-API) eine Konfigurationsquelle für Azure Key Vault erstellt. Weitere Informationen zu dieser Bibliothek sowie den Code finden Sie auf der [GitHub-Projektseite](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). Durch die Verwendung dieser Bibliothek können wir uns beim Code in diesem Tutorial einfach auf die Konfiguration der Bibliothek sowie auf das Einfügen von Schlüsseln in den Code konzentrieren und müssen keinerlei Azure-spezifischen Code schreiben.

Im Anschluss erfahren Sie, wie Sie diesen Code auf Ihrem lokalen Computer ausführen. Dabei erstellen Sie zunächst eine Azure Key Vault-Ressource.

## <a name="creating-an-azure-key-vault-resource"></a>Erstellen einer Azure Key Vault-Ressource

Wir verwenden die Azure-Befehlszeilenschnittstelle, um die Azure Key Vault-Ressource zu erstellen und mit einem einzelnen Geheimnis zu füllen.

1. Als Erstes erstellen wir einen Azure-Dienstprinzipal. Dadurch erhalten wir die Client-ID und den Schlüssel für den Zugriff auf Key Vault:

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

Angenommen, wir verwenden im vorherigen Schritt `microprofile-keyvault-service-principal` als Dienstprinzipalname. In diesem Fall sieht die (leicht verschleierte) Antwort von Azure wie folgt aus:

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

Von besonderem Interesse sind hier die Werte `appID` und `password`: Diese werden später für `client ID` und `key` benötigt.

Nach der Erstellung des Dienstprinzipals können wir optional eine Ressourcengruppe erstellen. (Falls Sie bereits über eine Ressourcengruppe verfügen, die Sie verwenden möchten, können Sie diesen Schritt überspringen.) Sie können eine Liste mit Ressourcengruppenstandorten abrufen. Rufen Sie hierzu `az account list-locations` auf, und verwenden Sie den Wert `name` aus dieser Liste, um anzugeben, wo die Ressourcengruppe erstellt werden soll.

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

Als Nächstes erstellen wir eine Azure Key Vault-Ressource. Der Key Vault-Name sollte gut zu merken sein, da Sie später anhand dieses Namens auf den Schlüsseltresor verweisen.

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

Darüber hinaus müssen wir dem zuvor erstellten Dienstprinzipal die erforderlichen Berechtigungen für den Zugriff auf die Key Vault-Geheimnisse gewähren. Hinweis: Der appID-Wert ist der Wert `appId` aus der Dienstprinzipalerstellung von weiter oben (also `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79`; verwenden Sie aber den Wert aus Ihrer Terminalausgabe).

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

Als Nächstes können wir ein Geheimnis an Key Vault pushen. In diesem Beispiel verwenden wir den Schlüsselnamen `demo-key` und legen den Wert des Schlüssels auf `demo-value` fest:

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

Das ist alles! Key Vault wird nun mit einem einzelnen Geheimnis in Azure ausgeführt. Als Nächstes können wir dieses Repository klonen und für die Verwendung dieser Ressource in unserer App konfigurieren.

## <a name="getting-up-and-running-locally"></a>Einrichten und Ausführen in der lokalen Umgebung

Dieses Beispiel basiert auf einer auf GitHub verfügbaren Beispielanwendung, deren Code wir hier klonen und Schritt für Schritt durchgehen. Gehen Sie wie folgt vor, um den Code auf Ihrem Computer zu klonen:

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. Navigieren Sie zu `src/main/resources/META-INF/microprofile-config.properties`, und aktualisieren Sie die Eigenschaften in der Datei „microprofile-config.properties“ mit den obigen Details.

1. Führen Sie den Server mit `mvn clean package payara-micro:start` aus.

1. Greifen Sie in Ihrem Webbrowser auf [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) zu. Daraufhin sollte eine einfache Antwort angezeigt werden, die deutlich macht, dass Werte aus Azure Key Vault gelesen werden.

## <a name="summary"></a>Zusammenfassung

Diese Beispielanwendung kombiniert die MicroProfile-Konfigurations-API mit Azure Key Vault und der kostenlosen Open-Source-Bibliothek [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault), um das Einfügen von Konfigurationsdaten und Geheimnissen in MicroProfile-Webdienste zu vereinfachen.
