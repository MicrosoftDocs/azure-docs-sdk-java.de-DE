---
title: Verwenden von Spring Boot Starter für Azure Active Directory
description: Hier erfahren Sie, wie Sie eine Spring Boot Initializer-App mit Azure Active Directory Starter konfigurieren.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 06/20/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: adcbc78cc129daf589bf070741308e4024432e5d
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090833"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="52639-103">Verwenden von Spring Boot Starter für Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52639-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="52639-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="52639-104">Overview</span></span>

<span data-ttu-id="52639-105">In diesem Artikel erfahren Sie, wie Sie eine App mit **[Spring Initializr]** erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52639-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52639-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="52639-106">Prerequisites</span></span>

<span data-ttu-id="52639-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="52639-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="52639-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="52639-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="52639-109">[Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="52639-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="52639-110">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="52639-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="52639-111">Erstellen einer benutzerdefinierten Anwendung mit dem Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="52639-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="52639-112">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="52639-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="52639-113">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.</span><span class="sxs-lookup"><span data-stu-id="52639-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Angeben von Gruppen- und Artefaktnamen][security-01]

1. <span data-ttu-id="52639-115">Aktivieren Sie im Abschnitt **Core** das Kontrollkästchen für **Sicherheit** und im Abschnitt **Web** das Kontrollkästchen für **Web**.</span><span class="sxs-lookup"><span data-stu-id="52639-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Auswählen der Starter für Sicherheit und Web][security-02]

1. <span data-ttu-id="52639-117">Scrollen Sie nach unten zum Abschnitt **Azure**, und aktivieren Sie das Kontrollkästchen für **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52639-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Auswählen des Starters für Azure Active Directory][security-03]

1. <span data-ttu-id="52639-119">Klicken Sie am unteren Seitenrand auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="52639-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generieren eines Spring Boot-Projekts][security-04]

1. <span data-ttu-id="52639-121">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="52639-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="52639-122">Erstellen und Konfigurieren einer neuen Azure Active Directory-Instanz</span><span class="sxs-lookup"><span data-stu-id="52639-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="52639-123">Erstellen der Active Directory-Instanz</span><span class="sxs-lookup"><span data-stu-id="52639-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="52639-124">Melden Sie sich bei <https://portal.azure.com> an.</span><span class="sxs-lookup"><span data-stu-id="52639-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="52639-125">Klicken Sie auf **+Neu** > **Sicherheit + Identität** > **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52639-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Erstellen einer neuen Azure Active Directory-Instanz][directory-01]

1. <span data-ttu-id="52639-127">Geben Sie Werte für **Name der Organisation** und **Name der Anfangsdomäne** ein, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="52639-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Angeben von Azure Active Directory-Namen][directory-02]

1. <span data-ttu-id="52639-129">Wählen Sie im Dropdownmenü auf der oberen Symbolleiste des Azure-Portals Ihre neue Azure Active Directory-Instanz aus.</span><span class="sxs-lookup"><span data-stu-id="52639-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Auswählen Ihrer Azure Active Directory-Instanz][directory-03]

1. <span data-ttu-id="52639-131">Klicken Sie im Portalmenü auf **Azure Active Directory**, klicken Sie auf **Eigenschaften**, und kopieren Sie die **Verzeichnis-ID**. (Sie wird im weiteren Verlauf des Artikels benötigt.)</span><span class="sxs-lookup"><span data-stu-id="52639-131">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID** - you will use that later in this article.</span></span>

   ![Kopieren der Azure Active Directory-ID][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="52639-133">Hinzufügen einer Anwendungsregistrierung für Ihre Spring Boot-App</span><span class="sxs-lookup"><span data-stu-id="52639-133">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="52639-134">Wählen Sie im Portalmenü die Option **Azure Active Directory** aus, und klicken Sie anschließend auf **Übersicht** > **App-Registrierungen**.</span><span class="sxs-lookup"><span data-stu-id="52639-134">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Hinzufügen einer neuen App-Registrierung][directory-04]

1. <span data-ttu-id="52639-136">Klicken Sie auf **Registrierung einer neuen Anwendung**, geben Sie unter **Name** den Namen Ihrer Anwendung an, geben Sie für die **Anmelde-URL** den Wert http://localhost:8080 an, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="52639-136">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Erstellen einer neuen App-Registrierung][directory-05]

1. <span data-ttu-id="52639-138">Klicken Sie nach Abschluss der Erstellung auf Ihre Anwendungsregistrierung.</span><span class="sxs-lookup"><span data-stu-id="52639-138">Click your application registration after it has been created.</span></span>

   ![Auswählen Ihrer App-Registrierung][directory-06]

1. <span data-ttu-id="52639-140">Kopieren Sie auf der Seite für Ihre App-Registrierung Ihre **Anwendungs-ID** zur späteren Verwendung, klicken Sie auf **Einstellungen**, und klicken Sie anschließend auf **Schlüssel**.</span><span class="sxs-lookup"><span data-stu-id="52639-140">When the page for your app registration, copy your **Application ID** for later use, then click **Settings**, and then click **Keys**.</span></span>

   ![Erstellen von App-Registrierungsschlüsseln][directory-07]

