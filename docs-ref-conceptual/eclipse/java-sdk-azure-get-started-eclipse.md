---
title: "Erste Schritte mit Azure für Java mithilfe von Eclipse"
description: "Machen Sie sich mit der grundlegenden Verwendung der Azure-Bibliotheken für Java mit Ihrem eigenen Azure-Abonnement vertraut."
keywords: Azure, Java, SDK, API, authentifizieren, erste Schritte
services: 
documentationcenter: java
author: roygara
manager: timlt
editor: 
ms.author: v-rogara
ms.date: 02/01/2018
ms.devlang: java
ms.prod: azure
ms.technology: azure
ms.topic: get-started-article
ms.service: multiple
ms.openlocfilehash: 740679197981f49d99b8d8251e257963d3030fb1
ms.sourcegitcommit: 720c2eaf66532d277015610ec375c71e934d9ee6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="get-started-with-the-azure-libraries-using-eclipse"></a>Erste Schritte mit den Azure-Bibliotheken mithilfe von Eclipse

In diesem Leitfaden werden die Schritte zum Einrichten einer Entwicklungsumgebung und zum Verwenden der Azure-Bibliotheken für Java erläutert. Sie erstellen einen Dienstprinzipal für die Authentifizierung mit Azure und führen Beispielcode aus, der Azure-Ressourcen in Ihrem Abonnement erstellt und verwendet. Die Verwendung von Eclipse ist für die Java-Entwicklung mit Azure optional. Es kann jede IDE mit Maven-Integration verwendet werden. Alternativ können Sie Ihren Code mit Maven über die Befehlszeile ausführen, wenn Sie keine IDE verwenden möchten.

## <a name="prerequisites"></a>Voraussetzungen

