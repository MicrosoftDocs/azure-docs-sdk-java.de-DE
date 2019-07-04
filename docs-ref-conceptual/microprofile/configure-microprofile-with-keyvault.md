---
title: Konfigurieren von MicroProfile über Azure Key Vault
description: Hier erfahren Sie, wie Sie Geheimnisse in einen MicroProfile-Webdienst einfügen, indem Sie Azure Key Vault verwenden.
services: key-vault
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: c405711813176823f2ddee6b4002f75c2b25fdb5
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533612"
---
# <a name="configure-microprofile-by-using-azure-key-vault"></a><span data-ttu-id="45ff7-103">Konfigurieren von MicroProfile über Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="45ff7-103">Configure MicroProfile by using Azure Key Vault</span></span>

<span data-ttu-id="45ff7-104">In diesem Artikel wird veranschaulicht, wie eine [MicroProfile](http://microprofile.io)-Anwendung zu konfigurieren ist, um Geheimnisse aus einer [Azure Key Vault-Instanz](https://azure.microsoft.com/services/key-vault/) (Azure-Schlüsseltresor) abzurufen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-104">This article demonstrates how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from an [Azure key vault](https://azure.microsoft.com/services/key-vault/).</span></span> <span data-ttu-id="45ff7-105">In diesem Prozess verwenden Sie die [MicroProfile Config-APIs](https://microprofile.io/project/eclipse/microprofile-config), um eine direkte Verbindung mit einem Azure-Schlüsseltresor herzuerstellen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-105">In this process, you use the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to an Azure key vault.</span></span> <span data-ttu-id="45ff7-106">Als Entwickler profitieren Sie, wenn Sie die MicroProfile Config-APIs verwenden, von einer Standard-API zum Abrufen und Einfügen von Konfigurationsdaten für ihre Microservices.</span><span class="sxs-lookup"><span data-stu-id="45ff7-106">As a developer, by using the MicroProfile Config APIs, you benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="45ff7-107">Bevor Sie beginnen, sollten Sie sich kurz ansehen, was Sie in Ihrem Code schreiben können, wenn Sie Azure Key Vault und die MicroProfile Config-API kombinieren.</span><span class="sxs-lookup"><span data-stu-id="45ff7-107">Before you start, take a quick look at what a combination of Azure Key Vault and the MicroProfile Config API enables you to write in your code.</span></span> <span data-ttu-id="45ff7-108">Der folgende Codeausschnitt gehört zu einem Feld in einer Klasse, die die Annotationen `@Inject` und `@ConfigProperty` hat.</span><span class="sxs-lookup"><span data-stu-id="45ff7-108">The following code snippet is of a field in a class that's annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="45ff7-109">Der in der Annotation angegebene Name (*name*) ist der Name der Eigenschaft, nach dem in Ihrem Schlüsseltresor gesucht werden soll, und *defaultValue* ist der Wert, auf den der Name festgelegt wird, wenn der Schlüssel nicht festgestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="45ff7-109">The *name* that's specified in the annotation is the name of the property to look up in your key vault, and the *defaultValue* is what will be set if the key is not discovered.</span></span> <span data-ttu-id="45ff7-110">Das Ergebnis ist, dass der im Schlüsseltresor gespeicherte Wert oder der Standardwert zur Laufzeit automatisch in das Feld eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="45ff7-110">The result is that the value that's stored in the key vault, or the default value, is injected automatically into the field at runtime.</span></span> <span data-ttu-id="45ff7-111">Diese Vorgehensweise kann Ihnen das Programmieren vereinfachen, weil Sie keine Werte mehr in Konstruktoren und Setter-Methoden übergeben müssen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-111">This action can simplify your life, because you no longer need to pass values around in constructors and setter methods.</span></span> <span data-ttu-id="45ff7-112">Stattdessen erledigt MicroProfile diese Aufgabe.</span><span class="sxs-lookup"><span data-stu-id="45ff7-112">Instead, MicroProfile handles this task.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="45ff7-113">Um Geheimnisse nach Bedarf anzufordern, können Sie auch direkt auf die MicroProfile-Konfiguration zugreifen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-113">To request secrets, as necessary, you can also access the MicroProfile config directly.</span></span> <span data-ttu-id="45ff7-114">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="45ff7-114">For example:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="45ff7-115">In diesem Beispiel werden [Payara Micro](https://www.payara.fish/payara_micro) und [MicroProfile](https://microprofile.io/) verwendet, um eine kleine Java-WAR-Datei (Web Application Requirement) zu erstellen, die Sie lokal auf Ihrem Computer ausführen können.</span><span class="sxs-lookup"><span data-stu-id="45ff7-115">This sample code uses [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java web application requirement (WAR) file that you can run locally on your machine.</span></span> <span data-ttu-id="45ff7-116">Im Beispiel wird nicht gezeigt, wie der Code in Docker verpackt oder an Azure gepusht wird, aber am Ende dieses Artikels finden Sie Links zu weiteren nützlichen Tutorials, in denen dieser Punkt erläutert wird.</span><span class="sxs-lookup"><span data-stu-id="45ff7-116">It doesn't demonstrate how to Dockerize or push the code to Azure, but the section at the end of this article has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="45ff7-117">In diesem Beispiel wird eine kostenlose Open-Source-Bibliothek verwendet, über die (mit der MicroProfile Config-API) eine Konfigurationsquelle in Ihrem Schlüsseltresor erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="45ff7-117">The sample uses a free and open source library that creates a config source (using the MicroProfile Config API) in your key vault.</span></span> <span data-ttu-id="45ff7-118">Wenn Sie weitere Informationen zu dieser Bibliothek wünschen und sich den Code ansehen möchten, lesen Sie die [GitHub-Projektseite](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="45ff7-118">To learn more about this library and review the code, see the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="45ff7-119">Wenn Sie die Bibliothek verwenden, lässt sich mit dem Code in diesem Tutorial der Fokus einfach auf die Konfiguration der Bibliothek legen, und Sie können dann Schlüssel in Ihren Code einfügen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-119">If you use the library, the code in this tutorial can simply focus on the configuration of the library and then inject keys into your code.</span></span> <span data-ttu-id="45ff7-120">Sie müssen keinen Azure-spezifischen Code schreiben.</span><span class="sxs-lookup"><span data-stu-id="45ff7-120">You don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="45ff7-121">Um diesen Code auf Ihrem lokalen Computer auszuführen, wobei Sie mit dem Erstellen einer Schlüsseltresorressource beginnen, gehen Sie entsprechend den Anweisungen in den nächsten Abschnitten vor.</span><span class="sxs-lookup"><span data-stu-id="45ff7-121">To run this code on your local machine, starting with creating a key vault resource, follow the instructions in the next sections.</span></span>

## <a name="create-a-key-vault-resource"></a><span data-ttu-id="45ff7-122">Erstellen einer Schlüsseltresorressource</span><span class="sxs-lookup"><span data-stu-id="45ff7-122">Create a key vault resource</span></span>

<span data-ttu-id="45ff7-123">In diesem Abschnitt verwenden Sie die Azure-Befehlszeilenschnittstelle, um eine Schlüsseltresorressource zu erstellen und diese mit einem Geheimnis zu füllen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-123">In this section, you use the Azure CLI to create a key vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="45ff7-124">Erstellen Sie einen Azure-Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="45ff7-124">Create an Azure service principal.</span></span> <span data-ttu-id="45ff7-125">In diesem Schritt erhalten Sie die Client-ID und den Schlüssel, die Sie benötigen, um auf Ihren Schlüsseltresor zugreifen zu können:</span><span class="sxs-lookup"><span data-stu-id="45ff7-125">This step gives you the client ID and key that you need to access your key vault:</span></span>

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    <span data-ttu-id="45ff7-126">Es soll *microprofile-keyvault-service-principal* verwendet werden, um *\<service_principal_name>* in diesem Schritt zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-126">Let's use *microprofile-keyvault-service-principal* to replace *\<service_principal_name>* in the preceding step.</span></span> <span data-ttu-id="45ff7-127">Die Antwort von Azure sieht so aus wie die folgende Antwort:</span><span class="sxs-lookup"><span data-stu-id="45ff7-127">The response from Azure would be similar to the following:</span></span>

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    <span data-ttu-id="45ff7-128">Von besonderer Bedeutung sind hier die Werte von *appId* und *password*.</span><span class="sxs-lookup"><span data-stu-id="45ff7-128">Of particular note here are the *appId* and *password* values.</span></span> <span data-ttu-id="45ff7-129">Sie benötigen diese Werte später in diesem Artikel als Client-ID (*client ID*) und Schlüssel (*key*).</span><span class="sxs-lookup"><span data-stu-id="45ff7-129">You'll use them later in this article as *client ID* and *key*.</span></span>

1. <span data-ttu-id="45ff7-130">(Optional) Nachdem Sie einen Dienst Dienstprinzipal erstellt haben, können Sie eine Ressourcengruppe erstellen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-130">(Optional) Now that you've created a service principal, you can create a resource group.</span></span> <span data-ttu-id="45ff7-131">Wenn Sie bereits eine Ressourcengruppe haben, die Sie verwenden möchten, können Sie diesen Schritt überspringen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-131">If you already have a resource group that you want to use, you can skip this step.</span></span> <span data-ttu-id="45ff7-132">Um eine Liste mit Ressourcengruppenstandorten abzurufen, können Sie `az account list-locations` aufrufen. Anschließend können Sie den *name*-Wert aus dieser Liste verwenden, um anzugeben, wo die Ressourcengruppe erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="45ff7-132">To get a list of resource group locations, you can call `az account list-locations` and use the *name* value from that list to specify where the resource group should be created.</span></span>

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. <span data-ttu-id="45ff7-133">Erstellen Sie eine Schlüsseltresorressource.</span><span class="sxs-lookup"><span data-stu-id="45ff7-133">Create a key vault resource.</span></span> <span data-ttu-id="45ff7-134">Sie verwenden Ihren Schlüsseltresornamen, um später auf den Schlüsseltresor zu verweisen. Daher sollten Sie einen einprägsamen Namen wählen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-134">You'll use your key vault name to refer to the key vault later, so be sure to choose a memorable name.</span></span>

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. <span data-ttu-id="45ff7-135">Weisen Sie dem zuvor von Ihnen erstellten Dienstprinzipal die erforderlichen Berechtigungen zu, damit er auf die Schlüsseltresorgeheimnisse zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="45ff7-135">Grant the appropriate permissions to the service principal that you created earlier, so that it can access the key vault secrets.</span></span> <span data-ttu-id="45ff7-136">Der appId-Wert im folgenden Code ist der *appId*-Wert aus Schritt 1, in dem Sie den Dienstprinzipal erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="45ff7-136">The appId value in the following code is the *appId* value from step 1, where you created the service principal.</span></span> <span data-ttu-id="45ff7-137">Das heißt, der *appId*-Wert in Schritt 1 war *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, Sie müssen aber den Wert aus Ihren eigenen Terminalausgabe verwenden.</span><span class="sxs-lookup"><span data-stu-id="45ff7-137">That is, the *appId* in step 1 was *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, but you should use the value from your own terminal output.</span></span>

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. <span data-ttu-id="45ff7-138">Jetzt können Sie ein Geheimnis in Ihren Schlüsseltresor schreiben.</span><span class="sxs-lookup"><span data-stu-id="45ff7-138">Now you can push a secret into your key vault.</span></span> <span data-ttu-id="45ff7-139">Verwenden Sie den Schlüsselnamen *demo-key*, und legen den Wert des Schlüssels auf *demo-value* fest:</span><span class="sxs-lookup"><span data-stu-id="45ff7-139">Use the key name *demo-key*, and set the value of the key to *demo-value*:</span></span>

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

<span data-ttu-id="45ff7-140">Das ist alles!</span><span class="sxs-lookup"><span data-stu-id="45ff7-140">That's it!</span></span> <span data-ttu-id="45ff7-141">Sie haben nun einen Schlüsseltresor, der in Azure ausgeführt wird und ein Geheimnis enthält.</span><span class="sxs-lookup"><span data-stu-id="45ff7-141">You now have a key vault running in Azure with a single secret.</span></span> <span data-ttu-id="45ff7-142">Sie können dieses Repository jetzt klonen und so konfigurieren, dass es diese Ressource in Ihrer App verwendet.</span><span class="sxs-lookup"><span data-stu-id="45ff7-142">You can now clone this repo and configure it to use this resource in your app.</span></span>

## <a name="get-up-and-running-locally"></a><span data-ttu-id="45ff7-143">Einrichten und Ausführen in der lokalen Umgebung</span><span class="sxs-lookup"><span data-stu-id="45ff7-143">Get up and running locally</span></span>

<span data-ttu-id="45ff7-144">Dieses Beispiel basiert auf einer auf GitHub verfügbaren Beispielanwendung. Daher klonen Sie diese Anwendung, und durchlaufen Sie den Code Schritt für Schritt.</span><span class="sxs-lookup"><span data-stu-id="45ff7-144">This example is based on a sample application that's available on GitHub, so you'll clone that application and then step through the code.</span></span> 

1. <span data-ttu-id="45ff7-145">Klonen Sie den Code auf Ihrem Computer, indem Sie die folgenden Befehle eingeben:</span><span class="sxs-lookup"><span data-stu-id="45ff7-145">Clone the code onto your machine by entering the following commands:</span></span>

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="45ff7-146">Wechseln Sie zu *src/main/resources/META-INF/microprofile-config.properties*, und ändern Sie dann die Eigenschaften in der Datei *microprofile-config.properties*, indem Sie die Werte aus den vorherigen Schritten verwenden.</span><span class="sxs-lookup"><span data-stu-id="45ff7-146">Go to *src/main/resources/META-INF/microprofile-config.properties*, and then change the properties in the *microprofile-config.properties* file by using the values from the previous steps.</span></span>

1. <span data-ttu-id="45ff7-147">Führen Sie den Server durch Verwenden von `mvn clean package payara-micro:start` aus.</span><span class="sxs-lookup"><span data-stu-id="45ff7-147">Try running the server by using `mvn clean package payara-micro:start`.</span></span>

1. <span data-ttu-id="45ff7-148">Greifen Sie aus Ihrem Webbrowser auf [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) zu.</span><span class="sxs-lookup"><span data-stu-id="45ff7-148">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser.</span></span> <span data-ttu-id="45ff7-149">Daraufhin sollte eine einfache Antwort angezeigt werden, in der die Werte enthalten sind, die aus Ihrem Schlüsseltresor gelesen werden.</span><span class="sxs-lookup"><span data-stu-id="45ff7-149">You should see a simple response that demonstrates values that are being read from your key vault.</span></span>

## <a name="summary"></a><span data-ttu-id="45ff7-150">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="45ff7-150">Summary</span></span>

<span data-ttu-id="45ff7-151">In dieser Beispielanwendung sind die MicroProfile Config-API, Azure Key Vault und die kostenlose Open-Source-Bibliothek [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) kombiniert, um einfaches Einfügen von Konfigurationsdaten und Geheimnissen in Ihre MicroProfile-Webdienste zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="45ff7-151">This sample application combines the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into your MicroProfile web services.</span></span>
