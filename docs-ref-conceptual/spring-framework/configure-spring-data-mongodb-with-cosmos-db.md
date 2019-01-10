---
title: Verwenden der Spring Data-MongoDB-API mit Azure Cosmos DB
description: Erfahren Sie, wie Sie die Spring Data-MongoDB-API mit Azure Cosmos DB verwenden.
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
ms.openlocfilehash: 55fb356820e2cc5eb8d1fe4030053d9e580583af
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992404"
---
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a><span data-ttu-id="d1940-103">Verwenden der Spring Data-MongoDB-API mit Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d1940-103">How to use Spring Data MongoDB API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="d1940-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="d1940-104">Overview</span></span>

<span data-ttu-id="d1940-105">In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen mithilfe der [MongoDB-API für Azure Cosmos DB](/azure/cosmos-db/mongodb-introduction) zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="d1940-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB MongoDB API](/azure/cosmos-db/mongodb-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1940-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="d1940-106">Prerequisites</span></span>

<span data-ttu-id="d1940-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="d1940-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="d1940-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="d1940-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d1940-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="d1940-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="d1940-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="d1940-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="d1940-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="d1940-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="d1940-112">Einen [Git-Client](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="d1940-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="d1940-113">Erstellen eines Azure Cosmos DB-Kontos</span><span class="sxs-lookup"><span data-stu-id="d1940-113">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="d1940-114">Erstellen eines Cosmos DB-Kontos im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="d1940-114">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="d1940-115">Ausführlichere Informationen zum Erstellen von Azure Cosmos DB-Konten finden Sie in der [Dokumentation für Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d1940-115">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="d1940-116">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="d1940-116">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="d1940-117">Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="d1940-117">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Erstellen eines Azure Cosmos DB-Kontos][COSMOSDB01]

1. <span data-ttu-id="d1940-119">Geben Sie die folgenden Informationen an:</span><span class="sxs-lookup"><span data-stu-id="d1940-119">Specify the following information:</span></span>

   - <span data-ttu-id="d1940-120">**Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="d1940-120">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="d1940-121">**Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="d1940-121">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="d1940-122">**Kontoname**: Wählen Sie einen eindeutigen Namen für Ihr Cosmos DB-Konto aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoysmongodb.documents.azure.com*) verwendet.</span><span class="sxs-lookup"><span data-stu-id="d1940-122">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoysmongodb.documents.azure.com*.</span></span>
   - <span data-ttu-id="d1940-123">**API**: Geben Sie für dieses Tutorial `Azure Cosmos DB for MongoDB API` an.</span><span class="sxs-lookup"><span data-stu-id="d1940-123">**API**: Specify `Azure Cosmos DB for MongoDB API` for this tutorial.</span></span>
   - <span data-ttu-id="d1940-124">**Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.</span><span class="sxs-lookup"><span data-stu-id="d1940-124">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Festlegen der Cosmos DB-Kontoeinstellungen][COSMOSDB02]
   
1. <span data-ttu-id="d1940-126">Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Bewerten + erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d1940-126">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="d1940-127">Wenn die Angaben auf der Seite „Überprüfen“ korrekt sind, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d1940-127">If everything looks correct on the review page, click **Create**.</span></span>

   ![Überprüfen der Cosmos DB-Kontoeinstellungen][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a><span data-ttu-id="d1940-129">Abrufen der Verbindungszeichenfolge für das Azure Cosmos DB-Konto</span><span class="sxs-lookup"><span data-stu-id="d1940-129">Retrieve the connection string for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="d1940-130">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="d1940-130">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="d1940-131">Klicken Sie auf **Alle Ressourcen** und anschließend auf das Azure Cosmos DB-Konto, das Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="d1940-131">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Auswählen des Azure Cosmos DB-Kontos][COSMOSDB04]

1. <span data-ttu-id="d1940-133">Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie den Wert im Feld **Primäre Verbindungszeichenfolge**. Diesen Wert verwenden Sie später zum Konfigurieren Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="d1940-133">Click **Connection strings**, and copy the value for the **Primary Connection String** field; you will use that value to configure your application later.</span></span>

   ![Abrufen der Cosmos DB-Verbindungszeichenfolge][COSMOSDB06]

## <a name="configure-the-sample-application"></a><span data-ttu-id="d1940-135">Konfigurieren der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="d1940-135">Configure the sample application</span></span>

1. <span data-ttu-id="d1940-136">Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:</span><span class="sxs-lookup"><span data-stu-id="d1940-136">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. <span data-ttu-id="d1940-137">Erstellen Sie ein Verzeichnis *resources* im Verzeichnis *&lt;Projektstamm&gt;/complete/src/main* des Beispielprojekts und eine Datei *application.properties*  im Verzeichnis *resources*.</span><span class="sxs-lookup"><span data-stu-id="d1940-137">Create a *resources* directory in the *&lt;project root&gt;/complete/src/main* directory of the sample project, and create an *application.properties* file in the *resources* directory.</span></span>

1. <span data-ttu-id="d1940-138">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:</span><span class="sxs-lookup"><span data-stu-id="d1940-138">Open the *application.properties* file in a text editor, and add the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   <span data-ttu-id="d1940-139">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="d1940-139">Where:</span></span>

   | <span data-ttu-id="d1940-140">Parameter</span><span class="sxs-lookup"><span data-stu-id="d1940-140">Parameter</span></span> | <span data-ttu-id="d1940-141">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="d1940-141">Description</span></span> |
   |---|---|
   | `spring.data.mongodb.database` | <span data-ttu-id="d1940-142">Der Name des Cosmos DB-Kontos, das Sie weiter oben in diesem Artikel erstellt haben</span><span class="sxs-lookup"><span data-stu-id="d1940-142">Specifies the name of your Cosmos DB account from earlier in this article.</span></span> |
   | `spring.data.mongodb.uri` | <span data-ttu-id="d1940-143">Die **primäre Verbindungszeichenfolge**, die Sie weiter oben in diesem Artikel kopiert haben</span><span class="sxs-lookup"><span data-stu-id="d1940-143">Specifies the **Primary Connection String** from earlier in this article.</span></span> |

1. <span data-ttu-id="d1940-144">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="d1940-144">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="d1940-145">Verpacken und Testen der Beispielanwendung</span><span class="sxs-lookup"><span data-stu-id="d1940-145">Package and test the sample application</span></span> 

1. <span data-ttu-id="d1940-146">Erstellen Sie die Beispielanwendung mit Maven, und konfigurieren Sie Maven zum Überspringen der Tests. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d1940-146">Build the sample application with Maven, and configure Maven to skip tests; for example:</span></span>

   ```shell
   mvn clean package -DskipTests
   ```

1. <span data-ttu-id="d1940-147">Starten Sie die Beispielanwendung. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d1940-147">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   <span data-ttu-id="d1940-148">Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="d1940-148">Your application should return values like the following:</span></span>

   ```json
   Customers found with findAll():
   -------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   
   Customer found with findByFirstName('Alice'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customers found with findByLastName('Smith'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   ```

## <a name="summary"></a><span data-ttu-id="d1940-149">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="d1940-149">Summary</span></span>

<span data-ttu-id="d1940-150">In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen mithilfe der MongoDB-API für Azure Cosmos DB zu speichern und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="d1940-150">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB MongoDB API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1940-151">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="d1940-151">Next steps</span></span>

<span data-ttu-id="d1940-152">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1940-152">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1940-153">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="d1940-153">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="d1940-154">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d1940-154">Additional Resources</span></span>

<span data-ttu-id="d1940-155">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="d1940-155">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB06]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-06.png
