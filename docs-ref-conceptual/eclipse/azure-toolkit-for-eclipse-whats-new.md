---
title: "Neuerungen im Azure-Toolkit für Eclipse"
description: "Hier können Sie sich über die neuesten Features des Azure-Toolkits für Eclipse informieren."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 16b066ea-aae7-4c30-9a12-fa0c3711b93e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 31af7e6494f978f341e1f99a30117c57ef30a05b
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-eclipse"></a>Neuerungen im Azure-Toolkit für Eclipse

## <a name="azure-toolkit-for-eclipse-releases"></a>Versionen des Azure-Toolkits für Eclipse
Dieser Artikel enthält Informationen zu den verschiedenen Versionen und den neuesten Updates des Azure-Toolkits für Eclipse.

> [!NOTE]
> Es gibt auch ein Azure-Toolkit für die IntelliJ-IDE. Weitere Informationen finden Sie unter [Azure-Toolkit für IntelliJ].
> 
> 

### <a name="april-14-2017"></a>14. April 2017
Die Version des Azure-Toolkits für Eclipse vom April 2017 umfasst folgende Verbesserungen:

* **Verbesserte Azure-Anmeldung**: Das Azure-Toolkit für Eclipse unterstützt nun zwei Methoden zur Anmeldung bei Ihrem Azure-Konto: *Interaktiv* und *Automatisch*. Weitere Informationen finden Sie in der [Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse].
* **Veröffentlichen mit Docker-Containern**: Sie können jetzt mithilfe des Azure-Toolkits für Eclipse Ihre Webanwendungen als Docker-Container veröffentlichen. Weitere Informationen finden Sie unter [Informationen zum Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für Eclipse].
* **Speicherkontenverwaltung**: Das Azure-Toolkit für Eclipse unterstützt jetzt das Verwalten Ihrer Speicherkonten in der Azure-Explorer-Ansicht. Weitere Informationen finden Sie unter [Verwalten von Speicherkonten mit dem Azure-Explorer für Eclipse].
* **Verwaltung virtueller Computer**: Das Azure-Toolkit für Eclipse unterstützt jetzt das Verwalten Ihrer virtuellen Computer in der Azure-Explorer-Ansicht. Weitere Informationen finden Sie unter [Verwalten virtueller Computer mit dem Azure-Explorer für Eclipse].
* **Entfernen der Unterstützung für das Remotedebuggen**. Das Remotedebuggen von Java-Web-Apps in Azure App Service wurde aus dem Azure-Toolkit für Eclipse entfernt. Dies war es erforderlich, um einige Probleme zu beheben, die bei Kunden bei Verwendung des Toolkits aufgetreten waren.

### <a name="august-26-2016"></a>26. August 2016
Das Release des Azure-Toolkits für Eclipse vom August 2016 umfasst folgende Erweiterungen:

* **Benutzerdefinierte JDK-Distributionen**. Das Azure-Toolkit für Eclipse unterstützt jetzt das Angeben und Bereitstellen einer beliebigen JDK-Version in Ihrem Azure-WebApp-Container:
  * Zusätzlich zu den von Azure bereitgestellten JDKs können Sie aus einem umfassenden Angebot an Zulu OpenJDK-Versionen auswählen, die von Azul Systems für Azure zur Verfügung gestellt wurden.
  * Sie können auch eine eigene JDK-Distribution angeben, wenn Sie diese als ZIP-Datei in Ihr Speicherkonto hochladen.
* **Verbesserungen der Azure Explorer-Ansicht**:
  * Unterstützung für die Verwaltung virtueller Computer über das neue Resource Manager-Modell von Azure: Sie können auf Resource Manager basierende virtuelle Computer auflisten, erstellen und löschen, ohne die IDE verlassen zu müssen.
  * Unterstützung für die Blobverwaltung im Speicherkonto über Azure Resource Manager, zur Ergänzung der vorhandenen Funktionalität für die Verwaltung „klassischer“ Speicherkonten.
* **Microsoft JDBC Driver 6.0 für SQL Server**. Dieses Update enthält den neuesten JDBC-Treiber für Microsoft SQL Server (Version 6.0) – dieser wird jetzt als Bibliothek bereitgestellt, die Sie ganz einfach zu Ihren Java-Projekten hinzufügen können. Die ältere Version wird hierdurch ersetzt.

### <a name="june-29-2016"></a>29. Juni 2016
Die Version des Azure-Toolkits für Eclipse vom Juni 2016 umfasst folgende Erweiterungen:

* **Java 8 erforderlich**. Für das Azure-Toolkit für Eclipse ist nun Java 8 erforderlich, was allerdings nur für das Toolkit gilt. Ihre Anwendungen können weiterhin alle Java-Versionen verwenden, die von Azure unterstützt werden.
* **Unterstützung der neuesten Java JDKs**. Die neuesten Versionen der Java JDKs werden jetzt vom Azure-Toolkit für Eclipse unterstützt.
* **Unterstützung des Azure SDK, Version 2.9.1**. Die neueste Version des Azure SDK ist jetzt die Mindestvoraussetzung für das Azure-Toolkit für Eclipse.
* **Integrierte Beispiele**. Das Azure-Toolkit für Eclipse bietet jetzt mehrere Beispielanwendungen, die Entwicklern den Einstieg erleichtern sollen.
* **Integration von HDInsight-Tools**. Die Azure HDInsight-Tools stehen nun im Paket mit dem Azure-Toolkit für Eclipse zur Verfügung. Weitere Informationen finden Sie unter [Verwenden des HDInsight-Tools-Plug-Ins für Eclipse zum Erstellen von Spark-Anwendungen für HDInsight Spark-Cluster unter Linux].
* **Remotedebuggen von Java-Web-Apps**. Das Azure-Toolkit für Eclipse unterstützt jetzt das Remotedebuggen von Java-Web-Apps in Azure App Service.
* **Unterstützung der Luna-Version von Eclipse.** In diesem Zusammenhang wird mindestens die Luna-Version der Eclipse-IDE benötigt.

### <a name="april-12-2016"></a>12. April 2016
Die Version des Azure-Toolkits für Eclipse vom April 2016 umfasst folgende Erweiterungen:

* **Unterstützung des Azure SDK, Version 2.9.0**. Die neueste Version des Azure SDK ist jetzt die Mindestvoraussetzung für das Azure-Toolkit für Eclipse.
* **Verschiedene Verbesserungen bei der Benutzerfreundlichkeit, Reaktionsfähigkeit und Leistung in Bezug auf die Unterstützung von Azure-Web-Apps**. Eine Reihe von Leistungsoptimierungen bei der Kommunikation zwischen Toolkit und Azure führen zu einer besseren Reaktionsfähigkeit der Benutzeroberfläche.
* **Möglichkeit zum Löschen eines vorhandenen Webanwendungscontainers in Azure direkt aus Eclipse heraus**. Mit dem Azure-Toolkit für Eclipse können Sie jetzt einen vorhandenen Azure-Webcontainer löschen, ohne Eclipse zu verlassen.

### <a name="march-7-2016"></a>7. März 2016
Die Version des Azure-Toolkits für Eclipse vom März 2016 umfasst folgende Erweiterungen:

