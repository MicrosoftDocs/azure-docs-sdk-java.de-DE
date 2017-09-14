---
title: "Azure DNS-Bibliotheken für Java"
description: "Referenzdokumentation für die Azure DNS-Verwaltungsbibliotheken für Java"
keywords: "Azure, Java, SDK, API, Domänen, DNS, Name, Dienst, Domain Name Service"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: 123f61004c473bc060f0360f0fcb027d1591523e
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="e2d39-104">Azure Traffic Manager-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="e2d39-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="e2d39-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="e2d39-105">Overview</span></span>

<span data-ttu-id="e2d39-106">Mit [Azure DNS](/azure/dns/dns-overview) können Sie die Auflösung des Domänennamens bereitstellen und DNS-Ressourceneinträge mithilfe der gleichen Anmeldeinformationen, APIs, Tools und Abrechnung wie für die anderen Azure-Dienste verwalten.</span><span class="sxs-lookup"><span data-stu-id="e2d39-106">Provide domain name resolution and manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services with [Azure DNS](/azure/dns/dns-overview).</span></span>

<span data-ttu-id="e2d39-107">Informationen zu den ersten Schritten mit Azure DNS finden Sie unter [Erste Schritte mit Azure DNS mithilfe der Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span><span class="sxs-lookup"><span data-stu-id="e2d39-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span></span>

## <a name="management-api"></a><span data-ttu-id="e2d39-108">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="e2d39-108">Management API</span></span>

<span data-ttu-id="e2d39-109">Erstellen Sie mit der Verwaltungs-API DNS-Zonen, und fügen Sie Einträge zu Zonen hinzu.</span><span class="sxs-lookup"><span data-stu-id="e2d39-109">Create DNS zones and add records to zones with the management API.</span></span>

<span data-ttu-id="e2d39-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="e2d39-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.2.1</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="e2d39-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="e2d39-111">Example</span></span>

<span data-ttu-id="e2d39-112">Erstellen einer DNS-Stammzone und Hinzufügen eines `www`-CNAME-Eintrags in einer vorhandenen Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="e2d39-112">Create a root DNS zone and add a `www` CNAME record in an existing resource group.</span></span>

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e2d39-113">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="e2d39-113">Explore the Management APIs</span></span>](/java/api/overview/azure/dns/managementapi)

## <a name="samples"></a><span data-ttu-id="e2d39-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="e2d39-114">Samples</span></span>

[<span data-ttu-id="e2d39-115">Hosten und Verwalten von Domänen mit Azure DNS</span><span class="sxs-lookup"><span data-stu-id="e2d39-115">Host and manage your domains with Azure DNS</span></span>](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

<span data-ttu-id="e2d39-116">Sehen Sie sich weitere [Java-Codebeispiele für Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="e2d39-116">Explore more [sample Java code for Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) you can use in your apps.</span></span>