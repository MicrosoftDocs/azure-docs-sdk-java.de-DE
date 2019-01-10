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
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a>Verwenden der Spring Data-MongoDB-API mit Azure Cosmos DB

## <a name="overview"></a>Übersicht

In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen mithilfe der [MongoDB-API für Azure Cosmos DB](/azure/cosmos-db/mongodb-introduction) zu speichern und abzurufen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher
* Einen [Git-Client](https://git-scm.com/downloads)

## <a name="create-an-azure-cosmos-db-account"></a>Erstellen eines Azure Cosmos DB-Kontos

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a>Erstellen eines Cosmos DB-Kontos im Azure-Portal

> [!NOTE]
> 
> Ausführlichere Informationen zum Erstellen von Azure Cosmos DB-Konten finden Sie in der [Dokumentation für Azure Cosmos DB](/azure/cosmos-db/).

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **+ Ressource erstellen**, auf **Datenbanken** und dann auf **Azure Cosmos DB**.

   ![Erstellen eines Azure Cosmos DB-Kontos][COSMOSDB01]

1. Geben Sie die folgenden Informationen an:

   - **Abonnement**: Geben Sie das Azure-Abonnement an, das Sie verwenden möchten.
   - **Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, oder wählen Sie eine vorhandene Ressourcengruppe aus.
   - **Kontoname**: Wählen Sie einen eindeutigen Namen für Ihr Cosmos DB-Konto aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoysmongodb.documents.azure.com*) verwendet.
   - **API**: Geben Sie für dieses Tutorial `Azure Cosmos DB for MongoDB API` an.
   - **Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.

   ![Festlegen der Cosmos DB-Kontoeinstellungen][COSMOSDB02]
   
1. Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Bewerten + erstellen**.

1. Wenn die Angaben auf der Seite „Überprüfen“ korrekt sind, klicken Sie auf **Erstellen**.

   ![Überprüfen der Cosmos DB-Kontoeinstellungen][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a>Abrufen der Verbindungszeichenfolge für das Azure Cosmos DB-Konto

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **Alle Ressourcen** und anschließend auf das Azure Cosmos DB-Konto, das Sie gerade erstellt haben.

   ![Auswählen des Azure Cosmos DB-Kontos][COSMOSDB04]

1. Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie den Wert im Feld **Primäre Verbindungszeichenfolge**. Diesen Wert verwenden Sie später zum Konfigurieren Ihrer Anwendung.

   ![Abrufen der Cosmos DB-Verbindungszeichenfolge][COSMOSDB06]

## <a name="configure-the-sample-application"></a>Konfigurieren der Beispielanwendung

1. Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. Erstellen Sie ein Verzeichnis *resources* im Verzeichnis *&lt;Projektstamm&gt;/complete/src/main* des Beispielprojekts und eine Datei *application.properties*  im Verzeichnis *resources*.

1. Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `spring.data.mongodb.database` | Der Name des Cosmos DB-Kontos, das Sie weiter oben in diesem Artikel erstellt haben |
   | `spring.data.mongodb.uri` | Die **primäre Verbindungszeichenfolge**, die Sie weiter oben in diesem Artikel kopiert haben |

1. Speichern und schließen Sie die Datei *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Verpacken und Testen der Beispielanwendung 

1. Erstellen Sie die Beispielanwendung mit Maven, und konfigurieren Sie Maven zum Überspringen der Tests. Beispiel:

   ```shell
   mvn clean package -DskipTests
   ```

1. Starten Sie die Beispielanwendung. Beispiel:

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:

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

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen mithilfe der MongoDB-API für Azure Cosmos DB zu speichern und abzurufen.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.

> [!div class="nextstepaction"]
> [Spring Framework in Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Weitere Ressourcen

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).

<!-- URL List -->

[Azure für Java-Entwickler]: /java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Arbeiten mit Azure DevOps und Java)
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
