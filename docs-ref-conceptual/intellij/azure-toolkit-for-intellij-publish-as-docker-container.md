---
title: "Veröffentlichen eines Docker-Containers mit dem Azure-Toolkit für IntelliJ"
description: "Erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine Web-App in Microsoft Azure als Docker-Container veröffentlichen."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm
ms.openlocfilehash: 1da5cc058038830ca09710a1dc8eede71bb67387
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="7c2df-103">Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7c2df-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="7c2df-104">Docker-Container sind eine weit verbreitete Methode zum Bereitstellen von Webanwendungen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="7c2df-105">Mithilfe von Docker-Containern können Entwickler ihre Projektdateien und Abhängigkeiten für die Bereitstellung auf einem Server in einem einzelnen Paket zusammenfassen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="7c2df-106">Mit dem Azure-Toolkit für IntelliJ wird dieser Prozess für Java-Entwickler vereinfacht, indem Features vom Typ *Als Docker-Container veröffentlichen* für die Bereitstellung in Microsoft Azure hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="7c2df-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="7c2df-107">In diesem Artikel werden die Schritte beschrieben, die zum Veröffentlichen Ihrer Anwendungen in Azure als Docker-Container erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="7c2df-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="7c2df-108">Weitere Informationen zu Docker finden Sie auf der [Docker-Website].</span><span class="sxs-lookup"><span data-stu-id="7c2df-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="7c2df-109">Veröffentlichen Ihrer Web-App in Azure mithilfe eines Docker-Containers</span><span class="sxs-lookup"><span data-stu-id="7c2df-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="7c2df-110">Zum Veröffentlichen Ihrer Web-App müssen Sie ein Artefakt erstellen, das für die Bereitstellung bereit ist.</span><span class="sxs-lookup"><span data-stu-id="7c2df-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="7c2df-111">Weitere Informationen finden Sie im Abschnitt [Zusätzliche Informationen zum Erstellen von Artefakten](#artifacts).</span><span class="sxs-lookup"><span data-stu-id="7c2df-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="7c2df-112">Nachdem Sie den Bereitstellungs-Assistenten mindestens einmal ausgeführt haben, sind die meisten Einstellungen bereits als Standardwerte vorhanden, wenn Sie den Assistenten erneut ausführen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="7c2df-113">Öffnen Sie Ihr Web-App-Projekt in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7c2df-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="7c2df-114">Wählen Sie eine der Optionen, um den Assistenten **Publish as Docker Container** (Als Docker-Container veröffentlichen) zu starten:</span><span class="sxs-lookup"><span data-stu-id="7c2df-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="7c2df-115">Klicken Sie im Fenster des Tools **Projekt** mit der rechten Maustaste auf Ihr Projekt, und klicken Sie dann auf **Azure** und **Publish as Docker Container** (Als Docker-Container veröffentlichen):</span><span class="sxs-lookup"><span data-stu-id="7c2df-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Befehl „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PUB01]

   * <span data-ttu-id="7c2df-117">Klicken Sie auf der IntelliJ-Symbolleiste auf die Schaltfläche **Publish Group** (Gruppe veröffentlichen) und anschließend auf **Publish as Docker Container** (Als Docker-Container veröffentlichen):</span><span class="sxs-lookup"><span data-stu-id="7c2df-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="7c2df-118">![Befehl „Publish as Docker Container“ (Als Docker-Container veröffentlichen)][PUB02]</span><span class="sxs-lookup"><span data-stu-id="7c2df-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="7c2df-119">Der Assistent **Deploy Docker Container on Azure** (Docker-Container in Azure bereitstellen) wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="7c2df-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB03]

