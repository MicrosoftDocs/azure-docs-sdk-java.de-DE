---
title: Verwenden von Spring Boot Starter für Azure Active Directory B2C
description: Hier erfahren Sie, wie Sie eine Spring Boot Initializer-App mit Azure Active Directory B2C Starter konfigurieren.
services: active-directory-b2c
documentationcenter: java
author: panli
manager: kevinzha
editor: panli
ms.assetid: ''
ms.author: panli
ms.date: 02/28/2019
ms.devlang: java
ms.service: active-directory-b2c
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 21aa6c812a519d686356851a57f00688d9a24fa4
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625712"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a><span data-ttu-id="c52ee-103">Tutorial: Schützen einer Java-Web-App mithilfe von Spring Boot Starter für Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="c52ee-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory B2C.</span></span>

## <a name="overview"></a><span data-ttu-id="c52ee-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="c52ee-104">Overview</span></span>

<span data-ttu-id="c52ee-105">In diesem Artikel erfahren Sie, wie Sie eine Java-App mit [Spring Initializr](https://start.spring.io/) erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c52ee-105">This article demonstrates creating a Java app with the [Spring Initializr](https://start.spring.io/) that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c52ee-106">In diesem Tutorial lernen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c52ee-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c52ee-107">Erstellen einer Java-Anwendung mit dem Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="c52ee-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="c52ee-108">Konfigurieren von Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="c52ee-108">Configure Azure Active Directory B2C</span></span>
> * <span data-ttu-id="c52ee-109">Schützen der Anwendung mit Spring Boot-Klassen und -Anmerkungen</span><span class="sxs-lookup"><span data-stu-id="c52ee-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="c52ee-110">Erstellen und Testen der Java-Anwendung</span><span class="sxs-lookup"><span data-stu-id="c52ee-110">Build and test your Java application</span></span>

<span data-ttu-id="c52ee-111">Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.</span><span class="sxs-lookup"><span data-stu-id="c52ee-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c52ee-112">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c52ee-112">Prerequisites</span></span>

<span data-ttu-id="c52ee-113">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="c52ee-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="c52ee-114">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="c52ee-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c52ee-115">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c52ee-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c52ee-116">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="c52ee-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="c52ee-117">Erstellen einer App mithilfe von Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="c52ee-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="c52ee-118">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="c52ee-118">Browse to <https://start.spring.io/>.</span></span>

2. <span data-ttu-id="c52ee-119">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und wählen Sie dann die Module **Web** und **Sicherheit** von Spring Initializr aus.</span><span class="sxs-lookup"><span data-stu-id="c52ee-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select the **Web** and **Security** module of the Spring Initializr.</span></span>

   ![Angeben von Gruppen- und Artefaktnamen](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. <span data-ttu-id="c52ee-121">Klicken Sie auf `Generate Project`, und laden Sie das Projekt nach entsprechender Aufforderung in einen Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="c52ee-121">Click `Generate Project`, download the project to a path on your local computer when prompted.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="c52ee-122">Erstellen einer Azure Active Directory-Instanz</span><span class="sxs-lookup"><span data-stu-id="c52ee-122">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="c52ee-123">Erstellen der Active Directory-Instanz</span><span class="sxs-lookup"><span data-stu-id="c52ee-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="c52ee-124">Melden Sie sich bei <https://portal.azure.com> an.</span><span class="sxs-lookup"><span data-stu-id="c52ee-124">Log into <https://portal.azure.com>.</span></span>

2. <span data-ttu-id="c52ee-125">Klicken Sie auf **+Ressource erstellen** > **Identität** > **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="c52ee-125">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory B2C**.</span></span>

   ![Erstellen einer neuen Azure Active Directory B2C-Instanz](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. <span data-ttu-id="c52ee-127">Geben Sie Werte für **Name der Organisation** und **Name der Anfangsdomäne** ein, erfassen Sie den **Domänennamen** als `${your-tenant-name}`, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c52ee-127">Enter your **Organization name** and your **Initial domain name**, record the **domain name** as your `${your-tenant-name}` and click **Create**.</span></span>

   ![Abrufen des Namens Ihres B2C-Mandanten](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. <span data-ttu-id="c52ee-129">Wählen Sie im Azure-Portal auf der Symbolleiste oben rechts Ihren Kontonamen aus, und klicken Sie dann auf **Verzeichnis wechseln**.</span><span class="sxs-lookup"><span data-stu-id="c52ee-129">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Auswählen Ihrer Azure Active Directory-Instanz](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. <span data-ttu-id="c52ee-131">Wählen Sie im Dropdownmenü Ihre neue Azure Active Directory-Instanz aus.</span><span class="sxs-lookup"><span data-stu-id="c52ee-131">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Auswählen Ihrer Azure Active Directory-Instanz](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. <span data-ttu-id="c52ee-133">Suchen Sie nach `b2c`, und klicken Sie auf den Dienst `Azure AD B2C`.</span><span class="sxs-lookup"><span data-stu-id="c52ee-133">Search `b2c` and click `Azure AD B2C` service.</span></span>

   ![Suchen der Azure Active Directory B2C-Instanz](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="c52ee-135">Hinzufügen einer Anwendungsregistrierung für Ihre Spring Boot-App</span><span class="sxs-lookup"><span data-stu-id="c52ee-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="c52ee-136">Wählen Sie im Portalmenü **Azure AD B2C** aus, und klicken Sie auf **Anwendungen** und dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c52ee-136">Select **Azure AD B2C** from the portal menu, click **Applications**, and then click **Add**.</span></span>

   ![Hinzufügen einer neuen App-Registrierung](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. <span data-ttu-id="c52ee-138">Geben Sie unter **Name** Ihren Anwendungsnamen ein, fügen Sie `http://localhost:8080/home` ins Feld **Antwort-URL**, und erfassen Sie Ihre **Anwendungs-ID** als `${your-client-id}`. Klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c52ee-138">Specify your application **Name**, add `http://localhost:8080/home` for the **Reply URL**, record the **Application ID** as your `${your-client-id}` and then click **Save**.</span></span>

   ![Hinzufügen der Antwort-URL Ihrer Anwendung](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. <span data-ttu-id="c52ee-140">Wählen Sie in Ihrer Anwendung **Schlüssel** aus, klicken Sie zum Generieren von `${your-client-secret}` auf **Schlüssel generieren**, und klicken Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c52ee-140">Select **Keys** from your application, click **Generate key** to generate `${your-client-secret}` and then **Save**.</span></span>

4. <span data-ttu-id="c52ee-141">Wählen Sie auf der linken Seite **Benutzerflows** aus, und klicken Sie dann auf **Neuer Benutzerflow**.</span><span class="sxs-lookup"><span data-stu-id="c52ee-141">Select **User flows** on your left, and then **Click** \*\*New user flow \*\*.</span></span>

   ![Erstellen eines Benutzerflows](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. <span data-ttu-id="c52ee-143">Wählen Sie **Registrieren und Anmelden**, **Profilbearbeitung** und **Kennwortzurücksetzung** aus, um entsprechende Benutzerflows zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c52ee-143">Choose **Sign up or in**, **Profile editing** and **Password reset** to create user flows respectively.</span></span> <span data-ttu-id="c52ee-144">Geben Sie unter **Name** einen Namen für den Benutzerflow und unter **Benutzerattribute und Ansprüche** die entsprechenden Werte ein, und klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c52ee-144">Specify your user flow **Name** and **User attributes and claims**, click **Create**.</span></span>

   ![Konfigurieren des Benutzerflows](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="c52ee-146">Konfigurieren und Kompilieren Ihrer App</span><span class="sxs-lookup"><span data-stu-id="c52ee-146">Configure and compile your app</span></span>

1. <span data-ttu-id="c52ee-147">Extrahieren Sie die Dateien aus dem Projektarchiv, das Sie zuvor in diesem Tutorial erstellt und heruntergeladen haben, in ein Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="c52ee-147">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

2. <span data-ttu-id="c52ee-148">Navigieren Sie zum übergeordneten Ordner für Ihr Projekt, und öffnen Sie die Maven-Projektdatei `pom.xml` in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="c52ee-148">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

3. <span data-ttu-id="c52ee-149">Fügen Sie die Abhängigkeiten für Spring OAuth2-Sicherheit zu `pom.xml` hinzu:</span><span class="sxs-lookup"><span data-stu-id="c52ee-149">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-active-directory-b2c-spring-boot-starter</artifactId>
       <version>2.1.6.M2</version>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-thymeleaf</artifactId>
   </dependency>
   <dependency>
       <groupId>org.thymeleaf.extras</groupId>
       <artifactId>thymeleaf-extras-springsecurity5</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="c52ee-150">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="c52ee-150">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="c52ee-151">Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.yml* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="c52ee-151">Navigate to the *src/main/resources* folder in your project and open the *application.yml* file in a text editor.</span></span>

6. <span data-ttu-id="c52ee-152">Geben Sie die Einstellungen für Ihre App-Registrierung mithilfe der zuvor erstellten Werte an. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c52ee-152">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

   ```yaml
   azure:
     activedirectory:
       b2c:
         tenant: ${your-tenant-name}
         client-id: ${your-client-id}
         client-secret: ${your-client-secret}
         reply-url: ${your-reply-url-from-aad} # should be absolute url.
         logout-success-url: ${you-logout-success-url}
         user-flows:
           sign-up-or-sign-in: ${your-sign-up-or-in-user-flow}
           profile-edit: ${your-profile-edit-user-flow}     # optional
           password-reset: ${your-password-reset-user-flow} # optional
   ```
   <span data-ttu-id="c52ee-153">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="c52ee-153">Where:</span></span>

   | <span data-ttu-id="c52ee-154">Parameter</span><span class="sxs-lookup"><span data-stu-id="c52ee-154">Parameter</span></span> | <span data-ttu-id="c52ee-155">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c52ee-155">Description</span></span> |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | <span data-ttu-id="c52ee-156">Enthält den zuvor erfassten AD B2C-Wert für `${your-tenant-name`.</span><span class="sxs-lookup"><span data-stu-id="c52ee-156">Contains your AD B2C's `${your-tenant-name` from earlier.</span></span> |
   | `azure.activedirectory.b2c.client-id` | <span data-ttu-id="c52ee-157">Enthält den Wert für `${your-client-id}` aus der zuvor erstellten Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c52ee-157">Contains the `${your-client-id}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.client-secret` | <span data-ttu-id="c52ee-158">Enthält den Wert für `${your-client-secret}` aus der zuvor erstellten Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c52ee-158">Contains the `${your-client-secret}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.reply-url` | <span data-ttu-id="c52ee-159">Enthält eine **Antwort-URL** aus der zuvor erstellten Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c52ee-159">Contains one of the **Reply URL** from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.logout-success-url` | <span data-ttu-id="c52ee-160">Geben Sie die URL an, wenn Ihre Anwendung erfolgreich abgemeldet wurde.</span><span class="sxs-lookup"><span data-stu-id="c52ee-160">Specify the URL when your application logout successfully.</span></span> |
   | `azure.activedirectory.b2c.user-flows` | <span data-ttu-id="c52ee-161">Enthält den Namen der zuvor erstellten Benutzerflows.</span><span class="sxs-lookup"><span data-stu-id="c52ee-161">Contains the name of the user flows that you completed earlier.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="c52ee-162">Eine vollständige Liste mit verfügbaren Werten in der Datei *application.yml* finden Sie im [Spring Boot-Beispiel für Azure Active Directory B2C][Spring Boot-Beispiel für AAD B2C] auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="c52ee-162">For a full list of values that are available in your *application.yml* file, see the [Azure Active Directory B2C Spring Boot Sample][AAD B2C Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="c52ee-163">Speichern und schließen Sie die Datei *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="c52ee-163">Save and close the *application.yml* file.</span></span>

8. <span data-ttu-id="c52ee-164">Erstellen Sie einen Ordner mit dem Namen *controller* im Java-Quellordner für Ihre Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c52ee-164">Create a folder named *controller* in the Java source folder for your application.</span></span>

9. <span data-ttu-id="c52ee-165">Erstellen Sie im Ordner *controller* eine neue Java-Datei namens *HelloController.java*, und öffnen Sie sie in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="c52ee-165">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="c52ee-166">Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:</span><span class="sxs-lookup"><span data-stu-id="c52ee-166">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.controller;
    
    import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
    import org.springframework.security.oauth2.core.user.OAuth2User;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class WebController {
    
        private void initializeModel(Model model, OAuth2AuthenticationToken token) {
            if (token != null) {
                final OAuth2User user = token.getPrincipal();
    
                model.addAttribute("grant_type", user.getAuthorities());
                model.addAllAttributes(user.getAttributes());
            }
        }
    
        @GetMapping(value = "/")
        public String index(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    
        @GetMapping(value = "/greeting")
        public String greeting(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "greeting";
        }
    
        @GetMapping(value = "/home")
        public String home(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    }
    ```

11. <span data-ttu-id="c52ee-167">Erstellen Sie einen Ordner mit dem Namen *security* im Java-Quellordner für Ihre Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c52ee-167">Create a folder named *security* in the Java source folder for your application.</span></span>

12. <span data-ttu-id="c52ee-168">Erstellen Sie im Ordner *security* eine neue Java-Datei namens *WebSecurityConfig.java*, und öffnen Sie sie in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="c52ee-168">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="c52ee-169">Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:</span><span class="sxs-lookup"><span data-stu-id="c52ee-169">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.security;
    
    import com.microsoft.azure.spring.autoconfigure.b2c.AADB2COidcLoginConfigurer;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    
    @EnableWebSecurity
    public class WebSecurityConfiguration extends WebSecurityConfigurerAdapter {
    
        private final AADB2COidcLoginConfigurer configurer;
    
        public WebSecurityConfiguration(AADB2COidcLoginConfigurer configurer) {
            this.configurer = configurer;
        }
    
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                    .authorizeRequests()
                    .anyRequest()
                    .authenticated()
                    .and()
                    .apply(configurer)
            ;
        }
    }
    ```
14. <span data-ttu-id="c52ee-170">Kopieren Sie `greeting.html` und `home.html` aus dem [Spring Boot-Beispiel für Azure AD B2C](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), und ersetzen Sie `${your-profile-edit-user-flow}` und `${your-password-reset-user-flow}` jeweils durch den Namen des zuvor erstellten Benutzerflows.</span><span class="sxs-lookup"><span data-stu-id="c52ee-170">Copy the `greeting.html` and `home.html` from [Azure AD B2C Spring Boot Sample](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), and replace the `${your-profile-edit-user-flow}` and `${your-password-reset-user-flow}` with your user flow name respectively that completed earlier.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="c52ee-171">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="c52ee-171">Build and test your app</span></span>

1. <span data-ttu-id="c52ee-172">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zu dem Ordner, in dem sich die Datei *pom.xml* Ihrer App befindet.</span><span class="sxs-lookup"><span data-stu-id="c52ee-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

2. <span data-ttu-id="c52ee-173">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="c52ee-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. <span data-ttu-id="c52ee-174">Nachdem Ihre Anwendung durch Maven erstellt und gestartet wurde, öffnen Sie <http://localhost:8080/> in einem Webbrowser. Daraufhin sollten Sie zur Anmeldeseite weitergeleitet werden.</span><span class="sxs-lookup"><span data-stu-id="c52ee-174">After your application is built and started by Maven, open <http://localhost:8080/> in a web browser; you should be redirected to login page.</span></span>

   ![Anmeldeseite](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. <span data-ttu-id="c52ee-176">Klicken Sie auf den Link mit dem Namen des Benutzerflows `${your-sign-up-or-in}`. Daraufhin sollten Sie zu Azure AD B2C weitergeleitet werden, um den Authentifizierungsprozess zu starten.</span><span class="sxs-lookup"><span data-stu-id="c52ee-176">Click linke with name of `${your-sign-up-or-in}` user flow, you should be rediected Azure AD B2C to start the authentication process.</span></span>

   ![Azure AD B2C-Anmeldung](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. <span data-ttu-id="c52ee-178">Nach erfolgreicher Anmeldung sollte das Beispiel `home page` im Browser angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c52ee-178">After you have logged in successfully, you should see the sample `home page` from the browser,</span></span>

   ![Erfolgreiche Anmeldung](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a><span data-ttu-id="c52ee-180">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c52ee-180">Summary</span></span>

<span data-ttu-id="c52ee-181">In diesem Tutorial haben Sie mit Azure Active Directory B2C Starter eine neue Java-Webanwendung erstellt, einen neuen Azure AD B2C-Mandanten konfiguriert und eine neue Anwendung darin registriert. Anschließend haben Sie Ihre Anwendung zur Verwendung der Spring-Anmerkungen und -Klassen zum Schützen der Web-App konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="c52ee-181">In this tutorial, you created a new Java web application using the Azure Active Directory B2C starter, configured a new Azure AD B2C tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c52ee-182">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c52ee-182">Next steps</span></span>

<span data-ttu-id="c52ee-183">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="c52ee-183">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c52ee-184">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="c52ee-184">Spring on Azure</span></span>](/java/azure/spring-framework)
