---
title: Verwenden von Spring Boot Starter für Azure Key Vault
description: Hier erfahren Sie, wie Sie eine Spring Boot Initializer-App mit Azure Key Vault Starter konfigurieren.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: fcb18de809f4465239f1f360a755624a5095e03a
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339154"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="c0f38-103">Verwenden von Spring Boot Starter für Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c0f38-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="c0f38-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="c0f38-104">Overview</span></span>

<span data-ttu-id="c0f38-105">In diesem Artikel erfahren Sie, wie Sie eine App mit **[Spring Initializr]** erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Key Vault, um eine Verbindungszeichenfolge abzurufen, die als Geheimnis in einem Schlüsseltresor gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="c0f38-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0f38-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c0f38-106">Prerequisites</span></span>

<span data-ttu-id="c0f38-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="c0f38-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="c0f38-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="c0f38-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c0f38-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="c0f38-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c0f38-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c0f38-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c0f38-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="c0f38-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="c0f38-112">Erstellen einer App mithilfe von Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="c0f38-112">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="c0f38-113">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="c0f38-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="c0f38-114">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.</span><span class="sxs-lookup"><span data-stu-id="c0f38-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Angeben von Gruppen- und Artefaktnamen][secrets-01]

1. <span data-ttu-id="c0f38-116">Scrollen Sie nach unten zum Abschnitt **Azure**, und aktivieren Sie das Kontrollkästchen für **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="c0f38-116">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Auswählen von Azure Key Vault Starter][secrets-02]

1. <span data-ttu-id="c0f38-118">Klicken Sie am unteren Seitenrand auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="c0f38-118">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generieren eines Spring Boot-Projekts][secrets-03]

1. <span data-ttu-id="c0f38-120">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="c0f38-120">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure"></a><span data-ttu-id="c0f38-121">Anmelden bei Azure</span><span class="sxs-lookup"><span data-stu-id="c0f38-121">Sign into Azure</span></span>

1. <span data-ttu-id="c0f38-122">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="c0f38-122">Open a command prompt.</span></span>

1. <span data-ttu-id="c0f38-123">Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="c0f38-123">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="c0f38-124">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="c0f38-124">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="c0f38-125">Listen Sie Ihre Abonnements auf:</span><span class="sxs-lookup"><span data-stu-id="c0f38-125">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="c0f38-126">Azure gibt eine Liste mit Ihren Abonnements zurück. Kopieren Sie die GUID für das Abonnement, das Sie verwenden möchten. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-126">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="c0f38-127">Geben Sie die GUID für das Konto an, das Sie mit Azure verwenden möchten. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-127">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-a-new-azure-key-vault"></a><span data-ttu-id="c0f38-128">Erstellen einer neuen Azure Key Vault-Instanz</span><span class="sxs-lookup"><span data-stu-id="c0f38-128">Create a new Azure Key Vault</span></span>

