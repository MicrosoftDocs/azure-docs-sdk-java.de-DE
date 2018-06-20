---
title: Verwalten von Pools für elastische SQL-Datenbanken mit Java | Microsoft-Dokumentation
description: Beispielcode zum Erstellen und Konfigurieren von Azure SQL-Datenbanken mithilfe des Azure SDKs für Java
author: rloutlaw
manager: douge
ms.assetid: 9b461de8-46bc-4650-8e9e-59531f4e2a53
ms.topic: article
ms.service: Azure
ms.devlang: java
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 9ec0cf3083b8659fa850b798ca0ecf18b2757234
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931116"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a><span data-ttu-id="52455-103">Verwalten von Azure SQL-Datenbanken in Pools für elastische Datenbanken über Ihre Java-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="52455-103">Manage Azure SQL databases in elastic pools from your Java applications</span></span>

<span data-ttu-id="52455-104">[Dieses Beispiel](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) erstellt einen SQL-Datenbankserver mit einem [Pool für elastische Datenbanken](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) zur Verwaltung und Skalierung von Ressourcen für mehrere Datenbanken in einem einzelnen Plan.</span><span class="sxs-lookup"><span data-stu-id="52455-104">[This sample](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) creates a SQL database server with an [elastic pool](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to manage and scale resources for mulitple databases in a single plan.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="52455-105">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="52455-105">Run the sample</span></span>

<span data-ttu-id="52455-106">Erstellen Sie eine [Authentifizierungsdatei](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), und legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Datei auf Ihrem Computer fest.</span><span class="sxs-lookup"><span data-stu-id="52455-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="52455-107">Führen Sie anschließend Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="52455-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

[<span data-ttu-id="52455-108">Sehen Sie sich das vollständige Codebeispiel auf GitHub an.</span><span class="sxs-lookup"><span data-stu-id="52455-108">View the complete code sample on GitHub</span></span>](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)

## <a name="authenticate-with-azure"></a><span data-ttu-id="52455-109">Authentifizieren über Azure</span><span class="sxs-lookup"><span data-stu-id="52455-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a><span data-ttu-id="52455-110">Erstellen eines SQL-Datenbankservers mit einem Pool für elastische Datenbanken</span><span class="sxs-lookup"><span data-stu-id="52455-110">Create a SQL database server with an elastic pool</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    // Use ElasticPoolEditions.STANDARD as the edition
                    // and create two databases
                    .withNewElasticPool(elasticPoolName, ElasticPoolEditions.STANDARD, 
                        database1Name, database2Name)
                    .create();
```

<span data-ttu-id="52455-111">Aktuelle Editionswerte finden Sie in der [ElasticPoolEditions-Klassenreferenz](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions).</span><span class="sxs-lookup"><span data-stu-id="52455-111">See the [ElasticPoolEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) for current edition values.</span></span> <span data-ttu-id="52455-112">Die Merkmale der Editionsressourcen können Sie in der [Dokumentation zu Pools für elastische SQL-Datenbanken](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) vergleichen.</span><span class="sxs-lookup"><span data-stu-id="52455-112">Review the [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to compare edition resource characteristics.</span></span> 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a><span data-ttu-id="52455-113">Ändern der DTU-Einstellungen (Database Transaction Unit, Datenübertragungseinheit) in einem Pool für elastische Datenbanken</span><span class="sxs-lookup"><span data-stu-id="52455-113">Change Database Transaction Unit (DTU) settings in an elastic pool</span></span>

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

<span data-ttu-id="52455-114">Weitere Informationen zum Zuweisen von Ressourcen zu SQL-Datenbanken finden Sie in der [Dokumentation zu DTUs und eDTUs](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu).</span><span class="sxs-lookup"><span data-stu-id="52455-114">Review the [DTUs and eDTUs documentation](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) to learn more about allocating resources to SQL databases.</span></span>

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a><span data-ttu-id="52455-115">Erstellen einer neuen Datenbank in einem Pool für elastische Datenbanken</span><span class="sxs-lookup"><span data-stu-id="52455-115">Create a new database and add it to an elastic pool</span></span>

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

<span data-ttu-id="52455-116">In der ersten Anweisung erstellt die API `anotherDatabase` im [S0-Tarif](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers).</span><span class="sxs-lookup"><span data-stu-id="52455-116">The API creates `anotherDatabase` at [S0 tier](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) in the first statement.</span></span> <span data-ttu-id="52455-117">Durch Verschieben von `anotherDatabase` in den Pool für elastische Datenbanken werden die Datenbankressourcen auf der Grundlage der Pooleinstellungen zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="52455-117">Moving `anotherDatabase` to the elastic pool assigns the database resources based on the pool settings.</span></span>

## <a name="remove-a-database-from-an-elastic-pool"></a><span data-ttu-id="52455-118">Entfernen einer Datenbank aus einem Pool für elastische Datenbanken</span><span class="sxs-lookup"><span data-stu-id="52455-118">Remove a database from an elastic pool</span></span>
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

<span data-ttu-id="52455-119">An `withEdition()` übergebbare Werte finden Sie in der [DatabaseEditions-Klassenreferenz](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions).</span><span class="sxs-lookup"><span data-stu-id="52455-119">See the [DatabaseEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) for values to pass to `withEdition()`.</span></span>

## <a name="list-current-database-activities-in-an-elastic-pool"></a><span data-ttu-id="52455-120">Auflisten der aktuellen Datenbankaktivitäten in einem Pool für elastische Datenbanken</span><span class="sxs-lookup"><span data-stu-id="52455-120">List current database activities in an elastic pool</span></span>
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

<span data-ttu-id="52455-121">Zu Datenbankaktivitäten zählen das Verschieben in einen oder aus einem Pool für elastische Datenbanken sowie das Aktualisieren von Datenbanken in einem Pool für elastische Datenbanken.</span><span class="sxs-lookup"><span data-stu-id="52455-121">Database activities include moving a database in or out of an elastic pool and updating databases in an elastic pool.</span></span>


## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="52455-122">Auflisten von Datenbanken in einem elastischen Pool</span><span class="sxs-lookup"><span data-stu-id="52455-122">List databases in an elastic pool</span></span>
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

<span data-ttu-id="52455-123">Sehen Sie sich die Methoden in [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) an, um detailliertere Datenbankabfragen auszuführen.</span><span class="sxs-lookup"><span data-stu-id="52455-123">Review the methods in [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) to query the databases in more detail.</span></span>

## <a name="delete-an-elastic-pool"></a><span data-ttu-id="52455-124">Löschen eines Pools für elastische Datenbanken</span><span class="sxs-lookup"><span data-stu-id="52455-124">Delete an elastic pool</span></span>
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

<span data-ttu-id="52455-125">Der zu löschende Pool für elastische Datenbanken muss leer sein.</span><span class="sxs-lookup"><span data-stu-id="52455-125">The elastic pool must be empty before deleting it.</span></span>

## <a name="sample-code-summary"></a><span data-ttu-id="52455-126">Zusammenfassung des Beispielcodes</span><span class="sxs-lookup"><span data-stu-id="52455-126">Sample code summary.</span></span>

<span data-ttu-id="52455-127">Das Beispiel erstellt eine SQL Server-Instanz mit zwei Datenbanken, die in einem einzelnen Pool für elastische Datenbanken verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="52455-127">The sample creates a SQL server with two databases managed in a single elasic pool.</span></span> <span data-ttu-id="52455-128">Die Ressourcenlimits des Pools für elastische Datenbanken werden aktualisiert, und dem Pool werden anschließend zusätzliche Datenbanken hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="52455-128">The elastic pool resource limits are updated, then additional databases are added to the pool.</span></span> <span data-ttu-id="52455-129">Danach liest der Code die Konfiguration und den Zustand des Pools für elastische Datenbanken.</span><span class="sxs-lookup"><span data-stu-id="52455-129">The code then reads the elastic pool's configuration and state.</span></span> 

<span data-ttu-id="52455-130">Vor dem Beenden des Beispiels werden alle erstellten Ressourcen wieder gelöscht.</span><span class="sxs-lookup"><span data-stu-id="52455-130">The sample deletes all resources it created before exiting.</span></span>

| <span data-ttu-id="52455-131">Im Beispiel verwendete Klasse</span><span class="sxs-lookup"><span data-stu-id="52455-131">Class used in sample</span></span> | <span data-ttu-id="52455-132">Hinweise</span><span class="sxs-lookup"><span data-stu-id="52455-132">Notes</span></span> |
|-------|-------|
| [<span data-ttu-id="52455-133">SqlServer</span><span class="sxs-lookup"><span data-stu-id="52455-133">SqlServer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | <span data-ttu-id="52455-134">Durch die Fluent-Kette `azure.sqlServers().define()...create()` erstellter SQL-Datenbankserver in Azure.</span><span class="sxs-lookup"><span data-stu-id="52455-134">SQL DB server in Azure created by `azure.sqlServers().define()...create()` fluent chain.</span></span> <span data-ttu-id="52455-135">Stellt Methoden zum Erstellen und Verwenden von Datenbanken und von Pools für elastische Datenbanken bereit.</span><span class="sxs-lookup"><span data-stu-id="52455-135">Provides methods to create and work with elastic pools and databases.</span></span> 
| [<span data-ttu-id="52455-136">SqlDatabase</span><span class="sxs-lookup"><span data-stu-id="52455-136">SqlDatabase</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | <span data-ttu-id="52455-137">Clientseitiges Objekt, das eine SQL-Datenbank darstellt.</span><span class="sxs-lookup"><span data-stu-id="52455-137">Client side object representing a SQL database.</span></span> <span data-ttu-id="52455-138">Erstellt durch `sqlServer().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="52455-138">Created through `sqlServer().define()...create()`.</span></span> 
| [<span data-ttu-id="52455-139">DatabaseEditions</span><span class="sxs-lookup"><span data-stu-id="52455-139">DatabaseEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | <span data-ttu-id="52455-140">Konstante statische Felder zum Festlegen von Datenbankressourcen beim Erstellen einer Datenbank außerhalb eines Pools für elastische Datenbanken oder beim Verschieben einer Datenbank aus einem Pool für elastische Datenbanken.</span><span class="sxs-lookup"><span data-stu-id="52455-140">Constant static fields used to set database resources when creating a database outside of an elastic pool or when moving a database out of an elastic pool</span></span>  
| [<span data-ttu-id="52455-141">SqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="52455-141">SqlElasticPool</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | <span data-ttu-id="52455-142">Wird auf der Grundlage des Abschnitts `withNewElasticPool()` der Fluent-Kette erstellt, die die SQL Server-Instanz in Azure erstellt hat.</span><span class="sxs-lookup"><span data-stu-id="52455-142">Created from the `withNewElasticPool()` section of the fluent chain that created the SqlServer in Azure.</span></span> <span data-ttu-id="52455-143">Stellt Methoden zum Festlegen der Ressourcenlimits bereit, die für Datenbanken, die im Pool für elastische Datenbanken ausgeführt werden, und für den eigentlichen Pool für elastische Datenbanken gelten.</span><span class="sxs-lookup"><span data-stu-id="52455-143">Provides methods to set resource limits for databases running in the elastic pool and for the elastic pool itself.</span></span> 
| [<span data-ttu-id="52455-144">ElasticPoolEditions</span><span class="sxs-lookup"><span data-stu-id="52455-144">ElasticPoolEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | <span data-ttu-id="52455-145">Klasse konstanter Felder zum Definieren der verfügbaren Ressourcen für einen Pool für elastische Datenbanken.</span><span class="sxs-lookup"><span data-stu-id="52455-145">Class of constant fields defining the resources available to an elastic pool.</span></span> <span data-ttu-id="52455-146">Tarifdetails finden Sie in der [Dokumentation zu Pools für elastische SQL-Datenbanken](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="52455-146">See [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) for tier details.</span></span> 
| [<span data-ttu-id="52455-147">ElasticPoolDatabaseActivity</span><span class="sxs-lookup"><span data-stu-id="52455-147">ElasticPoolDatabaseActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | <span data-ttu-id="52455-148">Abgerufen aus `SqlElasticPool.listDatabaseActivities()`.</span><span class="sxs-lookup"><span data-stu-id="52455-148">Retreived from `SqlElasticPool.listDatabaseActivities()`.</span></span> <span data-ttu-id="52455-149">Jedes Objekt dieses Typs stellt eine Aktivität dar, die für eine Datenbank im Pool für elastische Datenbanken ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="52455-149">Each object of this type represents an activity performed on a database in the elastic pool.</span></span>
| [<span data-ttu-id="52455-150">ElasticPoolActivity</span><span class="sxs-lookup"><span data-stu-id="52455-150">ElasticPoolActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | <span data-ttu-id="52455-151">Abgerufen in einer Liste aus `SqlElasticPool.listActivities()`.</span><span class="sxs-lookup"><span data-stu-id="52455-151">Retrieved in a List from `SqlElasticPool.listActivities()`.</span></span> <span data-ttu-id="52455-152">Jedes Objekt in der Liste stellt eine Aktivität dar, die für den Pool für elastische Datenbanken (nicht für die Datenbanken im Pool) ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="52455-152">Each of object in the list represents an activity performed on the elastic pool (not the databases in the elastic pool).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52455-153">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="52455-153">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]