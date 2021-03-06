---
title: Dateiwiederherstellungen (vollständiges Wiederherstellungsmodell) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server]
- full recovery model [SQL Server], performing restores
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- file restores [SQL Server], full recovery model
- restoring files [SQL Server], full recovery model
- Transact-SQL restore sequence
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: d2236a2a-4cf1-4c3f-b542-f73f6096e15c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a78b177b1fb429535a4bb9b271d0b1dbc4eedc79
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "62921941"
---
# <a name="file-restores-full-recovery-model"></a>Dateiwiederherstellungen (vollständiges Wiederherstellungsmodell)
  Dieses Thema ist nur für Datenbanken relevant, die mehrere Dateien oder Dateigruppen enthalten, die das vollständige oder massenprotokollierte Wiederherstellungsmodell verwenden.  
  
 Das Ziel einer Dateiwiederherstellung besteht darin, eine oder mehrere beschädigte Dateien wiederherzustellen, ohne dabei die gesamte Datenbank wiederherstellen zu müssen. Ein Dateiwiederherstellungsszenario besteht aus einer einzigen Wiederherstellungssequenz, bei der die entsprechenden Daten kopiert werden, ein Rollforward ausgeführt wird und die Daten wiederhergestellt werden.  
  
 Wenn die wiederherzustellende Dateigruppe Lese-/Schreibzugriff aufweist, muss nach der Wiederherstellung der letzten Daten bzw. der letzten differenziellen Sicherung eine fortlaufende Kette von Protokollsicherungen angewendet werden. Auf diese Weise wird die Dateigruppe auf den Stand der Protokolldatensätze in der aktuellen Protokolldatei gebracht. Der Wiederherstellungspunkt befindet sich normalerweise – aber nicht zwingend – gegen Ende der Protokolldatei.  
  
 Ist die wiederherzustellende Dateigruppe schreibgeschützt, müssen normalerweise keine Protokollsicherungen angewendet werden; dieser Schritt wird daher ausgelassen. Wenn die Sicherung durchgeführt wurde, nachdem die Datei schreibgeschützt worden war, ist dies die letzte Sicherung, die wiederhergestellt werden muss. Die Ausführung des Rollforwards endet am Zielpunkt.  
  
 Für die Dateiwiederherstellung sind folgende Szenarien möglich:  
  
-   Offlinedateiwiederherstellung  
  
     Bei einer *Offlinedateiwiederherstellung*ist die Datenbank offline, während die beschädigten Dateien oder Dateigruppen wiederhergestellt werden. Am Ende der Wiederherstellungssequenz wird die Datenbank wieder online geschaltet.  
  
     Offlinewiederherstellungen werden von allen Editionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt.  
  