1. <span data-ttu-id="52639-142">Fügen Sie eine **Beschreibung** hinzu, geben Sie die **Dauer** für einen neuen Schlüssel an, und klicken Sie auf **Speichern**. Der Wert für den Schlüssel wird nach dem Klicken auf das Symbol **Speichern** automatisch ausgefüllt. Notieren Sie sich den Wert des Schlüssels zur späteren Verwendung.</span><span class="sxs-lookup"><span data-stu-id="52639-142">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="52639-143">(Dieser Wert kann später nicht mehr abgerufen werden.)</span><span class="sxs-lookup"><span data-stu-id="52639-143">(You will not be able to retrieve this value later.)</span></span>

   ![Angeben von Parametern für App-Registrierungsschlüssel][directory-08]

1. <span data-ttu-id="52639-145">Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Einstellungen** und anschließend auf **Erforderliche Berechtigungen**.</span><span class="sxs-lookup"><span data-stu-id="52639-145">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Erforderliche Berechtigungen für die App-Registrierung][directory-09]

1. <span data-ttu-id="52639-147">Klicken Sie auf **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52639-147">Click **Windows Azure Active Directory**.</span></span>

   ![Auswählen von „Windows Azure Active Directory“][directory-10]

1. <span data-ttu-id="52639-149">Aktivieren Sie die Kontrollkästchen **Hiermit greifen Sie als angemeldeter Benutzer auf das Verzeichnis zu.** und **Anmelden und Benutzerprofil lesen**, und klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="52639-149">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Aktivieren von Zugriffsberechtigungen][directory-11]

1. <span data-ttu-id="52639-151">Klicken Sie auf der Seite **Erforderliche Berechtigungen** auf **Berechtigungen erteilen** und anschließend auf **Ja**, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="52639-151">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Erteilen von Zugriffsberechtigungen][directory-12]

1. <span data-ttu-id="52639-153">Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Einstellungen** und anschließend auf **Antwort-URLs**.</span><span class="sxs-lookup"><span data-stu-id="52639-153">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

   ![Bearbeiten der Antwort-URLs][directory-14]

1. <span data-ttu-id="52639-155">Geben Sie http://localhost:8080/login/oauth2/code/azure als neue Antwort-URL ein, und klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="52639-155">Enter "http://localhost:8080/login/oauth2/code/azure" as a new reply URL, and then click **Save**.</span></span>

   ![Hinzufügen einer neuen Antwort-URL][directory-15]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="52639-157">Konfigurieren und Kompilieren Ihrer Spring Boot-Anwendung</span><span class="sxs-lookup"><span data-stu-id="52639-157">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="52639-158">Extrahieren Sie die Dateien aus dem heruntergeladenen Projektarchiv in ein Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="52639-158">Extract the files from the downloaded project archive into a directory.</span></span>

2. <span data-ttu-id="52639-159">Navigieren Sie in Ihrem Projekt zum übergeordneten Ordner, und öffnen Sie die Datei *pom.xml* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="52639-159">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

3. <span data-ttu-id="52639-160">Fügen Sie die Abhängigkeiten für Spring OAuth2-Sicherheit hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="52639-160">Add the dependencies for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-client</artifactId>
   </dependency>
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-jose</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="52639-161">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="52639-161">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="52639-162">Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="52639-162">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

6. <span data-ttu-id="52639-163">Fügen Sie den Schlüssel für Ihr Speicherkonto hinzu. Verwenden Sie dabei den Wert von vorhin. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="52639-163">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.active-directory-groups=Users
   ```
   <span data-ttu-id="52639-164">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="52639-164">Where:</span></span>

   | <span data-ttu-id="52639-165">Parameter</span><span class="sxs-lookup"><span data-stu-id="52639-165">Parameter</span></span> | <span data-ttu-id="52639-166">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="52639-166">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="52639-167">Enthält die **Verzeichnis-ID** Ihrer Active Directory-Instanz von vorhin.</span><span class="sxs-lookup"><span data-stu-id="52639-167">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="52639-168">Enthält die **Anwendungs-ID** aus der zuvor durchgeführten App-Registrierung.</span><span class="sxs-lookup"><span data-stu-id="52639-168">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="52639-169">Enthält den **Wert** aus dem zuvor erstellten App-Registrierungsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="52639-169">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="52639-170">Enthält eine Liste mit Active Directory-Gruppen für die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="52639-170">Contains a list of Active Directory groups to use for authentication.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="52639-171">Eine vollständige Liste mit verfügbaren Werten in der Datei *application.properties* finden Sie im [Spring Boot-Beispiel für Azure Active Directory][AAD Spring Boot Sample] auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="52639-171">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="52639-172">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="52639-172">Save and close the *application.properties* file.</span></span>

8. <span data-ttu-id="52639-173">Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *controller*. Beispiel: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="52639-173">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

9. <span data-ttu-id="52639-174">Erstellen Sie im Ordner *controller* eine neue Java-Datei namens *HelloController.java*, und öffnen Sie sie in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="52639-174">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="52639-175">Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:</span><span class="sxs-lookup"><span data-stu-id="52639-175">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.oauth2.client.OAuth2AuthorizedClient;
   import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
   import org.springframework.ui.Model;

   @RestController
   public class HelloController {
      @Autowired
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String helloWorld() {
         return "Hello World!";
      }
   }
   ```
   > [!NOTE]
   > 
   > <span data-ttu-id="52639-176">Der Gruppenname, den Sie für die Methode `@PreAuthorize("hasRole('')")` angeben, muss eine der Gruppen enthalten, die Sie im Feld `azure.activedirectory.active-directory-groups` der Datei *application.properties* angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="52639-176">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="52639-177">Sie können verschiedene Autorisierungseinstellungen für verschiedene Anforderungszuordnungen angeben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="52639-177">You can specify different authorization settings for different request mappings; for example:</span></span>
   >
   > ``` java
   > public class HelloController {
   >    @Autowired
   >    @PreAuthorize("hasRole('Users')")
   >    @RequestMapping("/")
   >    public String helloWorld() {
   >       return "Hello Users!";
   >    }
   >    @PreAuthorize("hasRole('Group1')")
   >    @RequestMapping("/Group1")
   >    public String groupOne() {
   >       return "Hello Group 1 Users!";
   >    }
   >    @PreAuthorize("hasRole('Group2')")
   >    @RequestMapping("/Group2")
   >    public String groupTwo() {
   >       return "Hello Group 2 Users!";
   >    }
   > }
   > ```
   >    

