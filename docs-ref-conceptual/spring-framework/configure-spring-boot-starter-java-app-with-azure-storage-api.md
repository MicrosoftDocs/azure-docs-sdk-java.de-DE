---
title: Verwenden von Spring Boot Starter mit der Azure Storage-API
description: Erfahren Sie, wie Sie eine Spring Boot Initializer-App mit der Azure Storage-API konfigurieren.
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 8ee985f28b7fa80548e13681089e0a5a9226851d
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506460"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-storage-api"></a><span data-ttu-id="6270d-103">Verwenden von Spring Boot Starter mit der Azure Storage-API</span><span class="sxs-lookup"><span data-stu-id="6270d-103">How to use the Spring Boot Starter with the Azure Storage API</span></span>

## <a name="overview"></a><span data-ttu-id="6270d-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="6270d-104">Overview</span></span>

<span data-ttu-id="6270d-105">In diesem Artikel wird beschrieben, wie Sie eine benutzerdefinierte Anwendung mit **Spring Initializr** erstellen und diese Anwendung anschließend verwenden, um mit der Azure Storage-API auf Azure Storage zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="6270d-105">This article walks you through creating a custom application using the **Spring Initializr**, and then using that application to access Azure storage by using the Azure Storage API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6270d-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="6270d-106">Prerequisites</span></span>

