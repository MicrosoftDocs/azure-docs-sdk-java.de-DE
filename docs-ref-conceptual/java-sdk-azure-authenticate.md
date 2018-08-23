---
title: Authentifizieren bei den Azure-Verwaltungsbibliotheken für Java
description: Authentifizieren mit einem Dienstprinzipal bei den Azure-Verwaltungsbibliotheken für Java
keywords: Azure, Java, SDK, API, Maven, Gradle, Authentifizierung, Active Directory, Dienstprinzipal
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 10f457e3-578b-4655-8cd1-51339226ee7d
ms.openlocfilehash: 88354039ad98050f5dee2e7eeadf7f399cd36014
ms.sourcegitcommit: 0f38ef9ad64cffdb7b2e9e966224dfd0af251b0f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703383"
---
# <a name="authenticate-with-the-azure-libraries-for-java"></a>Authentifizieren bei den Azure-Bibliotheken für Java 

## <a name="connect-to-services-with-connection-strings"></a>Herstellen einer Verbindung mit Diensten mit Verbindungszeichenfolgen

Die meisten Azure-Dienstbibliotheken verwenden eine Verbindungszeichenfolge oder einen sicheren Schlüssel für die Authentifizierung. SQL-Datenbank enthält beispielsweise Benutzernamen-und Kennwortinformationen in der JDBC-Verbindungszeichenfolge:

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

Azure Storage nutzt einen Speicherschlüssel zum Autorisieren der Anwendung:

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

Dienstverbindungszeichenfolgen werden zum Authentifizieren bei anderen Azure-Diensten wie [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) und [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues) verwendet. Die Verbindungszeichenfolgen können mithilfe des Azure-Portals oder der CLI abgerufen werden.  Sie können auch die Azure-Verwaltungsbibliotheken für Java zum Abfragen von Ressourcen verwenden, um Verbindungszeichenfolgen in Ihrem Code zu erstellen. 

Dieser Code verwendet beispielsweise die Verwaltungsbibliotheken, um eine Verbindungszeichenfolge für ein Speicherkonto zu erstellen:

```java
// create a new storage account
StorageAccount storage = azure.storageAccounts().getByResourceGroup("myResourceGroup","myStorageAccount");

// create a storage container to hold the file
List<StorageAccountKey> keys = storage.getKeys();
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.name()
        + ";AccountKey=" + keys.get(0).value()
        + ";EndpointSuffix=core.windows.net";
```

Bei anderen Bibliotheken muss Ihre Anwendung mit einem [Dienstprinzipal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) ausgeführt werden, der die Ausführung der Anwendung mit erteilten Anmeldeinformationen autorisiert. Diese Konfiguration ist vergleichbar mit den objektbasierten Authentifizierungsschritten für die unten aufgeführte Verwaltungsbibliothek.

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a>Authentifizieren bei den Azure-Verwaltungsbibliotheken für Java

Wenn Sie mithilfe der Java-Verwaltungsbibliotheken Ressourcen erstellen und verwalten, stehen zwei Optionen zum Authentifizieren Ihrer Anwendung bei Azure zur Verfügung.

### <a name="authenticate-with-an-applicationtokencredentials-object"></a>Authentifizieren mit einem ApplicationTokenCredentials-Objekt

Erstellen Sie eine Instanz von `ApplicationTokenCredentials`, um für das `Azure`-Objekt der obersten Ebene die Dienstprinzipal-Anmeldeinformationen aus Ihrem Code bereitzustellen.

```java
import com.microsoft.azure.credentials.ApplicationTokenCredentials;
import com.microsoft.azure.AzureEnvironment;

// ...

ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(client, 
        tenant,
        key, 
        AzureEnvironment.AZURE);
        
Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credentials)
        .withDefaultSubscription();
```

`client`, `tenant` und `key` sind die gleichen Dienstprinzipalwerte, die auch bei der [dateibasierten Authentifizierung](#mgmt-file) verwendet werden. Der `AzureEnvironment.AZURE`-Wert erstellt Anmeldeinformationen für die öffentliche Azure-Cloud. Ändern Sie diesen Wert, wenn Sie auf eine andere Cloud (etwa `AzureEnvironment.AZURE_GERMANY`) zugreifen müssen.  

 Lesen Sie die Dienstprinzipalwerte aus Umgebungsvariablen oder einem Geheimnisverwaltungsspeicher wie [Key Vault](/azure/key-vault/key-vault-whatis) ein. Legen Sie diese Werte nicht als Klartextzeichenfolgen in Ihrem Code fest, damit Anmeldeinformationen nicht versehentlich im Versionskontrollverlauf verfügbar gemacht werden.   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a>Dateibasierte Authentifizierung (Vorschau)

Die einfachste Authentifizierungsmethode besteht in der Erstellung einer Eigenschaftendatei mit Anmeldeinformationen für einen [Azure-Dienstprinzipal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) im folgenden Format:

```text
# sample management library properties file
subscription=########-####-####-####-############
client=########-####-####-####-############
key=XXXXXXXXXXXXXXXX
tenant=########-####-####-####-############
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

- subscription: Verwenden Sie den *id*-Wert aus `az account show` in der Azure CLI 2.0.
- client: Verwenden Sie den *appId*-Wert aus der Ausgabe eines Dienstprinzipals, der zum Ausführen der Anwendung erstellt wurde. Wenn kein Dienstprinzipal für Ihre App vorhanden ist, [erstellen Sie einen mit der Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).
- key: Verwenden Sie den *password*-Wert aus der CLI-Ausgabe zur Erstellung des Dienstprinzipals. 
- tenant: Verwenden Sie den *tenant*-Wert aus der CLI-Ausgabe zur Erstellung des Dienstprinzipals.

Speichern Sie diese Datei an einem sicheren Ort in Ihrem System, an dem sie vom Code gelesen werden kann. Legen Sie eine Umgebungsvariable mit dem vollständigen Pfad zur Datei in der Shell fest:

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Erstellen Sie das Einstiegspunktobjekt `Azure`, um mit der Verwendung der Bibliotheken zu beginnen. Lesen Sie den Speicherort der Eigenschaftendatei über die Umgebungsvariable ein.

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



