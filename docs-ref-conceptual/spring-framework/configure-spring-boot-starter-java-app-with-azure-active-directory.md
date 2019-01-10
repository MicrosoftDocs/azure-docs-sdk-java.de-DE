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
ms.date: 12/19/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: b3d97917deffa75bfab5f0d9ded64affd90139e1
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991394"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="2edfe-103">Tutorial: Schützen einer Java-Web-App mithilfe von Spring Boot Starter für Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2edfe-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="2edfe-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="2edfe-104">Overview</span></span>

<span data-ttu-id="2edfe-105">In diesem Artikel erfahren Sie, wie Sie eine Java-App mit **[Spring Initializr]** erstellen. Spring Initializr verwendet Spring Boot Starter für Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2edfe-105">This article demonstrates creating a Java app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2edfe-106">In diesem Tutorial lernen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="2edfe-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2edfe-107">Erstellen einer Java-Anwendung mit dem Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="2edfe-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="2edfe-108">Konfigurieren von Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2edfe-108">Configure Azure Active Directory</span></span>
> * <span data-ttu-id="2edfe-109">Schützen der Anwendung mit Spring Boot-Klassen und -Anmerkungen</span><span class="sxs-lookup"><span data-stu-id="2edfe-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="2edfe-110">Erstellen und Testen der Java-Anwendung</span><span class="sxs-lookup"><span data-stu-id="2edfe-110">Build and test your Java application</span></span>

<span data-ttu-id="2edfe-111">Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.</span><span class="sxs-lookup"><span data-stu-id="2edfe-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2edfe-112">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="2edfe-112">Prerequisites</span></span>

<span data-ttu-id="2edfe-113">Für die Durchführung der Schritte in diesem Artikel müssen folgende Voraussetzungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="2edfe-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="2edfe-114">Ein unterstütztes Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="2edfe-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="2edfe-115">Weitere Informationen zu den für die Entwicklung in Azure verfügbaren JDKs finden Sie unter <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="2edfe-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="2edfe-116">[Apache Maven](http://maven.apache.org/), Version 3.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="2edfe-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="2edfe-117">Erstellen einer App mithilfe von Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="2edfe-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="2edfe-118">Navigieren Sie zu <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="2edfe-118">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="2edfe-119">Geben Sie an, dass Sie ein **Maven**-Projekt mit **Java** generieren möchten, geben Sie die Namen für **Gruppe** und **Artefakt** für Ihre Anwendung ein, und klicken Sie dann auf den Link, um zur **Vollversion von Spring Initializr zu wechseln**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Angeben von Gruppen- und Artefaktnamen][create-spring-app-01]

1. <span data-ttu-id="2edfe-121">Scrollen Sie nach unten zum Abschnitt **Core**, und aktivieren Sie das Kontrollkästchen **Sicherheit** und im Abschnitt **Web** das Kontrollkästchen **Web**. Scrollen Sie anschließend nach unten zum Abschnitt **Azure**, und aktivieren Sie das Kontrollkästchen für **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-121">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**, then scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Auswählen der Starter-Optionen „Sicherheit“, „Web“ und „Azure Active Directory“][create-spring-app-02]

1. <span data-ttu-id="2edfe-123">Klicken Sie am oberen oder unteren Seitenrand auf die Schaltfläche **Projekt generieren**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-123">Scroll to the top or bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generieren eines Spring Boot-Projekts][create-spring-app-03]

1. <span data-ttu-id="2edfe-125">Laden Sie das Projekt nach entsprechender Aufforderung unter einem Pfad auf dem lokalen Computer herunter.</span><span class="sxs-lookup"><span data-stu-id="2edfe-125">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="2edfe-126">Erstellen einer Azure Active Directory-Instanz</span><span class="sxs-lookup"><span data-stu-id="2edfe-126">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="2edfe-127">Erstellen der Active Directory-Instanz</span><span class="sxs-lookup"><span data-stu-id="2edfe-127">Create the Active Directory instance</span></span>

