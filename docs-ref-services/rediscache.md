---
title: "Redis Cache-Bibliotheken für Java"
description: "Referenzdokumentation für die Java-Clientbibliotheken und -Verwaltungsbibliotheken für Redis Cache"
keywords: "Azure, Java, SDK, API, Cache, Redis, Webcache, Schlüssel-Wert, In-Memory"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: redis-cache
ms.openlocfilehash: 2bba290e16cac638685aa91b435876433fc1ea91
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2017
---
# <a name="redis-cache-libraries-for-java"></a>Redis Cache-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Azure Redis Cache ist ein sicherer, verteilter Schlüssel-Wert-Speicher, der auf dem beliebten Open Source-[Redis](https://redis.io/)-Cache basiert. 

Informationen zu den ersten Schritten mit Azure Redis Cache finden Sie unter [Verwenden von Azure Redis Cache mit Java](/azure/redis-cache/cache-java-get-started).

## <a name="client-library"></a>Clientbibliothek

Mit dem Open Source-[Jedis](https://github.com/xetorthio/jedis)-Client können Sie eine Verbindung mit Azure Redis Cache herstellen und Werte im Cache speichern bzw. daraus abrufen.  

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a>Beispiel

Stellen Sie eine Verbindung mit Azure Redis her, und fügen Sie eine Zeichenfolge in den Cache ein:

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a>Verwaltungs-API

Mit der Verwaltungs-API können Sie Azure Redis-Ressourcen erstellen und skalieren und Zugriffsschlüssel verwalten.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="example"></a>Beispiel

Erstellen einer neuen Azure Redis Cache-Instanz im [Standard-Tarif mit zwei Knoten](https://azure.microsoft.com/services/cache/). 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/rediscache/managementapi)

## <a name="samples"></a>Beispiele

[Verwalten von Azure Redis Cache](https://github.com/Azure-Samples/redis-java-manage-cache)   

Sehen Sie sich weitere [Java-Codebeispiele für Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) an, die Sie in Ihren Apps verwenden können.
