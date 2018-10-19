---
title: Partner Center Java SDK
description: Referenzdokumentation für das Partner Center-Java-SDK
keywords: API, CSP, Cloud Solution Provider, Java, Partner Center, SDK
author: iswillia
ms.author: iswillia
manager: lesliep
ms.date: 10/09/2018
ms.topic: reference
ms.prod: partnercenter
ms.technology: partnercenter
ms.devlang: java
ms.openlocfilehash: 2adfbdbd37d6eb91e48ee37091f951b3f7d59eb9
ms.sourcegitcommit: 4da7d2f470331feb7d76a1658f5825f365cdba9a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121643"
---
# <a name="partner-center-libraries-for-java"></a><span data-ttu-id="19788-104">Partner Center-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="19788-104">Partner Center libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="19788-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="19788-105">Overview</span></span>

<span data-ttu-id="19788-106">Die Partner Center-Bibliotheken für Java sind ein SDK, welches die Interaktion mit dem Partner Center-Dienst von Microsoft ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="19788-106">The Partner Center libraries for Java is a SDK that provides the ability to interact with Microsoft's Partner Center service.</span></span> <span data-ttu-id="19788-107">Mithilfe des SDK können Partner die Partner Center-Vorgänge programmgesteuert ausführen.</span><span class="sxs-lookup"><span data-stu-id="19788-107">This enables partners to perform the Partner Center operations programmatically.</span></span> <span data-ttu-id="19788-108">Dieses SDK ist die neueste Ergänzung für das vorhandene Portfolio von REST-APIs und das .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="19788-108">This is the latest addition to existing portfolio of REST APIs and the .NET SDK.</span></span>

## <a name="client-library"></a><span data-ttu-id="19788-109">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="19788-109">Client library</span></span>

<span data-ttu-id="19788-110">Verwalten Sie Ressourcen im Partner Center mithilfe der Clientbibliothek.</span><span class="sxs-lookup"><span data-stu-id="19788-110">Manage resources in Partner Center using the client library.</span></span>

<span data-ttu-id="19788-111">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="19788-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="19788-112">Beispiel</span><span class="sxs-lookup"><span data-stu-id="19788-112">Example</span></span>

<span data-ttu-id="19788-113">Ruft eine vollständige Liste der Kunden ab, die dem authentifizierten Handelspartner zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="19788-113">Retrieves a complete list of customer associated with the authenticated reseller.</span></span>

```java
IPartnerCredentials appCredentials = PartnerCredentials.getInstance().generateByApplicationCredentials('YOUR_APP_ID', 'YOUR_APP_SECRET', 'YOUR_TENANT_ID');
IAggregatePartner partnerOperations = PartnerService.getInstance().createPartnerOperations(appCredentials);

// Query the customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(100));
this.getContext().getConsoleHelper().stopProgress();

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while ( customersEnumerator.hasValue() )
{
    /*
     * Perform some operation with the current page of customers using 
     * customersEnumerator.getCurrent()  
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="samples"></a><span data-ttu-id="19788-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="19788-114">Samples</span></span>

<span data-ttu-id="19788-115">[Unterstützte Szenarien](https://docs.microsoft.com/partner-center/develop/scenarios)
[Beispiel für Konsolenanwendung](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="19788-115">[Supported scenarios](https://docs.microsoft.com/partner-center/develop/scenarios)
[Sample console application](https://github.com/Microsoft/Partner-Center-Java-Samples)</span></span>  