1. <span data-ttu-id="2edfe-128">Melden Sie sich bei <https://portal.azure.com> an.</span><span class="sxs-lookup"><span data-stu-id="2edfe-128">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="2edfe-129">Klicken Sie auf **+Ressource erstellen**, **Identität** und dann auf **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-129">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory**.</span></span>

   ![Erstellen einer neuen Azure Active Directory-Instanz][create-directory-01]

1. <span data-ttu-id="2edfe-131">Geben Sie Werte für **Name der Organisation** und **Name der Anfangsdomäne** ein.</span><span class="sxs-lookup"><span data-stu-id="2edfe-131">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="2edfe-132">Kopieren Sie die vollständige URL Ihres Verzeichnisses. Sie verwenden diese später in diesem Tutorial zum Hinzufügen von Benutzerkonten.</span><span class="sxs-lookup"><span data-stu-id="2edfe-132">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="2edfe-133">(Beispiel: `wingtiptoysdirectory.onmicrosoft.com`.) Wenn Sie fertig sind, klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-133">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Angeben von Azure Active Directory-Namen][create-directory-02]

1. <span data-ttu-id="2edfe-135">Wählen Sie im Azure-Portal auf der Symbolleiste oben rechts Ihren Kontonamen aus, und klicken Sie dann auf **Verzeichnis wechseln**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-135">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Auswählen Ihres Azure-Kontonamens][create-directory-03]

1. <span data-ttu-id="2edfe-137">Wählen Sie im Dropdownmenü Ihre neue Azure Active Directory-Instanz aus.</span><span class="sxs-lookup"><span data-stu-id="2edfe-137">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Auswählen Ihrer Azure Active Directory-Instanz][create-directory-04]

1. <span data-ttu-id="2edfe-139">Wählen Sie im Portalmenü **Azure Active Directory**, klicken Sie auf **Eigenschaften**, und kopieren Sie die **Verzeichnis-ID**. Diesen Wert verwenden Sie später in diesem Tutorial zum Konfigurieren Ihrer Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="2edfe-139">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Kopieren der Azure Active Directory-ID][create-directory-05]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="2edfe-141">Hinzufügen einer Anwendungsregistrierung für Ihre Spring Boot-App</span><span class="sxs-lookup"><span data-stu-id="2edfe-141">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="2edfe-142">Wählen Sie im Portalmenü die Option **Azure Active Directory** aus, und klicken Sie anschließend auf **App-Registrierungen** > **Registrierung einer neuen Anwendung**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-142">Select **Azure Active Directory** from the portal menu, click **App registrations**, and then click **New application registration**, .</span></span>

   ![Hinzufügen einer neuen App-Registrierung][create-app-registration-01]

2. <span data-ttu-id="2edfe-144">Wählen Sie unter **Name** den Namen Ihrer Anwendung aus, geben Sie für die http://localhost:8080Anmelde-URL**den Wert** an, und klicken Sie anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-144">Specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Erstellen einer neuen App-Registrierung][create-app-registration-02]

4. <span data-ttu-id="2edfe-146">Wenn die Seite für Ihre App-Registrierung angezeigt wird, kopieren Sie Ihre **Anwendungs-ID**. Diesen Wert verwenden Sie später in diesem Tutorial zum Konfigurieren Ihrer Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="2edfe-146">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="2edfe-147">Klicken Sie auf **Einstellungen** und dann auf **Schlüssel**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-147">Click **Settings**, and then click **Keys**.</span></span>

   ![Erstellen von App-Registrierungsschlüsseln][create-app-registration-03]

5. <span data-ttu-id="2edfe-149">Fügen Sie eine **Beschreibung** hinzu, geben Sie die **Dauer** für einen neuen Schlüssel an, und klicken Sie auf **Speichern**. Der Wert für den Schlüssel wird nach dem Klicken auf das Symbol **Speichern** automatisch ausgefüllt. Notieren Sie sich den Wert des Schlüssels, um später in diesem Tutorial Ihre Datei *application.properties* damit zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="2edfe-149">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="2edfe-150">(Dieser Wert kann später nicht mehr abgerufen werden.)</span><span class="sxs-lookup"><span data-stu-id="2edfe-150">(You will not be able to retrieve this value later.)</span></span>

   ![Angeben von Parametern für App-Registrierungsschlüssel][create-app-registration-04]

