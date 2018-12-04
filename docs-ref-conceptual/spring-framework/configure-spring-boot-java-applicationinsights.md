---
title: Konfigurieren einer Spring Boot Initializer-App für die Verwendung von Azure Application Insights Spring Boot Starter
description: Hier erfahren Sie, wie Sie eine mit Spring Initializr erstellte Spring Boot-Anwendung für die Verwendung von Application Insights Spring Boot Starter konfigurieren.
services: Application-Insights
documentationcenter: java
author: dhaval24
manager: alexklim
editor: ''
ms.assetid: ''
ms.author: dhdoshi
ms.date: 11/21/2018
ms.devlang: java
ms.service: Azure Monitor
ms.tgt_pltfrm: application-insights
ms.topic: article
ms.workload: na
ms.openlocfilehash: eef5afa1bcd8ceb92eca1584df8816b73ac78948
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338734"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a><span data-ttu-id="edffb-103">Konfigurieren einer Spring Boot Initializer-App für die Verwendung von Application Insights</span><span class="sxs-lookup"><span data-stu-id="edffb-103">Configure a Spring Boot Initializer app to use Application Insights</span></span>

<span data-ttu-id="edffb-104">In diesem Artikel erfahren Sie Schritt für Schritt, wie Sie eine Spring Boot-Anwendung unter Verwendung von **[Spring Initializr]** erstellen, die Azure Application Insights Spring Boot Starter für die End-to-End-Überwachung von Java-Anwendungen in der Cloud verwendet.</span><span class="sxs-lookup"><span data-stu-id="edffb-104">This article walks you through creating a Spring Boot application using **[Spring Initializr]**, that uses Azure Application Insights Spring Boot Starter for end-to-end monitoring of Java applications on cloud.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="edffb-105">\*Diese Starter-Option ist momentan als \**Betaversion (Public Preview)* <em>erhältlich.</em></span><span class="sxs-lookup"><span data-stu-id="edffb-105">\*This starter is currently in \**BETA (public preview)*<em>.</em></span></span>

## <a name="prerequisites"></a><span data-ttu-id="edffb-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="edffb-106">Prerequisites</span></span>

<span data-ttu-id="edffb-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="edffb-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="edffb-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="edffb-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="edffb-109">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="edffb-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="edffb-110">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="edffb-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="edffb-111">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="edffb-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="edffb-112">Erstellen einer benutzerdefinierten Anwendung mit dem Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="edffb-112">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="edffb-113">Navigieren Sie zu [https://start.spring.io/](https://start.spring.io/).</span><span class="sxs-lookup"><span data-stu-id="edffb-113">Browse to [https://start.spring.io/](https://start.spring.io/).</span></span>

