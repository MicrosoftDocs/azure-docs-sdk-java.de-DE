---
title: "Azure App Service-Bibliotheken für Java"
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
ms.openlocfilehash: e5d2a66dc984d34fb9a6668d2ea3bf1ee6164e70
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2017
---
# <a name="azure-app-service-libraries-for-java"></a><span data-ttu-id="a8e31-104">Azure App Service-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="a8e31-104">Azure App Service libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a8e31-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="a8e31-105">Overview</span></span>

<span data-ttu-id="a8e31-106">Stellen Sie mit [Azure App Service](/azure/app-service) Websites, Webanwendungen und REST-APIs bereit, und verwalten Sie sie.</span><span class="sxs-lookup"><span data-stu-id="a8e31-106">Deploy and manage websites, web applications, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="a8e31-107">Informationen zu den ersten Schritten mit Azure App Service finden Sie unter [Erstellen Ihrer ersten Java-Web-App in Azure](/azure/app-service-web/app-service-web-get-started-java).</span><span class="sxs-lookup"><span data-stu-id="a8e31-107">To get started with Azure App Service, see [Create your first Java web app in Azure](/azure/app-service-web/app-service-web-get-started-java).</span></span>

## <a name="management-api"></a><span data-ttu-id="a8e31-108">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="a8e31-108">Management API</span></span>

<span data-ttu-id="a8e31-109">Mit der Verwaltungs-API können Sie Anwendungen in Azure App Service bereitstellen, skalieren und konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="a8e31-109">Deploy, scale, and configure applications in Azure App Service with the management API.</span></span>

<span data-ttu-id="a8e31-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a8e31-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.2.1</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8e31-111">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="a8e31-111">Explore the Management APIs</span></span>](/java/api/overview/azure)

### <a name="example"></a><span data-ttu-id="a8e31-112">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a8e31-112">Example</span></span>

<span data-ttu-id="a8e31-113">Stellen Sie eine Web-App über ein Docker-Image in einer Azure-Web-App unter Linux bereit:</span><span class="sxs-lookup"><span data-stu-id="a8e31-113">Deploy a webapp from a Docker image into an Azure Web App running on Linux.</span></span>

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a><span data-ttu-id="a8e31-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a8e31-114">Samples</span></span>

<span data-ttu-id="a8e31-115">[Bereitstellen einer Web-App über FTP oder GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="a8e31-115">[Deploy a web app from FTP or GitHub][1]</span></span>  
<span data-ttu-id="a8e31-116">[Austausch zwischen App-Versionen mit Bereitstellungsslots][2]</span><span class="sxs-lookup"><span data-stu-id="a8e31-116">[Swap between app versions with deployment slots][2]</span></span>  
<span data-ttu-id="a8e31-117">[Konfigurieren einer benutzerdefinierten Domäne][3] </span><span class="sxs-lookup"><span data-stu-id="a8e31-117">[Configure a custom domain][3] </span></span>  
<span data-ttu-id="a8e31-118">[Skalieren einer Web-App über mehrere Regionen hinweg][4]</span><span class="sxs-lookup"><span data-stu-id="a8e31-118">[Scale a web app across multiple regions][4]</span></span>   

<span data-ttu-id="a8e31-119">Sehen Sie sich weitere [Java-Codebeispiele für Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="a8e31-119">Explore more [sample Java code for Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) you can use in your apps.</span></span>

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
