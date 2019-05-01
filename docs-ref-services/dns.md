---
title: Azure DNS-Bibliotheken für Java
description: Referenzdokumentation für die Azure DNS-Verwaltungsbibliotheken für Java
keywords: Azure, Java, SDK, API, Domänen, DNS, Name, Dienst, Domain Name Service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: 364c51f985b7bf3a8c445cd7e03a5e91a8e589ba
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593435"
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="c3a61-104">Azure Traffic Manager-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="c3a61-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="c3a61-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="c3a61-105">Overview</span></span>

<span data-ttu-id="c3a61-106">Mit [Azure DNS](/azure/dns/dns-overview) können Sie die Auflösung des Domänennamens bereitstellen und DNS-Ressourceneinträge mithilfe der gleichen Anmeldeinformationen, APIs, Tools und Abrechnung wie für die anderen Azure-Dienste verwalten.</span><span class="sxs-lookup"><span data-stu-id="c3a61-106">Provide domain name resolution and manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services with [Azure DNS](/azure/dns/dns-overview).</span></span>

<span data-ttu-id="c3a61-107">Informationen zu den ersten Schritten mit Azure DNS finden Sie unter [Erste Schritte mit Azure DNS mithilfe der Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span><span class="sxs-lookup"><span data-stu-id="c3a61-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span></span>

## <a name="management-api"></a><span data-ttu-id="c3a61-108">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="c3a61-108">Management API</span></span>

<span data-ttu-id="c3a61-109">Erstellen Sie mit der Verwaltungs-API DNS-Zonen, und fügen Sie Einträge zu Zonen hinzu.</span><span class="sxs-lookup"><span data-stu-id="c3a61-109">Create DNS zones and add records to zones with the management API.</span></span>

<span data-ttu-id="c3a61-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="c3a61-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="c3a61-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="c3a61-111">Example</span></span>

<span data-ttu-id="c3a61-112">Erstellen einer DNS-Stammzone und Hinzufügen eines `www`-CNAME-Eintrags in einer vorhandenen Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="c3a61-112">Create a root DNS zone and add a `www` CNAME record in an existing resource group.</span></span>

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3a61-113">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="c3a61-113">Explore the Management APIs</span></span>](/java/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="c3a61-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="c3a61-114">Samples</span></span>

[<span data-ttu-id="c3a61-115">Hosten und Verwalten von Domänen mit Azure DNS</span><span class="sxs-lookup"><span data-stu-id="c3a61-115">Host and manage your domains with Azure DNS</span></span>](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

<span data-ttu-id="c3a61-116">Sehen Sie sich weitere [Java-Codebeispiele für Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c3a61-116">Explore more [sample Java code for Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) you can use in your apps.</span></span>

<!---Loc Comment: Please, refer to conversation section to check the issue. Thanks.--->
