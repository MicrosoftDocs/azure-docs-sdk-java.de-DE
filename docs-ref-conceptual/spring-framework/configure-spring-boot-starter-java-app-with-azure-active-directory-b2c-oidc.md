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
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a>Tutorial: Schützen einer Java-Web-App mithilfe von Spring Boot Starter für Azure Active Directory B2C

## <a name="overview"></a>Übersicht

In diesem Artikel erfahren Sie, wie Sie eine Java-App mit [Spring Initializr](https://start.spring.io/) erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Active Directory (Azure AD).

In diesem Tutorial lernen Sie Folgendes:

> [!div class="checklist"]
> * Erstellen einer Java-Anwendung mit dem Spring Initializr
> * Konfigurieren von Azure Active Directory B2C
> * Schützen der Anwendung mit Spring Boot-Klassen und -Anmerkungen
> * Erstellen und Testen der Java-Anwendung

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein unterstütztes Java Development Kit (JDK). Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher

## <a name="create-an-app-using-spring-initializr"></a>Erstellen einer App mithilfe von Spring Initializr

1. Navigieren Sie zu <https://start.spring.io/>.

2. Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und wählen Sie dann die Module **Web** und **Sicherheit** von Spring Initializr aus.

   ![Angeben von Gruppen- und Artefaktnamen](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. Klicken Sie auf `Generate Project`, und laden Sie das Projekt nach entsprechender Aufforderung in einen Pfad auf dem lokalen Computer herunter.

## <a name="create-azure-active-directory-instance"></a>Erstellen einer Azure Active Directory-Instanz

### <a name="create-the-active-directory-instance"></a>Erstellen der Active Directory-Instanz

1. Melden Sie sich bei <https://portal.azure.com> an.

2. Klicken Sie auf **+Ressource erstellen** > **Identität** > **Azure Active Directory B2C**.

   ![Erstellen einer neuen Azure Active Directory B2C-Instanz](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. Geben Sie Werte für **Name der Organisation** und **Name der Anfangsdomäne** ein, erfassen Sie den **Domänennamen** als `${your-tenant-name}`, und klicken Sie anschließend auf **Erstellen**.

   ![Abrufen des Namens Ihres B2C-Mandanten](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. Wählen Sie im Azure-Portal auf der Symbolleiste oben rechts Ihren Kontonamen aus, und klicken Sie dann auf **Verzeichnis wechseln**.

   ![Auswählen Ihrer Azure Active Directory-Instanz](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. Wählen Sie im Dropdownmenü Ihre neue Azure Active Directory-Instanz aus.

   ![Auswählen Ihrer Azure Active Directory-Instanz](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. Suchen Sie nach `b2c`, und klicken Sie auf den Dienst `Azure AD B2C`.

   ![Suchen der Azure Active Directory B2C-Instanz](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Hinzufügen einer Anwendungsregistrierung für Ihre Spring Boot-App

1. Wählen Sie im Portalmenü **Azure AD B2C** aus, und klicken Sie auf **Anwendungen** und dann auf **Hinzufügen**.

   ![Hinzufügen einer neuen App-Registrierung](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. Geben Sie unter **Name** Ihren Anwendungsnamen ein, fügen Sie `http://localhost:8080/home` ins Feld **Antwort-URL**, und erfassen Sie Ihre **Anwendungs-ID** als `${your-client-id}`. Klicken Sie anschließend auf **Speichern**.

   ![Hinzufügen der Antwort-URL Ihrer Anwendung](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. Wählen Sie in Ihrer Anwendung **Schlüssel** aus, klicken Sie zum Generieren von `${your-client-secret}` auf **Schlüssel generieren**, und klicken Sie dann auf **Speichern**.

4. Wählen Sie auf der linken Seite **Benutzerflows** aus, und klicken Sie dann auf **Neuer Benutzerflow**.

   ![Erstellen eines Benutzerflows](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. Wählen Sie **Registrieren und Anmelden**, **Profilbearbeitung** und **Kennwortzurücksetzung** aus, um entsprechende Benutzerflows zu erstellen. Geben Sie unter **Name** einen Namen für den Benutzerflow und unter **Benutzerattribute und Ansprüche** die entsprechenden Werte ein, und klicken Sie auf **Erstellen**.

   ![Konfigurieren des Benutzerflows](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a>Konfigurieren und Kompilieren Ihrer App

1. Extrahieren Sie die Dateien aus dem Projektarchiv, das Sie zuvor in diesem Tutorial erstellt und heruntergeladen haben, in ein Verzeichnis.

2. Navigieren Sie zum übergeordneten Ordner für Ihr Projekt, und öffnen Sie die Maven-Projektdatei `pom.xml` in einem Text-Editor.

3. Fügen Sie die Abhängigkeiten für Spring OAuth2-Sicherheit zu `pom.xml` hinzu:

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

4. Speichern und schließen Sie die Datei *pom.xml*.

5. Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.yml* in einem Text-Editor.

6. Geben Sie die Einstellungen für Ihre App-Registrierung mithilfe der zuvor erstellten Werte an. Beispiel:

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
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | Enthält den zuvor erfassten AD B2C-Wert für `${your-tenant-name`. |
   | `azure.activedirectory.b2c.client-id` | Enthält den Wert für `${your-client-id}` aus der zuvor erstellten Anwendung. |
   | `azure.activedirectory.b2c.client-secret` | Enthält den Wert für `${your-client-secret}` aus der zuvor erstellten Anwendung. |
   | `azure.activedirectory.b2c.reply-url` | Enthält eine **Antwort-URL** aus der zuvor erstellten Anwendung. |
   | `azure.activedirectory.b2c.logout-success-url` | Geben Sie die URL an, wenn Ihre Anwendung erfolgreich abgemeldet wurde. |
   | `azure.activedirectory.b2c.user-flows` | Enthält den Namen der zuvor erstellten Benutzerflows.

   > [!NOTE]
   > 
   > Eine vollständige Liste mit verfügbaren Werten in der Datei *application.yml* finden Sie im [Spring Boot-Beispiel für Azure Active Directory B2C][Spring Boot-Beispiel für AAD B2C] auf GitHub.
   >

7. Speichern und schließen Sie die Datei *application.yml*.

8. Erstellen Sie einen Ordner mit dem Namen *controller* im Java-Quellordner für Ihre Anwendung.

9. Erstellen Sie im Ordner *controller* eine neue Java-Datei namens *HelloController.java*, und öffnen Sie sie in einem Text-Editor.

10. Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:

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

11. Erstellen Sie einen Ordner mit dem Namen *security* im Java-Quellordner für Ihre Anwendung.

12. Erstellen Sie im Ordner *security* eine neue Java-Datei namens *WebSecurityConfig.java*, und öffnen Sie sie in einem Text-Editor.

13. Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:

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
14. Kopieren Sie `greeting.html` und `home.html` aus dem [Spring Boot-Beispiel für Azure AD B2C](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), und ersetzen Sie `${your-profile-edit-user-flow}` und `${your-password-reset-user-flow}` jeweils durch den Namen des zuvor erstellten Benutzerflows.

## <a name="build-and-test-your-app"></a>Erstellen und Testen der App

1. Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zu dem Ordner, in dem sich die Datei *pom.xml* Ihrer App befindet.

2. Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. Nachdem Ihre Anwendung durch Maven erstellt und gestartet wurde, öffnen Sie <http://localhost:8080/> in einem Webbrowser. Daraufhin sollten Sie zur Anmeldeseite weitergeleitet werden.

   ![Anmeldeseite](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. Klicken Sie auf den Link mit dem Namen des Benutzerflows `${your-sign-up-or-in}`. Daraufhin sollten Sie zu Azure AD B2C weitergeleitet werden, um den Authentifizierungsprozess zu starten.

   ![Azure AD B2C-Anmeldung](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. Nach erfolgreicher Anmeldung sollte das Beispiel `home page` im Browser angezeigt werden.

   ![Erfolgreiche Anmeldung](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie mit Azure Active Directory B2C Starter eine neue Java-Webanwendung erstellt, einen neuen Azure AD B2C-Mandanten konfiguriert und eine neue Anwendung darin registriert. Anschließend haben Sie Ihre Anwendung zur Verwendung der Spring-Anmerkungen und -Klassen zum Schützen der Web-App konfiguriert.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.

> [!div class="nextstepaction"]
> [Spring Framework in Azure](/java/azure/spring-framework)
