---
title: sys. dm_os_tasks (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_tasks
- sys.dm_os_tasks_TSQL
- dm_os_tasks_TSQL
- dm_os_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_tasks dynamic management view
ms.assetid: 180a3c41-e71b-4670-819d-85ea7ef98bac
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 086065aa79ca6fba7ad84e5b7e7f99f6f462f7dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "74164900"
---
# <a name="sysdm_os_tasks-transact-sql"></a>sys.dm_os_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jeden aktiven Task in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zurück. Bei einer Aufgabe handelt es sich um die grundlegende Ausführungs Einheit in SQL Server. Zu den Aufgaben zählen z. b. eine Abfrage, eine-Anmeldung, eine Abmelde-und System Tasks wie Aktivität für inaktive Bereinigungs Aktivität, Prüf Punkt Aktivität, protokollwriter, parallele Wiederholungs Aktivitäten. Weitere Informationen zu Aufgaben finden Sie im [Handbuch zur Thread-und Task Architektur](../../relational-databases/thread-and-task-architecture-guide.md).
  
> [!NOTE]  
> Um dies von oder [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]aus aufzurufen, verwenden Sie den Namen **sys. dm_pdw_nodes_os_tasks**.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|Speicheradresse des Objekts.|  
|**task_state**|**nvarchar (60)**|Der Status des Tasks. Mögliche Werte:<br /><br /> PENDING: Warten auf einen Arbeitsthread.<br /><br /> RUNNABLE: Ausführbar, doch wird auf das Eintreffen eines Quantums gewartet.<br /><br /> RUNNING: Wird derzeit auf dem Zeitplanungsmodul ausgeführt.<br /><br /> SUSPENDED: Verfügt über einen Arbeitsthread, wartet jedoch auf ein Ereignis.<br /><br /> DONE: Abgeschlossen.<br /><br /> SPINLOOP: In einem Spinlock festgehalten.|  
|**context_switches_count**|**int**|Anzahl der Kontextwechsel im Zeitplanungsmodul, die dieser Task abgeschlossen hat.|  
|**pending_io_count**|**int**|Anzahl der physischen E/A-Vorgänge, die dieser Task ausgeführt hat.|  
|**pending_io_byte_count**|**BIGINT**|Gesamtbytezahl der von diesem Task ausgeführten E/A-Vorgänge.|  
|**pending_io_byte_average**|**int**|Durchschnittliche Bytezahl der von diesem Task ausgeführten E/A-Vorgänge.|  
|**scheduler_id**|**int**|ID des übergeordneten Zeitplanungsmoduls. Dies ist ein Handle für die Zeitplanungsmodul-Informationen zu diesem Task. Weitere Informationen finden Sie unter [sys. dm_os_schedulers &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|**session_id**|**smallint**|ID der Sitzung, die dem Task zugeordnet ist.|  
|**exec_context_id**|**int**|Die dem Task zugeordnete Ausführungskontext-ID.|  
|**request_id**|**int**|Die ID der Anforderung des Tasks. Weitere Informationen finden Sie unter [sys. dm_exec_requests &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|**worker_address**|**varbinary(8)**|Speicheradresse des Arbeitsthreads, der den Task ausführt.<br /><br /> NULL = Task wartet entweder darauf, dass ein Arbeitsthread ausgeführt werden kann, oder die Ausführung des Threads wurde soeben beendet.<br /><br /> Weitere Informationen finden Sie unter [sys. dm_os_workers &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|**host_address**|**varbinary(8)**|Speicheradresse des Hosts.<br /><br /> 0 = Hosting wurde zum Erstellen des Tasks nicht verwendet. Dadurch kann der Host identifiziert werden, der zum Erstellen dieses Tasks verwendet wurde.<br /><br /> Weitere Informationen finden Sie unter [sys. dm_os_hosts &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md).|  
|**parent_task_address**|**varbinary(8)**|Speicheradresse des Tasks, der dem Objekt übergeordnet ist.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, auf dem sich diese Distribution befindet.|  
  
## <a name="permissions"></a>Berechtigungen
In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]ist die `VIEW SERVER STATE` -Berechtigung erforderlich.   
Bei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium-Tarifen ist die `VIEW DATABASE STATE` -Berechtigung in der Datenbank erforderlich. In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] den Tarifen "Standard" und "Basic" ist der **Server Administrator** oder ein **Azure Active Directory Administrator** Konto erforderlich.   

## <a name="examples"></a>Beispiele  
  
### <a name="a-monitoring-parallel-requests"></a>A. Überwachung paralleler Anforderungen  
 Bei Anforderungen, die parallel ausgeführt werden, werden mehrere Zeilen für die gleiche Kombination von (\<**session_id**> \< **request_id**>) angezeigt. Verwenden Sie die folgende Abfrage, um die [Server Konfigurations Option max. Grad an Parallelität konfigurieren](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) für alle aktiven Anforderungen zu finden.  
  
> [!NOTE]  
>  Eine **request_id** ist innerhalb einer Sitzung eindeutig.  
  
```  
SELECT  
    task_address,  
    task_state,  
    context_switches_count,  
    pending_io_count,  
    pending_io_byte_count,  
    pending_io_byte_average,  
    scheduler_id,  
    session_id,  
    exec_context_id,  
    request_id,  
    worker_address,  
    host_address  
  FROM sys.dm_os_tasks  
  ORDER BY session_id, request_id;  
```  
  
### <a name="b-associating-session-ids-with-windows-threads"></a>B. Zuordnen von Sitzungs-IDs und Windows-Threads  
 Mithilfe der folgenden Abfrage lässt sich eine Sitzungs-ID einer Windows-Thread-ID zuordnen. Sie können die Leistung des Threads dann im Windows-Systemmonitor überwachen. Mit der folgenden Abfrage werden keine Informationen für ruhende Sitzungen (sleeping) zurückgegeben.  
  
```  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen  
[SQL Server dynamischen Verwaltungs Sichten im Zusammenhang mit dem Betriebs System &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
[Handbuch zur Thread- und Taskarchitektur](../../relational-databases/thread-and-task-architecture-guide.md)     
  


