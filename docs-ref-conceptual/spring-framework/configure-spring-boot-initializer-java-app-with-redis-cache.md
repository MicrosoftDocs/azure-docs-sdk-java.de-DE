---
title: Konfigurieren einer Spring Boot Initializer-App für die Verwendung von Azure Redis Cache
description: Konfigurieren Sie eine mit Spring Initializr erstellte Spring Boot-Anwendung für die Verwendung von Redis in der Cloud mit Azure Redis Cache.
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: cache
ms.tgt_pltfrm: cache-redis
ms.topic: article
ms.workload: na
ms.openlocfilehash: 2c4dfe35ed2f4728e5704aac938410f847fe5b1f
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338674"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-redis-in-the-cloud-with-azure-redis-cache"></a><span data-ttu-id="e0134-103">Konfigurieren einer Spring Boot Initializer-App für die Verwendung von Redis in der Cloud mit Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e0134-103">Configure a Spring Boot Initializer app to use Redis in the cloud with Azure Redis Cache</span></span>

<span data-ttu-id="e0134-104">Dieser Artikel führt Sie durch das Erstellen einer Redis Cache-Instanz in der Cloud über das Azure-Portal, das anschließende Erstellen einer benutzerdefinierten Anwendung mit **[Spring Initializr]** und schließlich das Erstellen einer Java-Webanwendung, die Daten mithilfe Ihrer Redis Cache-Instanz speichert und abruft.</span><span class="sxs-lookup"><span data-stu-id="e0134-104">This article walks you through creating a Redis cache in the cloud using the Azure portal, then using the **[Spring Initializr]** to create a custom application, and then creating a Java web application that stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0134-105">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="e0134-105">Prerequisites</span></span>

<span data-ttu-id="e0134-106">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="e0134-106">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="e0134-107">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="e0134-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e0134-108">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="e0134-108">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="e0134-109">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="e0134-109">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="e0134-110">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="e0134-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="e0134-111">Erstellen einer benutzerdefinierten Anwendung mit dem Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="e0134-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="e0134-112">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e0134-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e0134-113">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.</span><span class="sxs-lookup"><span data-stu-id="e0134-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="e0134-115">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt**, z.B. *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="e0134-115">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="e0134-116">Scrollen Sie nach unten zum Abschnitt **Web**, und aktivieren Sie das Kontrollkästchen für **Web**, scrollen Sie nach unten zum Abschnitt **NoSQL**, und aktivieren Sie das Kontrollkästchen für **Redis**, scrollen Sie zum unteren Rand der Seite, und klicken Sie auf die Schaltfläche, um das **Projekt zu generieren**.</span><span class="sxs-lookup"><span data-stu-id="e0134-116">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Vollständige Spring Initializr-Optionen][SI02]

1. <span data-ttu-id="e0134-118">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="e0134-118">When prompted, download the project to a path on your local computer.</span></span>

   ![Herunterladen eines benutzerdefinierten Spring Boot-Projekts][SI03]

1. <span data-ttu-id="e0134-120">Nachdem Sie die Dateien auf dem lokalen System extrahiert haben, kann Ihre benutzerdefinierte Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="e0134-120">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI04]

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="e0134-122">Erstellen eines Redis-Caches in Azure</span><span class="sxs-lookup"><span data-stu-id="e0134-122">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="e0134-123">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und klicken Sie auf **+Neu**.</span><span class="sxs-lookup"><span data-stu-id="e0134-123">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure-Portal][AZ01]

1. <span data-ttu-id="e0134-125">Klicken Sie auf **Datenbank**, und klicken Sie dann auf **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="e0134-125">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure-Portal][AZ02]

1. <span data-ttu-id="e0134-127">Geben Sie auf der Seite **Neuer Redis Cache** Folgendes an:</span><span class="sxs-lookup"><span data-stu-id="e0134-127">On the **New Redis Cache** page, specify the following information:</span></span>

   * <span data-ttu-id="e0134-128">Geben Sie den **DNS-Namen** für den Cache ein.</span><span class="sxs-lookup"><span data-stu-id="e0134-128">Enter the **DNS name** for your cache.</span></span>
   * <span data-ttu-id="e0134-129">Geben Sie Ihre Informationen zu **Abonnement**, **Ressourcengruppe**, **Standort** und **Tarif** an.</span><span class="sxs-lookup"><span data-stu-id="e0134-129">Specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span>
   * <span data-ttu-id="e0134-130">Wählen Sie für dieses Tutorial **Unblock port 6379** aus.</span><span class="sxs-lookup"><span data-stu-id="e0134-130">For this tutorial, choose **Unblock port 6379**.</span></span>

   > [!NOTE]
   >
   > <span data-ttu-id="e0134-131">Sie können SSL mit Redis Caches verwenden, müssen jedoch einen anderen Redis-Client als Jedis verwenden.</span><span class="sxs-lookup"><span data-stu-id="e0134-131">You can use SSL with Redis caches, but you would need to use a different Redis client like Jedis.</span></span> <span data-ttu-id="e0134-132">Weitere Informationen finden Sie unter [Verwenden von Azure Redis Cache mit Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="e0134-132">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

   <span data-ttu-id="e0134-133">Wenn Sie diese Optionen angegeben haben, klicken Sie zum Erstellen des Cache auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e0134-133">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Azure-Portal][AZ03]

1. <span data-ttu-id="e0134-135">Nachdem Ihr Cache abgeschlossen wurde, wird er auf Ihrem Azure-**Dashboard** sowie auf den Seiten **Alle Ressourcen** und **Redis-Caches** aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="e0134-135">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="e0134-136">Sie können an jedem dieser Orte auf Ihren Cache klicken, um die Seite „Eigenschaften“ für den Cache zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="e0134-136">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Azure-Portal][AZ04]