6. <span data-ttu-id="2edfe-152">Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Einstellungen** und anschließend auf **Erforderliche Berechtigungen**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-152">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Erforderliche Berechtigungen für die App-Registrierung][create-app-registration-05]

7. <span data-ttu-id="2edfe-154">Klicken Sie auf **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-154">Click **Windows Azure Active Directory**.</span></span>

   ![Auswählen von „Windows Azure Active Directory“][create-app-registration-06]

8. <span data-ttu-id="2edfe-156">Aktivieren Sie die Kontrollkästchen **Hiermit greifen Sie als angemeldeter Benutzer auf das Verzeichnis zu.** und **Anmelden und Benutzerprofil lesen**, und klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-156">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Aktivieren von Zugriffsberechtigungen][create-app-registration-07]

9. <span data-ttu-id="2edfe-158">Klicken Sie auf der Seite **Erforderliche Berechtigungen** auf **Berechtigungen erteilen** und anschließend auf **Ja**, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="2edfe-158">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Erteilen von Zugriffsberechtigungen][create-app-registration-08]

10. <span data-ttu-id="2edfe-160">Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Einstellungen** und anschließend auf **Antwort-URLs**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-160">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![Bearbeiten der Antwort-URLs][create-app-registration-09]

11. <span data-ttu-id="2edfe-162">Geben Sie <http://localhost:8080/login/oauth2/code/azure> als neue Antwort-URL ein, und klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-162">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![Hinzufügen einer neuen Antwort-URL][create-app-registration-10]

12. <span data-ttu-id="2edfe-164">Klicken Sie auf der Hauptseite für Ihre App-Registrierung auf **Manifest**, legen Sie den Wert des `oauth2AllowImplicitFlow`-Parameters auf `true` fest, und klicken Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-164">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![App-Manifest konfigurieren][create-app-registration-11]

    > [!NOTE]
    > 
    > <span data-ttu-id="2edfe-166">Weitere Informationen zum `oauth2AllowImplicitFlow`-Parameter und anderen Anwendungseinstellungen finden Sie unter [Azure Active Directory-Anwendungsmanifest][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="2edfe-166">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="2edfe-167">Hinzufügen eines Benutzerkontos zu Ihrem Verzeichnis und Hinzufügen dieses Kontos zu einer Gruppe</span><span class="sxs-lookup"><span data-stu-id="2edfe-167">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="2edfe-168">Klicken Sie auf der Seite **Übersicht** Ihrer Active Directory-Instanz auf **Alle Benutzer** und dann auf **Neuer Benutzer**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-168">From the **Overview** page of your Active Directory, click **All Users**, and then click **New user**.</span></span>

   ![Hinzufügen eines neuen Benutzerkontos][create-user-01]

1. <span data-ttu-id="2edfe-170">Wenn der Bereich **Benutzer** angezeigt wird, geben Sie den **Namen** und den **Benutzernamen** ein.</span><span class="sxs-lookup"><span data-stu-id="2edfe-170">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Eingeben der Benutzerkontoinformationen][create-user-02]

   > [!NOTE]
   > 
   > <span data-ttu-id="2edfe-172">Sie müssen die Verzeichnis-URL von weiter oben in diesem Tutorial eingeben, wenn Sie den Benutzernamen eingeben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="2edfe-172">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="2edfe-173">Klicken Sie auf **Gruppen**, wählen Sie dann die Gruppen aus, die Sie für die Autorisierung in Ihrer Anwendung verwenden, und klicken Sie dann auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="2edfe-173">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="2edfe-174">(Fügen Sie in diesem Tutorial das Konto der Gruppe _Benutzer_ hinzu.)</span><span class="sxs-lookup"><span data-stu-id="2edfe-174">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Auswählen der Gruppen des Benutzers][create-user-03]

