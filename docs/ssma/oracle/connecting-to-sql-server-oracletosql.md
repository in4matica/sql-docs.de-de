---
title: Herstellen einer Verbindung mit SQL Server (oracleto SQL) | Microsoft-Dokumentation
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: cd8f0e57554f32d3b02a6e0e98d3a3645d683bac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266162"
---
# <a name="connecting-to-sql-server-oracletosql"></a>Herstellen einer Verbindung mit SQL Server (OracleToSQL)
Zum Migrieren von Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Banken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R2 oder 2012 oder 2014 müssen Sie eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dieser Ziel Instanzen von herstellen. Wenn Sie eine Verbindung herstellen, erhält SSMA Metadaten zu allen Datenbanken in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz von und zeigt Daten Bank [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Metadaten im Metadaten-Explorer an. SSMA speichert Informationen zu der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mit der Sie verbunden sind, speichert aber keine Kenn Wörter.  
  
Die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie erneut eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verbindung mit herstellen, wenn Sie eine aktive Verbindung mit dem Server herstellen möchten. Sie können offline arbeiten, bis Sie Datenbankobjekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in laden und Daten migrieren.  
  
Metadaten über die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden nicht automatisch synchronisiert. Stattdessen müssen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Metadaten manuell aktualisieren, um die Metadaten im metadatenexplorer zu aktualisieren. Weitere Informationen finden Sie im Abschnitt "Synchronisieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-sql-server-permissions"></a>Erforderliche SQL Server Berechtigungen  
Das Konto, das verwendet wird, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Verbindung mit herzustellen, erfordert abhängig von den Aktionen, die das Konto ausführt, unterschiedliche Berechtigungen:  
  
-   Das Konto muss über die [!INCLUDE[tsql](../../includes/tsql-md.md)] Berechtigung verfügen, sich bei der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anzumelden, um Oracle-Objekte in die-Syntax zu konvertieren, um Metadaten aus zu aktualisieren oder um konvertierte Syntax in Skripts zu speichern.  
  
-   Das Konto muss ein Mitglied [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]der **sysadmin** -Server Rolle sein, um Datenbankobjekte in laden zu können. Dies ist erforderlich, um CLR-Assemblys zu installieren.  
  
-   Zum Migrieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Daten zu muss das Konto Mitglied der **sysadmin** -Server Rolle sein. Dies ist erforderlich, um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Daten Migrations Pakete auszuführen.  
  
-   Um den von SSMA generierten Code auszuführen, muss das Konto über **Ausführungs** Berechtigungen für alle benutzerdefinierten Funktionen im **ssma_oracle** Schema der Zieldatenbank verfügen. Diese Funktionen bieten äquivalente Funktionalität von Oracle-Systemfunktionen und werden von konvertierten Objekten verwendet.  
  
Wenn das Konto, das zum Herstellen einer Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit verwendet wird, alle Migrations Aufgaben durchführen soll, muss das Konto Mitglied der **sysadmin** -Server Rolle sein.  
  
## <a name="establishing-a-sql-server-connection"></a>Einrichten einer SQL Server Verbindung  
Bevor Sie Oracle Database-Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die-Syntax konvertieren, müssen Sie eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz von herstellen, in der Sie die Oracle-Datenbank oder-Datenbanken migrieren möchten.  
  
Wenn Sie die Verbindungs Eigenschaften definieren, geben Sie auch die Datenbank an, in die Objekte und Daten migriert werden. Sie können diese Zuordnung auf der Oracle-Schema Ebene anpassen, nachdem Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eine Verbindung mit hergestellt haben. Weitere Informationen finden Sie unter [Mapping von Oracle-Schemas zu SQL Server Schemas &#40;oracleto SQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mit herzustellen, stellen Sie sicher, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dass die Instanz von ausgeführt wird und Verbindungen akzeptieren kann.  
  
**So stellen Sie eine Verbindung mit SQL Server her**  
  
1.  Wählen Sie im Menü **Datei** die Option **mit SQL Server verbinden**aus.  
  
    Wenn Sie zuvor eine Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mit hergestellt haben, wird der Befehls Name **erneut mit SQL Server**verbunden.  
  
2.  Geben Sie im Dialogfeld Verbindung den Namen der Instanz von ein, oder wählen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Sie ihn aus.  
  
    -   Wenn Sie eine Verbindung mit der Standard Instanz auf dem lokalen Computer herstellen, können Sie **localhost** oder einen Punkt (**.**) eingeben.  
  
    -   Wenn Sie eine Verbindung mit der Standard Instanz auf einem anderen Computer herstellen, geben Sie den Namen des Computers ein.  
  
    -   Wenn Sie eine Verbindung mit einer benannten Instanz auf einem anderen Computer herstellen, geben Sie den Computernamen gefolgt von einem umgekehrten Schrägstrich und dem Instanznamen ein, z. b. MyServer\MyInstance.  
  
3.  Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Annahme von Verbindungen an einem nicht standardmäßigen Port konfiguriert ist, geben Sie die Portnummer ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die im Feld **Serverport** für Verbindungen verwendet wird. Die Standard Portnummer für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die Standard Instanz von ist 1433. Bei benannten Instanzen wird von SSMA versucht, die Portnummer vom- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser Dienst abzurufen.  
  
4.  Geben Sie im Feld **Datenbank** den Namen der Zieldatenbank ein.  
  
    Diese Option ist nicht verfügbar, wenn Sie erneut eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Verbindung mit herstellen.  
  
5.  Wählen Sie im Feld **Authentifizierung** den Authentifizierungstyp aus, der für die Verbindung verwendet werden soll. Um das aktuelle Windows-Konto zu verwenden, wählen Sie **Windows-Authentifizierung**aus. Wählen Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Server Authentifizierung**aus, und geben Sie dann den Anmelde Namen und das Kennwort ein, um eine Anmeldung zu verwenden.  
  
6.  Für eine sichere Verbindung werden zwei-Steuerelemente hinzugefügt: die Kontrollkästchen **Verbindung verschlüsseln** und **TrustServerCertificate** . Nur wenn **Verbindung verschlüsseln** aktiviert ist, ist das Kontrollkästchen **TrustServerCertificate** sichtbar. Wenn **Verbindung verschlüsseln** (true) und **TrustServerCertificate** deaktiviert (false) ist, wird das SQL Server SSL-Zertifikat überprüft. Das Überprüfen des Serverzertifikats ist Teil des SSL-Handshakes und stellt sicher, dass es sich bei dem Server tatsächlich um den Server handelt, mit dem eine Verbindung hergestellt werden soll. Um dies zu gewährleisten, muss ein Zertifikat sowohl auf Clientseite als auch auf Serverseite installiert werden.  
  
7.  Klicken Sie auf **Verbinden**.  
  
**Höhere Versions Kompatibilität**  
  
-   Sie können eine Verbindung mit 2008 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 herstellen, wenn das erstellte Migrationsprojekt auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 festgelegt ist.  
  
-   Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können eine Verbindung mit 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 herstellen, wenn das erstellte Migrationsprojekt 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist, aber Sie können keine Verbindung mit niedrigeren Versionen herstellen, z. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] b. 2005.  
  
-   Sie können eine Verbindung mit 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 herstellen, wenn das erstellte Projekt SQL Server 2012 ist.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**Projekttyp und Ziel Server Version**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005<br /> (Version: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008<br /> (Version: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 <br />(Version: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />(Version: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version: 13. x)|Azure SQL-Datenbank|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005|Ja|Ja|Ja|Ja|Ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008||Ja|Ja|Ja|Ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012|||Ja|Ja|Ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Ja|Ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Ja||
|Azure SQL-Datenbank||||||Ja|
  
> [!IMPORTANT]
> Die Konvertierung der Datenbankobjekte erfolgt gemäß dem Projekttyp, jedoch nicht gemäß der Version von, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit der Sie verbunden sind. Im Fall von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 Project wird die Konvertierung gemäß [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 durchgeführt, obwohl eine Verbindung mit einer höheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016) besteht.  
  
## <a name="synchronizing-sql-server-metadata"></a>Synchronisieren von SQL Server-Metadaten  
Metadaten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbanken werden nicht automatisch aktualisiert. Bei den Metadaten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im metadatenexplorer handelt es sich um eine Momentaufnahme der Metadaten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], wenn Sie zum ersten Mal eine Verbindung mit hergestellt haben oder wenn Sie die Metadaten zuletzt manuell aktualisiert haben Sie können Metadaten für alle Datenbanken oder für eine einzelne Datenbank oder ein Datenbankobjekt manuell aktualisieren.  
  
**So synchronisieren Sie Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verbunden sind.  
  
2.  Aktivieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sie im metadatenexplorer das Kontrollkästchen neben der Datenbank oder dem Datenbankschema, das Sie aktualisieren möchten.  
  
    Wenn Sie z. b. die Metadaten für alle Datenbanken aktualisieren möchten, aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Datenbanken**oder die einzelne Datenbank oder das Datenbankschema, und wählen Sie dann **mit Datenbank synchronisieren**aus.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Projektanforderungen ab:  
  
-   Informationen zum Anpassen der Zuordnung zwischen Oracle-Schemas und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken und-Schemas finden Sie unter Mapping von Oracle- [Schemas zu SQL Server Schemas &#40;oracleto SQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
-   Informationen zum Anpassen der Konfigurationsoptionen für die Projekte finden Sie unter [Festlegen von Projektoptionen &#40;oracleto SQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
-   Informationen zum Anpassen der Zuordnung von Quell-und Ziel Datentypen finden Sie unter [Mapping von Oracle-und SQL Server-Datentypen &#40;oracletosql-&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   Wenn Sie diese Aufgaben nicht ausführen müssen, können Sie die Definitionen der Oracle-Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Objekt Definitionen konvertieren. Weitere Informationen finden Sie unter [umstellen von Oracle-Schemas &#40;oracleto SQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Weitere Informationen  
[Migrieren von Oracle-Datenbanken zu SQL Server &#40;oracleto SQL-&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
