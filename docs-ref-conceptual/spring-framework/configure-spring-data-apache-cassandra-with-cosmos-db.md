---
title: Verwenden der Spring Data-Apache Cassandra-API mit Azure Cosmos DB
description: Erfahren Sie, wie Sie die Spring Data-Apache Cassandra-API mit Azure Cosmos DB verwenden.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 1f3f7a55b49d64077df9e7d4d6acc3af4495b424
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992325"
---
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a><span data-ttu-id="05341-103">Verwenden der Spring Data-Apache Cassandra-API mit Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="05341-103">How to use Spring Data Apache Cassandra API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="05341-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="05341-104">Overview</span></span>

<span data-ttu-id="05341-105">In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen mithilfe der [Cassandra-API für Azure Cosmos DB](/azure/cosmos-db/cassandra-introduction) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="05341-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB Cassandra API](/azure/cosmos-db/cassandra-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05341-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="05341-106">Prerequisites</span></span>

<span data-ttu-id="05341-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="05341-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="05341-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="05341-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="05341-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="05341-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="05341-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="05341-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="05341-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="05341-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="05341-112">[cURL](https://curl.haxx.se/) oder ein ähnliches HTTP-Hilfsprogramm zum Testen der Funktionalität</span><span class="sxs-lookup"><span data-stu-id="05341-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="05341-113">Einen [Git-Client](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="05341-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="05341-114">Erstellen eines Azure Cosmos DB-Kontos</span><span class="sxs-lookup"><span data-stu-id="05341-114">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="05341-115">Erstellen eines Cosmos DB-Kontos im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="05341-115">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="05341-116">Ausführlichere Informationen zum Erstellen von Azure Cosmos DB-Konten finden Sie in der [Dokumentation für Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="05341-116">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="05341-117">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="05341-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="05341-118">Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="05341-118">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Erstellen eines Azure Cosmos DB-Kontos][COSMOSDB01]

1. <span data-ttu-id="05341-120">Geben Sie die folgenden Informationen an:</span><span class="sxs-lookup"><span data-stu-id="05341-120">Specify the following information:</span></span>

   - <span data-ttu-id="05341-121">**Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="05341-121">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="05341-122">**Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="05341-122">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="05341-123">**Kontoname**: Wählen Sie einen eindeutigen Namen für Ihr Cosmos DB-Konto aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoyscassandra.documents.azure.com*) verwendet.</span><span class="sxs-lookup"><span data-stu-id="05341-123">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoyscassandra.documents.azure.com*.</span></span>
   - <span data-ttu-id="05341-124">**API**: Geben Sie für dieses Tutorial `Cassandra` an.</span><span class="sxs-lookup"><span data-stu-id="05341-124">**API**: Specify `Cassandra` for this tutorial.</span></span>
   - <span data-ttu-id="05341-125">**Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="05341-125">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Festlegen der Cosmos DB-Kontoeinstellungen][COSMOSDB02]
   
1. <span data-ttu-id="05341-127">Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Bewerten + erstellen**.</span><span class="sxs-lookup"><span data-stu-id="05341-127">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="05341-128">Wenn die Angaben auf der Seite „Überprüfen“ korrekt sind, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="05341-128">If everything looks correct on the review page, click **Create**.</span></span>

   ![Überprüfen der Cosmos DB-Kontoeinstellungen][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a><span data-ttu-id="05341-130">Hinzufügen eines Keyspace zu Ihrem Azure Cosmos DB-Konto</span><span class="sxs-lookup"><span data-stu-id="05341-130">Add a keyspace to your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="05341-131">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="05341-131">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="05341-132">Klicken Sie auf **Alle Ressourcen** und anschließend auf das Azure Cosmos DB-Konto, das Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="05341-132">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Auswählen des Azure Cosmos DB-Kontos][COSMOSDB04]

1. <span data-ttu-id="05341-134">Klicken Sie auf **Daten-Explorer** und anschließend auf **New Keyspace** (Neuer Keyspace).</span><span class="sxs-lookup"><span data-stu-id="05341-134">Click **Data Explorer**, then click **New Keyspace**.</span></span> <span data-ttu-id="05341-135">Geben Sie einen eindeutigen Bezeichner für Ihre **Keyspace id** (Keyspace-ID) ein, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="05341-135">Enter a unique identifier for your **Keyspace id**, then click **OK**.</span></span>

   ![Erstellen eines Cosmos DB-Keyspace][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a><span data-ttu-id="05341-137">Abrufen der Verbindungseinstellungen für das Azure Cosmos DB-Konto</span><span class="sxs-lookup"><span data-stu-id="05341-137">Retrieve the connection settings for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="05341-138">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="05341-138">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="05341-139">Klicken Sie auf **Alle Ressourcen** und anschließend auf das Azure Cosmos DB-Konto, das Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="05341-139">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Auswählen des Azure Cosmos DB-Kontos][COSMOSDB04]

