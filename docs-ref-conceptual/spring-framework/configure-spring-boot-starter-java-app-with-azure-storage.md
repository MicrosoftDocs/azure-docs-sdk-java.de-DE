---
title: Verwenden von Spring Boot Starter für Azure Storage
description: Hier erfahren Sie, wie Sie eine Spring Boot Initializer-App mit Azure Storage Starter konfigurieren.
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
ms.openlocfilehash: 4838b6dbd354ad941df12933dddfa7f3e7eef905
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799966"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="62f7d-103">Verwenden von Spring Boot Starter für Azure Storage</span><span class="sxs-lookup"><span data-stu-id="62f7d-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="62f7d-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="62f7d-104">Overview</span></span>

<span data-ttu-id="62f7d-105">In diesem Artikel wird beschrieben, wie Sie mit **Spring Initializr** eine benutzerdefinierte Anwendung erstellen, Ihrer Anwendung anschließend Azure Storage Starter hinzufügen und dann mithilfe der Anwendung ein Blob in Ihr Azure-Speicherkonto hochladen.</span><span class="sxs-lookup"><span data-stu-id="62f7d-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62f7d-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="62f7d-106">Prerequisites</span></span>

<span data-ttu-id="62f7d-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="62f7d-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="62f7d-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) anwenden oder sich für ein [Kostenloses Azure-Konto](https://azure.microsoft.com/pricing/free-trial/) registrieren</span><span class="sxs-lookup"><span data-stu-id="62f7d-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="62f7d-109">Die [Azure-Befehlszeilenschnittstelle (CLI)](http://docs.microsoft.com/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="62f7d-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="62f7d-110">Ein aktuelles [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) (ab Version 1.7)</span><span class="sxs-lookup"><span data-stu-id="62f7d-110">An up-to-date [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="62f7d-111">[Maven](http://maven.apache.org/) von Apache (ab Version 3.0)</span><span class="sxs-lookup"><span data-stu-id="62f7d-111">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="62f7d-112">Für die Schritte in diesem Artikel wird mindestens die Spring Boot-Version 2.0 benötigt.</span><span class="sxs-lookup"><span data-stu-id="62f7d-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="62f7d-113">Erstellen eines Azure-Speicherkontos und Blobcontainers für Ihre Anwendung</span><span class="sxs-lookup"><span data-stu-id="62f7d-113">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="62f7d-114">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="62f7d-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="62f7d-115">Klicken Sie auf **+ Ressource erstellen**, auf **Speicher** und dann auf **Speicherkonto**.</span><span class="sxs-lookup"><span data-stu-id="62f7d-115">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Erstellen eines Azure-Speicherkontos][IMG01]

1. <span data-ttu-id="62f7d-117">Geben Sie auf der Seite **Namespace erstellen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="62f7d-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="62f7d-118">Geben Sie einen eindeutigen **Namen** ein, der als Teil des URI für Ihr Speicherkonto verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="62f7d-118">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="62f7d-119">Beispiel: Wenn Sie **wingtiptoysstorage** für **Name** eingegeben haben, lautet der URI *wingtiptoysstorage.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="62f7d-119">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="62f7d-120">Wählen Sie für **Kontoart** die Option **BLOB-Speicher** aus.</span><span class="sxs-lookup"><span data-stu-id="62f7d-120">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="62f7d-121">Geben Sie den **Speicherort** für das Speicherkonto an.</span><span class="sxs-lookup"><span data-stu-id="62f7d-121">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="62f7d-122">Wählen Sie das **Abonnement** aus, das Sie für Ihr Speicherkonto verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="62f7d-122">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="62f7d-123">Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihr Speicherkonto erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="62f7d-123">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Angeben der Optionen für das Azure-Speicherkonto][IMG02]

1. <span data-ttu-id="62f7d-125">Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Erstellen**, um das Speicherkonto zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="62f7d-125">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="62f7d-126">Nachdem Ihr Speicherkonto vom Azure-Portal erstellt wurde, klicken Sie auf **BLOBs** und dann auf **+ Container**.</span><span class="sxs-lookup"><span data-stu-id="62f7d-126">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Erstellen eines Blobcontainers][IMG03]

