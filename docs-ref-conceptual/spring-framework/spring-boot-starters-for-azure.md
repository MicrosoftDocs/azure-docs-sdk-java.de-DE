---
title: Spring Boot Starter für Azure
description: In diesem Artikel werden die verschiedenen verfügbaren Spring Boot Starter-Optionen für Azure beschrieben.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 678d4b279cecb83c95b3bf0f6bcdf1581924aa62
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893501"
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="30b76-103">Spring Boot Starter für Azure</span><span class="sxs-lookup"><span data-stu-id="30b76-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="30b76-104">In diesem Artikel werden die verschiedenen Spring Boot Starter-Optionen für [Spring Initializr] beschrieben, die Java-Entwicklern Integrationsfeatures für die Arbeit mit Microsoft Azure bieten.</span><span class="sxs-lookup"><span data-stu-id="30b76-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Spring Boot Starter-Optionen für Azure][spring-boot-starters]

<span data-ttu-id="30b76-106">Für Azure stehen aktuell folgende Spring Boot Starter-Optionen zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="30b76-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="30b76-107">**[Azure-Support](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="30b76-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="30b76-108">Bietet Unterstützung für die automatische Konfiguration von Azure-Diensten wie Service Bus, Storage und Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30b76-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="30b76-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="30b76-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="30b76-110">Bietet Integrationsunterstützung für Spring Security mit Azure Active Directory-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="30b76-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="30b76-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="30b76-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="30b76-112">Bietet Spring-Wertanmerkungsunterstützung für die Integration von Azure Key Vault-Geheimnissen.</span><span class="sxs-lookup"><span data-stu-id="30b76-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="30b76-113">**[Azure Storage](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="30b76-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="30b76-114">Bietet Spring Boot-Unterstützung für Azure Storage-Dienste.</span><span class="sxs-lookup"><span data-stu-id="30b76-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="30b76-115">Azure-Support</span><span class="sxs-lookup"><span data-stu-id="30b76-115">Azure Support</span></span>

<span data-ttu-id="30b76-116">Diese Spring Boot Starter-Option bietet Unterstützung für die automatische Konfiguration von Azure-Diensten wie Service Bus, Storage, Active Directory, Cosmos DB und Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30b76-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="30b76-117">Verwendungsbeispiele für die verschiedenen Azure-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="30b76-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

<span data-ttu-id="30b76-118">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="30b76-118">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="30b76-119">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="30b76-119">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="30b76-120">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="30b76-120">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="30b76-121">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="30b76-121">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="30b76-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30b76-122">Azure Active Directory</span></span>

<span data-ttu-id="30b76-123">Diese Spring Boot Starter-Option bietet Unterstützung für die automatische Konfiguration von Spring Security zur Integration von Azure Active Directory für die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="30b76-123">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="30b76-124">Verwendungsbeispiele für die Azure Active Directory-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="30b76-124">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

<span data-ttu-id="30b76-125">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="30b76-125">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="30b76-126">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="30b76-126">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="30b76-127">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="30b76-127">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="30b76-128">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="30b76-128">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="30b76-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="30b76-129">Azure Key Vault</span></span>

<span data-ttu-id="30b76-130">Diese Spring Boot Starter-Option bietet Spring-Wertanmerkungsunterstützung für die Integration von Azure Key Vault-Geheimnissen.</span><span class="sxs-lookup"><span data-stu-id="30b76-130">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="30b76-131">Verwendungsbeispiele für die Azure Key Vault-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="30b76-131">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

<span data-ttu-id="30b76-132">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="30b76-132">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="30b76-133">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="30b76-133">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="30b76-134">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="30b76-134">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="30b76-135">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="30b76-135">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="30b76-136">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="30b76-136">Azure Storage</span></span>

<span data-ttu-id="30b76-137">Diese Spring Boot Starter-Option bietet Spring Boot-Integrationsunterstützung für Azure Storage-Dienste.</span><span class="sxs-lookup"><span data-stu-id="30b76-137">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="30b76-138">Verwendungsbeispiele für die Azure Storage-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="30b76-138">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="30b76-139">Verwenden von Spring Boot Starter für Azure Storage</span><span class="sxs-lookup"><span data-stu-id="30b76-139">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

<span data-ttu-id="30b76-140">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="30b76-140">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="30b76-141">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="30b76-141">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="30b76-142">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="30b76-142">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="30b76-143">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="30b76-143">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="30b76-144">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="30b76-144">Next steps</span></span>

<span data-ttu-id="30b76-145">Weitere Informationen zur Verwendung von [Spring Boot] in Azure finden Sie unter [Spring Framework in Azure].</span><span class="sxs-lookup"><span data-stu-id="30b76-145">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="30b76-146">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="30b76-146">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="30b76-147">Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie bei **Spring Initializr** unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="30b76-147">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework in Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring on Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
