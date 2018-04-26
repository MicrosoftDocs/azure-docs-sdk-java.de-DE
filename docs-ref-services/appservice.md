---
title: Azure App Service-Bibliotheken für Java
description: Automatisieren der Bereitstellung von Web-Apps in Azure App Service mit den Azure-Verwaltungs-APIs
keywords: Azure, Java, SDK, API, Web-Apps, mobil, App Service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/09/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appservice
ms.openlocfilehash: adbb527666553ecc3039ce35c035d017f502c801
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="azure-app-service-libraries-for-java"></a>Azure App Service-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Stellen Sie mit [Azure App Service](/azure/app-service) Websites, Webanwendungen und REST-APIs bereit, und verwalten Sie sie.

Informationen zu den ersten Schritten mit Azure App Service finden Sie unter [Erstellen Ihrer ersten Java-Web-App in Azure](/azure/app-service-web/app-service-web-get-started-java).

## <a name="management-api"></a>Verwaltungs-API

Mit der Verwaltungs-API können Sie Anwendungen in Azure App Service bereitstellen, skalieren und konfigurieren.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.3.0</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/appservice/management)

### <a name="example"></a>Beispiel

Stellen Sie eine Web-App über ein Docker-Image in einer Azure-Web-App unter Linux bereit:

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a>Beispiele

[Bereitstellen einer Web-App über FTP oder GitHub][1]  
[Austausch zwischen App-Versionen mit Bereitstellungsslots][2]  
[Konfigurieren einer benutzerdefinierten Domäne][3]   
[Skalieren einer Web-App über mehrere Regionen hinweg][4]   

Sehen Sie sich weitere [Java-Codebeispiele für Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) an, die Sie in Ihren Apps verwenden können.

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
