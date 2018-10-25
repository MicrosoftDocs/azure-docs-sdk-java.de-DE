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
ms.openlocfilehash: 665768ffe7bec977d553ffa62e1dbd6b968eb9de
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799906"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="5c164-103">Verwenden von Spring Boot Starter für Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c164-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="5c164-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="5c164-104">Overview</span></span>

<span data-ttu-id="5c164-105">In diesem Artikel erfahren Sie, wie Sie eine App mit **[Spring Initializr]** erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c164-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c164-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="5c164-106">Prerequisites</span></span>

<span data-ttu-id="5c164-107">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="5c164-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="5c164-108">Ein Azure-Abonnement – wenn Sie noch kein Azure-Abonnement besitzen, können Sie Ihre [Vorteile für MSDN-Abonnenten] anwenden oder sich für ein [Kostenloses Azure-Konto] registrieren</span><span class="sxs-lookup"><span data-stu-id="5c164-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="5c164-109">[Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), Version 1.7 oder höher</span><span class="sxs-lookup"><span data-stu-id="5c164-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="5c164-110">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="5c164-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="5c164-111">Erstellen einer benutzerdefinierten Anwendung mit dem Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="5c164-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="5c164-112">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="5c164-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="5c164-113">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.</span><span class="sxs-lookup"><span data-stu-id="5c164-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Angeben von Gruppen- und Artefaktnamen][security-01]

1. <span data-ttu-id="5c164-115">Aktivieren Sie im Abschnitt **Core** das Kontrollkästchen für **Sicherheit** und im Abschnitt **Web** das Kontrollkästchen für **Web**.</span><span class="sxs-lookup"><span data-stu-id="5c164-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Auswählen der Starter für Sicherheit und Web][security-02]

1. <span data-ttu-id="5c164-117">Scrollen Sie nach unten zum Abschnitt **Azure**, und aktivieren Sie das Kontrollkästchen für **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c164-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Auswählen des Starters für Azure Active Directory][security-03]

1. <span data-ttu-id="5c164-119">Klicken Sie am unteren Seitenrand auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="5c164-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generieren eines Spring Boot-Projekts][security-04]

1. <span data-ttu-id="5c164-121">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="5c164-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="5c164-122">Erstellen und Konfigurieren einer neuen Azure Active Directory-Instanz</span><span class="sxs-lookup"><span data-stu-id="5c164-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="5c164-123">Erstellen der Active Directory-Instanz</span><span class="sxs-lookup"><span data-stu-id="5c164-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="5c164-124">Melden Sie sich bei <https://portal.azure.com> an.</span><span class="sxs-lookup"><span data-stu-id="5c164-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="5c164-125">Klicken Sie auf **+Neu** > **Sicherheit + Identität** > **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c164-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Erstellen einer neuen Azure Active Directory-Instanz][directory-01]

1. <span data-ttu-id="5c164-127">Geben Sie Werte für **Name der Organisation** und **Name der Anfangsdomäne** ein.</span><span class="sxs-lookup"><span data-stu-id="5c164-127">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="5c164-128">Kopieren Sie die vollständige URL Ihres Verzeichnisses. Sie verwenden diese später in diesem Tutorial zum Hinzufügen von Benutzerkonten.</span><span class="sxs-lookup"><span data-stu-id="5c164-128">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="5c164-129">(Beispiel: `wingtiptoysdirectory.onmicrosoft.com`.) Wenn Sie fertig sind, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5c164-129">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Angeben von Azure Active Directory-Namen][directory-02]

1. <span data-ttu-id="5c164-131">Wählen Sie im Dropdownmenü auf der oberen Symbolleiste des Azure-Portals Ihre neue Azure Active Directory-Instanz aus.</span><span class="sxs-lookup"><span data-stu-id="5c164-131">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Auswählen Ihrer Azure Active Directory-Instanz][directory-03]

