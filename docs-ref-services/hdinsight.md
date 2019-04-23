---
title: Azure HDInsight SDK für Java
description: Referenz zum Azure HDInsight SDK für Java Das HDInsight SDK für Java bietet Klassen und Methoden, mit denen Sie Ihre HDInsight-Cluster verwalten können.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 04/15/2019
ms.openlocfilehash: fe87c9214e2a620230cf2f1f52261fd66a2b8857
ms.sourcegitcommit: f33befab25a66a252b4c91c7aeb1b77cb32821bb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59705118"
---
# <a name="hdinsight-sdk-for-java"></a><span data-ttu-id="a1ce7-104">HDInsight SDK für Java</span><span class="sxs-lookup"><span data-stu-id="a1ce7-104">HDInsight SDK for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a1ce7-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="a1ce7-105">Overview</span></span>

<span data-ttu-id="a1ce7-106">Das HDInsight SDK für Java bietet Klassen und Methoden, mit denen Sie Ihre HDInsight-Cluster verwalten können.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-106">The HDInsight SDK for Java provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="a1ce7-107">Es enthält Vorgänge zum Erstellen, Löschen, Aktualisieren, Auflisten, Ändern der Größe, Ausführen von Skriptaktionen, Überwachen, Abrufen der Eigenschaften von HDInsight-Clustern und mehr.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1ce7-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="a1ce7-108">Prerequisites</span></span>

