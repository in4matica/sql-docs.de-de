---
title: sys. dm_os_process_memory (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fcbab4d5dc1bbc86fe9083e9c3407749040a0023
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68265703"
---
# <a name="sysdm_os_process_memory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Die meisten Speicherbelegungen, die für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozessraum attributiert sind, werden über Schnittstellen gesteuert, die eine Nachverfolgung und Berücksichtigung dieser Zuordnungen ermöglichen. Speicherbelegungen werden jedoch eventuell in dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Adressraum ausgeführt, der die internen Arbeitsspeicherverwaltungsroutinen umgeht. Die Werte werden durch Aufrufe des Basisbetriebssystems erhalten. Sie werden nicht durch interne Methoden von manipuliert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es sei denn, Sie passen sich für gesperrte oder große Seiten Zuordnungen an.  
  
 Alle zurückgegebenen Werte mit Angaben zu den Arbeitsspeichergrößen werden in Kilobytes (KB) angezeigt. Der Spalten **total_virtual_address_space_reserved_kb** ist ein Duplikat von **virtual_memory_in_bytes** aus **sys. dm_os_sys_info**.  
  
 In der folgenden Tabelle wird ein vollständiges Bild des Prozessadressraums angegeben.  
  
> [!NOTE]  
>  Um dies von oder [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]aus aufzurufen, verwenden Sie den Namen **sys. dm_pdw_nodes_os_process_memory**.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**BIGINT**|Gibt das Prozessworkingset in KB an, wie vom Betriebssystem gemeldet, sowie nachverfolgte Zuordnungen, die über APIs umfangreicher Seiten und AWE-APIs durchgeführt wurden. Lässt keine NULL-Werte zu.|  
|**large_page_allocations_kb**|**BIGINT**|Gibt den physischen Arbeitsspeicher an, der über APIs umfangreicher Seiten zugeordnet wird. Lässt keine NULL-Werte zu.|  
|**locked_page_allocations_kb**|**BIGINT**|Gibt im Arbeitsspeicher gesperrte Speicherseiten an. Lässt keine NULL-Werte zu.|  
|**total_virtual_address_space_kb**|**BIGINT**|Gibt die Gesamtgröße des Benutzermodusteils im virtuellen Adressraum an. Lässt keine NULL-Werte zu.|  
|**virtual_address_space_reserved_kb**|**BIGINT**|Gibt die Gesamtmenge des vom Prozess reservierten virtuellem Adressraums an. Lässt keine NULL-Werte zu.|  
|**virtual_address_space_committed_kb**|**BIGINT**|Gibt die Menge des reservierten virtuellen Adressraums an, für die ein Commit oder eine Zuordnung zu physischen Seiten besteht. Lässt keine NULL-Werte zu.|  
|**virtual_address_space_available_kb**|**BIGINT**|Gibt die Menge an virtuellen Adressräumen an, die gerade frei sind. Lässt keine NULL-Werte zu.<br /><br /> **Hinweis:** Freie Regionen, die kleiner als die Zuordnungs Granularität sind, können vorhanden sein. Diese Bereiche sind für Zuordnungen nicht verfügbar.|  
|**page_fault_count**|**BIGINT**|Gibt die Anzahl der Seitenfehler an, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess verursacht wurden. Lässt keine NULL-Werte zu.|  
|**memory_utilization_percentage**|**int**|Gibt den Prozentwert des Arbeitsspeichers an, für den ein Commit ausgeführt wurde und der sich im Workingset befindet. Lässt keine NULL-Werte zu.|  
|**available_commit_limit_kb**|**BIGINT**|Gibt den Arbeitsspeicher an, der für den Commit durch den Prozess verfügbar ist. Lässt keine NULL-Werte zu.|  
|**process_physical_memory_low**|**bit**|Gibt an, dass der Prozess auf Benachrichtigung zu nicht genügend physischem Arbeitsspeicher reagiert. Lässt keine NULL-Werte zu.|  
|**process_virtual_memory_low**|**bit**|Gibt an, dass eine Bedingung nicht genügenden virtuellen Arbeitsspeichers erkannt wurde. Lässt keine NULL-Werte zu.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, auf dem sich diese Distribution befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]ist die `VIEW SERVER STATE` -Berechtigung erforderlich.   
Bei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium-Tarifen ist die `VIEW DATABASE STATE` -Berechtigung in der Datenbank erforderlich. In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] den Tarifen "Standard" und "Basic" ist der **Server Administrator** oder ein **Azure Active Directory Administrator** Konto erforderlich.   
  
## <a name="see-also"></a>Weitere Informationen  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server dynamischen Verwaltungs Sichten im Zusammenhang mit dem Betriebs System &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


