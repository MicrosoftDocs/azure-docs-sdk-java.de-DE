---
title: Erstellen einer Spring Cloud Stream Binder-Anwendung mit Azure Event Hubs
description: Erfahren Sie, wie Sie eine mit Spring Boot Initializer erstellte Java-basierte Spring Cloud Stream Binder-Anwendung mit Azure Event Hubs konfigurieren.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: 49fd85690d21fa2eb4a2830e3958ef21cbd2e8c1
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338894"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a><span data-ttu-id="51705-103">Erstellen einer Spring Cloud Stream Binder-Anwendung mit Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="51705-103">How to create a Spring Cloud Stream Binder application with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="51705-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="51705-104">Overview</span></span>

<span data-ttu-id="51705-105">In diesem Artikel wird beschrieben, wie Sie eine mit Spring Boot Initializer erstellte Java-basierte Spring Cloud Stream Binder-Anwendung mit Azure Event Hubs konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="51705-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializer with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51705-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="51705-106">Prerequisites</span></span>

<span data-ttu-id="51705-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="51705-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="51705-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="51705-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="51705-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="51705-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="51705-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="51705-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="51705-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="51705-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="51705-112">Für die Schritte in diesem Artikel wird mindestens die Spring Boot-Version 2.0 benötigt.</span><span class="sxs-lookup"><span data-stu-id="51705-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="51705-113">Erstellen eines Azure Event Hubs über das Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="51705-113">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="51705-114">Erstellen eines Azure Event Hub-Namespaces</span><span class="sxs-lookup"><span data-stu-id="51705-114">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="51705-115">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="51705-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="51705-116">Klicken Sie auf **+ Ressource erstellen**, auf **Internet der Dinge** und dann auf **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="51705-116">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Erstellen eines Azure Event Hub-Namespaces][IMG01]

1. <span data-ttu-id="51705-118">Geben Sie auf der Seite **Namespace erstellen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="51705-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="51705-119">Geben Sie einen eindeutigen **Namen** ein, der als Teil des URI für Ihren Event Hub-Namespace verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="51705-119">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="51705-120">Beispiel: Wenn Sie **wingtiptoys** für **Name** eingegeben haben, lautet der URI *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="51705-120">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="51705-121">Wählen Sie einen **Tarif** für Ihren Event Hub-Namespace aus.</span><span class="sxs-lookup"><span data-stu-id="51705-121">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="51705-122">Wählen Sie das **Abonnement** aus, das Sie für Ihren Namespace verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="51705-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="51705-123">Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihren Namespace erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="51705-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="51705-124">Geben Sie den **Speicherort** für Ihren Event Hub-Namespace an.</span><span class="sxs-lookup"><span data-stu-id="51705-124">Specify the **Location** for your event hub namespace.</span></span>

   ![Angeben der Optionen für den Azure Event Hub-Namespace][IMG02]

1. <span data-ttu-id="51705-126">Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Erstellen**, um den Namespace zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="51705-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="51705-127">Erstellen eines Azure Event Hubs in Ihrem Namespace</span><span class="sxs-lookup"><span data-stu-id="51705-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="51705-128">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="51705-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="51705-129">Klicken Sie auf **Alle Ressourcen** und dann auf den von Ihnen erstellten Namespace.</span><span class="sxs-lookup"><span data-stu-id="51705-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Auswählen des Azure Event Hub-Namespaces][IMG03]

1. <span data-ttu-id="51705-131">Klicken Sie auf **Event Hubs** und dann auf **+ Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="51705-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Hinzufügen eines neuen Azure Event Hubs][IMG04]

1. <span data-ttu-id="51705-133">Geben Sie auf der Seite **Event Hub erstellen** einen eindeutigen **Namen** für Ihren Event Hub ein, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="51705-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Erstellen eines Azure Event Hubs][IMG05]

1. <span data-ttu-id="51705-135">Nachdem Ihr Event Hub erstellt wurde, wird er auf der Seite **Event Hubs** aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="51705-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Erstellen eines Azure Event Hubs][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a><span data-ttu-id="51705-137">Erstellen eines Azure-Speicherkontos für Ihre Event Hub-Prüfpunkte</span><span class="sxs-lookup"><span data-stu-id="51705-137">Create an Azure Storage Account for your Event Hub checkpoints</span></span>