-   Onlinedateiwiederherstellung  
  
     Bei einer *Onlinedateiwiederherstellung*bleibt die Datenbank online, wenn die Datenbank während einer Dateiwiederherstellung online ist. Dateigruppen, in denen eine Datei wiederhergestellt wird, sind während des Wiederherstellungsvorgangs jedoch offline. Sobald die Dateien einer Offlinedateigruppe wiederhergestellt sind, wird die Dateigruppe automatisch wieder online geschaltet.  
  
     Informationen zur Unterstützung von Onlinewiederherstellungen von Seiten und Dateien finden Sie unter [Von den SQL Server 2014-Editionen unterstützte Funktionen](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Weitere Informationen zur Onlinewiederherstellung finden Sie unter [Onlinewiederherstellung &#40;SQL Server&#41;](online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Wenn Sie die Datenbank für eine Dateiwiederherstellung offline schalten möchten, tun Sie dies vor dem Starten der Wiederherstellungssequenz, indem Sie die folgende [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) -Anweisung ausführen: ALTER DATABASE *Datenbankname* SET OFFLINE.  
  
  
  
##  <a name="Overview"></a> Wiederherstellen von beschädigten Dateien aus Dateisicherungen  
  
1.  Erstellen Sie vor dem Wiederherstellen von beschädigten Dateien nach Möglichkeit eine [Sicherung des Protokollfragments](tail-log-backups-sql-server.md).  
  
     Wenn das Protokoll beschädigt wurde, kann keine Sicherung des Protokollfragments erstellt werden, und Sie müssen die gesamte Datenbank wiederherstellen.  
  
     Informationen zum Sichern eines Transaktionsprotokolls finden Sie unter [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](transaction-log-backups-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Bei einer Offlinedateiwiederherstellung müssen Sie immer im Voraus eine Sicherung des Protokollfragments erstellen. Bei einer Onlinedateiwiederherstellung müssen Sie die Sicherung des Protokollfragments immer danach erstellen. Die Protokollsicherung ist erforderlich, um für die wiederherzustellenden Dateien einen mit der restlichen Datenbank konsistenten Status zu gewährleisten.  
  
2.  Stellen Sie jede beschädigte Datei von der letzten Dateisicherung dieser Datei wieder her.  
  
3.  Stellen Sie für jede wiederhergestellte Datei die letzte differenzielle Dateisicherung wieder her (falls vorhanden).  
  
4.  Stellen Sie Transaktionsprotokollsicherungen in der chronologischen Reihenfolge wieder her, beginnend mit der Sicherung für die älteste der wiederhergestellten Dateien bis hin zu der in Schritt 1 erstellen Sicherung des Protokollfragments.  
  
     Um eine Datenbank in einen konsistenten Status zu versetzen, müssen Sie die Transaktionsprotokollsicherungen wiederherstellen, die nach den Dateisicherungen erstellt wurden. Für die Transaktionsprotokollsicherungen kann schnell ein Rollforward ausgeführt werden, weil nur die Änderungen, die die wiederhergestellten Dateien betreffen, angewendet werden. Die Wiederherstellung einzelner Dateien ist der Wiederherstellung der gesamten Datenbank vorzuziehen, da nicht beschädigte Dateien dann nicht kopiert werden müssen und für diese Dateien auch kein Rollforward ausgeführt werden muss. Es muss jedoch trotzdem die gesamte Kette der Protokollsicherungen gelesen werden.  
  
5.  Stellen Sie die Datenbank wieder her.  
  
> [!NOTE]  
>  Mit Dateisicherungen kann der Status der Datenbank zu einem früheren Zeitpunkt wiederhergestellt werden. Dazu müssen Sie einen vollständigen Dateisicherungssatz wiederherstellen und anschließend die Transaktionsprotokollsicherungen in der chronologischen Reihenfolge wiederherstellen, um einen Zielpunkt zu erreichen, der nach dem Ende der letzten wiederhergestellten Dateisicherung liegt. Weitere Informationen zum Wiederherstellen eines zu einem bestimmten Zeitpunkt bestehenden Datenbankzustands finden Sie unter [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
## <a name="transact-sql-restore-sequence-for-an-offline-file-restore-full-recovery-model"></a>Transact-SQL-Wiederherstellungssequenz für die Offlinedateiwiederherstellung (vollständiges Wiederherstellungsmodell)  
 Ein Dateiwiederherstellungsszenario besteht aus einer einzigen Wiederherstellungssequenz, bei der die entsprechenden Daten kopiert werden, ein Rollforward ausgeführt wird und die Daten wiederhergestellt werden.  
  
 In diesem Abschnitt werden die grundlegenden [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) -Optionen für eine vollständige Dateiwiederherstellungssequenz erläutert. Hierfür unwichtige Syntax und Informationen werden ausgelassen.  
  
 Die folgende Beispielwiederherstellungssequenz zeigt eine Offlinewiederherstellung von zwei sekundären Dateien ( `A` und `B`) mit WITH NORECOVERY. Anschließend werden zwei Protokollsicherungen mit NORECOVERY angewendet, gefolgt von der Sicherung des Protokollfragments, die mit WITH RECOVERY wiederhergestellt wird.  
  
> [!NOTE]  
>  Die folgende Beispielwiederherstellungssequenz startet, indem sie die Datei offline schaltet und dann eine Sicherung des Protokollfragments erstellt.  
  
```  
--Take the file offline.  
ALTER DATABASE database_name MODIFY FILE SET OFFLINE;  
-- Back up the currently active transaction log.  
BACKUP LOG database_name  
   TO <tail_log_backup>  
   WITH NORECOVERY;  
GO   
-- Restore the files.  
RESTORE DATABASE database_name FILE=name   
   FROM <file_backup_of_file_A>   
   WITH NORECOVERY;  
RESTORE DATABASE database_name FILE=<name> ......  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
-- Restore the log backups.  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <tail_log_backup>   
   WITH RECOVERY;  
```  
  
## <a name="examples"></a>Beispiele  
  
-   [Beispiel: Onlinewiederherstellung einer Datei mit Lese-/Schreibzugriff &#40;vollständiges Wiederherstellungsmodell&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;vollständiges Wiederherstellungsmodell&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
-   [Beispiel: Offlinewiederherstellung der primären Dateigruppe und einer weiteren Dateigruppe &#40;vollständiges Wiederherstellungsmodell&#41;](example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So stellen Sie Dateien und Dateigruppen wieder her**  
  
-   [Wiederherstellen von Dateien an einem neuen Speicherort &#40;SQL Server&#41;](restore-files-to-a-new-location-sql-server.md)  
  
-   [Wiederherstellen von Dateien und Dateigruppen &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  

  
## <a name="see-also"></a>Weitere Informationen  
 [Sicherung und Wiederherstellung: Interoperabilität und Koexistenz &#40;SQL Server&#41;](backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Differenzielle Sicherungen &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Vollständige Dateisicherungen &#40;SQL Server&#41;](full-file-backups-sql-server.md)   
 [Übersicht über Sicherungen &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Vollständige Datenbankwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](complete-database-restores-simple-recovery-model.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
