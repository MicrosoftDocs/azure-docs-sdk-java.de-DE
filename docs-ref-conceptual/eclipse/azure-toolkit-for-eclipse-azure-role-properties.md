---
title: Azure-Rolleneigenschaften
description: "Informationen Sie zum Azure-Toolkit für Eclipse verwenden, um Einstellungen für Azure-Rolle zu konfigurieren."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: cd734c64ba6d1394cb261bace92dee9dd579dd08
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-properties"></a>Azure-Rolleneigenschaften
Verschiedene Konfigurationseinstellungen für Ihre Azure-Rolle können im Azure-Toolkit für Eclipse festgelegt werden.

## <a name="configuring-azure-role-properties"></a>Konfigurieren von Azure-Rolleneigenschaften
Konfigurieren Ihre Azure-Rolleneigenschaften erfolgt über die Eigenschaftendialogfelder für Ihre workerrolle. Öffnen Sie das Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, und wählen Sie die **Azure** Untermenü. (Wenn die Rolle im Projekt-Explorer von Eclipse nicht angezeigt wird, erweitern Sie das Azure-Projekt im Projekt-Explorer.)

![][ic789599]

Die verschiedenen Eigenschaften, die von festgelegt werden, können die **Eigenschaften** Dialogfelder werden in diesem Thema beschrieben. Beachten Sie, dass viele Eigenschaften automatisch ausgefüllt werden, wenn Sie ein neues Azure-Bereitstellungsprojekt erstellen.

Die folgenden Eigenschaftenseiten stehen für Azure-Rollen zur Verfügung.