* **Unterstützung der schnellen Bereitstellung schlanker Java-Anwendungen**. Azure-Toolkit für Eclipse unterstützt jetzt die schnelle Bereitstellung von einfachen Java-Anwendungen in Azure Web App-Container, sodass die Bereitstellung von Java-Anwendungen jetzt Sekunden statt Minuten dauert.
* **Unterstützung der Web-App-Verwaltung in der Azure Explorer-Ansicht**. Die Azure-Explorer-Ansicht im Toolkit unterstützt nun das Auflisten, Starten und Beenden von Azure-Web-Apps.
* **Aktualisierte OpenJDK-Distributionen für Tomcat, Jetty und Zulu**. Das Azure-Toolkit für Eclipse bietet Unterstützung für aktualisierte Versionen von Tomcat, Jetty und Zulu OpenJDK für Java-Bereitstellungen in Azure-Cloud-Diensten.

### <a name="january-4-2016"></a>4. Januar 2016
Die Version des Azure-Toolkits für Eclipse vom Januar 2016 umfasst folgende Erweiterungen:

* **Unterstützung der Zulu OpenJDK-Updates**. Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].
* **Aktualisierte Tomcat- und Jetty-Distributionen**. Die im Rahmen von Microsoft Azure verfügbaren Jetty- und Tomcat-Distributionen für die Verwendung mit dem Azure-Toolkit für Eclipse wurden aktualisiert.
* **Featureübereinstimmung zwischen den Eclipse- und IntelliJ-Toolkits für Azure**. Das Azure-Toolkit für Eclipse und das [Azure-Toolkit für IntelliJ] unterstützen nun dieselben Features.

### <a name="september-1-2015"></a>1. September 2015
Die Version des Azure-Toolkits für Eclipse vom September 2015 umfasst folgende Erweiterungen:

* **Unterstützung der Zulu OpenJDK-Updates**. Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].
* **Aktualisierte Tomcat- und Jetty-Distributionen**. Die im Rahmen von Microsoft Azure verfügbaren Jetty- und Tomcat-Distributionen für die Verwendung mit dem Azure-Toolkit für Eclipse wurden aktualisiert. (Mit diesen Distributionen können Entwickler schnell Entwicklungs- und Testprojekte mit dem Azure-Toolkit für Eclipse erstellen).
* **Unterstützung automatisch aktualisierter Tomcat- und Jetty-Verweise**. Zusätzlich zu den spezifischen Versionen von Tomcat und Jetty, die im Rahmen von Azure verfügbar sind, können Entwickler jetzt auch auf Distribution mit der Bezeichnung „Neueste (automatisch aktualisiert)“ verweisen. (Das Recycling erfolgt automatisch, über das Azure-Portal können Entwickler aber manuell einen Recyclingvorgang auslösen.) Dieses neue Feature hat den Vorteil, dass Entwickler ihre Serversoftware ohne erneute Bereitstellung ihrer Anwendung aktualisieren können. (
* Diese Funktion ist momentan nur für Entwicklungs- und Testszenarien sowie für nicht geschäftskritische Anwendung vorgesehen und sollte nicht in der Produktion eingesetzt werden.)
* **Azure Explorer-Ansicht für Blobs, Warteschlangen und Tabellen in Azure Storage**. Damit können Entwickler eine Reihe allgemeiner Aufgaben für Speicherartefakte direkt über die Eclipse-IDE erledigen und beispielsweise Blobs löschen, hochladen oder herunterladen.

### <a name="august-1-2015"></a>1. August 2015
Die Version des Azure-Toolkits für Eclipse vom August 2015 umfasst folgende Erweiterungen:

* **Verwaltung von Application Insights-Instrumentierungsschlüsseln**. Mit diesem Update können Sie Ihre Application Insights-Instrumentierungsschlüssel direkt über die Eclipse-IDE abrufen, erstellen und verwalten.
* **Microsoft JDBC Driver 4.1 für SQL Server**. Dieses Update beinhaltet die Unterstützung des neuesten JDBC-Treibers für Microsoft SQL Server.
* **Version 2.7 des Azure-SDKs**. Dieses neueste Update für das Azure-SDK ist die neue erforderliche Komponente, wenn das Toolkit unter Windows installiert wird. (Für Windows-fremde Betriebssysteme nicht relevant.)
* **Unterstützung des v7-Updates von Zulu OpenJDK**. Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].

### <a name="may-1-2015"></a>1. Mai 2015
Die Version des Azure-Toolkits für Eclipse vom Mai 2015 umfasst folgende Erweiterungen:

* **Verbesserte Benutzeroberfläche für die Serverauswahl**. Diese Version vereinfacht die Verwendung des Toolkits unter Windows-fremden Betriebssystemen.
* **Unterstützung von Maven-Projekten**. Diese Version unterstützt Maven-Projekte als Anwendungen, was die Bereitstellung in Azure und die Konfiguration von Application Insights durch das Toolkit ermöglicht.
* **Version 2.6 des Azure-SDKs**. Dieses neueste Update für das Azure-SDK ist die neue erforderliche Komponente, wenn das Toolkit unter Windows installiert wird. (Für Windows-fremde Betriebssysteme nicht relevant.)
* **Bereitstellungsupgrade statt Neuveröffentlichung**. Wenn Sie ein Bereitstellungsprojekt veröffentlichen, nachdem die vorherige Version bereits aktiv ist, verwendet das Toolkit nun die Bereitstellungsupgradefunktion von Azure, anstatt wie bisher die vorherige Bereitstellung herunterzufahren und von Grund auf neu zu veröffentlichen. Dies ermöglicht eine möglichst unterbrechungsfreie Ausführung des Clouddienst, sorgt auch während Updates für hohe Verfügbarkeit und beschleunigt die Neuveröffentlichung.
* **Unterstützung der neuesten Version von Zulu OpenJDK (v8, Update 40)**. Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].

### <a name="march-9-2015"></a>9. März 2015
Die Version des Azure-Toolkits für Eclipse vom März 2015 umfasst folgende Erweiterungen:

* **Unterstützung von Mac, Ubuntu und weiteren Linux-Varianten**. Diese Version des Azure-Toolkits für Eclipse unterstützt nun auch Mac OS und einige Unix-Plattformen. Dadurch können Entwickler das Toolkit unter Windows-fremden Betriebssystemen installieren und mithilfe von Eclipse Java-Projekte erstellen, konfigurieren und in Azure Cloud Services (PaaS) veröffentlichen.

> [!NOTE]
> Diese Funktion befindet sich in der Vorschauphase und sollte nicht in Produktionsumgebungen verwendet werden. Es gibt zwar keine kundensupportbezogene Vereinbarung zum Servicelevel (Service Level Agreement, SLA), wir sind jedoch für jegliches Feedback dankbar.
> 
> 

