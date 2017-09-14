---
title: "Erste Schritte mit den Azure-Bibliotheken für Java"
description: "Machen Sie sich mit der grundlegenden Verwendung der Azure-Bibliotheken für Java mit Ihrem eigenen Azure-Abonnement vertraut."
keywords: Azure, Java, SDK, API, authentifizieren, erste Schritte
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: b1e10b79-f75e-4605-aecd-eed64873e2d3
ms.openlocfilehash: c9b654ea927563e8255f5d189ddc84733a1202e2
ms.sourcegitcommit: 30d502b3150fa14bcc1251f5f88c7c0dd83e531e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/12/2017
---
# <a name="get-started-with-the-azure-libraries-for-java"></a><span data-ttu-id="56eb5-104">Erste Schritte mit den Azure-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="56eb5-104">Get started with the Azure libraries for Java</span></span>

<span data-ttu-id="56eb5-105">In dieser Anleitung erfahren Sie, wie Sie eine Entwicklungsumgebung mit einem Azure-Dienstprinzipal einrichten und Beispielcode ausführen, der Ressourcen in Ihrem Azure-Abonnement mithilfe der Azure-Bibliotheken für Java erstellt und verwendet.</span><span class="sxs-lookup"><span data-stu-id="56eb5-105">This guide walks you through setting up a development environment with an Azure service principal and running sample code that creates and uses resources in your Azure subscription using the Azure libraries for Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56eb5-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="56eb5-106">Prerequisites</span></span>

