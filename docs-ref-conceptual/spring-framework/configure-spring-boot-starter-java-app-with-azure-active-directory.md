---
title: "Verwenden von Spring Boot Starter für Azure Active Directory"
description: Hier erfahren Sie, wie Sie eine Spring Boot Initializer-App mit Azure Active Directory Starter konfigurieren.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: cf1cad0b87626058f7204a6565d09fb8901b7ce4
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a>Verwenden von Spring Boot Starter für Azure Active Directory

## <a name="overview"></a>Übersicht

In diesem Artikel erfahren Sie, wie Sie eine App mit **[Spring Initializr]** erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Active Directory (Azure AD).

## <a name="prerequisites"></a>Voraussetzungen

Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:

* Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [MSDN-Abonnentenvorteile] anwenden oder sich für ein [kostenloses Azure-Konto] registrieren
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

1. Melden Sie sich unter <https://portal.azure.com> an.

1. Klicken Sie auf **+Neu** > **Sicherheit + Identität** > **Azure Active Directory**.

   ![Erstellen einer neuen Azure Active Directory-Instanz][directory-01]

1. Geben Sie Werte für **Name der Organisation** und **Name der Anfangsdomäne** ein, und klicken Sie anschließend auf **Erstellen**.

   ![Angeben von Azure Active Directory-Namen][directory-02]

1. Wählen Sie im Dropdownmenü auf der oberen Symbolleiste des Azure-Portals Ihre neue Azure Active Directory-Instanz aus.

   ![Auswählen Ihrer Azure Active Directory-Instanz][directory-03]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Hinzufügen einer Anwendungsregistrierung für Ihre Spring Boot-App

1. Wählen Sie im Portalmenü die Option **Azure Active Directory** aus, und klicken Sie anschließend auf **Übersicht** > **App-Registrierungen**.

   ![Hinzufügen einer neuen App-Registrierung][directory-04]

1. Klicken Sie auf **Registrierung einer neuen Anwendung**, geben Sie unter **Name** den Namen Ihrer Anwendung an, geben Sie für die **Anmelde-URL** den Wert „ http://localhost:8080 “ an, und klicken Sie anschließend auf **Erstellen**.

   ![Erstellen einer neuen App-Registrierung][directory-05]

1. Klicken Sie nach Abschluss der Erstellung auf Ihre Anwendungsregistrierung.

   ![Auswählen Ihrer App-Registrierung][directory-06]

1. Kopieren Sie auf der Seite für Ihre App-Registrierung Ihre **Anwendungs-ID** zur späteren Verwendung, und klicken Sie anschließend auf **Schlüssel**.

   ![Erstellen von App-Registrierungsschlüsseln][directory-07]

1. Fügen Sie eine **Beschreibung** hinzu, geben Sie die **Dauer** für einen neuen Schlüssel an, und klicken Sie auf **Speichern**. Der Wert für den Schlüssel wird nach dem Klicken auf das Symbol **Speichern** automatisch ausgefüllt. Notieren Sie sich den Wert des Schlüssels zur späteren Verwendung. (Dieser Wert kann später nicht mehr abgerufen werden.)

   ![Angeben von Parametern für App-Registrierungsschlüssel][directory-08]

1. Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Erforderliche Berechtigungen**.

   ![Erforderliche Berechtigungen für die App-Registrierung][directory-09]

1. Klicken Sie auf **Windows Azure Active Directory**.

   ![Auswählen von „Windows Azure Active Directory“][directory-10]

1. Aktivieren Sie die Kontrollkästchen **Hiermit greifen Sie als angemeldeter Benutzer auf das Verzeichnis zu.** und **Anmelden und Benutzerprofil lesen**, und klicken Sie anschließend auf **Speichern**.

   ![Aktivieren von Zugriffsberechtigungen][directory-11]

1. Klicken Sie auf der Seite **Erforderliche Berechtigungen** auf **Berechtigungen erteilen** und anschließend auf **Ja**, wenn Sie dazu aufgefordert werden.

   ![Erteilen von Zugriffsberechtigungen][directory-12]

## <a name="configure-and-compile-your-spring-boot-application"></a>Konfigurieren und Kompilieren Ihrer Spring Boot-Anwendung