* **Neues Application Insights-Plug-In**. Entwickler können jetzt mithilfe von Application Insights in Azure automatische Servertelemetrie konfigurieren.
* **Ant-basierte Automatisierung der Bereitstellung über die Befehlszeile**. Dieses Feature ermöglicht Entwicklern die Automatisierung der Veröffentlichung neuerer Bereitstellungsversionen mithilfe von Ant außerhalb von Eclipse. Nach der erstmaligen Bereitstellung eines Projekts über Eclipse wird automatisch ein vorab generiertes Skript für das Projekt konfiguriert. Dieses kann dann zur vollständigen Automatisierung nachfolgender Bereitstellungen über die Befehlszeile verwendet werden.
* **Einfachere und schnellere Bereitstellung dank Verfügbarkeit von Tomcat und Jetty in Azure**. Entwickler können nun direkt auf verschiedene, in Azure verfügbare Versionen von Tomcat und Jetty verweisen, anstatt einen Java-Server in ihre Konten hochzuladen (oder das Toolkit zu verwenden). So lassen sich schnell Einstiegsszenarien ohne Upload eines Java-Servers realisieren.
* **Einfachere Methode zum Veröffentlichen von Java-Web-Apps in Azure Cloud Services**. Zur Verbesserung der Lernkurve in einfachen Entwicklungs- und Testszenarien können Entwickler Java-Anwendungen jetzt direkter in Azure veröffentlichen. Anwendungen werden mit einer Standardinstanz von Tomcat v8 und Zulu JVM (OpenJDK) bereitgestellt, anstatt den Prozess zum Erstellen und Konfigurieren eines Azure-Bereitstellungsprojekts durchlaufen zu müssen.

### <a name="january-30-2015"></a>30. Januar 2015
Die Version des Azure-Toolkits für Eclipse vom Januar 2015 umfasst folgende Erweiterungen:

* **Unterstützung von IBM® WebSphere® Application Server Liberty Core**. Diese Version fügt IBM WebSphere Application Server Liberty Core zur Liste der unterstützten Anwendungsserver hinzu, über die mithilfe des Toolkits Bereitstellungen in Azure möglich sind. Diese neueste Ergänzung erweitert die aktuelle Liste der Anwendungsserver, die &quot;standardmäßig&quot; durch das Toolkit unterstützt werden. Dazu zählen bereits verschiedene Versionen von Tomcat, Jetty, JBoss und GlassFish.
* **Einbeziehung von Application Insights SDK**. Diese neu veröffentlichte Client-API-Bibliothek (v0.9.0) ist jetzt Teil des Pakets für Azure-Bibliotheken für Java.
* **Aktualisiertes Paket für Azure-Bibliotheken für Java**. Dieses Update enthält Azure-Bibliotheken für Java v0.7.0 und die Speicherclient-API v2.0.0 sowie das neu veröffentlichte Application Insights SDK v0.9.0.

### <a name="november-12-2014"></a>12. November 2014
Die Version des Azure-Toolkits für Eclipse vom November 2014 umfasst folgende Erweiterungen:

* **Unterstützung von Azure SDK 2.5**. Dieses neueste Update für das Azure-SDK ist die neue erforderliche Komponente für das Toolkit.
* **Unterstützung der aktualisierten Version des v1.8-, v1.7- und v1.6-Pakets von Zulu OpenJDK**. Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].
* **Unterstützung der neuen Standard D-Größen für Clouddienste**für mehr Leistung und zusätzliche Speicherressourcen. Weitere Informationen finden Sie unter [Größen virtueller Computer und Clouddienste für Azure].

### <a name="october-17-2014"></a>17. Oktober 2014
Die Version des Azure-Toolkits für Eclipse vom Oktober 2014 umfasst folgende Erweiterungen:

* **Leistungssteigerungen bei der Veröffentlichung in der Cloud**. Abonnementinformationen werden wesentlich schneller geladen, wenn Benutzer über mehrere Abonnements und Speicherkonten verfügen.
* **Unterstützung der aktualisierten Version des v1.8-Pakets von Zulu OpenJDK**. Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].
* **Unterstützung der Ausmusterung älterer Versionen von Drittanbieter-JDKs**. Veraltete JDK-Pakete werden nicht mehr im Dropdownmenü für neue Bereitstellungsprojekte angezeigt. Vorhandene Projekte mit Verweisen auf veraltete JDK-Pakete können diese vorerst weiter verwenden. Es empfiehlt sich jedoch, diese Projekte auf die neueste Version zu aktualisieren.
* **Aktualisierte Version des Pakets für Azure-Bibliotheken für die Java-Client-API-Bibliothek**. Weitere Informationen finden Sie unter [Microsoft Azure-Client-API].
* **Fehlerbehebungen.** Diese Version enthält zahlreiche Fehlerbehebungen, die auf Benutzerberichten und Tests basieren.

### <a name="august-5-2014"></a>5. August 2014
Die Version des Azure-Toolkits für Eclipse vom August 2014 umfasst folgende Erweiterungen:

* **Unterstützung von Azure SDK 2.4.** Ältere Versionen des Eclipse-Toolkits können mit diesem neu veröffentlichten SDK nicht mehr verwendet werden.
* **Aktualisierte Versionen des v1.6-, v1.7- und v1.8-Pakets von Zulu OpenJDK.** Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].
* **Aktualisierte Version des Pakets für Azure-Bibliotheken für die Java-Client-API-Bibliothek.** Weitere Informationen finden Sie unter [Microsoft Azure-Client-API].
* **Unterstützung des neuesten Formats für die Veröffentlichungseinstellungsdatei.** Version 2.0 des Formats für die Veröffentlichungseinstellungsdatei wird nun unterstützt.
* **Geänderte Architektur für das Cloudveröffentlichungsfeature.** Das Toolkit verwendet zur Unterstützung der Cloudveröffentlichung nun die neu veröffentlichte Microsoft Azure-Client-API für Java.
* **Fehlerbehebungen.** Diese Version enthält eine Reihe von Fehlerbehebungen, die von Benutzern angefordert wurden.

### <a name="june-12-2014"></a>12. Juni 2014
Die Version des Azure-Toolkits für Eclipse vom Juni 2014 ist ein kleineres Wartungsupdate mit folgenden Erweiterungen:

* **Unterstützung des v1.8-Pakets von Zulu OpenJDK.** Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].
* **Aktualisierte Versionen des v1.6- und v1.7-Pakets von Zulu OpenJDK.** Weitere Informationen finden Sie auf der [Azul Systems-Webseite zu Zulu OpenJDK].
* **Aktualisierte Version des Pakets für Azure-Bibliotheken für die Java-Client-API-Bibliothek.** Weitere Informationen finden Sie unter [Microsoft Azure-Client-API].
* **Fehlerbehebungen.** Diese Version enthält eine Reihe von Fehlerbehebungen, die von Benutzern angefordert wurden.

### <a name="april-4-2014"></a>4. April 2014
Die Version des Azure-Plug-Ins für Eclipse vom April 2014 wird veröffentlicht. Hierbei handelt es sich um ein begleitendes Update für Azure SDK 2.3. Dieses ist eine erforderliche Komponente und wird beim Installieren des Plug-Ins automatisch heruntergeladen. Das Update enthält neue Features, Fehlerbehebungen und einige feedbackbasierte Verbesserungen der Benutzerfreundlichkeit (verglichen mit der Vorschauversion vom Februar 2014):

