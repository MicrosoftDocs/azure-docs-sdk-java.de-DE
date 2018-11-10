---
title: Verwenden von Spring Boot Starter für Apache Kafka mit Azure Event Hubs
description: Erfahren Sie, wie Sie eine mit Spring Boot Initializer erstellte Anwendung zur Verwendung von Apache Kafka mit Azure Event Hubs konfigurieren.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: ccef834d0ff1c40b061946f8ab1852584da80d7b
ms.sourcegitcommit: a168dc8c2396b6c4749abef03debb1f69298da38
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2018
ms.locfileid: "50747001"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a><span data-ttu-id="d09ef-103">Verwenden von Spring Boot Starter für Apache Kafka mit Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d09ef-103">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="d09ef-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="d09ef-104">Overview</span></span>

<span data-ttu-id="d09ef-105">In diesem Artikel wird beschrieben, wie Sie eine mit Spring Boot Initializer erstellte Java-basierte Spring Cloud Stream Binder-Anwendung zur Verwendung von [Apache Kafka] mit Azure Event Hubs konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d09ef-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder created with the Spring Boot Initializer to use [Apache Kafka] with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d09ef-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="d09ef-106">Prerequisites</span></span>

<span data-ttu-id="d09ef-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="d09ef-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="d09ef-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="d09ef-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d09ef-109">[Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="d09ef-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="d09ef-110">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="d09ef-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="d09ef-111">Für die Schritte in diesem Artikel wird mindestens die Spring Boot-Version 2.0 benötigt.</span><span class="sxs-lookup"><span data-stu-id="d09ef-111">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="d09ef-112">Erstellen eines Azure Event Hubs über das Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="d09ef-112">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="d09ef-113">Erstellen eines Azure Event Hub-Namespaces</span><span class="sxs-lookup"><span data-stu-id="d09ef-113">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="d09ef-114">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="d09ef-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="d09ef-115">Klicken Sie auf **+ Ressource erstellen**, auf **Internet der Dinge** und dann auf **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="d09ef-115">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Erstellen eines Azure Event Hub-Namespaces][IMG01]

1. <span data-ttu-id="d09ef-117">Geben Sie auf der Seite **Namespace erstellen** die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="d09ef-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="d09ef-118">Geben Sie einen eindeutigen **Namen** ein, der als Teil des URI für Ihren Event Hub-Namespace verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="d09ef-118">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="d09ef-119">Beispiel: Wenn Sie **wingtiptoys** für **Name** eingegeben haben, lautet der URI *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="d09ef-119">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="d09ef-120">Wählen Sie einen **Tarif** für Ihren Event Hub-Namespace aus.</span><span class="sxs-lookup"><span data-stu-id="d09ef-120">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="d09ef-121">Geben Sie **Kafka aktivieren** für Ihren Namespace an.</span><span class="sxs-lookup"><span data-stu-id="d09ef-121">Specify **Enable Kafka** for your namespace.</span></span>
   * <span data-ttu-id="d09ef-122">Wählen Sie das **Abonnement** aus, das Sie für Ihren Namespace verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="d09ef-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="d09ef-123">Legen Sie fest, ob eine neue **Ressourcengruppe** für Ihren Namespace erstellt werden soll, oder wählen Sie eine vorhandene Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="d09ef-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="d09ef-124">Geben Sie den **Speicherort** für Ihren Event Hub-Namespace an.</span><span class="sxs-lookup"><span data-stu-id="d09ef-124">Specify the **Location** for your event hub namespace.</span></span>

   ![Angeben der Optionen für den Azure Event Hub-Namespace][IMG02]

1. <span data-ttu-id="d09ef-126">Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Erstellen**, um den Namespace zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d09ef-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="d09ef-127">Erstellen eines Azure Event Hubs in Ihrem Namespace</span><span class="sxs-lookup"><span data-stu-id="d09ef-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="d09ef-128">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="d09ef-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="d09ef-129">Klicken Sie auf **Alle Ressourcen** und dann auf den von Ihnen erstellten Namespace.</span><span class="sxs-lookup"><span data-stu-id="d09ef-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Auswählen des Azure Event Hub-Namespaces][IMG03]