1. <span data-ttu-id="62f7d-128">Geben Sie einen **Namen** für den Blobcontainer ein, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="62f7d-128">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Angeben der Optionen für den Blobcontainer][IMG04]

1. <span data-ttu-id="62f7d-130">Ihr Blobcontainer wird im Azure-Portal aufgelistet, nachdem er erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="62f7d-130">The Azure portal will list your blob container after is has been created.</span></span>

   ![Überprüfen der Liste der Blobcontainer][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="62f7d-132">Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="62f7d-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="62f7d-133">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="62f7d-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="62f7d-134">Verwenden Sie die folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="62f7d-134">Specify the following options:</span></span>

   * <span data-ttu-id="62f7d-135">Generieren Sie ein **Maven**-Projekt mit **Java**.</span><span class="sxs-lookup"><span data-stu-id="62f7d-135">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="62f7d-136">Geben Sie eine **Spring Boot**-Version ab 2.0 an.</span><span class="sxs-lookup"><span data-stu-id="62f7d-136">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="62f7d-137">Geben Sie Namen für die **Gruppe** und das **Artefakt** für Ihre Anwendung an.</span><span class="sxs-lookup"><span data-stu-id="62f7d-137">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="62f7d-138">Fügen Sie die **Web**-Abhängigkeit hinzu.</span><span class="sxs-lookup"><span data-stu-id="62f7d-138">Add the **Web** dependency.</span></span>

      ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="62f7d-140">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für die **Gruppe** und das **Artefakt**, beispielsweise *com.wingtiptoys.storage*.</span><span class="sxs-lookup"><span data-stu-id="62f7d-140">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="62f7d-141">Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Generate Project** (Projekt generieren).</span><span class="sxs-lookup"><span data-stu-id="62f7d-141">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="62f7d-142">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="62f7d-142">When prompted, download the project to a path on your local computer.</span></span>

   ![Herunterladen des Spring-Projekts][SI02]

1. <span data-ttu-id="62f7d-144">Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="62f7d-144">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="62f7d-145">Konfigurieren der Spring Boot-App zur Verwendung von Azure Storage Starter</span><span class="sxs-lookup"><span data-stu-id="62f7d-145">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="62f7d-146">Suchen Sie im Stammverzeichnis Ihrer App nach der Datei *pom.xml*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-146">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="62f7d-147">Oder</span><span class="sxs-lookup"><span data-stu-id="62f7d-147">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="62f7d-148">Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie Spring Cloud Azure Storage Starter der Liste von `<dependencies>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="62f7d-148">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][SI03]

1. <span data-ttu-id="62f7d-150">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="62f7d-150">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="62f7d-151">Erstellen einer Azure-Anmeldeinformationsdatei</span><span class="sxs-lookup"><span data-stu-id="62f7d-151">Create an Azure Credential File</span></span>

1. <span data-ttu-id="62f7d-152">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="62f7d-152">Open a command prompt.</span></span>

1. <span data-ttu-id="62f7d-153">Navigieren Sie zum Verzeichnis *resources* Ihrer Spring Boot-App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-153">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="62f7d-154">Oder</span><span class="sxs-lookup"><span data-stu-id="62f7d-154">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="62f7d-155">Melden Sie sich bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="62f7d-155">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="62f7d-156">Listen Sie Ihre Abonnements auf:</span><span class="sxs-lookup"><span data-stu-id="62f7d-156">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="62f7d-157">Azure gibt eine Liste mit Ihren Abonnements zurück. Kopieren Sie die GUID für das Abonnement, das Sie verwenden möchten. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-157">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]