1. <span data-ttu-id="05341-141">Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie die Werte für **Kontaktpunkt**, **Port**, **Benutzername** und **Primäres Kennwort**. Sie verwenden diese Werte später zum Konfigurieren Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="05341-141">Click **Connection strings**, and copy the values for the **Contact Point**, **Port**, **Username**, and **Primary Password** fields; you will use those values to configure your application later.</span></span>

   ![Abrufen der Cosmos DB-Verbindungseinstellungen][COSMOSDB05]

## <a name="configure-the-sample-application"></a><span data-ttu-id="05341-143">Konfigurieren der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="05341-143">Configure the sample application</span></span>

1. <span data-ttu-id="05341-144">Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:</span><span class="sxs-lookup"><span data-stu-id="05341-144">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. <span data-ttu-id="05341-145">Suchen Sie im Verzeichnis *resources* des Beispielprojekts nach der Datei *application.properties*, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="05341-145">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="05341-146">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu, bzw. konfigurieren Sie diese Zeilen. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:</span><span class="sxs-lookup"><span data-stu-id="05341-146">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   <span data-ttu-id="05341-147">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="05341-147">Where:</span></span>

   | <span data-ttu-id="05341-148">Parameter</span><span class="sxs-lookup"><span data-stu-id="05341-148">Parameter</span></span> | <span data-ttu-id="05341-149">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="05341-149">Description</span></span> |
   |---|---|
   | `spring.data.cassandra.contact-points` | <span data-ttu-id="05341-150">Der **Kontaktpunkt**, den Sie weiter oben in diesem Artikel kopiert haben</span><span class="sxs-lookup"><span data-stu-id="05341-150">Specifies the **Contact Point** from earlier in this article.</span></span> |
   | `spring.data.cassandra.port` | <span data-ttu-id="05341-151">Der **Port**, den Sie weiter oben in diesem Artikel kopiert haben</span><span class="sxs-lookup"><span data-stu-id="05341-151">Specifies the **Port** from earlier in this article.</span></span> |
   | `spring.data.cassandra.username` | <span data-ttu-id="05341-152">Der **Benutzername**, den Sie weiter oben in diesem Artikel kopiert haben</span><span class="sxs-lookup"><span data-stu-id="05341-152">Specifies your **Username** from earlier in this article.</span></span> |
   | `spring.data.cassandra.password` | <span data-ttu-id="05341-153">Das **primäre Kennwort**, das Sie weiter oben in diesem Artikel kopiert haben</span><span class="sxs-lookup"><span data-stu-id="05341-153">Specifies your **Primary Password** from earlier in this article.</span></span> |

1. <span data-ttu-id="05341-154">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="05341-154">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="05341-155">Verpacken und Testen der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="05341-155">Package and test the sample application</span></span> 

1. <span data-ttu-id="05341-156">Erstellen Sie die Beispielanwendung mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="05341-156">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="05341-157">Starten Sie die Beispielanwendung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="05341-157">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="05341-158">Erstellen Sie wie in den folgenden Beispielen dargestellt über eine Eingabeaufforderung mit `curl` neue Datensätze:</span><span class="sxs-lookup"><span data-stu-id="05341-158">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="05341-159">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="05341-159">Your application should return values like the following:</span></span>

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. <span data-ttu-id="05341-160">Rufen Sie wie im folgenden Beispiel dargestellt über eine Eingabeaufforderung mit `curl` alle vorhandenen Datensätze ab:</span><span class="sxs-lookup"><span data-stu-id="05341-160">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="05341-161">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="05341-161">Your application should return values like the following:</span></span>

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="05341-162">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="05341-162">Summary</span></span>

<span data-ttu-id="05341-163">In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen mithilfe der Cassandra-API für Azure Cosmos DB zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="05341-163">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB Cassandra API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05341-164">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="05341-164">Next steps</span></span>

<span data-ttu-id="05341-165">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="05341-165">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="05341-166">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="05341-166">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="05341-167">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="05341-167">Additional Resources</span></span>

<span data-ttu-id="05341-168">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="05341-168">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Azure für Java-Entwickler]: /java/azure/
[Azure for Java Developers]: /java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Arbeiten mit Azure DevOps und Java)
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
