---
title: Erste Schritte mit den Azure-Bibliotheken für Java
description: Hier finden Sie Informationen zum Erstellen von Azure-Cloudressourcen und erfahren, wie Sie sie verbinden und in Ihren Java-Anwendungen nutzen.
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
ms.openlocfilehash: 22389ce7346a1d97c072dcc82162c9286f21f178
ms.sourcegitcommit: 04d0d92c46399976b58a9dfa107ba644378bf171
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2019
ms.locfileid: "65986197"
---
# <a name="get-started-with-cloud-development-using-java-on-azure"></a><span data-ttu-id="b2225-104">Erste Schritte bei der Cloudentwicklung mit Java in Azure</span><span class="sxs-lookup"><span data-stu-id="b2225-104">Get started with cloud development using Java on Azure</span></span>

<span data-ttu-id="b2225-105">In diesem Leitfaden werden die Schritte zum Einrichten einer Entwicklungsumgebung für die Azure-Entwicklung in Java erläutert.</span><span class="sxs-lookup"><span data-stu-id="b2225-105">This guide walks you through setting up a development environment for Azure development in Java.</span></span> <span data-ttu-id="b2225-106">Sie erstellen Azure-Ressourcen und verbinden Sie, um einige allgemeine Aufgaben (etwa Hochladen einer Datei oder Bereitstellen einer Webanwendung) auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b2225-106">You'll then create some Azure resources and connect them to to perform some basic tasks, like uploading a file or deploying a web application.</span></span> <span data-ttu-id="b2225-107">Wenn Sie fertig sind, können Sie Azure-Dienste in Ihren eigenen Java-Anwendungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="b2225-107">When you're done, you'll be ready to start using Azure services in your own Java applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2225-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="b2225-108">Prerequisites</span></span>

