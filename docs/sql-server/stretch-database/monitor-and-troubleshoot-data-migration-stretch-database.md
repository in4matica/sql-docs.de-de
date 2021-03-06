---
title: Überwachung und Problembehandlung bei der Datenmigration
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, monitoring
- monitoring Stretch Database
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: d204c7acfbd8598a7cbb66a41dcf89915fc711ef
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "73843777"
---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>Überwachen und Behandeln von Problemen der Datenmigration (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Wählen Sie **Aufgaben | Stretch | Überwachung** für eine Datenbank in SQL Server Management Studio aus, um die Datenmigration im Stretch Database-Monitor zu überwachen.  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>Prüfen des Status der Datenmigration in Stretch Database-Monitor  
 Wählen Sie **Aufgaben | Stretch | Überwachung** für eine Datenbank in SQL Server Management Studio aus, um Stretch Database-Monitor zu öffnen und die Datenmigration zu überwachen.  
  
-   Im oberen Bereich der Überwachung werden allgemeine Informationen über die SQL Server-Datenbank mit aktivierter Funktion Stretch-Datenbank und die Azure-Remotedatenbank angezeigt.  
  
-   Im unteren Bereich der Überwachung wird der Status der Datenmigration für jede Tabelle mit aktivierter Funktion Stretch-Datenbank in der Datenbank angezeigt.  
  
 ![Stretch-Database-Monitor](../../sql-server/stretch-database/media/stretch-monitor.PNG "Stretch-Database-Monitor")  
  
##  <a name="Migration"></a> Überprüfen des Status der Datenmigration in einer dynamischen Verwaltungsansicht  
 Öffnen Sie die dynamische Verwaltungssicht **sys.dm_db_rda_migration_status** , um anzuzeigen, wie viele Batches und Datenzeilen migriert wurden. Weitere Informationen finden Sie unter [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
##  <a name="Firewall"></a> Problembehandlung der Datenmigration  
 **Zeilen aus meiner Stretch-aktivierten Tabelle werden nicht zu Azure migriert. Wo liegt das Problem?**  
 Es gibt mehrere Probleme, die die Migration beeinflussen können. Überprüfen Sie folgende Aspekte.  
  
-   Überprüfen Sie die Netzwerkkonnektivität für den SQL Server-Computer.  
  
-   Stellen Sie sicher, dass die Azure Firewall Ihren SQL-Server nicht daran hindert, sich mit dem Remoteendpunkt zu verbinden.  
  
-   Überprüfen Sie die dynamische Verwaltungssicht **sys.dm_db_rda_migration_status** für den Status des aktuellen Batches. Wenn ein Fehler aufgetreten ist, überprüfen Sie die Werte „error_number“, „error_state“ und „error_severity“ für den Batch.  
  
    -   Weitere Informationen zu dieser Sicht finden Sie unter [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
    -   Weitere Informationen zum Inhalt einer SQL Server-Fehlermeldung finden Sie unter [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md).  
  
 **Die Azure Firewall blockiert Verbindungen von meinem lokalen Server.**  
 Möglicherweise müssen Sie eine Regel zu den Azure Firewall Einstellungen des Azure-Servers hinzufügen, damit SQL Server mit dem Azure-Remoteserver kommunizieren kann.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Verwalten von Stretch Database und Behandeln von Problemen](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  
