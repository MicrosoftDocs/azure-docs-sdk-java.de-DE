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
ms.date: 07/02/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 6d20593620c7fb73f8481be8705bdc42d4e9ce32
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/06/2018
ms.locfileid: "37864050"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a>Verwenden von Spring Boot Starter für Azure Active Directory

## <a name="overview"></a>Übersicht

In diesem Artikel erfahren Sie, wie Sie eine App mit **[Spring Initializr]** erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Active Directory (Azure AD).

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren
* [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), Version 1.7 oder höher
* [Apache Maven](http://maven.apache.org/), Version 3.0 oder höher

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Erstellen einer benutzerdefinierten Anwendung mit dem Spring Initializr

1. Navigieren Sie zu <https://start.spring.io/>.

1. Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.

   ![Angeben von Gruppen- und Artefaktnamen][security-01]

1. Aktivieren Sie im Abschnitt **Core** das Kontrollkästchen für **Sicherheit** und im Abschnitt **Web** das Kontrollkästchen für **Web**.

   ![Auswählen der Starter für Sicherheit und Web][security-02]

1. Scrollen Sie nach unten zum Abschnitt **Azure**, und aktivieren Sie das Kontrollkästchen für **Azure Active Directory**.

   ![Auswählen des Starters für Azure Active Directory][security-03]

1. Klicken Sie am unteren Seitenrand auf die Schaltfläche **Projekt generieren**.

   ![Generieren eines Spring Boot-Projekts][security-04]

1. Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a>Erstellen und Konfigurieren einer neuen Azure Active Directory-Instanz

### <a name="create-the-active-directory-instance"></a>Erstellen der Active Directory-Instanz

1. Melden Sie sich bei <https://portal.azure.com> an.

1. Klicken Sie auf **+Neu** > **Sicherheit + Identität** > **Azure Active Directory**.

   ![Erstellen einer neuen Azure Active Directory-Instanz][directory-01]

1. Geben Sie Werte für **Name der Organisation** und **Name der Anfangsdomäne** ein. Kopieren Sie die vollständige URL Ihres Verzeichnisses. Sie verwenden diese später in diesem Tutorial zum Hinzufügen von Benutzerkonten. (Beispiel: `wingtiptoysdirectory.onmicrosoft.com`.) Wenn Sie fertig sind, klicken Sie auf **Erstellen**.

   ![Angeben von Azure Active Directory-Namen][directory-02]

1. Wählen Sie im Dropdownmenü auf der oberen Symbolleiste des Azure-Portals Ihre neue Azure Active Directory-Instanz aus.

   ![Auswählen Ihrer Azure Active Directory-Instanz][directory-03]

1. Wählen Sie im Portalmenü **Azure Active Directory**, klicken Sie auf **Eigenschaften**, und kopieren Sie die **Verzeichnis-ID**. Diesen Wert verwenden Sie später in diesem Tutorial zum Konfigurieren Ihrer Datei *application.properties*.

   ![Kopieren der Azure Active Directory-ID][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Hinzufügen einer Anwendungsregistrierung für Ihre Spring Boot-App

1. Wählen Sie im Portalmenü die Option **Azure Active Directory** aus, und klicken Sie anschließend auf **Übersicht** > **App-Registrierungen**.

   ![Hinzufügen einer neuen App-Registrierung][directory-04]

1. Klicken Sie auf **Registrierung einer neuen Anwendung**, geben Sie unter **Name** den Namen Ihrer Anwendung an, geben Sie für die **Anmelde-URL** den Wert http://localhost:8080 an, und klicken Sie anschließend auf **Erstellen**.

   ![Erstellen einer neuen App-Registrierung][directory-05]

1. Klicken Sie nach Abschluss der Erstellung auf Ihre Anwendungsregistrierung.

   ![Auswählen Ihrer App-Registrierung][directory-06]

1. Wenn die Seite für Ihre App-Registrierung angezeigt wird, kopieren Sie Ihre **Anwendungs-ID**. Diesen Wert verwenden Sie später in diesem Tutorial zum Konfigurieren Ihrer Datei *application.properties*. Klicken Sie auf **Einstellungen** und dann auf **Schlüssel**.

   ![Erstellen von App-Registrierungsschlüsseln][directory-07]

1. Fügen Sie eine **Beschreibung** hinzu, geben Sie die **Dauer** für einen neuen Schlüssel an, und klicken Sie auf **Speichern**. Der Wert für den Schlüssel wird nach dem Klicken auf das Symbol **Speichern** automatisch ausgefüllt. Notieren Sie sich den Wert des Schlüssels, um später in diesem Tutorial Ihre Datei *application.properties* damit zu konfigurieren. (Dieser Wert kann später nicht mehr abgerufen werden.)

   ![Angeben von Parametern für App-Registrierungsschlüssel][directory-08]

1. Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Einstellungen** und anschließend auf **Erforderliche Berechtigungen**.

   ![Erforderliche Berechtigungen für die App-Registrierung][directory-09]

1. Klicken Sie auf **Windows Azure Active Directory**.

   ![Auswählen von „Windows Azure Active Directory“][directory-10]

1. Aktivieren Sie die Kontrollkästchen **Hiermit greifen Sie als angemeldeter Benutzer auf das Verzeichnis zu.** und **Anmelden und Benutzerprofil lesen**, und klicken Sie anschließend auf **Speichern**.

   ![Aktivieren von Zugriffsberechtigungen][directory-11]

1. Klicken Sie auf der Seite **Erforderliche Berechtigungen** auf **Berechtigungen erteilen** und anschließend auf **Ja**, wenn Sie dazu aufgefordert werden.

   ![Erteilen von Zugriffsberechtigungen][directory-12]

1. Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Einstellungen** und anschließend auf **Antwort-URLs**.

   ![Bearbeiten der Antwort-URLs][directory-14]

1. Geben Sie http://localhost:8080/login/oauth2/code/azure als neue Antwort-URL ein, und klicken Sie anschließend auf **Speichern**.

   ![Hinzufügen einer neuen Antwort-URL][directory-15]

1. Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Manifest**, legen Sie den Wert des `oauth2AllowImplicitFlow`-Parameters auf `true` fest, und klicken Sie dann auf **Speichern**.

   ![App-Manifest konfigurieren][directory-16]

   > [!NOTE]
   > 
   > Weitere Informationen zum `oauth2AllowImplicitFlow`-Parameter und anderen Anwendungseinstellungen finden Sie unter [Azure Active Directory-Anwendungsmanifest][AAD app manifest]. 
   >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a>Hinzufügen eines Benutzerkontos zu Ihrem Verzeichnis und Hinzufügen dieses Kontos zu einer Gruppe

1. Klicken Sie auf der Seite **Übersicht** Ihrer Active Directory-Instanz auf **Benutzer**.

   ![Öffnen des Bereichs „Benutzer“][directory-17]

1. Wenn der Bereich **Benutzer** angezeigt wird, klicken Sie auf **Neuer Benutzer**.

   ![Hinzufügen eines neuen Benutzerkontos][directory-18]

1. Wenn der Bereich **Benutzer** angezeigt wird, geben Sie den **Namen** und den **Benutzernamen** ein.

   ![Eingeben der Benutzerkontoinformationen][directory-19]

   > [!NOTE]
   > 
   > Sie müssen die Verzeichnis-URL von weiter oben in diesem Tutorial eingeben, wenn Sie den Benutzernamen eingeben. Beispiel:
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. Klicken Sie auf **Gruppen**, wählen Sie dann die Gruppen aus, die Sie für die Autorisierung in Ihrer Anwendung verwenden, und klicken Sie dann auf **Auswählen**. (Fügen Sie in diesem Tutorial das Konto der Gruppe _Benutzer_ hinzu.)

   ![Auswählen der Gruppen des Benutzers][directory-20]

1. Klicken Sie auf **Kennwort anzeigen**, und kopieren Sie das Kennwort, Sie verwenden es später in diesem Tutorial für die Anmeldung bei Ihrer Anwendung.

   ![Anzeigen des Kennworts][directory-21]

1. Klicken Sie auf **Erstellen** um das neue Benutzerkonto Ihrem Verzeichnis hinzuzufügen.

   ![Erstellen des neuen Benutzerkontos][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a>Konfigurieren und Kompilieren Ihrer Spring Boot-Anwendung

1. Extrahieren Sie die Dateien aus dem Projektarchiv, das Sie zuvor in diesem Tutorial erstellt und heruntergeladen haben, in ein Verzeichnis.

1. Navigieren Sie zum übergeordneten Ordner für Ihr Projekt, und öffnen Sie die Datei *pom.xml* in einem Text-Editor.

1. Fügen Sie die Abhängigkeiten für Spring OAuth2-Sicherheit hinzu. Beispiel:

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

1. Speichern und schließen Sie die Datei *pom.xml*.

1. Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.

1. Geben Sie die Einstellungen für Ihre App-Registrierung mithilfe der zuvor erstellten Werte an. Beispiel:

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authorization:
   azure.activedirectory.active-directory-groups=Users
   ```
   Hinweis:

   | Parameter | BESCHREIBUNG |
   |---|---|
   | `azure.activedirectory.tenant-id` | Enthält die **Verzeichnis-ID** Ihrer Active Directory-Instanz von vorhin. |
   | `spring.security.oauth2.client.registration.azure.client-id` | Enthält die **Anwendungs-ID** aus der zuvor durchgeführten App-Registrierung. |
   | `spring.security.oauth2.client.registration.azure.client-secret` | Enthält den **Wert** aus dem zuvor erstellten App-Registrierungsschlüssel. |
   | `azure.activedirectory.active-directory-groups` | Enthält eine Liste mit Active Directory-Gruppen für die Autorisierung. |

   > [!NOTE]
   > 
   > Eine vollständige Liste mit verfügbaren Werten in der Datei *application.properties* finden Sie im [Spring Boot-Beispiel für Azure Active Directory][AAD Spring Boot Sample] auf GitHub.
   >

1. Speichern und schließen Sie die Datei *application.properties*.

1. Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *controller*. Beispiel: *src/main/java/com/wingtiptoys/security/controller*.

1. Erstellen Sie im Ordner *controller* eine neue Java-Datei namens *HelloController.java*, und öffnen Sie sie in einem Text-Editor.

1. Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:

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
   > Der Gruppenname, den Sie für die Methode `@PreAuthorize("hasRole('')")` angeben, muss eine der Gruppen enthalten, die Sie im Feld `azure.activedirectory.active-directory-groups` der Datei *application.properties* angegeben haben.
   >

   > [!NOTE]
   > 
   > Sie können verschiedene Autorisierungseinstellungen für verschiedene Anforderungszuordnungen angeben. Beispiel:
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

1. Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *security*. Beispiel: *src/main/java/com/wingtiptoys/security/security*.

1. Erstellen Sie im Ordner *security* eine neue Java-Datei namens *WebSecurityConfig.java*, und öffnen Sie sie in einem Text-Editor.

1. Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:

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

## <a name="build-and-test-your-app"></a>Erstellen und Testen der App

1. Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zu dem Ordner, in dem sich die Datei *pom.xml* Ihrer App befindet.

1. Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Erstellen Ihrer Anwendung][build-application]

1. Nachdem Ihre Anwendung durch Maven erstellt und gestartet wurde, öffnen Sie <http://localhost:8080> in einem Webbrowser. Daraufhin sollten Sie zur Eingabe eines Benutzernamens und eines Kennworts aufgefordert werden.

   ![Anmelden bei Ihrer Anwendung][application-login]

   > [!NOTE]
   > 
   > Wenn dies die erste Anmeldung für ein neues Benutzerkonto ist, werden Sie möglicherweise zum Ändern Ihres Kennworts aufgefordert.
   > 
   > ![Ändern des Kennworts][update-password]
   > 

1. Nach erfolgreicher Anmeldung sollte der Beispieltext „Hello World“ des Controllers angezeigt werden.

   ![Erfolgreiche Anmeldung][hello-world]

   > [!NOTE]
   > 
   > Für nicht autorisierte Benutzerkonten wird eine Meldung vom Typ **HTTP 403 (nicht autorisiert)** zurückgegeben.
   >

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von Azure Active Directory finden Sie in den folgenden Artikeln:

* [Azure Active Directory-Dokumentation]

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen. Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt. Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.

Ein ausführlicheres Beispiel finden Sie im [Spring Boot-Beispiel für Azure Active Directory][AAD Spring Boot Sample] auf GitHub.

<!-- URL List -->

[Azure Active Directory-Dokumentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure für Java-Entwickler]: /java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[Vorteile für MSDN-Abonnenten]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
[directory-16]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-16.png
[directory-17]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-17.png
[directory-18]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-18.png
[directory-19]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-19.png
[directory-20]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-20.png
[directory-21]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-21.png
[directory-22]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-22.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
