---
title: Azure Active Directory-Bibliotheken für Java
description: Referenzdokumentation für die Azure Active Directory-Clientbibliotheken und -Verwaltungsbibliotheken für Java
keywords: Azure, Java, SDK, API, SQL, Authentifizierung, AAD, Active Directory, Graph, OAuth 2.0
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: active-directory
ms.openlocfilehash: 28063a1a4299fd78ba76533d0ffdc0346434eea2
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="azure-active-directory-libraries-for-java"></a><span data-ttu-id="ca39e-104">Azure Active Directory-Bibliotheken für Java</span><span class="sxs-lookup"><span data-stu-id="ca39e-104">Azure Active Directory libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="ca39e-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="ca39e-105">Overview</span></span>

<span data-ttu-id="ca39e-106">Mit [Azure Active Directory](/azure/active-directory/active-directory-whatis) können Sie Benutzer anmelden und den Zugriff auf Anwendungen und APIs steuern.</span><span class="sxs-lookup"><span data-stu-id="ca39e-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

<span data-ttu-id="ca39e-107">Informationen zu den ersten Schritten mit Azure AD finden Sie unter [An- und Abmeldung bei Java-Web-Apps mit Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span><span class="sxs-lookup"><span data-stu-id="ca39e-107">To get started with Azure AD, see [Java web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="ca39e-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="ca39e-108">Client library</span></span>

<span data-ttu-id="ca39e-109">Konfigurieren Sie OAuth2-, OpenID Connect- oder Active Directory Graph-Authentifizierung und [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)-SSO mit der [Azure Active Directory-Authentifizierungsbibliothek (ADAL) für Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span><span class="sxs-lookup"><span data-stu-id="ca39e-109">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span></span>

<span data-ttu-id="ca39e-110">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ca39e-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="ca39e-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ca39e-111">Example</span></span>

<span data-ttu-id="ca39e-112">Rufen Sie mit der [Graph-API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) von Azure Active Directory ein JSON-Webtoken (JWT) für einen Benutzer in Ihrem Active Directory-Mandanten ab.</span><span class="sxs-lookup"><span data-stu-id="ca39e-112">Retrieve a JSON Web Token (JWT) for a user in your an Active Directory tenant using Azure Active Directory's [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api).</span></span> <span data-ttu-id="ca39e-113">Dieses Token kann dann zur Authentifizierung des Benutzers bei einer Anwendung oder API verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ca39e-113">This token can then be used to authenticate the user with an application or API.</span></span>

```java
ExecutorService service = Executors.newFixedThreadPool(1);
AuthenticationContext context = new AuthenticationContext(AUTHORITY, false, service);
Future<AuthenticationResult> future = context.acquireToken(
    "https://graph.windows.net", YOUR_TENANT_ID, username, password,
    null);
AuthenticationResult result = future.get();
System.out.println("Access Token - " + result.getAccessToken());
System.out.println("Refresh Token - " + result.getRefreshToken());
System.out.println("ID Token - " + result.getIdToken());
```

## <a name="management-api"></a><span data-ttu-id="ca39e-114">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="ca39e-114">Management API</span></span>

<span data-ttu-id="ca39e-115">Konfigurieren Sie die [rollenbasierte Zugriffssteuerung](/azure/active-directory/role-based-access-control-what-is), und weisen Sie diesen Rollen dann mit der Verwaltungs-API Identitäten (z.B. Benutzer und [Dienstprinzipale](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) zu.</span><span class="sxs-lookup"><span data-stu-id="ca39e-115">Configure [role based access control](/azure/active-directory/role-based-access-control-what-is) and assign identities (such as users and [service principals](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) to those roles with the management API.</span></span> 

<span data-ttu-id="ca39e-116">Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ca39e-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="ca39e-117">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ca39e-117">Example</span></span> 

<span data-ttu-id="ca39e-118">Erstellen Sie einen neuen Dienstprinzipal, und weisen Sie ihn der Rolle „Mitwirkender“ zu.</span><span class="sxs-lookup"><span data-stu-id="ca39e-118">Create a new service principal and assign it the Contributor role.</span></span>

```java
ServicePrincipal sp = Azure.servicePrincipals().define(spName)
    .withNewApplication("http://" + spName)
    .create();
RoleAssignment roleAssignment2 = authenticated.roleAssignments()
    .define("contribRoleAssignment")
    .forServicePrincipal(sp)
    .withBuiltInRole(BuiltInRole.CONTRIBUTOR)
    .withSubscriptionScope("862f67bc-d3ae-4243-bec7-3da6dca77717")
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca39e-119">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="ca39e-119">Explore the Management APIs</span></span>](/java/api/overview/azure/activedirectory/management)


## <a name="samples"></a><span data-ttu-id="ca39e-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ca39e-120">Samples</span></span>

<span data-ttu-id="ca39e-121">[Verwalten von Gruppen, Benutzern und Rollen](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)  </span><span class="sxs-lookup"><span data-stu-id="ca39e-121">[Manage groups, users, and roles](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)  </span></span>  
<span data-ttu-id="ca39e-122">[An- und Abmelden von Benutzern in einer Java-Web-App](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span><span class="sxs-lookup"><span data-stu-id="ca39e-122">[Sign-in and sign-out users in a Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span></span>  
<span data-ttu-id="ca39e-123">[Verwenden einer Befehlszeilen-App für den Zugriff auf eine API mit Azure AD](https://github.com/Azure-Samples/active-directory-java-native-headless) </span><span class="sxs-lookup"><span data-stu-id="ca39e-123">[Access an API with Azure AD using a command line app](https://github.com/Azure-Samples/active-directory-java-native-headless) </span></span>  
[<span data-ttu-id="ca39e-124">Abrufen der Azure AD-Graph-API aus Ihrer Java-Web-App</span><span class="sxs-lookup"><span data-stu-id="ca39e-124">Call the Active AD Graph API from your Java web app</span></span>](https://github.com/Azure-Samples/active-directory-java-graphapi-web/)  

<span data-ttu-id="ca39e-125">Sehen Sie sich weitere [Java-Codebeispiele für Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ca39e-125">Explore more [sample Java code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) you can use in your apps.</span></span>
