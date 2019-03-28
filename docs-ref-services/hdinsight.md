---
title: Azure HDInsight Java SDK
description: Referenz zum Azure HDInsight Java SDK Das HDInsight Java SDK bietet Klassen und Methoden, mit denen Sie Ihre HDInsight-Cluster verwalten können.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 11/21/2018
ms.openlocfilehash: 0ae8d78a0618c4dbcc5e734fce311f7c2e5684bd
ms.sourcegitcommit: a108a82414bd35be896e3c4e7047f5eb7b1518cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2019
ms.locfileid: "58489648"
---
# <a name="hdinsight-java-management-sdk-preview"></a>HDInsight Java Management SDK (Vorschauversion)

## <a name="overview"></a>Übersicht

Das HDInsight Java SDK bietet Klassen und Methoden, mit denen Sie Ihre HDInsight-Cluster verwalten können. Es enthält Vorgänge zum Erstellen, Löschen, Aktualisieren, Auflisten, Ändern der Größe, Ausführen von Skriptaktionen, Überwachen, Abrufen der Eigenschaften von HDInsight-Clustern und mehr.

## <a name="prerequisites"></a>Voraussetzungen

* Ein Azure-Konto. Falls Sie noch kein Konto haben, können Sie eine [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.
* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Maven](https://maven.apache.org/download.cgi)

## <a name="sdk-installation"></a>SDK-Installation

Das HDInsight Java SDK steht über Maven [hier](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight) zur Verfügung. Fügen Sie Ihrer Datei „pom.xml“ die folgende Abhängigkeit hinzu:

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

Außerdem müssen Sie der Datei „pom.xml“ die folgenden Abhängigkeiten hinzufügen:

* [Azure-Clientauthentifizierungsbibliothek:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
  </dependency>
  ```

* [Azure Java-Clientruntime für ARM:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
  </dependency>
  ```

## <a name="authentication"></a>Authentication

Das SDK muss zunächst für Ihr Azure-Abonnement authentifiziert werden.  Erstellen Sie anhand des Beispiels unten einen Dienstprinzipal, und verwenden Sie ihn für die Authentifizierung. Nachdem dies erfolgt ist, verfügen Sie über eine Instanz von `HDInsightManagementClientImpl` mit vielen Methoden (in den Abschnitten unten beschrieben), die zum Durchführen von Verwaltungsvorgängen verwendet werden können.

> [!NOTE]
> Neben dem Beispiel unten gibt es noch andere Möglichkeiten der Authentifizierung, die für Ihre Anforderungen unter Umständen besser geeignet sind. Hier werden alle Methoden beschrieben: [Authentifizieren bei den Azure-Verwaltungsbibliotheken für Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)

### <a name="authentication-example-using-a-service-principal"></a>Beispiel für die Authentifizierung mit einem Dienstprinzipal

Melden Sie sich zuerst bei [Azure Cloud Shell](https://shell.azure.com/bash) an. Vergewissern Sie sich, dass Sie derzeit das Abonnement verwenden, in dem der Dienstprinzipal erstellt werden soll. 

```azurecli-interactive
az account show
```

Die Informationen zu Ihrem Abonnement werden im JSON-Format angezeigt.

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

Wenn Sie nicht am richtigen Abonnement angemeldet sind, können Sie das richtige auswählen, indem Sie Folgendes ausführen: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Falls Sie den HDInsight-Ressourcenanbieter nicht bereits mit einer anderen Methode registriert haben (z.B. durch das Erstellen eines HDInsight-Clusters über das Azure-Portal), müssen Sie dies vor dem Authentifizieren durchführen. Dies ist über [Azure Cloud Shell](https://shell.azure.com/bash) möglich, indem Sie den folgenden Befehl ausführen:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Wählen Sie als Nächstes einen Namen für Ihren Dienstprinzipal aus, und erstellen Sie ihn mit dem folgenden Befehl:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

Die Dienstprinzipalinformationen werden im JSON-Format angezeigt.

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
Kopieren Sie den unten angegebenen Codeausschnitt, und geben Sie für `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` und `SUBSCRIPTION_ID` die Zeichenfolgen aus dem JSON-Code ein, der nach dem Ausführen des Befehls zurückgegeben wurde, um den Dienstprinzipal zu erstellen.

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


## <a name="cluster-management"></a>Clusterverwaltung

> [!NOTE]
> In diesem Abschnitt wird davon ausgegangen, dass Sie bereits eine `HDInsightManagementClientImpl`-Instanz authentifiziert und in einer Variablen mit dem Namen `client` gespeichert haben. Eine Anleitung zum Authentifizieren und Abrufen eines `HDInsightManagementClientImpl`-Elements finden Sie oben im Abschnitt „Authentifizierung“.

### <a name="create-a-cluster"></a>Erstellen eines Clusters

Sie können einen neuen Cluster erstellen, indem Sie `client.clusters().create()` aufrufen.

#### <a name="example"></a>Beispiel

In diesem Beispiel wird gezeigt, wie Sie einen Spark-Cluster mit zwei Hauptknoten und einem Workerknoten erstellen.

> [!NOTE]
> Sie müssen zuerst wie unten beschrieben eine Ressourcengruppe und ein Speicherkonto erstellen. Wenn Sie diese Komponenten bereits erstellt haben, können Sie diese Schritte überspringen.

##### <a name="creating-a-resource-group"></a>Erstellen einer Ressourcengruppe

Sie können eine Ressourcengruppe erstellen, indem Sie mit [Azure Cloud Shell](https://shell.azure.com/bash) Folgendes ausführen:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Erstellen eines Speicherkontos

Sie können ein Speicherkonto erstellen, indem Sie mit [Azure Cloud Shell](https://shell.azure.com/bash) Folgendes ausführen:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Führen Sie jetzt den folgenden Befehl aus, um den Schlüssel für Ihr Speicherkonto abzurufen (Sie benötigen ihn, um einen Cluster zu erstellen):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
Der unten stehende Java-Codeausschnitt erstellt einen Spark-Cluster mit zwei Hauptknoten und einem Workerknoten. Geben Sie gemäß den Anweisungen in den Kommentaren Werte in die leeren Variablen ein, und ändern Sie ggf. auch andere Parameter, um diese an Ihre Anforderungen anzupassen.

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

### <a name="get-cluster-details"></a>Abrufen von Clusterdetails

Rufen Sie die Eigenschaften für einen Cluster wie folgt ab:

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Beispiel

Sie können `get` verwenden, um zu bestätigen, dass die Erstellung des Clusters erfolgreich war.

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

Die Ausgabe sollte wie folgt aussehen:

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a>Auflisten von Clustern

#### <a name="list-clusters-under-the-subscription"></a>Auflisten von Clustern unter dem Abonnement

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a>Auflisten von Clustern nach Ressourcengruppe

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> Sowohl `List()` als auch `ListByResourceGroup()` geben ein `PagedList<ClusterInner>`-Objekt zurück. Wenn Sie `loadNext()` aufrufen, wird eine Liste der Cluster auf dieser Seite zurückgegeben und das `ClusterPaged`-Objekt auf der nächsten Seite fortgesetzt. Dies kann wiederholt werden, bis `false` für `hasNextPage()` zurückgegeben wird (d. h. es sind keine Seiten mehr vorhanden).

#### <a name="example"></a>Beispiel

Im folgenden Beispiel werden die Eigenschaften aller Cluster für das aktuelle Abonnement ausgegeben:

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

### <a name="delete-a-cluster"></a>Löschen eines Clusters

Löschen Sie einen Cluster wie folgt:

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>Aktualisieren von Clustermarkierungen

Sie können die Markierungen eines Clusters wie folgt aktualisieren:

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a>Ändern der Clustergröße

Sie können die Anzahl von Workerknoten für einen Cluster ändern, indem Sie wie folgt eine neue Größe angeben:

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>Clusterüberwachung

Das HDInsight Management SDK kann auch verwendet werden, um die Überwachung Ihrer Cluster per Operations Management Suite (OMS) zu verwalten.

### <a name="enable-oms-monitoring"></a>Aktivieren der OMS-Überwachung

> [!NOTE]
> Sie müssen über einen vorhandenen Log Analytics-Arbeitsbereich verfügen, um die OMS-Überwachung zu ermöglichen. Wenn Sie noch keinen erstellt haben, erfahren Sie an dieser Stelle, wie Sie dazu vorgehen: [Erstellen eines Log Analytics-Arbeitsbereichs im Azure-Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace)

Aktivieren Sie die OMS-Überwachung in Ihrem Cluster wie folgt:

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>Anzeigen des Status der OMS-Überwachung

Rufen Sie den Status von OMS in Ihrem Cluster wie folgt ab:

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>Deaktivieren der OMS-Überwachung

Deaktivieren Sie OMS in Ihrem Cluster wie folgt:

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>Skriptaktionen

HDInsight verfügt über eine Konfigurationsmethode mit der Bezeichnung „Skriptaktionen“, mit der benutzerdefinierte Skripts zum Anpassen des Clusters aufgerufen werden.
> [!NOTE]
> Weitere Informationen zum Verwenden von Skriptaktionen finden Sie hier: [Anpassen Linux-basierter HDInsight-Cluster mithilfe von Skriptaktionen](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>Ausführen von Skriptaktionen

Sie können Skriptaktionen für einen Cluster wie folgt ausführen:

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

### <a name="delete-script-action"></a>Löschen der Skriptaktion

Löschen Sie eine angegebene permanente Skriptaktion für einen Cluster wie folgt:

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>Auflisten von permanenten Skriptaktionen

> [!NOTE]
> `listByCluster()` gibt ein `PagedList<RuntimeScriptActionDetailInner>`-Objekt zurück. Wenn Sie `currentPage().items()` aufrufen, wird eine Liste von `RuntimeScriptActionDetailInner` zurückgegeben, und `loadNextPage()` fährt mit der nächsten Seite fort. Dies kann wiederholt werden, bis `false` für `hasNextPage()` zurückgegeben wird (d. h. es sind keine Seiten mehr vorhanden).

Listen Sie alle permanenten Skriptaktionen für den angegebenen Cluster wie folgt auf:
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Beispiel

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

### <a name="list-all-scripts-execution-history"></a>Auflisten des Ausführungsverlaufs aller Skripts

Listen Sie den Ausführungsverlauf aller Skripts für den angegebenen Cluster wie folgt auf:

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Beispiel

In diesem Beispiel werden alle Details zu allen erfolgten Skriptausführungen ausgegeben.

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
