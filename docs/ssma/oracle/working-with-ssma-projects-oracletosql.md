---
title: Arbeiten mit SSMA-Projekten (oracleto SQL) | Microsoft-Dokumentation
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: b96aba990231225516a7ba8ccf1523b91cb56c86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266364"
---
# <a name="working-with-ssma-projects-oracletosql"></a>Arbeiten mit SSMA-Projekten (OracleToSQL)
Wenn Sie Oracle-Daten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Banken zu migrieren möchten, erstellen Sie zunächst ein SSMA-Projekt. Das Projekt ist eine Datei, die die folgenden Informationen enthält:  
  
-   Metadaten zu den Oracle-Datenbanken, zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]denen Sie migrieren möchten.  
  
-   Metadaten zur Ziel Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die die migrierten Objekte und Daten empfängt.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Verbindungsinformationen.  
  
-   Projekteinstellungen.  
  
Wenn Sie ein Projekt öffnen, wird es von Oracle und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]getrennt. Auf diese Weise können Sie offline arbeiten. Weitere Informationen zum erneuten Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Verbindung mit finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40;oracleto SQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Überprüfen der Standard Projekteinstellungen  
SSMA enthält mehrere Einstellungen zum wandeln und Laden von Datenbankobjekten, zum Migrieren von Daten und zum Synchronisieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA mit Oracle und. Die Standardeinstellungen sind für viele Benutzer geeignet. Bevor Sie jedoch ein neues SSMA-Projekt erstellen, sollten Sie die Einstellungen überprüfen. Wenn Sie möchten, können Sie die Standardeinstellungen ändern, die für alle neuen Projekte verwendet werden.  
  
**So überprüfen Sie die Standard Projekteinstellungen**  
  
1.  Klicken Sie **im Menü Extras** auf **Standard Projekteinstellungen**.  
  
2.  Wählen Sie in der Dropdown Liste **Migrations Ziel Version** den Projekttyp aus, für den Einstellungen angezeigt oder geändert werden müssen, und klicken Sie dann auf die Registerkarte **Allgemein**  
  
3.  Klicken Sie im linken Bereich auf **Konvertierung**.  
  