1. Specify the GUID for the subscription you want to use with Azure; for example:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="62f7d-158">Erstellen Sie die Azure-Anmeldeinformationsdatei:</span><span class="sxs-lookup"><span data-stu-id="62f7d-158">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="62f7d-159">Dieser Befehl erstellt im Verzeichnis *resources* eine Datei *my.azureauth*, deren Inhalt in etwa wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="62f7d-159">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="62f7d-160">Konfigurieren der Spring Boot-App zur Verwendung Ihres Azure-Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="62f7d-160">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="62f7d-161">Suchen Sie im Verzeichnis *resources* Ihrer App nach der Datei *application.properties*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-161">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="62f7d-162">Oder</span><span class="sxs-lookup"><span data-stu-id="62f7d-162">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

2. <span data-ttu-id="62f7d-163">Öffnen Sie die Datei *application.properties* in einem Text-Editor, fügen Sie die folgenden Zeilen hinzu, und ersetzen Sie dann die Beispielwerte durch die entsprechenden Eigenschaften für Ihr Speicherkonto:</span><span class="sxs-lookup"><span data-stu-id="62f7d-163">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="62f7d-164">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="62f7d-164">Where:</span></span>

   |                   <span data-ttu-id="62f7d-165">Feld</span><span class="sxs-lookup"><span data-stu-id="62f7d-165">Field</span></span>                   |                                            <span data-ttu-id="62f7d-166">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="62f7d-166">Description</span></span>                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            <span data-ttu-id="62f7d-167">Gibt die Azure-Anmeldeinformationsdatei an, die Sie zuvor in diesem Tutorial erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="62f7d-167">Specifies Azure credential file that you created earlier in this tutorial.</span></span>             |
   |    `spring.cloud.azure.resource-group`    |           <span data-ttu-id="62f7d-168">Gibt die Azure-Ressourcengruppe an, die Ihr Azure-Speicherkonto enthält.</span><span class="sxs-lookup"><span data-stu-id="62f7d-168">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span>            |
   |        `spring.cloud.azure.region`        | <span data-ttu-id="62f7d-169">Gibt die geografische Region an, die Sie beim Erstellen Ihres Azure-Speicherkontos angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="62f7d-169">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   |   `spring.cloud.azure.storage.account`    |            <span data-ttu-id="62f7d-170">Gibt das Azure-Speicherkonto an, das Sie zuvor in diesem Tutorial erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="62f7d-170">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>             |


3. <span data-ttu-id="62f7d-171">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="62f7d-171">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="62f7d-172">Hinzufügen von Beispielcode zum Implementieren grundlegender Azure-Speicherfunktionen</span><span class="sxs-lookup"><span data-stu-id="62f7d-172">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="62f7d-173">In diesem Abschnitt erstellen Sie die Java-Klassen, die erforderlich sind, um ein Blob in Ihrem Azure-Speicherkonto zu speichern.</span><span class="sxs-lookup"><span data-stu-id="62f7d-173">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="62f7d-174">Ändern der Hauptanwendungsklasse</span><span class="sxs-lookup"><span data-stu-id="62f7d-174">Modify the main application class</span></span>

