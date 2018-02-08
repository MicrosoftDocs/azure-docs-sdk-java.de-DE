---
title: "Veröffentlichen eines Docker-Containers mithilfe des Azure-Toolkits für Eclipse"
description: "Erfahren Sie, wie Sie mit dem Azure-Toolkit für Eclipse eine Web-App in Microsoft Azure als Docker-Container veröffentlichen."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: aec3682cc14204ca2b395d4b851db7bb68cb8728
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="76195-103">Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für Eclipse</span><span class="sxs-lookup"><span data-stu-id="76195-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="76195-104">Docker-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen.</span><span class="sxs-lookup"><span data-stu-id="76195-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="76195-105">Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen.</span><span class="sxs-lookup"><span data-stu-id="76195-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="76195-106">Mit dem Azure-Toolkit für Eclipse wird dieser Prozess für Java-Entwickler vereinfacht, indem Features vom Typ *Als Docker-Container veröffentlichen* für die Bereitstellung in Microsoft Azure hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="76195-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="76195-107">In diesem Artikel werden die Schritte beschrieben, die zum Veröffentlichen Ihrer Anwendungen in Azure als Docker-Container erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="76195-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="76195-108">Weitere Informationen zu Docker finden Sie auf der [Docker-Website].</span><span class="sxs-lookup"><span data-stu-id="76195-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="76195-109">Veröffentlichen Ihrer Web-App in Azure mithilfe eines Docker-Containers</span><span class="sxs-lookup"><span data-stu-id="76195-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="76195-110">Öffnen Sie Ihr Web-App-Projekt in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="76195-110">Open your web app project in Eclipse.</span></span>

1. <span data-ttu-id="76195-111">Wählen Sie eine der Optionen, um den Assistenten **Publish as Docker Container** (Als Docker-Container veröffentlichen) zu starten:</span><span class="sxs-lookup"><span data-stu-id="76195-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="76195-112">Klicken Sie in der Ansicht **Navigator** mit der rechten Maustaste auf Ihr Projekt, und klicken Sie dann auf **Azure** und **Publish as Docker Container** (Als Docker-Container veröffentlichen).</span><span class="sxs-lookup"><span data-stu-id="76195-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Navigator-Ansicht „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PUB01]

   * <span data-ttu-id="76195-114">Klicken Sie auf der Eclipse-Symbolleiste auf die Schaltfläche **Publish** (Veröffentlichen) und anschließend auf **Publish as Docker Container** (Als Docker-Container veröffentlichen).</span><span class="sxs-lookup"><span data-stu-id="76195-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Eclipse-Symbolleiste „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PUB02]
      
   <span data-ttu-id="76195-116">Der Assistent **Deploy Docker Container on Azure** (Docker-Container in Azure bereitstellen) wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="76195-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB03]

1. <span data-ttu-id="76195-118">Gehen Sie im Fenster **Type an image name, select the artifact's path and check a Docker host to be used** (Geben Sie einen Imagenamen ein, wählen Sie den Pfad des Artefakts aus, und aktivieren Sie den gewünschten Docker-Host) wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="76195-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

   <span data-ttu-id="76195-119">a.</span><span class="sxs-lookup"><span data-stu-id="76195-119">a.</span></span> <span data-ttu-id="76195-120">Geben Sie im Feld **Docker image name** (Docker-Imagename) einen eindeutigen Namen für Ihren Docker-Host ein.</span><span class="sxs-lookup"><span data-stu-id="76195-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="76195-121">(Der Assistent gibt automatisch einen Namen vor, aber Sie können den Namen ändern.)</span><span class="sxs-lookup"><span data-stu-id="76195-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

   <span data-ttu-id="76195-122">b.</span><span class="sxs-lookup"><span data-stu-id="76195-122">b.</span></span> <span data-ttu-id="76195-123">Im Bereich **Hosts** werden die Docker-Hosts angezeigt, die Sie bereits erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="76195-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="76195-124">Führen Sie einen der folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="76195-124">Do either of the following:</span></span>

   * <span data-ttu-id="76195-125">Wenn Sie über einen vorhandenen Docker-Host verfügen, können Sie Ihre Web-App darauf bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="76195-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
   * <span data-ttu-id="76195-126">Um einen neuen Docker-Host zu erstellen, klicken Sie auf **Add** (Hinzufügen).</span><span class="sxs-lookup"><span data-stu-id="76195-126">To create a new Docker host, click **Add**.</span></span>  
      
      <span data-ttu-id="76195-127">Das Dialogfeld **Create Docker Host** (Docker-Host erstellen) wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="76195-127">The **Create Docker Host** dialog box opens.</span></span>

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB04a]

