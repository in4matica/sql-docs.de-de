---
title: sys. query_store_runtime_stats (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0bd7f1870a88ae2050445050565e0f268f4d9b0e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "70148286"
---
# <a name="sysquery_store_runtime_stats-transact-sql"></a>sys. query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Enthält Informationen zu den Lauf Zeit Ausführungs Statistik-Informationen für die Abfrage.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**BIGINT**|Der Bezeichner der Zeile, die die Lauf Zeit Ausführungs Statistik für die **plan_id**darstellt, **execution_type** und **runtime_stats_interval_id**. Er ist nur für die letzten Lauf Zeit Statistik Intervalle eindeutig. Für das derzeit aktive Intervall kann es mehrere Zeilen geben, die Lauf Zeit Statistiken für den Plan darstellen, auf den von **plan_id**verwiesen wird, wobei der Ausführungstyp **execution_type**ist. In der Regel stellt eine Zeile Lauf Zeit Statistiken dar, die auf den Datenträger geleert werden, während andere (n) den Speicher internen Status darstellen. Wenn Sie den tatsächlichen Status für jedes Intervall erhalten möchten, müssen Sie daher Metriken aggregieren, indem Sie **plan_id** **execution_type** und **runtime_stats_interval_id**gruppieren.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**plan_id**|**BIGINT**|Fremdschlüssel. Joins mit [sys. query_store_plan &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**BIGINT**|Fremdschlüssel. Joins mit [sys. query_store_runtime_stats_interval &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Bestimmt den Typ der Abfrage Ausführung:<br /><br /> 0-reguläre Ausführung (erfolgreich abgeschlossen)<br /><br /> 3-vom Client initiierte Ausführung abgebrochen<br /><br /> 4-Ausnahme Abbruch abgebrochen|  
|**execution_type_desc**|**nvarchar(128)**|Textbeschreibung des Felds "Ausführungstyp":<br /><br /> 0-regulär<br /><br /> 3-abgebrochen<br /><br /> 4-Ausnahme|  
|**first_execution_time**|**datetimeoffset**|Die erste Ausführungszeit für den Abfrageplan innerhalb des Aggregations Intervalls. Dies bezieht sich auf die Endzeit der Abfrage Ausführung.|  
|**last_execution_time**|**datetimeoffset**|Die letzte Ausführungszeit für den Abfrageplan innerhalb des Aggregations Intervalls. Dies bezieht sich auf die Endzeit der Abfrage Ausführung.|  
|**count_executions**|**BIGINT**|Gesamtanzahl der Ausführungen für den Abfrageplan innerhalb des Aggregations Intervalls.|  
|**avg_duration**|**float**|Die durchschnittliche Dauer für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).|  
|**last_duration**|**BIGINT**|Die letzte Dauer für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).|  
|**min_duration**|**BIGINT**|Minimale Dauer für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).|  
|**max_duration**|**BIGINT**|Maximale Dauer für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).|  
|**stdev_duration**|**float**|Dauer der Standardabweichung für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden gemeldet).|  
|**avg_cpu_time**|**float**|Durchschnittliche CPU-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_cpu_time**|**BIGINT**|Die letzte CPU-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_cpu_time**|**BIGINT**|Minimale CPU-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_cpu_time**|**BIGINT**|Maximale CPU-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**stdev_cpu_time**|**float**|Die Standardabweichung der CPU-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden gemeldet).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**avg_logical_io_reads**|**float**|Die durchschnittliche Anzahl von logischen e/a-Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_logical_io_reads**|**BIGINT**|Die letzte Anzahl von logischen e/a-Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_logical_io_reads**|**BIGINT**|Die Mindestanzahl logischer e/a-Lesevorgänge für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_logical_io_reads**|**BIGINT**|Maximale Anzahl von logischen e/a-Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**stdev_logical_io_reads**|**float**|Die Anzahl von logischen e/a-Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**avg_logical_io_writes**|**float**|Die durchschnittliche Anzahl logischer e/a-Schreibvorgänge für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_logical_io_writes**|**BIGINT**|Die letzte Anzahl logischer e/a-Schreibvorgänge für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_logical_io_writes**|**BIGINT**|Die Mindestanzahl logischer e/a-Schreibvorgänge für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_logical_io_writes**|**BIGINT**|Maximale Anzahl logischer e/a-Schreibvorgänge für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**stdev_logical_io_writes**|**float**|Die Anzahl von logischen e/a-Vorgängen schreibt die Standardabweichung für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**avg_physical_io_reads**|**float**|Die durchschnittliche Anzahl physischer e/a-Lesevorgänge für den Abfrageplan innerhalb des Aggregations Intervalls (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_physical_io_reads**|**BIGINT**|Die letzte Anzahl physischer e/a-Lesevorgänge für den Abfrageplan innerhalb des Aggregations Intervalls (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_physical_io_reads**|**BIGINT**|Die Mindestanzahl physischer e/a-Lesevorgänge für den Abfrageplan innerhalb des Aggregations Intervalls (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_physical_io_reads**|**BIGINT**|Maximale Anzahl physischer e/a-Lesevorgänge für den Abfrageplan innerhalb des Aggregations Intervalls (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**stdev_physical_io_reads**|**float**|Die Anzahl physischer e/a-Vorgänge liest die Standardabweichung für den Abfrageplan innerhalb des Aggregations Intervalls (ausgedrückt als Anzahl von 8 KB gelesenen Seiten).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**avg_clr_time**|**float**|Durchschnittliche CLR-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_clr_time**|**BIGINT**|Die letzte CLR-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden gemeldet).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_clr_time**|**BIGINT**|Minimale CLR-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_clr_time**|**BIGINT**|Maximale CLR-Zeit für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden angegeben).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**stdev_clr_time**|**float**|CLR-Zeitstandard Abweichung für den Abfrageplan innerhalb des Aggregations Intervalls (in Mikrosekunden gemeldet).<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**avg_dop**|**float**|Durchschnittlicher DOP (Grad an Parallelität) für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_dop**|**BIGINT**|Letztes DOP (Grad an Parallelität) für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_dop**|**BIGINT**|Minimaler DOP (Grad an Parallelität) für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_dop**|**BIGINT**|Maximaler DOP (Grad an Parallelität) für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**stdev_dop**|**float**|DOP (Grad an Parallelität) Standardabweichung für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**avg_query_max_used_memory**|**float**|Durchschnittliche Arbeitsspeicher Zuweisung (als Anzahl von 8-KB-Seiten angegeben) für den Abfrageplan innerhalb des Aggregations Intervalls. Immer 0 für Abfragen, die nativ kompilierte Speicher optimierte Prozeduren verwenden.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_query_max_used_memory**|**BIGINT**|Die letzte Arbeitsspeicher Zuweisung (als Anzahl von 8-KB-Seiten angegeben) für den Abfrageplan innerhalb des Aggregations Intervalls. Immer 0 für Abfragen, die nativ kompilierte Speicher optimierte Prozeduren verwenden.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_query_max_used_memory**|**BIGINT**|Minimale Arbeitsspeicher Zuweisung (als Anzahl von 8-KB-Seiten angegeben) für den Abfrageplan innerhalb des Aggregations Intervalls. Immer 0 für Abfragen, die nativ kompilierte Speicher optimierte Prozeduren verwenden.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_query_max_used_memory**|**BIGINT**|Maximale Arbeitsspeicher Zuweisung (als Anzahl von 8-KB-Seiten angegeben) für den Abfrageplan innerhalb des Aggregations Intervalls. Immer 0 für Abfragen, die nativ kompilierte Speicher optimierte Prozeduren verwenden.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**stdev_query_max_used_memory**|**float**|Standardabweichung der Arbeitsspeicher Zuweisung (als Anzahl von 8-KB-Seiten angegeben) für den Abfrageplan innerhalb des Aggregations Intervalls. Immer 0 für Abfragen, die nativ kompilierte Speicher optimierte Prozeduren verwenden.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**avg_rowcount**|**float**|Die durchschnittliche Anzahl der zurückgegebenen Zeilen für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_rowcount**|**BIGINT**|Anzahl der zurückgegebenen Zeilen bei der letzten Ausführung des Abfrage Plans innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_rowcount**|**BIGINT**|Mindestanzahl von zurückgegebenen Zeilen für den Abfrageplan innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_rowcount**|**BIGINT**|Maximale Anzahl der zurückgegebenen Zeilen für den Abfrageplan innerhalb des Aggregations Intervalls.|  
|**stdev_rowcount**|**float**|Anzahl der zurückgegebenen Zeilen der Standardabweichung für den Abfrageplan innerhalb des Aggregations Intervalls.|
|**avg_log_bytes_used**|**float**|Die durchschnittliche Anzahl von Bytes im Daten Bank Protokoll, die vom Abfrageplan innerhalb des Aggregations Intervalls verwendet werden.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**last_log_bytes_used**|**BIGINT**|Anzahl von Bytes im Daten Bank Protokoll, das von der letzten Ausführung des Abfrage Plans innerhalb des Aggregations Intervalls verwendet wird.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**min_log_bytes_used**|**BIGINT**|Die Mindestanzahl von Bytes im Daten Bank Protokoll, die vom Abfrageplan innerhalb des Aggregations Intervalls verwendet werden.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**max_log_bytes_used**|**BIGINT**|Maximale Anzahl von Bytes im Daten Bank Protokoll, die vom Abfrageplan innerhalb des Aggregations Intervalls verwendet werden.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|
|**stdev_log_bytes_used**|**float**|Standard Abweichung der Anzahl von Bytes im Daten Bank Protokoll, das von einem Abfrageplan verwendet wird, innerhalb des Aggregations Intervalls.<br/>**Hinweis:** Azure SQL Data Warehouse gibt immer 0 (null) zurück.|  
|**avg_tempdb_space_used**|**float**|Durchschnittliche Anzahl von Seiten Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**last_tempdb_space_used**|**BIGINT**|Die letzte Anzahl von Seiten Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**min_tempdb_space_used**|**BIGINT**|Die Mindestanzahl von Seiten Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**max_tempdb_space_used**|**BIGINT**|Maximale Anzahl von Seiten Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**stdev_tempdb_space_used**|**float**|Anzahl der Seiten, die Standardabweichung für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**avg_page_server_io_reads**|**float**|Die durchschnittliche Anzahl von Seiten Server-e/a-Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** Hyperskalierung von Azure SQL-Datenbank</br>**Hinweis:** Azure SQL Data Warehouse gibt Azure SQL-Datenbank, Mi (nicht Hyperscale), immer NULL (0) zurück.|
|**last_page_server_io_reads**|**BIGINT**|Die letzte Anzahl von Seiten Server-e/a-Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** Hyperskalierung von Azure SQL-Datenbank</br>**Hinweis:** Azure SQL Data Warehouse gibt Azure SQL-Datenbank, Mi (nicht Hyperscale), immer NULL (0) zurück.|
|**min_page_server_io_reads**|**BIGINT**|Minimale Anzahl von Seiten Server-e/a-Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** Hyperskalierung von Azure SQL-Datenbank</br>**Hinweis:** Azure SQL Data Warehouse gibt Azure SQL-Datenbank, Mi (nicht Hyperscale), immer NULL (0) zurück.|
|**max_page_server_io_reads**|**BIGINT**|Maximale Anzahl von Seiten Server-e/a-Lesevorgängen für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** Hyperskalierung von Azure SQL-Datenbank</br>**Hinweis:** Azure SQL Data Warehouse gibt Azure SQL-Datenbank, Mi (nicht Hyperscale), immer NULL (0) zurück.|
|**stdev_page_server_io_reads**|**float**|Die Anzahl der Seiten Server-e/a-Vorgänge für den Abfrageplan innerhalb des Aggregations Intervalls. (ausgedrückt als Anzahl von 8-KB-Seiten gelesen).<br><br/>**Gilt für:** Hyperskalierung von Azure SQL-Datenbank</br>**Hinweis:** Azure SQL Data Warehouse gibt Azure SQL-Datenbank, Mi (nicht Hyperscale), immer NULL (0) zurück.|
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die `VIEW DATABASE STATE`-Berechtigung.  
  
## <a name="see-also"></a>Weitere Informationen  
 [sys. database_query_store_options &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys. query_context_settings &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys. query_store_plan &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys. query_store_query &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys. query_store_query_text &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys. query_store_wait_stats &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys. query_store_runtime_stats_interval &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Gespeicherte Prozeduren für den Abfragespeicher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)    
 [Bewährte Methoden für den Abfragespeicher](../../relational-databases/performance/best-practice-with-the-query-store.md)   
  