1. <span data-ttu-id="62f7d-175">Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-175">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="62f7d-176">Oder</span><span class="sxs-lookup"><span data-stu-id="62f7d-176">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="62f7d-177">Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="62f7d-177">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class StorageApplication {
      public static void main(String[] args) {
         SpringApplication.run(StorageApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="62f7d-178">Speichern und schließen Sie die Java-Hauptanwendungsdatei.</span><span class="sxs-lookup"><span data-stu-id="62f7d-178">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="62f7d-179">Hinzufügen einer Webcontrollerklasse</span><span class="sxs-lookup"><span data-stu-id="62f7d-179">Add a web controller class</span></span>

1. <span data-ttu-id="62f7d-180">Erstellen Sie eine neue Java-Datei mit dem Namen *WebController.java* im Paketverzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-180">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="62f7d-181">Oder</span><span class="sxs-lookup"><span data-stu-id="62f7d-181">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="62f7d-182">Öffnen Sie die Java-Webcontrollerdatei in einem Text-Editor, und fügen Sie der Datei die folgenden Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="62f7d-182">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.core.io.Resource;
   import org.springframework.core.io.WritableResource;
   import org.springframework.util.StreamUtils;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   import java.io.IOException;
   import java.io.OutputStream;
   import java.nio.charset.Charset;

   @RestController
   public class WebController {

      @Value("blob://test/myfile.txt")
      private Resource blobFile;

      @GetMapping(value = "/")
      public String readBlobFile() throws IOException {
         return StreamUtils.copyToString(
            this.blobFile.getInputStream(),
            Charset.defaultCharset()) + "\n";
      }

      @PostMapping(value = "/")
      public String writeBlobFile(@RequestBody String data) throws IOException {
         try (OutputStream os = ((WritableResource) this.blobFile).getOutputStream()) {
            os.write(data.getBytes());
         }
         return "File was updated.\n";
      }
   }
   ```

   <span data-ttu-id="62f7d-183">Die Syntax `@Value("blob://[container]/[blob]")` definiert die Namen des Containers bzw. des Blobs, in denen Sie die Daten speichern möchten.</span><span class="sxs-lookup"><span data-stu-id="62f7d-183">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="62f7d-184">Speichern und schließen Sie die Java-Webcontrollerdatei.</span><span class="sxs-lookup"><span data-stu-id="62f7d-184">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="62f7d-185">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-185">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="62f7d-186">Oder</span><span class="sxs-lookup"><span data-stu-id="62f7d-186">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="62f7d-187">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-187">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="62f7d-188">Sobald Ihre Anwendung ausgeführt wird, können Sie sie mit *curl* testen. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="62f7d-188">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="62f7d-189">a.</span><span class="sxs-lookup"><span data-stu-id="62f7d-189">a.</span></span> <span data-ttu-id="62f7d-190">Senden Sie eine POST-Anforderung zum Aktualisieren des Inhalts einer Datei:</span><span class="sxs-lookup"><span data-stu-id="62f7d-190">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="62f7d-191">Es sollte eine Antwort angezeigt werden, dass die Datei aktualisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="62f7d-191">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="62f7d-192">b.</span><span class="sxs-lookup"><span data-stu-id="62f7d-192">b.</span></span> <span data-ttu-id="62f7d-193">Senden Sie eine GET-Anforderung zum Überprüfen des Inhalts der Datei:</span><span class="sxs-lookup"><span data-stu-id="62f7d-193">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="62f7d-194">Der von Ihnen bereitgestellte Text „Hallo Welt“ sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="62f7d-194">You should see the "Hello World" text that you posted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62f7d-195">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="62f7d-195">Next steps</span></span>

<span data-ttu-id="62f7d-196">Weitere Informationen zu weiteren verfügbaren Spring Boot Starter-Optionen für Microsoft Azure finden Sie unter [Spring Boot Starter für Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="62f7d-196">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="62f7d-197">Weitere Informationen zum Integrieren von Azure-Funktionen in Spring-basierte Anwendungen finden Sie unter [Spring Framework in Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="62f7d-197">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="62f7d-198">Ausführliche Informationen zu weiteren Azure Storage-APIs, die Sie über Ihre Spring Boot-Anwendungen aufrufen können, finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="62f7d-198">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="62f7d-199">Verwenden von Azure Blob Storage mit Java</span><span class="sxs-lookup"><span data-stu-id="62f7d-199">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="62f7d-200">Verwenden des Warteschlangenspeichers mit Java</span><span class="sxs-lookup"><span data-stu-id="62f7d-200">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="62f7d-201">Verwenden von Azure Table Storage mit Java</span><span class="sxs-lookup"><span data-stu-id="62f7d-201">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="62f7d-202">Entwickeln für Azure Files mit Java</span><span class="sxs-lookup"><span data-stu-id="62f7d-202">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