1. <span data-ttu-id="51705-138">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="51705-138">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="51705-139">Klicken Sie auf **+ Ressource erstellen**, auf **Speicher** und dann auf **Speicherkonto**.</span><span class="sxs-lookup"><span data-stu-id="51705-139">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Erstellen eines Azure-Speicherkontos][IMG07]

1. <span data-ttu-id="51705-141">Geben Sie auf der Seite **Namespace erstellen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="51705-141">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="51705-142">Geben Sie einen eindeutigen **Namen** ein, der als Teil des URI für Ihr Speicherkonto verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="51705-142">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="51705-143">Beispiel: Wenn Sie **wingtiptoys** für **Name** eingegeben haben, lautet der URI *wingtiptoys.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="51705-143">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.core.windows.net*.</span></span>
   * <span data-ttu-id="51705-144">Wählen Sie für **Kontoart** die Option **BLOB-Speicher** aus.</span><span class="sxs-lookup"><span data-stu-id="51705-144">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="51705-145">Geben Sie den **Speicherort** für das Speicherkonto an.</span><span class="sxs-lookup"><span data-stu-id="51705-145">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="51705-146">Wählen Sie das **Abonnement** aus, das Sie für Ihr Speicherkonto verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="51705-146">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="51705-147">Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihr Speicherkonto erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="51705-147">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Angeben der Optionen für das Azure-Speicherkonto][IMG08]

1. <span data-ttu-id="51705-149">Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Erstellen**, um das Speicherkonto zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="51705-149">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="51705-150">Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="51705-150">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="51705-151">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="51705-151">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="51705-152">Verwenden Sie die folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="51705-152">Specify the following options:</span></span>

   * <span data-ttu-id="51705-153">Generieren Sie ein **Maven**-Projekt mit **Java**.</span><span class="sxs-lookup"><span data-stu-id="51705-153">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="51705-154">Geben Sie eine **Spring Boot**-Version ab 2.0 an.</span><span class="sxs-lookup"><span data-stu-id="51705-154">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="51705-155">Geben Sie Namen für die **Gruppe** und das **Artefakt** für Ihre Anwendung an.</span><span class="sxs-lookup"><span data-stu-id="51705-155">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="51705-156">Fügen Sie die **Web**-Abhängigkeit hinzu.</span><span class="sxs-lookup"><span data-stu-id="51705-156">Add the **Web** dependency.</span></span>

      ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="51705-158">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für die **Gruppe** und das **Artefakt**, beispielsweise *com.wingtiptoys.eventhub*.</span><span class="sxs-lookup"><span data-stu-id="51705-158">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.eventhub*.</span></span>
   >

1. <span data-ttu-id="51705-159">Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Generate Project** (Projekt generieren).</span><span class="sxs-lookup"><span data-stu-id="51705-159">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="51705-160">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="51705-160">When prompted, download the project to a path on your local computer.</span></span>

   ![Herunterladen des Spring-Projekts][SI02]

1. <span data-ttu-id="51705-162">Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="51705-162">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a><span data-ttu-id="51705-163">Konfigurieren der Spring Boot-App zur Verwendung von Azure Event Hub Starter</span><span class="sxs-lookup"><span data-stu-id="51705-163">Configure your Spring Boot app to use the Azure Event Hub starter</span></span>

1. <span data-ttu-id="51705-164">Suchen Sie im Stammverzeichnis Ihrer App nach der Datei *pom.xml*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="51705-164">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\pom.xml`

   <span data-ttu-id="51705-165">Oder</span><span class="sxs-lookup"><span data-stu-id="51705-165">-or-</span></span>

   `/users/example/home/eventhub/pom.xml`

1. <span data-ttu-id="51705-166">Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie Spring Cloud Azure Event Hub Stream Binder Starter der Liste von `<dependencies>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="51705-166">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Event Hub Stream Binder starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][SI03]

1. <span data-ttu-id="51705-168">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="51705-168">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="51705-169">Erstellen einer Azure-Anmeldeinformationsdatei</span><span class="sxs-lookup"><span data-stu-id="51705-169">Create an Azure Credential File</span></span>

1. <span data-ttu-id="51705-170">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="51705-170">Open a command prompt.</span></span>

