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
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a>Verwenden der Spring Data-Apache Cassandra-API mit Azure Cosmos DB

## <a name="overview"></a>Übersicht

In diesem Artikel wird die Erstellung einer Beispielanwendung veranschaulicht, die [Spring Data] verwendet, um Informationen mithilfe der [Cassandra-API für Azure Cosmos DB](/azure/cosmos-db/cassandra-introduction) zu speichern und abzurufen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher
* [cURL](https://curl.haxx.se/) oder ein ähnliches HTTP-Hilfsprogramm zum Testen der Funktionalität
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
   - **Kontoname**: Wählen Sie einen eindeutigen Namen für Ihr Cosmos DB-Konto aus. Dieser Name wird zum Erstellen eines vollqualifizierten Domänennamens (z. B. *wingtiptoyscassandra.documents.azure.com*) verwendet.
   - **API**: Geben Sie für dieses Tutorial `Cassandra` an.
   - **Standort**: Geben Sie die nächstgelegene geografische Region für Ihre Datenbank an.

   ![Festlegen der Cosmos DB-Kontoeinstellungen][COSMOSDB02]
   
1. Nachdem Sie alle oben genannten Informationen eingegeben haben, klicken Sie auf **Bewerten + erstellen**.

1. Wenn die Angaben auf der Seite „Überprüfen“ korrekt sind, klicken Sie auf **Erstellen**.

   ![Überprüfen der Cosmos DB-Kontoeinstellungen][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a>Hinzufügen eines Keyspace zu Ihrem Azure Cosmos DB-Konto

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **Alle Ressourcen** und anschließend auf das Azure Cosmos DB-Konto, das Sie gerade erstellt haben.

   ![Auswählen des Azure Cosmos DB-Kontos][COSMOSDB04]

1. Klicken Sie auf **Daten-Explorer** und anschließend auf **New Keyspace** (Neuer Keyspace). Geben Sie einen eindeutigen Bezeichner für Ihre **Keyspace id** (Keyspace-ID) ein, und klicken Sie dann auf **OK**.

   ![Erstellen eines Cosmos DB-Keyspace][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a>Abrufen der Verbindungseinstellungen für das Azure Cosmos DB-Konto

1. Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.

1. Klicken Sie auf **Alle Ressourcen** und anschließend auf das Azure Cosmos DB-Konto, das Sie gerade erstellt haben.

   ![Auswählen des Azure Cosmos DB-Kontos][COSMOSDB04]

1. Klicken Sie auf **Verbindungszeichenfolgen**, und kopieren Sie die Werte für **Kontaktpunkt**, **Port**, **Benutzername** und **Primäres Kennwort**. Sie verwenden diese Werte später zum Konfigurieren Ihrer Anwendung.

   ![Abrufen der Cosmos DB-Verbindungseinstellungen][COSMOSDB05]

## <a name="configure-the-sample-application"></a>Konfigurieren der Beispielanwendung

1. Öffnen Sie eine Befehlsshell, und klonen Sie das Beispielprojekt wie im folgenden Beispiel gezeigt mit einem Git-Befehl:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. Suchen Sie im Verzeichnis *resources* des Beispielprojekts nach der Datei *application.properties*, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.

1. Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie die folgenden Zeilen in der Datei hinzu, bzw. konfigurieren Sie diese Zeilen. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Werte, die Sie zuvor festgelegt haben:

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `spring.data.cassandra.contact-points` | Der **Kontaktpunkt**, den Sie weiter oben in diesem Artikel kopiert haben |
   | `spring.data.cassandra.port` | Der **Port**, den Sie weiter oben in diesem Artikel kopiert haben |
   | `spring.data.cassandra.username` | Der **Benutzername**, den Sie weiter oben in diesem Artikel kopiert haben |
   | `spring.data.cassandra.password` | Das **primäre Kennwort**, das Sie weiter oben in diesem Artikel kopiert haben |

1. Speichern und schließen Sie die Datei *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Verpacken und Testen der Beispielanwendung 

1. Erstellen Sie die Beispielanwendung mit Maven. Beispiel:

   ```shell
   mvn clean package
   ```

1. Starten Sie die Beispielanwendung. Beispiel:

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. Erstellen Sie wie in den folgenden Beispielen dargestellt über eine Eingabeaufforderung mit `curl` neue Datensätze:

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. Rufen Sie wie im folgenden Beispiel dargestellt über eine Eingabeaufforderung mit `curl` alle vorhandenen Datensätze ab:

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   Ihre Anwendung sollte Werte zurückgeben, die dem folgenden Beispiel ähneln:

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie eine Java-Beispielanwendung erstellt, die Spring Data verwendet, um Informationen mithilfe der Cassandra-API für Azure Cosmos DB zu speichern und abzurufen.

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

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