4.  Überprüfen Sie im rechten Bereich die Einstellungen, und ändern Sie Sie nach Bedarf. Weitere Informationen zu diesen Einstellungen finden Sie unter [Project Settings &#40;Conversion&#41; &#40;oracleto SQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
5.  Wiederholen Sie die Schritte 1-3 für die Seiten Migration, Synchronisierung, Laden von System Objekten, GUI und Typzuordnung.  
  
    -   Informationen zu den Migrations Einstellungen finden Sie unter [Project Settings &#40;Migration&#41; &#40;oracleto SQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md).  
  
    -   Weitere Informationen zu Systemobjekt Einstellungen finden Sie unter [Projekteinstellungen&#40;Laden von System Objekten&#41; &#40;oracleto SQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md).  
  
    -   Informationen zu den Einstellungen für die Synchronisierung mit finden Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unter [Project Settings&#40;Synchronisierung&#41; &#40;oracleto SQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
    -   Informationen zu den GUI-Einstellungen finden Sie unter [Project Settings &#40;GUI&#41; &#40;oracleto SQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md).  
  
    -   Informationen zu den Einstellungen für die Datentyp Zuordnung finden Sie unter [Project Settings &#40;Type Mapping&#41; &#40;oracleto SQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="creating-new-projects"></a>Erstellen neuer Projekte  
Wenn Sie Daten aus Oracle-Daten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Banken zu migrieren möchten, müssen Sie zunächst ein Projekt erstellen.  
  
**So erstellen Sie ein Projekt**  
  
1.  Klicken Sie im Menü **Datei** auf **Neues Projekt**.  
  
    Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
2.  Geben Sie im Feld **Name** einen Namen für das Projekt ein.  
  
3.  Geben Sie im Feld **Speicherort** einen Ordner für das Projekt ein, oder wählen Sie einen Ordner aus, und klicken Sie dann auf **OK**.  
  
4.  Wählen Sie in der Dropdown Liste **Migration zu** die Version des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ziels aus, die für die Migration verwendet wird. Die verfügbaren Optionen sind:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL-Datenbank  
  
## <a name="customizing-project-settings"></a>Anpassen von Projekteinstellungen  
Zusätzlich zum Definieren von Standard Projekteinstellungen, die für alle neuen SSMA-Projekte gelten, können Sie die Einstellungen für jedes Projekt anpassen. Weitere Informationen finden Sie unter [Festlegen von Projektoptionen &#40;oracleto SQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
Wenn Sie Datentyp Zuordnungen zwischen Quell-und Ziel Datenbanken anpassen, können Sie Zuordnungen auf Projekt-, Datenbank-oder Objektebene definieren. Weitere Informationen finden Sie unter [Mapping von Oracle-und SQL Server-Datentypen &#40;oracletosql&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
## <a name="saving-projects"></a>Speichern von Projekten  
Wenn Sie ein Projekt speichern, behält SSMA die Projekteinstellungen und optional die Daten Bank Metadaten in der Projektdatei.  
  
**So speichern Sie ein Projekt**  
  
-   Klicken Sie im Menü **Datei** auf **Projekt speichern**.  
  
    Wenn sich Schemas im Projekt geändert haben oder nicht konvertiert wurden, werden Sie von SSMA aufgefordert, Metadaten zu laden und zu speichern. Wenn Sie Metadaten laden und speichern, können Sie offline arbeiten. Außerdem können Sie eine komplette Projektdatei an andere Personen senden, z. b. technische Supportmitarbeiter. Wenn Sie zum Speichern von Metadaten aufgefordert werden, gehen Sie wie folgt vor:  
  
    1.  Aktivieren Sie für jedes Schema, das den Status **fehlender Metadaten**anzeigt, das Kontrollkästchen neben dem Datenbanknamen.  
  
        Das Speichern von Metadaten kann einige Minuten dauern. Wenn Sie noch keine Metadaten speichern möchten, aktivieren Sie keine Kontrollkästchen.  
  
    2.  Klicken Sie auf die Schaltfläche **Speichern**.  
  
        SSMA analysiert die Oracle-Schemas und speichert die Metadaten in der Projektdatei.  
  
## <a name="opening-projects"></a>Öffnen von Projekten  
Wenn Sie ein Projekt öffnen, wird es von Oracle und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]getrennt. Auf diese Weise können Sie offline arbeiten. Laden Sie Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um Metadaten zu aktualisieren. Zum Migrieren von Daten müssen Sie erneut eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Oracle und herstellen.  
  
**So öffnen Sie ein Projekt**  
  
1.  Verwenden Sie eines der folgenden Verfahren:  
  
    -   Zeigen Sie im Menü **Datei** auf **zuletzt verwendete Projekte**, und klicken Sie dann auf das Projekt, das Sie öffnen möchten.  
  
    -   Wählen Sie im Menü **Datei** die Option **Projekt öffnen**aus, suchen Sie die Projektdatei. o2ssproj, wählen Sie die Datei aus, und klicken Sie dann auf **Öffnen**.  
  
2.  Um die Verbindung mit Oracle wiederherzustellen, klicken Sie im Menü **Datei** auf **Verbindung mit Oracle wieder**herstellen.  
  
3.  Um erneut eine Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mit herzustellen, klicken Sie im Menü **Datei** auf **Verbindung wiederherstellen, um SQL Server**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrations Vorgangs besteht darin, eine [Verbindung mit Oracle Database (oracleto SQL)](https://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)herzustellen.  
  
## <a name="see-also"></a>Weitere Informationen  
[Migrieren von Oracle-Datenbanken zu SQL Server &#40;oracleto SQL-&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Herstellen einer Verbindung mit Oracle Database &#40;oracleto SQL-&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[Herstellen einer Verbindung mit SQL Server &#40;oracleto SQL-&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