1. Extrahieren Sie die Dateien aus dem heruntergeladenen Projektarchiv in ein Verzeichnis.

1. Navigieren Sie in Ihrem Projekt zum übergeordneten Ordner, und öffnen Sie die Datei *pom.xml* in einem Text-Editor.

1. Fügen Sie die Abhängigkeit für Spring OAuth2-Sicherheit hinzu. Beispiel:

   ```xml
   <dependency>
      <groupId>org.springframework.security.oauth</groupId>
      <artifactId>spring-security-oauth2</artifactId>
   </dependency>
   ```

1. Speichern und schließen Sie die Datei *pom.xml*.

1. Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.

1. Fügen Sie den Schlüssel für Ihr Speicherkonto hinzu. Verwenden Sie dabei den Wert von vorhin. Beispiel:

   ```yaml
   # Specifies your Active Directory Application ID:
   azure.activedirectory.clientId=11111111-1111-1111-1111-1111111111111111

   # Specifies your secret key:
   azure.activedirectory.clientSecret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.activeDirectoryGroups=Users
   ```
   Hinweis:
   | Parameter | BESCHREIBUNG |
   |---|---|
   | `azure.activedirectory.clientId` | Enthält Ihre **Anwendungs-ID** von vorhin. |
   | `azure.activedirectory.clientSecret` | Enthält den Schlüsselwert aus der zuvor durchgeführten App-Registrierung. |
   | `azure.activedirectory.activeDirectoryGroups` | Enthält eine Liste mit Active Directory-Gruppen für die Authentifizierung. |


1. Speichern und schließen Sie die Datei *application.properties*.

1. Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *controller*. Beispiel: *src/main/java/com/wingtiptoys/security/controller*.

1. Erstellen Sie im Ordner *controller* eine neue Java-Datei namens *HelloController.java*, und öffnen Sie sie in einem Text-Editor.

1. Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:

   ```java
   package com.wingtiptoys.security;
   
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.web.authentication.preauth.PreAuthenticatedAuthenticationToken;
   
   @RestController
   public class HelloController {
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String hello() {
         return "Hello World!";
      }
   }
   ```

1. Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *security*. Beispiel: *src/main/java/com/wingtiptoys/security/security*.

1. Erstellen Sie im Ordner *security* eine neue Java-Datei namens *WebSecurityConfig.java*, und öffnen Sie sie in einem Text-Editor.

1. Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:

   ```java
   package com.wingtiptoys.security;

   import com.microsoft.azure.spring.autoconfigure.aad.AADAuthenticationFilter;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.autoconfigure.security.oauth2.client.EnableOAuth2Sso;
   import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
   import org.springframework.security.config.annotation.web.builders.HttpSecurity;
   import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
   import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
   import org.springframework.security.web.csrf.CookieCsrfTokenRepository;
   
   @EnableOAuth2Sso
   @EnableGlobalMethodSecurity(securedEnabled = true, prePostEnabled = true)
   
   public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
      @Autowired
      private AADAuthenticationFilter aadAuthFilter;
      @Override
      protected void configure(HttpSecurity http) throws Exception {
         http.authorizeRequests().anyRequest().permitAll();
         http.addFilterBefore(aadAuthFilter, UsernamePasswordAuthenticationFilter.class);
      }
   }
   ```

## <a name="build-and-test-your-app"></a>Erstellen und Testen der App

1. Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zu dem Ordner, in dem sich die Datei *pom.xml* Ihrer App befindet.

1. Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:

   ```shell
   mvn clean package
   ```

   ![Erstellen Ihrer Anwendung][build-application]

1. Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Nachdem Ihre Anwendung mit Maven erstellt und gestartet wurde, öffnen Sie <http://localhost:8080> in einem Webbrowser.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von Azure Active Directory finden Sie in den folgenden Artikeln:

* [Dokumentation zu Azure Active Directory]

Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:

* [Bereitstellen von Spring Boot-Anwendungen in Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].

**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft. Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen. Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt. Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.

<!-- URL List -->

[Dokumentation zu Azure Active Directory]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure für Java-Entwickler]: https://docs.microsoft.com/java/azure/
[kostenloses Azure-Konto]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools für Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN-Abonnentenvorteile]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

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

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
