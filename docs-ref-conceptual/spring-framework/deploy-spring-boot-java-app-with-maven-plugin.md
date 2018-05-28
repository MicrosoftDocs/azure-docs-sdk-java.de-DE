---
title: Bereitstellen einer Spring Boot-App in der Cloud mit Maven und Azure
description: Hier erfahren Sie, wie Sie eine Spring Boot-App mithilfe des Maven-Plug-Ins für Azure-Web-Apps in der Cloud bereitstellen.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 82cb0da3ce49fa77f888808af14455bf226d5cb0
ms.sourcegitcommit: 024b3127daf396a17bd43d57642e3534ae87f120
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/23/2018
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-web-apps"></a><span data-ttu-id="0d048-103">Bereitstellen einer Spring Boot-App in der Cloud mithilfe des Maven-Plug-Ins für Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="0d048-103">Deploy a Spring Boot app to the cloud using the Maven Plugin for Azure Web Apps</span></span>

<span data-ttu-id="0d048-104">In diesem Artikel wird veranschaulicht, wie Sie mithilfe des Maven-Plug-Ins für Azure-Web-Apps eine Spring Boot-Beispielanwendung in Azure App Services bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="0d048-104">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application to Azure App Services.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="0d048-105">Das [Maven-Plug-In für Azure-Web-Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) für [Apache Maven](http://maven.apache.org/) ermöglicht die nahtlose Integration von Azure App Service in Maven-Projekte und optimiert für Entwickler den Bereitstellungsprozess für Web-Apps in Azure App Service .</span><span class="sxs-lookup"><span data-stu-id="0d048-105">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="0d048-106">Das Maven-Plug-In für Azure-Web-Apps ist derzeit als Vorschauversion verfügbar.</span><span class="sxs-lookup"><span data-stu-id="0d048-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="0d048-107">Zur Zeit wird nur FTP-Veröffentlichung unterstützt. Für die Zukunft sind jedoch weitere Features geplant.</span><span class="sxs-lookup"><span data-stu-id="0d048-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="0d048-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="0d048-108">Prerequisites</span></span>

<span data-ttu-id="0d048-109">Zur Durchführung der Schritte in diesem Tutorial benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="0d048-109">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="0d048-110">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="0d048-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="0d048-111">Die [Azure-Befehlszeilenschnittstelle (CLI)]</span><span class="sxs-lookup"><span data-stu-id="0d048-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="0d048-112">Ein aktuelles [Java Development Kit (JDK)], Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="0d048-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="0d048-113">Das Erstellungstool Apache [Maven] (Version 3)</span><span class="sxs-lookup"><span data-stu-id="0d048-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="0d048-114">Einen [Git]</span><span class="sxs-lookup"><span data-stu-id="0d048-114">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="0d048-115">Klonen der Beispiel-Web-App für Spring Boot</span><span class="sxs-lookup"><span data-stu-id="0d048-115">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="0d048-116">In diesem Abschnitt klonen Sie eine vollständige Spring Boot-Anwendung und testen sie lokal.</span><span class="sxs-lookup"><span data-stu-id="0d048-116">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="0d048-117">Öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, erstellen Sie ein lokales Verzeichnis zum Speichern Ihrer Spring Boot-Anwendung, und wechseln Sie in dieses Verzeichnis. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="0d048-117">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="0d048-118">– oder –</span><span class="sxs-lookup"><span data-stu-id="0d048-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="0d048-119">Klonen Sie das Beispielprojekt [Spring Boot Getting Started] in das Verzeichnis, das Sie erstellt haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="0d048-119">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="0d048-120">Wechseln Sie in das Verzeichnis mit dem abgeschlossenen Projekt. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="0d048-120">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="0d048-121">Erstellen Sie die JAR-Datei mit Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="0d048-121">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="0d048-122">Starten Sie die Web-App nach der Erstellung mithilfe von Maven. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="0d048-122">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="0d048-123">Testen Sie die Web-App, indem Sie sie lokal mit einem Webbrowser durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="0d048-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="0d048-124">Sie können beispielsweise den folgenden Befehl verwenden, wenn curl verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="0d048-124">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="0d048-125">Daraufhin sollte die folgende Meldung angezeigt werden: **Greetings from Spring Boot!**.</span><span class="sxs-lookup"><span data-stu-id="0d048-125">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="0d048-126">Erstellen eines Azure-Dienstprinzipals</span><span class="sxs-lookup"><span data-stu-id="0d048-126">Create an Azure service principal</span></span>

<span data-ttu-id="0d048-127">In diesem Abschnitt erstellen Sie einen Azure-Dienstprinzipal, den das Maven-Plug-In beim Bereitstellen der Web-App in Azure verwendet.</span><span class="sxs-lookup"><span data-stu-id="0d048-127">In this section, you will create an Azure service principal that the Maven plugin uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="0d048-128">Öffnen Sie eine Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="0d048-128">Open a command prompt.</span></span>

1. <span data-ttu-id="0d048-129">Melden Sie sich mithilfe der Azure CLI bei Ihrem Azure-Konto an:</span><span class="sxs-lookup"><span data-stu-id="0d048-129">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="0d048-130">Folgen Sie den Anweisungen, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="0d048-130">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="0d048-131">Erstellen Sie einen Azure-Dienstprinzipal:</span><span class="sxs-lookup"><span data-stu-id="0d048-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="0d048-132">Dabei ist `uuuuuuuu` der Benutzername und `pppppppp` das Kennwort für den Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="0d048-132">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="0d048-133">Azure antwortet mit JSON-Code, der etwa wie folgendes Beispiel aussieht:</span><span class="sxs-lookup"><span data-stu-id="0d048-133">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="0d048-134">Sie verwenden die Werte aus dieser JSON-Antwort, wenn Sie das Maven-Plug-In für die Bereitstellung der Web-App in Azure konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="0d048-134">You will use the values from this JSON response when you configure the Maven plugin to deploy your web app to Azure.</span></span> <span data-ttu-id="0d048-135">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` und `tttttttt` sind Platzhalterwerte. Sie werden in diesem Beispiel dazu verwendet, die Zuordnung der Werte zu ihren entsprechenden Elementen zu vereinfachen, wenn Sie die Maven-Datei `settings.xml` im nächsten Abschnitt konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="0d048-135">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="0d048-136">Konfigurieren von Maven zur Verwendung des Azure-Dienstprinzipals</span><span class="sxs-lookup"><span data-stu-id="0d048-136">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="0d048-137">In diesem Abschnitt verwenden Sie die Werte Ihres Azure-Dienstprinzipals zum Konfigurieren der Authentifizierung, die Maven bei der Bereitstellung Ihrer Web-App in Azure verwendet.</span><span class="sxs-lookup"><span data-stu-id="0d048-137">In this section, you will use the values from your Azure service principal to configure the authentication that Maven uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="0d048-138">Öffnen Sie die Maven-Datei `settings.xml` in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="0d048-138">Open your Maven `settings.xml` file in a text editor.</span></span> <span data-ttu-id="0d048-139">Diese Datei befindet sich unter Umständen an einem Pfad wie in den folgenden Beispielen:</span><span class="sxs-lookup"><span data-stu-id="0d048-139">This file may be in a path similar to the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="0d048-140">Fügen Sie Ihre Azure-Dienstprinzipaleinstellungen aus dem vorherigen Abschnitt dieses Tutorials zur Auflistung `<servers>` in der Datei *settings.xml* hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="0d048-140">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="0d048-141">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="0d048-141">Where:</span></span>
   | <span data-ttu-id="0d048-142">Element</span><span class="sxs-lookup"><span data-stu-id="0d048-142">Element</span></span> | <span data-ttu-id="0d048-143">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="0d048-143">Description</span></span> |
   |---|---|
   | `<id>` | <span data-ttu-id="0d048-144">Gibt einen eindeutigen Namen an, mit dem Maven Ihre Sicherheitseinstellungen abruft, wenn Sie die Web-App in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="0d048-144">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span> |
   | `<client>` | <span data-ttu-id="0d048-145">Enthält den Wert `appId` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="0d048-145">Contains the `appId` value from your service principal.</span></span> |
   | `<tenant>` | <span data-ttu-id="0d048-146">Enthält den Wert `tenant` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="0d048-146">Contains the `tenant` value from your service principal.</span></span> |
   | `<key>` | <span data-ttu-id="0d048-147">Enthält den Wert `password` aus dem Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="0d048-147">Contains the `password` value from your service principal.</span></span> |
   | `<environment>` | <span data-ttu-id="0d048-148">Definiert die Azure-Zielcloudumgebung (in diesem Beispiel: `AZURE`).</span><span class="sxs-lookup"><span data-stu-id="0d048-148">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="0d048-149">(Eine vollständige Liste der Umgebungen finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)</span><span class="sxs-lookup"><span data-stu-id="0d048-149">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |

1. <span data-ttu-id="0d048-150">Speichern und schließen Sie die Datei *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="0d048-150">Save and close the *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a><span data-ttu-id="0d048-151">OPTIONAL: Anpassen der Datei „pom.xml“ vor der Bereitstellung der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="0d048-151">OPTIONAL: Customize your pom.xml before deploying your web app to Azure</span></span>

<span data-ttu-id="0d048-152">Öffnen Sie die Datei `pom.xml` für Ihre Spring Boot-Anwendung in einem Text-Editor, und suchen Sie das Element `<plugin>` für `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="0d048-152">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="0d048-153">Dieses Element sollte etwa wie folgendes Beispiel aussehen:</span><span class="sxs-lookup"><span data-stu-id="0d048-153">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="0d048-154">Für das Maven-Plug-In können mehrere Werte angepasst werden. Eine ausführliche Beschreibung der einzelnen Elemente finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].</span><span class="sxs-lookup"><span data-stu-id="0d048-154">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="0d048-155">Für diesen Artikel sind jedoch besonders folgende Werte hervorzuheben:</span><span class="sxs-lookup"><span data-stu-id="0d048-155">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="0d048-156">Element</span><span class="sxs-lookup"><span data-stu-id="0d048-156">Element</span></span> | <span data-ttu-id="0d048-157">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="0d048-157">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="0d048-158">Gibt die Version des [Maven-Plug-In für Azure-Web-Apps] an.</span><span class="sxs-lookup"><span data-stu-id="0d048-158">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="0d048-159">Überprüfen Sie die im [zentralen Maven-Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) angegebene Version, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="0d048-159">Verify the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="0d048-160">Gibt die Authentifizierungsinformationen für Azure an, die in diesem Beispiel ein `<serverId>`-Element enthalten, das `azure-auth` enthält. Maven nutzt diesen Wert, um die Azure-Dienstprinzipalwerte in Ihrer Maven-Datei *settings.xml* abzurufen, die Sie weiter oben in diesem Artikel festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="0d048-160">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="0d048-161">Gibt die Zielressourcengruppe an (in diesem Beispiel: `maven-plugin`).</span><span class="sxs-lookup"><span data-stu-id="0d048-161">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="0d048-162">Wenn die Ressourcengruppe nicht bereits vorhanden ist, wird sie während der Bereitstellung erstellt.</span><span class="sxs-lookup"><span data-stu-id="0d048-162">The resource group is created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="0d048-163">Gibt den Zielnamen für Ihre Web-App an.</span><span class="sxs-lookup"><span data-stu-id="0d048-163">Specifies the target name for your web app.</span></span> <span data-ttu-id="0d048-164">In diesem Beispiel lautet der Zielname `maven-web-app-${maven.build.timestamp}`. Dabei wird das Suffix `${maven.build.timestamp}` angehängt, um Konflikte zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="0d048-164">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="0d048-165">(Der Zeitstempel ist optional. Sie können eine beliebige eindeutige Zeichenfolge für den App-Namen angeben.)</span><span class="sxs-lookup"><span data-stu-id="0d048-165">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="0d048-166">Gibt die Zielregion an (in diesem Beispiel: `westus`).</span><span class="sxs-lookup"><span data-stu-id="0d048-166">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="0d048-167">(Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)</span><span class="sxs-lookup"><span data-stu-id="0d048-167">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<javaVersion>` | <span data-ttu-id="0d048-168">Gibt die Java Runtime-Version für Ihre Web-App an.</span><span class="sxs-lookup"><span data-stu-id="0d048-168">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="0d048-169">(Eine vollständige Liste finden Sie in der Dokumentation zum [Maven-Plug-In für Azure-Web-Apps].)</span><span class="sxs-lookup"><span data-stu-id="0d048-169">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<deploymentType>` | <span data-ttu-id="0d048-170">Gibt den Bereitstellungstyp für Ihre Web-App an.</span><span class="sxs-lookup"><span data-stu-id="0d048-170">Specifies deployment type for your web app.</span></span> <span data-ttu-id="0d048-171">Derzeit wird nur `ftp` unterstützt. An der Unterstützung anderer Bereitstellungstypen wird jedoch bereits gearbeitet.</span><span class="sxs-lookup"><span data-stu-id="0d048-171">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span> |
| `<resources>` | <span data-ttu-id="0d048-172">Gibt Ressourcen und Ziele an, die von Maven bei der Bereitstellung Ihrer Web-App in Azure verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="0d048-172">Specifies resources and target destinations which Maven uses when deploying your web app to Azure.</span></span> <span data-ttu-id="0d048-173">In diesem Beispiel geben zwei `<resource>`-Elemente an, dass Maven die JAR-Datei für Ihre Web-App und die Datei *web.config* aus dem Spring Boot-Projekt bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="0d048-173">In this example, two `<resource>` elements specify that Maven will deploy the JAR file for your web app and the *web.config* file from the Spring Boot project.</span></span> |

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="0d048-174">Erstellen und Bereitstellen der Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="0d048-174">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="0d048-175">Nachdem Sie alle Einstellungen in den vorhergehenden Abschnitten in diesem Artikel konfiguriert haben, können Sie Ihre Web-App in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="0d048-175">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="0d048-176">Führen Sie dazu die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="0d048-176">To do so, use the following steps:</span></span>

1. <span data-ttu-id="0d048-177">Erstellen Sie an der Eingabeaufforderung oder im zuvor verwendeten Terminalfenster die JAR-Datei mithilfe von Maven neu, wenn Sie Änderungen an der Datei *pom.xml* vorgenommen haben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="0d048-177">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="0d048-178">Stellen Sie Ihre Web-App mit Maven in Azure bereit. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="0d048-178">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="0d048-179">Maven stellt Ihre Web-App in Azure bereit. Falls die Web-App noch nicht vorhanden ist, wird sie erstellt.</span><span class="sxs-lookup"><span data-stu-id="0d048-179">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="0d048-180">Wenn Ihre Web-App bereitgestellt wurde, können Sie sie mit dem [Azure-Portal] verwalten.</span><span class="sxs-lookup"><span data-stu-id="0d048-180">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="0d048-181">Ihre Web-App wird unter **App Services** aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="0d048-181">Your web app will be listed in **App Services**:</span></span>

   ![Im Azure-Portal unter „App Services“ aufgeführte Web-App][AP01]

* <span data-ttu-id="0d048-183">Die URL für Ihre Web-App wird in der **Übersicht** für Ihre Web-App aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="0d048-183">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0d048-185">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="0d048-185">Next steps</span></span>

<span data-ttu-id="0d048-186">Weitere Informationen zu den verschiedenen in diesem Artikel besprochenen Technologien finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="0d048-186">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="0d048-187">[Maven-Plug-In für Azure-Web-Apps] (Maven-Plug-In für Azure-Web-Apps)</span><span class="sxs-lookup"><span data-stu-id="0d048-187">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="0d048-188">Anmelden bei Azure über die Azure-Befehlszeilenschnittstelle (CLI)</span><span class="sxs-lookup"><span data-stu-id="0d048-188">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="0d048-189">Bereitstellen einer containerbasierten Spring Boot-App in Azure mithilfe des Maven-Plug-Ins für Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="0d048-189">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="0d048-190">Erstellen eines Azure-Dienstprinzipals mit Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0d048-190">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* <span data-ttu-id="0d048-191">[Maven Settings Reference](https://maven.apache.org/settings.html) (Referenz zu Maven-Einstellungen)</span><span class="sxs-lookup"><span data-stu-id="0d048-191">[Maven Settings Reference](https://maven.apache.org/settings.html)</span></span>

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
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven-Plug-In für Azure-Web-Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin (Maven-Plug-In für Azure-Web-Apps)
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
