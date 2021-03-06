---
title: Initialisieren eines Abonnements mit einer Momentaufnahme | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3624d1eef64f10ae93802c4a7514fd54edcc0e74
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287927"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Initialisieren eines Abonnements mit einer Momentaufnahme
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Nachdem eine Veröffentlichung erstellt wurde, wird normalerweise eine Anfangsmomentaufnahme erstellt und in den Momentaufnahmeordner kopiert (dies erfolgt standardmäßig bei Mergeveröffentlichungen, die mit dem Assistenten für neue Veröffentlichung erstellt wurden). Die Momentaufnahme wird dann während der Erstsynchronisierung des Abonnements vom Verteilungs-Agent (für Transaktions- und Snapshotveröffentlichungen) oder vom Merge-Agent (für Mergeveröffentlichungen) auf den Abonnenten angewendet. Der Momentaufnahmeprozess hängt vom Veröffentlichungstyp ab:  
  
-   Handelt es sich um eine Momentaufnahme für eine Momentaufnahmeveröffentlichung, eine Transaktionsveröffentlichung oder eine Mergeveröffentlichung, die keine parametrisierte Filter verwendet, enthält die Momentaufnahme das Schema und die Daten in BCP-Dateien (Bulk Copy Program, Massenkopierprogramm) sowie Einschränkungen, erweiterte Eigenschaften, Indizes, Trigger und die für die Replikation erforderlichen Systemtabellen. Weitere Informationen zum Erstellen und Anwenden einer Momentaufnahme finden Sie unter [Erstellen und Anwenden der Momentaufnahme](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
-   Handelt es sich um eine Momentaufnahme für eine Mergeveröffentlichung, die parametrisierte Filter verwendet, wird die Momentaufnahme mit einem zweiteiligen Prozess erstellt. Zuerst wird eine Schemamomentaufnahme erstellt, die die Replikationsskripts und das Schema der veröffentlichten Objekte enthält, nicht jedoch die Daten. Jedes Abonnement wird dann mit einer Momentaufnahme initialisiert, die die aus der Schemamomentaufnahme kopierten Skripts und das Schema sowie die Daten enthält, die zur Partition des Abonnements gehören. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Die Momentaufnahme besteht aus verschiedenen Dateien, die vom Replikationstyp und den Artikeln in der Veröffentlichung abhängen. Diese Dateien werden in den Standardmomentaufnahmeordner kopiert, der beim Konfigurieren des Verteilers angegeben wurde, oder in den beim Erstellen der Veröffentlichung angegeben alternativen Momentaufnahmeordner.  
  
|Replikationstyp|Gemeinsame Momentaufnahmedateien|  
|-------------------------|---------------------------|  
|Momentaufnahmereplikation oder Transaktionsreplikation|Schema (SCH); Daten (BCP); Einschränkungen und Indizes (DRI); Einschränkungen (IDX); Trigger (TRG): nur für Updateabonnenten; komprimierte Momentaufnahmedateien (CAP).|  
|Mergereplikation|Schema (SCH); Daten (BCP); Einschränkungen und Indizes (DRI); Trigger (TRG); Systemtabellendaten (SYS); Konflikttabellen (CFT); komprimierte Momentaufnahmedateien (CAP).|  
  
 Falls das Übertragen der Momentaufnahme an einer Stelle unterbrochen wird, wird es anschließend automatisch fortgesetzt. Bereits vollständig übertragene Dateien werden nicht noch einmal gesendet. Teilweise übermittelte Dateien müssen vollständig neu übermittelt werden, da beim Momentaufnahme-Agent die BCP-Datei für jeden Veröffentlichungsartikel zur Übermittlung verwendet wird. Das Fortsetzen der Momentaufnahmeübertragung kann jedoch die Menge der übermittelten Daten erheblich reduzieren und eine rechtzeitige Übermittlung der Momentaufnahme auch bei einer unzuverlässigen Verbindung sicherstellen.  
  
## <a name="snapshot-options"></a>Momentaufnahmeoptionen  
 Zum Initialisieren eines Abonnements mit einer Momentaufnahme stehen verschiedene Optionen zur Verfügung. Ihre Möglichkeiten:  
  
-   Geben Sie anstelle des oder zusätzlich zum Speicherort des Standardmomentaufnahmeordners einen alternativen Speicherort für den Momentaufnahmeordner an. Weitere Informationen finden Sie unter [Ändern von Momentaufnahmeoptionen](../../relational-databases/replication/snapshot-options.md).  
  
-   Komprimieren Sie Momentaufnahmen zum Speichern auf Wechselmedien oder zum Übertragen in einem langsamen Netzwerk. Weitere Informationen finden Sie unter [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots). 

-   Führen Sie vor oder nach dem Anwenden der Momentaufnahme Transact-SQL-Skripts aus. Weitere Informationen finden Sie unter [Ausführen von Skripts vor und nach dem Anwenden der Momentaufnahme](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  
  
-   Übertragen Sie Momentaufnahmedateien über FTP (File Transfer Protocol). Weitere Informationen finden Sie unter [Übertragen von Momentaufnahmen über FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
## <a name="see-also"></a>Weitere Informationen  
 [Initialize a Subscription](../../relational-databases/replication/initialize-a-subscription.md)   
 [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
