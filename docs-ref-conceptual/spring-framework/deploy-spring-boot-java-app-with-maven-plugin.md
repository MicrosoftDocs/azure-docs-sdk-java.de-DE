---
title: Bereitstellen einer Spring Boot-App mit JAR-Datei in der Cloud mit Maven und Azure
description: Hier erfahren Sie, wie Sie eine Spring Boot-App mithilfe des Maven-Plug-Ins für Azure-Web-Apps für Linux in der Cloud bereitstellen.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: b133290d1f14429cbf36d6ed5a67d27e1a637593
ms.sourcegitcommit: 599405a9ce892d75073ef0776befa2fa22407b4c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2019
ms.locfileid: "67237601"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="8941d-103">Bereitstellen einer Spring Boot-App mit JAR-Datei in Azure App Service unter Linux</span><span class="sxs-lookup"><span data-stu-id="8941d-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="8941d-104">In diesem Artikel wird veranschaulicht, wie Sie mithilfe des [Maven-Plug-Ins für Azure App Service-Web-Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) eine Spring Boot-Anwendung als Java SE-JAR-Paket in [Azure App Service unter Linux](/azure/app-service/containers/) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="8941d-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](/azure/app-service/containers/).</span></span> <span data-ttu-id="8941d-105">Wählen Sie eine Java SE-Bereitstellung über [Tomcat- und WAR-Dateien](/azure/app-service/containers/quickstart-java), wenn Sie die Abhängigkeiten, Runtime und Konfiguration Ihrer App in einem einzigen bereitstellbaren Artefakt zusammenfassen möchten.</span><span class="sxs-lookup"><span data-stu-id="8941d-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's dependencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="8941d-106">Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.</span><span class="sxs-lookup"><span data-stu-id="8941d-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8941d-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="8941d-107">Prerequisites</span></span>

<span data-ttu-id="8941d-108">Zur Durchführung der Schritte in diesem Tutorial müssen die folgenden Komponenten installiert und konfiguriert sein:</span><span class="sxs-lookup"><span data-stu-id="8941d-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="8941d-109">Die [Azure CLI](/cli/azure/), entweder lokal oder über [Azure Cloud Shell](https://shell.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8941d-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="8941d-110">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="8941d-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="8941d-111">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="8941d-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="8941d-112">[Maven](https://maven.apache.org/) von Apache, Version 3)</span><span class="sxs-lookup"><span data-stu-id="8941d-112">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="8941d-113">Einen [Git-Client](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="8941d-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="install-and-sign-in-to-azure-cli"></a><span data-ttu-id="8941d-114">Installieren der Azure CLI und Anmelden bei der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8941d-114">Install and sign in to Azure CLI</span></span>

<span data-ttu-id="8941d-115">Bei Verwendung des Maven-Plug-Ins lässt sich die Spring Boot-Anwendung am einfachsten und komfortabelsten über die [Azure CLI](/cli/azure/) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="8941d-115">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](/cli/azure/).</span></span>

<span data-ttu-id="8941d-116">Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="8941d-116">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
<span data-ttu-id="8941d-117">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="8941d-117">Follow the instructions to complete the sign-in process.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="8941d-118">Klonen der Beispiel-App</span><span class="sxs-lookup"><span data-stu-id="8941d-118">Clone the sample app</span></span>

<span data-ttu-id="8941d-119">In diesem Abschnitt klonen Sie eine vollständige Spring Boot-Anwendung und testen sie lokal.</span><span class="sxs-lookup"><span data-stu-id="8941d-119">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="8941d-120">Öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Spring Boot-Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8941d-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="8941d-121">– oder –</span><span class="sxs-lookup"><span data-stu-id="8941d-121">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="8941d-122">Klonen Sie das Beispielprojekt [Spring Boot Getting Started] in das Verzeichnis, das Sie erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8941d-122">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="8941d-123">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8941d-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="8941d-124">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8941d-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="8941d-125">Starten Sie die Web-App nach der Erstellung mithilfe von Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8941d-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="8941d-126">Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="8941d-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="8941d-127">Sie können beispielsweise den folgenden Befehl verwenden, wenn curl verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="8941d-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="8941d-128">Die folgende Meldung sollte angezeigt werden: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="8941d-128">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="8941d-129">Konfigurieren des Maven-Plug-Ins für Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8941d-129">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="8941d-130">In diesem Abschnitt konfigurieren Sie das Spring Boot-Projekt `pom.xml` so, dass Maven die App in Azure App Service unter Linux bereitstellen kann.</span><span class="sxs-lookup"><span data-stu-id="8941d-130">In this section, you will configure the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="8941d-131">Öffnen Sie `pom.xml` in einem Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="8941d-131">Open `pom.xml` in a code editor.</span></span>

