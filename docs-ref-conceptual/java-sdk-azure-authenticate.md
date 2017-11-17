---
title: "Authentifizieren bei den Azure-Verwaltungsbibliotheken für Java"
description: "Authentifizieren mit einem Dienstprinzipal bei den Azure-Verwaltungsbibliotheken für Java"
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
ms.openlocfilehash: dd1273d5fc79f513e8dae5420eb6a6988d327d58
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="authenticate-with-the-azure-libraries-for-java"></a><span data-ttu-id="687f3-104">Authentifizieren bei den Azure-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="687f3-104">Authenticate with the Azure libraries for Java</span></span> 

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="687f3-105">Herstellen einer Verbindung mit Diensten mit Verbindungszeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="687f3-105">Connect to services with connection strings</span></span>

<span data-ttu-id="687f3-106">Die meisten Azure-Dienstbibliotheken verwenden eine Verbindungszeichenfolge oder einen sicheren Schlüssel für die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="687f3-106">Most Azure service libraries use a connection string or secure key for authentication.</span></span> <span data-ttu-id="687f3-107">SQL-Datenbank enthält beispielsweise Benutzernamen-und Kennwortinformationen in der JDBC-Verbindungszeichenfolge:</span><span class="sxs-lookup"><span data-stu-id="687f3-107">For example, SQL Database includes username and password information in the JDBC connection string:</span></span>

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

<span data-ttu-id="687f3-108">Azure Storage nutzt einen Speicherschlüssel zum Autorisieren der Anwendung:</span><span class="sxs-lookup"><span data-stu-id="687f3-108">Azure Storage uses a storage key to authorize the application:</span></span>

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

