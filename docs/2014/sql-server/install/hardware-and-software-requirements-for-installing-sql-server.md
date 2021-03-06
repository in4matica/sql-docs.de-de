---
title: Hardware-und Software Anforderungen für die Installation von SQL Server 2014 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/10/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce6cef69abe7c2461552229363c8334ca56555b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245657"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server-2014"></a>Hardware- und Softwareanforderungen für die Installation von SQL Server 2014

 > - Probieren Sie SQL Server 2016 aus, indem Sie die ** [Kostenlose Developer Edition](https://my.visualstudio.com/Downloads?q=SQL%20Server%20Developer)installieren!**  
  
## <a name="considerations"></a>Überlegungen 
  
-   Es wird empfohlen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , auf Computern mit dem NTFS-Dateiformat zu laufen. Das FAT32-Dateisystem wird zwar unterstützt, aber nicht empfohlen, da es weniger sicher ist als das NTFS-Dateisystem.  
  
-   Sie können nicht auf schreibgeschützten, zugeordneten oder komprimierten Laufwerken installieren.  
  
-   Damit die Visual Studio-Komponente ordnungsgemäß installiert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann, müssen Sie ein Update installieren. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Setup prüft, ob dieses Update vorhanden ist, und fordert Sie auf, dieses Update herunterzuladen und zu installieren, bevor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sie mit der Installation fortfahren können. Um die Unterbrechung während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] des Setups zu vermeiden, müssen Sie das Update **vor dem Ausführen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] des Setups** herunterladen und installieren, wie unten beschrieben (oder alle Updates für .NET 3,5 SP1 installieren, die auf Windows Update verfügbar sind):  
  
    -   Holen [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] Sie sich für SP2 das erforderliche Update [hier](https://go.microsoft.com/fwlink/?LinkId=198093).  
  
    -   Bei allen anderen unterstützten Betriebssystemen ist dieses Update enthalten.  
  
-   Das Starten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setups durch den Terminaldiensteclient wird nicht unterstützt. Die Installation schlägt fehl, wenn Sie Setup über den Terminal Dienste-Client starten.   
  
-   Beim[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup werden die folgenden vom Produkt benötigten Softwarekomponenten installiert:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Unterstützungs Dateien für Setup  
  
-   Die Mindestanforderungen an die Version für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Installation [!INCLUDE[win8](../../includes/win8-md.md)]von unter oder finden Sie unter [Installieren von SQL Server unter Windows Server 2012 oder Windows 8](https://support.microsoft.com/kb/2681562) (https://support.microsoft.com/kb/2681562).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Hardware- und Softwareanforderungen](hardware-and-software-requirements-for-installing-sql-server.md#hwswr)  
  
-   [Anforderungen an Prozessor, Arbeitsspeicher und Betriebs System](hardware-and-software-requirements-for-installing-sql-server.md#pmosr)  
  
-   [Sprachübergreifende Unterstützung](hardware-and-software-requirements-for-installing-sql-server.md#CrossLanguageSupport)  
  
-   [Erweiterte Systemunterstützung](hardware-and-software-requirements-for-installing-sql-server.md#ess)  
  
-   [Erforderlicher Festplattenspeicherplatz (32-Bit und 64-Bit)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)  
  
-   [Speichertypen für Datendateien](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)  
  
-   [Installieren von SQL Server auf einem Domänen Controller](hardware-and-software-requirements-for-installing-sql-server.md#DC_support)  
  
##  <a name="hwswr"></a>Hardware-und Software Anforderungen  
 Die folgenden Anforderungen gelten für alle Installationen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] :  
  
|Komponente|Anforderung|  
|---------------|-----------------|  
|.NET Framework|.NET 3.5 SP1 ist eine Voraussetzung für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , wenn Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)], die Replikation oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]auswählen, und es wird nicht mehr von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup installiert. <br />: Wenn Sie Setup ausführen und .NET 3,5 SP1 nicht installiert ist, müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sie .NET 3,5 SP1 herunterladen und installieren, bevor Sie mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Installation fortfahren können. (Installieren Sie .NET 3,5 SP1 aus [Microsoft .NET Framework 3,5 Service Pack 1](https://www.microsoft.com/download/details.aspx?id=22).) Die Fehlermeldung enthält einen Link zum Download Center, oder Sie können .NET 3,5 SP1 von Windows Update herunterladen. Um die Unterbrechung beim [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup zu vermeiden, können Sie .NET 3.5 SP1 herunterladen und installieren, bevor Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup ausführen.<br />-Wenn Sie das Setup auf einem Computer mit [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 oder [!INCLUDE[win8](../../includes/win8-md.md)]ausführen, müssen Sie .NET Framework 3,5 SP1 aktivieren, bevor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Sie installieren.<br />Wenn es keinen Internetzugang gibt, müssen Sie .NET Framework 3,5 SP1 herunterladen und installieren, bevor Sie Setup ausführen, um eine der oben genannten Komponenten zu installieren. Weitere Informationen zu den Empfehlungen und Anleitungen zum Abrufen und Aktivieren von .NET Framework 3,5 [!INCLUDE[win8](../../includes/win8-md.md)] unter und [!INCLUDE[win8srv](../../includes/win8srv-md.md)]finden Sie unter [Überlegungen zur Bereitstellung von Microsoft .NET Framework 3,5](https://msdn.microsoft.com/library/windows/hardware/hh975396) (.https://msdn.microsoft.com/library/windows/hardware/hh975396)<br /><br /> .NET 4.0 ist eine Voraussetzung für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert .NET 4.0 während des Funktionsinstallationsschritts.<br />-Wenn Sie die [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] -Editionen installieren, stellen Sie sicher, dass eine Internet Verbindung auf dem Computer verfügbar ist. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup lädt .NET Framework 4 herunter und installiert die Komponente, da sie nicht in den [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]-Medien enthalten ist.<br />-[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]installiert .NET 4,0 nicht im Server Core-Modus von [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 oder. [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Sie müssen dann .NET 4.0 installieren, bevor Sie [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] in einer Server Core-Installation von [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 oder [!INCLUDE[win8srv](../../includes/win8srv-md.md)]installieren.|  
|Windows PowerShell|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Windows PowerShell 2,0 wird von nicht installiert oder aktiviert. Windows PowerShell 2,0 ist jedoch eine Installations Voraussetzung für [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Komponenten [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]und. Wenn beim Setup gemeldet wird, dass Windows PowerShell 2.0 nicht vorhanden ist, können Sie die Komponente installieren oder aktivieren, indem Sie die Anweisungen auf der Seite [Windows Management Framework](https://go.microsoft.com/fwlink/?LinkId=186214) ausführen.|  
|Netzwerksoftware|Die unterstützten Betriebssysteme für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verfügen über integrierte Netzwerksoftware. Benannte und Standardinstanzen einer eigenständigen Installation unterstützen die folgenden Netzwerkprotokolle: Shared Memory, Named Pipes, TCP/IP und VIA.<br /><br /> Hinweis: Das VIA-Protokoll wird auf Failoverclustern nicht unterstützt. Clients oder Anwendungen, die auf demselben Knoten des Failoverclusters wie die SQL Server-Instanz ausgeführt werden, können das Shared Memory-Protokoll verwenden, um eine Verbindung zum SQL Server über dessen lokale Pipeadresse herzustellen. Diese Art der Verbindung ist jedoch nicht clusterfähig und schlägt nach einem Failover der Instanz fehl. Deswegen wird sie nicht empfohlen und sollte nur in sehr speziellen Szenarien verwendet werden. Das VIA-Protokoll ist veraltet. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> Weitere Informationen zu Netzwerkprotokollen und Netzwerkbibliotheken finden Sie unter [Network Protocols and Network Libraries](network-protocols-and-network-libraries.md).|  
|Virtualisierung|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] wird in virtuellen Computerumgebungen unterstützt, die unter der Hyper-V-Rolle in den folgenden Editionen ausgeführt werden:<br />-<br />                    
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard, Enterprise und Datacenter<br />-[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard, Enterprise und Datacenter Edition.<br />-<br />                    [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Datacenter und Standard Edition.<br /><br /> Zusätzlich zu den Ressourcen, die von der übergeordneten Partition benötigt werden, müssen jedem virtuellen Computer (untergeordnete Partition) ausreichend Prozessorressourcen, Speicherplatz und Datenträgerressourcen für die jeweilige [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz bereitgestellt werden. Die Anforderungen werden später in diesem Thema aufgeführt.\*<br /><br /> Innerhalb der Hyper-V-Rolle für [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 oder [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 können virtuellen Computern, auf denen eine 32-Bit-/64-Bit-Edition von [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 bzw. eine 64-Bit-Edition von [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 oder eine 64-Bit-Edition von [!INCLUDE[win8srv](../../includes/win8srv-md.md)] ausgeführt wird, maximal vier virtuelle Prozessoren zugeordnet werden.<br /><br /> Innerhalb der Hyper-V-Rolle für [!INCLUDE[win8srv](../../includes/win8srv-md.md)]:<br />Virtuellen Computern, auf denen eine 32-Bit- oder 64-Bit-Edition von [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 ausgeführt wird, können maximal acht virtuelle Prozessoren zugeordnet werden.<br />können virtuellen Computern mit einer 64-Bit-Edition von [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 oder [!INCLUDE[win8srv](../../includes/win8srv-md.md)] maximal 64 virtuelle Prozessoren zugeordnet werden.<br /><br /> Weitere Informationen zu Rechen Kapazitätsgrenzen für verschiedene Editionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und deren Unterschiede in physischen und virtualisierten Umgebungen mit hyperthreadprozessoren finden Sie unter [Compute Capacity Limits by Edition of SQL Server](../compute-capacity-limits-by-edition-of-sql-server.md). Weitere Informationen über die Rolle für Hyper-V finden Sie auf der [Windows Server 2008-Website](https://go.microsoft.com/fwlink/?LinkId=182820).<br /><br /> ** \* Wichtig \* \* ** Gastfailoverclustering wird in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]unterstützt. Weitere Informationen zu den unterstützten Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Betriebssystemen für Gast-Failoverclustering und zur Unterstützung für Virtualisierung finden Sie in der [Unterstützungsrichtlinie für Microsoft SQL Server-Produkte in einer virtuellen Hardwareumgebung](https://go.microsoft.com/fwlink/?LinkId=151676).|  
|Festplatte|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] erfordert mindestens 6 GB verfügbaren Festplattenspeicher.<br /><br /> Der erforderliche freie Festplattenspeicher ist von den installierten [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Komponenten abhängig. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Hard Disk Space Requirements (32-Bit and 64 Bit)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) . Informationen zu unterstützten Speichertypen für Datendateien finden Sie unter [Speichertypen für Datendateien](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).|  
|Laufwerk|Ein DVD-Laufwerk ist erforderlich, falls die Installation von einem DVD-Medium erfolgt.|  
|Überwachen|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] erfordert eine Super VGA-Grafikkarte mit einer Mindestauflösung von 800x600 Pixel.|  
|Internet|Zur Nutzung des Internets ist ein Internetzugang erforderlich (möglicherweise gebührenpflichtig).|  
  
 * Das [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ausführen auf einem virtuellen Computer ist aufgrund des Aufwands der Virtualisierung langsamer als das systemeigene ausführen.  
  
##  <a name="pmosr"></a>Anforderungen an Prozessor, Arbeitsspeicher und Betriebs System  
 Der folgende Arbeitsspeicher- und Prozessoranforderungen gelten für alle Editionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Komponente|Anforderung|  
|---------------|-----------------|  
|Arbeitsspeicher<sup>[1]</sup>|**Garantien**<br /><br /> Express-Editionen: 512 MB<br /><br /> Alle anderen Editionen: 1 GB<br /><br /> **Empfohlen**<br /><br /> Express-Editionen: 1 GB<br /><br /> Alle anderen Editionen: mindestens 4 GB. Mit zunehmender Datenbankgröße sollte außerdem der Speicher erhöht werden, um eine optimale Leistung sicherzustellen.|  
|Prozessorgeschwindigkeit:|**Garantien**<br /><br /> x86-Prozessor: 1,0 GHz<br /><br /> x64-Prozessor: 1,4 GHz<br /><br /> **Empfohlen:** 2,0 GHz oder schneller|  
|Prozessortyp|x64-Prozessor: AMD Opteron, AMD Athlon 64, Intel Xeon mit Intel EM64T-Unterstützung, Intel Pentium IV mit EM64T-Unterstützung<br /><br /> x86-Prozessor: Pentium III-kompatibler Prozessor oder schneller|  
  
 <sup>[1]</sup> Der für die Installation der [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] -Komponente in [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) erforderliche Mindestarbeitsspeicher beträgt 2 GB RAM, was sich von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] den minimalen Arbeitsspeicher Anforderungen unterscheidet. Informationen zum Installieren von DQS finden Sie unter [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 **WOW64-Unterstützung:**  
  
 WOW64 (Windows 32-bit on Windows 64-bit) ist eine Funktion von 64-Bit-Editionen von Windows, die es ermöglicht, 32-Bit-Anwendungen systemintern im 32-Bit-Modus auszuführen. Anwendungen sind im 32-Bit-Modus funktionsfähig, obwohl es sich beim zugrunde liegenden Betriebssystem um ein 64-Bit-Betriebssystem handelt.  
  
-   Unter einem unterstützten 64-Bit-Betriebssystem können Installationen der 32-Bit-Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem 32-Bit-Subsystem (WOW64) eines 64-Bit-Servers installiert werden. WOW64 wird nur für eigenständige Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt. WOW64 wird nicht für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstallationen unterstützt.  
  
-   Für Installationen der 64-Bit-Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf unterstützten 64-Bit-Betriebssystemen werden Verwaltungstools in WOW64 unterstützt. Um weitere Informationen zu unterstützten Betriebssystemen zu erhalten, wählen Sie eine Edition von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in den Abschnitten unten aus.  
  
 **Server Core-Unterstützung:**  

 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] wird jetzt auf einer Server Core-Installation von Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 und Windows Server 2019 unterstützt. 


  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Installationen werden im Server Core-Modus folgender Windows Server-Editionen unterstützt:

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2 Datacenter|
| Windows Server 2012 Standard | Windows Server 2012 Datacenter |
| Windows Server 2008 R2 SP1 Standard | Windows Server 2008 R2 SP1 Datacenter |
| Windows Server 2008 R2 SP1 Enterprise | Windows Server 2008 R2 SP1 Web|
   | &nbsp; | &nbsp; |
  
 Weitere Informationen zum Installieren [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] von auf Server Core finden Sie unter Installieren von [SQL Server 2014 auf Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
   >[!NOTE]
   > 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen, die auf der [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 64-Bit x64 Standard Edition unterstützt werden, werden auch auf [!INCLUDE[sbs_2](../../includes/sbs-2-md.md)] 64-Bit x64 unterstützt.  
  
 **Betriebs System Unterstützung:**  
  
 Die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Editionen werden wie folgt unterteilt:  
  
-   [Prinzipaleditionen von SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [Spezielle Editionen von SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md#TOP_SP)  
  
-   [Breiteneditionen von SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
###  <a name="TOP_Principal"></a>Betriebssystemanforderungen für die Prinzipal Editionen  
 In der folgenden Tabelle werden die Betriebssystemanforderungen für die Prinzipaleditionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]angezeigt:  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]AntiVir|32 Bit|64 Bit|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32-Bit<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32-Bit|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Business Intelligence|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32-Bit<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32-Bit|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|Windows 10 Home 64-Bit<br /><br /> Windows 10 Professional 64-Bit<br /><br /> Windows 10 Enterprise 64-Bit<br /><br /> Windows 10 Home 32-Bit<br /><br /> Windows 10 Professional 32-Bit<br /><br /> Windows 10 Enterprise 32-Bit<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 32-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32-Bit<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32-Bit|Windows 10 Home 64-Bit<br /><br /> Windows 10 Professional 64-Bit<br /><br /> Windows 10 Enterprise 64-Bit<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit| 
  
###  <a name="TOP_SP"></a>Betriebs System Anforderungen für spezialisierte Editionen  
 In der folgenden Tabelle werden die Betriebssystemanforderungen für die Spezialeditionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]angezeigt:  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]AntiVir|32 Bit|64 Bit|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|Windows 10 Home 64-Bit<br /><br /> Windows 10 Professional 64-Bit<br /><br /> Windows 10 Enterprise 64-Bit<br /><br /> Windows 10 Home 32-Bit<br /><br /> Windows 10 Professional 32-Bit<br /><br /> Windows 10 Enterprise 32-Bit<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32-Bit<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32-Bit|Windows 10 Home 64-Bit<br /><br /> Windows 10 Professional 64-Bit<br /><br /> Windows 10 Enterprise 64-Bit<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit| 
  
###  <a name="TOP_Breadth"></a>Breite Editionen Betriebs System Anforderungen
 In der folgenden Tabelle werden die Betriebssystemanforderungen für die Breiteneditionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]angezeigt:  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]AntiVir|32 Bit|64 Bit|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|Windows 10 Home 64-Bit<br /><br /> Windows 10 Professional 64-Bit<br /><br /> Windows 10 Enterprise 64-Bit<br /><br /> Windows 10 Home 32-Bit<br /><br /> Windows 10 Professional 32-Bit<br /><br /> Windows 10 Enterprise 32-Bit<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 32-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32-Bit<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32-Bit|Windows 10 Home 64-Bit<br /><br /> Windows 10 Professional 64-Bit<br /><br /> Windows 10 Enterprise 64-Bit<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|Windows 10 Home 64-Bit<br /><br /> Windows 10 Professional 64-Bit<br /><br /> Windows 10 Enterprise 64-Bit<br /><br /> Windows 10 Home 32-Bit<br /><br /> Windows 10 Professional 32-Bit<br /><br /> Windows 10 Enterprise 32-Bit<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 32-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 32-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32-Bit<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32-Bit|Windows 10 Home 64-Bit<br /><br /> Windows 10 Professional 64-Bit<br /><br /> Windows 10 Enterprise 64-Bit<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64-Bit<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter (64-Bit)<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64-Bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64-Bit<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64 Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64-Bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64-Bit<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64-Bit<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Professional 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64-Bit<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64-Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 Bit<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64-Bit|  
  
## <a name="minimum-sql-server-version-requirements-for-windows-10"></a>SQL Server-Mindestanforderungen der Versionen für Windows 10  
 Vor der Installation von SQL Server auf einem Computer unter Windows 10 müssen Sie überprüfen, ob die folgenden Mindestanforderungen erfüllt sind:  
  
-   Für SQL Server 2014 muss SQL Server 2014 Service Pack 1 oder ein neueres Update angewendet werden. Weitere Informationen finden Sie unter [So erhalten Sie das neueste Servicepack für SQL Server 2014](https://support.microsoft.com/kb/2958069).  
  
-   Für SQL Server 2012 muss SQL Server 2012 Service Pack 2 oder ein neueres Update angewendet werden. Weitere Informationen finden Sie unter [So erhalten Sie das neueste Servicepack für SQL Server 2012](https://support.microsoft.com/kb/2755533).  
  
-   SQL Server 2008 R2  
    SQL Server 2008 R2 und SQL Server 10 werden unter Windows 10 nicht unterstützt.  
  
##  <a name="CrossLanguageSupport"></a>Sprachübergreifende Unterstützung  
 Weitere Informationen zu sprachübergreifender Unterstützung und Überlegungen zur Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lokalisierten Sprachen finden Sie unter [Lokale Sprachversionen in SQL Server](local-language-versions-in-sql-server.md).  
  
##  <a name="ess"></a>Erweiterte System Unterstützung  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-64-Bit-Versionen enthalten die Unterstützung für erweiterte Systeme, auch bekannt als WOW64 (Windows 32-bit on Windows 64-bit). WOW64 ist eine Funktion von 64-Bit-Editionen von Windows, die es ermöglicht, 32-Bit-Anwendungen systemintern im 32-Bit-Modus auszuführen. Anwendungen sind im 32-Bit-Modus funktionsfähig, obwohl es sich beim zugrunde liegenden Betriebssystem um ein 64-Bit-Betriebssystem handelt.  
  
##  <a name="HardDiskSpace"></a>Anforderungen an den Festplatten Speicherplatz (32 Bit und 64 Bit)  
 Während der Installation erstellt Windows Installer temporäre Dateien auf dem Systemlaufwerk. Bevor Sie Setup zum Installieren oder aktualisieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausführen, vergewissern Sie sich, dass mindestens **6,0 GB** verfügbarer Speicherplatz auf dem Systemlaufwerk für diese Dateien vorhanden sind. Diese Anforderung gilt auch, wenn Sie-Komponenten auf einem nicht standardmäßigen Laufwerk installieren.  
  
 Die tatsächlichen Anforderungen für den Festplattenspeicherplatz basieren auf der Systemkonfiguration und den Funktionen, die Sie installieren möchten. Eine Liste der Funktionen, die von den Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt werden, finden Sie unter [von den Editionen von SQL Server 2014 unterstützte Funktionen](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). In der folgenden Tabelle sind die Speicherplatzanforderungen für die Komponenten von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aufgeführt.  
  
|**Feature**|**Speicherplatzbedarf**|  
|-----------------|--------------------------------|  
|
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] und Datendateien, Replikation, Volltextsuche und Data Quality Services|811 MB|  
|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und Datendateien|345 MB|  
|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und Berichts-Manager|304 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|591 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|243 MB|  
|Clientkomponenten (außer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation und Integration Services-Tools)|1823 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Online Dokumentation zum Anzeigen und Verwalten von Hilfe Inhalten<sup>1</sup>|375 KB|  
  
 <sup>1</sup> Der Speicherplatzbedarf für heruntergeladene Online Dokumentation beträgt 200 MB.  
  
##  <a name="StorageTypes"></a>Speichertypen für Datendateien  
 Für Datendateien werden folgende Speichertypen unterstützt:  
  
-   Lokaler Datenträger  
  
-   Freigegebener Speicher  
  
-   SMB-Dateifreigabe  
  
    > **Hinweis:**  Der SMB-Speicher wird für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datendateien für eigenständige Installationen oder für gruppierte Installationen nicht unterstützt. Verwenden Sie stattdessen den direkt angeschlossenen Speicher oder ein SAN (Storage Area Network).  
  
    > **WICHTIG!** Der SMB-Speicher kann von einem Windows File Server oder einem SMB-Speichergerät eines Drittanbieters gehostet werden. Bei Verwendung von Windows File Server sollte die Windows File Server-Version 2008 oder höher verwendet werden. Weitere Informationen zum Installieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit SMB-Dateifreigabe als Speicheroption finden Sie unter [Installieren von SQL Server mit SMB-Dateifreigabe als Speicheroption](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)aufgeführt.  
  
    > **Warnung!!!!**  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstallation wird nur der lokale Datenträger zum Installieren der tempdb-Dateien unterstützt. Stellen Sie sicher, dass der für die tempdb-Daten-und Protokolldateien angegebene Pfad auf **allen** Cluster Knoten gültig ist. Sind die tempdb-Verzeichnisse auf dem Failoverzielknoten während des Failovers nicht verfügbar, wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressource nicht online geschaltet.  
  
##  <a name="DC_support"></a>Installieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von auf einem Domänen Controller: Einschränkungen  
 Aus Sicherheitsgründen sollte [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nicht auf einem Domänencontroller installiert werden. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup wird die Installation auf einem Computer, der als Domänencontroller fungiert, nicht blockieren, es gelten jedoch die folgenden Einschränkungen:  
  
-   Sie können keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste auf einem Domänencontroller unter einem lokalen Dienstkonto ausführen.  
  
-   Nachdem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installiert wurde, können Sie den Computer nicht von einem Domänenmitglied zu einem Domänencontroller ändern. Sie müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deinstallieren, bevor Sie den Hostcomputer zu einem Domänencontroller ändern.  
  
-   Nachdem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installiert wurde, können Sie den Computer nicht von einem Domänencontroller zu einem Domänenmitglied ändern. Sie müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deinstallieren, bevor Sie den Hostcomputer zu einem Domänenmitglied ändern.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden nicht unterstützt, wenn es sich bei den Clusterknoten um Domänencontroller handelt.  
  
-   Beim Setup von[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können keine Sicherheitsgruppen erstellt oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonten für einen schreibgeschützten Domänencontroller bereitgestellt werden. In diesem Szenario tritt ein Setupfehler auf.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Planen einer SQL Server Installation](planning-a-sql-server-installation.md)   
 [Überlegungen zur Sicherheit bei SQL Server-Installationen](security-considerations-for-a-sql-server-installation.md)   
 [Produktspezifikationen für SQL Server 2014](../../getting-started/sql-server-2014-product-specifications.md)  