3. <span data-ttu-id="7c2df-121">Gehen Sie im Fenster **Type an image name, select the artifact's path and check a Docker host to be used** (Geben Sie einen Imagenamen ein, wählen Sie den Pfad des Artefakts aus, und aktivieren Sie den gewünschten Docker-Host) wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="7c2df-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="7c2df-122">a.</span><span class="sxs-lookup"><span data-stu-id="7c2df-122">a.</span></span> <span data-ttu-id="7c2df-123">Geben Sie im Feld **Docker image name** (Docker-Imagename) einen eindeutigen Namen für Ihren Docker-Host ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="7c2df-124">(Der Assistent gibt automatisch einen Namen vor, aber Sie können den Namen ändern.)</span><span class="sxs-lookup"><span data-stu-id="7c2df-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="7c2df-125">b.</span><span class="sxs-lookup"><span data-stu-id="7c2df-125">b.</span></span> <span data-ttu-id="7c2df-126">Im Bereich **Hosts** werden die Docker-Hosts angezeigt, die Sie bereits erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="7c2df-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="7c2df-127">Führen Sie einen der folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="7c2df-127">Do either of the following:</span></span> 
      * <span data-ttu-id="7c2df-128">Wenn Sie über einen vorhandenen Docker-Host verfügen, können Sie Ihre Web-App darauf bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="7c2df-129">Klicken Sie zum Erstellen eines Docker-Hosts auf das grüne Pluszeichen (**+**).</span><span class="sxs-lookup"><span data-stu-id="7c2df-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="7c2df-130">Das Dialogfeld **Create Docker Host** (Docker-Host erstellen) wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="7c2df-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB04a]

4. <span data-ttu-id="7c2df-132">Geben Sie im Fenster **Configure the new virtual machine** (Neuen virtuellen Computer konfigurieren) die folgenden Informationen zu Ihrem Docker-Host ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="7c2df-133">(Der Assistent generiert die meisten Informationen für Sie automatisch, aber Sie können sie ändern.)</span><span class="sxs-lookup"><span data-stu-id="7c2df-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="7c2df-134">a.</span><span class="sxs-lookup"><span data-stu-id="7c2df-134">a.</span></span> <span data-ttu-id="7c2df-135">Geben Sie im Feld **Name** einen eindeutigen Namen für den Docker-Host ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="7c2df-136">(Dieser ist nicht mit dem Namen des Docker-Image identisch, den Sie zuvor angegeben haben.)</span><span class="sxs-lookup"><span data-stu-id="7c2df-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="7c2df-137">b.</span><span class="sxs-lookup"><span data-stu-id="7c2df-137">b.</span></span> <span data-ttu-id="7c2df-138">Geben Sie im Feld **Abonnement** das Azure-Abonnement ein, das Sie für Ihren Host verwenden.</span><span class="sxs-lookup"><span data-stu-id="7c2df-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="7c2df-139">c.</span><span class="sxs-lookup"><span data-stu-id="7c2df-139">c.</span></span> <span data-ttu-id="7c2df-140">Geben Sie im Feld **Region** die geografische Region ein, in der sich Ihr Host befindet.</span><span class="sxs-lookup"><span data-stu-id="7c2df-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="7c2df-141">d.</span><span class="sxs-lookup"><span data-stu-id="7c2df-141">d.</span></span> <span data-ttu-id="7c2df-142">Gehen Sie auf der Registerkarte **OS and Size** (Betriebssystem und Größe) wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="7c2df-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="7c2df-143">**Host OS** (Hostbetriebssystem): Geben Sie das Betriebssystem für den virtuellen Computer ein, der Ihren Host enthält.</span><span class="sxs-lookup"><span data-stu-id="7c2df-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="7c2df-144">**Größe**: Geben Sie die Größe des virtuellen Computers für Ihren Host ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="7c2df-145">e.</span><span class="sxs-lookup"><span data-stu-id="7c2df-145">e.</span></span> <span data-ttu-id="7c2df-146">Wählen Sie auf der Registerkarte **Ressourcengruppe** eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="7c2df-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="7c2df-147">**Neue Ressourcengruppe**: Erstellen Sie eine Ressourcengruppe für Ihren Host.</span><span class="sxs-lookup"><span data-stu-id="7c2df-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="7c2df-148">**Vorhandene Ressourcengruppe**: Geben Sie eine vorhandene Ressourcengruppe Ihres Azure-Kontos an.</span><span class="sxs-lookup"><span data-stu-id="7c2df-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="7c2df-149">f.</span><span class="sxs-lookup"><span data-stu-id="7c2df-149">f.</span></span> <span data-ttu-id="7c2df-150">Wählen Sie auf der Registerkarte **Netzwerk** eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="7c2df-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="7c2df-151">**Neues virtuelles Netzwerk**: Erstellen Sie ein virtuelles Netzwerk für Ihren Host.</span><span class="sxs-lookup"><span data-stu-id="7c2df-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="7c2df-152">**Existing virtual network** (Vorhandenes virtuelles Netzwerk): Geben Sie ein vorhandenes virtuelles Netzwerk Ihres Azure-Kontos an.</span><span class="sxs-lookup"><span data-stu-id="7c2df-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="7c2df-153">g.</span><span class="sxs-lookup"><span data-stu-id="7c2df-153">g.</span></span> <span data-ttu-id="7c2df-154">Wählen Sie auf der Registerkarte **Speicher** eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="7c2df-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="7c2df-155">**Neues Speicherkonto**: Erstellen Sie ein Speicherkonto für Ihren Host.</span><span class="sxs-lookup"><span data-stu-id="7c2df-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="7c2df-156">**Vorhandenes Speicherkonto**: Geben Sie ein vorhandenes Speicherkonto Ihres Azure-Kontos an.</span><span class="sxs-lookup"><span data-stu-id="7c2df-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="7c2df-157">Klicken Sie auf **Weiter**.
   </span><span class="sxs-lookup"><span data-stu-id="7c2df-157">Click **Next**.</span></span>  
  <span data-ttu-id="7c2df-158">Das Fenster **Configure log in credentials and port settings** (Anmeldeinformationen und Porteinstellungen konfigurieren) wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="7c2df-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![Fenster „Configure log in credentials and port settings“ (Anmeldeinformationen und Porteinstellungen konfigurieren)][PUB05]

