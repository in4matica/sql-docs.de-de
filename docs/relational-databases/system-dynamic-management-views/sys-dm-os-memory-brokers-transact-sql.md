---
title: sys. dm_os_memory_brokers (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_brokers
- dm_os_memory_brokers_TSQL
- sys.dm_os_memory_brokers_TSQL
- dm_os_memory_brokers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_brokers dynamic management view
ms.assetid: 48dd6ad9-0d36-4370-8a12-4921d0df4b86
author: stevestein
ms.author: sstein
ms.openlocfilehash: a8e131e2550ffa5078df5e284898ffe936128b7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68265869"
---
# <a name="sysdm_os_memory_brokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Interne Zuordnungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden den Speicher-Manager von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn Sie den Unterschied zwischen Prozess Speicher-Leistungsindikatoren aus **sys. dm_os_process_memory** und internen Leistungsindikatoren nachverfolgen, können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sie die Speicherauslastung von externen Komponenten im Speicherbereich angeben.  
  
 Speicherbroker verteilen Speicherbelegungen gleichmäßig auf die verschiedenen Komponenten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf Basis der aktuellen und der prognostizierten Auslastung. Speicherbroker führen keine Zuordnungen durch. Sie verfolgen Zuordnungen nur zum Berechnen der Verteilung.  
  
 Die folgende Tabelle enthält Informationen zu Speicherbrokern.  
  
> [!NOTE]  
>  Um dies von oder [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]aus aufzurufen, verwenden Sie den Namen **sys. dm_pdw_nodes_os_memory_brokers**.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|ID des Ressourcenpools, wenn er einem Ressourcenkontrollenpool zugeordnet ist.|  
|**memory_broker_type**|**nvarchar (60)**|Typ des Speicherbrokers. Derzeit gibt es drei Typen von Speicher Brokern [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die unten mit ihren Beschreibungen aufgeführt sind.<br /><br /> **MEMORYBROKER_FOR_CACHE** : Arbeitsspeicher, der für zwischengespeicherte Objekte (nicht Puffer Pool Cache) reserviert ist.<br /><br /> **MEMORYBROKER_FOR_STEAL** : Arbeitsspeicher, der aus dem Pufferpool gestohlen wird. Dieser Speicher ist erst dann zur Wiederverwendung durch andere Komponenten verfügbar, wenn er durch den aktuellen Besitzer freigegeben wird.<br /><br /> **MEMORYBROKER_FOR_RESERVE** : Arbeitsspeicher, der für die zukünftige Verwendung durch aktuell ausgeführte Anforderungen reserviert ist.|  
|**allocations_kb**|**BIGINT**|Größe des Arbeitsspeichers in Kilobyte (KB), der diesem Typ Broker zugeordnet wurde.|  
|**allocations_kb_per_sec**|**BIGINT**|Rate der Speicherbelegungen in Kilobyte (KB) pro Sekunde. Dieser Wert kann für die Aufhebung von Arbeitsspeicherzuordnungen negativ sein.|  
|**predicted_allocations_kb**|**BIGINT**|Vorhergesagte Größe des durch den Broker belegten Arbeitsspeichers. Dieser Wert basiert auf dem Speicherauslastungsmuster.|  
|**target_allocations_kb**|**BIGINT**|Empfohlene Größe des belegten Speichers in Kilobyte (KB) auf Basis der aktuellen Einstellungen und des Speicherverwendungsmusters. Dieser Broker sollte auf diesen Wert vergrößert oder verkleinert werden.|  
|**future_allocations_kb**|**BIGINT**|Prognostizierte Anzahl der Zuordnungen in Kilobyte (KB), die in den nächsten Sekunden erfolgen werden.|  
|**overall_limit_kb**|**BIGINT**|Maximale Arbeitsspeicher Menge in Kilobyte (KB), die der Broker zuordnen kann.|  
|**last_notification**|**nvarchar (60)**|Speicherauslastungsempfehlung auf Basis der aktuellen Einstellungen und des Verwendungsmusters. Gültige Werte sind:<br /><br /> grow<br /><br /> shrink<br /><br /> stable|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, auf dem sich diese Distribution befindet.|  
  
## <a name="permissions"></a>Berechtigungen  

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]ist die `VIEW SERVER STATE` -Berechtigung erforderlich.   
Bei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium-Tarifen ist die `VIEW DATABASE STATE` -Berechtigung in der Datenbank erforderlich. In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] den Tarifen "Standard" und "Basic" ist der **Server Administrator** oder ein **Azure Active Directory Administrator** Konto erforderlich.   
  
## <a name="see-also"></a>Weitere Informationen  

  [SQL Server dynamischen Verwaltungs Sichten im Zusammenhang mit dem Betriebs System &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