1. <span data-ttu-id="e0134-138">Wenn die Seite mit der Liste der Eigenschaften für den Cache angezeigt wird, klicken Sie auf **Zugriffsschlüssel**, und kopieren Sie die Zugriffsschlüssel für Ihren Cache.</span><span class="sxs-lookup"><span data-stu-id="e0134-138">When the page that contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure-Portal][AZ05]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="e0134-140">Konfigurieren Ihres benutzerdefinierten Spring Boot für die Verwendung von Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e0134-140">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="e0134-141">Suchen Sie die Datei *application.properties* im *Ressourcen*-Verzeichnis Ihrer App, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="e0134-141">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Suchen der Datei „application.properties“][RE01]

1. <span data-ttu-id="e0134-143">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie der Datei die folgenden Zeilen hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften aus Ihrem Cache:</span><span class="sxs-lookup"><span data-stu-id="e0134-143">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6379

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Bearbeiten der Datei „application.properties“][RE02]

   > [!NOTE] 
   > 
   > <span data-ttu-id="e0134-145">Wenn Sie einen anderen SSL-fähigen Redis-Client als Jedis verwendet haben, geben Sie in Ihrer Datei *application.properties* an, dass Sie SSL verwenden möchten, und verwenden Sie Port 6380.</span><span class="sxs-lookup"><span data-stu-id="e0134-145">If you were using a different Redis client like Jedis that enables SSL, you would specify that you want to use SSL in your *application.properties* file and use port 6380.</span></span> <span data-ttu-id="e0134-146">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="e0134-146">For example:</span></span>
   > 
   > ```yaml
   > # Specify the DNS URI of your Redis cache.
   > spring.redis.host=myspringbootcache.redis.cache.windows.net
   > # Specify the access key for your Redis cache.
   > spring.redis.password=57686f6120447564652c2049495320526f636b73=
   > # Specify that you want to use SSL.
   > spring.redis.ssl=true
   > # Specify the SSL port for your Redis cache.
   > spring.redis.port=6380
   > ```
   > 
   > <span data-ttu-id="e0134-147">Weitere Informationen finden Sie unter [Verwenden von Azure Redis Cache mit Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="e0134-147">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span> 
   > 

1. <span data-ttu-id="e0134-148">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="e0134-148">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="e0134-149">Erstellen Sie einen Ordner mit dem Namen *controller* unter den Quellordner für Ihr Paket, zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="e0134-149">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="e0134-150">Oder</span><span class="sxs-lookup"><span data-stu-id="e0134-150">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="e0134-151">Erstellen Sie eine neue Datei mit dem Namen *HelloController.java* im *controller*-Ordner.</span><span class="sxs-lookup"><span data-stu-id="e0134-151">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="e0134-152">Öffnen Sie die Datei in einem Text-Editor, und fügen Sie den folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="e0134-152">Open the file in a text editor and add the following code to it:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.data.redis.core.StringRedisTemplate;
   import org.springframework.data.redis.core.ValueOperations;

   @RestController
   public class HelloController {
   
      @Autowired
      private StringRedisTemplate template;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         ValueOperations<String, String> ops = this.template.opsForValue();

         // Add a Hello World string to your cache.
         String key = "greeting";
         if (!this.template.hasKey(key)) {
             ops.set(key, "Hello World!");
         }

         // Return the string from your cache.
         return ops.get(key);
      }
   }
   ```
   
   <span data-ttu-id="e0134-153">Dabei müssen Sie `com.contoso.myazuredemo` durch den Paketnamen für das Projekt ersetzen.</span><span class="sxs-lookup"><span data-stu-id="e0134-153">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="e0134-154">Speichern und schließen Sie die Datei *HelloController.java*.</span><span class="sxs-lookup"><span data-stu-id="e0134-154">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="e0134-155">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="e0134-155">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="e0134-156">Testen Sie die Web-App unter http://localhost:8080 in einem Webbrowser, oder verwenden Sie die Syntax aus dem folgenden Beispiel (sofern Curl verfügbar ist):</span><span class="sxs-lookup"><span data-stu-id="e0134-156">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="e0134-157">Es sollte die Meldung „Hello World!“</span><span class="sxs-lookup"><span data-stu-id="e0134-157">You should see the "Hello World!"</span></span> <span data-ttu-id="e0134-158">von Ihrem Beispielcontroller angezeigt werden, die dynamisch aus dem Redis Cache abgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="e0134-158">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0134-159">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="e0134-159">Next steps</span></span>

<span data-ttu-id="e0134-160">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="e0134-160">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="e0134-161">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e0134-161">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="e0134-162">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="e0134-162">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="e0134-163">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e0134-163">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e0134-164">Weitere Informationen zu den ersten Schritten mit Redis Cache mit Java in Azure finden Sie unter [Verwenden von Azure Redis Cache mit Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="e0134-164">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<span data-ttu-id="e0134-165">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="e0134-165">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e0134-166">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="e0134-166">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="e0134-167">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="e0134-167">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="e0134-168">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="e0134-168">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: /azure/redis-cache/cache-java-get-started

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ01.png
[AZ02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ02.png
[AZ03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ03.png
[AZ04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ04.png
[AZ05]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ05.png

[SI01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI01.png
[SI02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI02.png
[SI03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI03.png
[SI04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI04.png

[RE01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE01.png
[RE02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE02.png