* **Unterstützung der Version 2.3 des Azure-SDKs.** Für die Version des Azure-Plug-Ins für Eclipse vom April 2014 wird Azure SDK 2.3 benötigt. Wenn Sie das neue Plug-In verwenden möchten und noch nicht über Azure SDK 2.3 verfügen, werden Sie aufgefordert, die Installation zuzulassen. Verwenden Sie Azure SDK 2.3 nicht mit älteren Versionen des Plug-Ins.
* **Upgraden von Anwendungen ohne vollständige Paketbereitstellung.** Wenn Sie Java-Anwendungen bereitstellen, die Teil Ihres Projekts sind, werden diese nun automatisch durch das Plug-In in Ihr ausgewähltes Speicherkonto hochgeladen. Dadurch können Sie es zur Bereitstellung der neuesten Anwendungskomponenten aktualisieren und die Rolleninstanzen recyceln, ohne das gesamte Paket neu erstellen und bereitstellen zu müssen.
* **Erkennung von Tomcat 8 als Anwendungsserver.** Wenn Sie auf Ihrem Computer auf der Registerkarte **Server** im Dialogfeld **Azure-Bereitstellungsprojekt** ein Tomcat 8-Installationsverzeichnis auswählen, wird dieses nun vom Plug-In automatisch erkannt, und das Plug-In kann Tomcat 8 ähnlich wie ältere Tomcat-Versionen aus der Liste automatisch bereitstellen.
* **Paketupdates für Azul Zulu OpenJDK: v1.7 (Update 51) und v1.6 (Update 47).** Ab dieser Version ist das Paketupdate 51 für Zulu OpenJDK v7 von Azul Systems verfügbar. Außerdem werden auch OpenJDK v6-Pakete verfügbar. Den Anfang macht das Update 47. Diese Updates stehen zusätzlich zu den bereits verfügbaren Paketupdates 45, 40 und 25 von Zulu OpenJDK v7 zur Verfügung.
* **Unterstützung virtueller Microsoft Azure-Maschinen der Größe A8 und A9.** Clouddienste können nun auf virtuellen Maschinen mit umfangreichem Arbeitsspeicher (Größe A8 und A9) bereitgestellt werden. Weitere Informationen zu diesen VM-Größen finden Sie unter [Größen virtueller Computer und Clouddienste für Azure].
* **Automatische Umleitung von HTTP zu HTTPS bei SSL-fähigen Rollen.** Wenn Ihr Clouddienst nur HTTPS-Rollen enthält und die Benutzeranforderung HTTP angibt, erfolgt eine automatische Umleitung zu HTTPS. Es muss also keine separate Rolle zur Verarbeitung von HTTP-Anforderungen erstellt werden.
* **Express-Emulator für die lokale Emulation.** Der Azure-Express-Emulator wird jetzt beim lokalen Debuggen von Anwendungen als Emulator verwendet.
* **Umbenennung von Azure in Microsoft Azure.** Die Benutzeroberfläche wurde im Zuge der Umbenennung von Azure entsprechend angepasst.

### <a name="february-6-2014"></a>6. Februar 2014
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom Februar 2014 wird veröffentlicht. Das Update enthält neue Features, Fehlerbehebungen und einige feedbackbasierte Verbesserungen der Benutzerfreundlichkeit (verglichen mit der Vorschauversion vom Oktober 2013):

* **Unterstützung der SSL-Abladung.** SSL-Abladung wurde als Feature hinzugefügt. Dies ermöglicht die unkomplizierte Unterstützung von HTTPS (Hypertext Transfer-Protokoll Secure) in Ihrer Java-Bereitstellung für Azure, ohne SSL (Secure Sockets Layer) auf Ihrem Java-Anwendungsserver konfigurieren zu müssen. Dies ist besonders in Szenarien mit Sitzungsaffinität und/oder authentifizierter Kommunikation relevant. Ein Beispiel wäre die Verwendung des bereits vom Toolkit unterstützten Access Control Service (ACS)-Filters. Weitere Informationen finden Sie unter [SSL-Abladung] sowie unter [Vorgehensweise: Verwenden der SSL-Abladung].
* **Erkennung von GlassFish 4 als Anwendungsserver.** Wenn Sie auf Ihrem Computer auf der Registerkarte **Server** im Dialogfeld **Azure-Bereitstellungsprojekt** ein GlassFish 4-Installationsverzeichnis auswählen, wird dieses nun vom Plug-In automatisch erkannt, und das Plug-In kann GlassFish OSE 4 ähnlich wie die bereits in der Liste enthaltene GlassFish OSE 3-Version automatisch bereitstellen.
* **Paketupdate 45 für Azul Zulu OpenJDK.** Ab dieser Version ist zusätzlich zu den bereits verfügbaren Updates 40 und 25 das Update 45 für Zulu (OpenJDK v7-Paket) von Azul Systems verfügbar.
* **Unterstützung der Automatikfunktion für private Endpunktports.** Sie können einen privaten Port für Eingabeendpunkte und interne Endpunkte auf „Automatisch“ festlegen, um eine automatische Portzuweisung durch Azure zu ermöglichen. Bislang konnte lediglich eine bestimmte Portnummer zugewiesen werden.
* **Unterstützung der Anpassung des Zertifikatnamens (Certificate Name, CN) auf der Benutzeroberfläche zum Erstellen selbst signierter Zertifikate.** Bislang wurde für alle neuen Zertifikate der gleiche hartcodierte Name verwendet. Nun können Sie einen eigenen Zertifikatnamen angeben, um für unterschiedliche Zwecke verwendete Zertifikate im Azure-Portal besser unterscheiden zu können.
* **Azure-Symbolleiste** : Die Azure-Symbolleiste wurde wie folgt aktualisiert: 
  * ![][ic710876] Dieses Symbol wurde für **Neues Azure-Bereitstellungsprojekt**hinzugefügt.
  * ![][ic710877] Dieses Symbol wurde zum schnellen Aufrufen des Dialogfelds für die Erstellung selbstsignierter Zertifikate hinzugefügt.
* **Unterstützung virtueller Azure-Maschinen der Größe A5.** Clouddienste können nun auf virtuellen Maschinen mit umfangreichem Arbeitsspeicher (Größe A5) bereitgestellt werden. Weitere Informationen zu dieser VM-Größe finden Sie unter [Größen virtueller Computer und Clouddienste für Azure].
* **Unterstützung von Microsoft Windows Server 2012 R2.** Windows Server 2012 R2 kann nun als Cloudbetriebssystem ausgewählt werden.

### <a name="october-22-2013"></a>22. Oktober 2013
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom Oktober 2013 wird veröffentlicht. Das Update enthält neue Features, Fehlerbehebungen und einige feedbackbasierte Verbesserungen der Benutzerfreundlichkeit (verglichen mit der Vorschauversion vom September 2013):

