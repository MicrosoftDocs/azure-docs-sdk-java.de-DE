---
title: "Erste Schritte mit Azure für Java mithilfe von IntelliJ"
description: "Machen Sie sich mit der grundlegenden Verwendung der Azure-Bibliotheken für Java mit Ihrem eigenen Azure-Abonnement vertraut."
keywords: Azure, Java, SDK, API, authentifizieren, erste Schritte
author: roygara
ms.author: v-rogara
manager: timlt
ms.date: 10/30/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.openlocfilehash: 1e10a7c5a46ed0e36143fd4a99decc037c04e1fe
ms.sourcegitcommit: fcf1189ede712ae30f8c7626bde50c9b8bb561bc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="get-started-with-the-azure-libraries-using-intellij"></a><span data-ttu-id="b2a9d-104">Erste Schritte mit den Azure-Bibliotheken mithilfe von IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b2a9d-104">Get started with the Azure libraries using Intellij</span></span>

<span data-ttu-id="b2a9d-105">In diesem Leitfaden werden die Schritte zum Einrichten einer Entwicklungsumgebung und zum Verwenden der Azure-Bibliotheken für Java erläutert.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-105">This guide walks you through setting up a development environment and using the Azure libraries for Java.</span></span> <span data-ttu-id="b2a9d-106">Sie erstellen einen Dienstprinzipal für die Authentifizierung mit Azure und führen Beispielcode aus, der Azure-Ressourcen in Ihrem Abonnement erstellt und verwendet.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-106">You'll create a service principal to authenticate with Azure and run some sample code that creates and uses Azure resources in your subscription.</span></span> <span data-ttu-id="b2a9d-107">Die Verwendung von IntelliJ ist für die Java-Entwicklung mit Azure optional.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-107">Using Intellij is optional for Java development with Azure.</span></span> <span data-ttu-id="b2a9d-108">Es kann jede IDE mit Maven-Integration verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-108">Any IDE that has Maven integration works.</span></span> <span data-ttu-id="b2a9d-109">Alternativ können Sie Ihren Code mit Maven über die Befehlszeile ausführen, wenn Sie keine IDE verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-109">Alternatively, you can run your code from the commandline using Maven if you prefer not to use any IDE.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2a9d-110">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="b2a9d-110">Prerequisites</span></span>

- <span data-ttu-id="b2a9d-111">Ein Azure-Konto.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-111">An Azure account.</span></span> <span data-ttu-id="b2a9d-112">Falls Sie noch kein Konto haben, können Sie eine [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-112">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="b2a9d-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) oder [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b2a9d-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="b2a9d-114">Die letzte stabile Version von [IntelliJ](https://www.jetbrains.com/idea/)</span><span class="sxs-lookup"><span data-stu-id="b2a9d-114">The latest stable version of [Intellij](https://www.jetbrains.com/idea/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="b2a9d-115">Einrichten der Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="b2a9d-115">Set up authentication</span></span>

<span data-ttu-id="b2a9d-116">Die Java-Anwendung benötigt Lese- und Schreibberechtigungen in Ihrem Azure-Abonnement, um den Beispielcode in diesem Tutorial ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-116">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="b2a9d-117">Erstellen Sie einen Dienstprinzipal, und konfigurieren Sie Ihre Anwendung so, dass sie mit dessen Anmeldeinformationen ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-117">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="b2a9d-118">Dienstprinzipale ermöglichen die Erstellung eines nicht interaktiven, Ihrer Identität zugeordneten Kontos, dem Sie nur die Berechtigungen erteilen, die zum Ausführen Ihrer App erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-118">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="b2a9d-119">[Erstellen Sie einen Dienstprinzipal](/cli/azure/create-an-azure-service-principal-azure-cli), um dem Code Berechtigungen zum Erstellen und Aktualisieren von Ressourcen in Ihrem Abonnement ohne direkte Verwendung Ihrer Kontoanmeldeinformationen zu erteilen.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-119">[Create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli) to grant your code permission to create and update resources in your subscription without using your account credentials directly.</span></span> <span data-ttu-id="b2a9d-120">Erfassen Sie unbedingt die Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-120">Make sure to capture the output.</span></span> <span data-ttu-id="b2a9d-121">Geben Sie im Kennwortargument anstelle von `MY_SECURE_PASSWORD` ein [sicheres Kennwort](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) an.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-121">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="b2a9d-122">Ihr Kennwort muss 8 bis 16 Zeichen lang sein und mindestens drei der folgenden Merkmale aufweisen:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-122">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="b2a9d-123">Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="b2a9d-123">Include lowercase characters</span></span>
* <span data-ttu-id="b2a9d-124">Großbuchstaben</span><span class="sxs-lookup"><span data-stu-id="b2a9d-124">Include uppercase characters</span></span>
* <span data-ttu-id="b2a9d-125">Zahlen</span><span class="sxs-lookup"><span data-stu-id="b2a9d-125">Include numbers</span></span>
* <span data-ttu-id="b2a9d-126">Eins der folgenden Symbole: @ # $ % ^ & * - _ !</span><span class="sxs-lookup"><span data-stu-id="b2a9d-126">Include one of the following symbols: @ # $ % ^ & * - _ !</span></span> <span data-ttu-id="b2a9d-127">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="b2a9d-127">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="b2a9d-128">?</span><span class="sxs-lookup"><span data-stu-id="b2a9d-128">?</span></span> <span data-ttu-id="b2a9d-129">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="b2a9d-129">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="b2a9d-130">Sie erhalten eine Antwort im folgenden Format:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-130">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="b2a9d-131">Kopieren Sie als Nächstes Folgendes in eine Textdatei auf Ihrem System:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-131">Next, copy the following into a text file on your system:</span></span>

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

