---
title: "Verwenden von Spring Boot Starter für Azure Storage"
description: Hier erfahren Sie, wie Sie eine Spring Boot Initializer-App mit Azure Storage Starter konfigurieren.
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: yungez;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 50c8475c66250c8e872849007349277fd3fe797b
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a>Verwenden von Spring Boot Starter für Azure Storage

## <a name="overview"></a>Übersicht

In diesem Artikel erfahren Sie Schritt für Schritt, wie Sie eine benutzerdefinierte Anwendung unter Verwendung von **Spring Initializr** erstellen und mit dieser Anwendung anschließend auf Azure Storage zugreifen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) anwenden oder sich für ein [kostenloses Azure-Konto](https://azure.microsoft.com/pricing/free-trial/) registrieren.
* Die [Azure-Befehlszeilenschnittstelle (CLI)](http://docs.microsoft.com/cli/azure/overview)
* Ein aktuelles [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) (ab Version 1.7)
* [Maven](http://maven.apache.org/) von Apache (ab Version 3.0)

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Erstellen einer benutzerdefinierten Anwendung mit dem Spring Initializr

1. Navigieren Sie zu <https://start.spring.io/>.

1. Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.

   ![Grundlegende Spring Initializr-Optionen](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt**. Beispiel: *com.contoso.wingtiptoysdemo*.
   >

1. Scrollen Sie nach unten zum Abschnitt **Azure**, und aktivieren Sie das Kontrollkästchen für **Azure Storage**.

   ![Vollständige Spring Initializr-Optionen](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. Klicken Sie am unteren Seitenrand auf die Schaltfläche **Projekt generieren**.

   ![Vollständige Spring Initializr-Optionen](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.

   ![Herunterladen eines benutzerdefinierten Spring Boot-Projekts](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a>Anmelden bei Azure und Auswählen des zu verwendenden Abonnements

1. Öffnen Sie eine Eingabeaufforderung.

1. Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:

   ```azurecli
   az login
   ```
   Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.

1. Listen Sie Ihre Abonnements auf:

   ```azurecli
   az account list
   ```
   Azure gibt eine Liste mit Ihren Abonnements zurück. Kopieren Sie die GUID für das Abonnement, das Sie verwenden möchten. Beispiel:

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

1. Specify the GUID for the account you want to use with Azure; for example:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a>Erstellen eines Azure-Speicherkontos

1. Erstellen Sie eine Ressourcengruppe für die in diesem Artikel verwendeten Azure-Ressourcen. Beispiel:
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `name` | Gibt einen eindeutigen Namen für Ihre Ressourcengruppe an. |
   | `location` | Gibt die [Azure-Region](https://azure.microsoft.com/regions/) an, in der Ihre Ressourcengruppe gehostet wird. |

   Die Azure CLI zeigt die Ergebnisse der Erstellung Ihrer Ressourcengruppe an, Beispiel:  

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

1. Erstellen Sie in der Ressourcengruppe für Ihre Spring Boot-App ein Azure-Speicherkonto. Beispiel:
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `name` | Gibt einen eindeutigen Namen für Ihr Speicherkonto an. |
   | `resource-group` | Gibt den Namen der Ressourcengruppe an, die Sie im vorherigen Schritt erstellt haben. |
   | `location` | Gibt die [Azure-Region](https://azure.microsoft.com/regions/) an, in der Ihr Speicherkonto gehostet wird. |
   | `sku` | Gibt eine der folgenden Optionen an: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`. |

   Azure gibt eine lange JSON-Zeichenfolge mit dem Bereitstellungszustand zurück. Beispiel: |
   
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

1. Rufen Sie die Verbindungszeichenfolge für Ihr Speicherkonto ab. Beispiel:
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   | ---|---|
   | `name` | Gibt einen eindeutigen Namen des Speicherkontos an, das Sie in den vorherigen Schritten erstellt haben. |
   | `resource-group` | Gibt den Namen der Ressourcengruppe an, die Sie in den vorherigen Schritten erstellt haben. |

   Azure gibt eine JSON-Zeichenfolge mit der Verbindungszeichenfolge für Ihr Speicherkonto zurück. Beispiel:

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a>Konfigurieren und Kompilieren Ihrer Spring Boot-Anwendung

1. Extrahieren Sie die Dateien aus dem heruntergeladenen Projektarchiv in ein Verzeichnis.

1. Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.

1. Fügen Sie den Schlüssel für Ihr Speicherkonto hinzu. Beispiel:
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. Navigieren Sie in Ihrem Projekt zum Ordner */src/main/java/com/example/wingtiptoysdemo*, und öffnen Sie die Datei *WingtiptoysdemoApplication.java* in einem Text-Editor.

1. Ersetzen Sie den vorhandenen Java-Code durch das folgende Beispiel zum Auflisten der Blobs in einem Container:

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
   > Im obigen Beispiel werden die Speicherkontoeinstellungen, die Sie in der Datei *application.properties* definiert haben, per Autowiring verwendet.
   >

1. Kompilieren Sie die Anwendung, und führen Sie sie aus:
   ```shell
   mvn clean package spring-boot:run
   ```
   
   Die Anwendung erstellt einen Container und lädt eine Textdatei als Blob in den Container hoch. Das Blob wird dann unter Ihrem Speicherkonto im [Azure-Portal](https://portal.azure.com) aufgelistet.

   ![Auflisten von Blobs im Azure-Portal](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > Beim Kompilieren Ihrer Anwendung wird unter Umständen die folgende Fehlermeldung angezeigt:
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
   > In diesem Fall empfiehlt es sich möglicherweise, das Maven Surefire-Testen zu deaktivieren. Fügen Sie hierzu der Datei *pom.xml* den folgenden Plug-In-Eintrag hinzu:
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

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu weiteren verfügbaren Spring Boot Starter-Optionen für Microsoft Azure finden Sie unter [Spring Boot Starter für Azure](spring-boot-starters-for-azure.md).

Weitere Informationen zum Integrieren von Azure-Funktionen in Spring-basierte Anwendungen finden Sie unter [Spring Framework in Azure](/java/azure/spring-framework/).

Ausführliche Informationen zu weiteren Azure Storage-APIs, die Sie über Ihre Spring Boot-Anwendungen aufrufen können, finden Sie in den folgenden Artikeln:
* [Verwenden des Blob-Speichers mit Java](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [Verwenden des Warteschlangenspeichers mit Java](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [Verwenden von Azure Table Storage mit Java](/azure/cosmos-db/table-storage-how-to-use-java)
* [Entwickeln für Azure Files mit Java](/azure/storage/files/storage-java-how-to-use-file-storage)
