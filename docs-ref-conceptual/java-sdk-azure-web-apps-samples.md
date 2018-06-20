---
title: Azure-Verwaltungsbibliotheken für Java-Web-App-Beispiele
description: Abrufen von Beispielcode zum Erstellen und Aktualisieren von in App Service gehosteten Azure-Web-Apps mit den Azure-Verwaltungsbibliotheken für Java
keywords: Azure, Java, SDK, API, Maven, Gradle, Web-Apps, App Service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 43633e5c-9fb1-4807-ba63-e24c126754e2
ms.openlocfilehash: 2f1e43f3835ffcdb138bf7e29a1656b7ee381281
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930896"
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a><span data-ttu-id="a8ccd-104">Azure-Verwaltungsbibliotheken für Java-Beispiele für Web-Apps</span><span class="sxs-lookup"><span data-stu-id="a8ccd-104">Azure management libraries for Java samples for web apps</span></span>

| <span data-ttu-id="a8ccd-105">**Erstellen einer App**</span><span class="sxs-lookup"><span data-stu-id="a8ccd-105">**Create an app**</span></span> ||
|---|---|
| <span data-ttu-id="a8ccd-106">[Erstellen einer Web-App und Bereitstellen über FTP oder GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="a8ccd-106">[Create a web app and deploy from FTP or GitHub][1]</span></span> | <span data-ttu-id="a8ccd-107">Bereitstellen von Web-Apps über das lokale Git, FTP und Continuous Integration über GitHub</span><span class="sxs-lookup"><span data-stu-id="a8ccd-107">Deploy web apps from local Git, FTP, and continuous integration from GitHub.</span></span> |
| <span data-ttu-id="a8ccd-108">[Erstellen einer Web-App und Verwalten von Bereitstellungsslots][2]</span><span class="sxs-lookup"><span data-stu-id="a8ccd-108">[Create a web app and manage deployment slots][2]</span></span> | <span data-ttu-id="a8ccd-109">Erstellen einer Web-App und Bereitstellen in Stagingslots sowie Austauschen von Bereitstellungen zwischen Slots</span><span class="sxs-lookup"><span data-stu-id="a8ccd-109">Create a web app and deploy to staging slots, and then swap deployments between slots.</span></span> |
| <span data-ttu-id="a8ccd-110">**Konfigurieren der App**</span><span class="sxs-lookup"><span data-stu-id="a8ccd-110">**Configure app**</span></span> ||
| <span data-ttu-id="a8ccd-111">[Erstellen einer Web-App und Konfigurieren einer benutzerdefinierten Domäne][3]</span><span class="sxs-lookup"><span data-stu-id="a8ccd-111">[Create a web app and configure a custom domain][3]</span></span> | <span data-ttu-id="a8ccd-112">Erstellen einer Web-App mit einer benutzerdefinierten Domäne und einem selbstsignierten SSL-Zertifikat</span><span class="sxs-lookup"><span data-stu-id="a8ccd-112">Create a web app with a custom domain and self-signed SSL certificate.</span></span> |
| <span data-ttu-id="a8ccd-113">**Skalieren von Apps**</span><span class="sxs-lookup"><span data-stu-id="a8ccd-113">**Scale apps**</span></span> ||
| <span data-ttu-id="a8ccd-114">[Skalieren einer Web-App mit hoher Verfügbarkeit in mehreren Regionen][4]</span><span class="sxs-lookup"><span data-stu-id="a8ccd-114">[Scale a web app with high availability across multiple regions][4]</span></span> | <span data-ttu-id="a8ccd-115">Skalieren einer Web-App in drei verschiedenen geografischen Regionen und Verfügbarmachen der App mithilfe von Azure Traffic Manager über einen einzelnen Endpunkt</span><span class="sxs-lookup"><span data-stu-id="a8ccd-115">Scale a web app in three different geographical regions and make them available through a single endpoint using Azure Traffic Manager.</span></span> | 
| <span data-ttu-id="a8ccd-116">**Verbinden der App mit Ressourcen**</span><span class="sxs-lookup"><span data-stu-id="a8ccd-116">**Connect app to resources**</span></span> ||
| <span data-ttu-id="a8ccd-117">[Verbinden einer Web-App mit einem Speicherkonto][5]</span><span class="sxs-lookup"><span data-stu-id="a8ccd-117">[Connect a web app to a storage account][5]</span></span> | <span data-ttu-id="a8ccd-118">Erstellen eines Azure-Speicherkontos und Hinzufügen der Speicherkonto-Verbindungszeichenfolge zu den App-Einstellungen</span><span class="sxs-lookup"><span data-stu-id="a8ccd-118">Create an Azure storage account and add the storage account connection string to the app settings.</span></span> |
| <span data-ttu-id="a8ccd-119">[Verbinden einer Web-App mit einer SQL­Datenbank][6]</span><span class="sxs-lookup"><span data-stu-id="a8ccd-119">[Connect a web app to a SQL database][6]</span></span> | <span data-ttu-id="a8ccd-120">Erstellen einer Web-App und einer SQL-Datenbank und Hinzufügen der SQL Datenbank-Verbindungszeichenfolge zu den App-Einstellungen</span><span class="sxs-lookup"><span data-stu-id="a8ccd-120">Create a web app and SQL database, and then add the SQL database connection string to the app settings.</span></span> |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/