1. <span data-ttu-id="d09ef-131">Klicken Sie auf **Event Hubs** und dann auf **+ Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="d09ef-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Hinzufügen eines neuen Azure Event Hubs][IMG04]

1. <span data-ttu-id="d09ef-133">Geben Sie auf der Seite **Event Hub erstellen** einen eindeutigen **Namen** für Ihren Event Hub ein, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d09ef-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Erstellen eines Azure Event Hubs][IMG05]

1. <span data-ttu-id="d09ef-135">Nachdem Ihr Event Hub erstellt wurde, wird er auf der Seite **Event Hubs** aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="d09ef-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Erstellen eines Azure Event Hubs][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="d09ef-137">Erstellen einer einfachen Spring Boot-Anwendung mit Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="d09ef-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="d09ef-138">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="d09ef-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="d09ef-139">Verwenden Sie die folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="d09ef-139">Specify the following options:</span></span>

   * <span data-ttu-id="d09ef-140">Generieren Sie ein **Maven**-Projekt mit **Java**.</span><span class="sxs-lookup"><span data-stu-id="d09ef-140">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="d09ef-141">Geben Sie eine **Spring Boot**-Version ab 2.0 an.</span><span class="sxs-lookup"><span data-stu-id="d09ef-141">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="d09ef-142">Geben Sie Namen für die **Gruppe** und das **Artefakt** für Ihre Anwendung an.</span><span class="sxs-lookup"><span data-stu-id="d09ef-142">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="d09ef-143">Fügen Sie die **Web**-Abhängigkeit hinzu.</span><span class="sxs-lookup"><span data-stu-id="d09ef-143">Add the **Web** dependency.</span></span>

      ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="d09ef-145">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für die **Gruppe** und das **Artefakt**, beispielsweise *com.wingtiptoys.kafka*.</span><span class="sxs-lookup"><span data-stu-id="d09ef-145">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.kafka*.</span></span>
   >

1. <span data-ttu-id="d09ef-146">Nachdem Sie die oben genannten Optionen angegeben haben, klicken Sie auf **Generate Project** (Projekt generieren).</span><span class="sxs-lookup"><span data-stu-id="d09ef-146">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="d09ef-147">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="d09ef-147">When prompted, download the project to a path on your local computer.</span></span>

   ![Herunterladen des Spring-Projekts][SI02]

1. <span data-ttu-id="d09ef-149">Nachdem Sie die Dateien auf Ihrem lokalen System extrahiert haben, kann Ihre einfache Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="d09ef-149">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a><span data-ttu-id="d09ef-150">Konfigurieren der Spring Boot-App zur Verwendung von Spring Cloud Kafka Stream und Azure Event Hub Starter</span><span class="sxs-lookup"><span data-stu-id="d09ef-150">Configure your Spring Boot app to use the Spring Cloud Kafka Stream and Azure Event Hub starters</span></span>

1. <span data-ttu-id="d09ef-151">Suchen Sie im Stammverzeichnis Ihrer App nach der Datei *pom.xml*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-151">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\pom.xml`

   <span data-ttu-id="d09ef-152">Oder</span><span class="sxs-lookup"><span data-stu-id="d09ef-152">-or-</span></span>

   `/users/example/home/kafka/pom.xml`