2. <span data-ttu-id="8941d-132">Fügen Sie im `<build>`-Abschnitt der Datei „pom.xml“ den folgenden `<plugin>`-Eintrag innerhalb des `<plugins>`-Tag hinzu.</span><span class="sxs-lookup"><span data-stu-id="8941d-132">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.6.0</version>
   </plugin>
   ```

3. <span data-ttu-id="8941d-133">Anschließend können Sie die Bereitstellung konfigurieren, den maven-Befehl `mvn azure-webapp:config` an der Eingabeaufforderung ausführen und mithilfe der **Nummer** die folgenden Optionen in der Aufforderung auswählen:</span><span class="sxs-lookup"><span data-stu-id="8941d-133">Then you can configure the deployment, run the maven command `mvn azure-webapp:config` in the Command Prompt and use the **number** to choose these options in the prompt:</span></span>
    * <span data-ttu-id="8941d-134">**OS**: linux</span><span class="sxs-lookup"><span data-stu-id="8941d-134">**OS**: linux</span></span>  
    * <span data-ttu-id="8941d-135">**javaVersion**: jre8</span><span class="sxs-lookup"><span data-stu-id="8941d-135">**javaVersion**: jre8</span></span>
    * <span data-ttu-id="8941d-136">**runtimeStack**: jre8</span><span class="sxs-lookup"><span data-stu-id="8941d-136">**runtimeStack**: jre8</span></span>

<span data-ttu-id="8941d-137">Wenn die Aufforderung **Confirm (Y/N)** (Bestätigen (J/N)) angezeigt wird, drücken Sie **Y**, und die Konfiguration ist abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="8941d-137">When you get the **Confirm (Y/N)** prompt, press **'y'** and the configuration is done.</span></span>

```cmd
~@Azure:~/gs-spring-boot/complete$ mvn azure-webapp:config
[INFO] Scanning for projects...
[INFO]
[INFO] -----------------< org.springframework:gs-spring-boot >-----------------
[INFO] Building gs-spring-boot 0.1.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- azure-webapp-maven-plugin:1.6.0:config (default-cli) @ gs-spring-boot ---
[WARNING] The plugin may not work if you change the os of an existing webapp.
Define value for OS(Default: Linux):
1. linux [*]
2. windows
3. docker
Enter index to use:
Define value for javaVersion(Default: jre8):
1. jre8 [*]
2. java11
Enter index to use:
Define value for runtimeStack(Default: TOMCAT 8.5):
1. TOMCAT 9.0
2. jre8
3. TOMCAT 8.5 [*]
4. WILDFLY 14
Enter index to use: 2
Please confirm webapp properties
AppName : gs-spring-boot-1559091271202
ResourceGroup : gs-spring-boot-1559091271202-rg
Region : westeurope
PricingTier : Premium_P1V2
OS : Linux
RuntimeStack : JAVA 8-jre8
Deploy to slot : false
Confirm (Y/N)? : Y
```

4. <span data-ttu-id="8941d-138">Fügen Sie dem Abschnitt `<configuration>` von `<azure-webapp-maven-plugin>` den Abschnitt `<appSettings>` hinzu, um an Port *80* zu lauschen.</span><span class="sxs-lookup"><span data-stu-id="8941d-138">Add the `<appSettings>` section to the `<configuration>` section of `<azure-webapp-maven-plugin>` to listen on the *80* port.</span></span>

    ```xml
   <plugin>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-webapp-maven-plugin</artifactId>
       <version>1.6.0</version>
       <configuration>
          <schemaVersion>V2</schemaVersion>
          <resourceGroup>gs-spring-boot-1559091271202-rg</resourceGroup>
          <appName>gs-spring-boot-1559091271202</appName>
          <region>westeurope</region>
          <pricingTier>P1V2</pricingTier>

          <!-- Begin of App Settings  -->
          <appSettings>
             <property>
                   <name>JAVA_OPTS</name>
                   <value>-Dserver.port=80</value>
             </property>
          </appSettings>
          <!-- End of App Settings  -->
          ...
         </configuration>
   </plugin>
   ```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="8941d-139">Bereitstellen der Anwendung in Azure</span><span class="sxs-lookup"><span data-stu-id="8941d-139">Deploy the app to Azure</span></span>

<span data-ttu-id="8941d-140">Nachdem Sie alle Einstellungen in den vorhergehenden Abschnitten in diesem Artikel konfiguriert haben, können Sie Ihre Web-App in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="8941d-140">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="8941d-141">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="8941d-141">To do so, use the following steps:</span></span>

1. <span data-ttu-id="8941d-142">Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8941d-142">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="8941d-143">Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8941d-143">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="8941d-144">Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App oder der Web-App-Plan noch nicht vorhanden ist, wird sie bzw. er erstellt.</span><span class="sxs-lookup"><span data-stu-id="8941d-144">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="8941d-145">Wenn Ihre Web-App bereitgestellt wurde, können Sie sie über das [Azure-Portal] verwalten.</span><span class="sxs-lookup"><span data-stu-id="8941d-145">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="8941d-146">Ihre Web-App wird unter **App Services** aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="8941d-146">Your web app will be listed in **App Services**:</span></span>

   ![Im Azure-Portal unter „App Services“ aufgeführte Web-App][AP01]

* <span data-ttu-id="8941d-148">Die URL für Ihre Web-App wird in der **Übersicht** für Ihre Web-App aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="8941d-148">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Festlegen der URL für Ihre Web-App][AP02]

<span data-ttu-id="8941d-150">Stellen Sie mit dem gleichen cURL-Befehl wie zuvor sicher, dass die Bereitstellung erfolgreich war. Verwenden Sie dabei die URL Ihrer Web-App aus dem Portal anstelle von `localhost`.</span><span class="sxs-lookup"><span data-stu-id="8941d-150">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="8941d-151">Die folgende Meldung sollte angezeigt werden: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="8941d-151">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8941d-152">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="8941d-152">Next steps</span></span>

<span data-ttu-id="8941d-153">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="8941d-153">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8941d-154">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="8941d-154">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="8941d-155">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="8941d-155">Additional Resources</span></span>

<span data-ttu-id="8941d-156">Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="8941d-156">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="8941d-157">[Maven Plugin for Azure Web Apps] (Maven-Plug-In für Azure-Web-Apps)</span><span class="sxs-lookup"><span data-stu-id="8941d-157">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="8941d-158">Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="8941d-158">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="8941d-159">Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8941d-159">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* <span data-ttu-id="8941d-160">[Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)</span><span class="sxs-lookup"><span data-stu-id="8941d-160">[Maven Settings Reference](https://maven.apache.org/settings.html)</span></span>

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[Azure-Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven Plugin for Azure Web Apps]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme (Maven-Plug-In für Azure-Web-Apps)

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