11. <span data-ttu-id="52639-178">Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *security*. Beispiel: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="52639-178">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

12. <span data-ttu-id="52639-179">Erstellen Sie im Ordner *security* eine neue Java-Datei namens *WebSecurityConfig.java*, und öffnen Sie sie in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="52639-179">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="52639-180">Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:</span><span class="sxs-lookup"><span data-stu-id="52639-180">Enter the following code, then save and close the file:</span></span>

    ```java
    package com.wingtiptoys.security;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    import org.springframework.security.oauth2.client.oidc.userinfo.OidcUserRequest;
    import org.springframework.security.oauth2.client.userinfo.OAuth2UserService;
    import org.springframework.security.oauth2.core.oidc.user.OidcUser;

    @EnableWebSecurity
    @EnableGlobalMethodSecurity(prePostEnabled = true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
        @Autowired
        private OAuth2UserService<OidcUserRequest, OidcUser> oidcUserService;

        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                .authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .oauth2Login()
                .userInfoEndpoint()
                .oidcUserService(oidcUserService);
        }
    }
    ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="52639-181">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="52639-181">Build and test your app</span></span>

1. <span data-ttu-id="52639-182">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zu dem Ordner, in dem sich die Datei *pom.xml* Ihrer App befindet.</span><span class="sxs-lookup"><span data-stu-id="52639-182">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="52639-183">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="52639-183">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Erstellen Ihrer Anwendung][build-application]

1. <span data-ttu-id="52639-185">Nachdem Ihre Anwendung durch Maven erstellt und gestartet wurde, öffnen Sie <http://localhost:8080> in einem Webbrowser. Daraufhin sollten Sie zur Eingabe eines Benutzernamens und eines Kennworts aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="52639-185">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Anmelden bei Ihrer Anwendung][application-login]

1. <span data-ttu-id="52639-187">Nach erfolgreicher Anmeldung sollte der Beispieltext „Hello World“ des Controllers angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="52639-187">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Erfolgreiche Anmeldung][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="52639-189">Für nicht autorisierte Benutzerkonten wird eine Meldung vom Typ **HTTP 403 (nicht autorisiert)** zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="52639-189">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="52639-190">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="52639-190">Next steps</span></span>

<span data-ttu-id="52639-191">Weitere Informationen zur Verwendung von Azure Active Directory finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="52639-191">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="52639-192">[Azure Active Directory-Dokumentation]</span><span class="sxs-lookup"><span data-stu-id="52639-192">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="52639-193">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="52639-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="52639-194">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="52639-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="52639-195">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="52639-195">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="52639-196">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="52639-196">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="52639-197">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="52639-197">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="52639-198">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="52639-198">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="52639-199">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="52639-199">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="52639-200">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="52639-200">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="52639-201">Ein ausführlicheres Beispiel finden Sie im [Spring Boot-Beispiel für Azure Active Directory][AAD Spring Boot Sample] auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="52639-201">For a more-detailed sample, see the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>

<!-- URL List -->

[Azure Active Directory-Dokumentation]: /azure/active-directory/
[Azure Active Directory Documentation]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[security-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-01.png
[security-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-02.png
[security-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-03.png
[security-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-04.png

[directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-01.png
[directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-02.png
[directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-03.png
[directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-04.png
[directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-05.png
[directory-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-06.png
[directory-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-07.png
[directory-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-08.png
[directory-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-09.png
[directory-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-10.png
[directory-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-11.png
[directory-12]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-12.png
[directory-13]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-13.png
[directory-14]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-14.png
[directory-15]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-15.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
