---
title: MSrepl_identity_range (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_identity_range_TSQL
- MSrepl_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_identity_range system table
ms.assetid: 6e92a8e8-7667-4c98-b1c4-46735bac50d8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 38f5037598e240585333d246a99c29c5fd8f40fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079160"
---
# <a name="msrepl_identity_range-transact-sql"></a>MSrepl_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSrepl_identity_range** Tabelle bietet Unterstützung für die Identitäts Bereichs Verwaltung. Diese Tabelle wird in den Datenbanken publication, distribution und subscription gespeichert.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**Gebers**|**sysname**|Der Name des Verlegers.|  
|**publisher_db**|**sysname**|Der Name der Veröffentlichungs Datenbank.|  
|**TableName**|**sysname**|Der Name der Tabelle.|  
|**identity_support**|**int**|Gibt an, ob die automatische Behandlung der Identitätsbereiche aktiviert ist. 0 gibt an, dass die automatische Behandlung der Identitätsbereiche nicht aktiviert ist.|  
|**next_seed**|**BIGINT**|Wenn die automatische Behandlung der Identitätsbereiche aktiviert ist, zeigt dieser Wert den Anfangspunkt des nächsten Bereichs an.|  
|**pub_range**|**BIGINT**|Die Größe des Identitätsbereichs für den Verleger.|  
|**Bereich**|**BIGINT**|Die Bereichsgröße der aufeinander folgenden Identitätswerte, die Abonnenten bei einer Anpassung zugewiesen würden.|  
|**max_identity**|**BIGINT**|Die obere Grenze des Identitätsbereichs.|  
|**Mindest**|**int**|Als Prozentsatz angegebener Schwellenwert für den Identitätsbereich.|  
|**current_max**|**BIGINT**|Der aktuelle maximale Wert, der zugewiesen werden kann, aber nicht notwendigerweise zugewiesen werden muss.|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Replikations Tabellen &#40;Transact-SQL-&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