- <span data-ttu-id="56eb5-107">Ein Azure-Konto.</span><span class="sxs-lookup"><span data-stu-id="56eb5-107">An Azure account.</span></span> <span data-ttu-id="56eb5-108">Falls Sie noch kein Konto besitzen, können Sie die [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.</span><span class="sxs-lookup"><span data-stu-id="56eb5-108">If you don't have one , [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="56eb5-109">[Azure Cloud Shell](https://docs.microsoft.coms/azure/cloud-shell/quickstart) oder [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="56eb5-109">[Azure Cloud Shell](https://docs.microsoft.coms/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="56eb5-110">[Java 8](https://www.azul.com/downloads/zulu/) (enthalten in Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="56eb5-110">[Java 8](https://www.azul.com/downloads/zulu/) (included in Azure Cloud Shell)</span></span>
- <span data-ttu-id="56eb5-111">[Maven 3](http://maven.apache.org/download.cgi) (enthalten in Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="56eb5-111">[Maven 3](http://maven.apache.org/download.cgi) (included in Azure Cloud Shell)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="56eb5-112">Einrichten der Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="56eb5-112">Set up authentication</span></span>

<span data-ttu-id="56eb5-113">Die Java-Anwendung benötigt Lese- und Schreibberechtigungen in Ihrem Azure-Abonnement, um den Beispielcode in diesem Tutorial ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="56eb5-113">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="56eb5-114">Erstellen Sie einen Dienstprinzipal, und konfigurieren Sie Ihre Anwendung so, dass sie mit dessen Anmeldeinformationen ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="56eb5-114">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="56eb5-115">Dienstprinzipale ermöglichen die Erstellung eines nicht interaktiven, Ihrer Identität zugeordneten Kontos, dem Sie nur die Berechtigungen erteilen, die zum Ausführen Ihrer App erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="56eb5-115">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="56eb5-116">[Erstellen Sie einen Dienstprinzipal mithilfe der Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli), und erfassen Sie die Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="56eb5-116">[Create a service principal using the Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) and capture the output.</span></span> <span data-ttu-id="56eb5-117">Geben Sie im Kennwortargument anstelle von `MY_SECURE_PASSWORD` ein [sicheres Kennwort](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) an.</span><span class="sxs-lookup"><span data-stu-id="56eb5-117">You'll need to provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```

<span data-ttu-id="56eb5-118">Kopieren Sie als Nächstes Folgendes in eine Textdatei auf Ihrem System:</span><span class="sxs-lookup"><span data-stu-id="56eb5-118">Next, copy the following into a text file on your system:</span></span>

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

<span data-ttu-id="56eb5-119">Ersetzen Sie die ersten vier Werte durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="56eb5-119">Replace the top four values with the following:</span></span>

- <span data-ttu-id="56eb5-120">subscription: Verwenden Sie den *id*-Wert aus `az account show` in der Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="56eb5-120">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="56eb5-121">client: Verwenden Sie den *appId*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="56eb5-121">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="56eb5-122">key: Verwenden Sie den *password*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="56eb5-122">key: use the *password* value from the service principal output .</span></span>
- <span data-ttu-id="56eb5-123">tenant: Verwenden Sie den *tenant*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="56eb5-123">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="56eb5-124">Speichern Sie diese Datei an einem sicheren Ort in Ihrem System, an dem sie vom Code gelesen werden kann.</span><span class="sxs-lookup"><span data-stu-id="56eb5-124">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="56eb5-125">Legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Authentifizierungsdatei in Ihrer Shell fest.</span><span class="sxs-lookup"><span data-stu-id="56eb5-125">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>    

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="56eb5-126">Erstellen eines neuen Maven-Projekts</span><span class="sxs-lookup"><span data-stu-id="56eb5-126">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="56eb5-127">Der Beispielcode in diesem Leitfaden wird mithilfe des Maven-Erstellungstools erstellt und ausgeführt. Die Azure-Bibliotheken für Java können aber auch mit anderen Erstellungstools (beispielsweise Gradle) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="56eb5-127">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="56eb5-128">Erstellen Sie über die Befehlszeile ein Maven-Projekt in einem neuen Verzeichnis auf Ihrem System:</span><span class="sxs-lookup"><span data-stu-id="56eb5-128">Create a Maven project from the command line in a new directory on your system:</span></span>

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

<span data-ttu-id="56eb5-129">Dadurch wird ein einfaches Maven-Projekt unter dem Ordner `testAzureApp` erstellt.</span><span class="sxs-lookup"><span data-stu-id="56eb5-129">This creates a basic Maven project under the `testAzureApp` folder.</span></span> <span data-ttu-id="56eb5-130">Fügen Sie dem Projekt `pom.xml` die folgenden Einträge hinzu, um die Bibliotheken zu importieren, die im Beispielcode dieses Tutorials verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="56eb5-130">Add the following entries into the project `pom.xml` to import the libraries used in the sample code in this tutorial.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="56eb5-131">Fügen Sie unter dem Element `project` der obersten Ebene einen Eintrag vom Typ `build` hinzu, um die Beispiele mithilfe von [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) auszuführen:</span><span class="sxs-lookup"><span data-stu-id="56eb5-131">Add a `build` entry under the top-level `project` element to use the [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) to run the samples:</span></span>

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.AzureApp</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
 ```
   
## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="56eb5-132">Erstellen einer virtuellen Linux-Maschine</span><span class="sxs-lookup"><span data-stu-id="56eb5-132">Create a Linux virtual machine</span></span>

<span data-ttu-id="56eb5-133">Erstellen Sie im Projektverzeichnis `src/main/java` eine neue Datei namens `AzureApp.java`, und fügen Sie den folgenden Codeblock ein.</span><span class="sxs-lookup"><span data-stu-id="56eb5-133">Create a new file named `AzureApp.java` in the project's `src/main/java` directory and paste in the following block of code.</span></span> <span data-ttu-id="56eb5-134">Aktualisieren Sie die Variablen `userName` und `sshKey` mit echten Werten für Ihren Computer.</span><span class="sxs-lookup"><span data-stu-id="56eb5-134">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="56eb5-135">Der Code erstellt einen neuen virtuellen Linux-Computer namens `testLinuxVM` in der Ressourcengruppe `sampleResourceGroup` in der Azure-Region „USA, Osten“.</span><span class="sxs-lookup"><span data-stu-id="56eb5-135">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

```java
package com.fabrikam.testAzureApp;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.WebApp;
import com.microsoft.azure.management.storage.StorageAccount;
import com.microsoft.azure.management.storage.SkuName;
import com.microsoft.azure.management.storage.StorageAccountKey;
import com.microsoft.azure.management.sql.SqlDatabase;
import com.microsoft.azure.management.sql.SqlServer;
import com.microsoft.azure.management.resources.fluentcore.arm.Region;
import com.microsoft.azure.management.resources.fluentcore.utils.SdkContext;

import com.microsoft.rest.LogLevel;

import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

import java.io.File;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class AzureApp {

    public static void main(String[] args) {

        final String userName = "YOUR_VM_USERNAME";
        final String sshKey = "YOUR_PUBLIC_SSH_KEY";

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));    
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();
           
            // create a Ubuntu virtual machine in a new resource group 
            VirtualMachine linuxVM = azure.virtualMachines().define("testLinuxVM")
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup("sampleVmResourceGroup")
                    .withNewPrimaryNetwork("10.0.0.0/24")
                    .withPrimaryPrivateIpAddressDynamic()
                    .withoutPrimaryPublicIpAddress()
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withUnmanagedDisks()
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();   

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

<span data-ttu-id="56eb5-136">Führen Sie das Beispiel über die Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="56eb5-136">Run the sample from the command line:</span></span>

```
mvn compile exec:java
```

<span data-ttu-id="56eb5-137">In der Konsole werden einige REST-Anforderungen und Antworten angezeigt, während das SDK die zugrunde liegenden Aufrufe an die REST-API ausführt, um den virtuellen Computer und die dazugehörigen Ressourcen zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="56eb5-137">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="56eb5-138">Überprüfen Sie den virtuellen Computer in Ihrem Abonnement nach Abschluss des Programms mithilfe der Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="56eb5-138">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="56eb5-139">Nachdem Sie sich vergewissert haben, dass der Code erfolgreich ausgeführt wurde, löschen Sie den virtuellen Computer und dessen Ressourcen über die Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="56eb5-139">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="56eb5-140">Bereitstellen einer Web-App aus einem GitHub-Repository</span><span class="sxs-lookup"><span data-stu-id="56eb5-140">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="56eb5-141">Ersetzen Sie die main-Methode in `AzureApp.java` durch die im Anschluss angegebene Methode, und legen Sie die Variable `appName` vor dem Ausführen des Codes auf einen eindeutigen Wert fest.</span><span class="sxs-lookup"><span data-stu-id="56eb5-141">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="56eb5-142">Dieser Code stellt eine Webanwendung aus der Verzweigung `master` in einem öffentlichen GitHub-Repository für eine neue [Azure App Service-Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) bereit, die unter dem Tarif „Free“ ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="56eb5-142">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

```java
    public static void main(String[] args) {
        try {

            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            final String appName = "YOUR_APP_NAME";

            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            WebApp app = azure.webApps().define(appName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleWebResourceGroup")
                    .withNewWindowsPlan(PricingTier.FREE_F1)
                    .defineSourceControl()
                    .withPublicGitRepository(
                            "https://github.com/Azure-Samples/app-service-web-java-get-started")
                    .withBranch("master")
                    .attach()
                    .create();

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
```

<span data-ttu-id="56eb5-143">Führen Sie den Code wie zuvor mit Maven aus:</span><span class="sxs-lookup"><span data-stu-id="56eb5-143">Run the code as before using Maven:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="56eb5-144">Öffnen Sie die Anwendung über die Befehlszeilenschnittstelle in einem Browser:</span><span class="sxs-lookup"><span data-stu-id="56eb5-144">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="56eb5-145">Entfernen Sie die Web-App und den Plan aus Ihrem Abonnement, nachdem Sie die Bereitstellung überprüft haben.</span><span class="sxs-lookup"><span data-stu-id="56eb5-145">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-a-sql-database"></a><span data-ttu-id="56eb5-146">Herstellen einer Verbindung mit einer SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="56eb5-146">Connect to a SQL database</span></span>

<span data-ttu-id="56eb5-147">Ersetzen Sie die aktuelle main-Methode in `AzureApp.java` durch den im Anschluss angegebenen Code, und legen Sie die Variable `dbPassword` auf einen echten Wert fest.</span><span class="sxs-lookup"><span data-stu-id="56eb5-147">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="56eb5-148">Dieser Code erstellt eine neue SQL­-Datenbank mit einer Firewallregel, die Remotezugriffe zulässt, und stellt anschließend unter Verwendung des SQL-Datenbank-JBDC-Treibers eine Verbindung mit der Datenbank her.</span><span class="sxs-lookup"><span data-stu-id="56eb5-148">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

```java

    public static void main(String args[])
    {
        // create the db using the management libraries
        try {
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            final String adminUser = SdkContext.randomResourceName("db",8);
            final String sqlServerName = SdkContext.randomResourceName("sql",10);
            final String sqlDbName = SdkContext.randomResourceName("dbname",8);
            final String dbPassword = "YOUR_PASSWORD_HERE";


            SqlServer sampleSQLServer = azure.sqlServers().define(sqlServerName)
                            .withRegion(Region.US_EAST)
                            .withNewResourceGroup("sampleSqlResourceGroup")
                            .withAdministratorLogin(adminUser)
                            .withAdministratorPassword(dbPassword)
                            .withNewFirewallRule("0.0.0.0","255.255.255.255")
                            .create();

            SqlDatabase sampleSQLDb = sampleSQLServer.databases().define(sqlDbName).create();

            // assemble the connection string to the database
            final String domain = sampleSQLServer.fullyQualifiedDomainName();
            String url = "jdbc:sqlserver://"+ domain + ":1433;" +
                    "database=" + sqlDbName +";" +
                    "user=" + adminUser+ "@" + sqlServerName + ";" +
                    "password=" + dbPassword + ";" +
                    "encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";

            // connect to the database, create a table and insert a entry into it
            Connection conn = DriverManager.getConnection(url);

            String createTable = "CREATE TABLE CLOUD ( name varchar(255), code int);";
            String insertValues = "INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);";
            String selectValues = "SELECT * FROM CLOUD";
            Statement createStatement = conn.createStatement();
            createStatement.execute(createTable);
            Statement insertStatement = conn.createStatement();
            insertStatement.execute(insertValues);
            Statement selectStatement = conn.createStatement();
            ResultSet rst = selectStatement.executeQuery(selectValues);

            while (rst.next()) {
                System.out.println(rst.getString(1) + " "
                        + rst.getString(2));
            }


        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println(e.getStackTrace().toString());
        }
    }
```
<span data-ttu-id="56eb5-149">Führen Sie das Beispiel über die Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="56eb5-149">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="56eb5-150">Bereinigen Sie die Ressourcen anschließend über die Befehlszeilenschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="56eb5-150">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="56eb5-151">Schreiben eines Blobs in ein neues Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="56eb5-151">Write a blob into a new storage account</span></span>

<span data-ttu-id="56eb5-152">Ersetzen Sie die aktuelle main-Methode in `AzureApp.java` durch den im Anschluss angegebenen Code.</span><span class="sxs-lookup"><span data-stu-id="56eb5-152">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="56eb5-153">Dieser Code erstellt ein [Azure-Speicherkonto](https://docs.microsoft.com/azure/storage/storage-introduction) und anschließend unter Verwendung von Azure Storage-Bibliotheken für Java eine neue Textdatei in der Cloud.</span><span class="sxs-lookup"><span data-stu-id="56eb5-153">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

```java
    public static void main(String[] args) {

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            // create a new storage account
            String storageAccountName = SdkContext.randomResourceName("st",8);
            StorageAccount storage = azure.storageAccounts().define(storageAccountName)
                        .withRegion(Region.US_WEST2)
                        .withNewResourceGroup("sampleStorageResourceGroup")
                        .create();

            // create a storage container to hold the file
            List<StorageAccountKey> keys = storage.getKeys();
            final String storageConnection = "DefaultEndpointsProtocol=https;"
                   + "AccountName=" + storage.name()
                   + ";AccountKey=" + keys.get(0).value()
                    + ";EndpointSuffix=core.windows.net";

            CloudStorageAccount account = CloudStorageAccount.parse(storageConnection);
            CloudBlobClient serviceClient = account.createCloudBlobClient();

            // Container name must be lower case.
            CloudBlobContainer container = serviceClient.getContainerReference("helloazure");
            container.createIfNotExists();

            // Make the container public
            BlobContainerPermissions containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // write a blob to the container
            CloudBlockBlob blob = container.getBlockBlobReference("helloazure.txt");
            blob.uploadText("hello Azure");

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

<span data-ttu-id="56eb5-154">Führen Sie das Beispiel über die Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="56eb5-154">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="56eb5-155">Sie können über das Azure-Portal oder mit dem [Azure-Speicher-Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) zur Datei `helloazure.txt` in Ihrem Speicherkonto navigieren.</span><span class="sxs-lookup"><span data-stu-id="56eb5-155">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="56eb5-156">Bereinigen Sie das Speicherkonto über die Befehlszeilenschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="56eb5-156">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="56eb5-157">Erkunden weiterer Beispiele</span><span class="sxs-lookup"><span data-stu-id="56eb5-157">Explore more samples</span></span>

<span data-ttu-id="56eb5-158">Weitere Informationen zur Ressourcenverwaltung und Aufgabenautomatisierung mit den Azure-Verwaltungsbibliotheken für Java finden Sie in unserem Beispielcode für [virtuelle Computer](java-sdk-azure-virtual-machine-samples.md), [Web-Apps](java-sdk-azure-web-apps-samples.md) und [SQL-Datenbank](java-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="56eb5-158">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](java-sdk-azure-virtual-machine-samples.md), [web apps](java-sdk-azure-web-apps-samples.md) and [SQL database](java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="56eb5-159">Referenz und Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="56eb5-159">Reference and release notes</span></span>

<span data-ttu-id="56eb5-160">Für alle Pakete steht eine [Referenz](http://docs.microsoft.com/java/api) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="56eb5-160">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="56eb5-161">Hilfe und Feedback</span><span class="sxs-lookup"><span data-stu-id="56eb5-161">Get help and give feedback</span></span>

<span data-ttu-id="56eb5-162">Stellen Sie in [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java) Fragen an die Community.</span><span class="sxs-lookup"><span data-stu-id="56eb5-162">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="56eb5-163">Melden Sie Fehler und Probleme im Zusammenhang mit den Azure-Bibliotheken für Java auf der [projektspezifischen GitHub-Seite](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="56eb5-163">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>