1. <span data-ttu-id="5c164-133">Wählen Sie im Portalmenü **Azure Active Directory**, klicken Sie auf **Eigenschaften**, und kopieren Sie die **Verzeichnis-ID**. Diesen Wert verwenden Sie später in diesem Tutorial zum Konfigurieren Ihrer Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="5c164-133">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Kopieren der Azure Active Directory-ID][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="5c164-135">Hinzufügen einer Anwendungsregistrierung für Ihre Spring Boot-App</span><span class="sxs-lookup"><span data-stu-id="5c164-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="5c164-136">Wählen Sie im Portalmenü die Option **Azure Active Directory** aus, und klicken Sie anschließend auf **Übersicht** > **App-Registrierungen**.</span><span class="sxs-lookup"><span data-stu-id="5c164-136">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Hinzufügen einer neuen App-Registrierung][directory-04]

2. <span data-ttu-id="5c164-138">Klicken Sie auf **Registrierung einer neuen Anwendung**, geben Sie unter **Name** den Namen Ihrer Anwendung an, geben Sie für die **Anmelde-URL** den Wert http://localhost:8080 an, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5c164-138">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Erstellen einer neuen App-Registrierung][directory-05]

3. <span data-ttu-id="5c164-140">Klicken Sie nach Abschluss der Erstellung auf Ihre Anwendungsregistrierung.</span><span class="sxs-lookup"><span data-stu-id="5c164-140">Click your application registration after it has been created.</span></span>

   ![Auswählen Ihrer App-Registrierung][directory-06]

4. <span data-ttu-id="5c164-142">Wenn die Seite für Ihre App-Registrierung angezeigt wird, kopieren Sie Ihre **Anwendungs-ID**. Diesen Wert verwenden Sie später in diesem Tutorial zum Konfigurieren Ihrer Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="5c164-142">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="5c164-143">Klicken Sie auf **Einstellungen** und dann auf **Schlüssel**.</span><span class="sxs-lookup"><span data-stu-id="5c164-143">Click **Settings**, and then click **Keys**.</span></span>

   ![Erstellen von App-Registrierungsschlüsseln][directory-07]

5. <span data-ttu-id="5c164-145">Fügen Sie eine **Beschreibung** hinzu, geben Sie die **Dauer** für einen neuen Schlüssel an, und klicken Sie auf **Speichern**. Der Wert für den Schlüssel wird nach dem Klicken auf das Symbol **Speichern** automatisch ausgefüllt. Notieren Sie sich den Wert des Schlüssels, um später in diesem Tutorial Ihre Datei *application.properties* damit zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="5c164-145">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="5c164-146">(Dieser Wert kann später nicht mehr abgerufen werden.)</span><span class="sxs-lookup"><span data-stu-id="5c164-146">(You will not be able to retrieve this value later.)</span></span>

   ![Angeben von Parametern für App-Registrierungsschlüssel][directory-08]

6. <span data-ttu-id="5c164-148">Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Einstellungen** und anschließend auf **Erforderliche Berechtigungen**.</span><span class="sxs-lookup"><span data-stu-id="5c164-148">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Erforderliche Berechtigungen für die App-Registrierung][directory-09]

7. <span data-ttu-id="5c164-150">Klicken Sie auf **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c164-150">Click **Windows Azure Active Directory**.</span></span>

   ![Auswählen von „Windows Azure Active Directory“][directory-10]

8. <span data-ttu-id="5c164-152">Aktivieren Sie die Kontrollkästchen **Hiermit greifen Sie als angemeldeter Benutzer auf das Verzeichnis zu.** und **Anmelden und Benutzerprofil lesen**, und klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="5c164-152">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Aktivieren von Zugriffsberechtigungen][directory-11]

9. <span data-ttu-id="5c164-154">Klicken Sie auf der Seite **Erforderliche Berechtigungen** auf **Berechtigungen erteilen** und anschließend auf **Ja**, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="5c164-154">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Erteilen von Zugriffsberechtigungen][directory-12]

10. <span data-ttu-id="5c164-156">Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Einstellungen** und anschließend auf **Antwort-URLs**.</span><span class="sxs-lookup"><span data-stu-id="5c164-156">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![Bearbeiten der Antwort-URLs][directory-14]

11. <span data-ttu-id="5c164-158">Geben Sie <http://localhost:8080/login/oauth2/code/azure> als neue Antwort-URL ein, und klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="5c164-158">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![Hinzufügen einer neuen Antwort-URL][directory-15]