* **Unterstützung der Version 2.2 des Azure-SDKs.** Die Vorschauversion des Azure-Plug-Ins für Eclipse vom Oktober 2013 unterstützt Azure SDK 2.2. Das Plug-In kann weiterhin mit Azure SDK 2.1 verwendet werden. Falls nicht mindestens Azure SDK 2.1 installiert ist, wird Azure SDK 2.2 automatisch installiert.
* **Paketupdate 40 für Azul Zulu OpenJDK.** Wie bereits für die Vorschauversion vom September 2013 angekündigt, ermöglicht das Plug-In nun die Verwendung eines JDK-Pakets von einem Drittanbieter direkt in Azure, ohne dass Sie Ihr eigenes JDK-Paket hochladen müssen. In der Version vom Oktober 2013 ist zusätzlich zum ursprünglich veröffentlichten Update 25 nun auch das Update 40 für Zulu (OpenJDK v7-Paket) von Azul Systems verfügbar.
* **Cloudbereitstellungslink im Aktivitätsprotokoll.** Im Azure-Aktivitätsprotokoll können Sie bei einer Bereitstellung mit dem Status **Veröffentlicht** auf **Veröffentlicht** klicken, da es sich hierbei nun um einen Link zu Ihrer Bereitstellung handelt. Die Bereitstellung wird dann in Ihrem Browser geöffnet. (Der Status des **Veröffentlicht** hatte vorher die Bezeichnung **Ausgeführt**.)
* **Zum Veröffentlichungszeitpunkt verfügbare Zielbetriebssystemauswahl.** Das Dialogfeld **Veröffentlichen in Azure** enthält ein neues Feld namens **Zielbetriebssystem**, um das Festlegen Ihres Zielbetriebssystems zu vereinfachen.
* **Automatisches Überschreiben einer vorherigen Bereitstellung.** Das Dialogfeld **Veröffentlichen in Azure** enthält ein neues Kontrollkästchen namens **Vorherige Bereitstellung überschreiben**. Wenn diese Option aktiviert ist, wird bei der Veröffentlichung Ihrer neuen Bereitstellung automatisch die vorherige Bereitstellung überschrieben. Dadurch treten keine &quot;409-Konflikte&quot; auf, wenn Sie bei der Veröffentlichung den gleichen Ort verwenden, ohne zuvor die Veröffentlichung der vorherigen Bereitstellung aufzuheben.
* **Erkennung von Jetty 9 als Anwendungsserver.** Wenn Sie auf Ihrem Computer auf der Registerkarte **Server** im Dialogfeld **Azure-Bereitstellungsprojekt** ein Jetty 9-Installationsverzeichnis auswählen, wird dieses nun vom Plug-In automatisch erkannt, und das Plug-In kann Jetty 9 ähnlich wie ältere Jetty-Versionen aus der Liste automatisch bereitstellen.
* **Hinzufügen einer Rolle über das Projektkontextmenü.** Das **Azure**-Projektkontextmenü enthält ein neues Menüelement namens **Rolle hinzufügen**. Damit können Sie Ihrem Azure-Projekt schneller und einfacher eine neue Rolle hinzufügen.
* **Paketupdate für die Azure-Bibliotheken für die Java-Bibliothek.** Basiert auf Version 0.4.6 der [Microsoft Azure-Client-API].

### <a name="september-25-2013"></a>25. September 2013
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom September 2013 wird veröffentlicht. Das Update enthält neue Features, Fehlerbehebungen und einige feedbackbasierte Verbesserungen der Benutzerfreundlichkeit (verglichen mit der Vorschauversion vom August 2013):

* **Möglichkeit zum Bereitstellen des verfügbaren Azul Zulu OpenJDK-Pakets in Azure.** Für die Angabe des gewünschten JDK-Pakets für Ihre Azure-Bereitstellung wurde eine neue Option hinzugefügt. Mit dieser Option können Sie ein JDK-Drittanbieterpaket direkt in der Azure-Cloud bereitstellen, ohne ein eigenes Paket hochladen zu müssen. Azul Systems bietet mit Zulu ein erstes geeignetes OpenJDK-Paket an, das nun mit dieser Option bereitgestellt werden kann.
* **Paketupdate für die Azure-Bibliotheken für die Java-Bibliothek.** Basiert auf Version 0.4.5 der [Microsoft Azure-Client-API].

### <a name="august-1-2013"></a>1. August 2013
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom August 2013 wird veröffentlicht. Hierbei handelt es sich um ein begleitendes Update für Azure SDK 2.1. Dieses ist eine erforderliche Komponente und wird beim Installieren des Plug-Ins automatisch heruntergeladen. Das Update enthält neue Features, Fehlerbehebungen und einige feedbackbasierte Verbesserungen der Benutzerfreundlichkeit (verglichen mit der Vorschauversion vom Juli 2013):

* **Entfernung von Optionen zum Einbetten des lokalen JDK-Pakets und des lokalen Anwendungsservers in das Bereitstellungspaket.** Das Herunterladen des JDK-Pakets und des Anwendungsservers aus dem Cloudspeicher zum Zeitpunkt der Bereitstellung ist dem Einbetten dieser Elemente in das Paket vorzuziehen, da Sie durch das Herunterladen der Elemente von einem kleineren Bereitstellungspaket, kürzeren Bereitstellungszeiten und einer einfacheren Wartung profitieren. Daher wurden die Optionen zum Einbetten des JDK-Pakets und des Anwendungsservers in das Bereitstellungspaket entfernt. Bereits vorhandene Projekte, bei denen das lokale JDK-Paket und der lokale Anwendungsserver Teil des Bereitstellungspakets sind, werden automatisch konvertiert. Dabei werden das JDK-Paket und der Anwendungsserver automatisch in den Cloudspeicher hochgeladen.
* **Unterstützung der Version 2.1 des Azure-SDKs.** Für die Vorschauversion des Azure-Plug-Ins für Eclipse vom August 2013 wird Azure SDK 2.1 benötigt. Verwenden Sie die Vorschauversion vom August 2013 nicht mit älteren Versionen des Azure-SDKs, und verwenden Sie Azure SDK 2.1 nicht mit älteren Versionen des Azure-Plug-Ins für Eclipse.
* **Unterstützung der Kepler-Version von Eclipse.** In diesem Zusammenhang wird mindestens die Indigo-Version der Eclipse-IDE benötigt. Das Azure-Plug-In für Eclipse wird offiziell nicht mehr unter Helios getestet.

### <a name="july-3-2013"></a>3. Juli 2013
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom Juli 2013 wird veröffentlicht. Das Update enthält neue Features, Fehlerbehebungen und einige feedbackbasierte Verbesserungen der Benutzerfreundlichkeit (verglichen mit der Vorschauversion vom Mai 2013):

* **Möglichkeit zum Erstellen eines neuen Speicherkontos.** Dem Dialogfeld **Speicherkonto hinzufügen** wurde die Schaltfläche **Neu** hinzugefügt. Dadurch können Sie innerhalb des Eclipse-Plug-Ins ein Speicherkonto erstellen, ohne sich beim Azure-Verwaltungsportal anmelden zu müssen. (Für dieses Feature müssen Sie bereits über ein Azure-Abonnement verfügen.) Weitere Informationen zum Erstellen eines neuen Speicherkontos finden Sie unter [So erstellen Sie ein neues Speicherkonto].
* **Neue Speicherkontooption &quot;(Auto)&quot; zur automatischen Bereitstellung von JDK-Paket und Server sowie zum Caching.** Bei Verwendung der Option **Automatisch hochladen** für das JDK-Paket und den Anwendungsserver können Sie nun für die URL und das Speicherkonto die Option **(Auto)** angeben, wenn Sie das JDK-Paket und den Anwendungsserver hochladen oder den Azure-Cachedienst verwenden. Dadurch wird automatisch das im Dialogfeld **Veröffentlichen in Azure** ausgewählte Speicherkonto verwendet. Das Tutorial [Erstellen einer Hello World-Anwendung für Azure in Eclipse] wurde mit der Verwendung der neuen **Automatikoption** aktualisiert.
* **Möglichkeit zum Festlegen Ihrer Azure-Dienstendpunkte.** Geben Sie die Azure-Dienstendpunkte an, die bestimmen, ob Ihre Anwendung auf der globalen Azure-Plattform, auf Azure 21Vianet in China oder auf einer privaten Azure-Plattform bereitgestellt und verwaltet wird. Weitere Informationen finden Sie unter [Azure-Dienstendpunkte].
* **Angabe einer lokalen Speicherressource bei umfangreichen Bereitstellungen.** Sollte die Bereitstellung für den Standardordner „approot“ zu groß sein, können Sie nun eine lokale Speicherressource als Bereitstellungsziel für Ihr JDK-Paket und Ihren Anwendungsserver angeben. Weitere Informationen finden Sie unter [Bereitstellen umfangreicher Bereitstellungen].
* **Unterstützung virtueller Azure-Maschinen der Größe A6 und A7.** Clouddienste können nun auf virtuellen Maschinen mit umfangreichem Arbeitsspeicher (Größe A6 und A7) bereitgestellt werden. Weitere Informationen zu diesen Größen finden Sie unter [Größen virtueller Computer und Clouddienste für Azure].
* **Paketupdate für die Azure-Bibliotheken für die Java-Bibliothek.** Basiert auf Version 0.4.4 der [Microsoft Azure-Client-API].