1. <span data-ttu-id="51705-171">Navigieren Sie zum Verzeichnis *resources* Ihrer Spring Boot-App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="51705-171">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="51705-172">Oder</span><span class="sxs-lookup"><span data-stu-id="51705-172">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="51705-173">Melden Sie sich bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="51705-173">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="51705-174">Listen Sie Ihre Abonnements auf:</span><span class="sxs-lookup"><span data-stu-id="51705-174">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="51705-175">Azure gibt eine Liste mit Ihren Abonnements zurück. Kopieren Sie die GUID für das Abonnement, das Sie verwenden möchten. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="51705-175">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="51705-176">Erstellen Sie die Azure-Anmeldeinformationsdatei:</span><span class="sxs-lookup"><span data-stu-id="51705-176">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="51705-177">Dieser Befehl erstellt im Verzeichnis *resources* eine Datei *my.azureauth*, deren Inhalt in etwa wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="51705-177">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="51705-178">Konfigurieren der Spring Boot-App zur Verwendung Ihres Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="51705-178">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="51705-179">Suchen Sie im Verzeichnis *resources* Ihrer App nach der Datei *application.properties*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="51705-179">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="51705-180">Oder</span><span class="sxs-lookup"><span data-stu-id="51705-180">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="51705-181">Öffnen Sie die Datei *application.properties* in einem Text-Editor, fügen Sie die folgenden Zeilen hinzu, und ersetzen Sie dann die Beispielwerte durch die entsprechenden Eigenschaften für Ihren Event Hub:</span><span class="sxs-lookup"><span data-stu-id="51705-181">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace
   spring.cloud.azure.eventhub.checkpoint-storage-account=wingtiptoysstorage
   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   spring.cloud.stream.eventhub.bindings.input.consumer.checkpoint-mode=MANUAL
   ```
   <span data-ttu-id="51705-182">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="51705-182">Where:</span></span>

   |                          <span data-ttu-id="51705-183">Feld</span><span class="sxs-lookup"><span data-stu-id="51705-183">Field</span></span>                           |                                                                                   <span data-ttu-id="51705-184">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="51705-184">Description</span></span>                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    <span data-ttu-id="51705-185">Gibt die Azure-Anmeldeinformationsdatei an, die Sie zuvor in diesem Tutorial erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="51705-185">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      <span data-ttu-id="51705-186">Gibt die Azure-Ressourcengruppe an, die Ihren Azure Event Hub enthält.</span><span class="sxs-lookup"><span data-stu-id="51705-186">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |               `spring.cloud.azure.region`                |                                           <span data-ttu-id="51705-187">Gibt die geografische Region an, die Sie beim Erstellen Ihres Azure Event Hubs angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="51705-187">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          <span data-ttu-id="51705-188">Gibt den eindeutigen Namen an, den Sie beim Erstellen Ihres Azure Event Hub-Namespaces angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="51705-188">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    <span data-ttu-id="51705-189">Gibt das Azure-Speicherkonto an, das Sie zuvor in diesem Tutorial erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="51705-189">Specifies Azure Storage Account that you created earlier in this tutorial.</span></span>                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            <span data-ttu-id="51705-190">Gibt den Azure Event Hub an, der das Eingabeziel ist (in diesem Fall ist dies der Hub, den Sie zuvor in diesem Tutorial erstellt haben).</span><span class="sxs-lookup"><span data-stu-id="51705-190">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |       `spring.cloud.stream.bindings.input.group `        | <span data-ttu-id="51705-191">Gibt eine Consumergruppe von Azure Event Hub an, die auf „$Default“ festgelegt werden kann, um die grundlegende Consumergruppe zu verwenden, die bei der Erstellung Ihres Azure Event Hubs erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="51705-191">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   |    `spring.cloud.stream.bindings.output.destination`     |                               <span data-ttu-id="51705-192">Gibt den Azure Event Hub an, der das Ausgabeziel ist (in diesem Tutorial ist das Ausgabeziel mit dem Eingabeziel identisch).</span><span class="sxs-lookup"><span data-stu-id="51705-192">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="51705-193">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="51705-193">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="51705-194">Hinzufügen von Beispielcode zum Implementieren grundlegender Event Hub-Funktionen</span><span class="sxs-lookup"><span data-stu-id="51705-194">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="51705-195">In diesem Abschnitt erstellen Sie die Java-Klassen, die erforderlich sind, um Ereignisse an Ihren Event Hub zu senden.</span><span class="sxs-lookup"><span data-stu-id="51705-195">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="51705-196">Ändern der Hauptanwendungsklasse</span><span class="sxs-lookup"><span data-stu-id="51705-196">Modify the main application class</span></span>

1. <span data-ttu-id="51705-197">Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="51705-197">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   <span data-ttu-id="51705-198">Oder</span><span class="sxs-lookup"><span data-stu-id="51705-198">-or-</span></span>

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. <span data-ttu-id="51705-199">Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="51705-199">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class EventhubApplication {
      public static void main(String[] args) {
         SpringApplication.run(EventhubApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="51705-200">Speichern und schließen Sie die Java-Hauptanwendungsdatei.</span><span class="sxs-lookup"><span data-stu-id="51705-200">Save and close the main application Java file.</span></span>

### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="51705-201">Erstellen einer neuen Klasse für den Quellconnector</span><span class="sxs-lookup"><span data-stu-id="51705-201">Create a new class for the source connector</span></span>

1. <span data-ttu-id="51705-202">Erstellen Sie eine neue Java-Datei mit dem Namen *EventhubSource.java* im Paketverzeichnis Ihrer App, öffnen Sie die Datei in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="51705-202">Create a new Java file named *EventhubSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class EventhubSource {

      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String postMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```
