---
title: Ihabonnements (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsubscriptions_TSQL
- IHsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- IHsubscriptions system table
ms.assetid: 9ec21119-35f1-4e39-abaa-b2c790c485b1
author: stevestein
ms.author: sstein
ms.openlocfilehash: b677e0f6c9be058650a46aee3465811b8f3eecc7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990144"
---
# <a name="ihsubscriptions-transact-sql"></a>IHsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **ihabonnements** -Systemtabelle enthält eine Zeile für jedes Abonnement einer Veröffentlichung von einem nicht-SQL Server-Verleger, der den aktuellen Verteiler verwendet. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Eindeutige Identifikation eines veröffentlichten Artikels.|  
|**srvid**|**smallint**|Die Server-ID des Abonnenten.|  
|**dest_db**|**sysname**|Der Name der Zieldatenbank.|  
|**login_name**|**sysname**|Der Anmeldename, der beim Hinzufügen des Abonnements verwendet wird.|  
|**distribution_jobid**|**Binary (16)**|Die Auftrags-ID des Verteilungs-Agents.|  
|**timestamp**|**timestamp**|Datum und Uhrzeit der Erstellung des Abonnements.|  
|**queued_reinit**|**bit**|Gibt an, ob der Artikel für die Initialisierung oder erneute Initialisierung markiert ist. Der Wert **1** gibt an, dass der abonnierte Artikel für die Initialisierung oder erneute Initialisierung markiert ist.|  
|**Stands**|**tinyint**|Status des Abonnements:<br /><br /> **0** = inaktiv.<br /><br /> **1** = abonniert.<br /><br /> **2** = aktiv.|  
|**sync_type**|**tinyint**|Der Typ der Erstsynchronisierung:<br /><br /> **1** = automatisch.<br /><br /> **2** = keine.|  
|**subscription_type**|**int**|Der Typ des Abonnements:<br /><br /> **0** = Push-der Verteilungs-Agent wird auf dem Abonnenten ausgeführt.<br /><br /> **1** = Pull-der Verteilungs-Agent wird auf dem Verteiler ausgeführt.|  
|**update_mode**|**tinyint**|Updatemodus:<br /><br /> **0** = schreibgeschützt.<br /><br /> **1** = sofortige Aktualisierung.|  
|**loopback_detection**|**bit**|Gilt für Abonnements, die Teil einer bidirektionalen Transaktionsreplikationstopologie sind. Bestimmt, ob der Verteilungs-Agent Transaktionen des Abonnenten zurück an den Abonnenten sendet:<br /><br /> **0** = sendet zurück.<br /><br /> **1** = sendet nicht zurück.|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikations Tabellen &#40;Transact-SQL-&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikations Sichten &#40;Transact-SQL-&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addsubscription &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