1. <span data-ttu-id="2edfe-176">Klicken Sie auf **Kennwort anzeigen**, und kopieren Sie das Kennwort, Sie verwenden es später in diesem Tutorial für die Anmeldung bei Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="2edfe-176">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span> <span data-ttu-id="2edfe-177">Klicken Sie nach dem Kopieren des Kennworts auf **Erstellen**, um das neue Benutzerkonto Ihrem Verzeichnis hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="2edfe-177">When you have copied the password, click **Create** to add the new user account to your directory.</span></span>

   ![Anzeigen des Kennworts][create-user-04]

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="2edfe-179">Konfigurieren und Kompilieren Ihrer App</span><span class="sxs-lookup"><span data-stu-id="2edfe-179">Configure and compile your app</span></span>

1. <span data-ttu-id="2edfe-180">Extrahieren Sie die Dateien aus dem Projektarchiv, das Sie zuvor in diesem Tutorial erstellt und heruntergeladen haben, in ein Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="2edfe-180">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="2edfe-181">Navigieren Sie zum übergeordneten Ordner für Ihr Projekt, und öffnen Sie die Maven-Projektdatei `pom.xml` in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="2edfe-181">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

1. <span data-ttu-id="2edfe-182">Fügen Sie die Abhängigkeiten für Spring OAuth2-Sicherheit zu `pom.xml` hinzu:</span><span class="sxs-lookup"><span data-stu-id="2edfe-182">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

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

1. <span data-ttu-id="2edfe-183">Speichern und schließen Sie die Datei *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="2edfe-183">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="2edfe-184">Navigieren Sie in Ihrem Projekt zum Ordner *src/main/resources*, und öffnen Sie die Datei *application.properties* in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="2edfe-184">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="2edfe-185">Geben Sie die Einstellungen für Ihre App-Registrierung mithilfe der zuvor erstellten Werte an. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="2edfe-185">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="2edfe-186">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="2edfe-186">Where:</span></span>

   | <span data-ttu-id="2edfe-187">Parameter</span><span class="sxs-lookup"><span data-stu-id="2edfe-187">Parameter</span></span> | <span data-ttu-id="2edfe-188">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="2edfe-188">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="2edfe-189">Enthält die **Verzeichnis-ID** Ihrer Active Directory-Instanz von vorhin.</span><span class="sxs-lookup"><span data-stu-id="2edfe-189">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="2edfe-190">Enthält die **Anwendungs-ID** aus der zuvor durchgeführten App-Registrierung.</span><span class="sxs-lookup"><span data-stu-id="2edfe-190">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="2edfe-191">Enthält den **Wert** aus dem zuvor erstellten App-Registrierungsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="2edfe-191">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="2edfe-192">Enthält eine Liste mit Active Directory-Gruppen für die Autorisierung.</span><span class="sxs-lookup"><span data-stu-id="2edfe-192">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="2edfe-193">Eine vollständige Liste mit verfügbaren Werten in der Datei *application.properties* finden Sie im [Spring Boot-Beispiel für Azure Active Directory][AAD Spring Boot Sample] auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="2edfe-193">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="2edfe-194">Speichern und schließen Sie die Datei *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="2edfe-194">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="2edfe-195">Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *controller*. Beispiel: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="2edfe-195">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="2edfe-196">Erstellen Sie im Ordner *controller* eine neue Java-Datei namens *HelloController.java*, und öffnen Sie sie in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="2edfe-196">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="2edfe-197">Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:</span><span class="sxs-lookup"><span data-stu-id="2edfe-197">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="2edfe-198">Der Gruppenname, den Sie für die Methode `@PreAuthorize("hasRole('')")` angeben, muss eine der Gruppen enthalten, die Sie im Feld `azure.activedirectory.active-directory-groups` der Datei *application.properties* angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="2edfe-198">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   > 
   > <span data-ttu-id="2edfe-199">Sie können auch verschiedene Autorisierungseinstellungen für verschiedene Anforderungszuordnungen angeben. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="2edfe-199">You can also specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="2edfe-200">Erstellen Sie im Java-Quellordner für Ihre Anwendung einen Ordner namens *security*. Beispiel: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="2edfe-200">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="2edfe-201">Erstellen Sie im Ordner *security* eine neue Java-Datei namens *WebSecurityConfig.java*, und öffnen Sie sie in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="2edfe-201">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="2edfe-202">Geben Sie den folgenden Code ein, speichern Sie die Datei, und schließen Sie sie:</span><span class="sxs-lookup"><span data-stu-id="2edfe-202">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="2edfe-203">Erstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="2edfe-203">Build and test your app</span></span>

