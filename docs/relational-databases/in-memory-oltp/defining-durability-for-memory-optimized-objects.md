---
title: Definieren von Dauerhaftigkeit für speicheroptimierte Objekte | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 764824a74480b6d17c890f57714b0df9221bf523
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "68219871"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>Definieren von Dauerhaftigkeit für speicheroptimierte Objekte
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Es gibt zwei Dauerhaftigkeitsoptionen für speicheroptimierte Tabellen:  
  
 SCHEMA_AND_DATA (Standard)  
 Diese Option gewährleistet Dauerhaftigkeit für Schema und Daten. Der Grad der Datendauerhaftigkeit ist abhängig davon, ob Sie ein Commit für eine Transaktion mit vollständiger oder verzögerter Dauerhaftigkeit ausführen. Vollständig dauerhafte Transaktionen bieten die gleiche Dauerhaftigkeitsgarantie für Daten und Schemas – ähnlich einer datenträgerbasierten Tabelle. Verzögerte Dauerhaftigkeit verbessert die Leistung, kann aber im Falle eines Serverabsturzes oder Failovers zu Datenverlusten führen. (Weitere Informationen zur verzögerten Dauerhaftigkeit finden Sie unter [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md).)  
  
 SCHEMA_ONLY  
 Diese Option stellt die Dauerhaftigkeit des Tabellenschemas sicher. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet wird oder eine Neukonfiguration in einer Azure SQL-Datenbank auftritt, besteht das Tabellenschema weiterhin, Daten in der Tabelle gehen jedoch verloren. (Dies steht im Gegensatz zu einer Tabelle in tempdb, bei der sowohl die Tabelle als auch die Daten beim Neustart verloren gehen.) Ein typisches Szenario zum Erstellen einer nichtdauerhaften Tabelle besteht darin, kurzlebige Daten wie eine Stagingtabelle für einen ETL-Vorgang zu speichern. Durch SCHEMA_ONLY-Dauerhaftigkeit werden Transaktionsprotokollierung und -prüfpunkt vermieden, was zu einer erheblichen Reduzierung von E/A-Vorgängen führen kann.  
  
 Bei der Verwendung der Standardtabelle SCHEMA_AND_DATA bietet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die gleiche Dauerhaftigkeit, die auch bei datenträgerbasierten Tabellen gewährleistet wird:  
  
 Dauerhaftigkeit von Transaktionen  
 Wenn Sie ein Commit für eine vollständig dauerhafte Transaktion ausführen, die DDL- oder DML-Änderungen an einer speicheroptimierten Tabelle vorgenommen hat, werden die Änderungen, die an einer dauerhaften speicheroptimierten Tabelle vorgenommen wurden, dauerhaft gespeichert.  
  
 Wenn Sie für eine verzögert dauerhafte Transaktion ein Commit in einer speicheroptimierte Tabelle ausführen, wird die Transaktion erst dauerhaft, nachdem das Transaktionsprotokoll im Arbeitsspeicher auf dem Datenträger gespeichert wurde. (Weitere Informationen zur verzögerten Dauerhaftigkeit finden Sie unter [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md).)  
  
 Dauerhaftigkeit bei Neustarts  
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach einem Systemabsturz oder einem geplanten Herunterfahren neu gestartet wird, werden die speicheroptimierten Tabellen erneut instanziiert, um den Status der Tabellen vor dem Herunterfahren oder Systemabsturz wiederherzustellen.  
  
 Dauerhaftigkeit bei Medienfehlern  
 Wenn sich auf einem fehlerhaften oder beschädigten Datenträger eine oder mehrere persistente Kopien von dauerhaften speicheroptimierten Objekten befinden, werden durch die Sicherungs- und Wiederherstellungsfunktion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speicheroptimierte Tabellen auf dem neuen Medium wiederhergestellt.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Verwalten von Speicher für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
