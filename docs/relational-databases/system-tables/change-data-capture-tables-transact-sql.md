---
title: Change Data Capture-Tabellen (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a4372d0b-50ca-4e58-80f6-2ed3cb52a84a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d6d87ee8b2aa05c3156acb2db9c6604380db887
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68082684"
---
# <a name="change-data-capture-tables-transact-sql"></a>Change Data Capture-Tabellen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Change Data Capture ermöglicht eine Änderungsnachverfolgung für Tabellen, sodass DML (Data Manipulation Language)- und DDL (Data Definition Language)-Änderungen an den Tabellen inkrementell in ein Data Warehouse geladen werden können. In den Themen in diesem Abschnitt werden die Systemtabellen beschrieben, in denen die von Change Data Capture-Vorgängen verwendeten Informationen gespeichert werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [capture_instance>_CT CDC. <](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
 Gibt eine Zeile für jede Änderung an einer aufgezeichneten Spalte in der zugeordneten Quelltabelle zurück.  
  
 [cdc.captured_columns](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
 Gibt eine Zeile für jede in einer Aufzeichnungsinstanz nachverfolgte Spalte zurück.  
  
 [cdc.change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
 Gibt eine Zeile pro Änderungstabelle in der Datenbank zurück.  
  
 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)  
 Gibt eine Zeile für jede Änderung an der Datendefinitionssprache (DDL) zurück, die an Tabellen vorgenommen wurde, die für Change Data Capture aktiviert wurden.  
  
 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)  
 Gibt eine Zeile für jede Transaktion zurück, für die Zeilen in einer Änderungstabelle aufgezeichnet sind. Diese Tabelle wird verwendet, um die Commitwerte der Protokollfolgenummer (Log Sequence Number, LSN) mit dem Commitzeitpunkt der Transaktion zu verknüpfen.  
  
 [cdc.index_columns](../../relational-databases/system-tables/cdc-index-columns-transact-sql.md)  
 Gibt eine Zeile für jede Indexspalte zurück, die einer Änderungstabelle zugeordnet ist.  
  
 [dbo. cdc_jobs &#40;Transact-SQL-&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
 Gibt die Konfigurationsparameter für Change Data Capture-Agentaufträge zurück.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Gespeicherte Prozeduren für Change Data Capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Change Data Capture-Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)  
  
  