- Ein Azure-Konto. Falls Sie noch kein Konto haben, können Sie eine [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.
- [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) oder [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).
- Die letzte stabile Version von [Eclipse](http://www.eclipse.org/downloads/)

## <a name="set-up-authentication"></a>Einrichten der Authentifizierung

Die Java-Anwendung benötigt Lese- und Schreibberechtigungen in Ihrem Azure-Abonnement, um den Beispielcode in diesem Tutorial ausführen zu können. Erstellen Sie einen Dienstprinzipal, und konfigurieren Sie Ihre Anwendung so, dass sie mit dessen Anmeldeinformationen ausgeführt wird. Dienstprinzipale ermöglichen die Erstellung eines nicht interaktiven, Ihrer Identität zugeordneten Kontos, dem Sie nur die Berechtigungen erteilen, die zum Ausführen Ihrer App erforderlich sind.

[Erstellen Sie einen Dienstprinzipal](/cli/azure/create-an-azure-service-principal-azure-cli), um dem Code Berechtigungen zum Erstellen und Aktualisieren von Ressourcen in Ihrem Abonnement ohne direkte Verwendung Ihrer Kontoanmeldeinformationen zu erteilen. Erfassen Sie unbedingt die Ausgabe. Geben Sie im Kennwortargument anstelle von `MY_SECURE_PASSWORD` ein [sicheres Kennwort](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) an. Ihr Kennwort muss 8 bis 16 Zeichen lang sein und mindestens drei der folgenden Merkmale aufweisen:

* Kleinbuchstaben
* Großbuchstaben
* Zahlen
* Eins der folgenden Symbole: @ # $ % ^ & * - _ ! + = [ ] { } | \ : ‘ , . ? / ` ~ “ ( ) ;


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

Sie erhalten eine Antwort im folgenden Format:

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

Kopieren Sie als Nächstes Folgendes in eine Textdatei auf Ihrem System:

```text
# sample management library properties file
subscription=ssssssss-ssss-ssss-ssss-ssssssssssss
client=cccccccc-cccc-cccc-cccc-cccccccccccc
key=kkkkkkkkkkkkkkkk
tenant=tttttttt-tttt-tttt-tttt-tttttttttttt
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

Ersetzen Sie die ersten vier Werte durch Folgendes:

- subscription: Verwenden Sie den *id*-Wert aus `az account show` in der Azure CLI 2.0.
- client: Verwenden Sie den *appId*-Wert aus der Dienstprinzipalausgabe.
- key: Verwenden Sie den *password*-Wert aus der Dienstprinzipalausgabe.
- tenant: Verwenden Sie den *tenant*-Wert aus der Dienstprinzipalausgabe.

Speichern Sie diese Datei an einem sicheren Ort in Ihrem System, an dem sie vom Code gelesen werden kann. Sie können diese Datei für künftigen Code verwenden. Daher wird empfohlen, sie außerhalb der Anwendung in diesem Artikel zu speichern.

Legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Authentifizierungsdatei in Ihrer Shell fest.

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Wenn Sie eine Windows-Umgebung verwenden, fügen Sie die Variable zu Ihren Systemeigenschaften hinzu. Öffnen Sie ein PowerShell-Fenster mit Administratorberechtigungen, ersetzen Sie die zweite Variable durch den Pfad zu Ihrer Datei, und geben Sie den folgenden Befehl ein:

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="create-a-new-maven-project"></a>Erstellen eines neuen Maven-Projekts

> [!NOTE]
> Der Beispielcode in diesem Leitfaden wird mithilfe des Maven-Erstellungstools erstellt und ausgeführt. Die Azure-Bibliotheken für Java können aber auch mit anderen Erstellungstools (beispielsweise Gradle) verwendet werden. 

Öffnen Sie Eclipse, und klicken Sie auf **File** -> **New** („Datei“ > „Neu“). Öffnen Sie in dem daraufhin angezeigten Fenster den Maven-Ordner, und klicken Sie auf „Maven Project“ (Maven-Projekt). 

Behalten Sie die Standardwerte auf dem nächsten Bildschirm bei, und klicken Sie auf **Next** (Weiter). Gehen Sie auf diesem Bildschirm für Archetypen genauso vor.

Geben Sie auf dem Bildschirm mit entsprechender Eingabeaufforderung für „groupID“, „ArtifactID usw. Folgendes ein: Geben Sie „com.fabrikam“ für „groupID“ und „AzureApp“ für „artifactID“ ein.

Öffnen Sie nun die Datei „pom.xml“. Fügen Sie im Tag `dependencies` den folgenden Code hinzu:

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
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

Speichern Sie nun die Datei „pom.xml“. Dadurch wird Eclipse angewiesen, alle angegebenen Abhängigkeiten herunterzuladen. Dies kann einen Moment dauern.
   
## <a name="install-the-azure-toolkit-for-eclipse"></a>Installieren des Azure-Toolkits für Eclipse

Das [Azure-Toolkit](azure-toolkit-for-eclipse.md) ist erforderlich, wenn Sie Web-Apps oder APIs programmgesteuert bereitstellen, wird derzeit jedoch nicht für andere Bereitstellungsarten verwendet. Es folgt eine Zusammenfassung des Installationsvorgangs. Ausführliche Schritte finden Sie unter [Azure-Toolkit für Eclipse](azure-toolkit-for-eclipse.md).

Klicken Sie auf das Menü **Help** (Hilfe) und dann auf **Install New Software** (Neue Software installieren).

Geben Sie `http://dl.microsoft.com/eclipse` in das Feld **Work with:** (Arbeiten mit:) ein, und drücken Sie die EINGABETASTE.

Aktivieren Sie anschließend das Kontrollkästchen neben **Azure toolkit for Java** (Azure-Toolkit für Java), und deaktivieren Sie das Kontrollkästchen **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu finden). Klicken Sie anschließend auf „Next“ (Weiter).

## <a name="create-a-linux-virtual-machine"></a>Erstellen einer virtuellen Linux-Maschine

Erstellen Sie im Projektverzeichnis `src/main/java` eine neue Datei namens `AzureApp.java`, und fügen Sie den folgenden Codeblock ein. Aktualisieren Sie die Variablen `userName` und `sshKey` mit echten Werten für Ihren Computer. Der Code erstellt einen neuen virtuellen Linux-Computer namens `testLinuxVM` in der Ressourcengruppe `sampleResourceGroup` in der Azure-Region „USA, Osten“.

Öffnen Sie zum Erstellen eines `sshkey`-Elements Azure Cloud Shell, und geben Sie `ssh-keygen -t rsa -b 2048` ein. Geben Sie einen Namen für die Datei ein, und rufen Sie dann die PUBLIC-Datei auf, um den Schlüssel abzurufen, den Sie im folgenden Code verwenden. Kopieren Sie den Schlüssel, und fügen Sie ihn vollständig in die Variable `sshKey` ein.

```java
package com.fabrikam.AzureApp;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.PricingTier;
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
import java.util.List;

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
                    .withPrimaryPrivateIPAddressDynamic()
                    .withoutPrimaryPublicIPAddress()
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


In der Konsole werden einige REST-Anforderungen und Antworten angezeigt, während das SDK die zugrunde liegenden Aufrufe an die Azure-REST-API ausführt, um den virtuellen Computer und die dazugehörigen Ressourcen zu konfigurieren. Überprüfen Sie den virtuellen Computer in Ihrem Abonnement nach Abschluss des Programms mithilfe der Azure CLI 2.0:

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

Nachdem Sie sich vergewissert haben, dass der Code erfolgreich ausgeführt wurde, löschen Sie den virtuellen Computer und dessen Ressourcen über die Befehlszeile.

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Bereitstellen einer Web-App aus einem GitHub-Repository

Ersetzen Sie die main-Methode in `AzureApp.java` durch die im Anschluss angegebene Methode, und legen Sie die Variable `appName` vor dem Ausführen des Codes auf einen eindeutigen Wert fest. Dieser Code stellt eine Webanwendung aus der Verzweigung `master` in einem öffentlichen GitHub-Repository für eine neue [Azure App Service-Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) bereit, die unter dem Tarif „Free“ ausgeführt wird.

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

Führen Sie den Code wie zuvor mit Maven aus:

Öffnen Sie die Anwendung über die Befehlszeilenschnittstelle in einem Browser:

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
Entfernen Sie die Web-App und den Plan aus Ihrem Abonnement, nachdem Sie die Bereitstellung überprüft haben.

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a>Herstellen einer Verbindung mit einer Azure SQL-Datenbank

Ersetzen Sie die aktuelle main-Methode in `AzureApp.java` durch den im Anschluss angegebenen Code, und legen Sie die Variable `dbPassword` auf einen echten Wert fest.
Dieser Code erstellt eine neue SQL­-Datenbank mit einer Firewallregel, die Remotezugriffe zulässt, und stellt anschließend unter Verwendung des SQL-Datenbank-JBDC-Treibers eine Verbindung mit der Datenbank her. 

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
Führen Sie das Beispiel über die Befehlszeile aus:

```
mvn clean compile exec:java
```

Bereinigen Sie die Ressourcen anschließend über die Befehlszeilenschnittstelle:

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a>Schreiben eines Blobs in ein neues Speicherkonto

Ersetzen Sie die aktuelle main-Methode in `AzureApp.java` durch den im Anschluss angegebenen Code. Dieser Code erstellt ein [Azure-Speicherkonto](https://docs.microsoft.com/azure/storage/storage-introduction) und anschließend unter Verwendung von Azure Storage-Bibliotheken für Java eine neue Textdatei in der Cloud.

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

            // create a storage container to hold the files
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

Führen Sie das Beispiel über die Befehlszeile aus:

Sie können über das Azure-Portal oder mit dem [Azure Storage-Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) zur Datei `helloazure.txt` in Ihrem Speicherkonto navigieren.

Bereinigen Sie das Speicherkonto über die Befehlszeilenschnittstelle:

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a>Erkunden weiterer Beispiele

Weitere Informationen zur Ressourcenverwaltung und Aufgabenautomatisierung mit den Azure-Verwaltungsbibliotheken für Java finden Sie in unserem Beispielcode für [virtuelle Computer](../java-sdk-azure-virtual-machine-samples.md), [Web-Apps](../java-sdk-azure-web-apps-samples.md) und [SQL-Datenbank](../java-sdk-azure-sql-database-samples.md).

## <a name="reference-and-release-notes"></a>Referenz und Versionshinweise

Für alle Pakete steht eine [Referenz](http://docs.microsoft.com/java/api) zur Verfügung.

## <a name="get-help-and-give-feedback"></a>Hilfe und Feedback

Stellen Sie in [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java) Fragen an die Community. Melden Sie Fehler und Probleme im Zusammenhang mit den Azure-Bibliotheken für Java auf der [projektspezifischen GitHub-Seite](https://github.com/Azure/azure-sdk-for-java).
