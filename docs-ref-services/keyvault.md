---
title: Azure Key Vault-Bibliotheken für Java
description: Übersicht über die Azure Key Vault-Bibliotheken für Java
keywords: Azure, Java, SDK, API, Key Vault, sicher, Schlüssel, Geheimnisse, Tresor
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: b3433d2da2054741015b9fa669753a8edb48cdf3
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324297"
---
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="ac891-104">Azure Key Vault-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="ac891-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="ac891-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="ac891-105">Overview</span></span>

<span data-ttu-id="ac891-106">Mit [Azure Key Vault](/azure/key-vault/) können Sie kryptografische Schlüssel und Geheimnisse schützen und verwalten, die von Cloudanwendungen und -diensten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ac891-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="ac891-107">Weitere Informationen zu den ersten Schritten mit Azure Key Vault finden Sie unter [Erste Schritte mit dem Azure-Schlüsseltresor](/azure/key-vault/key-vault-get-started).</span><span class="sxs-lookup"><span data-stu-id="ac891-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="ac891-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="ac891-108">Client library</span></span>

<span data-ttu-id="ac891-109">Erstellen, aktualisieren und löschen Sie Schlüssel und Geheimnisse in Azure Key Vault mit den Clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="ac891-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="ac891-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ac891-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.1.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="ac891-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ac891-111">Example</span></span>

<span data-ttu-id="ac891-112">Abrufen eines [JSON-Webschlüssels](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) aus einem Schlüsseltresor.</span><span class="sxs-lookup"><span data-stu-id="ac891-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac891-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="ac891-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a><span data-ttu-id="ac891-114">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="ac891-114">Management API</span></span>

<span data-ttu-id="ac891-115">Verwenden Sie die Azure Key Vault-Verwaltungsbibliotheken, um Schlüsseltresore zu erstellen, Anwendungen zu autorisieren und Berechtigungen zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="ac891-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="ac891-116">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ac891-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.15.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="ac891-117">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ac891-117">Example</span></span>

<span data-ttu-id="ac891-118">Autorisieren einer mit dem [Dienstprinzipal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` ausgeführten Anwendung zum Auflisten und Abrufen von Geheimnissen aus einem Schlüsseltresor</span><span class="sxs-lookup"><span data-stu-id="ac891-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

```java
vault1 = vault1.update()
            .defineAccessPolicy()
                .forServicePrincipal(clientId)
                .allowKeyAllPermissions()
                .allowSecretPermissions(SecretPermissions.GET)
                .allowSecretPermissions(SecretPermissions.LIST)
                .attach()
            .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac891-119">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="ac891-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a><span data-ttu-id="ac891-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ac891-120">Samples</span></span>

<span data-ttu-id="ac891-121">Sehen Sie sich weitere [Java-Codebeispiele für Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ac891-121">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>
