---
title: Bereitstellen einer Spring Boot-App mit JAR-Datei in der Cloud mit Maven und Azure
description: Hier erfahren Sie, wie Sie eine Spring Boot-App mithilfe des Maven-Plug-Ins für Azure-Web-Apps für Linux in der Cloud bereitstellen.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.author: robmcm
ms.date: 10/18/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: dc3038fed6859203f36e0c4dc9a9b01e81a7c4c5
ms.sourcegitcommit: dae7511a9d93ca7f388d5b0e05dc098e22c2f2f6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2018
ms.locfileid: "49962494"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="c61af-103">Bereitstellen einer Spring Boot-App mit JAR-Datei in Azure App Service unter Linux</span><span class="sxs-lookup"><span data-stu-id="c61af-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="c61af-104">In diesem Artikel wird veranschaulicht, wie Sie mithilfe des [Maven-Plug-Ins für Azure App Service-Web-Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) eine Spring Boot-Anwendung als Java SE-JAR-Paket in [Azure App Service unter Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c61af-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/).</span></span> <span data-ttu-id="c61af-105">Wählen Sie eine Java SE-Bereitstellung über [Tomcat- und WAR-Dateien](/azure/app-service/containers/quickstart-java), wenn Sie die Abhängigkeiten, Runtime und Konfiguration Ihrer App in einem einzigen bereitstellbaren Artefakt zusammenfassen möchten.</span><span class="sxs-lookup"><span data-stu-id="c61af-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's dependencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="c61af-106">Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.</span><span class="sxs-lookup"><span data-stu-id="c61af-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c61af-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c61af-107">Prerequisites</span></span>

