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
# <a name="redis-cache-libraries-for-java"></a><span data-ttu-id="44820-104">Redis Cache-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="44820-104">Redis Cache libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="44820-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="44820-105">Overview</span></span>

<span data-ttu-id="44820-106">Azure Redis Cache ist ein sicherer, verteilter Schlüssel-Wert-Speicher, der auf dem beliebten Open Source-[Redis](https://redis.io/)-Cache basiert.</span><span class="sxs-lookup"><span data-stu-id="44820-106">Azure Redis Cache is a secure, distributed key-value store based on the popular open source [Redis](https://redis.io/) cache.</span></span> 

<span data-ttu-id="44820-107">Informationen zu den ersten Schritten mit Azure Redis Cache finden Sie unter [Verwenden von Azure Redis Cache mit Java](/azure/redis-cache/cache-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="44820-107">To get started with Azure Redis Cache, see [How to use Azure Redis Cache with Java](/azure/redis-cache/cache-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="44820-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="44820-108">Client library</span></span>

<span data-ttu-id="44820-109">Mit dem Open Source-[Jedis](https://github.com/xetorthio/jedis)-Client können Sie eine Verbindung mit Azure Redis Cache herstellen und Werte im Cache speichern bzw. daraus abrufen.</span><span class="sxs-lookup"><span data-stu-id="44820-109">Connect to Azure Redis Cache and store and retrieve values from the cache using the open-source [Jedis](https://github.com/xetorthio/jedis) client.</span></span>  

<span data-ttu-id="44820-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="44820-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a><span data-ttu-id="44820-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="44820-111">Example</span></span>

<span data-ttu-id="44820-112">Stellen Sie eine Verbindung mit Azure Redis her, und fügen Sie eine Zeichenfolge in den Cache ein:</span><span class="sxs-lookup"><span data-stu-id="44820-112">Connect to Azure Redis and insert a string into the cache.</span></span>

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a><span data-ttu-id="44820-113">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="44820-113">Management API</span></span>

<span data-ttu-id="44820-114">Mit der Verwaltungs-API können Sie Azure Redis-Ressourcen erstellen und skalieren und Zugriffsschlüssel verwalten.</span><span class="sxs-lookup"><span data-stu-id="44820-114">Create and scale Azure Redis resources and manage access keys to with the management API.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="44820-115">Beispiel</span><span class="sxs-lookup"><span data-stu-id="44820-115">Example</span></span>

<span data-ttu-id="44820-116">Erstellen einer neuen Azure Redis Cache-Instanz im [Standard-Tarif mit zwei Knoten](https://azure.microsoft.com/services/cache/).</span><span class="sxs-lookup"><span data-stu-id="44820-116">Create a new Azure Redis Cache in the [two-node standard tier](https://azure.microsoft.com/services/cache/).</span></span> 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="44820-117">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="44820-117">Explore the Management APIs</span></span>](/java/api/overview/azure/rediscache/managementapi)

## <a name="samples"></a><span data-ttu-id="44820-118">Beispiele</span><span class="sxs-lookup"><span data-stu-id="44820-118">Samples</span></span>

[<span data-ttu-id="44820-119">Verwalten von Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="44820-119">Manage Azure Redis Cache</span></span>](https://github.com/Azure-Samples/redis-java-manage-cache)   

<span data-ttu-id="44820-120">Sehen Sie sich weitere [Java-Codebeispiele für Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="44820-120">Explore more [sample Java code for Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) you can use in your apps.</span></span>
