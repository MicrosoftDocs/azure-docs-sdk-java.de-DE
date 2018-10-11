---
title: Hinzufügen eines Stammzertifikats für Azure zum Java-Zertifizierungsstellenspeicher
description: Hier erfahren Sie, wie Sie ein ZS-Stammzertifikat (Zertifizierungsstelle) zum Speicher für Java-Zertifizierungsstellenzertifikate (cacerts) für die Verwendung mit Microsoft Azure hinzufügen.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 07/02/2018
ms.author: robmcm
ms.openlocfilehash: 3f2de63f7eb1422ff1dd6db45d68e02f4af188b8
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48898923"
---
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="622e7-103">Hinzufügen eines Stammzertifikats zum Java-ZS-Zertifikatspeicher</span><span class="sxs-lookup"><span data-stu-id="622e7-103">Adding a root certificate to the Java CA certificates store</span></span>

<span data-ttu-id="622e7-104">Anwendungen, die Azure-Dienste (beispielsweise Azure Service Bus) nutzen, müssen dem Baltimore CyberTrust-Stammzertifikat vertrauen.</span><span class="sxs-lookup"><span data-stu-id="622e7-104">Applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="622e7-105">Dieses Zertifikat ist möglicherweise bereits auf Ihrem System installiert. Falls nicht, erfahren Sie in diesem Tutorial, wie Sie dem für Azure-Dienste verwendeten Speicher für Java-Zertifizierungsstellenzertifikate (cacerts) mithilfe von **keytool** von Oracle das erforderliche ZS-Stammzertifikat (Zertifizierungsstelle) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="622e7-105">This certificate may already be installed on your system, but if it is not, the steps in this tutorial will show you how to use Oracle's **keytool** to add the required certificate authority (CA) root certificate to the Java CA certificate (cacerts) store that you will use for Azure services.</span></span>

<span data-ttu-id="622e7-106">Das keytool-Hilfsprogramm von Oracle ist ein _Schlüssel- und Zertifikatverwaltungstool_, mit dem Entwickler die Liste der vertrauenswürdigen Zertifikate für Java verwalten können.</span><span class="sxs-lookup"><span data-stu-id="622e7-106">Oracle's keytool utility is a _Key and Certificate Management Tool_, which allows developers to manage the list of trusted certificates for use with Java.</span></span> <span data-ttu-id="622e7-107">Sie können „keytool“ zum Hinzufügen des Zertifizierungsstellenzertifikats verwenden, bevor Sie das JDK komprimieren und zum Ordner **approot** des Azure-Projekts hinzufügen. Optional können Sie auch eine Azure-Startaufgabe ausführen, bei der zum Hinzufügen des Zertifikats „keytool“ zum Einsatz kommt.</span><span class="sxs-lookup"><span data-stu-id="622e7-107">You can use keytool to add the CA certificate before zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span>