1. <span data-ttu-id="edffb-114">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und wählen Sie im Abschnitt mit den Abhängigkeiten die Webabhängigkeit aus.</span><span class="sxs-lookup"><span data-stu-id="edffb-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select web dependency in the dependenies section.</span></span>

   ![Grundlegende Spring Initializr-Optionen][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="edffb-116">Spring Initializr verwendet zur Erstellung des Paketnamens die Namen für **Gruppe** und **Artefakt** (also beispielsweise *com.example.demo*).</span><span class="sxs-lookup"><span data-stu-id="edffb-116">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.example.demo*.</span></span>
   >

1. <span data-ttu-id="edffb-117">Klicken Sie auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="edffb-117">Click the button to **Generate Project**.</span></span>

1. <span data-ttu-id="edffb-118">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="edffb-118">When prompted, download the project to a path on your local computer.</span></span>

1. <span data-ttu-id="edffb-119">Nachdem Sie die Dateien auf dem lokalen System extrahiert haben, kann Ihre benutzerdefinierte Spring Boot-Anwendung bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="edffb-119">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Dateien eines benutzerdefinierten Spring Boot-Projekts][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a><span data-ttu-id="edffb-121">Erstellen einer Application Insights-Ressource in Azure</span><span class="sxs-lookup"><span data-stu-id="edffb-121">Create an Application Insights Resource on Azure</span></span>

1. <span data-ttu-id="edffb-122">Navigieren Sie zum Azure-Portal unter <https://portal.azure.com/>, und klicken Sie auf **+Neu**.</span><span class="sxs-lookup"><span data-stu-id="edffb-122">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure-Portal][AZ01]

1. <span data-ttu-id="edffb-124">Klicken Sie auf **Verwaltungstools** und anschließend auf **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="edffb-124">Click **Management Tools**, and then click **Application Insights**.</span></span>

   ![Azure-Portal][AZ02]

1. <span data-ttu-id="edffb-126">Geben Sie auf der Seite **Neue Application Insights-Ressource** folgende Informationen an:</span><span class="sxs-lookup"><span data-stu-id="edffb-126">On the **New Application Insights Resource** page, specify the following information:</span></span>

   * <span data-ttu-id="edffb-127">Geben Sie unter **Name** den Namen für Ihre Application Insights-Ressource ein.</span><span class="sxs-lookup"><span data-stu-id="edffb-127">Enter the **Name** for your Application Insights resource.</span></span>
   * <span data-ttu-id="edffb-128">Legen Sie den **Anwendungstyp** auf „Java-Webanwendung“ fest.</span><span class="sxs-lookup"><span data-stu-id="edffb-128">Choose the **Application Type** to Java Web Application.</span></span>
   * <span data-ttu-id="edffb-129">Geben Sie Ihr **Abonnement**, Ihre **Ressourcengruppe** und Ihren **Standort** an.</span><span class="sxs-lookup"><span data-stu-id="edffb-129">Specify your **Subscription**, **Resource group** and **Location**.</span></span>
   * <span data-ttu-id="edffb-130">Aktivieren Sie die Option „An Dashboard anheften“, wenn Sie die Ressource an Ihr Azure-Portal anheften möchten.</span><span class="sxs-lookup"><span data-stu-id="edffb-130">Select Pin to dashboard option, if you would like to pin the resource on your Azure portal.</span></span>

   <span data-ttu-id="edffb-131">Wenn Sie diese Optionen angegeben haben, klicken Sie auf **Erstellen**, um Ihre Application Insights-Ressource zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="edffb-131">When you have specified these options, click **Create** to create your Application Insights resource.</span></span>

   ![Azure-Portal][AZ03]

1. <span data-ttu-id="edffb-133">Die erstellte Ressource wird auf Ihrem **Azure-Dashboard** sowie auf den Seiten **Alle Ressourcen** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="edffb-133">Once your resource has been created, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources** pages.</span></span> <span data-ttu-id="edffb-134">Klicken Sie an einem dieser Orte auf Ihre Ressource, um die Übersichtsseite der Application Insights-Ressource zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="edffb-134">You can click on your resource on any of those locations to open the overview page of the Application Insights resource.</span></span> <span data-ttu-id="edffb-135">Kopieren Sie auf dieser Übersichtsseite den **Instrumentierungsschlüssel**.</span><span class="sxs-lookup"><span data-stu-id="edffb-135">From this overview page please copy the **instrumentation key**.</span></span>

   ![Azure-Portal][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a><span data-ttu-id="edffb-137">Konfigurieren Ihrer heruntergeladenen Spring Boot-Anwendung für die Verwendung von Application Insights</span><span class="sxs-lookup"><span data-stu-id="edffb-137">Configure your downloaded Spring Boot Application to use Application Insights</span></span>

1. <span data-ttu-id="edffb-138">Suchen Sie im Stammverzeichnis Ihrer App nach der Datei *POM.xml*, und fügen Sie dem Abschnitt mit den Abhängigkeiten die folgende Abhängigkeit hinzu.</span><span class="sxs-lookup"><span data-stu-id="edffb-138">Locate the *POM.xml* file in the root directory of your app, and add the following dependency in its dependencies section.</span></span> 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.0.1-BETA</version>
</dependency>
```

1. <span data-ttu-id="edffb-139">Suchen Sie die Datei *application.properties* im *Ressourcen*-Verzeichnis Ihrer App, oder erstellen Sie diese Datei, wenn sie noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="edffb-139">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Suchen der Datei „application.properties“][RE01]

1. <span data-ttu-id="edffb-141">Öffnen Sie die Datei *application.properties* in einem Text-Editor, und fügen Sie der Datei die folgenden Zeilen hinzu. Ersetzen Sie dabei die Beispielwerte durch die entsprechenden Eigenschaften mit entsprechenden Anmeldeinformationen:</span><span class="sxs-lookup"><span data-stu-id="edffb-141">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties with appropriate credentials:</span></span>

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   <span data-ttu-id="edffb-142">Weitere Optimierungsoptionen für Application Insights finden Sie in der [Infodatei für Application Insights Spring Boot Starter](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="edffb-142">For more ways to fine tune Application Insights please refer to [Application Insights Springboot starter readme](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="edffb-143">Sie können verschiedene Application Insights-Instrumentierungsschlüssel (sprich:</span><span class="sxs-lookup"><span data-stu-id="edffb-143">You can use different Application Insights instrumentation keys (i.e</span></span> <span data-ttu-id="edffb-144">verschiedene Ressourcen) für verschiedene Profile (etwa PROD oder DEV) verwenden. Weitere Informationen finden Sie unter [Spezifische Eigenschaften für Spring Boot-Profile] für zusätzliche Informationen.</span><span class="sxs-lookup"><span data-stu-id="edffb-144">different resources) for different profiles like PROD, DEV etc. Please refer to [Spring Boot Profile Specific Properties] for additional information.</span></span> 

1. <span data-ttu-id="edffb-145">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="edffb-145">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="edffb-146">Erstellen Sie einen Ordner mit dem Namen *controller* unter den Quellordner für Ihr Paket, zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="edffb-146">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   <span data-ttu-id="edffb-147">Oder</span><span class="sxs-lookup"><span data-stu-id="edffb-147">-or-</span></span>

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. <span data-ttu-id="edffb-148">Erstellen Sie im Ordner *controller* eine neue Datei mit dem Namen *TestController.java*.</span><span class="sxs-lookup"><span data-stu-id="edffb-148">Create a new file named *TestController.java* in the *controller* folder.</span></span> <span data-ttu-id="edffb-149">Öffnen Sie die Datei in einem Text-Editor, und fügen Sie den folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="edffb-149">Open the file in a text editor and add the following code to it:</span></span>

   ```java
    package com.example.demo;

    import com.microsoft.applicationinsights.TelemetryClient;
    import java.io.IOException;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    import com.microsoft.applicationinsights.telemetry.Duration;

    @RestController
    @RequestMapping("/sample")
    public class TestController {

        @Autowired
        TelemetryClient telemetryClient;

        @GetMapping("/hello")
        public String hello() {

            //track a custom event  
            telemetryClient.trackEvent("Sending a custom event...");

            //trace a custom trace
            telemetryClient.trackTrace("Sending a custom trace....");

            //track a custom metric
            telemetryClient.trackMetric("custom metric", 1.0);

            //track a custom dependency
            telemetryClient.trackDependency("SQL", "Insert", new Duration(0, 0, 1, 1, 1), true);

            return "hello";
        }
    }
   ```

   <span data-ttu-id="edffb-150">Dabei müssen Sie `com.example.demo` durch den Paketnamen für das Projekt ersetzen.</span><span class="sxs-lookup"><span data-stu-id="edffb-150">Where you will need to replace `com.example.demo` with the package name for your project.</span></span>

1. <span data-ttu-id="edffb-151">Speichern und schließen Sie die Datei *TestController.java*.</span><span class="sxs-lookup"><span data-stu-id="edffb-151">Save and close the *TestController.java* file.</span></span>

1. <span data-ttu-id="edffb-152">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="edffb-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="edffb-153">Testen Sie die Web-App unter http://localhost:8080/sample/hello in einem Webbrowser, oder verwenden Sie die Syntax aus dem folgenden Beispiel (sofern Curl verfügbar ist):</span><span class="sxs-lookup"><span data-stu-id="edffb-153">Test the web app by browsing to http://localhost:8080/sample/hello using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   <span data-ttu-id="edffb-154">Es sollte die Nachricht „hello“</span><span class="sxs-lookup"><span data-stu-id="edffb-154">You should see the "hello!"</span></span> <span data-ttu-id="edffb-155">von Ihrem Beispielcontroller angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="edffb-155">message from your sample controller displayed.</span></span> <span data-ttu-id="edffb-156">Application Insights erfasst diese Anforderung automatisch und sendet sie gemäß Angabe in der Controllerlogik als Telemetrieelement mit dem dazugehörigen benutzerdefinierten Ereignis, der benutzerdefinierten Metrik, der benutzerdefinierten Abhängigkeit und der benutzerdefinierten Ablaufverfolgung.</span><span class="sxs-lookup"><span data-stu-id="edffb-156">Application Insights will automatically collect this request and send it as a telemetry item with it's associated custom event, custom metric, custom dependency and custom trace as specified in the controller logic.</span></span> 

   <span data-ttu-id="edffb-157">Die Daten sollten nach wenigen Sekunden im Azure-Portal angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="edffb-157">After a few seconds you should see the data on Azure portal.</span></span> 

   ![Azure-Portal][AZ05]

   <span data-ttu-id="edffb-159">Sie können auf die Kachel „Anwendungsübersicht“ klicken, um übergeordnete Komponenten und deren Interaktionen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="edffb-159">You can click on Application Map tile to view high level components and their interaction with each other.</span></span> <span data-ttu-id="edffb-160">Hier können Sie sich einen allgemeinen Überblick über die gesamte Anwendung verschaffen.</span><span class="sxs-lookup"><span data-stu-id="edffb-160">This is a recommended place to get a high level overview of entire application.</span></span> <span data-ttu-id="edffb-161">Jeder Spring Boot-Microservice wird anhand des Spring-Anwendungsnamens erkannt.</span><span class="sxs-lookup"><span data-stu-id="edffb-161">Each Spring Boot Microservice is recognized by the spring application name.</span></span> <span data-ttu-id="edffb-162">Vergessen Sie nicht, ihn festzulegen.</span><span class="sxs-lookup"><span data-stu-id="edffb-162">Please remember to set it.</span></span>

   ![Azure-Portal][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a><span data-ttu-id="edffb-164">Konfigurieren der Spring Boot-Anwendung zum Senden von log4j-Protokollen an Application Insights</span><span class="sxs-lookup"><span data-stu-id="edffb-164">Configure Springboot Application to send log4j logs to Application Insights</span></span>

1. <span data-ttu-id="edffb-165">Bearbeiten Sie die Datei „POM.xml“ des Projekts, und fügen Sie den Abschnitt „dependencies“ mit Folgendem hinzu (oder passen Sie ihn entsprechend an).</span><span class="sxs-lookup"><span data-stu-id="edffb-165">Modify the POM.xml file of the project and add/modify the dependencies section with following.</span></span> 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-spring-boot-starter</artifactId>
        <version>1.0.1-BETA</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. <span data-ttu-id="edffb-166">Speichern und schließen Sie die Datei *POM.xml*.</span><span class="sxs-lookup"><span data-stu-id="edffb-166">Save and close the *POM.xml* file.</span></span>

3. <span data-ttu-id="edffb-167">Erstellen Sie im Ordner „\src\main\resources“ eine neue Datei namens *log4j2.xml*, und konfigurieren Sie sie.</span><span class="sxs-lookup"><span data-stu-id="edffb-167">In \src\main\resources folder, create a new file *log4j2.xml* and configure it.</span></span> <span data-ttu-id="edffb-168">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="edffb-168">For example:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Configuration packages="com.microsoft.applicationinsights.log4j.v2">
  <Properties>
    <Property name="LOG_PATTERN">
      %d{yyyy-MM-dd HH:mm:ss.SSS} %5p ${hostName} --- [%15.15t] %-40.40c{1.} : %m%n%ex
    </Property>
  </Properties>
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
    <ApplicationInsightsAppender name="aiAppender">
    </ApplicationInsightsAppender>
  </Appenders>
  <Loggers>
    <Root level="trace">
      <AppenderRef ref="Console"  />
      <AppenderRef ref="aiAppender"  />
    </Root>
  </Loggers>
</Configuration>
```
4. <span data-ttu-id="edffb-169">Erstellen Sie die Spring Boot-Anwendung wie oben gezeigt, und führen Sie sie erneut aus.</span><span class="sxs-lookup"><span data-stu-id="edffb-169">Build and run the Spring Boot application again as shown above.</span></span> 

<span data-ttu-id="edffb-170">Innerhalb weniger Sekunden sollten alle Spring-Protokolle angezeigt werden, die im Azure-Portal verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="edffb-170">Within few seconds, you should see all the spring logs being available on Azure Portal.</span></span> 

![Azure-Portal][AZ06]

<span data-ttu-id="edffb-172">Sie können sich sogar die ausführlichen Protokollmeldungen ansehen und Analysen im Analytics-Portal durchführen.</span><span class="sxs-lookup"><span data-stu-id="edffb-172">You can even look at the detailed log messages and do analysis on Analytics Portal.</span></span> 

![Azure-Portal][AZ07]

## <a name="next-steps"></a><span data-ttu-id="edffb-174">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="edffb-174">Next steps</span></span>

<span data-ttu-id="edffb-175">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="edffb-175">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="edffb-176">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="edffb-176">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="edffb-177">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="edffb-177">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="edffb-178">Application Insights unterstützt die automatische Erfassung externer Abhängigkeiten und deren Korrelation mit eingehenden Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="edffb-178">Application Insights supports automatic collection of external dependencies and its correlation with incoming requests.</span></span> <span data-ttu-id="edffb-179">Aktuell wird die automatische Erfassung von Oracle, MsSQL, MySQL und Redis unterstützt.</span><span class="sxs-lookup"><span data-stu-id="edffb-179">Currently we support autocollection of Oracle, MsSQL, MySQL and Redis.</span></span> <span data-ttu-id="edffb-180">Weitere Informationen zum Aktivieren der automatischen Erfassung finden Sie im Artikel [Überwachen von Abhängigkeiten, abgefangene Ausnahmen und Methodenausführungszeiten in Java-Web-Apps](https://docs.microsoft.com/azure/application-insights/app-insights-java-agent).</span><span class="sxs-lookup"><span data-stu-id="edffb-180">For more details on enabling autocollection please follow the article [how to use Application Insights Java agent](https://docs.microsoft.com/azure/application-insights/app-insights-java-agent).</span></span>

<span data-ttu-id="edffb-181">Weitere Informationen zu Azure Application Insights und den verfügbaren Überwachungsfunktionen finden Sie unter **[Application Insights]**.</span><span class="sxs-lookup"><span data-stu-id="edffb-181">For more information about Azure Application Insights, and it's monitoring capabilities, see the **[Application Insights]** home page.</span></span>

<span data-ttu-id="edffb-182">Weitere Informationen zu weiteren Konfigurationsdetails von Application Insights Spring Boot Starter finden Sie [hier](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="edffb-182">For more information about additional configuration details of Application Insights Spring Boot Starter, please refer to this [link](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

<span data-ttu-id="edffb-183">Wenn Sie Funktionen anfragen oder potenzielle Fehler melden möchten, stellen Sie bitte eine entsprechende Anfrage über unser [GitHub-Repository](https://github.com/Microsoft/ApplicationInsights-Java/issues).</span><span class="sxs-lookup"><span data-stu-id="edffb-183">For feature requests and potential bugs, please open issues on our [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues) repository.</span></span>

<span data-ttu-id="edffb-184">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="edffb-184">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="edffb-185">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="edffb-185">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="edffb-186">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="edffb-186">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="edffb-187">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter [https://github.com/spring-guides/](https://github.com/spring-guides/) mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="edffb-187">To help developers get started with Spring Boot, several sample Spring Boot packages are available at [https://github.com/spring-guides/](https://github.com/spring-guides/).</span></span> <span data-ttu-id="edffb-188">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="edffb-188">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

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
[Spezifische Eigenschaften für Spring Boot-Profile]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Boot Profile Specific Properties]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: https://docs.microsoft.com/azure/application-insights/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_2.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_3.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Get_IKey.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/OverviewBladeResults.png
[AZ06]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Search_and_traces.png
[AZ07]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/traces_details.png
[AZ08]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/AppMap.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/spring_start.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/After_extract.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationproperties_loc.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationinsightsproperties.png
