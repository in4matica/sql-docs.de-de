---
title: sys. dm_db_task_space_usage (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_task_space_usage_TSQL
- sys.dm_db_task_space_usage_TSQL
- dm_db_task_space_usage
- sys.dm_db_task_space_usage
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_task_space_usage dynamic management view
ms.assetid: fb0c87e5-43b9-466a-a8df-11b3851dc6d0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ee20a77440fd769e813f8335148c2b67a34d7bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68263965"
---
# <a name="sysdm_db_task_space_usage-transact-sql"></a>sys.dm_db_task_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt für die Datenbank Aktivitäten zu Seitenzuordnungen und aufgehobenen Seitenzuordnungen nach Tasks zurück.  
  
> [!NOTE]  
>  Diese Sicht gilt nur für die [tempdb-Datenbank](../../relational-databases/databases/tempdb-database.md).  
  
> [!NOTE]  
>  Um dies von oder [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]aus aufzurufen, verwenden Sie den Namen **sys. dm_pdw_nodes_db_task_space_usage**.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|Sitzungs-ID|  
|**request_id**|**int**|Anforderungs-ID innerhalb der Sitzung.<br /><br /> Eine Anforderung wird auch als Batch bezeichnet und enthält mindestens eine Abfrage. Für eine Sitzung können mehrere Anforderungen gleichzeitig aktiviert sein. Jede Abfrage der Anforderung kann mehrere Threads (Tasks) starten, falls ein paralleler Ausführungsplan verwendet wird.|  
|**exec_context_id**|**int**|Ausführungskontext-ID des Tasks. Weitere Informationen finden Sie unter [sys. dm_os_tasks &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md).|  
|**database_id**|**smallint**|Datenbank-ID|  
|**user_objects_alloc_page_count**|**BIGINT**|Anzahl von Seiten, die von diesem Task für Benutzerobjekte reserviert oder zugeordnet werden.|  
|**user_objects_dealloc_page_count**|**BIGINT**|Anzahl von Seiten, deren Zuordnung von diesem Task für Benutzerobjekte aufgehoben wird und die nicht mehr reserviert sind.|  
|**internal_objects_alloc_page_count**|**BIGINT**|Anzahl von Seiten, die von diesem Task für interne Objekte reserviert oder zugeordnet werden.|  
|**internal_objects_dealloc_page_count**|**BIGINT**|Anzahl von Seiten, deren Zuordnung von diesem Task für interne Objekte aufgehoben wird und die nicht mehr reserviert sind.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, auf dem sich diese Distribution befindet.|  
  
## <a name="permissions"></a>Berechtigungen

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]ist die `VIEW SERVER STATE` -Berechtigung erforderlich.   
Bei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium-Tarifen ist die `VIEW DATABASE STATE` -Berechtigung in der Datenbank erforderlich. In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] den Tarifen "Standard" und "Basic" ist der **Server Administrator** oder ein **Azure Active Directory Administrator** Konto erforderlich.   

## <a name="remarks"></a>Bemerkungen  
 IAM-Seiten werden nicht in die von dieser Sicht gemeldete Seitenanzahl einbezogen.  
  
 Seitenzähler werden zu Beginn einer Anforderung mit null (0) initialisiert. Diese Werte werden auf der Sitzungsebene aggregiert, wenn die Anforderung abgeschlossen ist. Weitere Informationen finden Sie unter [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md).  
  
 Das Zwischenspeichern von Arbeitstabellen bzw. temporären Tabellen sowie verzögerte Löschvorgänge beeinflussen die Anzahl von Seiten, die für einen angegebenen Task zugeordnet werden bzw. deren Zuordnung aufgehoben wird.  
  
## <a name="user-objects"></a>Benutzerobjekte  
 Die folgenden Objekte sind in den Seitenzählern für Benutzerobjekte enthalten:  
  
-   Benutzerdefinierte Tabellen und Indizes  
  
-   Systemtabellen und -indizes  
  
-   Globale temporäre Tabellen und Indizes  
  
-   Lokale temporäre Tabellen und Indizes  
  
-   Tabellenvariablen  
  
-   In Tabellenwertfunktionen zurückgegebene Tabellen  
  
## <a name="internal-objects"></a>Interne Objekte  
 Interne Objekte werden nur in **tempdb**gespeichert. Die folgenden Objekte sind in den Seitenzählern für interne Objekte enthalten:  
  
-   Arbeitstabellen für Cursor- oder Spoolvorgänge und temporären LOB-Speicher (Large Object)  
  
-   Arbeitsdateien für Vorgänge wie z. B. Hashjoins  
  
-   Sortierläufe  
  
## <a name="physical-joins"></a>Physische Joins  
 ![Physische Joins für sys.dm_db_session_task_usage](../../relational-databases/system-dynamic-management-views/media/join-dm-db-task-space-usage-1.gif "Physische Joins für sys.dm_db_session_task_usage")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|To|Beziehung|  
|----------|--------|------------------|  
|dm_db_task_space_usage.request_id|dm_exec_requests.request_id|1:1|  
|dm_db_task_space_usage.session_id|dm_exec_requests.session_id|1:1|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungs Sichten im Zusammenhang mit der Datenbank &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys. dm_os_tasks &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys. dm_db_session_space_usage &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)   
 [sys. dm_db_file_space_usage &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  


