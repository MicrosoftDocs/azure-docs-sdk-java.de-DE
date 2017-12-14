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
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="97008-103">Spring Boot Starter für Azure</span><span class="sxs-lookup"><span data-stu-id="97008-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="97008-104">In diesem Artikel werden die verschiedenen Spring Boot Starter-Optionen für [Spring Initializr] beschrieben, die Java-Entwicklern Integrationsfeatures für die Arbeit mit Microsoft Azure bieten.</span><span class="sxs-lookup"><span data-stu-id="97008-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Spring Boot Starter-Optionen für Azure][spring-boot-starters]

<span data-ttu-id="97008-106">Für Azure stehen aktuell folgende Spring Boot Starter-Optionen zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="97008-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="97008-107">**[Azure-Support](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="97008-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="97008-108">Bietet Unterstützung für die automatische Konfiguration von Azure-Diensten wie Service Bus, Storage und Active Directory.</span><span class="sxs-lookup"><span data-stu-id="97008-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="97008-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="97008-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="97008-110">Bietet Integrationsunterstützung für Spring Security mit Azure Active Directory-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="97008-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="97008-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="97008-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="97008-112">Bietet Spring-Wertanmerkungsunterstützung für die Integration von Azure Key Vault-Geheimnissen.</span><span class="sxs-lookup"><span data-stu-id="97008-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="97008-113">**[Azure Storage](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="97008-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="97008-114">Bietet Spring Boot-Unterstützung für Azure Storage-Dienste.</span><span class="sxs-lookup"><span data-stu-id="97008-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="97008-115">Azure-Support</span><span class="sxs-lookup"><span data-stu-id="97008-115">Azure Support</span></span>

<span data-ttu-id="97008-116">Diese Spring Boot Starter-Option bietet Unterstützung für die automatische Konfiguration von Azure-Diensten wie Service Bus, Storage, Active Directory, Cosmos DB und Key Vault.</span><span class="sxs-lookup"><span data-stu-id="97008-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="97008-117">Verwendungsbeispiele für die verschiedenen Azure-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="97008-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="97008-118"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples></span><span class="sxs-lookup"><span data-stu-id="97008-118"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples></span></span>

<span data-ttu-id="97008-119">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="97008-119">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="97008-120">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="97008-120">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="97008-121">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="97008-121">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="97008-122">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="97008-122">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="97008-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97008-123">Azure Active Directory</span></span>

<span data-ttu-id="97008-124">Diese Spring Boot Starter-Option bietet Unterstützung für die automatische Konfiguration von Spring Security zur Integration von Azure Active Directory für die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="97008-124">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="97008-125">Verwendungsbeispiele für die Azure Active Directory-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="97008-125">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="97008-126"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="97008-126"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample></span></span>

<span data-ttu-id="97008-127">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="97008-127">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="97008-128">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="97008-128">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="97008-129">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="97008-129">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="97008-130">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="97008-130">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="97008-131">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="97008-131">Azure Key Vault</span></span>

<span data-ttu-id="97008-132">Diese Spring Boot Starter-Option bietet Spring-Wertanmerkungsunterstützung für die Integration von Azure Key Vault-Geheimnissen.</span><span class="sxs-lookup"><span data-stu-id="97008-132">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="97008-133">Verwendungsbeispiele für die Azure Key Vault-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="97008-133">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="97008-134"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="97008-134"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample></span></span>

<span data-ttu-id="97008-135">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="97008-135">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="97008-136">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="97008-136">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="97008-137">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="97008-137">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="97008-138">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="97008-138">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="97008-139">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="97008-139">Azure Storage</span></span>

<span data-ttu-id="97008-140">Diese Spring Boot Starter-Option bietet Spring Boot-Integrationsunterstützung für Azure Storage-Dienste.</span><span class="sxs-lookup"><span data-stu-id="97008-140">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="97008-141">Verwendungsbeispiele für die Azure Storage-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="97008-141">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="97008-142">Verwenden von Spring Boot Starter für Azure Storage</span><span class="sxs-lookup"><span data-stu-id="97008-142">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <span data-ttu-id="97008-143"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="97008-143"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample></span></span>

<span data-ttu-id="97008-144">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="97008-144">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="97008-145">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="97008-145">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="97008-146">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="97008-146">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="97008-147">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="97008-147">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="97008-148">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="97008-148">Next steps</span></span>

<span data-ttu-id="97008-149">Weitere Informationen zur Verwendung von [Spring Boot] in Azure finden Sie unter [Spring Framework in Azure].</span><span class="sxs-lookup"><span data-stu-id="97008-149">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="97008-150">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="97008-150">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="97008-151">Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie im **Spring Initializr** unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="97008-151">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework in Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
