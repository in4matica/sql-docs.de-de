---
title: SQL Server, Puffer-Manager-Objekt | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Buffer Manager object
- SQLServer:Buffer Manager
ms.assetid: 9775ebde-111d-476c-9188-b77805f90e98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ed9c8ff90798205f9db02ae4b4b47eb4310d4b06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250760"
---
# <a name="sql-server-buffer-manager-object"></a>SQL Server, Puffer-Manager-Objekt
  Das **Puffer-Manager** -Objekt stellt Leistungsindikatoren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Überwachen der Verwendung von bereit  
  
-   Arbeitsspeicher zum Speichern von Datenseiten.  
  
-   Leistungsindikatoren zur Überwachung der physischen E/A, während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbankseiten liest und schreibt.  
  
-   Pufferpoolerweiterung zur Erweiterung des Puffercaches mithilfe von schnellem, nicht flüchtigem Speicher wie Festkörperlaufwerken (SSD).  
  
 Durch Überwachen des Arbeitsspeichers und der Leistungsindikatoren, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden, können Sie Folgendes ermitteln:  
  
-   Ob es zu Engpässen wegen nicht ausreichendem physischem Arbeitsspeicher kommt. Wenn häufig verwendete Daten nicht im Cache gespeichert werden können, muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Daten vom Datenträger abrufen.  
  
-   Ob die Abfrageleistung durch Hinzufügen von Arbeitsspeicher oder durch Zuordnen von zusätzlichem Arbeitsspeicher für den Datencache bzw. für interne Strukturen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbessert werden kann.  
  
-   Wie oft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten vom Datenträger lesen muss. Verglichen mit anderen Vorgängen, wie z. B. dem Arbeitsspeicherzugriff, beansprucht die physische E/A viel Zeit. Durch Minimieren der physischen E/A kann die Abfrageleistung verbessert werden.  
  
## <a name="buffer-manager-performance-objects"></a>Leistungsobjekte für den Puffer-Manager  
 In dieser Tabelle werden die Leistungsobjekte für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Puffer-Manager** beschrieben.  
  
|Puffer-Manager-Leistungsindikatoren von SQL Server|BESCHREIBUNG|  
|----------------------------------------|-----------------|  
|**Puffer Cache-Trefferquote**|Gibt den Prozentsatz der Seiten an, die im Puffercache gefunden wurden, ohne dass ein Lesevorgang vom Datenträger erforderlich war. Die Quote ist die Gesamtzahl von Cachetreffern dividiert durch die Gesamtzahl der Cachesuchvorgänge für die letzten paar Tausend Seitenzugriffe. Nach längerer Zeit verschiebt sich die Quote geringfügig. Da das Lesen vom Cache weniger aufwendig als das Lesen vom Datenträger ist, ist es in Ihrem Interesse, dass diese Quote hoch ist. Im Allgemeinen können Sie die Trefferquote des Puffercaches erhöhen, indem Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mehr Arbeitsspeicher zur Verfügung stellen oder die Pufferpoolerweiterungsfunktion verwenden.|  
|**Prüf Punkt Seiten/Sek.**|Gibt die Anzahl der Seiten an, die pro Sekunde durch einen Prüfpunkt oder eine andere Operation, die das Leeren aller modifizierten Seiten erfordert, auf den Datenträger geleert wurden.|  
|**Datenbankseiten**|Gibt die Anzahl der Seiten im Pufferpool mit Datenbankinhalt an.|  
|**Zugewiesene Seiten der Erweiterung**|Gesamtzahl nicht freier Cacheseiten in der Pufferpoolerweiterungsdatei.|  
|**Freie Seiten der Erweiterung**|Gesamtzahl freier Cacheseiten in der Pufferpoolerweiterungsdatei.|  
|**Erweiterung wird als Prozentsatz verwendet**|Prozentsatz der Pufferpoolerweiterungs-Auslagerungsdatei, der durch Puffer-Manager-Seiten belegt ist.|  
|**Ausstehende e/a-Zahl**|E/A-Warteschlangenlänge für die Pufferpoolerweiterungsdatei.|  
|**Entfernungs Entfernungs Erweiterungen/Sek.**|Anzahl der Seiten, die aus der Pufferpoolerweiterungsdatei pro Sekunde entfernt wurden.|  
|**Seiten Lesevorgänge der Erweiterung/Sek.**|Anzahl der Seiten, die aus der Pufferpoolerweiterungsdatei pro Sekunde gelesen wurden.|  
|**Nicht referenzierte Zeit der Erweiterungs Seite**|Durchschnittliche Sekunden, die eine Seite in der Pufferpoolerweiterung ohne Verweise darauf verbleibt.|  
|**Erweiterungs Seiten-Schreibvorgänge/Sekunde**|Anzahl der Seiten, die in die Pufferpoolerweiterungsdatei pro Sekunde geschrieben wurden.|  
|**Freie Listen Stände/Sek.**|Gibt die Anzahl der Anforderungen pro Sekunde an, die auf eine freie Seite warten mussten.|  
|**Verzögerte Schreibvorgänge/Sek.**|Gibt die Anzahl der Puffer pro Sekunde an, die vom Puffer-Manager verzögert geschrieben wurden. Beim *LAZY WRITER* -Prozess (verzögertes Schreiben) handelt es sich um einen Systemprozess, der Batches mit alten, modifizierten Puffern (die auf den Datenträger zurückgeschrieben werden müssen, bevor der Puffer für eine andere Seite erneut verwendet werden kann) auf den Datenträger schreibt und Benutzerprozessen zur Verfügung stellt. Durch den LAZY WRITER-Prozess ist es nicht mehr nötig, häufig Prüfpunkte auszuführen, um verfügbare Puffer zu erhalten.|  
|**Seiten Lebenserwartung**|Gibt die Anzahl der Sekunden an, für die eine Seite ohne Verweise im Pufferpool verbleibt.|  
|**Seiten Suchvorgänge/Sek.**|Gibt die Anzahl der Anforderungen pro Sekunde zum Suchen einer Seite im Pufferpool an.|  
|**Seiten Lesevorgänge/Sek.**|Gibt die Anzahl der pro Sekunde ausgegebenen Lesevorgänge für physische Datenbankseiten an. Diese Statistik zeigt die Gesamtanzahl der physischen Seitenlesevorgänge aller Datenbanken an. Da die physische E/A aufwendig ist, sind Sie eventuell in der Lage, die Kosten durch einen größeren Datencache, intelligente Indizes oder effizientere Abfragen oder durch Ändern des Datenbankentwurfs zu minimieren.|  
|**Seiten Schreibvorgänge/Sek.**|Gibt die Anzahl der pro Sekunde ausgegebenen Schreibvorgänge für physische Datenbankseiten an.|  
|**Read-Ahead-Seiten/Sekunde**|Gibt die Anzahl der Seiten pro Sekunde an, die vor dem Verwenden gelesen werden.|  
  
## <a name="see-also"></a>Weitere Informationen  
 [SQL Server: Puffer Knoten](sql-server-buffer-node.md)   
 [Server Konfigurationsoptionen für den Server Arbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server, Plancache-Objekt](sql-server-plan-cache-object.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](monitor-resource-usage-system-monitor.md)   
 [sys. dm_os_performance_counters &#40;Transact-SQL-&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)   
 [Pufferpoolerweiterung](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  
