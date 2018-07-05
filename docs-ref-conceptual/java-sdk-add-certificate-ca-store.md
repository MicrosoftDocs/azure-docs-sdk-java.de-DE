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
ms.date: 05/23/2018
ms.author: robmcm
ms.openlocfilehash: 29b2b598968c9a3a896fffee3ce56f9b0cb4b1ee
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090733"
---
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a>Hinzufügen eines Stammzertifikats zum Java-ZS-Zertifikatspeicher

Anwendungen, die Azure-Dienste (beispielsweise Azure Service Bus) nutzen, müssen dem Baltimore CyberTrust-Stammzertifikat vertrauen. Dieses Zertifikat ist möglicherweise bereits auf Ihrem System installiert. Falls nicht, erfahren Sie in diesem Tutorial, wie Sie dem für Azure-Dienste verwendeten Speicher für Java-Zertifizierungsstellenzertifikate (cacerts) mithilfe von **keytool** von Oracle das erforderliche ZS-Stammzertifikat (Zertifizierungsstelle) hinzufügen.

Das keytool-Hilfsprogramm von Oracle ist ein _Schlüssel- und Zertifikatverwaltungstool_, mit dem Entwickler die Liste der vertrauenswürdigen Zertifikate für Java verwalten können. Sie können „keytool“ zum Hinzufügen des Zertifizierungsstellenzertifikats verwenden, bevor Sie das JDK komprimieren und zum Ordner **approot** des Azure-Projekts hinzufügen. Optional können Sie auch eine Azure-Startaufgabe ausführen, bei der zum Hinzufügen des Zertifikats „keytool“ zum Einsatz kommt.

Am 15. April 2013 begann Azure mit der Migration des GTE CyberTrust Global-Stammzertifikats zum Baltimore CyberTrust-Stammzertifikat. Die folgenden Schritte zeigen, wie Sie das Baltimore CyberTrust-Stammzertifikat mithilfe von „keytool“ Ihrem Speicher für Java-ZS-Zertifikate (cacerts) hinzufügen.

> [!NOTE]
> 
> Mit den Schritten in diesem Artikel können Sie Ihr Java SDK so konfigurieren, dass es den Stammzertifikaten von anderen Zertifizierungsstellen vertraut. So können Sie beispielsweise ein Stammzertifikat aus der Zertifikatliste unter [GeoTrust-Stammzertifikate](http://www.geotrust.com/resources/root-certificates/) auswählen.
> 

## <a name="determining-which-root-certificates-are-installed"></a>Bestimmen der installierten Stammzertifikate

Das Baltimore-Zertifikat ist möglicherweise bereits in Ihrem cacerts-Speicher installiert. Gehen Sie daher wie folgt vor, um zu ermitteln, ob es bereits installiert ist.

1. Navigieren Sie an einer Administratoreingabeaufforderung zum Ordner **jdk\jre\lib\security** Ihres JDK, und führen Sie den folgenden Befehl aus, um die auf Ihrem System installierten Zertifikate aufzulisten:

   ```shell
   keytool -list -keystore cacerts
   ```

1. Falls Sie zur Eingabe des Speicherkennworts aufgefordert werden: Das Standardkennwort lautet **changeit**.

   > [!NOTE]
   > 
   > Informationen zum Ändern des Speicherkennworts finden Sie in der keytool-Dokumentation: <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.
   > 

1. Sollte kein Zertifikat mit dem Fingerabdruck `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` angezeigt werden, gehen Sie wie im folgenden Abschnitt beschrieben vor, um das Zertifikat herunterzuladen und zu installieren.

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a>So fügen Sie dem cacerts-Speicher ein Stammzertifikat hinzu

1. Laden Sie das Baltimore CyberTrust-Stammzertifikat von <https://cacert.omniroot.com/bc2025.crt> herunter, und speichern Sie es im Ordner **jdk\jre\lib\security** in einer lokalen Datei mit der Erweiterung **.cer**. In diesem Beispiel wird davon ausgegangen, dass Sie die Baltimore CyberTrust-Stammzertifikatdatei als **bc2025.cer** heruntergeladen haben.

   > [!NOTE]
   > 
   > Das Baltimore CyberTrust-Stammzertifikat hat die Seriennummer `02:00:00:b9` und den SHA1-Fingerabdruck `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.
   > 

2. Importieren Sie das Zertifikat mithilfe des folgenden Befehls in den cacerts-Speicher:

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   Hinweis:

   |  Parameter   |                              Beschreibung                               |
   |--------------|------------------------------------------------------------------------|
   |  `keystore`  |                    Gibt den Zertifikatspeicher an.                    |
   | `importcert` |            Gibt an, dass Sie ein Zertifikat importieren.             |
   |   `alias`    |                Gibt einen Alias für das Zertifikat an.                 |
   |    `file`    | Gibt den Dateinamen des Stammzertifikats an, das Sie importieren. |


3. Wenn Sie aufgefordert werden, dem Zertifikat zu vertrauen, vergewissern Sie sich, dass es den Fingerabdruck `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` hat, und geben Sie **y** ein, wenn der Fingerabdruck korrekt ist.

4. Führen Sie den folgenden Befehl aus, um sicherzustellen, dass das Zertifizierungsstellenzertifikat erfolgreich importiert wurde:

   ```shell
   keytool -list -keystore cacerts
   ```

Nachdem Sie das Stammzertifikat erfolgreich Ihrem JDK hinzugefügt haben, können Sie den JDK-Inhalt zippen und dem Ordner **approot** Ihres Azure-Projekts hinzufügen.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum keytool-Hilfsprogramm finden Sie unter <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

Weitere Informationen zu den von Azure verwendeten Stammzertifikaten finden Sie unter [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx)(in englischer Sprache).

Weitere Informationen zu Java finden Sie im Artikel [Azure für Java-Entwickler](/java/azure).