<span data-ttu-id="b2a9d-132">Ersetzen Sie die ersten vier Werte durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-132">Replace the top four values with the following:</span></span>

- <span data-ttu-id="b2a9d-133">subscription: Verwenden Sie den *id*-Wert aus `az account show` in der Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-133">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="b2a9d-134">client: Verwenden Sie den *appId*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-134">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="b2a9d-135">key: Verwenden Sie den *password*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-135">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="b2a9d-136">tenant: Verwenden Sie den *tenant*-Wert aus der Dienstprinzipalausgabe.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-136">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="b2a9d-137">Speichern Sie diese Datei an einem sicheren Ort in Ihrem System, an dem sie vom Code gelesen werden kann.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-137">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="b2a9d-138">Sie können diese Datei für künftigen Code verwenden. Daher wird empfohlen, sie außerhalb der Anwendung in diesem Artikel zu speichern.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-138">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span> 

<span data-ttu-id="b2a9d-139">Legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` mit dem vollständigen Pfad zur Authentifizierungsdatei in Ihrer Shell fest.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-139">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>  

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="b2a9d-140">Wenn Sie eine Windows-Umgebung verwenden, fügen Sie die Variable zu Ihren Systemeigenschaften hinzu.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-140">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="b2a9d-141">Öffnen Sie PowerShell, ersetzen Sie die zweite Variable durch den Pfad zu Ihrer Datei, und geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-141">Open PowerShell and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\<fullpath>\azureauth.properties", "Machine")
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="b2a9d-142">Erstellen eines neuen Maven-Projekts</span><span class="sxs-lookup"><span data-stu-id="b2a9d-142">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="b2a9d-143">Der Beispielcode in diesem Leitfaden wird mithilfe des Maven-Erstellungstools erstellt und ausgeführt. Die Azure-Bibliotheken für Java können aber auch mit anderen Erstellungstools (beispielsweise Gradle) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-143">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="b2a9d-144">Öffnen Sie IntelliJ, und klicken Sie auf „File“ > „New“ > „Project...“ („Datei“ > „Neu“ > „Projekt“). Fahren Sie dann mit dem nächsten Bildschirm fort.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-144">Open Intellij, select File > New > Project... Then proceed to the next screen.</span></span>

<span data-ttu-id="b2a9d-145">Geben Sie „com.fabrikam“ für „groupID“ und den gewünschten Wert für „artifactID“ ein.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-145">Enter "com.fabrikam" for the groupID and enter an artifactID of your choice.</span></span>

<span data-ttu-id="b2a9d-146">Wechseln Sie zum letzten Bildschirm, und schließen Sie die Erstellung des Projekts ab.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-146">Proceed to the final screen and finish creating the project.</span></span>

<span data-ttu-id="b2a9d-147">Öffnen Sie nun die Datei „pom.xml“.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-147">Now, open the pom.xml file.</span></span> <span data-ttu-id="b2a9d-148">Fügen Sie den folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-148">And add the following code:</span></span>

```XML
<dependencies>
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
</dependencies>
```

<span data-ttu-id="b2a9d-149">Speichern Sie die Datei „pom.xml“.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-149">Save the pom.xml.</span></span>
   
## <a name="install-the-azure-toolkit-for-intellij"></a><span data-ttu-id="b2a9d-150">Installieren des Azure-Toolkits für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b2a9d-150">Install the azure toolkit for Intellij</span></span>

<span data-ttu-id="b2a9d-151">Das [Azure-Toolkit](azure-toolkit-for-intellij-installation.md) ist erforderlich, wenn Sie Web-Apps oder APIs programmgesteuert bereitstellen, wird derzeit jedoch nicht für andere Bereitstellungsarten verwendet.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-151">The [Azure toolkit](azure-toolkit-for-intellij-installation.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="b2a9d-152">Es folgt eine Zusammenfassung des Installationsvorgangs.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-152">The following is a summary of the installation process.</span></span> <span data-ttu-id="b2a9d-153">Ausführliche Schritte finden Sie unter [Installieren des Azure-Toolkits für IntelliJ](azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="b2a9d-153">For detailed stpes, visit [Installing the Azure Toolkit for IntelliJ](azure-toolkit-for-intellij-installation.md).</span></span>

<span data-ttu-id="b2a9d-154">Wählen Sie im Menü **Datei** die Option **Einstellungen...** aus.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-154">Select the **File** menu and then select **Settings...**.</span></span> 

<span data-ttu-id="b2a9d-155">Klicken Sie auf **Browse repositories...** (Repositorys durchsuchen), suchen Sie nach „Azure“, und installieren Sie dann das **Azure-Toolkit für IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-155">Select **Browse repositories...** and then search "Azure" and install the **Azure toolkit for Intellij**.</span></span>

<span data-ttu-id="b2a9d-156">Starten Sie IntelliJ neu.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-156">Restart Intellij.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="b2a9d-157">Erstellen einer virtuellen Linux-Maschine</span><span class="sxs-lookup"><span data-stu-id="b2a9d-157">Create a Linux virtual machine</span></span>

<span data-ttu-id="b2a9d-158">Erstellen Sie im Projektverzeichnis `src/main/java` eine neue Datei namens `AzureApp.java`, und fügen Sie den folgenden Codeblock ein.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-158">Create a new file named `AzureApp.java` in the project's `src/main/java` directory and paste in the following block of code.</span></span> <span data-ttu-id="b2a9d-159">Aktualisieren Sie die Variablen `userName` und `sshKey` mit echten Werten für Ihren Computer.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-159">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="b2a9d-160">Der Code erstellt einen neuen virtuellen Linux-Computer namens `testLinuxVM` in der Ressourcengruppe `sampleResourceGroup` in der Azure-Region „USA, Osten“.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-160">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

<span data-ttu-id="b2a9d-161">Öffnen Sie zum Erstellen eines `sshkey`-Elements Azure Cloud Shell, und geben Sie `ssh-keygen -t rsa -b 2048` ein.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-161">In order to create an `sshkey`, open the azure cloud shell and enter `ssh-keygen -t rsa -b 2048`.</span></span> <span data-ttu-id="b2a9d-162">Geben Sie einen Namen für die Datei ein, und rufen Sie dann die PUBLIC-Datei auf, um den Schlüssel abzurufen, den Sie im folgenden Code verwenden. Kopieren Sie den Schlüssel, und fügen Sie ihn vollständig in die Variable `sshKey` ein.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-162">Enter a name for your file and then access the .public file to get the key, which you use in the following code, copy and paste it all into your variable `sshKey`.</span></span>

```java

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


