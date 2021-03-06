---
title: sys. dm_operation_status (Azure SQL-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/05/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_operation_status_TSQL
- dm_operation_status
- sys.dm_operation_status
- sys.dm_operation_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_operation_status dynamic management view
- sys.dm_operation_status dynamic management view
ms.assetid: cc847784-7f61-4c69-8b78-5f971bb24d61
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c49e4e01dd8ddaf0667546a8cc221a7918f42c81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "70911202"
---
# <a name="sysdm_operation_status-azure-sql-database"></a>sys.dm_operation_status (Azure SQL-Datenbank)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Gibt Informationen zu den Vorgängen zurück, die für Datenbanken auf einem [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]-Server ausgeführt werden.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|session_activity_id|**uniqueidentifier**|ID des Vorgangs. Nicht NULL.|  
|resource_type|**int**|Bezeichnet den Typ der Ressource, für die der Vorgang ausgeführt wird. Nicht NULL. In der aktuellen Version verfolgt diese Sicht nur die Vorgänge nach, die für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ausgeführt werden. Der entsprechende ganzzahlige Wert ist 0.|  
|resource_type_desc|**nvarchar (2048)**|Beschreibung des Ressourcentyps, für den der Vorgang ausgeführt wird. In der aktuellen Version verfolgt diese Sicht nur die Vorgänge nach, die für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ausgeführt werden.|  
|major_resource_id|**sql_variant**|Name von [!INCLUDE[ssSDS](../../includes/sssds-md.md)], für die der Vorgang ausgeführt wird. Nicht NULL.|  
|minor_resource_id|**sql_variant**|Nur zur internen Verwendung. Nicht NULL.|  
|Vorgang|**nvarchar (60)**|Für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ausgeführter Vorgang, z. B. CREATE oder ALTER.|  
|state|**tinyint**|Der Zustand des Vorgangs.<br /><br /> 0 = Ausstehend<br />1 = Vorgang wird ausgeführt<br />2 = Abgeschlossen<br />3 = fehlgeschlagen<br />4 = Abgebrochen|  
|state_desc|**nvarchar (120)**|PENDING = Vorgang wartet auf verfügbare Ressource oder verfügbares Kontingent.<br /><br /> IN_PROGRESS = Vorgang wurde gestartet und wird ausgeführt.<br /><br /> COMPLETED = Vorgang wurde erfolgreich abgeschlossen.<br /><br /> FAILED = Vorgang ist fehlgeschlagen. Weitere Informationen finden Sie in der Spalte **error_desc** .<br /><br /> CANCELLED = Vorgang wurde auf Anforderung des Benutzers beendet.|  
|percent_complete|**int**|Prozentsatz des Vorgangs, der abgeschlossen wurde. Werte sind nicht kontinuierlich, und die gültigen Werte sind unten aufgeführt. Nicht NULL.<br/><br/>0 = Vorgang wurde nicht gestartet.<br/>50 = Vorgang wird ausgeführt<br/>100 = Vorgang wurde beendet.|  
|error_code|**int**|Code, der den Fehler angibt, der während eines fehlgeschlagenen Vorgangs aufgetreten ist. Wenn der Wert 0 ist, bedeutet dies, dass der Vorgang erfolgreich abgeschlossen wurde.|  
|error_desc|**nvarchar (2048)**|Beschreibung des Fehlers, der während eines fehlgeschlagenen Vorgangs aufgetreten ist.|  
|error_severity|**int**|Schweregrad des Fehlers, der während eines fehlgeschlagenen Vorgangs aufgetreten ist. Weitere Informationen zu Schweregraden von Fehlern finden Sie unter [Datenbank-Engine schwere](https://go.microsoft.com/fwlink/?LinkId=251052)Grade von Fehlern.|  
|error_state|**int**|Für die zukünftige Verwendung reserviert. Zukünftige Kompatibilität wird nicht sichergestellt.|  
|start_time|**datetime**|Zeitstempel, an dem der Vorgang begonnen wurde.|  
|last_modify_time|**datetime**|Zeitstempel, an dem der Datensatz zuletzt für einen länger ausgeführten Vorgang geändert wurde. Im Fall von erfolgreich abgeschlossenen Vorgängen wird in diesem Feld der Zeitstempel angezeigt, an dem der Vorgang abgeschlossen wurde.|  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Ansicht ist nur in der **Master** -Datenbank für den Prinzipal Anmelde Namen auf Serverebene verfügbar.  
  
## <a name="remarks"></a>Bemerkungen  
 Um diese Ansicht verwenden zu können, müssen Sie mit der **Master** -Datenbank verbunden sein. Verwenden Sie `sys.dm_operation_status` die-Sicht in der **Master** - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Datenbank des-Servers, um den Status der folgenden Vorgänge zu [!INCLUDE[ssSDS](../../includes/sssds-md.md)]verfolgen, die auf einem ausgeführt werden:  
  
-   Erstellen einer Datenbank  
  
-   Kopieren einer Datenbank. Mit Datenbankkopie wird ein Datensatz in dieser Sicht auf den Quell- und Zielservern erstellt.  
  
-   Ändern einer Datenbank  
  
-   Ändern der Leistungsebene einer Dienstebene  
  
-   Ändern der Dienstebene einer Datenbank, z. B. von Basic in Standard.  
  
-   Einrichten einer Georeplikationsbeziehung  
  
-   Beenden einer Georeplikationsbeziehung  
  
-   Datenbank wiederherstellen  
  
-   Datenbank löschen  
  
## <a name="example"></a>Beispiel  
 Zeigt die letzten georeplikationsvorgänge an, die der Datenbank "MyDB" zugeordnet sind.  
  
```  
SELECT * FROM sys.dm_operation_status   
   WHERE major_resource_id = 'myddb'   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Dynamische Verwaltungs Sichten und-Funktionen für die georeplikation &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [sys. dm_geo_replication_link_status &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys. geo_replication_links &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [Alter Database &#40;Azure SQL-Datenbank&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  