1. <span data-ttu-id="2edfe-204">Öffnen Sie eine Eingabeaufforderung, und wechseln Sie zu dem Ordner, in dem sich die Datei *pom.xml* Ihrer App befindet.</span><span class="sxs-lookup"><span data-stu-id="2edfe-204">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="2edfe-205">Erstellen Sie mit Maven die Spring Boot-Anwendung, und führen Sie sie aus. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="2edfe-205">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Erstellen Ihrer Anwendung][build-application]

1. <span data-ttu-id="2edfe-207">Nachdem Ihre Anwendung durch Maven erstellt und gestartet wurde, öffnen Sie <http://localhost:8080> in einem Webbrowser. Daraufhin sollten Sie zur Eingabe eines Benutzernamens und eines Kennworts aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="2edfe-207">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Anmelden bei Ihrer Anwendung][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="2edfe-209">Wenn dies die erste Anmeldung für ein neues Benutzerkonto ist, werden Sie möglicherweise zum Ändern Ihres Kennworts aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="2edfe-209">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Ändern des Kennworts][update-password]
   > 

1. <span data-ttu-id="2edfe-211">Nach erfolgreicher Anmeldung sollte der Beispieltext „Hello World“ des Controllers angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="2edfe-211">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Erfolgreiche Anmeldung][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="2edfe-213">Für nicht autorisierte Benutzerkonten wird eine Meldung vom Typ **HTTP 403 (nicht autorisiert)** zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="2edfe-213">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="summary"></a><span data-ttu-id="2edfe-214">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="2edfe-214">Summary</span></span>

<span data-ttu-id="2edfe-215">In diesem Tutorial haben Sie mit Azure Active Directory Starter eine neue Java-Webanwendung erstellt, einen neuen Azure AD-Mandanten konfiguriert und eine neue Anwendung darin registriert. Anschließend haben Sie Ihre Anwendung zur Verwendung der Spring-Anmerkungen und -Klassen zum Schützen der Web-App konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="2edfe-215">In this tutorial, you created a new Java web application using the Azure Active Directory starter, configured a new Azure AD tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2edfe-216">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="2edfe-216">Next steps</span></span>

<span data-ttu-id="2edfe-217">Weitere Informationen zu Spring und Azure finden Sie im Dokumentationscenter zu Spring in Azure.</span><span class="sxs-lookup"><span data-stu-id="2edfe-217">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2edfe-218">Spring Framework in Azure</span><span class="sxs-lookup"><span data-stu-id="2edfe-218">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure for Java Developers]: /java/azure/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[create-spring-app-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-01.png
[create-spring-app-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-02.png
[create-spring-app-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-03.png

[create-directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-01.png
[create-directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-02.png
[create-directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-03.png
[create-directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-04.png
[create-directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-05.png

[create-app-registration-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-01.png
[create-app-registration-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-02.png
[create-app-registration-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-03.png
[create-app-registration-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-04.png
[create-app-registration-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-05.png
[create-app-registration-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-06.png
[create-app-registration-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-07.png
[create-app-registration-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-08.png
[create-app-registration-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-09.png
[create-app-registration-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-10.png
[create-app-registration-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-11.png

[create-user-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-01.png
[create-user-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-02.png
[create-user-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-03.png
[create-user-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-04.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