- <span data-ttu-id="b2225-109">Ein Azure-Konto.</span><span class="sxs-lookup"><span data-stu-id="b2225-109">An Azure account.</span></span> <span data-ttu-id="b2225-110">Falls Sie noch kein Konto haben, können Sie eine [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.</span><span class="sxs-lookup"><span data-stu-id="b2225-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="b2225-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) oder [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b2225-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="b2225-112">[Java 8](https://www.azul.com/downloads/zulu/) (enthalten in Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="b2225-112">[Java 8](https://www.azul.com/downloads/zulu/) (included in Azure Cloud Shell)</span></span>
- <span data-ttu-id="b2225-113">[Maven 3](http://maven.apache.org/download.cgi) (enthalten in Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="b2225-113">[Maven 3](http://maven.apache.org/download.cgi) (included in Azure Cloud Shell)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="b2225-114">Einrichten der Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="b2225-114">Set up authentication</span></span>

<span data-ttu-id="b2225-115">Die Java-Anwendung benötigt Lese- und Schreibberechtigungen in Ihrem Azure-Abonnement, um den Beispielcode in diesem Tutorial ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="b2225-115">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="b2225-116">Erstellen Sie einen Dienstprinzipal, und konfigurieren Sie Ihre Anwendung so, dass sie mit dessen Anmeldeinformationen ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b2225-116">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="b2225-117">Dienstprinzipale ermöglichen die Erstellung eines nicht interaktiven, Ihrer Identität zugeordneten Kontos, dem Sie nur die Berechtigungen erteilen, die zum Ausführen Ihrer App erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="b2225-117">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="b2225-118">[Erstellen Sie einen Dienstprinzipal mithilfe der Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli), und erfassen Sie die Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="b2225-118">[Create a service principal using the Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) and capture the output.</span></span> <span data-ttu-id="b2225-119">Geben Sie im Kennwortargument anstelle von `MY_SECURE_PASSWORD` ein [sicheres Kennwort](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) an.</span><span class="sxs-lookup"><span data-stu-id="b2225-119">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="b2225-120">Ihr Kennwort muss 8 bis 16 Zeichen lang sein und mindestens drei der folgenden Merkmale aufweisen:</span><span class="sxs-lookup"><span data-stu-id="b2225-120">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="b2225-121">Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="b2225-121">Include lowercase characters</span></span>
* <span data-ttu-id="b2225-122">Großbuchstaben</span><span class="sxs-lookup"><span data-stu-id="b2225-122">Include uppercase characters</span></span>
* <span data-ttu-id="b2225-123">Zahlen</span><span class="sxs-lookup"><span data-stu-id="b2225-123">Include numbers</span></span>
* <span data-ttu-id="b2225-124">Eins der folgenden Symbole: @ # $ % ^ & \* - _ !</span><span class="sxs-lookup"><span data-stu-id="b2225-124">Include one of the following symbols: @ # $ % ^ & \* - _ !</span></span> <span data-ttu-id="b2225-125">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="b2225-125">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="b2225-126">?</span><span class="sxs-lookup"><span data-stu-id="b2225-126">?</span></span> <span data-ttu-id="b2225-127">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="b2225-127">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="b2225-128">Sie erhalten eine Antwort im folgenden Format:</span><span class="sxs-lookup"><span data-stu-id="b2225-128">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="b2225-129">Kopieren Sie als Nächstes Folgendes in eine Textdatei auf Ihrem System:</span><span class="sxs-lookup"><span data-stu-id="b2225-129">Next, copy the following into a text file on your system:</span></span>

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

<span data-ttu-id="b2225-130">Ersetzen Sie die ersten vier Werte durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="b2225-130">Replace the top four values with the following:</span></span>

- <span data-ttu-id="b2225-131">subscription: Verwenden Sie den *id*-Wert aus `az account show` in der Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b2225-131">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="b2225-132">client: Verwenden Sie den *appId*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="b2225-132">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="b2225-133">key: Verwenden Sie den *password*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="b2225-133">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="b2225-134">tenant: Verwenden Sie den *tenant*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="b2225-134">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="b2225-135">Speichern Sie diese Datei an einem sicheren Ort in Ihrem System, an dem sie vom Code gelesen werden kann.</span><span class="sxs-lookup"><span data-stu-id="b2225-135">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="b2225-136">Sie können diese Datei für künftigen Code verwenden. Daher wird empfohlen, sie außerhalb der Anwendung in diesem Artikel zu speichern.</span><span class="sxs-lookup"><span data-stu-id="b2225-136">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span>

<span data-ttu-id="b2225-137">Legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Authentifizierungsdatei in Ihrer Shell fest.</span><span class="sxs-lookup"><span data-stu-id="b2225-137">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>   

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="b2225-138">Wenn Sie eine Windows-Umgebung verwenden, fügen Sie die Variable zu Ihren Systemeigenschaften hinzu.</span><span class="sxs-lookup"><span data-stu-id="b2225-138">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="b2225-139">Öffnen Sie ein PowerShell-Fenster mit Administratorberechtigungen, ersetzen Sie die zweite Variable durch den Pfad zu Ihrer Datei, und geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="b2225-139">Open a PowerShell window with administrator privledges and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="tooling"></a><span data-ttu-id="b2225-140">Tools</span><span class="sxs-lookup"><span data-stu-id="b2225-140">Tooling</span></span>

### <a name="create-a-new-maven-project"></a><span data-ttu-id="b2225-141">Erstellen eines neuen Maven-Projekts</span><span class="sxs-lookup"><span data-stu-id="b2225-141">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="b2225-142">Der Beispielcode in diesem Leitfaden wird mithilfe des Maven-Erstellungstools erstellt und ausgeführt. Die Azure-Bibliotheken für Java können aber auch mit anderen Erstellungstools (beispielsweise Gradle) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b2225-142">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="b2225-143">Erstellen Sie über die Befehlszeile ein Maven-Projekt in einem neuen Verzeichnis auf Ihrem System:</span><span class="sxs-lookup"><span data-stu-id="b2225-143">Create a Maven project from the command line in a new directory on your system:</span></span>

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=AzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

<span data-ttu-id="b2225-144">Dadurch wird ein einfaches Maven-Projekt unter dem Ordner `testAzureApp` erstellt.</span><span class="sxs-lookup"><span data-stu-id="b2225-144">This creates a basic Maven project under the `testAzureApp` folder.</span></span> <span data-ttu-id="b2225-145">Fügen Sie dem Projekt `pom.xml` die folgenden Einträge hinzu, um die Bibliotheken zu importieren, die im Beispielcode dieses Tutorials verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b2225-145">Add the following entries into the project `pom.xml` to import the libraries used in the sample code in this tutorial.</span></span>

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

<span data-ttu-id="b2225-146">Fügen Sie unter dem Element `project` der obersten Ebene einen Eintrag vom Typ `build` hinzu, um die Beispiele mithilfe von [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) auszuführen:</span><span class="sxs-lookup"><span data-stu-id="b2225-146">Add a `build` entry under the top-level `project` element to use the [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) to run the samples:</span></span>

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.AzureApp</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
 ```

### <a name="install-the-azure-toolkit-for-intellij"></a><span data-ttu-id="b2225-147">Installieren des Azure-Toolkits für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b2225-147">Install the Azure Toolkit for Intellij</span></span>

<span data-ttu-id="b2225-148">Das [Azure-Toolkit](intellij/azure-toolkit-for-intellij-installation.md) ist erforderlich, wenn Sie Web-Apps oder APIs programmgesteuert bereitstellen, wird derzeit jedoch nicht für andere Bereitstellungsarten verwendet.</span><span class="sxs-lookup"><span data-stu-id="b2225-148">The [Azure toolkit](intellij/azure-toolkit-for-intellij-installation.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="b2225-149">Es folgt eine Zusammenfassung des Installationsvorgangs.</span><span class="sxs-lookup"><span data-stu-id="b2225-149">The following is a summary of the installation process.</span></span> <span data-ttu-id="b2225-150">Eine Schnellstartanleitung finden Sie unter [Erstellen einer „Hello World“-Web-App für Azure mit IntelliJ](intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2225-150">For a quickstart, visit [Azure Toolkit for IntelliJ quickstart](intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md).</span></span>

- <span data-ttu-id="b2225-151">Wählen Sie im Menü **Datei** die Option **Einstellungen...** aus.</span><span class="sxs-lookup"><span data-stu-id="b2225-151">Select the **File** menu and then select **Settings...**.</span></span> 

- <span data-ttu-id="b2225-152">Klicken Sie auf **Browse repositories...** (Repositorys durchsuchen), suchen Sie nach „Azure“, und installieren Sie dann das **Azure-Toolkit für IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="b2225-152">Select **Browse repositories...** and then search "Azure" and install the **Azure toolkit for Intellij**.</span></span>

- <span data-ttu-id="b2225-153">Starten Sie IntelliJ neu.</span><span class="sxs-lookup"><span data-stu-id="b2225-153">Restart Intellij.</span></span>

### <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="b2225-154">Installieren des Azure-Toolkits für Eclipse</span><span class="sxs-lookup"><span data-stu-id="b2225-154">Install the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="b2225-155">Das [Azure-Toolkit](eclipse/azure-toolkit-for-eclipse.md) ist erforderlich, wenn Sie Web-Apps oder APIs programmgesteuert bereitstellen, wird derzeit jedoch nicht für andere Bereitstellungsarten verwendet.</span><span class="sxs-lookup"><span data-stu-id="b2225-155">The [Azure toolkit](eclipse/azure-toolkit-for-eclipse.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="b2225-156">Es folgt eine Zusammenfassung des Installationsvorgangs.</span><span class="sxs-lookup"><span data-stu-id="b2225-156">The following is a summary of the installation process.</span></span> <span data-ttu-id="b2225-157">Eine Schnellstartanleitung finden Sie unter [Erstellen einer „Hello World“-Web-App für Azure mit Eclipse](eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2225-157">For a quickstart, visit [Azure Toolkit for Eclipse quickstart](eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md).</span></span>

- <span data-ttu-id="b2225-158">Klicken Sie auf das Menü **Help** (Hilfe) und dann auf **Install New Software** (Neue Software installieren).</span><span class="sxs-lookup"><span data-stu-id="b2225-158">Select the **Help** menu and then select **Install New software**.</span></span>

- <span data-ttu-id="b2225-159">Geben Sie `http://dl.microsoft.com/eclipse` in das Feld **Work with:** (Arbeiten mit:) ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="b2225-159">In the **Work with:** field enter `http://dl.microsoft.com/eclipse` and press enter.</span></span>

- <span data-ttu-id="b2225-160">Aktivieren Sie anschließend das Kontrollkästchen neben **Azure toolkit for Java** (Azure-Toolkit für Java), und deaktivieren Sie das Kontrollkästchen **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu finden).</span><span class="sxs-lookup"><span data-stu-id="b2225-160">Then, select the checkbox next to **Azure toolkit for Java** and uncheck the checkbox for **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="b2225-161">Klicken Sie anschließend auf „Next“ (Weiter).</span><span class="sxs-lookup"><span data-stu-id="b2225-161">Then select next.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="b2225-162">Erstellen einer virtuellen Linux-Maschine</span><span class="sxs-lookup"><span data-stu-id="b2225-162">Create a Linux virtual machine</span></span>

<span data-ttu-id="b2225-163">Erstellen Sie im Projektverzeichnis `src/main/java/com/fabirkam` eine neue Datei namens `AzureApp.java`, und fügen Sie den folgenden Codeblock ein.</span><span class="sxs-lookup"><span data-stu-id="b2225-163">Create a new file named `AzureApp.java` in the project's `src/main/java/com/fabirkam` directory and paste in the following block of code.</span></span> <span data-ttu-id="b2225-164">Aktualisieren Sie die Variablen `userName` und `sshKey` mit echten Werten für Ihren Computer.</span><span class="sxs-lookup"><span data-stu-id="b2225-164">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="b2225-165">Der Code erstellt einen neuen virtuellen Linux-Computer namens `testLinuxVM` in der Ressourcengruppe `sampleResourceGroup` in der Azure-Region „USA, Osten“.</span><span class="sxs-lookup"><span data-stu-id="b2225-165">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

```java
package com.fabrikam;

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

<span data-ttu-id="b2225-166">Führen Sie das Beispiel über die Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="b2225-166">Run the sample from the command line:</span></span>

```
mvn compile exec:java
```

<span data-ttu-id="b2225-167">In der Konsole werden einige REST-Anforderungen und Antworten angezeigt, während das SDK die zugrunde liegenden Aufrufe an die REST-API ausführt, um den virtuellen Computer und die dazugehörigen Ressourcen zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="b2225-167">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="b2225-168">Überprüfen Sie den virtuellen Computer in Ihrem Abonnement nach Abschluss des Programms mithilfe der Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="b2225-168">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="b2225-169">Nachdem Sie sich vergewissert haben, dass der Code erfolgreich ausgeführt wurde, löschen Sie den virtuellen Computer und dessen Ressourcen über die Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="b2225-169">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="b2225-170">Bereitstellen einer Web-App aus einem GitHub-Repository</span><span class="sxs-lookup"><span data-stu-id="b2225-170">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="b2225-171">Ersetzen Sie die main-Methode in `AzureApp.java` durch die im Anschluss angegebene Methode, und legen Sie die Variable `appName` vor dem Ausführen des Codes auf einen eindeutigen Wert fest.</span><span class="sxs-lookup"><span data-stu-id="b2225-171">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="b2225-172">Dieser Code stellt eine Webanwendung aus der Verzweigung `master` in einem öffentlichen GitHub-Repository für eine neue [Azure App Service-Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) bereit, die unter dem Tarif „Free“ ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b2225-172">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

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

<span data-ttu-id="b2225-173">Führen Sie den Code wie zuvor mit Maven aus:</span><span class="sxs-lookup"><span data-stu-id="b2225-173">Run the code as before using Maven:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="b2225-174">Öffnen Sie die Anwendung über die Befehlszeilenschnittstelle in einem Browser:</span><span class="sxs-lookup"><span data-stu-id="b2225-174">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="b2225-175">Entfernen Sie die Web-App und den Plan aus Ihrem Abonnement, nachdem Sie die Bereitstellung überprüft haben.</span><span class="sxs-lookup"><span data-stu-id="b2225-175">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="b2225-176">Herstellen einer Verbindung mit einer Azure SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="b2225-176">Connect to an Azure SQL database</span></span>

<span data-ttu-id="b2225-177">Ersetzen Sie die aktuelle main-Methode in `AzureApp.java` durch den im Anschluss angegebenen Code, und legen Sie die Variable `dbPassword` auf einen echten Wert fest.</span><span class="sxs-lookup"><span data-stu-id="b2225-177">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="b2225-178">Mit diesem Code wird eine neue SQL-Datenbank mit einer Firewallregel erstellt, die Remotezugriff zulässt, und anschließend über den SQL-Datenbank-JBDC-Treiber eine Verbindung hergestellt.</span><span class="sxs-lookup"><span data-stu-id="b2225-178">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

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
<span data-ttu-id="b2225-179">Führen Sie das Beispiel über die Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="b2225-179">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="b2225-180">Bereinigen Sie die Ressourcen anschließend über die Befehlszeilenschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="b2225-180">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="b2225-181">Schreiben eines Blobs in ein neues Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="b2225-181">Write a blob into a new storage account</span></span>

<span data-ttu-id="b2225-182">Ersetzen Sie die aktuelle main-Methode in `AzureApp.java` durch den im Anschluss angegebenen Code.</span><span class="sxs-lookup"><span data-stu-id="b2225-182">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="b2225-183">Dieser Code erstellt ein [Azure-Speicherkonto](https://docs.microsoft.com/azure/storage/storage-introduction) und anschließend unter Verwendung von Azure Storage-Bibliotheken für Java eine neue Textdatei in der Cloud.</span><span class="sxs-lookup"><span data-stu-id="b2225-183">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

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

<span data-ttu-id="b2225-184">Führen Sie das Beispiel über die Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="b2225-184">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="b2225-185">Sie können über das Azure-Portal oder mit dem [Azure Storage-Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) zur Datei `helloazure.txt` in Ihrem Speicherkonto navigieren.</span><span class="sxs-lookup"><span data-stu-id="b2225-185">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="b2225-186">Bereinigen Sie das Speicherkonto über die Befehlszeilenschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="b2225-186">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="b2225-187">Erkunden weiterer Beispiele</span><span class="sxs-lookup"><span data-stu-id="b2225-187">Explore more samples</span></span>

<span data-ttu-id="b2225-188">Weitere Informationen zur Ressourcenverwaltung und Aufgabenautomatisierung mit den Azure-Verwaltungsbibliotheken für Java finden Sie in unserem Beispielcode für [virtuelle Computer](java-sdk-azure-virtual-machine-samples.md), [Web-Apps](java-sdk-azure-web-apps-samples.md) und [SQL-Datenbank](java-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2225-188">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](java-sdk-azure-virtual-machine-samples.md), [web apps](java-sdk-azure-web-apps-samples.md) and [SQL database](java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="b2225-189">Referenz und Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="b2225-189">Reference and release notes</span></span>

<span data-ttu-id="b2225-190">Für alle Pakete steht eine [Referenz](http://docs.microsoft.com/java/api) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="b2225-190">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="b2225-191">Hilfe und Feedback</span><span class="sxs-lookup"><span data-stu-id="b2225-191">Get help and give feedback</span></span>

<span data-ttu-id="b2225-192">Stellen Sie in [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java) Fragen an die Community.</span><span class="sxs-lookup"><span data-stu-id="b2225-192">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="b2225-193">Melden Sie Fehler und Probleme im Zusammenhang mit den Azure-Bibliotheken für Java auf der [projektspezifischen GitHub-Seite](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="b2225-193">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
