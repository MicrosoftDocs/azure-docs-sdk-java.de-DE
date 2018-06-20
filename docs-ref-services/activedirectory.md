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
ms.locfileid: "31823783"
---
# <a name="azure-active-directory-libraries-for-java"></a>Azure Active Directory-Bibliotheken für Java

## <a name="overview"></a>Übersicht

Mit [Azure Active Directory](/azure/active-directory/active-directory-whatis) können Sie Benutzer anmelden und den Zugriff auf Anwendungen und APIs steuern.

Informationen zu den ersten Schritten mit Azure AD finden Sie unter [An- und Abmeldung bei Java-Web-Apps mit Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).

## <a name="client-library"></a>Clientbibliothek

Konfigurieren Sie OAuth2-, OpenID Connect- oder Active Directory Graph-Authentifizierung und [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)-SSO mit der [Azure Active Directory-Authentifizierungsbibliothek (ADAL) für Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Clientbibliothek in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a>Beispiel

Rufen Sie mit der [Graph-API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) von Azure Active Directory ein JSON-Webtoken (JWT) für einen Benutzer in Ihrem Active Directory-Mandanten ab. Dieses Token kann dann zur Authentifizierung des Benutzers bei einer Anwendung oder API verwendet werden.

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

## <a name="management-api"></a>Verwaltungs-API

Konfigurieren Sie die [rollenbasierte Zugriffssteuerung](/azure/active-directory/role-based-access-control-what-is), und weisen Sie diesen Rollen dann mit der Verwaltungs-API Identitäten (z.B. Benutzer und [Dienstprinzipale](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) zu. 

Fügen Sie der Maven-Datei `pom.xml` eine [Abhängigkeit](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) hinzu, um die Verwaltungs-API in Ihrem Projekt zu verwenden.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Beispiel 

Erstellen Sie einen neuen Dienstprinzipal, und weisen Sie ihn der Rolle „Mitwirkender“ zu.

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
> [Informationen zu den Verwaltungs-APIs](/java/api/overview/azure/activedirectory/management)


## <a name="samples"></a>Beispiele

[Verwalten von Gruppen, Benutzern und Rollen](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)    
[An- und Abmelden von Benutzern in einer Java-Web-App](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)    
[Verwenden einer Befehlszeilen-App für den Zugriff auf eine API mit Azure AD](https://github.com/Azure-Samples/active-directory-java-native-headless)   
[Abrufen der Azure AD-Graph-API aus Ihrer Java-Web-App](https://github.com/Azure-Samples/active-directory-java-graphapi-web/)  

Sehen Sie sich weitere [Java-Codebeispiele für Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) an, die Sie in Ihren Apps verwenden können.
