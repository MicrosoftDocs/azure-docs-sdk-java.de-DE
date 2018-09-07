---
title: Bereitstellen einer Spring Boot-App in der Cloud mit Maven und Azure
description: Hier erfahren Sie, wie Sie eine Spring Boot-App mithilfe des Maven-Plug-Ins für Azure-Web-Apps in der Cloud bereitstellen.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ca788354d26964bd9f1e21a0d3a8005ff65ce4bc
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324346"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a><span data-ttu-id="a8ddb-103">Bereitstellen einer Spring Boot-App in der Cloud mithilfe des Maven-Plug-Ins für Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a8ddb-103">Deploy a Spring Boot app to the cloud using the Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="a8ddb-104">In diesem Artikel erfahren Sie, wie Sie mithilfe des Maven-Plug-Ins für Azure App Service-Web-Apps eine Spring Boot-Beispielanwendung bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-104">This article demonstrates using the Maven Plugin for Azure App Service Web Apps to deploy a sample Spring Boot application.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a8ddb-105">Das [Maven-Plug-In für Azure App Service-Web-Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) für [Apache Maven](http://maven.apache.org/) ermöglicht die nahtlose Integration von Azure App Service in Maven-Projekte und optimiert für Entwickler den Bereitstellungsprozess für Web-Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-105">The [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="a8ddb-106">Suchen Sie vor der Verwendung des Maven-Plug-Ins auf Maven Central nach der neuesten verfügbaren Version des Plug-Ins: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-106">Before using the Maven plugin, check on Maven Central for the latest available version of the plugin: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a8ddb-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="a8ddb-107">Prerequisites</span></span>

<span data-ttu-id="a8ddb-108">Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-108">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="a8ddb-109">Ein Azure-Abonnement. Sollten Sie noch nicht über ein Azure-Abonnement verfügen, können Sie sich für ein [kostenloses Azure-Konto] registrieren.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-109">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a8ddb-110">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="a8ddb-110">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="a8ddb-111">Ein aktuelles [Java Development Kit (JDK)], Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="a8ddb-111">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="a8ddb-112">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="a8ddb-113">Einen [Git]</span><span class="sxs-lookup"><span data-stu-id="a8ddb-113">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="a8ddb-114">Klonen der Beispiel-Web-App für Spring Boot</span><span class="sxs-lookup"><span data-stu-id="a8ddb-114">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="a8ddb-115">In diesem Abschnitt klonen Sie eine vollständige Spring Boot-Anwendung und testen sie lokal.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-115">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="a8ddb-116">Öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Spring Boot-Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-116">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="a8ddb-117">– oder –</span><span class="sxs-lookup"><span data-stu-id="a8ddb-117">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="a8ddb-118">Klonen Sie das Beispielprojekt [Spring Boot Getting Started] in das Verzeichnis, das Sie erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-118">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="a8ddb-119">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-119">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="a8ddb-120">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-120">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="a8ddb-121">Starten Sie die Web-App nach der Erstellung mithilfe von Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-121">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="a8ddb-122">Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-122">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="a8ddb-123">Sie können beispielsweise den folgenden Befehl verwenden, wenn curl verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-123">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="a8ddb-124">Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-124">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a><span data-ttu-id="a8ddb-125">Anpassen des Projekts für die WAR-basierte Bereitstellung in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a8ddb-125">Adjust project for WAR-based deployment on Azure App Service</span></span>

<span data-ttu-id="a8ddb-126">In diesem Abschnitt wird das Spring Boot-Projekt mit wenigen Handgriffen für die Bereitstellung als WAR-Datei in Azure App Service angepasst, wobei standardmäßig Tomcat als Laufzeit bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-126">In this section we will quickly adjust the Spring Boot project to be deployed as a WAR file on Azure App Service, which provides Tomcat as the runtime by default.</span></span> <span data-ttu-id="a8ddb-127">Hierzu müssen zwei Dateien geändert werden:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-127">For this to work, there are two files to be modified:</span></span>

- <span data-ttu-id="a8ddb-128">Die Maven-Datei `pom.xml`</span><span class="sxs-lookup"><span data-stu-id="a8ddb-128">The Maven `pom.xml` file</span></span>
- <span data-ttu-id="a8ddb-129">Die Java-Klasse `Application`</span><span class="sxs-lookup"><span data-stu-id="a8ddb-129">The `Application` Java class</span></span>

<span data-ttu-id="a8ddb-130">Beginnen wir mit den Maven-Einstellungen:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-130">Let's start with the Maven settings:</span></span>

1. <span data-ttu-id="a8ddb-131">Öffnen Sie `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-131">Open `pom.xml`</span></span>

1. <span data-ttu-id="a8ddb-132">Fügen Sie `<packaging>war</packaging>` direkt nach der Definition `<artifactId>` am Anfang der Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-132">Add `<packaging>war</packaging>` right after the `<artifactId>` definition at the top:</span></span>
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. <span data-ttu-id="a8ddb-133">Fügen Sie die folgende Abhängigkeit hinzu:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-133">Add the following dependency:</span></span>
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

<span data-ttu-id="a8ddb-134">Öffnen Sie als Nächstes die Klasse `Application`, und nehmen Sie die folgenden Änderungen vor. (Die neuen Abhängigkeiten sollten bereits von der IDE erkannt worden sein.)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-134">Now open the class `Application`, hopefully after your IDE has already picked up the new dependencies, and proceed with the following modifications:</span></span>

1. <span data-ttu-id="a8ddb-135">Legen Sie die Application-Klasse als Unterklasse von `SpringBootServletInitializer` fest:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-135">Make class Application a subclass of `SpringBootServletInitializer`:</span></span>
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. <span data-ttu-id="a8ddb-136">Fügen Sie der Application-Klasse die folgende Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-136">Add the following method to the Application class:</span></span>
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```
1. <span data-ttu-id="a8ddb-137">Strukturieren Sie Ihre Importe, um sicherzustellen, dass `SpringApplicationBuilder` und `SpringBootServletInitializer` richtig importiert werden.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-137">Organize your imports to ensure `SpringApplicationBuilder` and `SpringBootServletInitializer` are properly imported.</span></span>

<span data-ttu-id="a8ddb-138">Ihre Anwendung kann jetzt für Tomcat sowie für jede andere Servlet-Laufzeit (beispielsweise Jetty) bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-138">Your application is now ready to be deployed to Tomcat and any other Servlet runtime (e.g. Jetty).</span></span>

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a><span data-ttu-id="a8ddb-139">Hinzufügen des Maven-Plug-Ins für Azure App Service-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="a8ddb-139">Add the Maven Plugin for Azure App Service Web Apps</span></span>

<span data-ttu-id="a8ddb-140">In diesem Abschnitt wird ein Maven-Plug-In hinzugefügt, das die gesamte Bereitstellung dieser Anwendung in Azure App Service-Web-Apps automatisiert.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-140">In this section, we will add a Maven plugin that will automate the entire deployment of this application into Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="a8ddb-141">Öffnen Sie erneut `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-141">Open `pom.xml` once again.</span></span>

1. <span data-ttu-id="a8ddb-142">Legen Sie in `<properties>` mithilfe der Eigenschaft `maven.build.timestamp.format` ein benutzerdefiniertes Zeitstempelformat fest.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-142">Inside `<properties>`, set a custom timestamp format with the property `maven.build.timestamp.format`.</span></span> <span data-ttu-id="a8ddb-143">Da Azure App Service eine öffentliche URL für Ihre Anwendung erstellt, wird diese Einstellung verwendet, um den Namen Ihrer Bereitstellung zu generieren und so Konflikte mit Livebereitstellungen anderer Benutzer zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-143">Because Azure App Service creates a public URL for your application, this setting will be used to generate the name of your deployment, and avoid conflict with other users' live deployments.</span></span>
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. <span data-ttu-id="a8ddb-144">Fügen Sie im Element `<plugins>` Folgendes hinzu:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-144">In the `<plugins>` element, add the following:</span></span>
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

<span data-ttu-id="a8ddb-145">Mit diesen Einstellungen ist Ihr Maven-Projekt nun für die Livebereitstellung in Azure App Service-Web-Apps bereit.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-145">With these settings, your Maven project is now ready for live deployment to Azure App Service Web App.</span></span>

## <a name="install-and-log-in-to-azure-cli"></a><span data-ttu-id="a8ddb-146">Installieren der Azure CLI und Anmelden bei der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8ddb-146">Install and log in to Azure CLI</span></span>

<span data-ttu-id="a8ddb-147">Bei Verwendung des Maven-Plug-Ins lässt sich die Spring Boot-Anwendung am einfachsten und komfortabelsten über die [Azure CLI](https://docs.microsoft.com/cli/azure/) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-147">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span> <span data-ttu-id="a8ddb-148">Vergewissern Sie sich, dass sie installiert ist.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-148">Make sure you have it installed.</span></span>

1. <span data-ttu-id="a8ddb-149">Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-149">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
   <span data-ttu-id="a8ddb-150">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-150">Follow the instructions to complete the sign-in process.</span></span>

## <a name="optionally-customize-pomxml-before-deploying"></a><span data-ttu-id="a8ddb-151">Optional: Anpassen der Datei „pom.xml“ vor der Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="a8ddb-151">Optionally, customize pom.xml before deploying</span></span>

<span data-ttu-id="a8ddb-152">Öffnen Sie die Datei `pom.xml` für Ihre Spring Boot-Anwendung in einem Text-Editor, und suchen Sie das Element `<plugin>` für `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-152">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="a8ddb-153">Dieses Element sollte etwa wie folgendes Beispiel aussehen:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-153">This element should resemble the following example:</span></span>

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

<span data-ttu-id="a8ddb-154">Für das Maven-Plug-In können mehrere Werte angepasst werden. Eine ausführliche Beschreibung der einzelnen Elemente finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].</span><span class="sxs-lookup"><span data-stu-id="a8ddb-154">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="a8ddb-155">Für diesen Artikel sind jedoch besonders folgende Werte hervorzuheben:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-155">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="a8ddb-156">Element</span><span class="sxs-lookup"><span data-stu-id="a8ddb-156">Element</span></span> | <span data-ttu-id="a8ddb-157">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="a8ddb-157">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="a8ddb-158">Gibt die Version des [Maven-Plug-In für Azure-Web-Apps] an.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-158">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="a8ddb-159">Überprüfen Sie die im [zentralen Maven-Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) angegebene Version, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-159">Verify the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="a8ddb-160">Gibt die Zielressourcengruppe an (in diesem Beispiel: `maven-plugin`).</span><span class="sxs-lookup"><span data-stu-id="a8ddb-160">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="a8ddb-161">Wenn die Ressourcengruppe nicht bereits vorhanden ist, wird sie während der Bereitstellung erstellt.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-161">The resource group is created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="a8ddb-162">Gibt den Zielnamen für Ihre Web-App an.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-162">Specifies the target name for your web app.</span></span> <span data-ttu-id="a8ddb-163">In diesem Beispiel lautet der Zielname `maven-web-app-${maven.build.timestamp}`. Dabei wird das Suffix `${maven.build.timestamp}` angehängt, um Konflikte zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-163">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="a8ddb-164">(Der Zeitstempel ist optional. Sie können eine beliebige eindeutige Zeichenfolge für den App-Namen angeben.)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-164">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="a8ddb-165">Gibt die Zielregion an (in diesem Beispiel: `westus`).</span><span class="sxs-lookup"><span data-stu-id="a8ddb-165">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="a8ddb-166">(Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-166">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<javaVersion>` | <span data-ttu-id="a8ddb-167">Gibt die Java Runtime-Version für Ihre Web-App an.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-167">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="a8ddb-168">(Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-168">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<deploymentType>` | <span data-ttu-id="a8ddb-169">Gibt den Bereitstellungstyp für Ihre Web-App an.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="a8ddb-170">Der Standardwert ist `war`.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-170">Default is `war`.</span></span> |

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="a8ddb-171">Erstellen und Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="a8ddb-171">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="a8ddb-172">Nachdem Sie alle Einstellungen in den vorhergehenden Abschnitten in diesem Artikel konfiguriert haben, können Sie Ihre Web-App in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-172">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="a8ddb-173">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-173">To do so, use the following steps:</span></span>

1. <span data-ttu-id="a8ddb-174">Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-174">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="a8ddb-175">Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-175">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="a8ddb-176">Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App noch nicht vorhanden ist, wird sie erstellt.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-176">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="a8ddb-177">Wenn Ihre Web-App bereitgestellt wurde, können Sie sie mit dem [Azure-Portal] verwalten.</span><span class="sxs-lookup"><span data-stu-id="a8ddb-177">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="a8ddb-178">Ihre Web-App wird unter **App Services** aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-178">Your web app will be listed in **App Services**:</span></span>

   ![Im Azure-Portal unter „App Services“ aufgeführte Web-App][AP01]

* <span data-ttu-id="a8ddb-180">Die URL für Ihre Web-App wird in der **Übersicht** für Ihre Web-App aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-180">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Festlegen der URL für Ihre Web-App][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="a8ddb-182">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="a8ddb-182">Next steps</span></span>

<span data-ttu-id="a8ddb-183">Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="a8ddb-183">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="a8ddb-184">[Maven-Plug-In für Azure-Web-Apps] (Maven-Plug-In für Azure-Web-Apps)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-184">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="a8ddb-185">Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-185">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="a8ddb-186">Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="a8ddb-186">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="a8ddb-187">Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a8ddb-187">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* <span data-ttu-id="a8ddb-188">[Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)</span><span class="sxs-lookup"><span data-stu-id="a8ddb-188">[Maven Settings Reference](https://maven.apache.org/settings.html)</span></span>

<!-- URL List -->

[Azure-Befehlszeilenschnittstelle (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven-Plug-In für Azure-Web-Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme (Maven-Plug-In für Azure-Web-Apps)
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