<span data-ttu-id="6270d-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="6270d-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="6270d-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) anwenden oder sich für ein [Kostenloses Azure-Konto](https://azure.microsoft.com/pricing/free-trial/) registrieren</span><span class="sxs-lookup"><span data-stu-id="6270d-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6270d-109">Die [Azure-Befehlszeilenschnittstelle (CLI)](http://docs.microsoft.com/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="6270d-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="6270d-110">Ein aktuelles [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) (ab Version 1.7)</span><span class="sxs-lookup"><span data-stu-id="6270d-110">An up-to-date [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="6270d-111">[Maven](http://maven.apache.org/) von Apache (ab Version 3.0)</span><span class="sxs-lookup"><span data-stu-id="6270d-111">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="6270d-112">Erstellen einer benutzerdefinierten Anwendung mit dem Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="6270d-112">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="6270d-113">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="6270d-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="6270d-114">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.</span><span class="sxs-lookup"><span data-stu-id="6270d-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Grundlegende Spring Initializr-Optionen](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > <span data-ttu-id="6270d-116">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt**. Beispiel: *com.contoso.wingtiptoysdemo*.</span><span class="sxs-lookup"><span data-stu-id="6270d-116">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.contoso.wingtiptoysdemo*.</span></span>
   >

1. <span data-ttu-id="6270d-117">Scrollen Sie nach unten zum Abschnitt **Azure**, und aktivieren Sie das Kontrollkästchen für **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="6270d-117">Scroll down to the **Azure** section and check the box for **Azure Storage**.</span></span>

   ![Vollständige Spring Initializr-Optionen](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. <span data-ttu-id="6270d-119">Klicken Sie am unteren Seitenrand auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="6270d-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Vollständige Spring Initializr-Optionen](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. <span data-ttu-id="6270d-121">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="6270d-121">When prompted, download the project to a path on your local computer.</span></span>

   ![Herunterladen eines benutzerdefinierten Spring Boot-Projekts](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="6270d-123">Anmelden bei Azure und Auswählen des zu verwendenden Abonnements</span><span class="sxs-lookup"><span data-stu-id="6270d-123">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="6270d-124">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="6270d-124">Open a command prompt.</span></span>

1. <span data-ttu-id="6270d-125">Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="6270d-125">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="6270d-126">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="6270d-126">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="6270d-127">Listen Sie Ihre Abonnements auf:</span><span class="sxs-lookup"><span data-stu-id="6270d-127">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="6270d-128">Azure gibt eine Liste mit Ihren Abonnements zurück. Kopieren Sie die GUID für das Abonnement, das Sie verwenden möchten. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6270d-128">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="6270d-129">Geben Sie die GUID für das Konto an, das Sie mit Azure verwenden möchten. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6270d-129">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="6270d-130">Erstellen eines Azure-Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="6270d-130">Create an Azure Storage account</span></span>

1. <span data-ttu-id="6270d-131">Erstellen Sie eine Ressourcengruppe für die in diesem Artikel verwendeten Azure-Ressourcen. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6270d-131">Create a resource group for the Azure resources you will use in this article; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="6270d-132">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="6270d-132">Where:</span></span>

   | <span data-ttu-id="6270d-133">Parameter</span><span class="sxs-lookup"><span data-stu-id="6270d-133">Parameter</span></span> | <span data-ttu-id="6270d-134">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="6270d-134">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="6270d-135">Gibt einen eindeutigen Namen für Ihre Ressourcengruppe an.</span><span class="sxs-lookup"><span data-stu-id="6270d-135">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="6270d-136">Gibt die [Azure-Region](https://azure.microsoft.com/regions/) an, in der Ihre Ressourcengruppe gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="6270d-136">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="6270d-137">Die Azure CLI zeigt die Ergebnisse der Erstellung Ihrer Ressourcengruppe an, Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6270d-137">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

2. <span data-ttu-id="6270d-138">Erstellen Sie in der Ressourcengruppe für Ihre Spring Boot-App ein Azure-Speicherkonto. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6270d-138">Create an Azure storage account in the in the resource group for your Spring Boot app; for example:</span></span>
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   <span data-ttu-id="6270d-139">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="6270d-139">Where:</span></span>

   | <span data-ttu-id="6270d-140">Parameter</span><span class="sxs-lookup"><span data-stu-id="6270d-140">Parameter</span></span> | <span data-ttu-id="6270d-141">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="6270d-141">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="6270d-142">Gibt einen eindeutigen Namen für Ihr Speicherkonto an.</span><span class="sxs-lookup"><span data-stu-id="6270d-142">Specifies a unique name for your storage account.</span></span> |
   | `resource-group` | <span data-ttu-id="6270d-143">Gibt den Namen der Ressourcengruppe an, die Sie im vorherigen Schritt erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6270d-143">Specifies the name of the resource group group you created in the previous step.</span></span> |
   | `location` | <span data-ttu-id="6270d-144">Gibt die [Azure-Region](https://azure.microsoft.com/regions/) an, in der Ihr Speicherkonto gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="6270d-144">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your storage account will be hosted.</span></span> |
   | `sku` | <span data-ttu-id="6270d-145">Gibt eine der folgenden Optionen an: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span><span class="sxs-lookup"><span data-stu-id="6270d-145">Specifies one of the following: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span></span> |

   <span data-ttu-id="6270d-146">Azure gibt eine lange JSON-Zeichenfolge mit dem Bereitstellungszustand zurück. Beispiel: |</span><span class="sxs-lookup"><span data-stu-id="6270d-146">Azure will return a long JSON string which contains the provisioning state; for example: |</span></span>

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "identity": null,
     "kind": "Storage"
       ...
       ... (A long list of values will be displayed here.)
       ...
     "statusOfPrimary": "available",
     "statusOfSecondary": null,
     "tags": {},
     "type": "Microsoft.Storage/storageAccounts"
   }
   ```

3. <span data-ttu-id="6270d-147">Rufen Sie die Verbindungszeichenfolge für Ihr Speicherkonto ab. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6270d-147">Retrieve the connection string for your storage account; for example:</span></span>
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   <span data-ttu-id="6270d-148">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="6270d-148">Where:</span></span>

   | <span data-ttu-id="6270d-149">Parameter</span><span class="sxs-lookup"><span data-stu-id="6270d-149">Parameter</span></span> | <span data-ttu-id="6270d-150">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="6270d-150">Description</span></span> |
   | ---|---|
   | `name` | <span data-ttu-id="6270d-151">Gibt einen eindeutigen Namen des Speicherkontos an, das Sie in den vorherigen Schritten erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6270d-151">Specifies a unique name of the storage account you created in previous steps.</span></span> |
   | `resource-group` | <span data-ttu-id="6270d-152">Gibt den Namen der Ressourcengruppe an, die Sie in den vorherigen Schritten erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6270d-152">Specifies the name of the resource group you created in previous steps.</span></span> |

   <span data-ttu-id="6270d-153">Azure gibt eine JSON-Zeichenfolge mit der Verbindungszeichenfolge für Ihr Speicherkonto zurück. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6270d-153">Azure will return a JSON string which contains the connection string for your storage account; for example:</span></span>

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="6270d-154">Konfigurieren und Kompilieren Ihrer Spring Boot-Anwendung</span><span class="sxs-lookup"><span data-stu-id="6270d-154">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="6270d-155">Extrahieren Sie die Dateien aus dem heruntergeladenen Projektarchiv in ein Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="6270d-155">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="6270d-156">Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="6270d-156">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="6270d-157">Fügen Sie den Schlüssel für Ihr Speicherkonto hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6270d-157">Add the key for your storage account; for example:</span></span>
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. <span data-ttu-id="6270d-158">Navigieren Sie in Ihrem Projekt zum Ordner */src/main/java/com/example/wingtiptoysdemo*, und öffnen Sie die Datei *WingtiptoysdemoApplication.java* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="6270d-158">Navigate to the */src/main/java/com/example/wingtiptoysdemo* folder in your project and open the *WingtiptoysdemoApplication.java* file in a text editor.</span></span>

1. <span data-ttu-id="6270d-159">Ersetzen Sie den vorhandenen Java-Code durch das folgende Beispiel zum Auflisten der Blobs in einem Container:</span><span class="sxs-lookup"><span data-stu-id="6270d-159">Replace the existing Java code with the following example that lists the blobs in a container:</span></span>

   ```java
   package com.example.wingtiptoysdemo;

   import com.microsoft.azure.storage.*;
   import com.microsoft.azure.storage.blob.*;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   import java.net.URISyntaxException;

   @SpringBootApplication
   public class WingtiptoysdemoApplication implements CommandLineRunner {

      @Autowired
      private CloudStorageAccount cloudStorageAccount;

      final String containerName = "mycontainer";

      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysdemoApplication.class, args);
      }

      public void run(String... var1)
             throws URISyntaxException, StorageException {
          // Create a container (if it does not exist).
          createContainerIfNotExists(containerName);
          // Upload a blob to the container.
          uploadTextBlob(containerName);
      }

      private void createContainerIfNotExists(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Create the container if it does not exist.
            container.createIfNotExists();
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }

      private void uploadTextBlob(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Get a blob reference for a text file.
            CloudBlockBlob blob = container.getBlockBlobReference("test.txt");
            // Upload some text into the blob.
            blob.uploadText("Hello World!");
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }
   }
   ```
   > [!NOTE]
   >
   > <span data-ttu-id="6270d-160">Im obigen Beispiel werden die Speicherkontoeinstellungen, die Sie in der Datei *application.properties* definiert haben, per Autowiring verwendet.</span><span class="sxs-lookup"><span data-stu-id="6270d-160">The above example autowires the storage account settings that you defined in the *application.properties* file.</span></span>
   >

1. <span data-ttu-id="6270d-161">Kompilieren Sie die Anwendung, und führen Sie sie aus:</span><span class="sxs-lookup"><span data-stu-id="6270d-161">Compile and run the application:</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

   <span data-ttu-id="6270d-162">Die Anwendung erstellt einen Container und lädt eine Textdatei als Blob in den Container hoch. Das Blob wird dann unter Ihrem Speicherkonto im [Azure-Portal](https://portal.azure.com) aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="6270d-162">The application will create a container and upload a text file as a blob to the container, which will be listed under your storage account in the [Azure portal](https://portal.azure.com).</span></span>

   ![Auflisten von Blobs im Azure-Portal](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > <span data-ttu-id="6270d-164">Beim Kompilieren Ihrer Anwendung wird unter Umständen die folgende Fehlermeldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="6270d-164">When you compile your application, you might see the following error message:</span></span>
   > 
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] BUILD FAILURE`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] Total time: 2.616 s`<br/>
   > `[INFO] Finished at: 2017-11-11T13:14:15Z`<br/>
   > `[INFO] Final Memory: 26M/213M`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2`<br/>
   > `.18.1:test (default-test) on project wingtiptoysdemo: Execution default-test of`<br/>
   > `goal org.apache.maven.plugins:maven-surefire-plugin:2.18.1:test failed: The for`<br/>
   > `ked VM terminated without properly saying goodbye. VM crash or System.exit called?`<br/>
   > `[ERROR] Command was /bin/sh -c cd /home/robert/SpringBoot/wingtiptoysdemo && /u`<br/>
   > `sr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar /home/robert/SpringBoot/wingt`<br/>
   > `iptoysdemo/target/surefire/surefirebooter6371623993063346766.jar /home/robert/S`<br/>
   > `pringBoot/wingtiptoysdemo/target/surefire/surefire5107893623933537917tmp /home/`<br/>
   > `robert/SpringBoot/wingtiptoysdemo/target/surefire/surefire_01414159391084128068tmp`<br/>
   > `[ERROR] -> [Help 1]`<br/>
   > 
   > <span data-ttu-id="6270d-165">In diesem Fall empfiehlt es sich möglicherweise, das Maven Surefire-Testen zu deaktivieren. Fügen Sie hierzu der Datei *pom.xml* den folgenden Plug-In-Eintrag hinzu:</span><span class="sxs-lookup"><span data-stu-id="6270d-165">If this happens, you might want to disable the Maven Surefire testing; to do so, add the following plugin entry in your *pom.xml* file:</span></span>
   > 
   > ```xml
   > <plugin>
   >   <groupId>org.apache.maven.plugins</groupId>
   >   <artifactId>maven-surefire-plugin</artifactId>
   >   <version>2.20.1</version>
   >   <configuration>
   >     <skipTests>true</skipTests>
   >   </configuration>
   > </plugin>
   > ```
   > 

## <a name="next-steps"></a><span data-ttu-id="6270d-166">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6270d-166">Next steps</span></span>

<span data-ttu-id="6270d-167">Weitere Informationen zu weiteren verfügbaren Spring Boot Starter-Optionen für Microsoft Azure finden Sie unter [Spring Boot Starter für Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="6270d-167">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="6270d-168">Weitere Informationen zum Integrieren von Azure-Funktionen in Spring-basierte Anwendungen finden Sie unter [Spring Framework in Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="6270d-168">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="6270d-169">Ausführliche Informationen zu weiteren Azure Storage-APIs, die Sie über Ihre Spring Boot-Anwendungen aufrufen können, finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="6270d-169">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="6270d-170">Verwenden von Azure Blob Storage mit Java</span><span class="sxs-lookup"><span data-stu-id="6270d-170">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="6270d-171">Verwenden des Warteschlangenspeichers mit Java</span><span class="sxs-lookup"><span data-stu-id="6270d-171">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="6270d-172">Verwenden von Azure Table Storage mit Java</span><span class="sxs-lookup"><span data-stu-id="6270d-172">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="6270d-173">Entwickeln für Azure Files mit Java</span><span class="sxs-lookup"><span data-stu-id="6270d-173">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)