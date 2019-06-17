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
# <a name="install-the-jdk-for-azure-and-azure-stack"></a>Installieren des JDK für Azure und Azure Stack

Bei Azul Zulu Enterprise-Builds von OpenJDK handelt es sich um eine kostenlose, plattformübergreifende und produktionsbereite Distribution von OpenJDK für Azure und Azure Stack, die von Microsoft und Azul Systems unterstützt wird. Sie enthält alle Komponenten, die zum Erstellen und Ausführen von Java SE-Anwendungen benötigt werden.

Es stehen [mehrere unterstützte Downloadpakettypen für die jeweiligen Clientbetriebssysteme](https://www.azul.com/downloads/azure-only/zulu/) zur Verfügung. Für die folgenden Plattformen können Sie auch ein VM-Image aus dem Azure Marketplace-Katalog beziehen:

  * [Azul Zulu: Java 8 unter Ubuntu 18.04](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [Azul Zulu: Java 8 unter Windows Server 2019](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [Azul Zulu: Java 11 unter Ubuntu 18.04](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [Azul Zulu: Java 11 unter Windows Server 2019](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> Diese Anweisungen beziehen sich auf die Java 8-Version (64 Bit) des JDK. Die Java Runtime Environment (JRE) wird von Azul auch als eigenständige Installation angeboten. Die JRE ist in der JDK-Installation enthalten.
>
>  Auf der [Azure-Downloadseite von Azul](https://www.azul.com/downloads/azure-only/zulu/) stehen auch Java 11-Pakete zur Verfügung.

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a>Herunterladen und Installieren der Azul Zulu JDKs für Windows 

1. [Laden Sie die 64-Bit-Version von Azul Zulu JDK 8 als MSI-Datei herunter](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi), und verwenden Sie als Ziel einen Speicherort auf Ihrem Client (beispielsweise `C:\Users\<your_login>\Downloads`). (Auf der [Azure-Downloadseite von Azul](https://www.azul.com/downloads/azure-only/zulu/) stehen auch ZIP-Pakete zur Verfügung.)

2. Navigieren Sie zu dem Verzeichnis, und doppelklicken Sie auf die heruntergeladene MSI-Datei, um die Installation zu starten.

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a>Herunterladen und Installieren der Azul Zulu JDKs für Mac 

Mit den folgenden Schritten laden Sie eine ZIP-Datei auf Ihren Mac herunter. Es ist auch eine DMG-Version verfügbar.

1. [Laden Sie die 64-Bit-Version von Azul Zulu JDK 8 als ZIP-Datei herunter](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip), und verwenden Sie als Ziel einen Speicherort auf Ihrem Client (beispielsweise `/Library/Java/JavaVirtualMachines/`). (Auf der [Azure-Downloadseite von Azul](https://www.azul.com/downloads/azure-only/zulu/) stehen auch DMG-Pakete zur Verfügung.)

2. Starten Sie den Finder, navigieren Sie zum Downloadverzeichnis, und doppelklicken Sie auf die ZIP-Datei. Alternativ können Sie auch ein Terminalbefehlsfenster starten, zu dem Verzeichnis navigieren, und Folgendes ausführen:

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a>Herunterladen und Installieren der Azul Zulu JDKs für Alpine Linux

1. [Laden Sie die 64-Bit-Version von Azul Zulu JDK 8 als TAR-Datei herunter](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz), und verwenden Sie als Ziel einen Speicherort auf Ihrem Client (beispielsweise `/usr/lib/jvm`). (Auf der [Azure-Downloadseite von Azul](https://www.azul.com/downloads/azure-only/zulu/) stehen auch RPM- und DEB-Pakete zur Verfügung.)

2. Navigieren Sie zu Ihrem Verzeichnis, und führen Sie den folgenden Befehl aus, um die Datei zu entzippen und zu erweitern:

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a>Überprüfen der Installation

Führen Sie zur Überprüfung der Installation an der Befehlszeile Folgendes aus: `java -version`.

Die Ausgabe des Befehls sollte wie folgt aussehen:

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a>Herunterladen und Installieren der Azul Zulu JDKs aus einem Yum-Repository

Die Azul Zulu JDKs werden von Azul in einem [Yum-Repository](http://repos.azul.com/azure-only/zulu-azure.repo) bereitgestellt.

**Führen Sie über Ihre Befehlszeilenschnittstelle die folgenden Befehle aus, um das Azul Zulu JDK für Java 8 zu installieren:**

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

Java 11:

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

Java 12 (Vorschauversion):

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

**So aktualisieren Sie ein Zulu JDK 8-Paket aus einem Yum-Repository:**

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

(Bei Verwendung der Version 11 oder 12 muss die Versionsnummer im obigen Befehl entsprechend geändert werden.)

**So entfernen Sie ein Zulu JDK 8-Paket aus einem Yum-Repository:**

```cli
sudo yum -y erase zulu-8-azure-jdk
```
(Bei Verwendung der Version 11 oder 12 muss die Versionsnummer im obigen Befehl entsprechend geändert werden.)

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a>Herunterladen und Installieren der Azul Zulu JDKs aus einem apt-get-Repository

Die Azul Zulu JDKs werden von Azul auch in einem [apt-get-Repository](http://repos.azul.com/azure-only/zulu/apt) bereitgestellt.

**Führen Sie über Ihre Befehlszeilenschnittstelle die folgenden Befehle aus, um das Azul Zulu JDK für Java 8 mit apt-get zu installieren:**

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

Java 11:

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

Java 12 (Vorschauversion):

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

**So aktualisieren Sie ein Zulu JDK 8-Paket aus einem apt-get-Repository:**

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

Das vorherige Release wird automatisch entfernt.
(Bei Verwendung der Version 11 oder 12 muss die Versionsnummer im obigen Befehl entsprechend geändert werden.)

**So entfernen Sie ein Zulu JDK 8-Paket aus einem apt-get-Repository:**

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

(Bei Verwendung der Version 11 oder 12 muss die Versionsnummer im obigen Befehl entsprechend geändert werden.)

Ausführlichere Informationen zum Vorbereiten, Installieren und Verwalten Ihrer Azul Zulu JDKs für die Azure-Entwicklung finden Sie in der [offiziellen Zulu-Dokumentation](https://docs.azul.com/zulu/zuludocs/index.htm).

