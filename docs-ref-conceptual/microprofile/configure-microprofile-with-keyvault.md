---
title: Konfigurieren von MicroProfile mit Azure Key Vault
description: Hier erfahren Sie, wie Sie Geheimnisse in einen MicroProfile-Webdienst mit Azure Key Vault einfügen.
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
ms.openlocfilehash: fa93788f9b600d963f35ea599a58d309d3a3ee52
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240823"
---
# <a name="configure-microprofile-with-azure-key-vault"></a><span data-ttu-id="4861e-103">Konfigurieren von MicroProfile mit Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4861e-103">Configure MicroProfile with Azure Key Vault</span></span>

<span data-ttu-id="4861e-104">Dieses Tutorial zeigt, wie Sie eine [MicroProfile](http://microprofile.io)-Anwendung für den Abruf von Geheimnissen aus [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) konfigurieren und dabei die [MicroProfile-Konfigurations-APIs](https://microprofile.io/project/eclipse/microprofile-config) verwenden, um eine direkte Verbindung mit Azure Key Vault herzustellen.</span><span class="sxs-lookup"><span data-stu-id="4861e-104">This tutorial will demonstrate how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) using the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to Azure Key Vault.</span></span> <span data-ttu-id="4861e-105">Die MicroProfile-Konfigurations-APIs bieten Entwicklern eine Standard-API zum Abrufen und Einfügen von Konfigurationsdaten für ihre Microservices.</span><span class="sxs-lookup"><span data-stu-id="4861e-105">By using the MicroProfile Config APIs, developers benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="4861e-106">Bevor wir in die Details gehen, sehen wir uns zunächst kurz an, was wir in unserem Code schreiben können, wenn wir Azure Key Vault und die MicroProfile-Konfigurations-API miteinander kombinieren.</span><span class="sxs-lookup"><span data-stu-id="4861e-106">Before we dive in, lets quickly take a look at what a combination of Azure Key Vault and the MicroProfile Config API enables us to write in our code.</span></span> <span data-ttu-id="4861e-107">Hier sehen Sie einen Codeausschnitt für ein Feld in einer Klasse mit den Anmerkungen `@Inject` und `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="4861e-107">Here's a code snippet of a field in a class that has been annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="4861e-108">Der in den Anmerkungen angegebene Name (`name`) ist der Name der Eigenschaft, die in Azure Key Vault gesucht werden soll, und `defaultValue` ist der Wert, der festgelegt wird, wenn der Schlüssel nicht ermittelt werden kann.</span><span class="sxs-lookup"><span data-stu-id="4861e-108">The `name` specified in the annotation is the name of the property to look up in Azure Key Vault, and the `defaultValue` is what will be set if the key is not discovered.</span></span> <span data-ttu-id="4861e-109">Dadurch wird zur Laufzeit entweder der in Azure Key Vault gespeicherte Wert oder der Standardwert automatisch in das Feld eingefügt. Entwickler müssen somit keine Werte mehr in Konstruktoren und Setter-Methoden übergeben, sondern können die Behandlung MicroProfile überlassen.</span><span class="sxs-lookup"><span data-stu-id="4861e-109">The end result is that the value stored in Azure Key Vault, or the default value, will be injected automatically into the field at runtime, simplifying the life of developers as they no longer need to pass values around in constuctors and setter methods, instead leaving it to MicroProfile to handle.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="4861e-110">Auf die MicroProfile-Konfiguration kann auch direkt zugegriffen werden, um Geheimnisse nach Bedarf anzufordern. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4861e-110">It is also possible to access the MicroProfile config directly, to request secrets as necessary, e.g.:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="4861e-111">In diesem Beispiel wird unter Verwendung von [Payara Micro](https://www.payara.fish/payara_micro) und [MicroProfile](https://microprofile.io/) eine kleine Java-WAR-Datei erstellt, die lokal auf Ihrem Computer ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="4861e-111">This sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java war file that can be run locally on your machine.</span></span> <span data-ttu-id="4861e-112">Es zeigt nicht, wie der Code in Docker verpackt oder an Azure gepusht wird. Am Ende dieses Tutorials befindet sich jedoch ein Abschnitt mit Links zu weiteren hilfreichen Tutorials, in denen dieser Punkt erläutert wird.</span><span class="sxs-lookup"><span data-stu-id="4861e-112">It does not demonstrate how to dockerise or push the code to Azure, but the links section at the end of this tutorial has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="4861e-113">In diesem Beispiel wird eine kostenlose Open-Source-Bibliothek verwendet, die (unter Verwendung der MicroProfile-Konfigurations-API) eine Konfigurationsquelle für Azure Key Vault erstellt.</span><span class="sxs-lookup"><span data-stu-id="4861e-113">This sample makes use of a free and open source library that creats a config source (using the MicroProfile Config API) for Azure Key Vault.</span></span> <span data-ttu-id="4861e-114">Weitere Informationen zu dieser Bibliothek sowie den Code finden Sie auf der [GitHub-Projektseite](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="4861e-114">You can learn more about this library, and review the code, on the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="4861e-115">Durch die Verwendung dieser Bibliothek können wir uns beim Code in diesem Tutorial einfach auf die Konfiguration der Bibliothek sowie auf das Einfügen von Schlüsseln in den Code konzentrieren und müssen keinerlei Azure-spezifischen Code schreiben.</span><span class="sxs-lookup"><span data-stu-id="4861e-115">By using this library, the code in this tutorial can simply focus on configuration of the library, followed by injecting keys into your code, and we don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="4861e-116">Im Anschluss erfahren Sie, wie Sie diesen Code auf Ihrem lokalen Computer ausführen. Dabei erstellen Sie zunächst eine Azure Key Vault-Ressource.</span><span class="sxs-lookup"><span data-stu-id="4861e-116">Here are the steps required to run this code on your local machine, starting with creating an Azure Key Vault resource.</span></span>

## <a name="creating-an-azure-key-vault-resource"></a><span data-ttu-id="4861e-117">Erstellen einer Azure Key Vault-Ressource</span><span class="sxs-lookup"><span data-stu-id="4861e-117">Creating an Azure Key Vault resource</span></span>

<span data-ttu-id="4861e-118">Wir verwenden die Azure-Befehlszeilenschnittstelle, um die Azure Key Vault-Ressource zu erstellen und mit einem einzelnen Geheimnis zu füllen.</span><span class="sxs-lookup"><span data-stu-id="4861e-118">We will use the Azure CLI to create the Azure Key Vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="4861e-119">Als Erstes erstellen wir einen Azure-Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="4861e-119">Firstly, lets create an Azure service principal.</span></span> <span data-ttu-id="4861e-120">Dadurch erhalten wir die Client-ID und den Schlüssel für den Zugriff auf Key Vault:</span><span class="sxs-lookup"><span data-stu-id="4861e-120">This will provide us with the client ID and key we need to access Key Vault:</span></span>

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

<span data-ttu-id="4861e-121">Angenommen, wir verwenden im vorherigen Schritt `microprofile-keyvault-service-principal` als Dienstprinzipalname.</span><span class="sxs-lookup"><span data-stu-id="4861e-121">Lets say we use `microprofile-keyvault-service-principal` for the service principal name in the previous step.</span></span> <span data-ttu-id="4861e-122">In diesem Fall sieht die (leicht verschleierte) Antwort von Azure wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="4861e-122">The response from Azure for doing this will be in the following, slightly censored, form:</span></span>

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

<span data-ttu-id="4861e-123">Von besonderem Interesse sind hier die Werte `appID` und `password`: Diese werden später für `client ID` und `key` benötigt.</span><span class="sxs-lookup"><span data-stu-id="4861e-123">Of particular note here is the `appID` and `password` values - these are what we will use later on as `client ID` and `key`, respectively.</span></span>

<span data-ttu-id="4861e-124">Nach der Erstellung des Dienstprinzipals können wir optional eine Ressourcengruppe erstellen. (Falls Sie bereits über eine Ressourcengruppe verfügen, die Sie verwenden möchten, können Sie diesen Schritt überspringen.)</span><span class="sxs-lookup"><span data-stu-id="4861e-124">Now that we have created a service principal, we can optionally create a resource group (if you already have one you want to use, you can skip this step).</span></span> <span data-ttu-id="4861e-125">Sie können eine Liste mit Ressourcengruppenstandorten abrufen. Rufen Sie hierzu `az account list-locations` auf, und verwenden Sie den Wert `name` aus dieser Liste, um anzugeben, wo die Ressourcengruppe erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="4861e-125">Note that to get a list of resource group locations, you can call `az account list-locations` and use the `name` value from that list to specify where the resource group should be created.</span></span>

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

<span data-ttu-id="4861e-126">Als Nächstes erstellen wir eine Azure Key Vault-Ressource.</span><span class="sxs-lookup"><span data-stu-id="4861e-126">We now create an Azure Key Vault resource.</span></span> <span data-ttu-id="4861e-127">Der Key Vault-Name sollte gut zu merken sein, da Sie später anhand dieses Namens auf den Schlüsseltresor verweisen.</span><span class="sxs-lookup"><span data-stu-id="4861e-127">Note that the Key Vault name is what you will use to reference the key vault later, so choose something memorable.</span></span>

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

<span data-ttu-id="4861e-128">Darüber hinaus müssen wir dem zuvor erstellten Dienstprinzipal die erforderlichen Berechtigungen für den Zugriff auf die Key Vault-Geheimnisse gewähren.</span><span class="sxs-lookup"><span data-stu-id="4861e-128">We also need to grant the appropriate permissions to the service principal we created earlier, so that it may access the Key Vault secrets.</span></span> <span data-ttu-id="4861e-129">Hinweis: Der appID-Wert ist der Wert `appId` aus der Dienstprinzipalerstellung von weiter oben (also `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79`; verwenden Sie aber den Wert aus Ihrer Terminalausgabe).</span><span class="sxs-lookup"><span data-stu-id="4861e-129">Note that the appID value is the `appId` value from above where we created the service principal (that is, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79` - but use the value from your terminal output).</span></span>

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

<span data-ttu-id="4861e-130">Als Nächstes können wir ein Geheimnis an Key Vault pushen.</span><span class="sxs-lookup"><span data-stu-id="4861e-130">We are now at the point where we can push a secret into Key Vault.</span></span> <span data-ttu-id="4861e-131">In diesem Beispiel verwenden wir den Schlüsselnamen `demo-key` und legen den Wert des Schlüssels auf `demo-value` fest:</span><span class="sxs-lookup"><span data-stu-id="4861e-131">Lets use the key name `demo-key`, and set the value of the key to be `demo-value`:</span></span>

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

<span data-ttu-id="4861e-132">Das ist alles!</span><span class="sxs-lookup"><span data-stu-id="4861e-132">That's it!</span></span> <span data-ttu-id="4861e-133">Key Vault wird nun mit einem einzelnen Geheimnis in Azure ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="4861e-133">We now have Key Vault running in Azure with a single secret.</span></span> <span data-ttu-id="4861e-134">Als Nächstes können wir dieses Repository klonen und für die Verwendung dieser Ressource in unserer App konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="4861e-134">We can now clone this repo and configure it to use this resource in our app.</span></span>

## <a name="getting-up-and-running-locally"></a><span data-ttu-id="4861e-135">Einrichten und Ausführen in der lokalen Umgebung</span><span class="sxs-lookup"><span data-stu-id="4861e-135">Getting up and running locally</span></span>

<span data-ttu-id="4861e-136">Dieses Beispiel basiert auf einer auf GitHub verfügbaren Beispielanwendung, deren Code wir hier klonen und Schritt für Schritt durchgehen.</span><span class="sxs-lookup"><span data-stu-id="4861e-136">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="4861e-137">Gehen Sie wie folgt vor, um den Code auf Ihrem Computer zu klonen:</span><span class="sxs-lookup"><span data-stu-id="4861e-137">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="4861e-138">Navigieren Sie zu `src/main/resources/META-INF/microprofile-config.properties`, und aktualisieren Sie die Eigenschaften in der Datei „microprofile-config.properties“ mit den obigen Details.</span><span class="sxs-lookup"><span data-stu-id="4861e-138">Navigate to `src/main/resources/META-INF/microprofile-config.properties` and change the properties in microprofile-config.properties file with details from above.</span></span>

1. <span data-ttu-id="4861e-139">Führen Sie den Server mit `mvn clean package payara-micro:start` aus.</span><span class="sxs-lookup"><span data-stu-id="4861e-139">Try running the server using `mvn clean package payara-micro:start`</span></span>

1. <span data-ttu-id="4861e-140">Greifen Sie in Ihrem Webbrowser auf [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) zu. Daraufhin sollte eine einfache Antwort angezeigt werden, die deutlich macht, dass Werte aus Azure Key Vault gelesen werden.</span><span class="sxs-lookup"><span data-stu-id="4861e-140">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser - you should see a simple response that demonstrates values being read from Azure Key Vault.</span></span>

## <a name="summary"></a><span data-ttu-id="4861e-141">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="4861e-141">Summary</span></span>

<span data-ttu-id="4861e-142">Diese Beispielanwendung kombiniert die MicroProfile-Konfigurations-API mit Azure Key Vault und der kostenlosen Open-Source-Bibliothek [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault), um das Einfügen von Konfigurationsdaten und Geheimnissen in MicroProfile-Webdienste zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="4861e-142">This sample application bakes together the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into our MicroProfile web services.</span></span>