* <span data-ttu-id="a1ce7-109">Ein Azure-Konto.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-109">An Azure account.</span></span> <span data-ttu-id="a1ce7-110">Falls Sie noch kein Konto haben, können Sie eine [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="a1ce7-111">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="a1ce7-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="a1ce7-112">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* [<span data-ttu-id="a1ce7-113">Maven</span><span class="sxs-lookup"><span data-stu-id="a1ce7-113">Maven</span></span>](https://maven.apache.org/download.cgi)

## <a name="sdk-installation"></a><span data-ttu-id="a1ce7-114">SDK-Installation</span><span class="sxs-lookup"><span data-stu-id="a1ce7-114">SDK Installation</span></span>

<span data-ttu-id="a1ce7-115">Das HDInsight SDK für Java steht über Maven [hier](https://search.maven.org/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-115">The HDInsight SDK for Java is available through Maven [here](https://search.maven.org/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span></span> <span data-ttu-id="a1ce7-116">Fügen Sie Ihrer Datei „pom.xml“ die folgende Abhängigkeit hinzu:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-116">Add the following dependency to your pom.xml:</span></span>

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

<span data-ttu-id="a1ce7-117">Außerdem müssen Sie der Datei „pom.xml“ die folgenden Abhängigkeiten hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-117">You will also need to add the following dependencies to your pom.xml:</span></span>

* [<span data-ttu-id="a1ce7-118">Azure-Clientauthentifizierungsbibliothek:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-118">Azure Client Authentication Library:</span></span>](https://search.maven.org/artifact/com.microsoft.azure/azure-client-authentication)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.5</version>
  </dependency>
  ```

* [<span data-ttu-id="a1ce7-119">Azure Java-Clientruntime für ARM:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-119">Azure Java Client Runtime For ARM:</span></span>](https://search.maven.org/artifact/com.microsoft.azure/azure-arm-client-runtime)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.5</version>
  </dependency>
  ```

## <a name="authentication"></a><span data-ttu-id="a1ce7-120">Authentication</span><span class="sxs-lookup"><span data-stu-id="a1ce7-120">Authentication</span></span>

<span data-ttu-id="a1ce7-121">Das SDK muss zunächst für Ihr Azure-Abonnement authentifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-121">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="a1ce7-122">Erstellen Sie anhand des Beispiels unten einen Dienstprinzipal, und verwenden Sie ihn für die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-122">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="a1ce7-123">Nachdem dies erfolgt ist, verfügen Sie über eine Instanz von `HDInsightManagementClientImpl` mit vielen Methoden (in den Abschnitten unten beschrieben), die zum Durchführen von Verwaltungsvorgängen verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-123">After this is done, you will have an instance of an `HDInsightManagementClientImpl`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="a1ce7-124">Neben dem Beispiel unten gibt es noch andere Möglichkeiten der Authentifizierung, die für Ihre Anforderungen unter Umständen besser geeignet sind.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-124">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="a1ce7-125">Hier werden alle Methoden beschrieben: [Authentifizieren bei den Azure-Verwaltungsbibliotheken für Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span><span class="sxs-lookup"><span data-stu-id="a1ce7-125">All methods are outlined here: [Authenticate with the Azure management libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="a1ce7-126">Beispiel für die Authentifizierung mit einem Dienstprinzipal</span><span class="sxs-lookup"><span data-stu-id="a1ce7-126">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="a1ce7-127">Melden Sie sich zuerst bei [Azure Cloud Shell](https://shell.azure.com/bash) an.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-127">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="a1ce7-128">Vergewissern Sie sich, dass Sie derzeit das Abonnement verwenden, in dem der Dienstprinzipal erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-128">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="a1ce7-129">Die Informationen zu Ihrem Abonnement werden im JSON-Format angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-129">Your subscription information is displayed as JSON.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

<span data-ttu-id="a1ce7-130">Wenn Sie nicht am richtigen Abonnement angemeldet sind, können Sie das richtige auswählen, indem Sie Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-130">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="a1ce7-131">Falls Sie den HDInsight-Ressourcenanbieter nicht bereits mit einer anderen Methode registriert haben (z.B. durch das Erstellen eines HDInsight-Clusters über das Azure-Portal), müssen Sie dies vor dem Authentifizieren durchführen.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-131">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="a1ce7-132">Dies ist über [Azure Cloud Shell](https://shell.azure.com/bash) möglich, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-132">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="a1ce7-133">Wählen Sie als Nächstes einen Namen für Ihren Dienstprinzipal aus, und erstellen Sie ihn mit dem folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-133">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="a1ce7-134">Die Dienstprinzipalinformationen werden im JSON-Format angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-134">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
<span data-ttu-id="a1ce7-135">Kopieren Sie den unten angegebenen Codeausschnitt, und geben Sie für `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` und `SUBSCRIPTION_ID` die Zeichenfolgen aus dem JSON-Code ein, der nach dem Ausführen des Befehls zurückgegeben wurde, um den Dienstprinzipal zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-135">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

```java
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.*;
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.implementation.HDInsightManagementClientImpl;

public class Main {
    public static void main (String[] args) {

        // Tenant ID for your Azure Subscription
        String TENANT_ID = "";
        // Your Service Principal App Client ID
        String CLIENT_ID = "";
        // Your Service Principal Client Secret
        String CLIENT_SECRET = "";
        // Azure Subscription ID
        String SUBSCRIPTION_ID = "";

        ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(
                CLIENT_ID,
                TENANT_ID,
                CLIENT_SECRET,
                AzureEnvironment.AZURE);

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials)
                .withSubscriptionId(SUBSCRIPTION_ID);
```

## <a name="cluster-management"></a><span data-ttu-id="a1ce7-136">Clusterverwaltung</span><span class="sxs-lookup"><span data-stu-id="a1ce7-136">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="a1ce7-137">In diesem Abschnitt wird davon ausgegangen, dass Sie bereits eine `HDInsightManagementClientImpl`-Instanz authentifiziert und in einer Variablen mit dem Namen `client` gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-137">This section assumes you have already authenticated and constructed an `HDInsightManagementClientImpl` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="a1ce7-138">Eine Anleitung zum Authentifizieren und Abrufen eines `HDInsightManagementClientImpl`-Elements finden Sie oben im Abschnitt „Authentifizierung“.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-138">Instructions for authenticating and obtaining an `HDInsightManagementClientImpl` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="a1ce7-139">Erstellen eines Clusters</span><span class="sxs-lookup"><span data-stu-id="a1ce7-139">Create a Cluster</span></span>

<span data-ttu-id="a1ce7-140">Sie können einen neuen Cluster erstellen, indem Sie `client.clusters().create()` aufrufen.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-140">A new cluster can be created by calling `client.clusters().create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="a1ce7-141">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a1ce7-141">Samples</span></span>

<span data-ttu-id="a1ce7-142">Codebeispiele zum Erstellen verschiedener allgemeiner HDInsight-Clustertypen stehen zur Verfügung: [HDInsight-Java-Beispiele](https://github.com/Azure-Samples/hdinsight-java-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="a1ce7-142">Code samples for creating several common types of HDInsight clusters are available: [HDInsight Java Samples](https://github.com/Azure-Samples/hdinsight-java-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="a1ce7-143">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a1ce7-143">Example</span></span>

<span data-ttu-id="a1ce7-144">In diesem Beispiel wird gezeigt, wie Sie einen Spark-Cluster mit zwei Hauptknoten und einem Workerknoten erstellen.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-144">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="a1ce7-145">Sie müssen zuerst wie unten beschrieben eine Ressourcengruppe und ein Speicherkonto erstellen.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-145">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="a1ce7-146">Wenn Sie diese Komponenten bereits erstellt haben, können Sie diese Schritte überspringen.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-146">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="a1ce7-147">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="a1ce7-147">Creating a Resource Group</span></span>

<span data-ttu-id="a1ce7-148">Sie können eine Ressourcengruppe erstellen, indem Sie mit [Azure Cloud Shell](https://shell.azure.com/bash) Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-148">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="a1ce7-149">Erstellen eines Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="a1ce7-149">Creating a Storage Account</span></span>

<span data-ttu-id="a1ce7-150">Sie können ein Speicherkonto erstellen, indem Sie mit [Azure Cloud Shell](https://shell.azure.com/bash) Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-150">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="a1ce7-151">Führen Sie jetzt den folgenden Befehl aus, um den Schlüssel für Ihr Speicherkonto abzurufen (Sie benötigen ihn, um einen Cluster zu erstellen):</span><span class="sxs-lookup"><span data-stu-id="a1ce7-151">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="a1ce7-152">Der unten stehende Java-Codeausschnitt erstellt einen Spark-Cluster mit zwei Hauptknoten und einem Workerknoten.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-152">The below Java snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="a1ce7-153">Geben Sie gemäß den Anweisungen in den Kommentaren Werte in die leeren Variablen ein, und ändern Sie ggf. auch andere Parameter, um diese an Ihre Anforderungen anzupassen.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-153">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

```java
// The name for the cluster you are creating
String clusterName = "";
// The name of your existing Resource Group
String resourceGroupName = "";
// Choose a username
String username = "";
// Choose a password
String password = "";
// Replace <> with the name of your storage account
String storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
String storageAccountKey = "";
// Choose a region
String location = "";
String container = "default";

HashMap<String, HashMap<String, String>> configurations = new HashMap<String, HashMap<String, String>>();
        HashMap<String, String> gateway = new HashMap<String, String>();
        gateway.put("restAuthCredential.enabled_credential", "True");
        gateway.put("restAuthCredential.username", username);
        gateway.put("restAuthCredential.password", password);
        configurations.put("gateway", gateway);

        ClusterCreateParametersExtended parameters = new ClusterCreateParametersExtended()
            .withLocation(location)
            .withTags(Collections.EMPTY_MAP)
            .withProperties(
                new ClusterCreateProperties()
                    .withClusterVersion("3.6")
                    .withOsType(OSType.LINUX)
                    .withClusterDefinition(new ClusterDefinition()
                            .withKind("spark")
                            .withConfigurations(configurations)
                    )
                    .withTier(Tier.STANDARD)
                    .withComputeProfile(new ComputeProfile()
                        .withRoles(List.of(
                            new Role()
                                .withName("headnode")
                                .withTargetInstanceCount(2)
                                .withHardwareProfile(new HardwareProfile()
                                    .withVmSize("Large")
                                )
                                .withOsProfile(new OsProfile()
                                    .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                    )
                                ),
                            new Role()
                                    .withName("workernode")
                                    .withTargetInstanceCount(1)
                                    .withHardwareProfile(new HardwareProfile()
                                        .withVmSize("Large")
                                    )
                                    .withOsProfile(new OsProfile()
                                        .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                        )
                                    )
                        ))
                    )
                    .withStorageProfile(new StorageProfile()
                        .withStorageaccounts(List.of(
                                new StorageAccount()
                                    .withName(storageAccount)
                                    .withKey(storageAccountKey)
                                    .withContainer(container)
                                    .withIsDefault(true)
                        ))
                    )
            );
        client.clusters().create(resourceGroupName, clusterName, parameters);
```

### <a name="get-cluster-details"></a><span data-ttu-id="a1ce7-154">Abrufen von Clusterdetails</span><span class="sxs-lookup"><span data-stu-id="a1ce7-154">Get Cluster Details</span></span>

<span data-ttu-id="a1ce7-155">Rufen Sie die Eigenschaften für einen Cluster wie folgt ab:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-155">To get properties for a given cluster:</span></span>

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="a1ce7-156">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a1ce7-156">Example</span></span>

<span data-ttu-id="a1ce7-157">Sie können `get` verwenden, um zu bestätigen, dass die Erstellung des Clusters erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-157">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

<span data-ttu-id="a1ce7-158">Die Ausgabe sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-158">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a><span data-ttu-id="a1ce7-159">Auflisten von Clustern</span><span class="sxs-lookup"><span data-stu-id="a1ce7-159">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="a1ce7-160">Auflisten von Clustern unter dem Abonnement</span><span class="sxs-lookup"><span data-stu-id="a1ce7-160">List Clusters Under The Subscription</span></span>

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="a1ce7-161">Auflisten von Clustern nach Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="a1ce7-161">List Clusters By Resource Group</span></span>

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="a1ce7-162">Sowohl `List()` als auch `ListByResourceGroup()` geben ein `PagedList<ClusterInner>`-Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-162">Both `List()` and `ListByResourceGroup()` return a `PagedList<ClusterInner>` object.</span></span> <span data-ttu-id="a1ce7-163">Wenn Sie `loadNext()` aufrufen, wird eine Liste der Cluster auf dieser Seite zurückgegeben und das `ClusterPaged`-Objekt auf der nächsten Seite fortgesetzt.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-163">Calling `loadNext()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="a1ce7-164">Dies kann wiederholt werden, bis `false` für `hasNextPage()` zurückgegeben wird (d. h. es sind keine Seiten mehr vorhanden).</span><span class="sxs-lookup"><span data-stu-id="a1ce7-164">This can be repeated until `hasNextPage()` return `false`, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="a1ce7-165">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a1ce7-165">Example</span></span>

<span data-ttu-id="a1ce7-166">Im folgenden Beispiel werden die Eigenschaften aller Cluster für das aktuelle Abonnement ausgegeben:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-166">The following example prints the properties of all clusters for the current subscription:</span></span>

```java
PagedList<ClusterInner> clusterPages = client.clusters().list();
while (true) {
    for (ClusterInner cluster : clusterPages.currentPage().items()) {
        System.out.println(cluster.name());
    }
    if (clusterPages.hasNextPage()) {
        clusterPages.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="delete-a-cluster"></a><span data-ttu-id="a1ce7-167">Löschen eines Clusters</span><span class="sxs-lookup"><span data-stu-id="a1ce7-167">Delete a Cluster</span></span>

<span data-ttu-id="a1ce7-168">Löschen Sie einen Cluster wie folgt:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-168">To delete a cluster:</span></span>

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="a1ce7-169">Aktualisieren von Clustermarkierungen</span><span class="sxs-lookup"><span data-stu-id="a1ce7-169">Update Cluster Tags</span></span>

<span data-ttu-id="a1ce7-170">Sie können die Markierungen eines Clusters wie folgt aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-170">You can update the tags of a given cluster like so:</span></span>

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a><span data-ttu-id="a1ce7-171">Ändern der Clustergröße</span><span class="sxs-lookup"><span data-stu-id="a1ce7-171">Resize Cluster</span></span>

<span data-ttu-id="a1ce7-172">Sie können die Anzahl von Workerknoten für einen Cluster ändern, indem Sie wie folgt eine neue Größe angeben:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-172">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="a1ce7-173">Clusterüberwachung</span><span class="sxs-lookup"><span data-stu-id="a1ce7-173">Cluster Monitoring</span></span>

<span data-ttu-id="a1ce7-174">Das HDInsight Management SDK kann auch verwendet werden, um die Überwachung Ihrer Cluster per Operations Management Suite (OMS) zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-174">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="a1ce7-175">Aktivieren der OMS-Überwachung</span><span class="sxs-lookup"><span data-stu-id="a1ce7-175">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="a1ce7-176">Sie müssen über einen vorhandenen Log Analytics-Arbeitsbereich verfügen, um die OMS-Überwachung zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-176">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="a1ce7-177">Wenn Sie noch keinen erstellt haben, erfahren Sie an dieser Stelle, wie Sie dazu vorgehen: [Erstellen eines Log Analytics-Arbeitsbereichs im Azure-Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace)</span><span class="sxs-lookup"><span data-stu-id="a1ce7-177">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="a1ce7-178">Aktivieren Sie die OMS-Überwachung in Ihrem Cluster wie folgt:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-178">To enable OMS Monitoring on your cluster:</span></span>

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="a1ce7-179">Anzeigen des Status der OMS-Überwachung</span><span class="sxs-lookup"><span data-stu-id="a1ce7-179">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="a1ce7-180">Rufen Sie den Status von OMS in Ihrem Cluster wie folgt ab:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-180">To get the status of OMS on your cluster:</span></span>

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="a1ce7-181">Deaktivieren der OMS-Überwachung</span><span class="sxs-lookup"><span data-stu-id="a1ce7-181">Disable OMS Monitoring</span></span>

<span data-ttu-id="a1ce7-182">Deaktivieren Sie OMS in Ihrem Cluster wie folgt:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-182">To disable OMS on your cluster:</span></span>

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="a1ce7-183">Skriptaktionen</span><span class="sxs-lookup"><span data-stu-id="a1ce7-183">Script Actions</span></span>

<span data-ttu-id="a1ce7-184">HDInsight verfügt über eine Konfigurationsmethode mit der Bezeichnung „Skriptaktionen“, mit der benutzerdefinierte Skripts zum Anpassen des Clusters aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-184">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="a1ce7-185">Weitere Informationen zum Verwenden von Skriptaktionen finden Sie hier: [Anpassen Linux-basierter HDInsight-Cluster mithilfe von Skriptaktionen](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="a1ce7-185">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="a1ce7-186">Ausführen von Skriptaktionen</span><span class="sxs-lookup"><span data-stu-id="a1ce7-186">Execute Script Actions</span></span>

<span data-ttu-id="a1ce7-187">Sie können Skriptaktionen für einen Cluster wie folgt ausführen:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-187">You can execute script actions on a given cluster like so:</span></span>

```java
RuntimeScriptAction scriptAction1 = new RuntimeScriptAction()
    .withName("<Script Name>")
    .withUri("<URL To Script>")
    .withRoles(<List<String> of roles>);
client.clusters().executeScriptActions(
    resourceGroupName, 
    clusterName, 
    new ExecuteScriptActionParameters().withPersistOnSuccess(false).withScriptActions(new LinkedList<>(Arrays.asList(scriptAction1)))); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="a1ce7-188">Löschen der Skriptaktion</span><span class="sxs-lookup"><span data-stu-id="a1ce7-188">Delete Script Action</span></span>

<span data-ttu-id="a1ce7-189">Löschen Sie eine angegebene permanente Skriptaktion für einen Cluster wie folgt:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-189">To delete a specified persisted script action on a given cluster:</span></span>

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="a1ce7-190">Auflisten von permanenten Skriptaktionen</span><span class="sxs-lookup"><span data-stu-id="a1ce7-190">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="a1ce7-191">`listByCluster()` gibt ein `PagedList<RuntimeScriptActionDetailInner>`-Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-191">Both `listByCluster()` returns a `PagedList<RuntimeScriptActionDetailInner>` object.</span></span> <span data-ttu-id="a1ce7-192">Wenn Sie `currentPage().items()` aufrufen, wird eine Liste von `RuntimeScriptActionDetailInner` zurückgegeben, und `loadNextPage()` fährt mit der nächsten Seite fort.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-192">Calling `currentPage().items()` returns a list of `RuntimeScriptActionDetailInner`, and `loadNextPage()` advances to the next page.</span></span> <span data-ttu-id="a1ce7-193">Dies kann wiederholt werden, bis `false` für `hasNextPage()` zurückgegeben wird (d. h. es sind keine Seiten mehr vorhanden).</span><span class="sxs-lookup"><span data-stu-id="a1ce7-193">This can be repeated until `hasNextPage()` returns `false`, indicating that there are no more pages.</span></span>

<span data-ttu-id="a1ce7-194">Listen Sie alle permanenten Skriptaktionen für den angegebenen Cluster wie folgt auf:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-194">To list all persisted script actions for the specified cluster:</span></span>
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="a1ce7-195">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a1ce7-195">Example</span></span>

```java
PagedList<RuntimeScriptActionDetailInner> scriptsPaged = client.scriptActions().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptsPaged.hasNextPage()) {
        scriptsPaged.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="a1ce7-196">Auflisten des Ausführungsverlaufs aller Skripts</span><span class="sxs-lookup"><span data-stu-id="a1ce7-196">List All Scripts' Execution History</span></span>

<span data-ttu-id="a1ce7-197">Listen Sie den Ausführungsverlauf aller Skripts für den angegebenen Cluster wie folgt auf:</span><span class="sxs-lookup"><span data-stu-id="a1ce7-197">To list all scripts' execution history for the specified cluster:</span></span>

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="a1ce7-198">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a1ce7-198">Example</span></span>

<span data-ttu-id="a1ce7-199">In diesem Beispiel werden alle Details zu allen erfolgten Skriptausführungen ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="a1ce7-199">This example prints all the details for all past script executions.</span></span>

```java
PagedList<RuntimeScriptActionDetailInner> scriptExecutionsPaged = client.scriptExecutionHistorys().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptExecutionsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptExecutionsPaged.hasNextPage()) {
        scriptExecutionsPaged.loadNextPage();
    } else {
        break;
    }
}
```