<span data-ttu-id="b2a9d-163">In der Konsole werden einige REST-Anforderungen und Antworten angezeigt, während das SDK die zugrunde liegenden Aufrufe an die REST-API ausführt, um den virtuellen Computer und die dazugehörigen Ressourcen zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-163">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="b2a9d-164">Überprüfen Sie den virtuellen Computer in Ihrem Abonnement nach Abschluss des Programms mithilfe der Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-164">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="b2a9d-165">Nachdem Sie sich vergewissert haben, dass der Code erfolgreich ausgeführt wurde, löschen Sie den virtuellen Computer und dessen Ressourcen über die Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-165">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="b2a9d-166">Bereitstellen einer Web-App aus einem GitHub-Repository</span><span class="sxs-lookup"><span data-stu-id="b2a9d-166">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="b2a9d-167">Ersetzen Sie die main-Methode in `AzureApp.java` durch die im Anschluss angegebene Methode, und legen Sie die Variable `appName` vor dem Ausführen des Codes auf einen eindeutigen Wert fest.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-167">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="b2a9d-168">Dieser Code stellt eine Webanwendung aus der Verzweigung `master` in einem öffentlichen GitHub-Repository für eine neue [Azure App Service-Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) bereit, die unter dem Tarif „Free“ ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-168">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

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