1. <span data-ttu-id="d09ef-153">Öffnen Sie die Datei *pom.xml* in einem Text-Editor, und fügen Sie Spring Cloud Kafka Stream und Azure Event Hub Starter der Liste von `<dependencies>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="d09ef-153">Open the *pom.xml* file in a text editor, and add the Spring Cloud Kafka Stream and Azure Event Hub starters to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-stream-kafka</artifactId>
      <version>2.0.1.RELEASE</version>
   </dependency>
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-starter-eventhub</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Bearbeiten der Datei „pom.xml“][SI03]

1. <span data-ttu-id="d09ef-155">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="d09ef-155">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="d09ef-156">Erstellen einer Azure-Anmeldeinformationsdatei</span><span class="sxs-lookup"><span data-stu-id="d09ef-156">Create an Azure Credential File</span></span>

1. <span data-ttu-id="d09ef-157">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="d09ef-157">Open a command prompt.</span></span>

1. <span data-ttu-id="d09ef-158">Navigieren Sie zum Verzeichnis *resources* Ihrer Spring Boot-App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-158">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="d09ef-159">Oder</span><span class="sxs-lookup"><span data-stu-id="d09ef-159">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="d09ef-160">Melden Sie sich bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="d09ef-160">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="d09ef-161">Listen Sie Ihre Abonnements auf:</span><span class="sxs-lookup"><span data-stu-id="d09ef-161">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="d09ef-162">Azure gibt eine Liste mit Ihren Abonnements zurück. Kopieren Sie die GUID für das Abonnement, das Sie verwenden möchten. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-162">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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
   ```
   
1. <span data-ttu-id="d09ef-163">Geben Sie die GUID für das Abonnement an, das Sie mit Azure verwenden möchten. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-163">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="d09ef-164">Erstellen Sie die Azure-Anmeldeinformationsdatei:</span><span class="sxs-lookup"><span data-stu-id="d09ef-164">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="d09ef-165">Dieser Befehl erstellt im Verzeichnis *resources* eine Datei *my.azureauth*, deren Inhalt in etwa wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="d09ef-165">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="d09ef-166">Konfigurieren der Spring Boot-App zur Verwendung Ihres Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d09ef-166">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="d09ef-167">Suchen Sie im Verzeichnis *resources* Ihrer App nach der Datei *application.properties*. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-167">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="d09ef-168">Oder</span><span class="sxs-lookup"><span data-stu-id="d09ef-168">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="d09ef-169">Öffnen Sie die Datei *application.properties* in einem Text-Editor, fügen Sie die folgenden Zeilen hinzu, und ersetzen Sie dann die Beispielwerte durch die entsprechenden Eigenschaften für Ihren Event Hub:</span><span class="sxs-lookup"><span data-stu-id="d09ef-169">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   <span data-ttu-id="d09ef-170">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="d09ef-170">Where:</span></span>

   |                       <span data-ttu-id="d09ef-171">Feld</span><span class="sxs-lookup"><span data-stu-id="d09ef-171">Field</span></span>                       |                                                                                   <span data-ttu-id="d09ef-172">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="d09ef-172">Description</span></span>                                                                                    |
   |---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `spring.cloud.azure.credential-file-path`     |                                                    <span data-ttu-id="d09ef-173">Gibt die Azure-Anmeldeinformationsdatei an, die Sie zuvor in diesem Tutorial erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="d09ef-173">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |        `spring.cloud.azure.resource-group`        |                                                      <span data-ttu-id="d09ef-174">Gibt die Azure-Ressourcengruppe an, die Ihren Azure Event Hub enthält.</span><span class="sxs-lookup"><span data-stu-id="d09ef-174">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |            `spring.cloud.azure.region`            |                                           <span data-ttu-id="d09ef-175">Gibt die geografische Region an, die Sie beim Erstellen Ihres Azure Event Hubs angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="d09ef-175">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |      `spring.cloud.azure.eventhub.namespace`      |                                          <span data-ttu-id="d09ef-176">Gibt den eindeutigen Namen an, den Sie beim Erstellen Ihres Azure Event Hub-Namespaces angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="d09ef-176">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.stream.bindings.input.destination`  |                            <span data-ttu-id="d09ef-177">Gibt den Azure Event Hub an, der das Eingabeziel ist (in diesem Fall ist dies der Hub, den Sie zuvor in diesem Tutorial erstellt haben).</span><span class="sxs-lookup"><span data-stu-id="d09ef-177">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |    `spring.cloud.stream.bindings.input.group `    | <span data-ttu-id="d09ef-178">Gibt eine Consumergruppe von Azure Event Hub an, die auf „$Default“ festgelegt werden kann, um die grundlegende Consumergruppe zu verwenden, die bei der Erstellung Ihres Azure Event Hubs erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="d09ef-178">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.stream.bindings.output.destination` |                               <span data-ttu-id="d09ef-179">Gibt den Azure Event Hub an, der das Ausgabeziel ist (in diesem Tutorial ist das Ausgabeziel mit dem Eingabeziel identisch).</span><span class="sxs-lookup"><span data-stu-id="d09ef-179">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="d09ef-180">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="d09ef-180">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="d09ef-181">Hinzufügen von Beispielcode zum Implementieren grundlegender Event Hub-Funktionen</span><span class="sxs-lookup"><span data-stu-id="d09ef-181">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="d09ef-182">In diesem Abschnitt erstellen Sie die Java-Klassen, die erforderlich sind, um Ereignisse an Ihren Event Hub zu senden.</span><span class="sxs-lookup"><span data-stu-id="d09ef-182">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="d09ef-183">Ändern der Hauptanwendungsklasse</span><span class="sxs-lookup"><span data-stu-id="d09ef-183">Modify the main application class</span></span>