<span data-ttu-id="c61af-108">Zur Durchführung der Schritte in diesem Tutorial müssen die folgenden Komponenten installiert und konfiguriert sein:</span><span class="sxs-lookup"><span data-stu-id="c61af-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="c61af-109">Die [Azure CLI](/cli/azure/), entweder lokal oder über [Azure Cloud Shell](https://shell.azure.com)</span><span class="sxs-lookup"><span data-stu-id="c61af-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="c61af-110">[Java Development Kit (JDK)](https://www.azul.com/downloads/azure-only/zulu/), mindestens Version 1.7</span><span class="sxs-lookup"><span data-stu-id="c61af-110">[Java Development Kit (JDK)](https://www.azul.com/downloads/azure-only/zulu/), version 1.7 or later.</span></span>
* <span data-ttu-id="c61af-111">[Maven](https://maven.apache.org/) von Apache, Version 3)</span><span class="sxs-lookup"><span data-stu-id="c61af-111">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="c61af-112">Einen [Git-Client](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="c61af-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="install-and-sign-in-to-azure-cli"></a><span data-ttu-id="c61af-113">Installieren der Azure CLI und Anmelden bei der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c61af-113">Install and sign in to Azure CLI</span></span>

<span data-ttu-id="c61af-114">Bei Verwendung des Maven-Plug-Ins lässt sich die Spring Boot-Anwendung am einfachsten und komfortabelsten über die [Azure CLI](https://docs.microsoft.com/cli/azure/) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c61af-114">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span>

<span data-ttu-id="c61af-115">Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="c61af-115">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
<span data-ttu-id="c61af-116">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="c61af-116">Follow the instructions to complete the sign-in process.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="c61af-117">Klonen der Beispiel-App</span><span class="sxs-lookup"><span data-stu-id="c61af-117">Clone the sample app</span></span>

<span data-ttu-id="c61af-118">In diesem Abschnitt klonen Sie eine vollständige Spring Boot-Anwendung und testen sie lokal.</span><span class="sxs-lookup"><span data-stu-id="c61af-118">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="c61af-119">Öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Spring Boot-Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c61af-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c61af-120">– oder –</span><span class="sxs-lookup"><span data-stu-id="c61af-120">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="c61af-121">Klonen Sie das Beispielprojekt [Spring Boot Getting Started] in das Verzeichnis, das Sie erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c61af-121">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="c61af-122">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c61af-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="c61af-123">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c61af-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c61af-124">Starten Sie die Web-App nach der Erstellung mithilfe von Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c61af-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c61af-125">Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="c61af-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="c61af-126">Sie können beispielsweise den folgenden Befehl verwenden, wenn curl verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="c61af-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c61af-127">Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.</span><span class="sxs-lookup"><span data-stu-id="c61af-127">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="c61af-128">Konfigurieren des Maven-Plug-Ins für Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c61af-128">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="c61af-129">In diesem Abschnitt konfigurieren Sie das Spring Boot-Projekt `pom.xml` so, dass Maven die App in Azure App Service unter Linux bereitstellen kann.</span><span class="sxs-lookup"><span data-stu-id="c61af-129">In this section, you will configure the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="c61af-130">Öffnen Sie `pom.xml` in einem Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="c61af-130">Open `pom.xml` in a code editor.</span></span>

2. <span data-ttu-id="c61af-131">Fügen Sie im `<build>`-Abschnitt der Datei „pom.xml“ den folgenden `<plugin>`-Eintrag innerhalb des `<plugins>`-Tag hinzu.</span><span class="sxs-lookup"><span data-stu-id="c61af-131">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
   </plugin>
   ```

3. <span data-ttu-id="c61af-132">Aktualisieren Sie die folgenden Platzhalter in der Plug-In-Konfiguration:</span><span class="sxs-lookup"><span data-stu-id="c61af-132">Update the following placeholders in the plugin configuration:</span></span>

| <span data-ttu-id="c61af-133">Platzhalter</span><span class="sxs-lookup"><span data-stu-id="c61af-133">Placeholder</span></span> | <span data-ttu-id="c61af-134">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c61af-134">Description</span></span> |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | <span data-ttu-id="c61af-135">Der Name der neuen Ressourcengruppe, in der Ihre Web-App erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="c61af-135">Name for the new resource group in which to create your web app.</span></span> <span data-ttu-id="c61af-136">Indem Sie alle Ressourcen für eine App in einer Gruppe zusammenfassen, können Sie sie zusammen verwalten.</span><span class="sxs-lookup"><span data-stu-id="c61af-136">By putting all the resources for an app in a group, you can manage them together.</span></span> <span data-ttu-id="c61af-137">Wenn Sie beispielsweise die Ressourcengruppe löschen, werden alle Ressourcen gelöscht, die der App zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="c61af-137">For example, deleting the resource group would delete all resources associated with the app.</span></span> <span data-ttu-id="c61af-138">Aktualisieren Sie diesen Wert mit einem neuen eindeutigen Ressourcengruppennamen, z.B. *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="c61af-138">Update this value with a unique new resource group name, for example, *TestResources*.</span></span> <span data-ttu-id="c61af-139">In einem Abschnitt weiter unten verwenden Sie diesen Ressourcengruppennamen zum Bereinigen aller Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="c61af-139">You will use this resource group name to clean up all Azure resources in a later section.</span></span> |
| `WEBAPP_NAME` | <span data-ttu-id="c61af-140">Der App-Name wird bei der Bereitstellung in Azure als Teil des Hostnamens für die Web-App (WEBAPP_NAME.azurewebsites.net) verwendet.</span><span class="sxs-lookup"><span data-stu-id="c61af-140">The app name will be part the host name for the web app when deployed to Azure (WEBAPP_NAME.azurewebsites.net).</span></span> <span data-ttu-id="c61af-141">Aktualisieren Sie diesen Wert mit einem eindeutigen Namen für die neue Azure-Web-App, die Ihre Java-App hostet (z.B. *contoso*).</span><span class="sxs-lookup"><span data-stu-id="c61af-141">Update this value with a unique name for the new Azure web app, which will host your Java app, for example *contoso*.</span></span> |
| `REGION` | <span data-ttu-id="c61af-142">Eine Azure-Region, in der die Web-App gehostet wird, z. B. `westus2`.</span><span class="sxs-lookup"><span data-stu-id="c61af-142">An Azure region where the web app is hosted, for example `westus2`.</span></span> <span data-ttu-id="c61af-143">Sie können eine Liste von Regionen über die Cloud Shell oder CLI mit dem Befehl `az account list-locations` abrufen.</span><span class="sxs-lookup"><span data-stu-id="c61af-143">You can get a list of regions from the Cloud Shell or CLI using the `az account list-locations` command.</span></span> |

<span data-ttu-id="c61af-144">Eine vollständige Liste der Konfigurationsoptionen finden Sie der [Referenz zum Maven-Plug-In auf GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="c61af-144">A full list of configuration options can be found in the [Maven plugin reference on GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span></span>

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="c61af-145">Bereitstellen der Anwendung in Azure</span><span class="sxs-lookup"><span data-stu-id="c61af-145">Deploy the app to Azure</span></span>

<span data-ttu-id="c61af-146">Nachdem Sie alle Einstellungen in den vorhergehenden Abschnitten in diesem Artikel konfiguriert haben, können Sie Ihre Web-App in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c61af-146">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="c61af-147">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="c61af-147">To do so, use the following steps:</span></span>

1. <span data-ttu-id="c61af-148">Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c61af-148">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c61af-149">Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c61af-149">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="c61af-150">Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App oder der Web-App-Plan noch nicht vorhanden ist, wird sie bzw. er erstellt.</span><span class="sxs-lookup"><span data-stu-id="c61af-150">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="c61af-151">Wenn Ihre Web-App bereitgestellt wurde, können Sie sie über das [Azure-Portal] verwalten.</span><span class="sxs-lookup"><span data-stu-id="c61af-151">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="c61af-152">Ihre Web-App wird unter **App Services** aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="c61af-152">Your web app will be listed in **App Services**:</span></span>

   ![Im Azure-Portal unter „App Services“ aufgeführte Web-App][AP01]

* <span data-ttu-id="c61af-154">Die URL für Ihre Web-App wird in der **Übersicht** für Ihre Web-App aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="c61af-154">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Festlegen der URL für Ihre Web-App][AP02]

<span data-ttu-id="c61af-156">Stellen Sie mit dem gleichen cURL-Befehl wie zuvor sicher, dass die Bereitstellung erfolgreich war. Verwenden Sie dabei die URL Ihrer Web-App aus dem Portal anstelle von `localhost`.</span><span class="sxs-lookup"><span data-stu-id="c61af-156">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="c61af-157">Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.</span><span class="sxs-lookup"><span data-stu-id="c61af-157">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c61af-158">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c61af-158">Next steps</span></span>

<span data-ttu-id="c61af-159">Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="c61af-159">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="c61af-160">[Maven Plugin for Azure Web Apps] (Maven-Plug-In für Azure-Web-Apps)</span><span class="sxs-lookup"><span data-stu-id="c61af-160">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="c61af-161">Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="c61af-161">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="c61af-162">Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c61af-162">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* <span data-ttu-id="c61af-163">[Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)</span><span class="sxs-lookup"><span data-stu-id="c61af-163">[Maven Settings Reference](https://maven.apache.org/settings.html)</span></span>

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure-Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme (Maven-Plug-In für Azure-Web-Apps)

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
