---
title: Sichern und Wiederherstellen von DQS-Datenbanken | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3091f62-2234-4a80-a615-cf14c2a1da85
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 50b051cf2780fc1a94830c461d9ae30674bb7dad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481153"
---
# <a name="backing-up-and-restoring-dqs-databases"></a>Sichern und Wiederherstellen von DQS-Datenbanken
  In diesem Thema wird beschrieben, wie die DQS-Datenbanken gesichert und wiederhergestellt werden.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Voraussetzungen  
  
-   Sie müssen das Kennwort für den Datenbank-Hauptschlüssel kennen, das Sie während der DQS-Serverinstallation angegeben haben.  
  
-   Stellen Sie sicher, dass in DQS keine Aktivitäten oder Prozesse ausgeführt werden. Dies kann mithilfe des Bildschirms **Aktivitätsüberwachung** überprüft werden. Weitere Informationen zum Verwenden dieses Bildschirms finden Sie unter [Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md).  
  
-   Stellen Sie sicher, dass keine Benutzer am DQS-Server angemeldet sind.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Das Windows-Benutzerkonto muss ein Mitglied der festen sysadmin-Serverrolle in der SQL Server-Instanz sein, um die Sicherungs- und Wiederherstellungsvorgänge auszuführen.  
  
-   Sie müssen über die Rolle „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um ausgeführte Aktivitäten abzubrechen oder ausgeführte Prozesse in DQS anzuhalten.  
  
##  <a name="BackupRestore"></a>Sichern und Wiederherstellen von DQS-Datenbanken  
  
1.  Starten Sie Microsoft SQL Server Management Studio, und stellen Sie eine Verbindung mit der entsprechenden SQL Server-Instanz her.  
  
2.  Erweitern Sie im Objekt-Explorer den Knoten **Datenbanken** .  
  
3.  Sichern Sie die DQS_STAGING_DATA-Datenbank. Ausführliche Anweisungen zum Sichern einer SQL Server-Datenbank finden Sie unter [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
4.  Sichern Sie die DQS_PROJECTS-Datenbank.  
  
5.  Sichern Sie die DQS_MAIN-Datenbank.  
  
6.  Trennen Sie die Verbindung mit der aktuellen Instanz von SQL Server, und stellen Sie eine Verbindung mit der SQL Server-Instanz her, auf der Sie diese Datenbanken wiederherstellen möchten.  
  
7.  Stellen Sie die DQS_MAIN-Datenbank wieder her. Schritt-für-Schritt-Anweisungen zum Wiederherstellen einer SQL Server Datenbank finden Sie unter [Wiederherstellen einer Datenbanksicherung &#40;SQL Server Management Studio&#41;](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).  
  
8.  Stellen Sie die DQS_PROJECTS-Datenbank wieder her.  
  
9. Stellen Sie die DQS_STAGING_DATA-Datenbank wieder her.  
  
10. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Server, und klicken Sie dann auf **Neue Abfrage**.  
  
11. Kopieren Sie im Abfrage-Editor-Fenster die folgenden SQL-Anweisungen, * \<* und ersetzen Sie die Kenn Wort>durch das Kennwort, das Sie während der DQS-Installation für den Datenbank-Hauptschlüssel angegeben haben:  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    EXECUTE [internal_core].[RestoreDQDatabases] '<PASSWORD>'  
    GO  
  
    ```  
  
12. Drücken Sie F5, um die Anweisungen auszuführen. Überprüfen Sie im **Ergebnis** Bereich, ob die Anweisungen erfolgreich ausgeführt wurden.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Manage DQS Databases](../../2014/data-quality-services/manage-dqs-databases.md)  
  
  
