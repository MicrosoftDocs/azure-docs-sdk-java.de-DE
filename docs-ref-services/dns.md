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
ms.openlocfilehash: 7b4f26fe6d99620207e3a53c8262180cccc66fd6
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Azure Traffic Manager-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Mit [Azure DNS](/azure/dns/dns-overview) können Sie die Auflösung des Domänennamens bereitstellen und DNS-Ressourceneinträge mithilfe der gleichen Anmeldeinformationen, APIs, Tools und Abrechnung wie für die anderen Azure-Dienste verwalten.

Informationen zu den ersten Schritten mit Azure DNS finden Sie unter [Erste Schritte mit Azure DNS mithilfe der Azure CLI 2.0](/azure/dns/dns-getstarted-cli).

## <a name="management-api"></a>Verwaltungs-API

Erstellen Sie mit der Verwaltungs-API DNS-Zonen, und fügen Sie Einträge zu Zonen hinzu.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.1.2</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Erstellen einer DNS-Stammzone und Hinzufügen eines `www`-CNAME-Eintrags in einer vorhandenen Ressourcengruppe

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/dns/managementapi)

## <a name="samples"></a>Beispiele

[Hosten und Verwalten von Domänen mit Azure DNS](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

Sehen Sie sich weitere [Java-Codebeispiele für Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) an, die Sie in Ihren Apps verwenden können.