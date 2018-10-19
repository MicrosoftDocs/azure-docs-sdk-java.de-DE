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
# <a name="partner-center-libraries-for-java"></a>Partner Center-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Die Partner Center-Bibliotheken für Java sind ein SDK, welches die Interaktion mit dem Partner Center-Dienst von Microsoft ermöglicht. Mithilfe des SDK können Partner die Partner Center-Vorgänge programmgesteuert ausführen. Dieses SDK ist die neueste Ergänzung für das vorhandene Portfolio von REST-APIs und das .NET SDK.

## <a name="client-library"></a>Clientbibliothek

Verwalten Sie Ressourcen im Partner Center mithilfe der Clientbibliothek.

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Ruft eine vollständige Liste der Kunden ab, die dem authentifizierten Handelspartner zugeordnet sind.

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

## <a name="samples"></a>Beispiele

[Unterstützte Szenarien](https://docs.microsoft.com/partner-center/develop/scenarios)
[Beispiel für Konsolenanwendung](https://github.com/Microsoft/Partner-Center-Java-Samples)  