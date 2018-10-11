---
title: Versionshinweise zu Azure-Verwaltungsbibliotheken für Java | Microsoft-Dokumentation
description: Informieren Sie sich über Neuigkeiten und wichtige Änderungen in den Azure-Verwaltungsbibliotheken für Java.
keywords: Azure, Java, API, Referenz, Hinweise, Updates, veraltet
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 0aaa83ceb42192441decb5972baae56fed337fb2
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899080"
---
# <a name="release-notes"></a>Versionsinformationen 

## <a name="october-5-2017---130"></a>5. Oktober 2017 – 1.3.0 

Version 1.3.0 ist abwärtskompatibel mit vorherigen Versionen zur Verwendung von Diensten und Features, die in vorherigen Releases die (stabile) Phase der allgemeinen Verfügbarkeit erreicht haben.

Für diese Dienste sind wichtige Änderungen aus Vorschauversionen mit der Anmerkung @Beta versehen.

Wenn Sie Ihren Code zu 1.3.0 migrieren möchten, können Sie Ihren vorhandenen Code anhand [dieser Hinweise](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) für die Version 1.3 vorbereiten.

### <a name="generally-availabile-in-v13"></a>Allgemein verfügbar in V1.3

Einige der Beta-APIs aus vorherigen Releases sind nun allgemein verfügbar. Hierzu zählen insbesondere folgende:

- Asynchrone Methoden
- Alle Methoden im CDN, die sich zuvor noch in der Betaphase befanden
- Alle Methoden und Schnittstellen in Anwendungsgateways, die sich zuvor noch in der Betaphase befanden

  Teile der Bibliothek befinden sich immer noch in der Vorschauphase. Die folgende Tabelle gibt Aufschluss über den aktuellen Status der Bibliotheken:

Dienst oder Feature | Allgemein verfügbar | Als Vorschauversion verfügbar 
---------|---------|---------|-
Compute  | Virtuelle Computer und VM-Erweiterungen, VM-Skalierungsgruppen, verwaltete Datenträger   | Azure Container Service, Azure Container Registry 
Speicher   |  Speicherkonten       |    Verschlüsselung     
SQL-Datenbank  | Datenbanken, Firewalls, Pools für elastische Datenbanken              
Netzwerk    |  Virtuelle Netzwerke, Netzwerkschnittstellen, IP-Adressen, Routingtabellen, Netzwerksicherheitsgruppen, DNS, Traffic Manager, Anwendungsgateways  |    Lastenausgleichsmodule, Netzwerkpeering, Gateway für virtuelle Netzwerke, Network Watcher 
Weitere Dienste    |  Ressourcen-Manager, Key Vault, Redis, CDN, Batch       |  Web-Apps, Funktions-Apps, Service Bus, Graph (rollenbasierte Zugriffssteuerung), Cosmos DB, Search  
Grundlagen     |   Authentifizierung: Core, asynchrone Methoden, verwaltete Dienstidentität      |      |

> Vorschaufeatures sind in Bibliotheken auf Klassen-, Schnittstellen- oder Methodenebene mit dem Hinweis `@Beta` gekennzeichnet. Bei diesen Funktionen sind Änderungen vorbehalten. Sie können in Zukunft auf beliebige Weise geändert (oder sogar entfernt) werden.

### <a name="import-with-maven"></a>Importieren mit Maven

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>Hilfe und Feedback

Besuchen Sie die [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk)-Community, um Hilfe bei der Verwendung der Bibliotheken in Ihrem eigenen Code zu erhalten. Fehler oder Verbesserungsvorschläge für die Bibliotheken können über [GitHub](https://github.com/Azure/azure-sdk-for-java/issues) gemeldet bzw. eingereicht werden.