1. <span data-ttu-id="76195-129">Geben Sie im Fenster **Configure the new virtual machine** (Neuen virtuellen Computer konfigurieren) die folgenden Optionen für Ihren Docker-Host an.</span><span class="sxs-lookup"><span data-stu-id="76195-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="76195-130">(Der Assistent generiert die meisten Optionen für Sie automatisch, aber Sie können sie ändern.)</span><span class="sxs-lookup"><span data-stu-id="76195-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="76195-131">a.</span><span class="sxs-lookup"><span data-stu-id="76195-131">a.</span></span> <span data-ttu-id="76195-132">**Name**: Geben Sie einen eindeutigen Name für den Docker-Host ein.</span><span class="sxs-lookup"><span data-stu-id="76195-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="76195-133">(Dieser ist nicht mit dem Namen des Docker-Image identisch, den Sie zuvor angegeben haben.)</span><span class="sxs-lookup"><span data-stu-id="76195-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="76195-134">b.</span><span class="sxs-lookup"><span data-stu-id="76195-134">b.</span></span> <span data-ttu-id="76195-135">**Abonnement**: Geben Sie das Azure-Abonnement ein, das Sie für Ihren Host verwenden.</span><span class="sxs-lookup"><span data-stu-id="76195-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="76195-136">c.</span><span class="sxs-lookup"><span data-stu-id="76195-136">c.</span></span> <span data-ttu-id="76195-137">**Region**: Geben Sie die geografische Region ein, in der sich Ihr Host befindet.</span><span class="sxs-lookup"><span data-stu-id="76195-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="76195-138">d.</span><span class="sxs-lookup"><span data-stu-id="76195-138">d.</span></span> <span data-ttu-id="76195-139">Auf der Registerkarte **Host-BS und Größe**:</span><span class="sxs-lookup"><span data-stu-id="76195-139">On the **Host OS and Size** tab:</span></span> 
   * <span data-ttu-id="76195-140">**Host OS** (Hostbetriebssystem): Geben Sie das Betriebssystem für den virtuellen Computer ein, der Ihren Host enthält.</span><span class="sxs-lookup"><span data-stu-id="76195-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
   * <span data-ttu-id="76195-141">**Größe**: Geben Sie die Größe des virtuellen Computers für Ihren Host ein.</span><span class="sxs-lookup"><span data-stu-id="76195-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="76195-142">e.</span><span class="sxs-lookup"><span data-stu-id="76195-142">e.</span></span> <span data-ttu-id="76195-143">Auf der Registerkarte **Ressourcengruppe**:</span><span class="sxs-lookup"><span data-stu-id="76195-143">On the **Resource Group** tab:</span></span> 
   * <span data-ttu-id="76195-144">**Neue Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe für Ihren Host.</span><span class="sxs-lookup"><span data-stu-id="76195-144">**New resource group**: Create a new resource group for your host.</span></span>
   * <span data-ttu-id="76195-145">**Vorhandene Ressourcengruppe**: Geben Sie eine vorhandene Ressourcengruppe Ihres Azure-Kontos ein.</span><span class="sxs-lookup"><span data-stu-id="76195-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="76195-146">f.</span><span class="sxs-lookup"><span data-stu-id="76195-146">f.</span></span> <span data-ttu-id="76195-147">Auf der Registerkarte **Netzwerk**:</span><span class="sxs-lookup"><span data-stu-id="76195-147">On the **Network** tab:</span></span> 
   * <span data-ttu-id="76195-148">**Neues virtuelles Netzwerk**: Erstellen Sie ein neues virtuelles Netzwerk für Ihren Host.</span><span class="sxs-lookup"><span data-stu-id="76195-148">**New virtual network**: Create a new virtual network for your host.</span></span>
   * <span data-ttu-id="76195-149">**Existing virtual network** (Vorhandenes virtuelles Netzwerk): Geben Sie ein vorhandenes virtuelles Netzwerk Ihres Azure-Kontos ein.</span><span class="sxs-lookup"><span data-stu-id="76195-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="76195-150">g.</span><span class="sxs-lookup"><span data-stu-id="76195-150">g.</span></span> <span data-ttu-id="76195-151">Auf der Registerkarte **Storage**:</span><span class="sxs-lookup"><span data-stu-id="76195-151">On the **Storage** tab:</span></span> 
   * <span data-ttu-id="76195-152">**Neues Speicherkonto**: Erstellen Sie ein neues Speicherkonto für Ihren Host.</span><span class="sxs-lookup"><span data-stu-id="76195-152">**New storage account**: Create a new storage account for your host.</span></span>
   * <span data-ttu-id="76195-153">**Vorhandenes Speicherkonto**: Geben Sie ein vorhandenes Speicherkonto Ihres Azure-Kontos ein.</span><span class="sxs-lookup"><span data-stu-id="76195-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