### <a name="may-1-2013"></a>1. Mai 2013
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom Mai 2013 wird veröffentlicht. Hierbei handelt es sich um ein umfangreiches Update für Azure SDK 2.0. Dieses ist eine erforderliche Komponente und wird beim Installieren des Plug-Ins automatisch heruntergeladen. Die Version enthält neue Features, Fehlerbehebungen und einige feedbackbasierte Verbesserungen der Benutzerfreundlichkeit (verglichen mit der Vorschauversion vom Februar 2013):

* **Automatischer Upload von JDK-Paket und Anwendungsserver in Azure Storage sowie Bereitstellung von dort aus.** Eine neue Option, die das ausgewählte JDK-Paket und den ausgewählten Anwendungsserver bei Bedarf automatisch in ein angegebenes Azure-Speicherkonto hochlädt und die Komponenten von dort aus bereitstellt, anstatt sie in das Bereitstellungspaket einzubetten oder manuell durch den Benutzer hochladen zu lassen. Dieses auf vielfachen Wunsch implementierte Feature vereinfacht die Bereitstellung von JDK- und Serverkomponenten erheblich (insbesondere für Neulinge). Eine schrittweise Anleitung mit diesen Optionen finden Sie unter [Erstellen einer Hello World-Anwendung für Azure in Eclipse].
* **Zentralisierte Nachverfolgung von Speicherkonten sowie Möglichkeit zum einfacheren Verweisen auf Speicherkonten (über ein Dropdown-Steuerelement).** Betrifft mehrere speicherbasierte Features (etwa die Bereitstellung von JDK- und Serverkomponenten sowie das Caching). Weitere Informationen finden Sie unter [Azure-Speicherkontenliste].
* **Vereinfachte Einrichtung des Remotezugriffs im Cloudveröffenlichungs-Assistenten.** Geben Sie zur Aktivierung des Remotezugriffs einfach einen Benutzernamen und ein Kennwort an, oder lassen Sie die Felder leer, um den Remotezugriff nicht zu aktivieren.
* **Paketupdate für die Azure-Bibliotheken für die Java-Bibliothek.** Basiert auf Version 0.4.2 der [Microsoft Azure-Client-API].
* **Unterstützung persistenter Sitzungen unter Windows Server 2012.** Bislang konnten persistente Sitzungen nur unter Windows Server 2008 R2 verwendet werden. Ab sofort wird die Sitzungsaffinität von beiden Cloud-Zielbetriebssystemen unterstützt.
* **Leistungsverbesserungen beim Paketupload.** Der Uploadteil des Bereitstellungsprozesses ist im Vergleich zu älteren Versionen selbst bei Verwendung eines Bereitstellungspakets mit eingebettetem JDK-Paket und Anwendungsserver etwa doppelt so schnell.

### <a name="february-8-2013"></a>8. Februar 2013
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom Februar 2013 wird veröffentlicht. Dieses kleinere Update enthält Fehlerbehebungen, feedbackbasierte Verbesserungen der Benutzerfreundlichkeit und einige neue Features (verglichen mit der Vorschauversion vom November 2012):

* Unterstützung der Bereitstellung von JDK-Paketen, Anwendungsservern und anderen Komponenten aus öffentlichen oder privaten Azure Blob Storage-Downloads anstelle der Einbettung in das Bereitstellungspaket bei der Bereitstellung in der Cloud.
* Möglichkeit zum Ändern der Verarbeitungsreihenfolge der benutzerdefinierten Komponenten einer Rolle mithilfe der hinzugefügten Schaltflächen **Nach oben** und **Nach unten** im **Komponentenabschnitt** der **Azure-Rolleneigenschaften**.
* **Paketupdate für die Azure-Bibliotheken für die Java-Bibliothek** auf der Grundlage von Version 0.4.0 der [Microsoft Azure-Client-API].

### <a name="november-5-2012"></a>5. November 2012
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom November 2012 wird veröffentlicht. Dieses umfangreiche Update enthält eine Reihe neuer Features sowie zusätzliche Fehlerbehebungen und feedbackbasierte Verbesserungen der Benutzerfreundlichkeit (verglichen mit der Vorschauversion vom September 2012):

* Unterstützung von Microsoft Windows Server 2012 als Cloudbetriebssystem.
* Unterstützung von zusammengestelltem Azure-Caching für Memcache-Clients.
* Einbeziehung der Apache Qpid JMS-Clientbibliotheken zur Nutzung von Azure AMQP-basiertem Messaging.
* Verbesserter Assistent für **neue Projekt** mit einer neuen Seite, auf der die Benutzer in ihren Projekten schnell mehrere zentrale Features (persistente Sitzungen, Caching und Remotedebuggen) aktivieren können.
* Bei Ausführung im Serveremulator: Automatische Verringerung der Rolleninstanzen auf 1 zur Vermeidung von Portbindungskonflikten zwischen Serverinstanzen.

### <a name="september-28-2012"></a>28. September 2012
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom September 2012 wird veröffentlicht. Dieses Dienstupdate enthält eine Reihe von zusätzlichen Fehlerbehebungen seit der Vorschauversion vom August 2012 sowie einige feedbackbasierte Verbesserungen der Benutzerfreundlichkeit für vorhandene Features:

* Unterstützung von Microsoft Windows 8 und Microsoft Windows Server 2012 als Entwicklungsbetriebssystem und Behebung von Problemen, die zuvor eine ordnungsgemäße Verwendung des Plug-Ins unter diesen Betriebssystemen verhindert haben.
* Verbesserte Unterstützung der Angabe von Endpunktportbereichen.
* Fehlerbehebungen für Dateipfade mit Leerzeichen.
* Verbesserungen beim Rollenkontextmenü zur Beschleunigung des Zugriffs auf rollenspezifische Konfigurationseinstellungen.
* Geringfügige Optimierungen für den **Cloudveröffenlichungs-Assistenten** und eine Reihe zusätzlicher Fehlerbehebungen.

### <a name="august-28-2012"></a>28. August 2012
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom August 2012 wird veröffentlicht. Dieses Dienstupdate enthält zusätzliche Fehlerbehebungen seit der Vorschauversion vom Juli 2012 sowie mehrere feedbackbasierte Verbesserungen der Benutzerfreundlichkeit für vorhandene Features:

