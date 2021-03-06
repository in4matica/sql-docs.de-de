---
title: Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Server Instanz (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- cross-database queries [SQL Server]
- logins [SQL Server], recreating on another server instance
- triggers [SQL Server], DLL
- user-defined error messages [SQL Server]
- permissions [SQL Server], metadata access
- Full-Text Engine [SQL Server]
- metadata [SQL Server], databases available to other instances
- jobs [SQL Server Agent], recreating on another server instance
- failover [SQL Server], managing metadata
- event notifications [SQL Server], metadata
- database mirroring [SQL Server], metadata
- startup options [SQL Server]
- restoring [SQL Server], onto another server instance
- linked servers [SQL Server], metadata
- WMI Provider for Server Events, metadata
- attaching databases [SQL Server]
- log shipping [SQL Server], metadata
- encryption [SQL Server], metadata
- server configuration [SQL Server]
- distributed queries [SQL Server], metadata
- extended stored procedures [SQL Server], metadata
- credentials [SQL Server], metadata
- copying databases
ms.assetid: 5d98cf2a-9fc2-4610-be72-b422b8682681
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0b87c66eab08243a6339f1eb2bc1912e469f2b80
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "76929908"
---
# <a name="manage-metadata-when-making-a-database-available-on-another-server-instance-sql-server"></a>Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz (SQL Server)
  Dieses Thema ist in den folgenden Situationen relevant:  
  
-   Konfigurieren der Verfügbarkeitsreplikate einer [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] -Verfügbarkeitsgruppe.  
  
-   Einrichten der Datenbankspiegelung für eine Datenbank.  
  
-   Beim Vorbereiten einer Rollenänderung zwischen primären und sekundären Servern in einer Protokollversandkonfiguration.  
  
-   Wiederherstellen einer Datenbank auf einer anderen Serverinstanz.  
  
-   Anfügen einer Kopie einer Datenbank an eine andere Serverinstanz.  
  
 Einige Anwendungen sind von Informationen, Entitäten und/oder Objekten abhängig, die sich außerhalb des Bereichs einer einzelnen Benutzerdatenbank befinden. In der Regel weist eine Anwendung Abhängigkeiten von den Datenbanken **Master** und **msdb** sowie von der Benutzerdatenbank auf. Alle Daten, die außerhalb einer Benutzerdatenbank gespeichert werden und für die richtige Funktionsweise dieser Datenbank erforderlich sind, müssen auf der Zielserverinstanz bereitgestellt werden. Beispielsweise werden die Anmeldungen für eine Anwendung als Metadaten in der **Master** -Datenbank gespeichert und müssen auf dem Zielserver neu erstellt werden. Wenn ein Anwendungs- oder Datenbank-Wartungsplan von Aufträgen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents abhängig ist, deren Metadaten in der **msdb** -Datenbank gespeichert sind, müssen Sie diese Aufträge auf der Zielserverinstanz neu erstellen. Analog dazu werden die Metadaten für einen Server auf Serverebene in der **Master**-Datei gespeichert.  
  
 Wenn Sie die Datenbank für eine Anwendung auf eine andere Serverinstanz verschieben, müssen Sie alle Metadaten der abhängigen Entitäten und Objekte in **Master** und **msdb** auf der Zielserver Instanz neu erstellen. Wenn für eine Datenbankanwendung beispielsweise Trigger auf Serverebene verwendet werden, genügt es nicht, die Datenbank im neuen System lediglich anzufügen oder wiederherzustellen. Die Datenbank funktioniert nicht wie erwartet, es sei denn, Sie erstellen die Metadaten für diese Trigger in der **Master** -Datenbank manuell neu.  
  
##  <a name="information_entities_and_objects"></a>Informationen, Entitäten und Objekte, die außerhalb der Benutzer Datenbanken gespeichert werden  
 Im übrigen Teil dieses Themas werden die potenziellen Probleme zusammengefasst, die eine Datenbank betreffen können, die auf einer anderen Serverinstanz bereitgestellt werden soll. Möglicherweise müssen Sie einen oder mehrere Typen von Informationen, Entitäten oder Objekten neu erstellen, die in der folgenden Liste aufgeführt sind. Klicken Sie zum Anzeigen einer Zusammenfassung auf den Link für das Element.  
  
-   [Konfigurationseinstellungen für Server](#server_configuration_settings)  
  
-   [Anmeldeinformationen](#credentials)  
  
-   [Datenbankübergreifende Abfragen](#cross_database_queries)  
  
-   [Datenbankbesitz](#database_ownership)  
  
-   [Verteilte Abfragen/Verbindungs Server](#distributed_queries_and_linked_servers)  
  
-   [Verschlüsselte Daten](#encrypted_data)  
  
-   [Benutzerdefinierte Fehlermeldungen](#user_defined_error_messages)  
  
-   [Ereignis Benachrichtigungen und Windows-Verwaltungsinstrumentation (WMI)-Ereignisse (auf Serverebene)](#event_notif_and_wmi_events)  
  
-   [Erweiterte gespeicherte Prozeduren](#extended_stored_procedures)  
  
-   [Volltext-Engine für SQL Server Eigenschaften](#ifts_service_properties)  
  
-   [Aufträge](#jobs)  
  
-   [Anmeldungen](#logins)  
  
-   [Berechtigungen](#permissions)  
  
-   [Replikationseinstellungen](#replication_settings)  
  
-   [Service Broker Anwendungen](#sb_applications)  
  
-   [Start Prozeduren](#startup_procedures)  
  
-   [Trigger (auf Serverebene)](#triggers)  
  
##  <a name="server_configuration_settings"></a>Server Konfigurationseinstellungen  
 
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen werden wichtige Dienste und Funktionen selektiv installiert und gestartet. Auf diese Weise wird die angreifbare Oberfläche eines Systems verringert. Bei neuen Installationen sind viele Funktionen in der Standardkonfiguration nicht aktiviert. Wenn die Datenbank von einem standardmäßig deaktivierten Dienst oder Funktion abhängig ist, muss dieser Dienst bzw. diese Funktion auf der Zielserverinstanz aktiviert werden.  
  
 Weitere Informationen zu diesen Einstellungen sowie Informationen zum Aktivieren oder Deaktivieren dieser Einstellungen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="credentials"></a>Daten  
 Anmeldeinformationen sind in einem Datensatz gespeichert, in dem die Authentifizierungsinformationen enthalten sind, die zum Herstellen einer Verbindung mit einer Ressource außerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erforderlich sind. Die meisten Anmeldeinformationen bestehen aus einem Windows-Anmeldenamen und -Kennwort.  
  
 Weitere Informationen zu diesem Feature finden Sie unter [Anmeldeinformationen &#40;Datenbank-Engine&#41;](../security/authentication-access/credentials-database-engine.md).  
  
> [!NOTE]  
>  Für Proxykonten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents werden Anmeldeinformationen verwendet. Die ID der von einem Proxykonto verwendeten Anmeldeinformationen kann anhand der [sysproxies](/sql/relational-databases/system-tables/dbo-sysproxies-transact-sql) -Systemtabelle festgestellt werden.  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="cross_database_queries"></a>Datenbankübergreifende Abfragen  
 Die Datenbankoptionen DB_CHAINING und TRUSTWORTHY sind standardmäßig auf OFF festgelegt. Falls eine dieser Optionen für die ursprüngliche Datenbank auf ON festgelegt ist, müssen Sie die betreffende Option u. U. auch auf der Zielserverinstanz aktivieren. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
 Durch Anfüge- und Trennvorgänge wird die datenbankübergreifende Besitzverkettung für die Datenbank deaktiviert. Informationen zum Aktivieren der Verkettung finden Sie unter [Datenbankübergreifende Besitzverkettung (Serverkonfigurationsoption)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
 Weitere Informationen finden Sie auch unter [Einrichten der TRUSTWORTHY-Eigenschaft für eine Spiegeldatenbank &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md).  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="database_ownership"></a>Daten Bank Besitz  
 Wenn eine Datenbank auf einem anderen Computer wiederhergestellt wird, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename oder der Windows-Benutzer, der den Wiederherstellungsvorgang initiiert, automatisch zum Besitzer der neuen Datenbank. Nach dem Wiederherstellen der Datenbank kann der Systemadministrator oder der neue Datenbankbesitzer den Datenbankbesitz ändern.  
  
##  <a name="distributed_queries_and_linked_servers"></a>Verteilte Abfragen und Verbindungs Server  
 Verteilte Abfragen und Verbindungsserver werden für OLE DB-Anwendungen unterstützt. Verteilte Abfragen greifen auf Daten von mehreren heterogenen Datenquellen auf demselben oder auf unterschiedlichen Computern zu. Durch die Konfiguration von Verbindungsservern ist es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglich, Befehle für OLE DB-Datenquellen auf Remoteservern auszuführen. Weitere Informationen zu diesen Features finden Sie unter [Verbindungsserver &#40;Datenbank-Engine&#41;](../linked-servers/linked-servers-database-engine.md).  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="encrypted_data"></a>Verschlüsselte Daten  
 Wenn die Datenbank, die Sie auf einer anderen Serverinstanz verfügbar machen, verschlüsselte Daten enthält und wenn der Datenbank-Hauptschlüssel durch den Diensthauptschlüssel auf dem ursprünglichen Server geschützt wird, muss die Verschlüsselung des Diensthauptschlüssels u. U. neu erstellt werden. Der *Datenbank-Hauptschlüssel* ist ein symmetrischer Schlüssel, der zum Schützen von privaten Schlüsseln von Zertifikaten und asymmetrischen Schlüsseln in einer verschlüsselten Datenbank verwendet wird. Beim Erstellen wird der Datenbank-Hauptschlüssel mithilfe des Triple DES-Algorithmus und eines vom Benutzer angegebenen Kennworts verschlüsselt.  
  
 Um die automatische Entschlüsselung des Datenbank-Hauptschlüssels auf einer Serverinstanz zu ermöglichen, wird eine Kopie dieses Schlüssels mit dem Diensthauptschlüssel verschlüsselt. Diese verschlüsselte Kopie wird sowohl in der Datenbank als auch in der **master**-Datenbank gespeichert. In der Regel wird die in **Master** gespeicherte Kopie im Hintergrund aktualisiert, sobald der Hauptschlüssel geändert wird. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht zuerst, den Datenbank-Hauptschlüssel mit dem Diensthauptschlüssel der Instanz zu entschlüsseln. Wenn beim Entschlüsseln ein Fehler auftritt, wird der Anmeldeinformationsspeicher von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach Anmeldeinformationen des Hauptschlüssels durchsucht, die dieselbe Familien-GUID wie die Datenbank aufweisen, für die der Hauptschlüssel benötigt wird. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , den Datenbank-Hauptschlüssel mit allen übereinstimmenden Anmeldeinformationen zu entschlüsseln, bis die Entschlüsselung erfolgreich ausgeführt wurde oder keine Anmeldeinformationen mehr vorhanden sind. Ein Hauptschlüssel, der nicht mit dem Diensthauptschlüssel verschlüsselt ist, muss mithilfe der OPEN MASTER KEY-Anweisung und eines Kennworts geöffnet werden.  
  
 Wird eine verschlüsselte Datenbank auf eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kopiert, auf dieser wiederhergestellt oder an diese angefügt, wird keine Kopie des vom Diensthauptschlüssels verschlüsselten Datenbank-Hauptschlüssels in der **master** -Datenbank der Zielserverinstanz gespeichert. Auf der Zielserverinstanz müssen Sie den Hauptschlüssel der Datenbank öffnen. Führen Sie zum Öffnen des Hauptschlüssels die folgende Anweisung aus: OPEN MASTER KEY DECRYPTION BY PASSWORD **='***Kennwort***'**. Es empfiehlt sich, die automatische Entschlüsselung des Datenbank-Hauptschlüssels mit folgender Anweisung zu aktivieren: ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY. Durch diese ALTER MASTER KEY-Anweisung wird für die Serverinstanz eine Kopie des mit dem Diensthauptschlüssel verschlüsselten Datenbank-Hauptschlüssels bereitgestellt. Weitere Informationen finden Sie unter [OPEN MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-master-key-transact-sql) und [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql).  
  
 Informationen zum Aktivieren der automatischen Entschlüsselung des Datenbank-Hauptschlüssels einer Spiegeldatenbank finden Sie unter [Einrichten einer verschlüsselten Spiegeldatenbank](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md).  
  
 Weitere Informationen finden Sie auch unter:  
  
-   [Verschlüsselungshierarchie](../security/encryption/encryption-hierarchy.md)  
  
-   [Einrichten einer verschlüsselten Spiegeldatenbank](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
-   [Erstellen identischer symmetrischer Schlüssel auf zwei Servern](../security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="user_defined_error_messages"></a>Benutzerdefinierte Fehlermeldungen  
 Benutzerdefinierte Fehlermeldungen sind in der [sys.messages](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages) -Katalogsicht enthalten. Diese Katalogsicht wird in der **master**-Datenbank gespeichert. Wenn eine Datenbankanwendung benutzerdefinierte Fehlermeldungen verwenden muss und die Datenbank auf einer anderen Serverinstanz bereitgestellt wird, können Sie mit [sp_addmessage](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql) diese Fehlermeldungen auf der Zielserverinstanz hinzufügen.  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="event_notif_and_wmi_events"></a>Ereignis Benachrichtigungen und Windows-Verwaltungsinstrumentation (WMI)-Ereignisse (auf Server Ebene)  
  
### <a name="server-level-event-notifications"></a>Ereignisbenachrichtigungen auf Serverebene  
 Ereignisbenachrichtigungen auf Serverebene werden in **msdb**gespeichert. Wenn eine Datenbankanwendung von einer Ereignisbenachrichtigung auf Serverebene abhängt, muss diese Ereignisbenachrichtigung daher auf der Zielserverinstanz neu erstellt werden. Die Ereignisbenachrichtigungen auf einer Serverinstanz werden in der [sys.server_event_notifications](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql) -Katalogsicht angezeigt. Weitere Informationen finden Sie unter [Event Notifications](../service-broker/event-notifications.md).  
  
 Zudem werden Ereignisbenachrichtigungen mithilfe von [!INCLUDE[ssSB](../../includes/sssb-md.md)]übermittelt. Routen für eingehende Nachrichten sind in der Datenbank, die einen Dienst enthält, nicht eingeschlossen. Stattdessen werden explizite Routen in **msdb**gespeichert. Wenn Ihr Dienst eine explizite Route in der **msdb** -Datenbank verwendet, um eingehende Nachrichten an den Dienst weiterzuleiten, wenn Sie eine Datenbank in einer anderen Instanz anfügen, müssen Sie diese Route erneut erstellen.  
  
### <a name="windows-management-instrumentation-wmi-events"></a>WMI-Ereignisse (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation)  
 Über den WMI-Anbieter für Serverereignisse können Sie Ereignisse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mithilfe von WMI (Windows Management Instrumentation) überwachen. Jede Anwendung, die auf Ereignissen der Serverebene beruht, die über den WMI-Anbieter verfügbar gemacht werden, auf dem eine Datenbank beruht, muss für den Computer der Zielserverinstanz definiert werden. Der WMI-Ereignisanbieter erstellt Ereignisbenachrichtigungen mit einem Zieldienst, der in **msdb**definiert wird.  
  
> [!NOTE]  
>  Weitere Informationen finden Sie unter [Konzepte des WMI-Anbieters für Serverereignisse](../wmi-provider-server-events/wmi-provider-for-server-events-concepts.md).  
  
 **So erstellen Sie eine WMI-Warnung mithilfe von SQL Server Management Studio**  
  
-   [Erstellen einer WMI-Ereigniswarnung](../../ssms/agent/create-a-wmi-event-alert.md)  
  
### <a name="how-event-notifications-work-for-a-mirrored-database"></a>So funktionieren Ereignisbenachrichtigungen für eine gespiegelte Datenbank  
 Die datenbankübergreifende Übermittlung von Ereignisbenachrichtigungen, an der eine gespiegelte Datenbank beteiligt ist, erfolgt grundsätzlich remote, da für die gespiegelte Datenbank ein Failover auftreten kann. [!INCLUDE[ssSB](../../includes/sssb-md.md)]bietet besondere Unterstützung für gespiegelte Datenbanken in Form von *gespiegelten Routen*. Eine gespiegelte Route weist zwei Adressen auf: eine für die Prinzipalserverinstanz und eine für die Spiegelserverinstanz.  
  
 Durch das Einrichten gespiegelter Routen wird dem [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Routing die Datenbankspiegelung bewusst gemacht. Durch die gespiegelten Routen wird es [!INCLUDE[ssSB](../../includes/sssb-md.md)] ermöglicht, Konversationen mit der aktuellen Prinzipalserverinstanz transparent weiterzuleiten. Stellen Sie sich beispielsweise einen Dienst (Service_A) vor, der von einer gespiegelten Datenbank (Database_A) gehostet wird. Angenommen, Sie benötigen einen weiteren Dienst (Service_B), der von Database_B gehostet wird, sodass ein Dialog mit Service_A stattfinden kann. Damit dieser Dialog möglich ist, muss Database_B eine gespiegelte Route für Service_A enthalten. Zudem muss Database_A eine nicht gespiegelte TCP-Transportroute zu Service_B enthalten, die im Gegensatz zu einer lokalen Route nach einem Failover gültig bleibt. Mit diesen Routen können ACKs nach einem Failover wiederkehren. Da der Dienst des Absenders stets auf dieselbe Art und Weise benannt wird, muss mit der Route die Broker-Instanz angegeben werden.  
  
 Die Anforderung für gespiegelte Routen gilt unabhängig davon, ob der Dienst in der gespiegelten Datenbank den Initiatordienst darstellt oder den Zieldienst:  
  
-   Wenn sich der Zieldienst in der gespiegelten Datenbank befindet, muss der Initiatordienst eine gespiegelte Route zum Ziel zurück aufweisen. Das Ziel kann jedoch eine normale Route zurück zum Initiator besitzen.  
  
-   Wenn sich der Initiatordienst in der gespiegelten Datenbank befindet, muss der Zieldienst eine gespiegelte Route zum Initiator zurück aufweisen, damit Bestätigungen und Antworten übermittelt werden können. Der Initiator kann jedoch eine normale Route zum Ziel besitzen.  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="extended_stored_procedures"></a>Erweiterte gespeicherte Prozeduren  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwenden Sie stattdessen die [CLR-Integration](../clr-integration/common-language-runtime-integration-overview.md) .  
  
 Erweiterte gespeicherte Prozeduren werden mithilfe der API für erweiterte gespeicherte Prozeduren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programmiert. Mitglieder der festen Serverrolle **sysadmin** können eine erweiterte gespeicherte Prozedur bei einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registrieren und anderen Benutzern Berechtigungen zum Ausführen der Prozedur erteilen. Erweiterte gespeicherte Prozeduren können nur zur **master** -Datenbank hinzugefügt werden.  
  
 Erweiterte gespeicherte Prozeduren werden direkt im Adressraum einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt und können Arbeitsspeicherverluste oder andere Probleme hervorrufen, die die Leistung und Zuverlässigkeit des Servers reduzieren. Sie sollten in Betracht ziehen, erweiterte gespeicherte Prozeduren in einer anderen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als der Instanz zu speichern, die die Daten enthält, auf die verwiesen wird. Erwägen Sie auch die Verwendung von verteilten Abfragen für den Zugriff auf die Datenbank.  
  
> [!IMPORTANT]  
>  Systemadministratoren sollten, bevor sie dem Server erweiterte gespeicherte Prozeduren hinzufügen und Benutzern EXECUTE-Berechtigungen für die Prozedur erteilen, jede Prozedur gründlich überprüfen, um sicherzustellen, dass sie keinen schädlichen oder bösartigen Code enthält.  
  
 Weitere Informationen finden Sie unter [GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql), [DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-object-permissions-transact-sql) und [REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-object-permissions-transact-sql).  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="ifts_service_properties"></a>Volltext-Engine für SQL Server Eigenschaften  
 Die Eigenschaften für die Volltext-Engine werden mit [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)festgelegt. Stellen Sie sicher, dass die Zielserverinstanz die erforderlichen Einstellungen für diese Eigenschaften aufweist. Weitere Informationen zu diesen Eigenschaften finden Sie unter [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextserviceproperty-transact-sql).  
  
 Wenn die [Wörtertrennungs- und Wortstammerkennungs](../search/configure-and-manage-word-breakers-and-stemmers-for-search.md) -Komponente oder die [Filterkomponente](../search/configure-and-manage-filters-for-search.md) auf der ursprünglichen Serverinstanz und der Zielserverinstanz jeweils unterschiedliche Versionen haben, weisen die Volltextindizierung und die Volltextabfragen möglicherweise ein anderes Verhalten auf. Ebenso wird der [Thesaurus](../search/full-text-search.md) in instanzspezifischen Dateien gespeichert. Sie müssen entweder eine Kopie dieser Dateien in einen entsprechenden Speicherort auf der Zielserverinstanz übertragen oder die Dateien auf der neuen Instanz erneut erstellen.  
  
> [!NOTE]  
>  Wenn Sie eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank mit Volltextkatalogdateien an eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Serverinstanz anfügen, werden die Katalogdateien von ihrem vorherigen Speicherort aus zusammen mit den anderen Datenbankdateien angefügt. Dies entspricht der Vorgehensweise in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Weitere Informationen finden Sie unter [Upgrade der Volltextsuche](../search/upgrade-full-text-search.md).  
  
 Weitere Informationen finden Sie auch unter:  
  
-   [Sichern und Wiederherstellen von Volltextkatalogen und Indizes](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   [Daten Bank Spiegelung und voll Text Kataloge &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="jobs"></a>Tze  
 Wenn die Datenbank [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Aufträge verwendet, müssen Sie diese auf der Zielserverinstanz neu erstellen. Aufträge sind von der jeweiligen Umgebung abhängig. Wenn Sie vorhaben, einen vorhandenen Auftrag auf der Zielserverinstanz neu zu erstellen, müssen Sie die Zielserverinstanz ggf. so ändern, dass sie mit der Umgebung dieses Auftrags auf der ursprünglichen Serverinstanz übereinstimmt. Die folgenden Umgebungsfaktoren sind dabei von Bedeutung:  
  
-   Der vom Auftrag verwendete Anmeldename  
  
     Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Aufträge erstellen oder ausführen möchten, müssen Sie der Zielserverinstanz zuerst alle für den Auftrag erforderlichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen hinzufügen. Weitere Informationen finden Sie unter [Konfigurieren eines Benutzers zum Erstellen und Verwalten von SQL Server-Agent-Aufträgen](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md).  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst  
  
     Das Dienststartkonto definiert das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, in dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ausgeführt wird, und legt dessen Netzwerkberechtigungen fest. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent wird als angegebenes Benutzerkonto ausgeführt. Der Kontext des Agent-Diensts hat eine Auswirkung auf die Einstellungen für den Auftrag und dessen Ausführungsumgebung. Das Konto muss Zugriff auf die vom Auftrag benötigten Ressourcen haben, z. B. auf Netzwerkfreigaben. Informationen zum Auswählen und Ändern des Dienststartkontos finden Sie unter [Auswählen eines Kontos für den SQL Server-Agent-Dienst](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md).  
  
     Damit eine ordnungsgemäße Funktionsweise sichergestellt ist, muss das Dienststartkonto mit den richtigen Domänen-, Dateisystem- und Registrierungsberechtigungen konfiguriert sein. Ein Auftrag benötigt u. U. auch eine freigegebene Netzwerkressource, die für das Dienstkonto konfiguriert werden muss. Informationen finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst ist einer bestimmten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugeordnet und verfügt über eine eigene Registrierungsstruktur. Die Aufträge dieses Agents hängen in der Regel von einer oder mehreren Einstellungen in dieser Registrierungsstruktur ab. Das gewünschte Verhalten eines Auftrags ist nur dann sichergestellt, wenn diese Registrierungseinstellungen vorliegen. Wenn Sie einen Auftrag mithilfe eines Skripts in einem anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst neu erstellen, sind in dessen Registrierung möglicherweise nicht die richtigen Einstellungen für diesen Auftrag vorhanden. Damit sich die auf einer Zielserverinstanz neu erstellten Aufträge wie gewünscht verhalten, müssen der ursprüngliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst und der SQL Server-Agent-Zieldienst die gleichen Regstrierungseinstellungen aufweisen.  
  
    > [!CAUTION]  
    >  Das Ändern der Registrierungseinstellungen auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Zieldienst zum Verarbeiten eines neu erstellten Auftrags kann zu Problemen führen, wenn die aktuellen Einstellungen auch für andere Aufträge erforderlich sind. Ein fehlerhaftes Bearbeiten der Registrierung kann zudem eine schwerwiegende Beschädigung Ihres Systems zur Folge haben. Bevor Sie Änderungen an der Registrierung vornehmen, ist es empfehlenswert, alle wichtigen Daten zu sichern, die sich auf dem Computer befinden.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Proxys  
  
     Von einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Proxy wird der Sicherheitskontext für einen angegebenen Auftragsschritt definiert. Damit ein Auftrag auf der Zielserverinstanz ausgeführt werden kann, müssen alle dafür erforderlichen Proxys auf dieser Instanz manuell neu erstellt werden. Weitere Informationen finden Sie unter [Erstellen eines Proxys für den SQL Server-Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md) und [Problembehandlung von proxybasierten Multiserveraufträgen](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md).  
  
 Weitere Informationen finden Sie auch unter:  
  
-   [Implementieren von Aufträgen](../../ssms/agent/implement-jobs.md)  
  
-   [Verwaltung von Anmeldungen und Aufträgen nach einem Rollenwechsel &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md) (für die Daten Bank Spiegelung)  
  
-   [Konfigurieren von Windows-Dienst Konten und-Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) (beim Installieren einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Instanz von)  
  
-   [Konfigurieren von SQL Server-Agent](../../ssms/agent/sql-server-agent.md) (beim Installieren einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
  
-   [Implementieren der SQL Server-Agent-Sicherheit](../../ssms/agent/implement-sql-server-agent-security.md)  
  
 **So zeigen Sie vorhandene Aufträge und deren Eigenschaften an**  
  
-   [Überwachen der Auftragsaktivität](../../ssms/agent/monitor-job-activity.md)  
  
-   [sp_help_job &#40;Transact-SQL-&#41;](/sql/relational-databases/system-stored-procedures/sp-help-job-transact-sql)  
  
-   [View Job Step Information](../../ssms/agent/view-job-step-information.md)  
  
-   [dbo. sysjobs &#40;Transact-SQL-&#41;](/sql/relational-databases/system-tables/dbo-sysjobs-transact-sql)  
  
 **So erstellen Sie einen Auftrag**  
  
-   [Erstellen eines Auftrags](../../ssms/agent/create-a-job.md)  
  
-   [Erstellen eines Auftrags](../../ssms/agent/create-a-job.md)  
  
#### <a name="best-practices-for-using-a-script-to-re-create-a-job"></a>Bewährte Methoden zum erneuten Erstellen eines Auftrags mithilfe eines Skripts  
 Es wird empfohlen, zunächst ein Skript für einen einfachen Auftrag zu erstellen, den Auftrag für einen anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst neu zu erstellen und dann den Auftrag auszuführen, um zu sehen, ob er sich wie gewünscht verhält. Auf diese Weise können Sie Inkompatibilitäten feststellen und versuchen, diese zu lösen. Wenn ein durch Skript erstellter Auftrag in der neuen Umgebung nicht wie beabsichtigt ausgeführt wird, sollten Sie einen äquivalenten Auftrag erstellen, der in der betreffenden Umgebung ordnungsgemäß ausgeführt wird.  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="logins"></a>Anmeldungen  
 Für die Anmeldung bei einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename erforderlich. Dieser Anmeldename wird bei der Authentifizierung verwendet, die überprüft, ob der Prinzipal eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz herstellen kann. Ein Datenbankbenutzer, für den ein entsprechender [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename auf einer Serverinstanz nicht oder falsch definiert ist, kann sich bei der Instanz nicht anmelden. Diese Benutzer werden als *verwaiste Benutzer* der Datenbank dieser Serverinstanz bezeichnet. Ein Datenbankbenutzer kann zu einem verwaisten Benutzer werden, wenn die Datenbank auf einer anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz wiederhergestellt, an eine andere SQL Server-Instanz angefügt oder auf eine andere Instanz kopiert wird.  
  
 Zum Erstellen eines Skripts für einige oder für alle Objekte in der ursprünglichen Kopie der Datenbank können Sie den Assistenten zum Generieren von SQL Server-Skripts verwenden und im Dialogfeld **Skriptoptionen auswählen** die Option **Skripterstellung für Anmeldungen** auf **True**festlegen.  
  
> [!NOTE]  
>  Informationen zum Einrichten von Anmeldenamen für eine gespiegelte Datenbank finden Sie unter [Einrichten von Anmeldekonten für die Datenbankspiegelung oder AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md) und [Verwaltung von Anmeldenamen und Aufträgen nach einem Rollenwechsel &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md).  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="permissions"></a> Berechtigungen  
 Möglicherweise werden die folgenden Berechtigungstypen beeinflusst, wenn eine Datenbank auf einer anderen Serverinstanz verfügbar gemacht wird.  
  
-   GRANT-, REVOKE- oder DENY-Berechtigungen für Systemobjekte  
  
-   GRANT-, REVOKE- oder DENY-Berechtigungen für die Serverinstanz (*Berechtigungen auf Serverebene*)  
  
### <a name="grant-revoke-and-deny-permissions-on-system-objects"></a>GRANT-, REVOKE- und DENY-Berechtigungen für Systemobjekte  
 Berechtigungen für Systemobjekte wie z. B. gespeicherte Prozeduren, erweiterte gespeicherte Prozeduren, Funktionen und Sichten werden in der **master** -Datenbank gespeichert und müssen auf der Zielserverinstanz konfiguriert werden.  
  
 Zum Erstellen eines Skripts für einige oder für alle Objekte in der ursprünglichen Kopie der Datenbank können Sie den Assistenten zum Generieren von SQL Server-Skripts verwenden und im Dialogfeld **Skriptoptionen auswählen** die Option **Skripterstellung für Berechtigungen auf Objektebene** auf **True** festlegen.  
  
> [!IMPORTANT]  
>  Wenn Sie Skripts für Anmeldungen erstellen, werden keine Skripts für die Kennwörter erstellt. Bei Anmeldungen, die die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, müssen Sie das Skript auf dem Ziel ändern.  
  
 Systemobjekte werden in der [sys.system_objects](/sql/relational-databases/system-catalog-views/sys-system-objects-transact-sql) -Katalogsicht angezeigt. Die Berechtigungen für Systemobjekte werden in der [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) -Katalogsicht in der **master** -Datenbank angezeigt. Informationen zum Abfragen dieser Katalogsichten und zum Erteilen von Berechtigungen für Systemobjekte finden Sie unter [GRANT (Berechtigungen für Systemobjekte) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-system-object-permissions-transact-sql). Weitere Informationen finden Sie unter [REVOKE (Systemobjektberechtigungen) &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-system-object-permissions-transact-sql) und [DENY (Systemobjektberechtigungen) &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-system-object-permissions-transact-sql).  
  
### <a name="grant-revoke-and-deny-permissions-on-a-server-instance"></a>GRANT-, REVOKE- und DENY-Berechtigungen für eine Serverinstanz  
 Die Berechtigungen im Serverbereich werden in der **master** -Datenbank gespeichert und müssen auf der Zielserverinstanz konfiguriert werden. Informationen zu den Serverberechtigungen einer Serverinstanz erhalten Sie durch Abfragen der [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) -Katalogsicht, Informationen zu Serverprinzipalen erhalten Sie durch Abfragen der [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)-Katalogsicht, und Informationen zur Mitgliedschaft von Serverrollen erhalten Sie durch Abfragen der [sys.server_role_members](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql) -Katalogsicht.  
  
 Weitere Informationen finden Sie unter [GRANT (Serverberechtigungen) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-server-permissions-transact-sql), [REVOKE (Serverberechtigungen) &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-server-permissions-transact-sql) und [DENY (Serverberechtigungen) &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-server-permissions-transact-sql).  
  
#### <a name="server-level-permissions-for-a-certificate-or-asymmetric-key"></a>Berechtigungen auf Serverebene für ein Zertifikat oder einen asymmetrischen Schlüssel  
 Einem Zertifikat oder einem asymmetrischen Schlüssel können Berechtigungen auf Serverebene nicht direkt erteilt werden. Berechtigungen auf Serverebene werden stattdessen einem zugeordneten Anmeldenamen erteilt, der ausschließlich für ein bestimmtes Zertifikat oder einen bestimmten asymmetrischen Schlüssel erstellt wird. Jedes Zertifikat oder jeder asymmetrische Schlüssel, für das bzw. den Berechtigungen auf Serverebene erforderlich sind, benötigt daher einen eigenen dem *Zertifikat zugeordneten Anmeldenamen* bzw. einen eigenen dem *asymmetrischen Schlüssel zugeordneten Anmeldenamen*. Wenn Sie einem Zertifikat oder einem asymmetrischen Schlüssel Berechtigungen auf Serverebene erteilen möchten, müssen Sie die Berechtigungen dem jeweils zugeordneten Anmeldenamen erteilen.  
  
> [!NOTE]  
>  Ein zugeordneter Anmeldename wird nur für die Autorisierung von Code verwendet, der mit dem entsprechenden Zertifikat oder asymmetrischen Schlüssel signiert ist. Zugeordnete Anmeldenamen können nicht für Authentifizierungszwecke verwendet werden.  
  
 Der zugeordnete Anmeldename und dessen Berechtigungen werden in der **master**-Datenbank gespeichert. Zertifikate oder asymmetrische Schlüssel, die sich in einer anderen Datenbank als der **master**-Datenbank befinden, müssen in der **master** -Datenbank neu erstellt und einem Anmeldenamen zugeordnet werden. Wenn Sie die Datenbank auf eine andere Serverinstanz verschieben oder kopieren bzw. auf einer anderen Serverinstanz wiederherstellen, müssen Sie das zugehörige Zertifikat oder den zugehörigen asymmetrischen Schlüssel in der **master** -Datenbank der Zielserverinstanz neu erstellen, einem Anmeldenamen zuordnen und dem Anmeldenamen die erforderlichen Berechtigungen auf Serverebene erteilen.  
  
 **So erstellen Sie ein Zertifikat oder einen asymmetrischen Schlüssel**  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
 **So ordnen Sie einem Anmelde Namen ein Zertifikat oder einen asymmetrischen Schlüssel zu**  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
 **So weisen Sie dem zugeordneten Anmelde Namen Berechtigungen zu**  
  
-   [Erteilen von Server Berechtigungen &#40;Transact-SQL-&#41;](/sql/t-sql/statements/grant-server-permissions-transact-sql)  
  
 Weitere Informationen zu Zertifikaten und asymmetrischen Schlüsseln finden Sie unter [Encryption Hierarchy](../security/encryption/encryption-hierarchy.md).  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="replication_settings"></a>Replikationseinstellungen  
 Wenn Sie eine Sicherungskopie einer replizierten Datenbank auf einem anderen Server bzw. in einer anderen Datenbank wiederherstellen, können Replikationseinstellungen nicht beibehalten werden. In diesem Fall müssen nach der Wiederherstellung der Sicherungskopien sämtliche Veröffentlichungen und Abonnements neu erstellt werden. Um diesen Vorgang zu vereinfachen, können Sie für die aktuellen Replikationseinstellungen und auch für das Aktivieren und Deaktivieren der Replikation Skripts erstellen. Damit Sie diese Skripts beim Neuerstellen der Replikationseinstellungen verwenden können, kopieren Sie diese Skripts, und ändern Sie die Verweise auf die Servernamen passend für die Zielserverinstanz.  
  
 Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von replizierten Datenbanken](../replication/administration/back-up-and-restore-replicated-databases.md), [Datenbankspiegelung und Replikation &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md) und [Protokollversand und Replikation &#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="sb_applications"></a>Service Broker Anwendungen  
 Viele Aspekte einer [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Anwendung werden zusammen mit der Datenbank verschoben. Einige Aspekte der Anwendung müssen jedoch erneut erstellt oder am neuen Speicherort neu konfiguriert werden.  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="startup_procedures"></a>Start Prozeduren  
 Eine Autostartprozedur ist eine gespeicherte Prozedur, die für die automatische Ausführung markiert ist und bei jedem Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Wenn die Datenbank von irgendwelchen Autostartprozeduren abhängt, müssen Sie diese auf der Zielserverinstanz definieren und so konfigurieren, dass sie beim Start automatisch ausgeführt werden.  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
##  <a name="triggers"></a>Trigger (auf Server Ebene)  
 DDL-Trigger lösen gespeicherte Prozeduren als Reaktion auf verschiedene DDL-Ereignisse (Data Definition Language, Datendefinitionssprache) aus. Diese Ereignisse entsprechen in erster Linie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, die mit den Schlüsselwörtern CREATE, ALTER und DROP beginnen. Bestimmte gespeicherte Systemprozeduren, die DDL-ähnliche Vorgänge ausführen, können ebenfalls DDL-Trigger auslösen.  
  
 Informationen zu dieser Funktion finden Sie unter [DDL Triggers](../triggers/ddl-triggers.md).  
  
 [&#91;Anfang&#93;](#information_entities_and_objects)  
  
## <a name="see-also"></a>Weitere Informationen  
 [Eigenständige Datenbanken](contained-databases.md)   
 [Kopieren von Datenbanken auf andere Server](copy-databases-to-other-servers.md)   
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [Failover zu einem sekundären &#40;des Protokoll Versands SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)   
 [Rollenwechsel während einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Einrichten einer verschlüsselten Spiegeldatenbank](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [SQL Server-Konfigurations-Manager](../sql-server-configuration-manager.md)   
 [Problembehandlung bei verwaisten Benutzern &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
  