1. <span data-ttu-id="76195-154">Klicken Sie auf **Weiter**.
</span><span class="sxs-lookup"><span data-stu-id="76195-154">Click **Next**.</span></span>

1. <span data-ttu-id="76195-155">Wählen Sie im Fenster **Configure log in credentials and port settings** (Anmeldeinformationen und Porteinstellungen konfigurieren) eine der folgenden Optionen aus:</span><span class="sxs-lookup"><span data-stu-id="76195-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

   * <span data-ttu-id="76195-156">**Import credentials from Azure Key Vault** (Anmeldeinformationen aus Azure Key Vault importieren): Gibt zuvor gespeicherte Anmeldeinformationen an, die in Ihrem Azure-Abonnement gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="76195-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span> 

   >[!NOTE]
   ><span data-ttu-id="76195-157">Auf einem Azure Key Vault-Tresor, der in einem bestimmten Konto oder Dienstprinzipal erstellt wird, kann kein anderes Konto und kein anderer Dienstprinzipal desselben Abonnements automatisch zugreifen.</span><span class="sxs-lookup"><span data-stu-id="76195-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="76195-158">Damit ein anderes Konto oder ein anderer Dienstprinzipal den Key Vault-Schlüsseltresor verwenden kann, müssen Sie im Azure-Portal das Konto oder den Dienstprinzipal hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="76195-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>
   >

   * <span data-ttu-id="76195-159">**New log in credentials** (Neue Anmeldeinformationen): Erstellt neue Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="76195-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="76195-160">Gehen Sie bei Auswahl dieser Option wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="76195-160">If you select this option, do the following:</span></span> 
    
      * <span data-ttu-id="76195-161">Wählen Sie auf der Registerkarte **VM-Anmeldeinformationen** eine der folgenden Optionen für die Anmeldung beim virtuellen Computer Ihres Docker-Hosts:</span><span class="sxs-lookup"><span data-stu-id="76195-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span> 

         * <span data-ttu-id="76195-162">**Benutzername**: Geben Sie den Benutzernamen für die Anmeldungsinformationen bei Ihrem virtuellen Computer an.</span><span class="sxs-lookup"><span data-stu-id="76195-162">**Username**: Enter the username for your virtual machine login credentials.</span></span> 
         * <span data-ttu-id="76195-163">**Kennwort** und **Bestätigen**: Geben Sie das Kennwort für Ihre VM-Anmeldeinformationen ein.</span><span class="sxs-lookup"><span data-stu-id="76195-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span> 
         * <span data-ttu-id="76195-164">**SSH**: Geben Sie die SSH-Einstellungen (Secure Shell) für Ihren Docker-Host ein.</span><span class="sxs-lookup"><span data-stu-id="76195-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="76195-165">Sie können zwischen folgenden Optionen wählen:</span><span class="sxs-lookup"><span data-stu-id="76195-165">You can choose from the following options:</span></span> 
            * <span data-ttu-id="76195-166">**Keine**: Gibt an, dass Ihr virtueller Computer keine SSH-Verbindungen zulässt.</span><span class="sxs-lookup"><span data-stu-id="76195-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span> 
            * <span data-ttu-id="76195-167">**Automatisch generieren**: Mit dieser Option werden die erforderlichen Einstellungen zum Herstellen einer Verbindung über SSH automatisch erstellt.</span><span class="sxs-lookup"><span data-stu-id="76195-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span> 
            * <span data-ttu-id="76195-168">**Import from directory** (Aus Verzeichnis importieren): Gibt ein Verzeichnis an, das zuvor gespeicherte SSH-Einstellungen enthält.</span><span class="sxs-lookup"><span data-stu-id="76195-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="76195-169">Das Verzeichnis muss die folgenden beiden Dateien enthalten:</span><span class="sxs-lookup"><span data-stu-id="76195-169">The directory must contain the following two files:</span></span> 
               * <span data-ttu-id="76195-170">*id_rsa*: Enthält die RSA-Kennung eines Benutzers.</span><span class="sxs-lookup"><span data-stu-id="76195-170">*id_rsa*: Contains the RSA identification for a user.</span></span> 
               * <span data-ttu-id="76195-171">*id_rsa.pub*: Enthält den öffentlichen RSA-Schlüssel, der für die Authentifizierung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="76195-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span> 
        
         ![Erstellen eines Docker-Hosts][PUB05]

      * <span data-ttu-id="76195-173">Geben Sie auf der Registerkarte **Docker-Daemon-Anmeldeinformationen** die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="76195-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span> 

         * <span data-ttu-id="76195-174">**Docker-Daemon-Port**: Geben Sie den eindeutigen TCP-Port für den Docker-Host an.</span><span class="sxs-lookup"><span data-stu-id="76195-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span> 
         * <span data-ttu-id="76195-175">**TLS-Sicherheit**: Geben Sie die Transport Layer Security-Einstellungen für Ihren Docker-Host an.</span><span class="sxs-lookup"><span data-stu-id="76195-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="76195-176">Sie können zwischen folgenden Optionen wählen:</span><span class="sxs-lookup"><span data-stu-id="76195-176">You can choose from the following options:</span></span> 
            * <span data-ttu-id="76195-177">**Keine**: Gibt an, dass Ihr virtueller Computer keine TLS-Verbindungen zulässt.</span><span class="sxs-lookup"><span data-stu-id="76195-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span> 
            * <span data-ttu-id="76195-178">**Automatisch generieren**: Mit dieser Option werden die erforderlichen Einstellungen zum Herstellen einer Verbindung über TLS automatisch erstellt.</span><span class="sxs-lookup"><span data-stu-id="76195-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span> 
            * <span data-ttu-id="76195-179">**Import from directory** (Aus Verzeichnis importieren): Gibt ein Verzeichnis an, das zuvor gespeicherte TLS-Einstellungen enthält.</span><span class="sxs-lookup"><span data-stu-id="76195-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="76195-180">Genauer gesagt muss das Verzeichnis die folgenden sechs Dateien enthalten:</span><span class="sxs-lookup"><span data-stu-id="76195-180">More specifically, the directory must contain the following six files:</span></span> 
               * <span data-ttu-id="76195-181">*ca.pem* und *ca-key.pem*: Enthalten das Zertifikat und den öffentlichen Schlüssel für die TLS-Zertifizierungsstelle.</span><span class="sxs-lookup"><span data-stu-id="76195-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span> 
               * <span data-ttu-id="76195-182">*cert.pem* und *key.pem*: Enthalten das Clientzertifikat und einen öffentlichen Schlüssel für die TLS-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="76195-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span> 
               * <span data-ttu-id="76195-183">*server.pem* und *server-key.pem*: Enthalten das Serverzertifikat und den öffentlichen Schlüssel für den Host.</span><span class="sxs-lookup"><span data-stu-id="76195-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span> 

         ![Erstellen eines Docker-Hosts][PUB06]