1. <span data-ttu-id="51705-203">Speichern und schließen Sie die Datei *EventhubSource.java*.</span><span class="sxs-lookup"><span data-stu-id="51705-203">Save and close the *EventhubSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="51705-204">Erstellen einer neuen Klasse für den Senkenconnector</span><span class="sxs-lookup"><span data-stu-id="51705-204">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="51705-205">Erstellen Sie eine neue Java-Datei mit dem Namen *EventhubSink.java* im Paketverzeichnis Ihrer App, öffnen Sie die Datei in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="51705-205">Create a new Java file named *EventhubSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import com.microsoft.azure.spring.integration.core.AzureHeaders;
   import com.microsoft.azure.spring.integration.core.api.Checkpointer;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   import org.springframework.messaging.handler.annotation.Header;

   @EnableBinding(Sink.class)
   public class EventhubSink {

      private static final Logger LOGGER = LoggerFactory.getLogger(EventhubSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message, @Header(AzureHeaders.CHECKPOINTER) Checkpointer checkpointer) {
         LOGGER.info("New message received: '{}'", message);
         checkpointer.success().handle((r, ex) -> {
            if (ex == null) {
               LOGGER.info("Message '{}' successfully checkpointed", message);
            }
            return null;
         });
      }
   }
   ```

1. <span data-ttu-id="51705-206">Speichern und schließen Sie die Datei *EventhubSink.java*.</span><span class="sxs-lookup"><span data-stu-id="51705-206">Save and close the *EventhubSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="51705-207">Erstellen und Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="51705-207">Build and test your application</span></span>

1. <span data-ttu-id="51705-208">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="51705-208">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\eventhub`

   <span data-ttu-id="51705-209">Oder</span><span class="sxs-lookup"><span data-stu-id="51705-209">-or-</span></span>

   `cd /users/example/home/eventhub`

1. <span data-ttu-id="51705-210">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="51705-210">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="51705-211">Sobald Ihre Anwendung ausgeführt wird, können Sie sie mit *curl* testen. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="51705-211">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="51705-212">In den Protokollen Ihrer Anwendung sollte „hello“ angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="51705-212">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="51705-213">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="51705-213">For example:</span></span>

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a><span data-ttu-id="51705-214">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="51705-214">Next steps</span></span>

<span data-ttu-id="51705-215">Weitere Informationen zur Azure-Unterstützung für Event Hub Stream Binder finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="51705-215">For more information about Azure support for Event Hub Stream Binder, see the following articles:</span></span>

* [<span data-ttu-id="51705-216">Was ist Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="51705-216">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="51705-217">Erstellen eines Event Hubs-Namespaces und eines Event Hubs mithilfe des Azure-Portals</span><span class="sxs-lookup"><span data-stu-id="51705-217">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="51705-218">Verwenden von Spring Boot Starter für Apache Kafka mit Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="51705-218">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)

<span data-ttu-id="51705-219">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter „Azure für Java-Entwickler“ und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="51705-219">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="51705-220">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="51705-220">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="51705-221">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="51705-221">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="51705-222">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="51705-222">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="51705-223">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="51705-223">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-03.png