<span data-ttu-id="622e7-108">Am 15. April 2013 begann Azure mit der Migration des GTE CyberTrust Global-Stammzertifikats zum Baltimore CyberTrust-Stammzertifikat.</span><span class="sxs-lookup"><span data-stu-id="622e7-108">Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global root certificate to the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="622e7-109">Die folgenden Schritte zeigen, wie Sie das Baltimore CyberTrust-Stammzertifikat mithilfe von „keytool“ Ihrem Speicher für Java-ZS-Zertifikate (cacerts) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="622e7-109">The following steps show you how to use keytool to add the Baltimore CyberTrust root certificate to your Java CA certificate (cacerts) store.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="622e7-110">Mit den Schritten in diesem Artikel können Sie Ihr Java SDK so konfigurieren, dass es den Stammzertifikaten von anderen Zertifizierungsstellen vertraut.</span><span class="sxs-lookup"><span data-stu-id="622e7-110">You can use the steps in this article to configure your Java SDK to trust the root certificates from other trusted certificate authorities.</span></span> <span data-ttu-id="622e7-111">So können Sie beispielsweise ein Stammzertifikat aus der Zertifikatliste unter [GeoTrust-Stammzertifikate](http://www.geotrust.com/resources/root-certificates/) auswählen.</span><span class="sxs-lookup"><span data-stu-id="622e7-111">For example, you might choose a root certificate from the list of certificates at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span>
> 

## <a name="determining-which-root-certificates-are-installed"></a><span data-ttu-id="622e7-112">Bestimmen der installierten Stammzertifikate</span><span class="sxs-lookup"><span data-stu-id="622e7-112">Determining which root certificates are installed</span></span>

<span data-ttu-id="622e7-113">Das Baltimore-Zertifikat ist möglicherweise bereits in Ihrem cacerts-Speicher installiert. Gehen Sie daher wie folgt vor, um zu ermitteln, ob es bereits installiert ist.</span><span class="sxs-lookup"><span data-stu-id="622e7-113">The Baltimore certificate might already be installed in your cacerts store, so you need to use the following steps to determine if it has already been installed.</span></span>

1. <span data-ttu-id="622e7-114">Navigieren Sie an einer Administratoreingabeaufforderung zum Ordner **jdk\jre\lib\security** Ihres JDK, und führen Sie den folgenden Befehl aus, um die auf Ihrem System installierten Zertifikate aufzulisten:</span><span class="sxs-lookup"><span data-stu-id="622e7-114">At an administrator command prompt, navigate to your JDK's **jdk\jre\lib\security** folder, and then run the following command to list the certificates that are installed on your system:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

1. <span data-ttu-id="622e7-115">Falls Sie zur Eingabe des Speicherkennworts aufgefordert werden: Das Standardkennwort lautet **changeit**.</span><span class="sxs-lookup"><span data-stu-id="622e7-115">If you are prompted for the store password, the default password is **changeit**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="622e7-116">Informationen zum Ändern des Speicherkennworts finden Sie in der keytool-Dokumentation: <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="622e7-116">If you want to change the store password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>
   > 

1. <span data-ttu-id="622e7-117">Sollte kein Zertifikat mit dem Fingerabdruck `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` angezeigt werden, gehen Sie wie im folgenden Abschnitt beschrieben vor, um das Zertifikat herunterzuladen und zu installieren.</span><span class="sxs-lookup"><span data-stu-id="622e7-117">If you do not see the certificate with the thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, use the steps in the following section to download and install the certificate.</span></span>

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a><span data-ttu-id="622e7-118">So fügen Sie dem cacerts-Speicher ein Stammzertifikat hinzu</span><span class="sxs-lookup"><span data-stu-id="622e7-118">To add a root certificate to the cacerts store</span></span>

1. <span data-ttu-id="622e7-119">Laden Sie das Baltimore CyberTrust-Stammzertifikat von <https://cacert.omniroot.com/bc2025.crt> herunter, und speichern Sie es im Ordner **jdk\jre\lib\security** in einer lokalen Datei mit der Erweiterung **.cer**.</span><span class="sxs-lookup"><span data-stu-id="622e7-119">Download the Baltimore CyberTrust root certificate from <https://cacert.omniroot.com/bc2025.crt>, and save to a local file with extension **.cer** in your **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="622e7-120">In diesem Beispiel wird davon ausgegangen, dass Sie die Baltimore CyberTrust-Stammzertifikatdatei als **bc2025.cer** heruntergeladen haben.</span><span class="sxs-lookup"><span data-stu-id="622e7-120">For this example, assume that you downloaded the Baltimore CyberTrust root certificate file as **bc2025.cer**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="622e7-121">Das Baltimore CyberTrust-Stammzertifikat hat die Seriennummer `02:00:00:b9` und den SHA1-Fingerabdruck `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span><span class="sxs-lookup"><span data-stu-id="622e7-121">The Baltimore CyberTrust root certificate has a serial number of `02:00:00:b9`, and a SHA1 thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span></span>
   > 

2. <span data-ttu-id="622e7-122">Importieren Sie das Zertifikat mithilfe des folgenden Befehls in den cacerts-Speicher:</span><span class="sxs-lookup"><span data-stu-id="622e7-122">Import the certificate to the cacerts store by using the following command:</span></span>

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   <span data-ttu-id="622e7-123">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="622e7-123">Where:</span></span>

   |  <span data-ttu-id="622e7-124">Parameter</span><span class="sxs-lookup"><span data-stu-id="622e7-124">Parameter</span></span>   |                              <span data-ttu-id="622e7-125">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="622e7-125">Description</span></span>                               |
   |--------------|------------------------------------------------------------------------|
   | `keystore`   | <span data-ttu-id="622e7-126">Gibt den Zertifikatspeicher an.</span><span class="sxs-lookup"><span data-stu-id="622e7-126">Specifies the certificate store.</span></span>                                       |
   | `importcert` | <span data-ttu-id="622e7-127">Gibt an, dass Sie ein Zertifikat importieren.</span><span class="sxs-lookup"><span data-stu-id="622e7-127">Specifies that you are importing a certificate.</span></span>                        |
   | `alias`      | <span data-ttu-id="622e7-128">Gibt einen Alias für das Zertifikat an.</span><span class="sxs-lookup"><span data-stu-id="622e7-128">Specifies an alias for the certificate.</span></span>                                |
   | `file`       | <span data-ttu-id="622e7-129">Gibt den Dateinamen des Stammzertifikats an, das Sie importieren.</span><span class="sxs-lookup"><span data-stu-id="622e7-129">Specifies the filename of the root certificate that you are importing.</span></span> |


3. <span data-ttu-id="622e7-130">Wenn Sie aufgefordert werden, dem Zertifikat zu vertrauen, vergewissern Sie sich, dass es den Fingerabdruck `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` hat, und geben Sie **y** ein, wenn der Fingerabdruck korrekt ist.</span><span class="sxs-lookup"><span data-stu-id="622e7-130">If you are prompted to trust the certificate, verify the thumbprint as `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, and type **y** if the thumbprint is correct.</span></span>

4. <span data-ttu-id="622e7-131">Führen Sie den folgenden Befehl aus, um sicherzustellen, dass das Zertifizierungsstellenzertifikat erfolgreich importiert wurde:</span><span class="sxs-lookup"><span data-stu-id="622e7-131">Run the following command to ensure the CA certificate has been successfully imported:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

<span data-ttu-id="622e7-132">Nachdem Sie das Stammzertifikat erfolgreich Ihrem JDK hinzugefügt haben, können Sie den JDK-Inhalt zippen und dem Ordner **approot** Ihres Azure-Projekts hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="622e7-132">After you have successfully added the root certificate to your JDK, you can zip the contents of JDK and add it to your Azure project's **approot** folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="622e7-133">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="622e7-133">Next steps</span></span>

<span data-ttu-id="622e7-134">Weitere Informationen zum keytool-Hilfsprogramm finden Sie unter <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="622e7-134">For more information about the keytool utility, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

<span data-ttu-id="622e7-135">Weitere Informationen zu Java finden Sie im Artikel [Azure für Java-Entwickler](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="622e7-135">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

<!-- For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx). -->