<span data-ttu-id="687f3-109">Dienstverbindungszeichenfolgen werden zum Authentifizieren bei anderen Azure-Diensten wie [DocumentDB](https://docs.microsoft.com/azure/documentdb/documentdb-java-application#a-iduseserviceastep-4-using-the-documentdb-service-in-a-java-application), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) und [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues) verwendet.</span><span class="sxs-lookup"><span data-stu-id="687f3-109">Service connection strings are used to authenticate to other Azure services like [DocumentDB](https://docs.microsoft.com/azure/documentdb/documentdb-java-application#a-iduseserviceastep-4-using-the-documentdb-service-in-a-java-application), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started), and [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span></span> <span data-ttu-id="687f3-110">Die Verbindungszeichenfolgen können mithilfe des Azure-Portals oder der CLI abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="687f3-110">You can get the connection strings using the Azure portal or the CLI.</span></span>  <span data-ttu-id="687f3-111">Sie können auch die Azure-Verwaltungsbibliotheken für Java zum Abfragen von Ressourcen verwenden, um Verbindungszeichenfolgen in Ihrem Code zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="687f3-111">You can also use the Azure management libraries for Java to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="687f3-112">Dieser Code verwendet beispielsweise die Verwaltungsbibliotheken, um eine Verbindungszeichenfolge für ein Speicherkonto zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="687f3-112">For example, this code uses the management libraries to create a storage account connection string:</span></span>

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

<span data-ttu-id="687f3-113">Bei anderen Bibliotheken muss Ihre Anwendung mit einem [Dienstprinizpal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) ausgeführt werden, der die Ausführung der Anwendung mit erteilten Anmeldeinformationen autorisiert.</span><span class="sxs-lookup"><span data-stu-id="687f3-113">Other libraries require your application to run with a [service prinicpal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="687f3-114">Diese Konfiguration ist vergleichbar mit den objektbasierten Authentifizierungsschritten für die unten aufgeführte Verwaltungsbibliothek.</span><span class="sxs-lookup"><span data-stu-id="687f3-114">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a><span data-ttu-id="687f3-115">Authentifizieren bei den Azure-Verwaltungsbibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="687f3-115">Authenticate with the Azure management libraries for Java</span></span>

<span data-ttu-id="687f3-116">Wenn Sie mithilfe der Java-Verwaltungsbibliotheken Ressourcen erstellen und verwalten, stehen zwei Optionen zum Authentifizieren Ihrer Anwendung bei Azure zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="687f3-116">Two options are available to authenticate your application with Azure when using the Java management libraries to create and manage resources.</span></span>

### <a name="authenticate-with-an-applicationtokencredentials-object"></a><span data-ttu-id="687f3-117">Authentifizieren mit einem ApplicationTokenCredentials-Objekt</span><span class="sxs-lookup"><span data-stu-id="687f3-117">Authenticate with an ApplicationTokenCredentials object</span></span>

<span data-ttu-id="687f3-118">Erstellen Sie eine Instanz von `ApplicationTokenCredentials`, um für das `Azure`-Objekt der obersten Ebene die Dienstprinzipal-Anmeldeinformationen aus Ihrem Code bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="687f3-118">Create an instance of `ApplicationTokenCredentials` to supply the service principal credentials to the top-level `Azure` object from inside your code.</span></span>

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

<span data-ttu-id="687f3-119">`client`, `tenant` und `key` sind die gleichen Dienstprinzipalwerte, die auch bei der [dateibasierten Authentifizierung](#mgmt-file) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="687f3-119">The `client`, `tenant` and `key` are the same service principal values used with [file-based authentication](#mgmt-file).</span></span> <span data-ttu-id="687f3-120">Der `AzureEnvironment.AZURE`-Wert erstellt Anmeldeinformationen für die öffentliche Azure-Cloud.</span><span class="sxs-lookup"><span data-stu-id="687f3-120">The `AzureEnvironment.AZURE` value creates credentials against the Azure public cloud.</span></span> <span data-ttu-id="687f3-121">Ändern Sie diesen Wert, wenn Sie auf eine andere Cloud (etwa `AzureEnvironment.AZURE_GERMANY`) zugreifen müssen.</span><span class="sxs-lookup"><span data-stu-id="687f3-121">Change this to a different value if you need to access another cloud (for example, `AzureEnvironment.AZURE_GERMANY`).</span></span>  

 <span data-ttu-id="687f3-122">Lesen Sie die Dienstprinzipalwerte aus Umgebungsvariablen oder einem Geheimnisverwaltungsspeicher wie [Key Vault](/azure/key-vault/key-vault-whatis.md) ein.</span><span class="sxs-lookup"><span data-stu-id="687f3-122">Read the service principal values from environment variables or a secret management store like [Key Vault](/azure/key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="687f3-123">Legen Sie diese Werte nicht als Klartextzeichenfolgen in Ihrem Code fest, damit Anmeldeinformationen nicht versehentlich im Versionskontrollverlauf verfügbar gemacht werden.</span><span class="sxs-lookup"><span data-stu-id="687f3-123">Avoid setting these values as cleartext strings in your code to prevent accidentally exposing credentials in your version control history.</span></span>   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a><span data-ttu-id="687f3-124">Dateibasierte Authentifizierung (Vorschau)</span><span class="sxs-lookup"><span data-stu-id="687f3-124">File based authentication (Preview)</span></span>

<span data-ttu-id="687f3-125">Die einfachste Authentifizierungsmethode besteht in der Erstellung einer Eigenschaftendatei mit Anmeldeinformationen für einen [Azure-Dienstprinzipal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) im folgenden Format:</span><span class="sxs-lookup"><span data-stu-id="687f3-125">The simplest way to authenticate is to create a properties file that contains credentials for an [Azure service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) using the following format:</span></span>

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

- <span data-ttu-id="687f3-126">subscription: Verwenden Sie den *id*-Wert aus `az account show` in der Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="687f3-126">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="687f3-127">client: Verwenden Sie den *appId*-Wert aus der Ausgabe eines Dienstprinzipals, der zum Ausführen der Anwendung erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="687f3-127">client: use the *appId* value from the output taken from a service principal created to run the application.</span></span> <span data-ttu-id="687f3-128">Wenn kein Dienstprinzipal für Ihre App vorhanden ist, [erstellen Sie einen mit der Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="687f3-128">If you don't have a service principal for your app, [create one with the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>
- <span data-ttu-id="687f3-129">key: Verwenden Sie den *password*-Wert aus der CLI-Ausgabe zur Erstellung des Dienstprinzipals.</span><span class="sxs-lookup"><span data-stu-id="687f3-129">key: use the *password* value from the service principal create CLI output</span></span> 
- <span data-ttu-id="687f3-130">tenant: Verwenden Sie den *tenant*-Wert aus der CLI-Ausgabe zur Erstellung des Dienstprinzipals.</span><span class="sxs-lookup"><span data-stu-id="687f3-130">tenant: use the *tenant* value from the service principal create CLI output</span></span>

<span data-ttu-id="687f3-131">Speichern Sie diese Datei an einem sicheren Ort in Ihrem System, an dem sie vom Code gelesen werden kann.</span><span class="sxs-lookup"><span data-stu-id="687f3-131">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="687f3-132">Legen Sie eine Umgebungsvariable mit dem vollständigen Pfad zur Datei in der Shell fest:</span><span class="sxs-lookup"><span data-stu-id="687f3-132">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="687f3-133">Erstellen Sie das Einstiegspunktobjekt `Azure`, um mit der Verwendung der Bibliotheken zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="687f3-133">Create the entry point `Azure` object to start working with the libraries.</span></span> <span data-ttu-id="687f3-134">Lesen Sie den Speicherort der Eigenschaftendatei über die Umgebungsvariable ein.</span><span class="sxs-lookup"><span data-stu-id="687f3-134">Read the location of the properties file through the environment variable.</span></span>

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



