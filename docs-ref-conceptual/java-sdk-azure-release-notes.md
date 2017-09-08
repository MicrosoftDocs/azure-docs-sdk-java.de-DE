---
title: "Versionshinweise zu Azure-Verwaltungsbibliotheken für Java | Microsoft-Dokumentation"
description: "Informieren Sie sich über Neuigkeiten und wichtige Änderungen in den Azure-Verwaltungsbibliotheken für Java."
keywords: Azure, Java, API, Referenz, Hinweise, Updates, veraltet
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: fc246d499b2f5f20a7efbaed16c4b4193d8d8e6c
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="release-notes"></a>Versionsinformationen 

## <a name="june-30-2017---110"></a>30. Juni 2017: 1.1.0 

V1.1 ist in den für die öffentliche Verwendung vorgesehenen APIs, die in V1.0 die (stabile) Phase der allgemeinen Verfügbarkeit erreicht haben, abwärtskompatibel mit V1.0.

Für APIs, die in V.0 mit der Anmerkung @Beta markiert waren, wurden einige wichtige Änderungen eingeführt.

Wenn Sie Ihren Code zu 1.1.0 migrieren möchten, können Sie Ihren 1.0.0-Code anhand [dieser Hinweise](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) für 1.1.0 vorbereiten.

### <a name="generally-availabile-in-v11"></a>Allgemein verfügbar in V1.1

Einige der Beta-APIs aus V1.0 sind in V1.1 nun allgemein verfügbar. Hierzu zählen insbesondere folgende:

- Asynchrone Methoden
- Alle Methoden im CDN, die sich zuvor noch in der Betaphase befanden
- Alle Methoden und Schnittstellen in Anwendungsgateways, die sich zuvor noch in der Betaphase befanden

 Teile der Bibliothek befinden sich immer noch in der Vorschauphase. Die folgende Tabelle gibt Aufschluss über den aktuellen Status der Bibliotheken:

Dienst oder Feature | Allgemein verfügbar | Als Vorschauversion verfügbar  | In Kürze verfügbar |
---------|---------|---------|---------|
Compute  | Virtuelle Computer und VM-Erweiterungen, VM-Skalierungsgruppen, verwaltete Datenträger   | Azure Container Service, Azure Container Registry |    |
Speicher   |  Speicherkonten       |         |   Verschlüsselung      |
SQL-Datenbank  | Datenbanken, Firewalls, Pools für elastische Datenbanken        |         |   Weitere Features      |
Netzwerk    |  Virtuelle Netzwerke, Netzwerkschnittstellen, IP-Adressen, Routingtabellen, Netzwerksicherheitsgruppen, DNS, Traffic Manager, Anwendungsgateways  |    Load Balancer     |   VPN, Network Watcher   |
Weitere Dienste    |  Ressourcen-Manager, Key Vault, Redis, CDN, Batch       |  Web-Apps, Funkions-Apps, Service Bus, Graph RBAC, DocumentDB   | Überwachung, Planung, Funktionsverwaltung, Suche, weitere Graph RBAC-Features        |
Grundlagen     |   Authentifizierung: Core, asynchrone Methoden       |      |         |

### <a name="import-with-maven"></a>Importieren mit Maven

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>Hilfe und Feedback

Besuchen Sie die [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk)-Community, um Hilfe bei der Verwendung der Bibliotheken in Ihrem eigenen Code zu erhalten. Fehler oder Verbesserungsvorschläge für die Bibliotheken können über [GitHub](https://github.com/Azure/azure-sdk-for-java/issues) gemeldet bzw. eingereicht werden.

### <a name="migrate-from-previous-releases"></a>Migrieren von früheren Versionen

[Migrieren von 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [Migrieren von 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)


