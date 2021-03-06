---
title: sp_browsereplcmds (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: stevestein
ms.author: sstein
ms.openlocfilehash: d049a5e96d9c7212467595aa70cd44db727bdf6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769001"
---
# <a name="sp_browsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Wird als Diagnosetool verwendet und gibt ein Resultset mit einer lesbaren Version der replizierten Befehle zurück, die in der Verteilungsdatenbank gespeichert sind. Diese gespeicherte Prozedur wird auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol für Themenlink") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @xact_seqno_start = ] 'xact_seqno_start'`Gibt die niedrigste genaue Sequenznummer an, die zurückgegeben werden soll. *xact_seqno_start* ist vom Typ **NCHAR (22)** und hat den Standardwert 0x00000000000000000000.  
  
`[ @xact_seqno_end = ] 'xact_seqno_end'`Gibt die höchste genaue Sequenznummer an, die zurückgegeben werden soll. *xact_seqno_end* ist vom Typ **NCHAR (22)**. der Standardwert ist 0xFFFFFFFFFFFFFFFFFFFF.  
  
`[ @originator_id = ] 'originator_id'`Gibt an, ob Befehle mit dem angegebenen *originator_id* zurückgegeben werden. *originator_id* ist vom Datentyp **int**und hat den Standardwert NULL.  
  
`[ @publisher_database_id = ] 'publisher_database_id'`Gibt an, ob Befehle mit dem angegebenen *publisher_database_id* zurückgegeben werden. *publisher_database_id* ist vom Datentyp **int**und hat den Standardwert NULL.  
  
`[ @article_id = ] 'article_id'`Gibt an, ob Befehle mit dem angegebenen *article_id* zurückgegeben werden. *article_id* ist vom Datentyp **int**und hat den Standardwert NULL.  
  
`[ @command_id = ] command_id`Der Speicherort des Befehls in [MSrepl_commands &#40;Transact-SQL-&#41;](../../relational-databases/system-tables/msrepl-commands-transact-sql.md) decodiert werden. *command_id* ist vom Datentyp **int**und hat den Standardwert NULL. Wenn angegeben, müssen auch alle anderen Parameter angegeben werden, und *xact_seqno_start*müssen mit *xact_seqno_end*identisch sein.  
  
`[ @agent_id = ] agent_id`Gibt an, dass nur Befehle für einen bestimmten Replikations-Agent zurückgegeben werden. *agent_id* ist vom Datentyp **int**und hat den Standardwert NULL.  
  
`[ @compatibility_level = ] compatibility_level`Die Version [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von, auf der die *COMPATIBILITY_LEVEL* **int**ist, mit dem Standardwert 9 Millionen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|Sequenznummer des Befehls.|  
|**originator_srvname**|**sysname**|Server, von dem die Transaktion stammt|  
|**originator_db**|**sysname**|Datenbank, von der die Transaktion stammt|  
|**article_id**|**int**|ID des Artikels.|  
|**type**|**int**|Der Typ des Befehls.|  
|**partial_command**|**bit**|Zeigt an, ob dies ein Teilbefehl ist.|  
|**hashkey**|**int**|Nur interne Verwendung.|  
|**originator_publication_id**|**int**|ID der Veröffentlichung, von der die Transaktion stammt|  
|**originator_db_version**|**int**|Version der Datenbank, von der die Transaktion stammt|  
|**originator_lsn**|**varbinary(16)**|Identifiziert die Protokollfolgenummer (LSN, Log Sequence Number) für den Befehl in der ursprünglichen Veröffentlichung Wird in der Peer-zu-Peer-Transaktions Replikation verwendet.|  
|**s**|**nvarchar (1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)]s.|  
|**command_id**|**int**|ID des Befehls in [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
  
 Lange Befehle können auf mehrere Zeilen des Resultsets aufgeteilt werden.  
  
## <a name="remarks"></a>Bemerkungen  
 **sp_browsereplcmds** wird bei der Transaktions Replikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Server Rolle **sysadmin** oder Mitglieder der festen Daten bankrollen **db_owner** oder **replmonitor** in der Verteilungs Datenbank können **sp_browsereplcmds**ausführen.  
  
## <a name="see-also"></a>Weitere Informationen  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