1. <span data-ttu-id="d09ef-184">Suchen Sie die Java-Hauptanwendungsdatei im Paketverzeichnis Ihrer App. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-184">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   <span data-ttu-id="d09ef-185">Oder</span><span class="sxs-lookup"><span data-stu-id="d09ef-185">-or-</span></span>

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. <span data-ttu-id="d09ef-186">Öffnen Sie die Java-Hauptanwendungsdatei in einem Text-Editor, und fügen Sie die folgenden Zeilen zur Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="d09ef-186">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class KafkaApplication {
      public static void main(String[] args) {
         SpringApplication.run(KafkaApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="d09ef-187">Speichern und schließen Sie die Java-Hauptanwendungsdatei.</span><span class="sxs-lookup"><span data-stu-id="d09ef-187">Save and close the main application Java file.</span></span>


### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="d09ef-188">Erstellen einer neuen Klasse für den Quellconnector</span><span class="sxs-lookup"><span data-stu-id="d09ef-188">Create a new class for the source connector</span></span>

1. <span data-ttu-id="d09ef-189">Erstellen Sie eine neue Java-Datei mit dem Namen *KafkaSource.java* im Paketverzeichnis Ihrer App, öffnen Sie die Datei in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="d09ef-189">Create a new Java file named *KafkaSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class KafkaSource {
      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String sendMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```

1. <span data-ttu-id="d09ef-190">Speichern und schließen Sie die Datei *KafkaSource.java*.</span><span class="sxs-lookup"><span data-stu-id="d09ef-190">Save and close the *KafkaSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="d09ef-191">Erstellen einer neuen Klasse für den Senkenconnector</span><span class="sxs-lookup"><span data-stu-id="d09ef-191">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="d09ef-192">Erstellen Sie eine neue Java-Datei mit dem Namen *KafkaSink.java* im Paketverzeichnis Ihrer App, öffnen Sie die Datei in einem Text-Editor, und fügen Sie folgende Zeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="d09ef-192">Create a new Java file named *KafkaSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;

   @EnableBinding(Sink.class)
   public class KafkaSink {
      private static final Logger LOGGER = LoggerFactory.getLogger(KafkaSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message) {
         LOGGER.info("New message received: " + message);
      }
   }
   ```

1. <span data-ttu-id="d09ef-193">Speichern und schließen Sie die Datei *KafkaSink.java*.</span><span class="sxs-lookup"><span data-stu-id="d09ef-193">Save and close the *KafkaSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="d09ef-194">Erstellen und Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="d09ef-194">Build and test your application</span></span>

1. <span data-ttu-id="d09ef-195">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Ordnerverzeichnis, in dem sich die Datei *pom.xml* befindet. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-195">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\kafka`

   <span data-ttu-id="d09ef-196">Oder</span><span class="sxs-lookup"><span data-stu-id="d09ef-196">-or-</span></span>

   `cd /users/example/home/kafka`

1. <span data-ttu-id="d09ef-197">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-197">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="d09ef-198">Sobald Ihre Anwendung ausgeführt wird, können Sie sie mit *curl* testen. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d09ef-198">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="d09ef-199">In den Protokollen Ihrer Anwendung sollte „hello“ angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="d09ef-199">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="d09ef-200">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="d09ef-200">For example:</span></span>

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> <span data-ttu-id="d09ef-201">Sie können die Datei *KafkaSource.java* zu Testzwecken ändern, sodass sie wie im folgenden Beispiel gezeigt ein einfaches HTML-Formular enthält:</span><span class="sxs-lookup"><span data-stu-id="d09ef-201">For testing purposes, you could modify your *KafkaSource.java* so that it contains a simple HTML form like the following example:</span></span>
> 
> ```java
> package com.wingtiptoys.kafka;
>    
> import org.springframework.beans.factory.annotation.Autowired;
> import org.springframework.cloud.stream.annotation.EnableBinding;
> import org.springframework.cloud.stream.messaging.Source;
> import org.springframework.messaging.support.GenericMessage;
> import org.springframework.web.bind.annotation.GetMapping;
> import org.springframework.web.bind.annotation.PostMapping;
> import org.springframework.web.bind.annotation.RequestBody;
> import org.springframework.web.bind.annotation.RequestParam;
> import org.springframework.web.bind.annotation.RestController;
> 
> @EnableBinding(Source.class)
> @RestController
> public class KafkaSource {
>   @Autowired
>   private Source source;
> 
>   @GetMapping("/")
>   public String sendForm() {
>     return "<html><body>" +
>       "<form action=\"/messages\" method=\"post\">" +
>       "<input type=\"text\" name=\"text\">" +
>       "<input type=\"submit\">" +
>       "</form></body><html>";
>     }
> 
>   @PostMapping("/messages")
>   public String sendMessage(@RequestBody String message) {
>     this.source.output().send(new GenericMessage<>(message));
>     return message;
>   }
> }
> ```
> 
> <span data-ttu-id="d09ef-202">Dies ermöglicht es Ihnen, einen Webbrowser zum Testen der Anwendung zu verwenden:</span><span class="sxs-lookup"><span data-stu-id="d09ef-202">This will allow you to use a web browser to test your application:</span></span>
> 
> ![Testen der Anwendung mithilfe eines Webbrowsers][TB01]
> 
> <span data-ttu-id="d09ef-204">Wenn Sie das Formular senden, zeigt die Anwendung die Ergebnisse an:</span><span class="sxs-lookup"><span data-stu-id="d09ef-204">When you submit the form, your application will display the results:</span></span>
> 
> ![Antwort der Anwendung in einem Webbrowser][TB02]
> 

## <a name="next-steps"></a><span data-ttu-id="d09ef-206">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="d09ef-206">Next steps</span></span>

<span data-ttu-id="d09ef-207">Weitere Informationen zur Azure-Unterstützung für Event Hub Stream Binder und Apache Kafka finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="d09ef-207">For more information about Azure support for Event Hub Stream Binder and Apache Kafka, see the following articles:</span></span>

* [<span data-ttu-id="d09ef-208">Was ist Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="d09ef-208">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="d09ef-209">Azure Event Hubs für Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="d09ef-209">Azure Event Hubs for Apache Kafka</span></span>](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [<span data-ttu-id="d09ef-210">Erstellen eines Event Hubs-Namespaces und eines Event Hubs mithilfe des Azure-Portals</span><span class="sxs-lookup"><span data-stu-id="d09ef-210">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="d09ef-211">Erstellen von Apache Kafka-fähigen Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d09ef-211">Create Apache Kafka enabled event hubs</span></span>](/azure/event-hubs/event-hubs-create-kafka-enabled)

<span data-ttu-id="d09ef-212">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter „Azure für Java-Entwickler“ und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d09ef-212">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="d09ef-213">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="d09ef-213">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="d09ef-214">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="d09ef-214">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="d09ef-215">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="d09ef-215">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="d09ef-216">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="d09ef-216">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
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

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-03.png

[TB01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-01.png
[TB02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-02.png
