---
title: Erstellen und Konfigurieren von Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], creating
ms.assetid: 7f89fab8-6ee2-4273-9de0-e594bfb9407f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9858638287876d31733035d1a6bb6d95705708f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "75228721"
---
# <a name="creation-and-configuration-of-availability-groups-sql-server"></a>Erstellung und Konfiguration von Verfügbarkeitsgruppen (SQL Server)
  Die Themen in diesem Abschnitt erklären, wie eine [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Implementierung auf Instanzen von [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] bereitgestellt wird, die sich auf unterschiedlichen WSFC-Knoten (Windows Server-Failoverclustering) innerhalb eines einzelnen WSFC-Failoverclusters befinden.  
  
 Es wird dringend empfohlen, dass Sie sich vor dem Erstellen der ersten Verfügbarkeitsgruppe mit den Informationen in den folgenden Themen vertraut machen:  
  
 [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
 In diesem Thema werden die erforderlichen Voraussetzungen, Einschränkungen und Empfehlungen für Computer, WSFC-Knoten, Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Verfügbarkeitsgruppen, Replikate und Datenbanken beschrieben. Das Thema enthält auch Informationen zu Sicherheitsaspekten.  
  
 [Die ersten Schritte mit AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
 Enthält Informationen zu den Schritten zum Konfigurieren einer Serverinstanz, Erstellen einer Verfügbarkeitsgruppe, Konfigurieren der Verfügbarkeitsgruppe für Clientverbindungen, Verwalten von Verfügbarkeitsgruppen und Überwachen von Verfügbarkeitsgruppen.  
  
 
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So konfigurieren Sie eine Serverinstanz für[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Erstellen Sie einen Datenbankspiegelungs-Endpunkt für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung (Transact-SQL)](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Ermöglicht einem Datenbankspiegelungs-Endpunkt die Verwendung von Zertifikaten für ausgehende Verbindungen &#40;Transact-SQL-&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
 **Erste Schritte bei der Konfiguration von AlwaysOn-Verfügbarkeitsgruppen**  
  
-   [Die ersten Schritte mit AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **So erstellen und konfigurieren Sie eine neue Verfügbarkeits Gruppe**  
  
-   [Verwenden des Assistenten für Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Erstellen einer Verfügbarkeits Gruppe &#40;Transact-SQL-&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Erstellen Sie eine Verfügbarkeits Gruppe &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Verwenden des Dialogfelds Neue Verfügbarkeitsgruppe &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Geben Sie die Endpunkt-URL beim Hinzufügen oder Ändern eines Verfügbarkeits Replikat &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Konfigurieren der flexiblen Failoverrichtlinie zum Steuern der Bedingungen für ein automatisches Failover (AlwaysOn-Verfügbarkeitsgruppen)](configure-flexible-automatic-failover-policy.md)  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Zugriffs auf ein Verfügbarkeitsreplikat &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Starten Sie die Daten Verschiebung auf einer sekundären AlwaysOn-Datenbank &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Verwaltung von Anmeldungen und Aufträgen für die Datenbanken einer Verfügbarkeits Gruppe &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **So beheben Sie Probleme**  
  
-   [Problembehandlung AlwaysOn-Verfügbarkeitsgruppen Konfiguration (SQL Server) gelöscht](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Problembehandlung bei einem fehlgeschlagenen Vorgang zum Hinzufügen einer Datei &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Gt**  
  
     [AlwaysON - HADRON-Lernreihe: Nutzung des Arbeitsthreadpools für HADRON-fähige Datenbanken](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn-Teamblogs: Der offizielle SQL Server AlwaysOn-Teamblog](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server-Technikblogs](https://blogs.msdn.com/b/psssql/)  
  
-   **Videos**  
  
     [Microsoft SQL Server Codename "Denali" AlwaysOn-Reihe, Teil 1: Einführung in die nächste Generation von Lösungen mit hoher Verfügbarkeit](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Codename "Denali" AlwaysOn-Reihe, Teil 2: Erstellen einer unternehmenswichtigen Lösung für hohe Verfügbarkeit mit AlwaysOn](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepaper**  
  
     [Microsoft SQL Server AlwaysOn-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft-Whitepaper für SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepaper SQL Server Kundenberatungs Teams](http://sqlcat.com/)  
  
## <a name="see-also"></a>Weitere Informationen  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Verwaltung einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [AlwaysOn-Richtlinien für Betriebsprobleme mit AlwaysOn-Verfügbarkeitsgruppen (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Überwachen von Verfügbarkeitsgruppen (SQL Server)](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn-Verfügbarkeitsgruppen: Interoperabilität (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)  
  