* Dialogfeld „Azure Access Control Service-Filter“:
  * **Option zum Einbetten des Signaturzertifikats** in die WAR-Datei Ihrer Anwendung zur Vereinfachung der Cloudbereitstellung.
  * **Option zum Erstellen eines selbstsignierten Zertifikats** auf der Benutzeroberfläche für den ACS-Filter. Weitere Informationen zum Azure Access Control Service-Filter finden Sie unter [Authentifizieren von Webbenutzern mit dem Azure Access Control Service über Eclipse].
* Azure-Bereitstellungsprojekt-Assistent (gilt auch für die Eigenschaftenseite „Serverkonfiguration“ der Rolle):
  * **Automatische Erkennung des JDK-Speicherorts** auf Ihrem Computer (kann bei Bedarf überschrieben werden).
  * **Automatische Erkennung des Servertyps** beim Auswählen des Installationsverzeichnisses für den Anwendungsserver.

### <a name="july-15-2012"></a>15. Juli 2012
Die Vorschauversion des Azure-Plug-Ins für Eclipse vom Juli 2012 wird veröffentlicht. Diese Version behebt eine Reihe von Fehlern mit höchster Priorität, die seit der Version vom Juni 2012 gefunden oder von Benutzern gemeldet wurden. Dies ist lediglich ein Dienstupdate und enthält keine neuen Features.

### <a name="june-7-2012"></a>7. Juni 2012
Die CTP-Version des Azure-Plug-Ins für Eclipse vom Juni 2012 wird veröffentlicht. Neue Features:

* **Neuer Azure-Bereitstellungsprojekt-Assistent:** Ermöglicht die Auswahl von JDK, Java-Anwendungsserver und Java-Anwendungen direkt auf der verbesserten Benutzeroberfläche des Assistenten. Die Auswahlliste mit den standardmäßig verfügbaren Serverkonfigurationen umfasst Tomcat 6, Tomcat 7, GlassFish OSE 3, Jetty 7, Jetty 8, JBoss 6 und JBoss 7 (eigenständige Version). Darüber hinaus können Sie die Liste mit den Serverkonfigurationen anpassen. Diese Verbesserung der Benutzeroberfläche bietet eine Alternative zum Ziehen und Ablegen komprimierter Dateien und dem Kopieren von Startskripts (der zuvor verwendeten Vorgehensweise). Diese Methode kann zwar auch weiterhin verwendet werden, kommt aber vermutlich nur noch in erweiterten Szenarien zum Einsatz.
* **Rolleneigenschaftenseite für die Serverkonfiguration:** Hier können Sie nach der Projekterstellung problemlos die Ihrer Bereitstellung zugeordneten JDKs, Java-Anwendungsserver und Anwendungen ändern. Weitere Informationen finden Sie unter [Eigenschaften für die Serverkonfiguration].
* **&quot;Cloudveröffentlichungs-Assistent&quot;:** Ermöglicht die einfache Bereitstellung Ihres Projekts in Azure direkt über Eclipse und automatisiert das aufwendige manuelle Abrufen von Anmeldeinformationen, das Anmelden beim Azure-Verwaltungsportal, das Hochladen eines Pakets usw. Ein Beispiel für eine direkte Projektbereitstellung in Azure finden Sie unter [Erstellen einer Hello World-Anwendung für Azure in Eclipse].
* **Azure-Symbolleiste:** In Eclipse steht jetzt eine Azure-Symbolleiste mit Schaltflächen für folgende Features zur Verfügung:
  * ![][ic710879] **Ausführen in Azure-Emulator**: Führt Ihr Projekt im Emulator aus.
  * ![][ic710880] **Azure-Emulator zurücksetzen**: Setzt den Emulator zurück.
  * ![][ic710881] **Cloudpaket für Azure erstellen**: Kompiliert Ihr Paket für die Bereitstellung.
  * ![][ic710876] **Neues Azure-Bereitstellungsprojekt**: Erstellt ein neues Azure-Bereitstellungsprojekt.
  * ![][ic710882] **In Azure-Cloud veröffentlichen**: Veröffentlicht Ihr Projekt in Azure.
  * ![][ic710883] **Veröffentlichung aufheben**: Löscht Ihre Bereitstellung.
  * Viele dieser Azure-Symbolleistenschaltflächen werden in [Erstellen einer Hello World-Anwendung für Azure in Eclipse]verwendet.
* **Azure-Bibliotheken für Java:** Jetzt verfügbar als Teil des Einzelpakets für Azure-Bibliotheken für die Java-Bibliothek in Eclipse. Ist bei der Plug-In-Installation dabei und enthält alle erforderlichen Abhängigkeiten. Nachdem Sie Ihrem Java-Projekt einen Verweis auf die Bibliothek hinzugefügt haben, müssen Sie nichts mehr separat herunterladen. Weitere Informationen finden Sie unter [Installation des Azure Toolkit für Eclipse].
* **Microsoft JDBC Driver 4.0 für SQL Server bei der Plug-In-Installation verfügbar:** Im Rahmen der Installation des neuen Plug-Ins kann auch die neueste Version des Microsoft JDBC-Treibers für SQL Server installiert werden.
* **Azure Access Control Service-Filter bei der Plug-In-Installation verfügbar:** Diese neue Komponente ist als Eclipse-Bibliothek im Toolkit enthalten und ermöglicht Ihrer Java-Webanwendung die nahtlose Verwendung der Azure Access Control Service (ACS)-Authentifizierung mit verschiedenen Identitätsanbietern wie Google, Live.com und Yahoo!. Sie müssen keine eigene Authentifizierungslogik schreiben. Konfigurieren Sie einfach ein paar Optionen, und überlassen Sie den Rest (die ACS-basierte Benutzeranmeldung) dem Filter. Sie können sich ganz auf das Schreiben von Code konzentrieren, der den Benutzern auf der Grundlage ihrer Identität (gemäß Rückgabe des Filters an Ihre Anwendung im Anforderungsobjekt) den Zugriff auf Ressourcen ermöglicht. Ein Tutorial zur Verwendung des ACS-Filters finden Sie unter [Authentifizieren von Webbenutzern mit dem Azure Access Control Service über Eclipse].
* **Automatische Erkennung von Azure SDK 1.7 (erforderliche Komponente):** Bei der Erstellung eines neuen Azure-Bereitstellungsprojekts wird Azure SDK 1.7 automatisch heruntergeladen, sofern es nicht bereits installiert ist.
* **Instanzendpunkte:** Ermöglichen direkten Port-Endpunktzugriff für die Kommunikation mit Rolleninstanzen mit Lastenausgleich. Instanzendpunkte können über die Endpunkte-Benutzeroberfläche [Eigenschaften für Endpunkte] hinzugefügt werden. Dies vereinfacht die Aktivierung von Remotedebuggen und JMX-Diagnosen für bestimmte, in der Cloud ausgeführte Compute-Instanzen in Szenarien mit Bereitstellungen mit mehreren Instanzen. 
* **Benutzeroberfläche für Komponenten:** Erleichtert fortgeschrittenen Benutzern die Einrichtung von Projektabhängigkeiten zwischen einzelnen Azure-Rollen im Projekt und anderen externen Ressourcen wie Java-Anwendungsprojekten sowie die Beschreibung ihrer Bereitstellungslogik. Weitere Informationen finden Sie unter [Eigenschaften für Komponenten].
* **Automatisches Upgrade älterer Projektversionen:** Beim Öffnen eines Arbeitsbereichs mit Azure-Projekten, die mit einer älteren Version des Plug-Ins erstellt wurden, werden die alten Projekte in Eclipse als geschlossen angezeigt, da ältere Projektversionen nicht mit der neuen Version kompatibel sind. Beim Versuch, eines dieser alten Projekte zu öffnen, wird ein Upgrade-Assistent gestartet. Wenn Sie dem Upgrade zustimmen, wird ein neues Projekt mit dem Namenszusatz **_Upgraded** erstellt und automatisch für die Verwendung mit der neuen Version aktualisiert. Das neue Projekt kann bei Bedarf umbenannt werden. Das ursprüngliche Projekt wird dabei nicht geändert (und bleibt geschlossen).

