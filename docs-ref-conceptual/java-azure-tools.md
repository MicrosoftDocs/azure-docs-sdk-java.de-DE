---
title: "Tools für Azure-Java-Entwickler | Microsoft-Dokumentation"
description: "IDE-Integrationen, Emulatoren, Ressourcen-Explorer und Befehlszeilenschnittstellen für Java-Entwickler, die in Azure arbeiten."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: ce0b003cc7c48c8690f4236547ddec36e6ea9d53
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2017
---
# <a name="azure-tools-for-java-developers"></a>Azure-Tools für Java-Entwickler

## <a name="client-and-management-libraries"></a>Client- und Verwaltungsbibliotheken

Mit den Azure-Bibliotheken für Java können Sie über Ihre Anwendungen eine Verbindung mit Diensten herstellen und Azure-Ressourcen verwalten. Fügen Sie Ihrer Projektdatei *pom.xml* die folgende Abhängigkeit hinzu, um die Verwaltungsbibliotheken in Ihre Maven-Projekte zu importieren:

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

Weitere Informationen finden Sie in der [vollständigen Bibliothekenliste](java-sdk-azure-install.md) und in den [ersten Schritten mit den Azure-Bibliotheken für Java](java-sdk-azure-get-started.md).

## <a name="eclipse-and-intellij-plugins"></a>Eclipse- und IntelliJ-Plug-Ins

Mit den Azure-Toolkits für [Eclipse](eclipse/azure-toolkit-for-eclipse.md) und [IntelliJ](intellij/azure-toolkit-for-intellij.md) können Sie Azure-Ressourcen verwalten und Apps aus Ihrer IDE bereitstellen.   

![IntelliJ-Toolkit mit dem Azure-Explorer](media/intelliJ-azure-explorer.png)

[Erste Schritte mit dem Azure-Toolkit für Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Erste Schritte mit dem Azure-Toolkit für IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app) 

## <a name="azure-cli-20"></a>Azure CLI 2.0

Die Azure CLI 2.0 bietet eine Befehlszeilenumgebung für die Verwaltung von Azure-Ressourcen. Sie können sie in Ihrem Browser mit [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) verwenden oder unter macOS, Linux und Windows [installieren](https://docs.microsoft.com/cli/azure/install-azure-cli) und über die Befehlszeile ausführen.

[Erste Schritte mit der Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)

## <a name="azure-storage-explorer"></a>Azure-Speicher-Explorer 

Verwalten Sie Azure-Speicherkonten, Container und Blobs/Dateien von Ihrem Desktop aus. Der Azure-Speicher-Explorer ist derzeit als Vorschauversion für Windows, macOS und Linux verfügbar.

[Erste Schritte mit dem Speicher-Explorer (Vorschau)](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)