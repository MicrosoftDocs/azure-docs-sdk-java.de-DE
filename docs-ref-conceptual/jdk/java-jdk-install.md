---
title: Installieren des Azul Zulu JDK für Azure und Azure Stack
description: Hier erfahren Sie, wie Sie die Azul Zulu Java Development Kits (JDKs) für die Azure-Entwicklung mit Windows, Linux und Mac installieren.
author: erickson-doug
manager: douge
ms.author: douge
ms.date: 4/19/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 33d2206f9a0a1cc9fadc60b17c1a93f66c592fe3
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568593"
---
# <a name="install-the-jdk-for-azure-and-azure-stack"></a><span data-ttu-id="be2fc-103">Installieren des JDK für Azure und Azure Stack</span><span class="sxs-lookup"><span data-stu-id="be2fc-103">Install the JDK for Azure and Azure Stack</span></span>

<span data-ttu-id="be2fc-104">Bei Azul Zulu Enterprise-Builds von OpenJDK handelt es sich um eine kostenlose, plattformübergreifende und produktionsbereite Distribution von OpenJDK für Azure und Azure Stack, die von Microsoft und Azul Systems unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="be2fc-104">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="be2fc-105">Sie enthält alle Komponenten, die zum Erstellen und Ausführen von Java SE-Anwendungen benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="be2fc-105">They contain all the components for building and running Java SE applications.</span></span>