12. <span data-ttu-id="5c164-160">Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Manifest**, legen Sie den Wert des `oauth2AllowImplicitFlow`-Parameters auf `true` fest, und klicken Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="5c164-160">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![App-Manifest konfigurieren][directory-16]

    > [!NOTE]
    > 
    > <span data-ttu-id="5c164-162">Weitere Informationen zum `oauth2AllowImplicitFlow`-Parameter und anderen Anwendungseinstellungen finden Sie unter [Azure Active Directory-Anwendungsmanifest][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="5c164-162">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="5c164-163">Hinzufügen eines Benutzerkontos zu Ihrem Verzeichnis und Hinzufügen dieses Kontos zu einer Gruppe</span><span class="sxs-lookup"><span data-stu-id="5c164-163">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="5c164-164">Klicken Sie auf der Seite **Übersicht** Ihrer Active Directory-Instanz auf **Benutzer**.</span><span class="sxs-lookup"><span data-stu-id="5c164-164">From the **Overview** page of your Active Directory, click **Users**.</span></span>

   ![Öffnen des Bereichs „Benutzer“][directory-17]

1. <span data-ttu-id="5c164-166">Wenn der Bereich **Benutzer** angezeigt wird, klicken Sie auf **Neuer Benutzer**.</span><span class="sxs-lookup"><span data-stu-id="5c164-166">When the **Users** panel is displayed, click **New user**.</span></span>

   ![Hinzufügen eines neuen Benutzerkontos][directory-18]

1. <span data-ttu-id="5c164-168">Wenn der Bereich **Benutzer** angezeigt wird, geben Sie den **Namen** und den **Benutzernamen** ein.</span><span class="sxs-lookup"><span data-stu-id="5c164-168">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Eingeben der Benutzerkontoinformationen][directory-19]

   > [!NOTE]
   > 
   > <span data-ttu-id="5c164-170">Sie müssen die Verzeichnis-URL von weiter oben in diesem Tutorial eingeben, wenn Sie den Benutzernamen eingeben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="5c164-170">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="5c164-171">Klicken Sie auf **Gruppen**, wählen Sie dann die Gruppen aus, die Sie für die Autorisierung in Ihrer Anwendung verwenden, und klicken Sie dann auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="5c164-171">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="5c164-172">(Fügen Sie in diesem Tutorial das Konto der Gruppe _Benutzer_ hinzu.)</span><span class="sxs-lookup"><span data-stu-id="5c164-172">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Auswählen der Gruppen des Benutzers][directory-20]

1. <span data-ttu-id="5c164-174">Klicken Sie auf **Kennwort anzeigen**, und kopieren Sie das Kennwort, Sie verwenden es später in diesem Tutorial für die Anmeldung bei Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="5c164-174">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span>

   ![Anzeigen des Kennworts][directory-21]

1. <span data-ttu-id="5c164-176">Klicken Sie auf **Erstellen** um das neue Benutzerkonto Ihrem Verzeichnis hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="5c164-176">Click **Create** to add the new user account to your directory.</span></span>

   ![Erstellen des neuen Benutzerkontos][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="5c164-178">Konfigurieren und Kompilieren Ihrer Spring Boot-Anwendung</span><span class="sxs-lookup"><span data-stu-id="5c164-178">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="5c164-179">Extrahieren Sie die Dateien aus dem Projektarchiv, das Sie zuvor in diesem Tutorial erstellt und heruntergeladen haben, in ein Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="5c164-179">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="5c164-180">Navigieren Sie zum übergeordneten Ordner für Ihr Projekt, und öffnen Sie die Datei *pom.xml* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="5c164-180">Navigate to the parent folder for your project, and open the *pom.xml* file in a text editor.</span></span>

1. <span data-ttu-id="5c164-181">Fügen Sie die Abhängigkeiten für Spring OAuth2-Sicherheit hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="5c164-181">Add the dependencies for Spring OAuth2 security; for example:</span></span>

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

1. <span data-ttu-id="5c164-182">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="5c164-182">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="5c164-183">Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="5c164-183">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="5c164-184">Geben Sie die Einstellungen für Ihre App-Registrierung mithilfe der zuvor erstellten Werte an. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="5c164-184">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="5c164-185">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="5c164-185">Where:</span></span>

   | <span data-ttu-id="5c164-186">Parameter</span><span class="sxs-lookup"><span data-stu-id="5c164-186">Parameter</span></span> | <span data-ttu-id="5c164-187">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="5c164-187">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="5c164-188">Enthält die **Verzeichnis-ID** Ihrer Active Directory-Instanz von vorhin.</span><span class="sxs-lookup"><span data-stu-id="5c164-188">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="5c164-189">Enthält die **Anwendungs-ID** aus der zuvor durchgeführten App-Registrierung.</span><span class="sxs-lookup"><span data-stu-id="5c164-189">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="5c164-190">Enthält den **Wert** aus dem zuvor erstellten App-Registrierungsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="5c164-190">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="5c164-191">Enthält eine Liste mit Active Directory-Gruppen für die Autorisierung.</span><span class="sxs-lookup"><span data-stu-id="5c164-191">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="5c164-192">Eine vollständige Liste mit verfügbaren Werten in der Datei *application.properties* finden Sie im [Spring Boot-Beispiel für Azure Active Directory][AAD Spring Boot Sample] auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="5c164-192">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="5c164-193">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="5c164-193">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="5c164-194">Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *controller*. Beispiel: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="5c164-194">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="5c164-195">Erstellen Sie im Ordner *controller* eine neue Java-Datei namens *HelloController.java*, und öffnen Sie sie in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="5c164-195">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="5c164-196">Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:</span><span class="sxs-lookup"><span data-stu-id="5c164-196">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="5c164-197">Der Gruppenname, den Sie für die Methode `@PreAuthorize("hasRole('')")` angeben, muss eine der Gruppen enthalten, die Sie im Feld `azure.activedirectory.active-directory-groups` der Datei *application.properties* angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="5c164-197">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="5c164-198">Sie können verschiedene Autorisierungseinstellungen für verschiedene Anforderungszuordnungen angeben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="5c164-198">You can specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="5c164-199">Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *security*. Beispiel: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="5c164-199">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="5c164-200">Erstellen Sie im Ordner *security* eine neue Java-Datei namens *WebSecurityConfig.java*, und öffnen Sie sie in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="5c164-200">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="5c164-201">Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:</span><span class="sxs-lookup"><span data-stu-id="5c164-201">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="5c164-202">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="5c164-202">Build and test your app</span></span>

1. <span data-ttu-id="5c164-203">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zu dem Ordner, in dem sich die Datei *pom.xml* Ihrer App befindet.</span><span class="sxs-lookup"><span data-stu-id="5c164-203">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="5c164-204">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="5c164-204">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Erstellen Ihrer Anwendung][build-application]