6. <span data-ttu-id="7c2df-160">Wählen Sie eine der folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="7c2df-160">Select one of the following options:</span></span>

      * <span data-ttu-id="7c2df-161">**Import credentials from Azure Key Vault** (Anmeldeinformationen aus Azure Key Vault importieren): Geben Sie zuvor gespeicherte Anmeldeinformationen an, die in Ihrem Azure-Abonnement gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="7c2df-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="7c2df-162">Auf einen Azure-Schlüsseltresor, der in einem bestimmten Konto oder Dienstprinzipal erstellt wird, kann kein anderes Konto und kein anderer Dienstprinzipal desselben Abonnements automatisch zugreifen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="7c2df-163">Damit ein anderes Konto oder ein anderer Dienstprinzipal den Schlüsseltresor verwenden kann, müssen Sie im Azure-Portal das Konto oder den Dienstprinzipal hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="7c2df-164">**New log in credentials** (Neue Anmeldeinformationen): Erstellen Sie neue Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="7c2df-165">Gehen Sie bei Auswahl dieser Option wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="7c2df-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="7c2df-166">a.</span><span class="sxs-lookup"><span data-stu-id="7c2df-166">a.</span></span> <span data-ttu-id="7c2df-167">Geben Sie auf der Registerkarte **VM Credentials** (VM-Anmeldeinformationen) die folgenden Angaben für die VM-Anmeldeinformationen Ihres Docker-Hosts an: * **Benutzername**: Geben Sie den Benutzernamen für Ihre VM-Anmeldeinformationen ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: * **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="7c2df-168">* **Kennwort** und **Bestätigen**: Geben Sie das Kennwort für Ihre VM-Anmeldeinformationen ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-168">* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="7c2df-169">* **SSH**: Geben Sie die SSH-Einstellungen (Secure Shell) für Ihren Docker-Host ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-169">* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="7c2df-170">Sie können eine der folgenden Optionen auswählen: * **Keine**: Gibt an, dass für Ihren virtuellen Computer keine SSH-Verbindungen zulässig sind.</span><span class="sxs-lookup"><span data-stu-id="7c2df-170">You can select one of the following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="7c2df-171">* **Automatisch generieren**: Mit dieser Option werden die erforderlichen Einstellungen zum Herstellen einer Verbindung über SSH automatisch erstellt.</span><span class="sxs-lookup"><span data-stu-id="7c2df-171">* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="7c2df-172">* **Import from directory** (Aus Verzeichnis importieren): Ermöglicht das Angeben eines Verzeichnisses, das zuvor gespeicherte SSH-Einstellungen enthält.</span><span class="sxs-lookup"><span data-stu-id="7c2df-172">* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="7c2df-173">Das Verzeichnis muss die folgenden beiden Dateien enthalten:</span><span class="sxs-lookup"><span data-stu-id="7c2df-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="7c2df-174">b.</span><span class="sxs-lookup"><span data-stu-id="7c2df-174">b.</span></span> <span data-ttu-id="7c2df-175">Geben Sie auf der Registerkarte **Docker Daemon Access** (Docker-Daemon-Zugriff) die folgenden Informationen an:</span><span class="sxs-lookup"><span data-stu-id="7c2df-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

          ![Erstellen eines Docker-Hosts][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="7c2df-177">Klicken Sie nach dem Eingeben der erforderlichen Informationen auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="7c2df-177">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="7c2df-178">Der Assistent **Deploy Docker Container on Azure** (Docker-Container in Azure bereitstellen) wird wieder angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7c2df-178">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Assistent „Deploy Docker Container on Azure“ (Docker-Container in Azure bereitstellen)][PUB07]

8. <span data-ttu-id="7c2df-180">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="7c2df-180">Click **Next**.</span></span>  
    <span data-ttu-id="7c2df-181">Das Fenster **Configure the Docker container to be created** (Zu erstellenden Docker-Container konfigurieren) wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="7c2df-181">The **Configure the Docker container to be created** window opens.</span></span>

   ![Fenster „Configure the Docker container to be created“ (Zu erstellenden Docker-Container konfigurieren)][PUB08]

9. <span data-ttu-id="7c2df-183">Geben Sie im Fenster **Configure the Docker container to be created** (Zu erstellenden Docker-Container konfigurieren) die folgenden Informationen an:</span><span class="sxs-lookup"><span data-stu-id="7c2df-183">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="7c2df-184">a.</span><span class="sxs-lookup"><span data-stu-id="7c2df-184">a.</span></span> <span data-ttu-id="7c2df-185">Geben Sie im Feld **Docker container name** (Name des Docker-Containers) einen eindeutigen Namen für Ihren Docker-Container ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-185">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="7c2df-186">b.</span><span class="sxs-lookup"><span data-stu-id="7c2df-186">b.</span></span> <span data-ttu-id="7c2df-187">Wählen Sie eines der folgenden Docker-Images aus:</span><span class="sxs-lookup"><span data-stu-id="7c2df-187">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="7c2df-188">**Predefined Docker image** (Vordefiniertes Docker-Image): Geben Sie ein bereits in Azure vorhandenes Docker-Image an.</span><span class="sxs-lookup"><span data-stu-id="7c2df-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="7c2df-189">Die Liste mit den Docker-Images in diesem Feld enthält mehrere Images, für deren Patching das Azure-Toolkit konfiguriert ist, damit Ihr Artefakt automatisch bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="7c2df-189">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="7c2df-190">**Custom Dockerfile** (Benutzerdefinierte Dockerfile): Geben Sie eine zuvor auf Ihrem lokalen Computer gespeicherte Dockerfile an.</span><span class="sxs-lookup"><span data-stu-id="7c2df-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="7c2df-191">Dies ist eine komplexere Funktion für Entwickler, die ihre eigene Dockerfile bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="7c2df-191">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="7c2df-192">Es ist jedoch Aufgabe von Entwickler, die diese Option wählen, dafür zu sorgen, dass ihre Dockerfile ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7c2df-192">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="7c2df-193">Da das Azure-Toolkit den Inhalt einer benutzerdefinierten Dockerfile nicht überprüft, kann die Bereitstellung unter Umständen fehlschlagen, wenn die Dockerfile Probleme verursacht.</span><span class="sxs-lookup"><span data-stu-id="7c2df-193">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="7c2df-194">Weil vom Azure-Toolkit erwartet wird, dass die benutzerdefinierte Dockerfile ein Web-App-Artefakt enthält, wird außerdem versucht, eine HTTP-Verbindung zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-194">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="7c2df-195">Wenn Entwickler eine andere Art von Artefakt veröffentlichen, können nach der Bereitstellung ggf. harmlose Fehler auftreten.</span><span class="sxs-lookup"><span data-stu-id="7c2df-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="7c2df-196">c.</span><span class="sxs-lookup"><span data-stu-id="7c2df-196">c.</span></span> <span data-ttu-id="7c2df-197">Geben Sie im Feld **Porteinstellungen** die eindeutige TCP-Portbindung für Ihren Docker-Container ein.</span><span class="sxs-lookup"><span data-stu-id="7c2df-197">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="7c2df-198">Nachdem Sie die obigen Schritte abgeschlossen haben, können Sie auf **Fertig stellen** klicken.</span><span class="sxs-lookup"><span data-stu-id="7c2df-198">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="7c2df-199">Das Azure-Toolkit beginnt damit, Ihre Web-App in einem Docker-Container in Azure bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="7c2df-199">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="7c2df-200">Sofern Sie für IntelliJ nicht die Bereitstellung im Hintergrund konfiguriert haben, wird die Statusanzeige **Deploying to Azure** (Wird in Azure bereitgestellt) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7c2df-200">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![Statusanzeige für Bereitstellung][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="7c2df-202">Zusätzliche Informationen zum Erstellen von Artefakten</span><span class="sxs-lookup"><span data-stu-id="7c2df-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="7c2df-203">Gehen Sie wie folgt vor, um ein bereitstellungsfähiges Artefakt zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="7c2df-203">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="7c2df-204">Öffnen Sie Ihr Web-App-Projekt in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7c2df-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="7c2df-205">Klicken Sie auf **Datei** und dann auf **Projektstruktur**.</span><span class="sxs-lookup"><span data-stu-id="7c2df-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Befehl „Projektstruktur“][ART01]

3. <span data-ttu-id="7c2df-207">Klicken Sie zum Hinzufügen eines Artefakts auf das grüne Pluszeichen (**+**) und dann auf **Webanwendung: Archiv**.</span><span class="sxs-lookup"><span data-stu-id="7c2df-207">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Befehl „Webanwendung: Archiv“][ART02]

4. <span data-ttu-id="7c2df-209">Geben Sie im Feld **Name** einen Namen für Ihr Artefakt ein (ohne die Erweiterung *.war*), und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c2df-209">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![Feld „Name“ für Artefakt][ART03]

<span data-ttu-id="7c2df-211">Weitere Informationen zum Erstellen von Artefakten in IntelliJ finden Sie auf der JetBrains-Website unter [Konfigurieren von Artefakten].</span><span class="sxs-lookup"><span data-stu-id="7c2df-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c2df-212">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="7c2df-212">Next steps</span></span>

<span data-ttu-id="7c2df-213">Zusätzliche Ressourcen für Docker finden Sie auf der offiziellen [Docker-Website].</span><span class="sxs-lookup"><span data-stu-id="7c2df-213">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Docker-Website]: https://www.docker.com/
[Konfigurieren von Artefakten]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