1. <span data-ttu-id="c0f38-129">Erstellen Sie eine Ressourcengruppe für die Azure-Ressourcen, die Sie für Ihren Schlüsseltresor verwenden. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-129">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="c0f38-130">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0f38-130">Where:</span></span>

   | <span data-ttu-id="c0f38-131">Parameter</span><span class="sxs-lookup"><span data-stu-id="c0f38-131">Parameter</span></span> | <span data-ttu-id="c0f38-132">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0f38-132">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="c0f38-133">Gibt einen eindeutigen Namen für Ihre Ressourcengruppe an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-133">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="c0f38-134">Gibt die [Azure-Region](https://azure.microsoft.com/regions/) an, in der Ihre Ressourcengruppe gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="c0f38-134">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="c0f38-135">Die Azure CLI zeigt die Ergebnisse der Erstellung Ihrer Ressourcengruppe an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-135">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

2. <span data-ttu-id="c0f38-136">Erstellen Sie einen Azure-Dienstprinzipal auf der Grundlage Ihrer Anwendungsregistrierung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-136">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="c0f38-137">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0f38-137">Where:</span></span>

   | <span data-ttu-id="c0f38-138">Parameter</span><span class="sxs-lookup"><span data-stu-id="c0f38-138">Parameter</span></span> | <span data-ttu-id="c0f38-139">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0f38-139">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="c0f38-140">Gibt den Namen für den Azure-Dienstprinzipal an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-140">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="c0f38-141">Die Azure-Befehlszeilenschnittstelle gibt eine JSON-Statusmeldung mit der App-ID (*appId*) und dem Kennwort (*password*) zurück. Diese Werte werden später als Client-ID und Clientkennwort verwendet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-141">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. <span data-ttu-id="c0f38-142">Erstellen Sie in der Ressourcengruppe einen neuen Schlüsseltresor. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-142">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="c0f38-143">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0f38-143">Where:</span></span>

   | <span data-ttu-id="c0f38-144">Parameter</span><span class="sxs-lookup"><span data-stu-id="c0f38-144">Parameter</span></span> | <span data-ttu-id="c0f38-145">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0f38-145">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="c0f38-146">Gibt einen eindeutigen Namen für Ihren Schlüsseltresor an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-146">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="c0f38-147">Gibt die [Azure-Region](https://azure.microsoft.com/regions/) an, in der Ihre Ressourcengruppe gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="c0f38-147">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="c0f38-148">Gibt die [Bereitstellungsoption für den Schlüsseltresor](https://docs.microsoft.com/cli/azure/keyvault) an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-148">Specifies the [key vault deployment option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="c0f38-149">Gibt die [Verschlüsselungsoption für den Schlüsseltresor](https://docs.microsoft.com/cli/azure/keyvault) an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-149">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="c0f38-150">Gibt die [Verschlüsselungsoption für den Schlüsseltresor](https://docs.microsoft.com/cli/azure/keyvault) an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-150">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="c0f38-151">Gibt die [SKU-Option für den Schlüsseltresor](https://docs.microsoft.com/cli/azure/keyvault) an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-151">Specifies the [key vault SKU option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="c0f38-152">Gibt einen Wert an, der aus der Antwort abgerufen werden soll. Hierbei handelt es sich um den Schlüsseltresor-URI, den Sie im Rahmen dieses Tutorials benötigen.</span><span class="sxs-lookup"><span data-stu-id="c0f38-152">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="c0f38-153">Die Azure-Befehlszeilenschnittstelle zeigt den URI für den Schlüsseltresor an. Dieser wird später verwendet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-153">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. <span data-ttu-id="c0f38-154">Legen Sie die Zugriffsrichtlinie für den zuvor erstellten Azure-Dienstprinzipal fest. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-154">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="c0f38-155">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0f38-155">Where:</span></span>

   | <span data-ttu-id="c0f38-156">Parameter</span><span class="sxs-lookup"><span data-stu-id="c0f38-156">Parameter</span></span> | <span data-ttu-id="c0f38-157">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0f38-157">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="c0f38-158">Gibt den Schlüsseltresornamen von vorhin an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-158">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="c0f38-159">Gibt die [Sicherheitsrichtlinien](https://docs.microsoft.com/cli/azure/keyvault) für Ihren Schlüsseltresor an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-159">Specifies the [security policies](https://docs.microsoft.com/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="c0f38-160">Gibt die GUID für Ihre Anwendungsregistrierung von vorhin an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-160">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="c0f38-161">Die Azure-Befehlszeilenschnittstelle zeigt die Ergebnisse der Sicherheitsrichtlinienerstellung an. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-161">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

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

5. <span data-ttu-id="c0f38-162">Speichern Sie ein Geheimnis in Ihrem neuen Schlüsseltresor. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-162">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="c0f38-163">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0f38-163">Where:</span></span>

   | <span data-ttu-id="c0f38-164">Parameter</span><span class="sxs-lookup"><span data-stu-id="c0f38-164">Parameter</span></span> | <span data-ttu-id="c0f38-165">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0f38-165">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="c0f38-166">Gibt den Schlüsseltresornamen von vorhin an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-166">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="c0f38-167">Gibt den Namen Ihres Geheimnisses an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-167">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="c0f38-168">Gibt den Wert Ihres Geheimnisses an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-168">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="c0f38-169">Die Azure-Befehlszeilenschnittstelle zeigt die Ergebnisse der Geheimniserstellung an. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-169">The Azure CLI will display the results of your secret creation; for example:</span></span>  

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

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="c0f38-170">Konfigurieren und Kompilieren Ihrer App</span><span class="sxs-lookup"><span data-stu-id="c0f38-170">Configure and compile your app</span></span>

1. <span data-ttu-id="c0f38-171">Extrahieren Sie die Dateien aus den zuvor heruntergeladenen Spring Boot-Projektarchivdateien in ein Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="c0f38-171">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

2. <span data-ttu-id="c0f38-172">Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="c0f38-172">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

3. <span data-ttu-id="c0f38-173">Fügen Sie die Werte für Ihren Schlüsseltresor hinzu. Verwenden Sie dabei Werte aus den vorherigen Schritten dieses Tutorials. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-173">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="c0f38-174">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c0f38-174">Where:</span></span>

   |          <span data-ttu-id="c0f38-175">Parameter</span><span class="sxs-lookup"><span data-stu-id="c0f38-175">Parameter</span></span>          |                                 <span data-ttu-id="c0f38-176">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c0f38-176">Description</span></span>                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           <span data-ttu-id="c0f38-177">Gibt den URI von der Erstellung Ihres Schlüsseltresors an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-177">Specifies the URI from when you created your key vault.</span></span>           |
   | `azure.keyvault.client-id`  |  <span data-ttu-id="c0f38-178">Gibt die GUID *appId* von der Erstellung Ihres Dienstprinzipals an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-178">Specifies the *appId* GUID from when you created your service principal.</span></span>   |
   | `azure.keyvault.client-key` | <span data-ttu-id="c0f38-179">Gibt die GUID *password* von der Erstellung Ihres Dienstprinzipals an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-179">Specifies the *password* GUID from when you created your service principal.</span></span> |


4. <span data-ttu-id="c0f38-180">Navigieren Sie zur Quellcode-Hauptdatei Ihres Projekts. Beispiel: */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="c0f38-180">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

5. <span data-ttu-id="c0f38-181">Öffnen Sie die Java-Hauptdatei der Anwendung (beispielsweise *SecretsApplication.java*) in einem Text-Editor, und fügen Sie ihr folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="c0f38-181">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

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
   <span data-ttu-id="c0f38-182">Dieses Codebeispiel ruft die Verbindungszeichenfolge aus dem Schlüsseltresor ab und zeigt sie in der Befehlszeile an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-182">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

6. <span data-ttu-id="c0f38-183">Speichern und schließen Sie die Java-Datei.</span><span class="sxs-lookup"><span data-stu-id="c0f38-183">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="c0f38-184">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="c0f38-184">Build and test your app</span></span>

1. <span data-ttu-id="c0f38-185">Navigieren Sie zum Verzeichnis mit der Datei *pom.xml* für Ihre Spring Boot-App:</span><span class="sxs-lookup"><span data-stu-id="c0f38-185">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="c0f38-186">Erstellen Sie Ihre Spring Boot-Anwendung mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c0f38-186">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="c0f38-187">Maven zeigt die Ergebnisse des Buildvorgangs an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-187">Maven will display the results of your build.</span></span>

   ![Buildstatus der Spring Boot-Anwendung][build-application-01]

1. <span data-ttu-id="c0f38-189">Führen Sie Ihre Spring Boot-Anwendung mit Maven aus. Die Anwendung zeigt die Verbindungszeichenfolge aus Ihrem Schlüsseltresor an.</span><span class="sxs-lookup"><span data-stu-id="c0f38-189">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="c0f38-190">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="c0f38-190">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Spring Boot-Laufzeitmeldung][build-application-02]

## <a name="summary"></a><span data-ttu-id="c0f38-192">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c0f38-192">Summary</span></span>

<span data-ttu-id="c0f38-193">In diesem Tutorial haben Sie mit **[Spring Initializr]** eine neue Java-Web-App und eine Azure Key Vault-Instanz zum Speichern vertraulicher Informationen erstellt und anschließend Ihre Anwendung zum Abrufen von Informationen aus dem Schlüsseltresor konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="c0f38-193">In this tutorial, you created a new Java web application using the **[Spring Initializr]**, created ab Azure Key Vault to store sensitive information, and then configured your application to retrieve information from your key vault.</span></span>

<span data-ttu-id="c0f38-194">Weitere Informationen zur Verwendung von Azure Key Vault-Instanzen finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="c0f38-194">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="c0f38-195">[Dokumentation zu Key Vault]</span><span class="sxs-lookup"><span data-stu-id="c0f38-195">[Key Vault Documentation].</span></span>

* <span data-ttu-id="c0f38-196">[Erste Schritte mit dem Azure-Schlüsseltresor]</span><span class="sxs-lookup"><span data-stu-id="c0f38-196">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="c0f38-197">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="c0f38-197">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="c0f38-198">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c0f38-198">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="c0f38-199">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="c0f38-199">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="c0f38-200">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c0f38-200">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0f38-201">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c0f38-201">Next steps</span></span>

<span data-ttu-id="c0f38-202">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="c0f38-202">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0f38-203">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="c0f38-203">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Dokumentation zu Key Vault]: /azure/key-vault/
[Key Vault Documentation]: /azure/key-vault/
[Erste Schritte mit dem Azure-Schlüsseltresor]: /azure/key-vault/key-vault-get-started
[Get started with Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
