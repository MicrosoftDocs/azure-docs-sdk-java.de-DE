---
title: "Azure Resource Manager-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Resource Manager-Bibliotheken"
keywords: Azure, Java, SDK, API, Ressourcengruppen, ARM, Resource Manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 4b73f6b03258e7d99bcca235cc2728d5e085b32a
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2017
---
# <a name="azure-resource-manager-libraries-for-java"></a>Azure Resource Manager-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Mit [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) können Sie Ressourcen in Gruppen bereitstellen, überwachen und verwalten.

## <a name="management-api"></a>Verwaltungs-API

Verwenden Sie die Verwaltungs-API zum Erstellen von Ressourcengruppen und Bereitstellen von Ressourcen aus Vorlagen.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Beispiel

Erstellen Sie eine neue Ressourcengruppe in der Azure-Region „USA, Osten“.

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/resources/managementapi)

## <a name="samples"></a>Beispiele

[Verwalten von Azure-Ressourcengruppen mit Java][1] 
[Bereitstellen von Ressourcen mit einer ARM-Vorlage][2]

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) mit Azure Resource Manager-Beispielen an.
