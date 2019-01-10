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
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 69c0381313994796af31d5301ceadb9f6f40dcb5
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991554"
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="1daca-103">Spring Boot Starter für Azure</span><span class="sxs-lookup"><span data-stu-id="1daca-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="1daca-104">In diesem Artikel werden die verschiedenen Spring Boot Starter-Optionen für [Spring Initializr] beschrieben, die Java-Entwicklern Integrationsfeatures für die Arbeit mit Microsoft Azure bieten.</span><span class="sxs-lookup"><span data-stu-id="1daca-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Spring Boot Starter-Optionen für Azure][spring-boot-starters]

<span data-ttu-id="1daca-106">Für Azure stehen aktuell folgende Spring Boot Starter-Optionen zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="1daca-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="1daca-107">**[Azure-Support](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="1daca-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="1daca-108">Bietet Unterstützung für die automatische Konfiguration von Azure-Diensten wie Service Bus, Storage und Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1daca-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="1daca-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="1daca-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="1daca-110">Bietet Integrationsunterstützung für Spring Security mit Azure Active Directory-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="1daca-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="1daca-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="1daca-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="1daca-112">Bietet Spring-Wertanmerkungsunterstützung für die Integration von Azure Key Vault-Geheimnissen.</span><span class="sxs-lookup"><span data-stu-id="1daca-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="1daca-113">**[Azure Storage](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="1daca-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="1daca-114">Bietet Spring Boot-Unterstützung für Azure Storage-Dienste.</span><span class="sxs-lookup"><span data-stu-id="1daca-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="1daca-115">Azure-Support</span><span class="sxs-lookup"><span data-stu-id="1daca-115">Azure Support</span></span>

<span data-ttu-id="1daca-116">Dieser Spring Boot Starter bietet Unterstützung für die automatische Konfiguration für Azure-Dienste, z. B.: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault usw.</span><span class="sxs-lookup"><span data-stu-id="1daca-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="1daca-117">Verwendungsbeispiele für die verschiedenen Azure-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="1daca-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

<span data-ttu-id="1daca-118">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="1daca-118">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="1daca-119">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1daca-119">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="1daca-120">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="1daca-120">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="1daca-121">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1daca-121">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="1daca-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1daca-122">Azure Active Directory</span></span>

<span data-ttu-id="1daca-123">Diese Spring Boot Starter-Option bietet Unterstützung für die automatische Konfiguration von Spring Security zur Integration von Azure Active Directory für die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="1daca-123">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="1daca-124">Verwendungsbeispiele für die Azure Active Directory-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="1daca-124">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

<span data-ttu-id="1daca-125">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="1daca-125">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="1daca-126">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1daca-126">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="1daca-127">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="1daca-127">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="1daca-128">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1daca-128">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="1daca-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="1daca-129">Azure Key Vault</span></span>

<span data-ttu-id="1daca-130">Diese Spring Boot Starter-Option bietet Spring-Wertanmerkungsunterstützung für die Integration von Azure Key Vault-Geheimnissen.</span><span class="sxs-lookup"><span data-stu-id="1daca-130">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="1daca-131">Verwendungsbeispiele für die Azure Key Vault-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="1daca-131">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

<span data-ttu-id="1daca-132">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="1daca-132">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="1daca-133">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1daca-133">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="1daca-134">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="1daca-134">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="1daca-135">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1daca-135">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="1daca-136">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1daca-136">Azure Storage</span></span>

<span data-ttu-id="1daca-137">Diese Spring Boot Starter-Option bietet Spring Boot-Integrationsunterstützung für Azure Storage-Dienste.</span><span class="sxs-lookup"><span data-stu-id="1daca-137">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="1daca-138">Verwendungsbeispiele für die Azure Storage-Features, die von dieser Starter-Option bereitgestellt werden, finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="1daca-138">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="1daca-139">Verwenden von Spring Boot Starter für Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1daca-139">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

<span data-ttu-id="1daca-140">Wenn Sie diese Starter-Option einem Spring Boot-Projekt hinzufügen, werden an der Datei *pom.xml* folgende Änderungen vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="1daca-140">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="1daca-141">Dem Element `<properties>` wird folgende Eigenschaft hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1daca-141">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="1daca-142">Die Standardabhängigkeit `spring-boot-starter` wird durch Folgendes ersetzt:</span><span class="sxs-lookup"><span data-stu-id="1daca-142">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="1daca-143">Der Datei wird der folgende Abschnitt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1daca-143">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1daca-144">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="1daca-144">Next steps</span></span>

<span data-ttu-id="1daca-145">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="1daca-145">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1daca-146">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="1daca-146">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="1daca-147">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="1daca-147">Additional Resources</span></span>

<span data-ttu-id="1daca-148">Weitere Informationen zur Verwendung von [Spring Boot] in Azure finden Sie unter [Spring Framework in Azure].</span><span class="sxs-lookup"><span data-stu-id="1daca-148">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="1daca-149">Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und [Working with Azure DevOps and Java] (Arbeiten mit Azure DevOps und Java).</span><span class="sxs-lookup"><span data-stu-id="1daca-149">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="1daca-150">Hilfe zu den ersten Schritten mit eigenen Spring Boot-Anwendungen finden Sie bei **Spring Initializr** unter https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="1daca-150">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure für Java-Entwickler]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Working with Azure DevOps and Java]: /azure/devops/ (Arbeiten mit Azure DevOps und Java)
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework in Azure]: /java/azure/spring-framework/
[Spring on Azure]: /java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