* [Eigenschaften des virtuellen Computers](#virtual_machine_properties)
* [Zwischenspeichern von Eigenschaften](#caching_properties)
* [Zertifikateigenschaften](#certificates_properties)
* [Komponenteneigenschaften](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [Endpunkteigenschaften](#endpoints_properties)
* [Umgebungsvariableneigenschaften](#environment_variables_properties)
* [Lastenausgleich / Sitzungseigenschaften-Affinität (bzw. "persistente Sitzungen")](#session_affinity_properties)
* [Eigenschaften des lokalen Speichers](#local_storage_properties)
* [Eigenschaften der Serverkonfiguration](#server_configuration_properties)
* [SSL-abladungseigenschaften](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>Eigenschaften des virtuellen Computers
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Eigenschaften**, und Sie haben die Möglichkeit, die Größe des virtuellen Computers ändern und auch die Anzahl der Instanzen, ändern, wie in der folgenden Abbildung dargestellt.

![][ic719499]

> [!NOTE]
> Nur Windows: Wenn Sie die Anzahl der Instanzen auf einen Wert größer 1 festgelegt, und Sie auch einen Anwendungsserver konfigurieren, gestattet der Toolkit nur 1 Rolleninstanz im Emulator, unabhängig von dieser Einstellung auszuführen. Damit wird Port Bindungskonflikte zwischen den verschiedenen Serverinstanzen (z. B. alle beim Binden an Port 8080) zu vermeiden, wenn sie auf dem gleichen Computer ausgeführt werden. Die gewünschte Einstellung der instanzenanzahl wird beibehalten, jedoch wirksam wird, nur, wenn Sie in der Cloud bereitstellen.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Zwischenspeichern von Eigenschaften
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Caching**. In diesem Dialogfeld können Sie benannte zusammengestellten Memcache-kompatible Caches aktivieren, ermöglichen Sie, um die Webanwendungen zu beschleunigen.

![][ic719483]

Innerhalb der **Caching** Eigenschaftenseite können Sie globale Einstellungen für Folgendes angeben:

* Gibt an, ob zusammengestelltes caching aktiviert ist.
* die Cachegröße als Prozentsatz des Arbeitsspeichers.
* der speicherkontoname zum Speichern des cachezustands, wenn die Anwendung als Cloud-Dienst oder keine ausgeführt wird, wenn Sie nicht, um den Cachestatus speichern möchten. (Der Name des Speicherkontos wird nicht verwendet, wenn Sie Ihre Anwendung im Serveremulator ausführen.) Wenn Sie den Namen des Speicherkontos auf **(Auto)** (Dies ist die Standardeinstellung), verwendet Ihre Cachekonfiguration automatisch dasselbe Speicherkonto als diejenige, die Sie, in Auswählen der **Publish to Azure** Dialogfeld.

> [!NOTE]
> Die **(Auto)** Einstellung müssen den gewünschten Effekt nur, wenn Sie die Bereitstellung mithilfe der Eclipse-Toolkit Veröffentlichen Assistenten veröffentlichen. Wenn stattdessen die cspkg-Datei manuell wie z. B. mit einem externen Mechanismus Veröffentlichen der [Azure-Verwaltungsportal][Azure Management Portal], die Bereitstellung nicht ordnungsgemäß.
> 
> 

Das folgende Dialogfeld zeigt die Eigenschaften für einen Cache.

![][ic719501]

* **Name:** der Name des zusammengestellten Caches.
* **Portnummer:** die Portnummer für den Cache zu verwenden.
* **Ablaufrichtlinie:** einen der folgenden Werte, der angibt, wenn ein Schlüssel im Cache abläuft.
  * **Absolute:** der Schlüssel läuft ab, wenn die Zeit von angegeben **Minuten Gültigkeitsdauer** erreicht ist.
  * **NeverExpires:** des Schlüssels verfügt nicht über eine Ablaufzeit.
  * **SlidingWindow:** der Schlüssel läuft ab, wenn es nicht für den Zeitraum vom angegebenen zugegriffen wurde **Minuten Gültigkeitsdauer**; bei jedem Zugriff darauf ist möglich, wird die Ablaufdauer zurückgesetzt.
* **Minuten Gültigkeitsdauer:** maximale Anzahl von Minuten, bis ein Memcached-Schlüssel, unterliegt der Ablaufrichtlinie Gültigkeitsdauer.
* **Hohe Verfügbarkeit mit replizierter Sicherungen auf unterschiedliche Rolleninstanzen:** aktiviert, bietet hohe Verfügbarkeit mit Sicherungen auf unterschiedliche Rolleninstanzen repliziert. Beachten Sie, dass mindestens zwei Rolleninstanzen faktisch für Ihre Bereitstellung für diese Funktion gewährleistet sein müssen.

Um einen neuen Cache hinzuzufügen, klicken Sie auf die **hinzufügen** Schaltfläche der **Caching** auf der Seite und einen **Configure Named Cache** Dialogfeld wird geöffnet. Geben Sie Werte für die Eigenschaften, die oben beschrieben sind.

Um einen benannten Cache ändern, wählen Sie den Cache, und klicken Sie auf die **bearbeiten** Schaltfläche der **Caching** Eigenschaftenseite. Ein Dialogfeld wird geöffnet, in dem Sie die Cacheeigenschaften ändern. Drücken Sie **OK** um die cachewerte zu speichern.

Um einen Cache zu löschen, wählen Sie den Cache, und klicken Sie auf die **entfernen** Schaltfläche der **Caching** Eigenschaftenseite, und klicken Sie dann auf **Ja** zu bestätigen.

Weitere Informationen zur Verwendung von caching finden Sie unter [Gewusst wie: Verwenden Sie zusammengestellte Caching][How to Use Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Zertifikateigenschaften
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Zertifikate**.

![][ic710964]

In diesem Dialogfeld können Sie hinzufügen oder Entfernen von Zertifikaten, die Ihr Eclipse-Projekt verweist. Beachten Sie, dass die hier aufgeführten Zertifikate nicht automatisch in jedem Java-Schlüsselspeicher gespeichert und sind daher nicht automatisch für jede Verwendung von in einer Java-Anwendung zur Verfügung. Sie sind nur bei Azure registriert, damit sie vorab geladen werden können in der Windows-Zertifikat auf den virtuellen Computern, die Bereitstellung zu speichern und anschließend verwendet von anderer Windows-Software. Derzeit die einzige Funktion des Toolkits, die die Zertifikate verwendet, auf die verwiesen wird auf diese Weise in die **Zertifikate** Dialog ist [SSL-Abladung][SSL Offloading], da die Abhängigkeit von Internet Information Services (IIS) und Application Request Routing (ARR), dabei muss das richtige Zertifikat auf diese Weise verfügbar gemacht werden.

Wenn Sie das Projekt mithilfe des Veröffentlichungs-Assistenten in Azure bereitstellen, werden Sie aufgefordert, zeigen Sie die Personal Information Exchange (PFX)-Dateien, die mit diesen Zertifikaten, zusammen mit ihren Kennwörtern entspricht, um automatisch Hochladen in den Azure-Dienst, aber nur, wenn sie nicht es zuvor hochgeladen wurden.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Komponenteneigenschaften
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Komponenten**. In diesem Dialogfeld haben Sie die Möglichkeit zum Hinzufügen, ändern oder entfernen Sie die Komponenten Ihrer Rolle sowie Ändern der Reihenfolge, in der sie verarbeitet werden.

![][ic719502]

Die Komponenten-Funktion ermöglicht Ihnen das Hinzufügen von Abhängigkeiten zu Ihrer Azure-Bereitstellungsprojekt, z. B. Java-Anwendungsprojekte, spezielle Dateien und ausführbaren befehlszeilenanweisungen, die von Ihrer Bereitstellung erforderlich sind.

Für jede Komponente können Sie Folgendes angeben:

* Der Schritt, die ausgeführt werden, wenn die Komponente in Ihr Azure-Bereitstellungsprojekt importieren, wenn sie erstellt wird.
* Der Schritt, die ausgeführt werden, wenn diese Komponente in der Azure-Cloud bereitstellen.

> [!NOTE]
> Wenn Sie Komponentendateien oder Befehlszeilen angeben, sollten Sie bedenken, dass die Bereitstellung auf einem virtuellen Windows-Computer veröffentlicht wird, damit Ihre benutzerdefinierten Schritte für eine Windows-basiertes Betriebssystem gültig sein müssen. 
> 
> 

Komponenten haben die folgenden Eigenschaften:

* **Importieren:** Methode, die angibt, wie die Komponente in das Projekt importiert wird, wenn das Projekt erstellt wird. Dies kann einer der folgenden Werte sein:
  * **Kopieren:** die Komponente wird kopiert, aus dem lokalen Pfad gemäß der **aus** Eigenschaft in der Rolle **Approot** Verzeichnis.
  * **EAR:** die Komponente ist ein Java Enterprise-Archiv (EAR) aus in den lokalen Pfad angegeben werden, indem Sie ein Enterprise-Anwendungsprojekt importiert die **aus** Eigenschaft. (Dies wird automatisch vom Toolkit aufgrund der Natur des Projekts an dieser Stelle erkannt).
  * **JAR-Datei:** die Komponente ist ein Java-Archiv (JAR) und wird von Java-Projekt in den lokalen Pfad gemäß importiert die **aus** Eigenschaft. (Dies wird automatisch vom Toolkit aufgrund der Natur des Projekts an dieser Stelle erkannt).
  * **None:** wird keine Aktion ausgeführt, um die Komponente zu importieren. Dies ist anwendbar, wenn die Komponente angenommen wird, dass Sie bereits in der Rolle vorhanden sein **Approot** Verzeichnis, oder wenn die Komponente ist lediglich eine ausführbare befehlszeilenanweisung, entsprechend den Angaben in der **als** Eigenschaft bei der **bereitstellen** Methode ist **Exec**.
  * **WAR:** die Komponente ist eine Java-webanwendungsarchiv (WAR) und wird von einem dynamischen Webprojekt in den lokalen Pfad gemäß importiert die **aus** Eigenschaft. (Dies wird automatisch vom Toolkit aufgrund der Natur des Projekts an dieser Stelle erkannt).
  * **PLZ:** die Komponente ist eine Zip-Datei und wird durch das Komprimieren von das Verzeichnis oder die angegebene Datei importiert die **aus** Eigenschaft.
* **Von:** Quellpfads auf dem lokalen Computer zum Ordner oder zur Datei, die die Elemente so importieren Sie in Ihrer Bereitstellung darstellt. In dieser Eigenschaft können Windows-Umgebungsvariablen verwendet werden. Alle Importierbare Komponenten werden in der Rolle importiert **Approot** Verzeichnis, wenn das Projekt erstellt wird.
  
    Beachten Sie, dass Sie die Möglichkeit, eine Komponente aus einem Download bereitzustellen, wenn Sie in der Cloud (nicht im Serveremulator) bereitstellen. Finden Sie unter Informationen zum Hinzufügen einer Komponente aus.    
* **Als:** Dateiname, unter dem die Komponente in der Rolle importiert **Approot** Verzeichnis und letztlich in der Azure-Cloud bereitgestellt. Lassen Sie diese Eigenschaft leer, um dem Namen identisch zu halten, da er sich auf dem lokalen Computer befindet. (Für ausführbare Komponenten, d. h. solche, deren **bereitstellen** Methode festgelegt ist, um **Exec**, dies kann eine beliebige Windows-befehlszeilenanweisung sein.)
  
  > [!IMPORTANT]
  > Wenn Sie Leerzeichen für diesen Wert verwenden, werden diese je nach der Bereitstellungsmethode unterschiedlich behandelt. Wenn die Bereitstellungsmethode **Exec**, Leerzeichen als Trennzeichen für Befehlszeilenargumente und nicht als Teil des Dateinamens interpretiert. Bei allen anderen Bereitstellungsmethoden, die Leerzeichen werden als Teil des Dateinamens interpretiert.
  > 
  > 
* **Stellen Sie bereit:** -Methode, die gibt die Aktion, die auf die Komponente angewendet wird, wenn die Bereitstellung gestartet wird. Dies kann einer der folgenden Werte sein:
  
  * **Kopieren:** die Komponente wird in den Zielpfad kopiert gemäß der **auf** Eigenschaft.
  * **EXEC:** die Komponente ist eine ausführbare Windows-Befehlszeile-Anweisung ausgeführt wird, im Kontext des angegebenen Pfad die **auf** -Eigenschaft, die zum Zeitpunkt der Bereitstellung beginnt.
  * **None:** nichts wird an die Komponente angewendet, wenn die Bereitstellung beginnt.
  * **PLZ:** die Downloadkomponente wird in den Zielpfad gemäß der **auf** Eigenschaft. Diese Methode ist nur verfügbar, wenn die **Import** Eigenschaft **Zip**.
* **An:** Zielpfad auf dem virtuellen Computer, auf dem die Komponente bereitgestellt werden. In dieser Eigenschaft können Windows-Umgebungsvariablen verwendet werden, und die Dateipfade werden relativ zum **Approot**.

Um eine neue Komponente hinzuzufügen, klicken Sie auf die **hinzufügen** Schaltfläche der **Komponenten** Eigenschaftenseite, und ein **Azure Role Component** Dialogfeld wird geöffnet. Geben Sie Werte für die Eigenschaften, die oben beschrieben sind. 

Das folgende Beispiel zeigt ein Beispiel für das Hinzufügen einer neuen WAR-Komponente.

![][ic719503]

Wenn in der Cloud (nicht im Serveremulator), bereitstellen, wenn Sie die Komponente aus einem Download bereitstellen möchten sicherstellen, dass **in der Cloud, INSTEAD OF including in das Paket bereitstellen, von einem** aktiviert ist. Wenn Sie von Azure-Speicherkonto herunterladen möchten, wählen Sie das Speicherkonto aus der **Speicherkonto** Dropdown-Liste (klicken Sie auf die **Konten** Link zu ändern, was in der Liste enthalten ist), die teilweise ausgefüllt wird die **URL** Felds, und geben Sie dann in den verbleibenden Teil der URL. Wenn Sie kein Azure-Speicher verwenden möchten, wählen Sie **(keine)** aus der **Speicherkonto** Dropdown-Menü aus, und geben Sie die URL für die Komponente in der **URL** Feld. Geben Sie eine der folgenden Methoden:

* **Kopieren:** die Downloadkomponente wird in den Zielpfad kopiert gemäß der **in Verzeichnis** Pfad.
* **dieselbe:** dieselbe Methode zum **Deploy from Download** wie für **Deploy from Package**.
* **PLZ:** die Downloadkomponente wird in den Zielpfad gemäß der **in Verzeichnis** Pfad.

Um eine Komponente zu ändern, wählen Sie die Komponente, und klicken Sie auf die **bearbeiten** Schaltfläche der **Komponenten** Eigenschaftenseite. Ein Dialogfeld wird geöffnet, in dem Sie die Komponenteneigenschaften ändern. Drücken Sie **OK** um die Komponentenwerte zu speichern.

Um eine Komponente zu löschen, wählen Sie die Komponente, und klicken Sie auf die **entfernen** Schaltfläche der **Komponenten** Eigenschaftenseite, und klicken Sie dann auf **Ja** zu bestätigen.

Komponenten werden in der aufgeführten Reihenfolge verarbeitet. Verwenden der **nach oben** und **nach unten** Schaltflächen auf der gewünschten Reihenfolge anordnen.

> [!NOTE]
> Die serverkonfigurationsfunktion basiert auf Komponenten ebenfalls. Diese Komponenten nicht entfernt oder bearbeitet werden, ohne die entsprechende Serverkonfiguration zu entfernen. Beim Versuch, Änderungen an solchen Komponenten vorzunehmen, werden Sie dazu aufgefordert.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have the ability to enable or disable remote debugging, as well as create debug configurations, as shown in the following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Endpunkteigenschaften
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Endpunkte**. In diesem Dialogfeld haben Sie die Möglichkeit, erstellen Sie einen Endpunkt als auch bearbeiten oder entfernen einen Endpunkt an, wie in der folgenden Abbildung dargestellt.

![][ic719505]

Um einen Endpunkt hinzuzufügen, klicken Sie auf die **hinzufügen** Schaltfläche der **Endpunkte** Eigenschaftenseite, und ein **Add Endpoint** Dialogfeld wird geöffnet.

![][ic710897]

Geben Sie einen Namen für den Endpunkt, wählen Sie den Typ (entweder **Eingabe**, **intern**, oder **InstanceInput**), und geben Sie den öffentlichen und privaten Port. Drücken Sie **OK** um die neuen endpunktwerte zu speichern.

Je nach Typ des Endpunkts können Sie wie folgt Portbereiche verwenden:

* Für einen Eingabeinstanz-Endpunkt kann der öffentliche Port ein Portbereich (z. B. **2000-2010**) und der private Port ist ein fester Wert.
* Bei einem internen Endpunkt der öffentliche Port nicht verwendet wird, und der private Port kann einen Bereich oder leer sein oder auf ein Sternchen an, dass es automatisch von Azure festgelegt ist.
* Für den eingabeendpunkt kann der öffentliche Port kann nur ein fester Wert sein, und der private Port kann ein fester Wert oder leer sein oder auf ein Sternchen festgelegt werden, um anzugeben, dass es automatisch von Azure festgelegt wird.

Wenn Sie eine einzelne Portnummer anstelle eines Bereichs verwenden möchten, lassen Sie das Textfeld für das Ende des Bereichsende leer.

Die Anwendung kann für die Ports, die eine automatische, wenn Sie festgelegt werden müssen, um zu bestimmen, welcher Port tatsächlich während der Laufzeit verwendet wird, mithilfe der Azure Service Runtime-API, die in der dokumentiert wird die [com.microsoft.windowsazure.serviceruntime Paket Zusammenfassung][com.microsoft.windowsazure.serviceruntime package summary].

<!-- To see how instance input endpoints can be used to help with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

Um einen Endpunkt zu ändern, wählen Sie den Endpunkt, und klicken Sie auf die **bearbeiten** Schaltfläche der **Endpunkte** Eigenschaftenseite. Ein Dialogfeld wird geöffnet, in dem Sie den Endpunktnamen, den Typ und die öffentlichen und privaten Ports ändern. Drücken Sie **OK** um die geänderten endpunktwerte zu speichern.

Um einen Endpunkt zu löschen, wählen Sie den Endpunkt, und klicken Sie auf die **entfernen** Schaltfläche der **Endpunkte** Eigenschaftenseite, und klicken Sie dann auf **Ja** zu bestätigen.

Um einige der Funktionen (z. B. Caching, Sitzungsaffinität oder SSL-Abladung) aktiviert, indem der Benutzer auf eine Rolle ordnungsgemäß zu konfigurieren, kann das Toolkit automatisch spezielle Endpunkte konfigurieren, die zusammen mit benutzerdefinierten Endpunkten aufgeführt werden. Das Toolkit hindert den Benutzer am bearbeiten oder löschen solch automatisch generierter Endpunkte, solange die zugehörige Funktion aktiviert ist.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Umgebungsvariableneigenschaften
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Umgebungsvariablen**. In diesem Dialogfeld haben Sie die Möglichkeit, eine Umgebungsvariable zu erstellen als auch ändern oder entfernen eine Umgebungsvariable wie in der folgenden Abbildung dargestellt.

![][ic719506]

Umgebungsvariablen stehen Ihrem Startskript, wenn die Rolle gestartet wird.

> [!NOTE]
> Wenn Sie Umgebungsvariablen angeben, sollten Sie bedenken, dass die Bereitstellung auf einem virtuellen Windows-Computer veröffentlicht wird, also die Umgebungsvariablen für eine Windows-basiertes Betriebssystem gültig sein müssen.
> 
> 

Als Beispiel für eine Umgebungsvariable, die nicht verfügbar sind, wenn die Rolle gestartet wird, erstellen Sie eine neue Umgebungsvariable, indem Sie auf die **hinzufügen** Schaltfläche. Das folgende Beispiel zeigt eine Umgebungsvariable namens **MyRoleVersion** erstellt und der Wert zugewiesen wird **1.0**.

![][ic659268]

Innerhalb Ihres Jsp-Codes können Sie anzeigen, den Wert mit der `System.getenv` Methode:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Dies ergibt folgende Ausgabe, wenn die Anwendung ausgeführt wird:

![][ic552233]

Um eine Umgebungsvariable zu ändern, wählen Sie die Umgebungsvariable aus, und klicken Sie auf die **bearbeiten** Schaltfläche der **Umgebungsvariablen** Eigenschaftenseite. Ein Dialogfeld wird geöffnet, in dem Sie die Umgebungsvariableneigenschaften ändern. Drücken Sie **OK** an der Umgebung Umgebungsvariablenwerte zu speichern.

Um eine Umgebungsvariable zu löschen, wählen Sie die Umgebungsvariable aus, und klicken Sie auf die **entfernen** Schaltfläche der **Umgebungsvariablen** Eigenschaftenseite, und klicken Sie dann auf **Ja** zu bestätigen.

Um einige der Funktionen (z. B. Serverkonfiguration, Remotedebuggen oder lokaler Speicher) durch den Benutzer auf eine Rolle aktiviert ordnungsgemäß zu konfigurieren, kann das Toolkit automatisch spezielle Umgebungsvariablen konfigurieren, die zusammen mit benutzerdefinierten Umgebungsvariablen aufgeführt werden. Das Toolkit hindert den Benutzer am bearbeiten oder löschen solch automatisch generierter Umgebungsvariablen, solange die zugehörige Funktion aktiviert ist.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Lastenausgleich / Sitzungseigenschaften-Affinität (bzw. "persistente Sitzungen")
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Lastenausgleich**. In diesem Dialogfeld haben Sie die Möglichkeit zum Aktivieren oder deaktivieren die sitzungsaffinität, wie in der folgenden Abbildung dargestellt.

![][ic719492]

Weitere Informationen finden Sie unter [Sitzungsaffinität][Session Affinity]. Beachten Sie außerdem das Verhalten dieser Funktion im Kontext der SSL-Abladung, wie unter [SSL-Abladung][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Eigenschaften des lokalen Speichers
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **lokalen Speicher**. In diesem Dialogfeld haben Sie die Möglichkeit zum Erstellen, ändern oder Entfernen von vorübergehenden, lokalen Speicher für den virtuellen Computer, auf dem die Anwendung ausgeführt wird. Bestimmte Werte können für die Größe des lokalen Speichers festgelegt werden sowie, ob der Inhalt beibehalten werden, wenn die Rolle wiederverwendet wird, wie in der folgenden Abbildung dargestellt.

![][ic719508]

Sie können optional auch eine Umgebungsvariable angeben, die im lokalen Speicher entspricht.

Standardmäßig alle Funktionen, die Sie in Azure bereitstellen platziert (und entzippt) in der **Approot** Ordner der Rolleninstanz. Während die meisten einfache Bereitstellungen gibt es auch nach dem Entpacken passt, der zugeordnete Speicherplatz der **Approot** Verzeichnis ist beschränkt und nicht klar definiert (weniger als 1 GB eine gute Faustregel ist). Ordnet deshalb um sicherzustellen, dass Azure ausreichend Speicherplatz für größere Bereitstellungen, die nicht in Geschäftsgang der **Approot** , Sie sollten Ordnersatz Einrichten eines lokalen Speicher-Ressource mit der **lokalen Speicher** Dialogfeld. Eine einfache Möglichkeit hierzu ist, finden Sie unter [bereitstellen umfangreicher Bereitstellungen][Deploying Large Deployments].

Sie können die Speicherressource einfach aus Startskripts verweisen (z. B. Ihre **startup.cmd**) verwenden die Umgebungsvariable, die automatisch vom Eclipse-Toolkit bei der Ressource zugeordneten entsprechend der **lokalen Speicher** Dialogfeld. Diese Umgebungsvariable enthält den vollständigen Pfad der lokalen Ressource, die Sie zum Zeitpunkt Ihres Startskripts konfiguriert haben. 

Um eine lokale Speicherressource zu ändern, wählen Sie die lokale Speicherressource, und klicken Sie auf die **bearbeiten** Schaltfläche der **lokalen Speicher** Eigenschaftenseite. Ein Dialogfeld wird geöffnet, in dem Sie die Eigenschaften des lokalen Speichers Ressource ändern. Drücken Sie **OK** zum Speichern der Werte der lokalen Speicher-Ressource.

Um eine lokale Speicherressource zu löschen, wählen Sie die lokale Speicherressource, und klicken Sie auf die **entfernen** Schaltfläche der **lokalen Speicher** Eigenschaftenseite, und klicken Sie dann auf **Ja** zu bestätigen.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Eigenschaften der Serverkonfiguration
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **Serverkonfiguration**. In diesem Dialogfeld haben die Möglichkeit, hinzufügen, entfernen und Ändern von Ihrer Bereitstellung verwendeten JDK und Java-Anwendungsserver als auch hinzufügen oder entfernen Sie die Anwendungen (z. B. war-, JAR- oder EAR-Dateien) von Ihrer Bereitstellung verwendet werden.

### <a name="jdk-configuration"></a>JDK-Konfiguration
Dieses Dialogfeld ermöglicht Ihnen das Festlegen der JDK-Paket für Ihre Bereitstellung verwenden. Wenn Sie Eclipse unter Windows verwenden, können Sie angeben, das JDK-Paket lokal verwenden, wenn im Azure-Emulator ausgeführt und haben Sie die Möglichkeit, diese lokale Installation in Azure bereitstellen. Bei nicht-Windows-Betriebssystemen der Emulator-JDK-Einstellung gilt nicht, und das lokal installierte JDK nicht bereitgestellt werden, da er nicht mit Windows kompatibel ist. Jedoch können unabhängig vom Betriebssystem, das Sie verwenden, immer die Auswahl zwischen den 3rd Party JDK-Paketen in Azure bereitzustellen, oder zeigen Sie auf Ihr eigenes Windows-kompatibles JDK-Paket von einem alternativen Downloadspeicherort verweisen.

Im folgenden finden ein Beispiel dafür, wie Sie ein JDK unter Windows angeben können:

![][ic780647]

Wenn Sie Eclipse unter Windows verwenden, können Sie ein JDK für die Verwendung mit dem Serveremulator angeben; zu diesem Zweck stellen Sie sicher **JDK aus diesen Dateipfad für die Tests lokal verwenden** eingecheckt wird die **Emulator Deployment** Abschnitt. Geben Sie den lokalen Pfad zu Ihrem JDK; Sie können zu verschiedenen JDKS durchsuchen, wenn das Konto, das Sie verwenden möchten, nicht automatisch ausgewählt wurde. Sie haben auch die Möglichkeit, Ihr JDK in Azure-Clouddienst bereitstellen; Wählen Sie hierzu die **my local JDK (Auto-Upload, mit der Cloud) bereitstellen** -Option in der **Cloud-Bereitstellung** Abschnitt.

Hinweis: auf nicht-Windows-Betriebssystemen die **Emulator Deployment** Einstellungen und die **my local JDK bereitstellen** Option sind nicht verfügbar. Das folgende Beispiel veranschaulicht ein JDK auf einem Mac oder anderen unterstützten nicht-Windows-Betriebssystem angeben:

![][ic789643]

Unabhängig vom Betriebssystem nun wird, haben Sie die folgenden beiden **Cloud-Bereitstellung** Optionen für die Quelle und Typ Ihres JDK-Pakets:

* **Bereitstellen Sie 3rd Party JDK bei Verfügbarkeit ein Pakets in Azure** 
* **Bereitstellen von benutzerdefinierten download** 

Bei Verwendung der **bereitstellen 3rd Party JDK bei Verfügbarkeit ein Pakets aus Azure** Option:

1. Aktivieren Sie das Kontrollkästchen mit dem Namen **bereitstellen 3rd Party JDK bei Verfügbarkeit ein Pakets aus Azure**.
2. Wählen Sie aus der Dropdown-Liste das 3rd Party JDK-Paket, das in Azure verfügbar ist.
3. Ihre **JDK** Registerkarte sieht etwa wie folgt unter Windows: ![][ic780648] und sieht etwa wie folgt auf Mac OS oder anderen nicht-Windows-Betriebssystemen unterstützt:![][ic789643]
4. Klicken Sie auf **OK**, um Ihre Änderungen zu speichern.
5. Wenn Sie aufgefordert, den Lizenzvertrag aus der 3rd Party JDK paketanbieter, lesen Sie die Lizenzbedingungen. Angenommen, Sie zustimmen, klicken Sie auf **Ja** schließen die **Lizenzvertrag** Dialogfeld.
    Beachten Sie, die die zugrunde liegende Logik für welche Elemente angezeigt werden, in der Dropdown-Liste für die **bereitstellen 3rd Party JDK bei Verfügbarkeit ein Pakets aus Azure** Option angepasst werden. Anpassen der Elemente in der **JDK** Dialogfeld klicken Sie auf die **anpassen** Link. Dies schließt die **JDK** Eigenschaftenseite, und öffnen Sie die **componentsets.xml** Datei in Eclipse, die Sie dann nach Bedarf ändern können. Dokumentation für **componentsets.xml** dient in der **componentsets.xml** Datei selbst.

Bei Verwendung der **ein JDK aus einem benutzerdefinierten Download bereitgestellt** Option:

1. Erstellen Sie eine ZIP-Datei Ihres JDK-Installationsverzeichnisses, um sicherzustellen, dass der Verzeichnisknoten selbst das untergeordnete Element des ZIP-Struktur und nicht dessen Inhalt ist. Notieren Sie den Namen des Verzeichnisses, wie Sie ihn später benötigen, und beachten Sie, diese JDK-Installation auf einem virtuellen Windows-Computer bereitgestellt wird.
2. Laden Sie die ZIP-Datei in Ihr Azure-Speicherkonto als Blob hoch. Sie können hierzu ein extern verfügbares Tool zum Hochladen von Blobs in Azure-Speicher. Es wird empfohlen, einen privaten Blob zu verwenden. Notieren Sie die Blob-URL des ZIP-Dateiinhalts.
3. Aktivieren Sie das Kontrollkästchen mit dem Namen **ein JDK aus einem benutzerdefinierten Download bereitgestellt**.
    Wenn Sie von Azure-Speicherkonto herunterladen möchten, wählen Sie das Speicherkonto aus der **Speicherkonto** Dropdown-Liste (klicken Sie auf die **Konten** Link zu ändern, was in der Liste enthalten ist), die teilweise ausgefüllt wird die **URL** Felds, und geben Sie dann in den verbleibenden Teil der URL. Wenn Sie kein Azure-Speicher verwenden möchten, wählen Sie **(keine)** aus der **Speicherkonto** Dropdown-Menü aus, und geben Sie die URL zu Ihrem JDK-Download in der **URL** Feld. Wenn Sie Azure-Speicher verwenden zu können, müssen die blobnamen in der URL Kleinbuchstaben sein.
4. Sicherstellen, dass die **JAVA_HOME** Textfeld bezieht sich auf den richtigen Verzeichnisnamen. Standardmäßig wird es als Wert der gleichen JDK-Verzeichnisname verweisen, die Sie für die lokale Verwendung ausgewählt haben. Aber das im ZIP enthaltene Verzeichnis besitzt einen anderen Namen (z. B. aufgrund der mit einer anderen Version), aktualisieren Sie den Namen des Verzeichnisses, in dem **JAVA_HOME** Textfeld entsprechend, da diese Einstellung wird in der Cloud (nicht im Serveremulator) verwendet werden.
5. Klicken Sie auf **OK**, um Ihre Änderungen zu speichern.

Das wars. Nun, wenn Sie für die Cloud erstellen, bemerken Sie die Paketgröße wird weit weniger umfangreich werden, während des Erstellungsprozesses sollte normalerweise weniger Zeit beansprucht und die Bereitstellung selbst, wenn Sie in der Cloud veröffentlichen, sollten auch weniger Zeit benötigen. Beachten Sie, dass die **my local JDK (Auto-Upload, mit der Cloud) bereitstellen** oder **ein JDK aus einem benutzerdefinierten Download bereitgestellt** Optionen sind nur dann wirksam, wenn Ihre Anwendung in der Cloud bereitgestellt wird. Sie haben keine Auswirkung auf Ihre serveremulatorerfahrung; die lokale Version der Komponenten wird weiterhin verwendet werden, während der Bereitstellung im Serveremulator. 

### <a name="server-configuration"></a>Serverkonfiguration
Im folgenden ist ein Beispiel dafür, wie Sie einen Anwendungsserver angeben können.

![][ic796926]

Überprüfen Sie, ob die **Bereitstellen eines Servers dieses Typs** aktiviert ist, und wählen Sie dann den Typ des Anwendungsservers, die Sie verwenden möchten.

Für einen Server angeben, für die Cloudbereitstellung verwenden, können Sie die folgenden Optionen nutzen:

1. **Bereitstellen eines 3rd Party Servers in Azure verfügbar** – Dies gilt insbesondere bei Entwicklungs-/Testszenarios, in denen Bereitstellungseffizienz und Einfachheit ist eine Priorität und der Server erfordert eine benutzerdefinierte Konfiguration. Oder wenn Sie einen dieser Server als Ausgangspunkt verwenden möchten, die Sie enthalten jedoch geeignete serveranpassungsschritte in die Startlogik Ihrer Bereitstellung.
2. **Bereitstellen von benutzerdefinierten Download** – Dies gilt insbesondere in Produktionsszenarien bei einen gut vorbereiteten und konfigurierten Server, die Sie in der Cloud verwenden möchten.
3. **Meine lokale Serverinstallation bereitstellen** -Dies ist vor allem in anwendbar, wenn Ihre lokale Serverinstallation bereits für Ihre Verwendung benutzerdefiniert konfiguriert ist. Wenn Sie diese Option auswählen, müssen Sie auch angeben, auf Ihrem lokalen Server-Pfad in der **lokaler Serverpfad** Textfeld unten.

Bei Verwendung der **Bereitstellen eines 3rd Party Servers in Azure verfügbar** Option:

1. Aktivieren Sie das Kontrollkästchen mit dem Namen **Bereitstellen eines 3rd Party Servers in Azure verfügbar**.
2. Wählen Sie aus dem Dropdownmenü die gewünschte Serversoftware aus, die mit Ihrer Bereitstellung in der Cloud verwendet. Beachten Sie: Wenn Sie bereits einen Typ des Servers, verwenden Sie zuvor angegeben haben, werden Sie auf nur einer Cloudserver beschränkt, der in derselben Familie wie der Servertyp ist. Aber wenn Sie einen Servertyp nicht ausgewählt haben, können Sie auswählen, von einem beliebigen Server, die derzeit in Azure verfügbar sind und der Servertyp automatisch für Sie ausgewählt.
3. Klicken Sie auf **OK**, um Ihre Änderungen zu speichern.

Bei Verwendung der **bereitstellen aus einem benutzerdefinierten Download** Option:

1. Stellen Sie sicher, dass Sie bereits einen Servertyp entsprechend den vorhergehenden Schritten ausgewählt haben. Dies teilt dem Plug-in wie den Server aus Ihrem benutzerdefinierten Download bereitgestellt, da er aus derselben Familie wie Ihr ausgewählter Servertyp sein muss.
2. Aktivieren Sie das Kontrollkästchen mit dem Namen **bereitstellen aus einem benutzerdefinierten Download**.
    Wenn Sie von Azure-Speicherkonto herunterladen möchten, wählen Sie das Speicherkonto aus der **Speicherkonto** Dropdown-Liste (klicken Sie auf der **Konten** Link zu ändern, was in der Liste enthalten ist), die teilweise ausgefüllt wird die **URL** Feld, und füllen Sie den verbleibenden Teil der URL mit dem Server ZIP herunterladen, (Wenn Sie mit dem Azure-Speicher, Blob-Namen in der URL muss klein geschrieben sein). Wenn Sie kein Azure-Speicher verwenden möchten, wählen Sie **(keine)** aus der **Speicherkonto** Dropdownelement aus, und geben Sie die URL mit dem Server download ZIP-Datei in die **URL** Feld. Die ZIP-Datei enthält einen untergeordneten Ordner, die Ihrem Installationsverzeichnis des Anwendungsservers darstellt. Beispielsweise, wenn Sie eine ZIP-Datei für Apache Tomcat 7.0.35 verwenden, in die ZIP-Datei wäre es den untergeordneten Ordner, der das Installationsverzeichnis, etwa **Apache-Tomcat-7.0.35**. 
3. Geben Sie den Wert für die Basisverzeichnis-Umgebungsvariable. Wird standardmäßig des Werts für Ihren lokalen Anwendungsserver verwendet wird, sofern vorhanden, aber Sie können einen anderen Wert angeben, wenn Ihr Cloud-Anwendungsserver von Ihrem lokalen Anwendungsserver abweicht. Sie müssen jedoch sicherstellen, dass Ihre Cloud-Anwendungsserver derselben Familie wie der Server wird zuvor ausgewählte Servertyp angehört.
    Wenn Sie Ihre Cloud-Anwendung ZIP-Datei in der Zukunft aktualisieren, können Sie die Einstellung Basisverzeichnis manuell ändern oder, um ihn erneut zu entsprechen, Ihre lokale Einstellung (Wenn Sie Ihren lokalen Anwendungsserver ebenfalls geändert haben).
4. Klicken Sie auf **OK**, um Ihre Änderungen zu speichern.

Die zugrunde liegende Logik für die Elemente angezeigt, in werden der **Server** auf der Registerkarte die **Serverkonfiguration** Eigenschaftenseite angepasst werden. Dies ist eine erweiterte Funktion, die Sie benötigen möglicherweise, wenn die Standardwerte Ihren Anforderungen hinausgehen, oder wenn Sie weitere Server hinzufügen möchten. Anpassen die Logik in der **Server** Dialogfeld klicken Sie auf die **anpassen** Link. Dies schließt die **Serverkonfiguration** Eigenschaftenseite, und öffnen Sie die **componentsets.xml** Datei in Eclipse, die Sie dann nach Bedarf, um den Server Konfigurationsvorlage erweitern ändern können. Dokumentation für **componentsets.xml** dient in der **componentsets.xml** Datei selbst.

Bei Verwendung der **meinem lokalen Server (Auto-Upload, mit der Cloud) bereitstellen** Option:

1. Aktivieren Sie das Kontrollkästchen mit dem Namen **meinem lokalen Server (Auto-Upload, mit der Cloud) bereitstellen**.
2. Mithilfe der **Speicherkonto** Dropdown-Liste **(Auto)**. Bei Angabe von **(Auto)** hier das Eclipse-Toolkit verwenden dasselbe Speicherkonto für Ihren Server mit dem Sie, für die Bereitstellung in Auswählen der **Publish to Azure** Dialogfeld.
3. Klicken Sie auf **OK**, um Ihre Änderungen zu speichern.

Wählen Sie einen Serverinstallationspfad auf Ihrem Computer in der **lokaler Serverpfad** Textfeld, wenn eine der folgenden Bedingungen zutrifft:

* Sie möchten Ihre Bereitstellung im Emulator testen (gilt nur für Windows).
* Sie möchten Ihren lokal installierten Server in der Cloud bereitstellen.
* Sie verwenden möchten herunterladen durch einen benutzerdefinierten serverdownload in der Cloud, in dem Fall, stellen Sie außerdem sicher der **meinem lokalen Server (Auto-Upload, mit der Cloud) bereitstellen** über die Option ausgewählt ist.

Wenn keine der zuvor beschriebenen Optionen auf Ihre Situation zutreffen, ist die Einstellung für den lokalen Server optional.

### <a name="applications-configuration"></a>Anwendungskonfiguration
Im folgenden ist ein Beispiel dafür, wie Sie eine Anwendung angeben können.

![][ic719512]

Klicken Sie auf **hinzufügen** eine andere Anwendung hinzufügen oder **entfernen** eine Anwendung entfernen. Gründen der Effizienz, wenn Sie einen Download für die Quelle einer Anwendung verwenden, wenn Sie in der Cloud verwenden bereitstellen möchten die [Komponenteneigenschaften](#components_properties) usw. eine URL, Storage-Konto angeben. 

Ab der Version April 2014 werden automatisch Ihre Anwendungen in dasselbe Speicherkonto hochgeladen (unter der **Eclipsedeploy** Container) für Ihre Bereitstellung ausgewählt haben. Die Startlogik Ihrer Bereitstellung enthält einen Schritt, der diesen Anwendungen zuerst von diesem Speicherkonto herunterlädt. Dies bedeutet, dass Sie ein upgrade Ihrer Anwendungen in Ihrer Bereitstellung ohne erstellen und bereitzustellen, das gesamte Paket, indem Sie manuell hochladen neuere Versionen der Anwendung direkt in dieses Speicherkonto (z. B. unter Verwendung von Azure-Portal), und Ersetzen Sie dabei die WAR-Dateien ursprünglich vom Toolkit es hochgeladen. Dann initiieren Sie einfach die Wiederverwendung all dieser Rolleninstanzen, die mithilfe des Azure-Verwaltungsportal erneut, oder über die Befehlszeilen-Hilfsprogramme. (Auslösen der rollenwiederverwendung direkt aus innerhalb der Eclipse-Toolkit ist nicht aktuell unterstützt.)

### <a name="notes-about-server-configuration"></a>Hinweise zur Serverkonfiguration
Vorgenommenen Änderungen der **Serverkonfiguration** Eigenschaftenseite werden wiedergegeben, der `<component>` Elemente in der Datei "Package.xml".

Bei Verwendung der **automatisch hochladen...**  oder **Deploy from Download...**  Optionen für das JDK oder Anwendungsserver ausgeführt, und Sie sind für die Cloud (nicht im Serveremulator), erstellen und Sie mit dem Netzwerk verbunden sind, bemerken Sie möglicherweise Buildmeldungen wie die folgenden in der Konsolenausgabe, während der Ant-Builder die Verfügbarkeit des Downloads überprüft:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Bei Auswahl der **Deploy from Download...**  auswählen, werden möglicherweise die folgende Warnung angezeigt, aber die Erstellung wird fortgesetzt:

`[windowsazurepackage] warning: Failed to confirm blob availability! Make sure the URL and/or the access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Diese Warnung ist das einzige Anzeichen, dass die Verfügbarkeit des Downloads überprüft wurde. Also wenn eine Bereitstellung in der Cloud aus irgendeinem Grund fehlschlägt, überprüfen Sie, wenn Sie diese Warnung erhalten haben.

Wenn Sie verwenden möchten, deaktivieren die downloadüberprüfung (z. B., wenn Sie unsicher sind sie unnötig verlangsamt den Build), legen Sie die `verifydownloads` -Attribut `false` in die `<windowsazurepackage>` Element von "Package.xml": 

`<windowsazurepackage verifydownloads="false" ...>` 

Bei Auswahl der **automatisch hochladen...**  Option klicken Sie dann in das Konsolenfenster Sie sehen Buildmeldungen über den Status des Uploads alle 5 Sekunden, wenn ein Upload erforderlich ist.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>SSL-abladungseigenschaften
Öffnen Sie im Kontextmenü für die Rolle im Projekt-Explorer-Bereich von Eclipse, klicken Sie auf **Azure**, und klicken Sie dann auf **SSL-Abladung**. 

![][ic719481]

In diesem Dialogfeld können Sie SSL-Abladung, sodass Sie problemlos Hypertext Transfer Protocol Secure (HTTPS)-Unterstützung in Ihrer Java-Bereitstellung auf Azure zu aktivieren, ohne dass Sie zum Konfigurieren von SSL in Ihrem Java-Anwendungsserver. Weitere Informationen finden Sie unter [SSL-Abladung] [ SSL Offloading] und [wie verwenden SSL-Abladung][How to Use SSL Offloading].

## <a name="see-also"></a>Siehe auch
[Azure-Toolkit für Eclipse][Azure Toolkit for Eclipse]

[Installieren des Azure-Toolkits für Eclipse][Installing the Azure Toolkit for Eclipse]

[Erstellen einer Hello World-Anwendung für Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Azure-Projekteigenschaften][Azure Project Properties]

[Azure-Speicherkontoliste][Azure Storage Account List]

Weitere Informationen zur Verwendung von Azure mit Java finden Sie unter der [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How to Use Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How to Use SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
