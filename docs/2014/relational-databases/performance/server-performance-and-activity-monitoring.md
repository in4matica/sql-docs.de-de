---
title: Überwachen der Serverleistung und -aktivität | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- activity monitoring [SQL Server]
- traces [SQL Server], how-to topics
- monitoring server performance [SQL Server], activity monitoring
- stored procedures [SQL Server], traces
- performance [SQL Server], servers
- servers [SQL Server], performance
- SQL Server Profiler, how-to topics
- SQL Server Management Studio [SQL Server], monitoring system
- Profiler [SQL Server Profiler], how-to topics
ms.assetid: f9abe48d-d6e9-4c38-a355-fc5eb5a95a25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7289c18fac421bbdb5ccc0e00a3bea60b7a22d9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150614"
---
# <a name="server-performance-and-activity-monitoring"></a>Überwachen der Serverleistung und -aktivität
  Ziel der Überwachung von Datenbanken ist es, die Leistung eines Servers zu bewerten. Eine effektive Überwachung umfasst die regelmäßige Erstellung von Momentaufnahmen der aktuellen Leistung, um problematische Prozesse zu isolieren, und die kontinuierliche Sammlung von Daten, um Leistungstrends über längere Zeit zu verfolgen. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Betriebssystem stellen Hilfsprogramme bereit, mit denen Sie den aktuellen Zustand der Datenbank anzeigen und die Leistung bei Änderung der Bedingungen nachverfolgen können.  
  
 Der folgende Abschnitt enthält Themen zum Verwenden der Leistungs- und Aktivitätsüberwachungstools von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Windows. Die Lektion enthält die folgenden Themen:  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 **So führen Sie Überwachungsaufgaben mit Windows-Tools aus**  
  
-   [Starten Sie den System Monitor &#40;Windows&#41;](start-system-monitor-windows.md)  
  
-   [Anzeigen des Anwendungsprotokolls von Windows &#40;Windows&#41;](view-the-windows-application-log-windows-10.md)  
  
 **So erstellen Sie SQL Server Daten Bank Warnungen mithilfe von Windows-Tools**  
  
-   [Einrichten einer SQL Server-Daten Bank Warnung &#40;Windows-&#41;](set-up-a-sql-server-database-alert-windows.md)  
  
 **So führen Sie Überwachungsaufgaben mit SQL Server Management Studio aus**  
  
-   [Zeigen Sie die SQL Server Fehlerprotokoll &#40;SQL Server Management Studio an&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
-   [Öffnen des Aktivitätsmonitors &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)  
  
 **So führen Sie Überwachungsaufgaben mit der SQL-Ablauf Verfolgung mit gespeicherten Transact-SQL-Prozeduren aus**  
  
-   [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)  
  
-   [Festlegen eines Ablauf Verfolgungs Filters &#40;Transact-SQL-&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
-   [Ändern einer vorhandenen Ablauf Verfolgung &#40;Transact-SQL-&#41;](../sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [Anzeigen einer gespeicherten Ablauf Verfolgung &#40;Transact-SQL-&#41;](../sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [Anzeigen von Filter Informationen &#40;Transact-SQL-&#41;](../sql-trace/view-filter-information-transact-sql.md)  
  
-   [Löschen einer Ablauf Verfolgung &#40;Transact-SQL-&#41;](../sql-trace/delete-a-trace-transact-sql.md)  
  
 **So erstellen und ändern Sie Ablauf Verfolgungen mithilfe von SQL Server Profiler**  
  
-   [Erstellen einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [Festlegen globaler Ablauf Verfolgungs Optionen &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [Angeben von Ereignissen und Datenspalten für eine Ablauf Verfolgungs Datei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [Erstellen eines Transact-SQL-Skripts zum Ausführen einer Ablauf Verfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [Speichert Ablauf Verfolgungs Ergebnisse in einer Datei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [Festlegen einer maximalen Dateigröße für eine Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [Speichern von Ablauf Verfolgungs Ergebnissen in einer Tabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [Festlegen der maximalen Tabellengröße für eine Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [Filtern von Ereignissen in einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [Filter Informationen &#40;SQL Server Profiler anzeigen&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [Ändern eines Filters &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [Ereignisse basierend auf der Ereignis Start Zeit &#40;SQL Server Profiler Filtern&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [Filtern von Ereignissen anhand der Ereignisendzeit &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [Filtert Server-Prozess-IDs &#40;SPIDs&#41; in einer Ablauf Verfolgungs &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [Organisieren der in einer Ablauf Verfolgung angezeigten Spalten &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
 **So starten, anhalten und stoppen Sie Ablauf Verfolgungen mithilfe von SQL Server Profiler**  
  
-   [Automatisches Starten einer Ablaufverfolgung nach dem Herstellen einer Verbindung mit einem Server &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [Anhalten einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [Beenden einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [Ausführen einer Ablaufverfolgung, nachdem sie angehalten oder beendet wurde &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
 **So öffnen Sie Ablauf Verfolgungen und konfigurieren die Anzeige von Ablauf Verfolgungen mithilfe von SQL Server Profiler**  
  
-   [Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [Öffnen einer Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [Löschen des Inhalts eines Ablaufverfolgungsfensters &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [Schließen Sie ein Ablauf Verfolgungs Fenster &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [Standardeinstellungen für Ablauf Verfolgungs Definitionen festlegen &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [Festlegen der Standardeinstellungen für die Ablaufverfolgungsanzeige &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **So geben Sie Ablauf Verfolgungen mithilfe von SQL Server Profiler wieder**  
  
-   [Wiedergeben einer Ablauf Verfolgungs Datei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [Wiedergeben einer Ablauf Verfolgungs Tabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [Wiedergeben eines einzelnen Ereignisses zu einem Zeitpunkt &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [Wiedergeben bis zu einem Breakpoint &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [Wiedergeben bis zu einer Cursorposition &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Wiedergeben eines Transact-SQL-Skripts &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
 **So erstellen, ändern und verwenden Sie Ablauf Verfolgungs Vorlagen mithilfe von SQL Server Profiler**  
  
-   [Erstellen einer Ablaufverfolgungsvorlage &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [Modify a Trace Template &#40;SQL Server Profiler&#41; (Ändern einer Ablaufverfolgungsvorlage &#40;SQL Server Profiler&#41)](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
-   [Ableiten einer Vorlage von einer zurzeit ausgeführten Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [Ableiten einer Vorlage von einer Ablaufverfolgungsdatei oder Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [Exportieren einer Ablaufverfolgungsvorlage &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [Importieren einer Ablauf Verfolgungs Vorlage &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
 **So verwenden Sie SQL Server Profiler Ablauf Verfolgungen zum Erfassen und Überwachen der Server Leistung**  
  
-   [Suchen eines Werts oder einer Datenspalte während der Ablauf Verfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [Deadlockdiagramme &#40;SQL Server Profiler speichern&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
-   [Separates Speichern von Showplan XML-Ereignissen &#40;SQL Server Profiler&#41;](save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [Speichern Sie Showplan XML Statistics Profile-Ereignisse separat &#40;SQL Server Profiler&#41;](save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [Extrahieren eines Skripts aus einer Ablauf Verfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [Korrelieren einer Ablauf Verfolgung mit Windows-Leistungs Protokolldaten &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
