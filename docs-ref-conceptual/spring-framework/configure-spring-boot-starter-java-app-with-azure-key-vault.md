---
title: Verwenden von Spring Boot Starter für Azure Key Vault
description: Hier erfahren Sie, wie Sie eine Spring Boot Initializer-App mit Azure Key Vault Starter konfigurieren.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 1dda697cac80a6cad3ebbbbf8a5a4f18b515dfd8
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/08/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a>Verwenden von Spring Boot Starter für Azure Key Vault

## <a name="overview"></a>Übersicht

In diesem Artikel erfahren Sie, wie Sie eine App mit **[Spring Initializr]** erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Key Vault, um eine Verbindungszeichenfolge abzurufen, die als Geheimnis in einem Schlüsseltresor gespeichert ist.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
* [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), Version 1.7 oder höher
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher

## <a name="create-an-app-using-the-spring-initialzr"></a>Erstellen einer App mithilfe von Spring Initializr

1. Navigieren Sie zu <https://start.spring.io/>.

1. Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.

   ![Angeben von Gruppen- und Artefaktnamen][secrets-01]

1. Scrollen Sie nach unten zum Abschnitt **Azure**, und aktivieren Sie das Kontrollkästchen für **Azure Key Vault**.

   ![Auswählen von Azure Key Vault Starter][secrets-02]

1. Klicken Sie am unteren Seitenrand auf die Schaltfläche **Projekt generieren**.

   ![Generieren eines Spring Boot-Projekts][secrets-03]

1. Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a>Anmelden bei Azure und Auswählen des zu verwendenden Abonnements

1. Öffnen Sie eine Eingabeaufforderung.

1. Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:

   ```azurecli
   az login
   ```
   Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.

1. Listen Sie Ihre Abonnements auf:

   ```azurecli
   az account list
   ```
   Azure gibt eine Liste mit Ihren Abonnements zurück. Kopieren Sie die GUID für das Abonnement, das Sie verwenden möchten. Beispiel:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. Geben Sie die GUID für das Konto an, das Sie mit Azure verwenden möchten. Beispiel:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a>Erstellen und Konfigurieren einer neuen Azure Key Vault-Instanz mithilfe der Azure-Befehlszeilenschnittstelle