1. <span data-ttu-id="76195-185">Klicken Sie nach dem Eingeben aller erforderlichen Informationen auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="76195-185">After you have entered all of the preceding information, click **Finish**.</span></span>

1. <span data-ttu-id="76195-186">Klicken Sie im Assistenten **Deploy Docker Container on Azure** (Docker-Container in Azure bereitstellen) auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="76195-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB07]

1. <span data-ttu-id="76195-188">Im Fenster **Configure the Docker container to be created** (Zu erstellenden Docker-Container konfigurieren) tun Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="76195-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="76195-189">a.</span><span class="sxs-lookup"><span data-stu-id="76195-189">a.</span></span> <span data-ttu-id="76195-190">Geben Sie im Feld **Docker container name** (Name des Docker-Containers) einen eindeutigen Namen für Ihren Docker-Container ein.</span><span class="sxs-lookup"><span data-stu-id="76195-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="76195-191">b.</span><span class="sxs-lookup"><span data-stu-id="76195-191">b.</span></span> <span data-ttu-id="76195-192">Wählen Sie eines der folgenden Docker-Images aus:</span><span class="sxs-lookup"><span data-stu-id="76195-192">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="76195-193">**Predefined Docker image** (Vordefiniertes Docker-Image): Gibt ein bereits in Azure vorhandenes Docker-Image an.</span><span class="sxs-lookup"><span data-stu-id="76195-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span> 

      >[!NOTE]
      ><span data-ttu-id="76195-194">Die Liste mit den Docker-Images in diesem Feld enthält mehrere Images, für deren Patching das Azure-Toolkit konfiguriert ist, damit Ihr Artefakt automatisch bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="76195-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>
      >

      * <span data-ttu-id="76195-195">**Custom Dockerfile** (Benutzerdefinierte Dockerfile): Gibt eine zuvor auf Ihrem lokalen Computer gespeicherte Dockerfile an.</span><span class="sxs-lookup"><span data-stu-id="76195-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

      >[!NOTE]
      ><span data-ttu-id="76195-196">Dies ist eine komplexere Funktion für Entwickler, die ihre eigene Dockerfile bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="76195-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="76195-197">Es ist jedoch Aufgabe von Entwickler, die diese Option wählen, dafür zu sorgen, dass ihre Dockerfile ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="76195-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="76195-198">Das Azure-Toolkit überprüft nicht den Inhalt einer benutzerdefinierten Dockerfile, sodass die Bereitstellung möglicherweise fehlschlägt, wenn die Dockerfile Probleme verursacht.</span><span class="sxs-lookup"><span data-stu-id="76195-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="76195-199">Weil vom Azure-Toolkit erwartet wird, dass die benutzerdefinierte Dockerfile ein Web-App-Artefakt enthält, wird außerdem versucht, eine HTTP-Verbindung zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="76195-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="76195-200">Wenn Entwickler eine andere Art von Artefakt veröffentlichen, können nach der Bereitstellung womöglich harmlose Fehler auftreten.</span><span class="sxs-lookup"><span data-stu-id="76195-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>
      >

   <span data-ttu-id="76195-201">c.</span><span class="sxs-lookup"><span data-stu-id="76195-201">c.</span></span> <span data-ttu-id="76195-202">**Porteinstellungen**: Geben Sie die eindeutige TCP-Portbindung für Ihren Docker-Container ein.</span><span class="sxs-lookup"><span data-stu-id="76195-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

      ![Fenster „Configure the Docker container to be created“ (Zu erstellenden Docker-Container konfigurieren)][PUB08]

1. <span data-ttu-id="76195-204">Nachdem Sie alle obigen Schritte abgeschlossen haben, können Sie auf **Fertig stellen** klicken.</span><span class="sxs-lookup"><span data-stu-id="76195-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="76195-205">Das Azure-Toolkit beginnt damit, Ihre Web-App in einem Docker-Container in Azure bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="76195-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="76195-206">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="76195-206">Next steps</span></span>

<span data-ttu-id="76195-207">Zusätzliche Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website].</span><span class="sxs-lookup"><span data-stu-id="76195-207">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Docker-Website]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png