1. <span data-ttu-id="5c164-206">Nachdem Ihre Anwendung durch Maven erstellt und gestartet wurde, öffnen Sie <http://localhost:8080> in einem Webbrowser. Daraufhin sollten Sie zur Eingabe eines Benutzernamens und eines Kennworts aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="5c164-206">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Anmelden bei Ihrer Anwendung][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="5c164-208">Wenn dies die erste Anmeldung für ein neues Benutzerkonto ist, werden Sie möglicherweise zum Ändern Ihres Kennworts aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="5c164-208">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Ändern des Kennworts][update-password]
   > 

1. <span data-ttu-id="5c164-210">Nach erfolgreicher Anmeldung sollte der Beispieltext „Hello World“ des Controllers angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="5c164-210">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Erfolgreiche Anmeldung][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="5c164-212">Für nicht autorisierte Benutzerkonten wird eine Meldung vom Typ **HTTP 403 (nicht autorisiert)** zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="5c164-212">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="5c164-213">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="5c164-213">Next steps</span></span>

<span data-ttu-id="5c164-214">Weitere Informationen zur Verwendung von Azure Active Directory finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="5c164-214">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="5c164-215">[Azure Active Directory-Dokumentation]</span><span class="sxs-lookup"><span data-stu-id="5c164-215">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="5c164-216">Weitere Informationen zur Verwendung von Spring Boot-Anwendungen in Azure finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="5c164-216">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="5c164-217">Bereitstellen von Spring Boot-Anwendungen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5c164-217">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="5c164-218">Ausführen einer Spring Boot-Anwendung in einem Kubernetes-Cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="5c164-218">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="5c164-219">Weitere Informationen zum Verwenden von Azure mit Java finden Sie unter [Azure für Java-Entwickler] und im Thema zu den [Java-Tools für Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="5c164-219">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="5c164-220">**[Spring Framework]** ist eine Open-Source-Lösung, die Java-Entwicklern beim Erstellen von Anwendungen auf Unternehmensebene hilft.</span><span class="sxs-lookup"><span data-stu-id="5c164-220">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="5c164-221">Eines der gängigsten Projekte, das auf dieser Plattform aufbaut, ist [Spring Boot]. Es bietet einen vereinfachten Ansatz für das Erstellen eigenständiger Java-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="5c164-221">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="5c164-222">Um Entwicklern den Einstieg in Spring Boot zu vereinfachen, werden unter <https://github.com/spring-guides/> mehrere Spring Boot-Beispielpakete bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="5c164-222">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="5c164-223">Neben der Auswahl einer Liste grundlegender Spring Boot-Projekte ermöglicht **[Spring Initializr]** Entwicklern einen einfacheren Einstieg bei der Erstellung von benutzerdefinierten Spring Boot-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="5c164-223">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="5c164-224">Ein ausführlicheres Beispiel finden Sie im [Spring Boot-Beispiel für Azure Active Directory][AAD Spring Boot Sample] auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="5c164-224">For a more-detailed sample, see the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>

<!-- URL List -->

[Azure Active Directory-Dokumentation]: /azure/active-directory/
[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure für Java-Entwickler]: /java/azure/
[Azure for Java Developers]: /java/azure/
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