<span data-ttu-id="be2fc-106">Es stehen [mehrere unterstützte Downloadpakettypen für die jeweiligen Clientbetriebssysteme](https://www.azul.com/downloads/azure-only/zulu/) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="be2fc-106">There are [multiple download package types supported for each client OS](https://www.azul.com/downloads/azure-only/zulu/).</span></span> <span data-ttu-id="be2fc-107">Für die folgenden Plattformen können Sie auch ein VM-Image aus dem Azure Marketplace-Katalog beziehen:</span><span class="sxs-lookup"><span data-stu-id="be2fc-107">You can also get a virtual machine image from the Azure Marketplace Gallery for the following platforms:</span></span>

  * [<span data-ttu-id="be2fc-108">Azul Zulu: Java 8 unter Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="be2fc-108">Azul Zulu: Java 8 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [<span data-ttu-id="be2fc-109">Azul Zulu: Java 8 unter Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="be2fc-109">Azul Zulu: Java 8 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [<span data-ttu-id="be2fc-110">Azul Zulu: Java 11 unter Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="be2fc-110">Azul Zulu: Java 11 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [<span data-ttu-id="be2fc-111">Azul Zulu: Java 11 unter Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="be2fc-111">Azul Zulu: Java 11 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> <span data-ttu-id="be2fc-112">Diese Anweisungen beziehen sich auf die Java 8-Version (64 Bit) des JDK.</span><span class="sxs-lookup"><span data-stu-id="be2fc-112">These instructions target the 64-bit Java 8 version of the JDK.</span></span> <span data-ttu-id="be2fc-113">Die Java Runtime Environment (JRE) wird von Azul auch als eigenständige Installation angeboten.</span><span class="sxs-lookup"><span data-stu-id="be2fc-113">Azul also provides the Java Run-time Environment (JRE) as a stand-alone installation.</span></span> <span data-ttu-id="be2fc-114">Die JRE ist in der JDK-Installation enthalten.</span><span class="sxs-lookup"><span data-stu-id="be2fc-114">The JRE is included with the JDK install.</span></span>
>
>  <span data-ttu-id="be2fc-115">Auf der [Azure-Downloadseite von Azul](https://www.azul.com/downloads/azure-only/zulu/) stehen auch Java 11-Pakete zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="be2fc-115">Java 11 packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a><span data-ttu-id="be2fc-116">Herunterladen und Installieren der Azul Zulu JDKs für Windows</span><span class="sxs-lookup"><span data-stu-id="be2fc-116">Download and install the Azul Zulu JDKs for Windows</span></span> 

1. <span data-ttu-id="be2fc-117">[Laden Sie die 64-Bit-Version von Azul Zulu JDK 8 als MSI-Datei herunter](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi), und verwenden Sie als Ziel einen Speicherort auf Ihrem Client (beispielsweise `C:\Users\<your_login>\Downloads`).</span><span class="sxs-lookup"><span data-stu-id="be2fc-117">[Download the 64-bit Azul Zulu JDK 8 as an MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) to a location on your client, such as `C:\Users\<your_login>\Downloads`.</span></span> <span data-ttu-id="be2fc-118">(Auf der [Azure-Downloadseite von Azul](https://www.azul.com/downloads/azure-only/zulu/) stehen auch ZIP-Pakete zur Verfügung.)</span><span class="sxs-lookup"><span data-stu-id="be2fc-118">(.ZIP packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="be2fc-119">Navigieren Sie zu dem Verzeichnis, und doppelklicken Sie auf die heruntergeladene MSI-Datei, um die Installation zu starten.</span><span class="sxs-lookup"><span data-stu-id="be2fc-119">Navigate to the directory and double-click the downloaded MSI file to begin installation.</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a><span data-ttu-id="be2fc-120">Herunterladen und Installieren der Azul Zulu JDKs für Mac</span><span class="sxs-lookup"><span data-stu-id="be2fc-120">Download and install the Azul Zulu JDKs for Mac</span></span> 

<span data-ttu-id="be2fc-121">Mit den folgenden Schritten laden Sie eine ZIP-Datei auf Ihren Mac herunter.</span><span class="sxs-lookup"><span data-stu-id="be2fc-121">These steps download a ZIP file to your Mac.</span></span> <span data-ttu-id="be2fc-122">Es ist auch eine DMG-Version verfügbar.</span><span class="sxs-lookup"><span data-stu-id="be2fc-122">There is also a DMG version available.</span></span>

1. <span data-ttu-id="be2fc-123">[Laden Sie die 64-Bit-Version von Azul Zulu JDK 8 als ZIP-Datei herunter](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip), und verwenden Sie als Ziel einen Speicherort auf Ihrem Client (beispielsweise `/Library/Java/JavaVirtualMachines/`).</span><span class="sxs-lookup"><span data-stu-id="be2fc-123">[Download the 64-bit Azul Zulu JDK 8 as a ZIP file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) to a location on your client, such as `/Library/Java/JavaVirtualMachines/`.</span></span> <span data-ttu-id="be2fc-124">(Auf der [Azure-Downloadseite von Azul](https://www.azul.com/downloads/azure-only/zulu/) stehen auch DMG-Pakete zur Verfügung.)</span><span class="sxs-lookup"><span data-stu-id="be2fc-124">(.DMG packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="be2fc-125">Starten Sie den Finder, navigieren Sie zum Downloadverzeichnis, und doppelklicken Sie auf die ZIP-Datei.</span><span class="sxs-lookup"><span data-stu-id="be2fc-125">Launch Finder, navigate to the download directory, and double-click the ZIP file.</span></span> <span data-ttu-id="be2fc-126">Alternativ können Sie auch ein Terminalbefehlsfenster starten, zu dem Verzeichnis navigieren, und Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="be2fc-126">Alternatively, you can launch a terminal command window, navigate to the directory, and run:</span></span>

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a><span data-ttu-id="be2fc-127">Herunterladen und Installieren der Azul Zulu JDKs für Alpine Linux</span><span class="sxs-lookup"><span data-stu-id="be2fc-127">Download and install the Azul Zulu JDKs for Alpine Linux</span></span>

1. <span data-ttu-id="be2fc-128">[Laden Sie die 64-Bit-Version von Azul Zulu JDK 8 als TAR-Datei herunter](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz), und verwenden Sie als Ziel einen Speicherort auf Ihrem Client (beispielsweise `/usr/lib/jvm`).</span><span class="sxs-lookup"><span data-stu-id="be2fc-128">[Download the 64-bit Azul Zulu JDK 8 as a TAR file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) to a location on your client, such as `/usr/lib/jvm`.</span></span> <span data-ttu-id="be2fc-129">(Auf der [Azure-Downloadseite von Azul](https://www.azul.com/downloads/azure-only/zulu/) stehen auch RPM- und DEB-Pakete zur Verfügung.)</span><span class="sxs-lookup"><span data-stu-id="be2fc-129">(.RPM and .DEB packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="be2fc-130">Navigieren Sie zu Ihrem Verzeichnis, und führen Sie den folgenden Befehl aus, um die Datei zu entzippen und zu erweitern:</span><span class="sxs-lookup"><span data-stu-id="be2fc-130">Go to your directory and run the following command to unzip and expand the file:</span></span>

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a><span data-ttu-id="be2fc-131">Überprüfen der Installation</span><span class="sxs-lookup"><span data-stu-id="be2fc-131">Confirm your installation</span></span>

<span data-ttu-id="be2fc-132">Führen Sie zur Überprüfung der Installation an der Befehlszeile Folgendes aus: `java -version`.</span><span class="sxs-lookup"><span data-stu-id="be2fc-132">To confirm your installation, go to the command-line and run `java -version`.</span></span>

<span data-ttu-id="be2fc-133">Die Ausgabe des Befehls sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="be2fc-133">The output of the command should be:</span></span>

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a><span data-ttu-id="be2fc-134">Herunterladen und Installieren der Azul Zulu JDKs aus einem Yum-Repository</span><span class="sxs-lookup"><span data-stu-id="be2fc-134">Download and install the Azul Zulu JDKs from a Yum repository</span></span>

<span data-ttu-id="be2fc-135">Die Azul Zulu JDKs werden von Azul in einem [Yum-Repository](http://repos.azul.com/azure-only/zulu-azure.repo) bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="be2fc-135">The Azul Zulu JDKs are provided in a [Yum repository](http://repos.azul.com/azure-only/zulu-azure.repo) by Azul.</span></span>

<span data-ttu-id="be2fc-136">**Führen Sie über Ihre Befehlszeilenschnittstelle die folgenden Befehle aus, um das Azul Zulu JDK für Java 8 zu installieren:**</span><span class="sxs-lookup"><span data-stu-id="be2fc-136">**To install the Azul Zulu JDK for Java 8, run the following commands from your CLI:**</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="be2fc-137">Java 11:</span><span class="sxs-lookup"><span data-stu-id="be2fc-137">For Java 11, run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

<span data-ttu-id="be2fc-138">Java 12 (Vorschauversion):</span><span class="sxs-lookup"><span data-stu-id="be2fc-138">For Java 12 (Preview), run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

<span data-ttu-id="be2fc-139">**So aktualisieren Sie ein Zulu JDK 8-Paket aus einem Yum-Repository:**</span><span class="sxs-lookup"><span data-stu-id="be2fc-139">**To update a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="be2fc-140">(Bei Verwendung der Version 11 oder 12 muss die Versionsnummer im obigen Befehl entsprechend geändert werden.)</span><span class="sxs-lookup"><span data-stu-id="be2fc-140">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="be2fc-141">**So entfernen Sie ein Zulu JDK 8-Paket aus einem Yum-Repository:**</span><span class="sxs-lookup"><span data-stu-id="be2fc-141">**To remove a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -y erase zulu-8-azure-jdk
```
<span data-ttu-id="be2fc-142">(Bei Verwendung der Version 11 oder 12 muss die Versionsnummer im obigen Befehl entsprechend geändert werden.)</span><span class="sxs-lookup"><span data-stu-id="be2fc-142">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a><span data-ttu-id="be2fc-143">Herunterladen und Installieren der Azul Zulu JDKs aus einem apt-get-Repository</span><span class="sxs-lookup"><span data-stu-id="be2fc-143">Download and install the Azul Zulu JDKs from an apt-get repository</span></span>

<span data-ttu-id="be2fc-144">Die Azul Zulu JDKs werden von Azul auch in einem [apt-get-Repository](http://repos.azul.com/azure-only/zulu/apt) bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="be2fc-144">The Azul Zulu JDKs are also provided in an [apt-get repository](http://repos.azul.com/azure-only/zulu/apt) by Azul.</span></span>

<span data-ttu-id="be2fc-145">**Führen Sie über Ihre Befehlszeilenschnittstelle die folgenden Befehle aus, um das Azul Zulu JDK für Java 8 mit apt-get zu installieren:**</span><span class="sxs-lookup"><span data-stu-id="be2fc-145">**To install the Azul Zulu JDK for Java 8 with apt-get, run the following commands from your CLI:**</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="be2fc-146">Java 11:</span><span class="sxs-lookup"><span data-stu-id="be2fc-146">For Java 11, run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

<span data-ttu-id="be2fc-147">Java 12 (Vorschauversion):</span><span class="sxs-lookup"><span data-stu-id="be2fc-147">For Java 12 (Preview), run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

<span data-ttu-id="be2fc-148">**So aktualisieren Sie ein Zulu JDK 8-Paket aus einem apt-get-Repository:**</span><span class="sxs-lookup"><span data-stu-id="be2fc-148">**To update a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="be2fc-149">Das vorherige Release wird automatisch entfernt.</span><span class="sxs-lookup"><span data-stu-id="be2fc-149">The previous release will be automatically removed.</span></span>
<span data-ttu-id="be2fc-150">(Bei Verwendung der Version 11 oder 12 muss die Versionsnummer im obigen Befehl entsprechend geändert werden.)</span><span class="sxs-lookup"><span data-stu-id="be2fc-150">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="be2fc-151">**So entfernen Sie ein Zulu JDK 8-Paket aus einem apt-get-Repository:**</span><span class="sxs-lookup"><span data-stu-id="be2fc-151">**To remove a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

<span data-ttu-id="be2fc-152">(Bei Verwendung der Version 11 oder 12 muss die Versionsnummer im obigen Befehl entsprechend geändert werden.)</span><span class="sxs-lookup"><span data-stu-id="be2fc-152">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="be2fc-153">Ausführlichere Informationen zum Vorbereiten, Installieren und Verwalten Ihrer Azul Zulu JDKs für die Azure-Entwicklung finden Sie in der [offiziellen Zulu-Dokumentation](https://docs.azul.com/zulu/zuludocs/index.htm).</span><span class="sxs-lookup"><span data-stu-id="be2fc-153">For more detailed guidance on preparing, installing, and managing your Azul Zulu JDKs for Azure development, read [the official Zulu docs](https://docs.azul.com/zulu/zuludocs/index.htm).</span></span>