<span data-ttu-id="b2a9d-169">Führen Sie den Code wie zuvor mit Maven aus:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-169">Run the code as before using Maven:</span></span>

<span data-ttu-id="b2a9d-170">Öffnen Sie die Anwendung über die Befehlszeilenschnittstelle in einem Browser:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-170">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
<span data-ttu-id="b2a9d-171">Entfernen Sie die Web-App und den Plan aus Ihrem Abonnement, nachdem Sie die Bereitstellung überprüft haben.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-171">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="b2a9d-172">Herstellen einer Verbindung mit einer Azure SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="b2a9d-172">Connect to an Azure SQL database</span></span>

<span data-ttu-id="b2a9d-173">Ersetzen Sie die aktuelle main-Methode in `AzureApp.java` durch den im Anschluss angegebenen Code, und legen Sie die Variable `dbPassword` auf einen echten Wert fest.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-173">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="b2a9d-174">Dieser Code erstellt eine neue SQL­-Datenbank mit einer Firewallregel, die Remotezugriffe zulässt, und stellt anschließend unter Verwendung des SQL-Datenbank-JBDC-Treibers eine Verbindung mit der Datenbank her.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-174">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

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
<span data-ttu-id="b2a9d-175">Führen Sie das Beispiel über die Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-175">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="b2a9d-176">Bereinigen Sie die Ressourcen anschließend über die Befehlszeilenschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-176">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="b2a9d-177">Schreiben eines Blobs in ein neues Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="b2a9d-177">Write a blob into a new storage account</span></span>

<span data-ttu-id="b2a9d-178">Ersetzen Sie die aktuelle main-Methode in `AzureApp.java` durch den im Anschluss angegebenen Code.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-178">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="b2a9d-179">Dieser Code erstellt ein [Azure-Speicherkonto](https://docs.microsoft.com/azure/storage/storage-introduction) und anschließend unter Verwendung von Azure Storage-Bibliotheken für Java eine neue Textdatei in der Cloud.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-179">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

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

<span data-ttu-id="b2a9d-180">Führen Sie das Beispiel über die Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-180">Run the sample from the command line:</span></span>

<span data-ttu-id="b2a9d-181">Sie können über das Azure-Portal oder mit dem [Azure-Speicher-Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) zur Datei `helloazure.txt` in Ihrem Speicherkonto navigieren.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-181">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="b2a9d-182">Bereinigen Sie das Speicherkonto über die Befehlszeilenschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="b2a9d-182">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="b2a9d-183">Erkunden weiterer Beispiele</span><span class="sxs-lookup"><span data-stu-id="b2a9d-183">Explore more samples</span></span>

<span data-ttu-id="b2a9d-184">Weitere Informationen zur Ressourcenverwaltung und Aufgabenautomatisierung mit den Azure-Verwaltungsbibliotheken für Java finden Sie in unserem Beispielcode für [virtuelle Computer](../java-sdk-azure-virtual-machine-samples.md), [Web-Apps](../java-sdk-azure-web-apps-samples.md) und [SQL-Datenbank](../java-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2a9d-184">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](../java-sdk-azure-virtual-machine-samples.md), [web apps](../java-sdk-azure-web-apps-samples.md) and [SQL database](../java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="b2a9d-185">Referenz und Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="b2a9d-185">Reference and release notes</span></span>

<span data-ttu-id="b2a9d-186">Für alle Pakete steht eine [Referenz](http://docs.microsoft.com/java/api) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-186">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="b2a9d-187">Hilfe und Feedback</span><span class="sxs-lookup"><span data-stu-id="b2a9d-187">Get help and give feedback</span></span>

<span data-ttu-id="b2a9d-188">Stellen Sie in [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java) Fragen an die Community.</span><span class="sxs-lookup"><span data-stu-id="b2a9d-188">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="b2a9d-189">Melden Sie Fehler und Probleme im Zusammenhang mit den Azure-Bibliotheken für Java auf der [projektspezifischen GitHub-Seite](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="b2a9d-189">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
