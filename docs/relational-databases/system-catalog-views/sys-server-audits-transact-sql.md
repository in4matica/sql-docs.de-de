---
title: sys. server_audits (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_audits_TSQL
- sys.server_audits_TSQL
- sys.server_audits
- server_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_audits catalog view
ms.assetid: c2c4a000-1127-46a8-b1e9-947fd1136e1e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a00f6843a0ef379c12aa1d1d00df9380efbd139
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124996"
---
# <a name="sysserver_audits-transact-sql"></a>sys.server_audits (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Überwachung in einer Serverinstanz. Weitere Informationen finden Sie unter [SQL Server Audit &#40;Datenbank-Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|Die ID der Überwachung.|  
|**name**|**sysname**|Der Name der Überwachung.|  
|**audit_guid**|**uniqueidentifier**|GUID für die Überwachung, die zum Aufzählen von Überwachungen mit Mitglieds Server-&#124;Datenbank-Überwachungs Spezifikationen während der Server Start-und Anfüge Vorgänge für Datenbanken verwendet wird.|  
|**create_date**|**datetime**|Das UTC-Datum, an dem die Überwachung erstellt wurde|  
|**modify_date**|**datetime**|Das UTC-Datum, an dem die Überwachung zuletzt geändert wurde.|  
|**principal_id**|**int**|Die ID des Besitzers der Überwachung gemäß Registrierung beim Server.|  
|**type**|**char (2)**|Überwachungstyp:<br /><br /> SL-NT-Sicherheits Ereignisprotokoll<br /><br /> Al-NT-Anwendungs Ereignisprotokoll<br /><br /> FL-Datei im Dateisystem|  
|**type_desc**|**nvarchar (60)**|SECURITY LOG<br /><br /> APPLICATION LOG<br /><br /> FILE|  
|**on_failure**|**tinyint**|Bei einem Fehler schreiben Sie folgendermaßen einen Aktionseintrag:<br /><br /> 0-fortfahren<br /><br /> 1-Serverinstanz herunterfahren<br /><br /> 2-fehlerhafter Vorgang|  
|**on_failure_desc**|**nvarchar (60)**|Bei einem Fehler schreiben Sie folgendermaßen einen Aktionseintrag:<br /><br /> CONTINUE<br /><br /> SHUTDOWN SERVER INSTANCE<br /><br /> FAIL_OPERATION|  
|**is_state_enabled**|**tinyint**|0-deaktiviert<br /><br /> 1 – Aktiviert|  
|**queue_delay**|**int**|Maximale Wartezeit in Millisekunden, bevor auf den Datenträger geschrieben wird. Wenn 0, garantiert die Überwachung einen Schreibvorgang, bevor ein Ereignis fortgesetzt werden kann.|  
|**Prädikat**|**nvarchar (3000)**|Der Prädikatausdruck, der auf das Ereignis angewendet wird.|  
  
## <a name="permissions"></a>Berechtigungen  
 Prinzipale mit der Berechtigung **Alter any Server Audit** oder **View any Definition** haben Zugriff auf diese Katalog Sicht. Außerdem darf dem Prinzipal die **View any Definition** -Berechtigung nicht verweigert werden.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Weitere Informationen  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Erstellen einer Serverüberwachung und einer Serverüberwachungsspezifikation](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
