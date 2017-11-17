---
title: "Azure Key Vault-Bibliotheken für Java"
description: "Übersicht über die Azure Key Vault-Bibliotheken für Java"
keywords: "Azure, Java, SDK, API, Key Vault, sicher, Schlüssel, Geheimnisse, Tresor"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: 51ac51f5436397a0c9f1a4572dcf79a40f10b538
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2017
---
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="6d489-104">Azure Key Vault-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="6d489-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="6d489-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="6d489-105">Overview</span></span>

<span data-ttu-id="6d489-106">Mit [Azure Key Vault](/azure/key-vault/) können Sie kryptografische Schlüssel und Geheimnisse schützen und verwalten, die von Cloudanwendungen und -diensten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6d489-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="6d489-107">Weitere Informationen zu den ersten Schritten mit Azure Key Vault finden Sie unter [Erste Schritte mit dem Azure-Schlüsseltresor](/azure/key-vault/key-vault-get-started).</span><span class="sxs-lookup"><span data-stu-id="6d489-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="6d489-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="6d489-108">Client library</span></span>

<span data-ttu-id="6d489-109">Erstellen, aktualisieren und löschen Sie Schlüssel und Geheimnisse in Azure Key Vault mit den Clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="6d489-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="6d489-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d489-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="6d489-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="6d489-111">Example</span></span>

<span data-ttu-id="6d489-112">Abrufen eines [JSON-Webschlüssels](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) aus einem Schlüsseltresor.</span><span class="sxs-lookup"><span data-stu-id="6d489-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d489-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="6d489-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/clientlibrary)


## <a name="management-api"></a><span data-ttu-id="6d489-114">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="6d489-114">Management API</span></span>

<span data-ttu-id="6d489-115">Verwenden Sie die Azure Key Vault-Verwaltungsbibliotheken, um Schlüsseltresore zu erstellen, Anwendungen zu autorisieren und Berechtigungen zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="6d489-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="6d489-116">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d489-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="6d489-117">Beispiel</span><span class="sxs-lookup"><span data-stu-id="6d489-117">Example</span></span>

<span data-ttu-id="6d489-118">Autorisieren einer mit dem [Dienstprinzipal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` ausgeführten Anwendung zum Auflisten und Abrufen von Geheimnissen aus einem Schlüsseltresor</span><span class="sxs-lookup"><span data-stu-id="6d489-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

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
> [<span data-ttu-id="6d489-119">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="6d489-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/managementapi)


## <a name="samples"></a><span data-ttu-id="6d489-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="6d489-120">Samples</span></span>

<span data-ttu-id="6d489-121">[Verwalten von Schlüsseltresoren][1]</span><span class="sxs-lookup"><span data-stu-id="6d489-121">[Manage Key Vaults][1]</span></span>   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

<span data-ttu-id="6d489-122">Sehen Sie sich weitere [Java-Codebeispiele für Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="6d489-122">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>
