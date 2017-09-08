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
ms.openlocfilehash: dc5e0552728e362451c033317e5a804c8067e79c
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-key-vault-libraries-for-java"></a>Azure Key Vault-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Mit [Azure Key Vault](/azure/key-vault/) können Sie kryptografische Schlüssel und Geheimnisse schützen und verwalten, die von Cloudanwendungen und -diensten verwendet werden.

Weitere Informationen zu den ersten Schritten mit Azure Key Vault finden Sie unter [Erste Schritte mit dem Azure-Schlüsseltresor](/azure/key-vault/key-vault-get-started).

## <a name="client-library"></a>Clientbibliothek

Erstellen, aktualisieren und löschen Sie Schlüssel und Geheimnisse in Azure Key Vault mit den Clientbibliotheken.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a>Beispiel

Abrufen eines [JSON-Webschlüssels](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) aus einem Schlüsseltresor.

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/java/api/overview/azure/keyvault/clientlibrary)


## <a name="management-api"></a>Verwaltungs-API

Verwenden Sie die Azure Key Vault-Verwaltungsbibliotheken, um Schlüsseltresore zu erstellen, Anwendungen zu autorisieren und Berechtigungen zu verwalten. 

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.1.2</version>
</dependency>
```

## <a name="example"></a>Beispiel

Autorisieren einer mit dem [Dienstprinzipal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` ausgeführten Anwendung zum Auflisten und Abrufen von Geheimnissen aus einem Schlüsseltresor 

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
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/keyvault/managementapi)


## <a name="samples"></a>Beispiele

[Verwalten von Schlüsseltresoren][1]   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

Sehen Sie sich weitere [Java-Codebeispiele für Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) an, die Sie in Ihren Apps verwenden können.
