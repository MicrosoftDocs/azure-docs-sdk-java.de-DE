---
title: "Spring Boot Starter für Azure"
description: "In diesem Artikel werden die verschiedenen verfügbaren Spring Boot Starter-Optionen für Azure beschrieben."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm
ms.openlocfilehash: ba5829407d03d275784a3a458d88ea47ac8494b8
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
---
# <a name="spring-boot-starters-for-azure"></a>Spring Boot Starter für Azure

In diesem Artikel werden die verschiedenen Spring Boot Starter-Optionen für [Spring Initializr] beschrieben, die Java-Entwicklern Integrationsfeatures für die Arbeit mit Microsoft Azure bieten.

![Spring Boot Starter-Optionen für Azure][spring-boot-starters]

Für Azure stehen aktuell folgende Spring Boot Starter-Optionen zur Verfügung:

* **[Azure-Support](#azure-support)**

   Bietet Unterstützung für die automatische Konfiguration von Azure-Diensten wie Service Bus, Storage und Active Directory.

* **[Azure Active Directory](#azure-active-directory)**

   Bietet Integrationsunterstützung für Spring Security mit Azure Active Directory-Authentifizierung.

* **[Azure Key Vault](#azure-key-vault)**

   Bietet Spring-Wertanmerkungsunterstützung für die Integration von Azure Key Vault-Geheimnissen.

* **[Azure Storage](#azure-storage)**

   Bietet Spring Boot-Unterstützung für Azure Storage-Dienste.

<a name="azure-support"></a>
## <a name="azure-support"></a>Azure-Support

Diese Spring Boot Starter-Option bietet Unterstützung für die automatische Konfiguration von Azure-Diensten wie Service Bus, Storage, Active Directory, Cosmos DB und Key Vault.

Verwendungsbeispiele für die verschiedenen Azure-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:

* Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* Der Datei wird der folgende Abschnitt hinzugefügt:

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-active-directory"></a>
## <a name="azure-active-directory"></a>Azure Active Directory

Diese Spring Boot Starter-Option bietet Unterstützung für die automatische Konfiguration von Spring Security zur Integration von Azure Active Directory für die Authentifizierung.

Verwendungsbeispiele für die Azure Active Directory-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:

* Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* Der Datei wird der folgende Abschnitt hinzugefügt:

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-key-vault"></a>
## <a name="azure-key-vault"></a>Azure Key Vault

Diese Spring Boot Starter-Option bietet Spring-Wertanmerkungsunterstützung für die Integration von Azure Key Vault-Geheimnissen.

Verwendungsbeispiele für die Azure Key Vault-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:

* Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* Der Datei wird der folgende Abschnitt hinzugefügt:

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-storage"></a>
## <a name="azure-storage"></a>Azure Storage

Diese Spring Boot Starter-Option bietet Spring Boot-Integrationsunterstützung für Azure Storage-Dienste.

Verwendungsbeispiele für die Azure Storage-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:

* [Verwenden von Spring Boot Starter für Azure Storage](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:

* Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* Der Datei wird der folgende Abschnitt hinzugefügt:

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von [Spring Boot] in Azure finden Sie unter [Spring Framework in Azure].

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie im **Spring Initializr** unter https://start.spring.io/.

<!-- URL List -->

[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework in Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
