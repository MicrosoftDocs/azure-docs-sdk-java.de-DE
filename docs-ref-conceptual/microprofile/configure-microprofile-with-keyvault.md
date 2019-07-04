---
title: Konfigurieren von MicroProfile über Azure Key Vault
description: Hier erfahren Sie, wie Sie Geheimnisse in einen MicroProfile-Webdienst einfügen, indem Sie Azure Key Vault verwenden.
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
ms.openlocfilehash: c405711813176823f2ddee6b4002f75c2b25fdb5
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533612"
---
# <a name="configure-microprofile-by-using-azure-key-vault"></a>Konfigurieren von MicroProfile über Azure Key Vault

In diesem Artikel wird veranschaulicht, wie eine [MicroProfile](http://microprofile.io)-Anwendung zu konfigurieren ist, um Geheimnisse aus einer [Azure Key Vault-Instanz](https://azure.microsoft.com/services/key-vault/) (Azure-Schlüsseltresor) abzurufen. In diesem Prozess verwenden Sie die [MicroProfile Config-APIs](https://microprofile.io/project/eclipse/microprofile-config), um eine direkte Verbindung mit einem Azure-Schlüsseltresor herzuerstellen. Als Entwickler profitieren Sie, wenn Sie die MicroProfile Config-APIs verwenden, von einer Standard-API zum Abrufen und Einfügen von Konfigurationsdaten für ihre Microservices.

Bevor Sie beginnen, sollten Sie sich kurz ansehen, was Sie in Ihrem Code schreiben können, wenn Sie Azure Key Vault und die MicroProfile Config-API kombinieren. Der folgende Codeausschnitt gehört zu einem Feld in einer Klasse, die die Annotationen `@Inject` und `@ConfigProperty` hat. Der in der Annotation angegebene Name (*name*) ist der Name der Eigenschaft, nach dem in Ihrem Schlüsseltresor gesucht werden soll, und *defaultValue* ist der Wert, auf den der Name festgelegt wird, wenn der Schlüssel nicht festgestellt werden kann. Das Ergebnis ist, dass der im Schlüsseltresor gespeicherte Wert oder der Standardwert zur Laufzeit automatisch in das Feld eingefügt wird. Diese Vorgehensweise kann Ihnen das Programmieren vereinfachen, weil Sie keine Werte mehr in Konstruktoren und Setter-Methoden übergeben müssen. Stattdessen erledigt MicroProfile diese Aufgabe.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

Um Geheimnisse nach Bedarf anzufordern, können Sie auch direkt auf die MicroProfile-Konfiguration zugreifen. Beispiel:

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

In diesem Beispiel werden [Payara Micro](https://www.payara.fish/payara_micro) und [MicroProfile](https://microprofile.io/) verwendet, um eine kleine Java-WAR-Datei (Web Application Requirement) zu erstellen, die Sie lokal auf Ihrem Computer ausführen können. Im Beispiel wird nicht gezeigt, wie der Code in Docker verpackt oder an Azure gepusht wird, aber am Ende dieses Artikels finden Sie Links zu weiteren nützlichen Tutorials, in denen dieser Punkt erläutert wird.

In diesem Beispiel wird eine kostenlose Open-Source-Bibliothek verwendet, über die (mit der MicroProfile Config-API) eine Konfigurationsquelle in Ihrem Schlüsseltresor erstellt wird. Wenn Sie weitere Informationen zu dieser Bibliothek wünschen und sich den Code ansehen möchten, lesen Sie die [GitHub-Projektseite](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). Wenn Sie die Bibliothek verwenden, lässt sich mit dem Code in diesem Tutorial der Fokus einfach auf die Konfiguration der Bibliothek legen, und Sie können dann Schlüssel in Ihren Code einfügen. Sie müssen keinen Azure-spezifischen Code schreiben.

Um diesen Code auf Ihrem lokalen Computer auszuführen, wobei Sie mit dem Erstellen einer Schlüsseltresorressource beginnen, gehen Sie entsprechend den Anweisungen in den nächsten Abschnitten vor.

## <a name="create-a-key-vault-resource"></a>Erstellen einer Schlüsseltresorressource

In diesem Abschnitt verwenden Sie die Azure-Befehlszeilenschnittstelle, um eine Schlüsseltresorressource zu erstellen und diese mit einem Geheimnis zu füllen.

1. Erstellen Sie einen Azure-Dienstprinzipal. In diesem Schritt erhalten Sie die Client-ID und den Schlüssel, die Sie benötigen, um auf Ihren Schlüsseltresor zugreifen zu können:

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    Es soll *microprofile-keyvault-service-principal* verwendet werden, um *\<service_principal_name>* in diesem Schritt zu ersetzen. Die Antwort von Azure sieht so aus wie die folgende Antwort:

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    Von besonderer Bedeutung sind hier die Werte von *appId* und *password*. Sie benötigen diese Werte später in diesem Artikel als Client-ID (*client ID*) und Schlüssel (*key*).

1. (Optional) Nachdem Sie einen Dienst Dienstprinzipal erstellt haben, können Sie eine Ressourcengruppe erstellen. Wenn Sie bereits eine Ressourcengruppe haben, die Sie verwenden möchten, können Sie diesen Schritt überspringen. Um eine Liste mit Ressourcengruppenstandorten abzurufen, können Sie `az account list-locations` aufrufen. Anschließend können Sie den *name*-Wert aus dieser Liste verwenden, um anzugeben, wo die Ressourcengruppe erstellt werden soll.

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. Erstellen Sie eine Schlüsseltresorressource. Sie verwenden Ihren Schlüsseltresornamen, um später auf den Schlüsseltresor zu verweisen. Daher sollten Sie einen einprägsamen Namen wählen.

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. Weisen Sie dem zuvor von Ihnen erstellten Dienstprinzipal die erforderlichen Berechtigungen zu, damit er auf die Schlüsseltresorgeheimnisse zugreifen kann. Der appId-Wert im folgenden Code ist der *appId*-Wert aus Schritt 1, in dem Sie den Dienstprinzipal erstellt haben. Das heißt, der *appId*-Wert in Schritt 1 war *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, Sie müssen aber den Wert aus Ihren eigenen Terminalausgabe verwenden.

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. Jetzt können Sie ein Geheimnis in Ihren Schlüsseltresor schreiben. Verwenden Sie den Schlüsselnamen *demo-key*, und legen den Wert des Schlüssels auf *demo-value* fest:

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

Das ist alles! Sie haben nun einen Schlüsseltresor, der in Azure ausgeführt wird und ein Geheimnis enthält. Sie können dieses Repository jetzt klonen und so konfigurieren, dass es diese Ressource in Ihrer App verwendet.

## <a name="get-up-and-running-locally"></a>Einrichten und Ausführen in der lokalen Umgebung

Dieses Beispiel basiert auf einer auf GitHub verfügbaren Beispielanwendung. Daher klonen Sie diese Anwendung, und durchlaufen Sie den Code Schritt für Schritt. 

1. Klonen Sie den Code auf Ihrem Computer, indem Sie die folgenden Befehle eingeben:

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. Wechseln Sie zu *src/main/resources/META-INF/microprofile-config.properties*, und ändern Sie dann die Eigenschaften in der Datei *microprofile-config.properties*, indem Sie die Werte aus den vorherigen Schritten verwenden.

1. Führen Sie den Server durch Verwenden von `mvn clean package payara-micro:start` aus.

1. Greifen Sie aus Ihrem Webbrowser auf [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) zu. Daraufhin sollte eine einfache Antwort angezeigt werden, in der die Werte enthalten sind, die aus Ihrem Schlüsseltresor gelesen werden.

## <a name="summary"></a>Zusammenfassung

In dieser Beispielanwendung sind die MicroProfile Config-API, Azure Key Vault und die kostenlose Open-Source-Bibliothek [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) kombiniert, um einfaches Einfügen von Konfigurationsdaten und Geheimnissen in Ihre MicroProfile-Webdienste zu ermöglichen.