1. Erstellen Sie eine Ressourcengruppe für die Azure-Ressourcen, die Sie für Ihren Schlüsseltresor verwenden. Beispiel:
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `name` | Gibt einen eindeutigen Namen für Ihre Ressourcengruppe an. |
   | `location` | Gibt die [Azure-Region](https://azure.microsoft.com/regions/) an, in der Ihre Ressourcengruppe gehostet wird. |

   Die Azure CLI zeigt die Ergebnisse der Erstellung Ihrer Ressourcengruppe an, Beispiel:  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

1. Erstellen Sie einen Azure-Dienstprinzipal auf der Grundlage Ihrer Anwendungsregistrierung. Beispiel:
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `name` | Gibt den Namen für den Azure-Dienstprinzipal an. |

   Die Azure-Befehlszeilenschnittstelle gibt eine JSON-Statusmeldung mit der App-ID (*appId*) und dem Kennwort (*password*) zurück. Diese Werte werden später als Client-ID und Clientkennwort verwendet. Beispiel:

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

1. Erstellen Sie in der Ressourcengruppe einen neuen Schlüsseltresor. Beispiel:
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `name` | Gibt einen eindeutigen Namen für Ihren Schlüsseltresor an. |
   | `location` | Gibt die [Azure-Region](https://azure.microsoft.com/regions/) an, in der Ihre Ressourcengruppe gehostet wird. |
   | `enabled-for-deployment` | Gibt die [Bereitstellungsoption für den Schlüsseltresor](https://docs.microsoft.com/en-us/cli/azure/keyvault) an. |
   | `enabled-for-disk-encryption` | Gibt die [Verschlüsselungsoption für den Schlüsseltresor](https://docs.microsoft.com/en-us/cli/azure/keyvault) an. |
   | `enabled-for-template-deployment` | Gibt die [Verschlüsselungsoption für den Schlüsseltresor](https://docs.microsoft.com/en-us/cli/azure/keyvault) an. |
   | `sku` | Gibt die [SKU-Option für den Schlüsseltresor](https://docs.microsoft.com/en-us/cli/azure/keyvault) an. |
   | `query` | Gibt einen Wert an, der aus der Antwort abgerufen werden soll. Hierbei handelt es sich um den Schlüsseltresor-URI, den Sie im Rahmen dieses Tutorials benötigen. |

   Die Azure-Befehlszeilenschnittstelle zeigt den URI für den Schlüsseltresor an. Dieser wird später verwendet. Beispiel:  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

1. Legen Sie die Zugriffsrichtlinie für den zuvor erstellten Azure-Dienstprinzipal fest. Beispiel:
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `name` | Gibt den Schlüsseltresornamen von vorhin an. |
   | `secret-permission` | Gibt die [Sicherheitsrichtlinien](https://docs.microsoft.com/en-us/cli/azure/keyvault) für Ihren Schlüsseltresor an. |
   | `spn` | Gibt die GUID für Ihre Anwendungsregistrierung von vorhin an. |

   Die Azure-Befehlszeilenschnittstelle zeigt die Ergebnisse der Sicherheitsrichtlinienerstellung an. Beispiel:  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "location": "westus",
     "name": "wingtiptoyskeyvault",
     "properties": {
       ...
       ... (A long list of values will be displayed here.)
       ...
     },
     "resourceGroup": "wingtiptoysresources",
     "tags": {},
     "type": "Microsoft.KeyVault/vaults"
   }
   ```

1. Speichern Sie ein Geheimnis in Ihrem neuen Schlüsseltresor. Beispiel:
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `vault-name` | Gibt den Schlüsseltresornamen von vorhin an. |
   | `name` | Gibt den Namen Ihres Geheimnisses an. |
   | `value` | Gibt den Wert Ihres Geheimnisses an. |

   Die Azure-Befehlszeilenschnittstelle zeigt die Ergebnisse der Geheimniserstellung an. Beispiel:  

   ```json
   {
     "attributes": {
       "created": "2017-12-01T09:00:16+00:00",
       "enabled": true,
       "expires": null,
       "notBefore": null,
       "recoveryLevel": "Purgeable",
       "updated": "2017-12-01T09:00:16+00:00"
     },
     "contentType": null,
     "id": "https://wingtiptoyskeyvault.vault.azure.net/secrets/connectionString/123456789abcdef123456789abcdef",
     "kid": null,
     "managed": null,
     "tags": {
       "file-encoding": "utf-8"
     },
     "value": "jdbc:sqlserver://wingtiptoys.database.windows.net:1433;database=DATABASE;"
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a>Konfigurieren und Kompilieren Ihrer Spring Boot-Anwendung

1. Extrahieren Sie die Dateien aus den zuvor heruntergeladenen Spring Boot-Projektarchivdateien in ein Verzeichnis.

1. Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.

1. Fügen Sie die Werte für Ihren Schlüsseltresor hinzu. Verwenden Sie dabei Werte aus den vorherigen Schritten dieses Tutorials. Beispiel:
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `azure.keyvault.uri` | Gibt den URI von der Erstellung Ihres Schlüsseltresors an. |
   | `azure.keyvault.client-id` | Gibt die GUID *appId* von der Erstellung Ihres Dienstprinzipals an. |
   | `azure.keyvault.client-key` | Gibt die GUID *password* von der Erstellung Ihres Dienstprinzipals an. |

1. Navigieren Sie zur Quellcode-Hauptdatei Ihres Projekts. Beispiel: */src/main/java/com/wingtiptoys/secrets*.

1. Öffnen Sie die Java-Hauptdatei der Anwendung (beispielsweise *SecretsApplication.java*) in einem Text-Editor, und fügen Sie ihr folgende Zeilen hinzu:

   ```java
   package com.wingtiptoys.secrets;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class SecretsApplication implements CommandLineRunner {

      @Value("${connectionString}")
      private String connectionString;

      public static void main(String[] args) {
         SpringApplication.run(SecretsApplication.class, args);
      }

      public void run(String... varl) throws Exception {
         System.out.println(String.format("\nConnection String stored in Azure Key Vault:\n%s\n",connectionString));
      }
   }
   ```
   Dieses Codebeispiel ruft die Verbindungszeichenfolge aus dem Schlüsseltresor ab und zeigt sie in der Befehlszeile an.

1. Speichern und schließen Sie die Java-Datei.

## <a name="build-and-test-your-app"></a>Erstellen und Testen der App

1. Navigieren Sie zum Verzeichnis mit der Datei *pom.xml* für Ihre Spring Boot-App:

1. Erstellen Sie Ihre Spring Boot-Anwendung mit Maven. Beispiel:

   ```bash
   mvn clean package
   ```

   Maven zeigt die Ergebnisse des Buildvorgangs an.

   ![Buildstatus der Spring Boot-Anwendung][build-application-01]

1. Führen Sie Ihre Spring Boot-Anwendung mit Maven aus. Die Anwendung zeigt die Verbindungszeichenfolge aus Ihrem Schlüsseltresor an. Beispiel: 

   ```bash
   mvn spring-boot:run
   ```

   ![Spring Boot-Laufzeitmeldung][build-application-02]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von Azure Key Vault-Instanzen finden Sie in den folgenden Artikeln:

* [Dokumentation zu Key Vault]

* [Erste Schritte mit dem Azure-Schlüsseltresor]

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

<!-- URL List -->

[Dokumentation zu Key Vault]: /azure/key-vault/
[Erste Schritte mit dem Azure-Schlüsseltresor]: /azure/key-vault/key-vault-get-started
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