### <a name="december-10-2011"></a>10. Dezember 2011
Die CTP-Version des Azure-Plug-Ins für Eclipse vom Dezember 2011 wird veröffentlicht. Neue Features:

* **Unterstützung von Sitzungsaffinität (&quot;persistente Sitzungen&quot;):** Ermöglicht die Aktivierung zustandsbehafteter, gruppierter Java-Anwendungen mit nur einem Kontrollkästchen. Weitere Informationen finden Sie unter [Sitzungsaffinität].
* **Vorgefertigte Startskript-Beispiele:** Für die am häufigsten verwendeten Java-Server (Tomcat, Jetty, JBoss, GlassFish). Können einfach aus dem Beispielverzeichnis Ihres Projekts in Ihr Startskript kopiert werden.
* **Emulator-Startausgabe in Echtzeit:** Ermöglicht die Verfolgung sämtlicher Schritte Ihres Startskripts in einem dedizierten Konsolenfenster, das den Fortschritt und die Fehler in Ihrem Skript während der Ausführung durch Azure zeigt.
* **Automatische, einfache Überwachung von „java.exe“:** Erzwingt ein Rollenrecycling, wenn „java.exe“ nicht mehr ausgeführt wird. Dabei kommt ein einfaches, vorgefertigtes Skript zum Einsatz, das Ihrer Bereitstellung automatisch hinzugefügt wird.
* **Konfigurationsbenutzeroberfläche für das Remotedebuggen von Java-Apps:** Hiermit können Sie dem Eclipse-Remotedebugger komfortabel Zugriff auf Ihre im Emulator oder in der Azure-Cloud ausgeführte Java-App geben und Ihren Java-Code schrittweise in Echtzeit durchlaufen und debuggen. Weitere Informationen finden Sie unter [Debuggen von Azure-Anwendungen in Eclipse].
* **Konfigurationsbenutzeroberfläche für lokale Speicherressourcen:** Erspart die direkte Bearbeitung von XML-Code zum Konfigurieren lokaler Ressourcen. Dieses Feature ermöglicht auch den Zugriff auf den tatsächlichen Dateipfad Ihrer lokalen Ressource nach der Bereitstellung über eine Umgebungsvariable, auf die Sie direkt in Ihrem Startskript verweisen können. Weitere Informationen finden Sie unter [Eigenschaften für lokalen Speicher].
* **Konfigurationsbenutzeroberfläche für Umgebungsvariablen:** Erspart die manuelle Bearbeitung des XML-Konfigurationscodes zum Festlegen von Umgebungsvariablen. Weitere Informationen finden Sie unter [Eigenschaften für Umgebungsvariablen].
* **JDBC-Treiber für SQL Azure:** Wird zusammen mit dem Plug-In als nahtlos integrierte Eclipse-Bibliothek installiert und vereinfacht die Programmierung für SQL Azure. 
* **Schneller Kontextmenüzugriff auf die Benutzeroberfläche für die Rollenkonfiguration**: Klicken Sie einfach mit der rechten Maustaste auf den Rollenordner, und klicken Sie anschließend auf **Eigenschaften**.
* **Benutzerdefinierte Symbole für Azure-Projekt und Rollenordner:** Zur besseren Erkennbarkeit und einfacheren Navigation in Ihrem Arbeitsbereich und Projekt.

## <a name="next-steps"></a>Nächste Schritte

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Toolkit für IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Installation des Azure Toolkit für Eclipse]: azure-toolkit-for-eclipse-installation.md

[Anleitung zur Azure-Anmeldung für das Azure-Toolkit für Eclipse]: azure-toolkit-for-eclipse-sign-in-instructions.md
[Informationen zum Veröffentlichen einer Web-App als Docker-Container mit dem Azure-Toolkit für Eclipse]: ./azure-toolkit-for-eclipse-publish-as-docker-container.md
[Verwalten von Speicherkonten mit dem Azure-Explorer für Eclipse]: ./azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer.md
[Verwalten virtueller Computer mit dem Azure-Explorer für Eclipse]: ./azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: https://docs.microsoft.com/java/azure

[Azul Systems-Webseite zu Zulu OpenJDK]: http://go.microsoft.com/fwlink/?LinkId=402457
[Azure-Dienstendpunkte]: http://go.microsoft.com/fwlink/?LinkID=699526
[Azure-Speicherkontenliste]: http://go.microsoft.com/fwlink/?LinkID=699528
[Eigenschaften für Komponenten]: http://go.microsoft.com/fwlink/?LinkID=699525#components_properties
[Erstellen einer Hello World-Anwendung für Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debuggen von Azure-Anwendungen in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Bereitstellen umfangreicher Bereitstellungen]: http://go.microsoft.com/fwlink/?LinkID=699536
[Eigenschaften für Endpunkte]: http://go.microsoft.com/fwlink/?LinkID=699525#endpoints_properties
[Eigenschaften für Umgebungsvariablen]: http://go.microsoft.com/fwlink/?LinkID=699525#environment_variables_properties
[Verwenden des HDInsight-Tools-Plug-Ins für Eclipse zum Erstellen von Spark-Anwendungen für HDInsight Spark-Cluster unter Linux]: /azure/hdinsight/hdinsight-apache-spark-eclipse-tool-plugin
[Authentifizieren von Webbenutzern mit dem Azure Access Control Service über Eclipse]: http://go.microsoft.com/fwlink/?LinkID=264703
[Vorgehensweise: Verwenden der SSL-Abladung]: http://go.microsoft.com/fwlink/?LinkID=699545
[Eigenschaften für lokalen Speicher]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties
[Microsoft Azure-Client-API]: http://go.microsoft.com/fwlink/?LinkId=280397
[Eigenschaften für die Serverkonfiguration]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[Sitzungsaffinität]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL-Abladung]: http://go.microsoft.com/fwlink/?LinkID=699549
[So erstellen Sie ein neues Speicherkonto]: http://go.microsoft.com/fwlink/?LinkID=699528#create_new
[Größen virtueller Computer und Clouddienste für Azure]: http://go.microsoft.com/fwlink/?LinkId=466520

<!-- IMG List -->

[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710877]: media/azure-toolkit-for-eclipse-whats-new/ic710877.png
[ic710879]: media/azure-toolkit-for-eclipse-whats-new/ic710879.png
[ic710880]: media/azure-toolkit-for-eclipse-whats-new/ic710880.png
[ic710881]: media/azure-toolkit-for-eclipse-whats-new/ic710881.png
[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710882]: media/azure-toolkit-for-eclipse-whats-new/ic710882.png
[ic710883]: media/azure-toolkit-for-eclipse-whats-new/ic710883.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh694270.aspx -->
