---
title: Indizes und Schlüssel (Dialog Feld) (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65539
- vdt.ppg.indexeskeys
ms.assetid: 9e4060ba-80c3-468f-bccb-e12e99f672c2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0244530672e9db4a43f3dbe80f0c67cc86f8a67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63015416"
---
# <a name="indexes-and-keys-dialog-box-visual-database-tools"></a>Indizes und Schlüssel (Dialogfeld) (Visual Database Tools)
  Mit diesem Dialogfeld können Sie Indizes, Primärschlüssel und eindeutige Schlüssel erstellen oder ändern. Um auf das Dialogfeld zuzugreifen, öffnen Sie die Tabellendefinition für die Tabelle mit dem Index oder Schlüssel. Klicken Sie mit der rechten Maustaste auf das Tabellendefinitions-Datenblatt, und klicken Sie dann auf **Indizes/Schlüssel**.  
  
> [!NOTE]  
>  Wenn die Tabelle zur Replikation veröffentlicht ist, müssen Sie mit der Transact-SQL-Anweisung [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) oder mit SMO (SQL Server Management Objects) Schemaänderungen ausführen. Wenn die Schemaänderungen mit dem Tabellen-Designer oder dem Datenbankdiagramm-Designer ausgeführt werden, wird versucht, die Tabelle zu entfernen und erneut zu erstellen. Da veröffentlichte Objekte nicht gelöscht werden können, schlägt die Schemaänderung fehl.  
  
## <a name="options"></a>Tastatur  
 **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index**  
 Listet die vorhandenen Primärschlüssel, eindeutigen Schlüssel und Indizes auf. Wenn Sie einen Index oder Schlüssel auswählen, werden dessen Eigenschaften rechts im Datenblatt angezeigt. Falls die Liste leer ist, sind für die Tabelle Indizes definiert worden.  
  
 **Add (Hinzufügen)**  
 Erstellen Sie einen neuen Primärschlüssel, eindeutigen Schlüssel oder Index.  
  
 **Löschen**  
 Löschen Sie den in der Liste **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index** ausgewählten Schlüssel oder Index.  
  
 **Kategorie Allgemein**  
 Wenn diese Kategorie erweitert ist, werden die Eigenschaften **Spalten**, **Ist eindeutig**und **Typ**angezeigt.  
  
 **Spalten**  
 Listet die Sortierreihenfolgen auf, die für die im Schlüssel oder Index enthaltenen Spalten ausgewählt wurden, und bietet Zugriff auf ein Dialogfeld, in dem die Sortierreihenfolgen definiert werden können. Klicken Sie zum Anzeigen des Dialogfelds auf **Spalten**, und klicken Sie dann auf die Schaltfläche mit den Auslassungspunkten (...), die rechts neben dem Eigenschaftenfeld angezeigt wird.  
  
 **Ist eindeutig**  
 Gibt an, ob in diesen Index oder Schlüssel eingegebene Daten eindeutig sein müssen. Diese Einstellung ist für XML-Indizes nicht verfügbar.  
  
 **Typ**  
 Geben Sie an, ob es sich bei dem in der Liste **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index** ausgewählten Element um einen eindeutigen Schlüssel, einen Primärschlüssel oder einen Index handelt. Bei Primärschlüsseln ist dieses Feld schreibgeschützt.  
  
 **Kategorie Identität**  
 Wenn diese Kategorie erweitert ist, werden die Eigenschaftenfelder für **Name** und **Beschreibung**angezeigt.  
  
 **Name**  
 Zeigt den Namen des Schlüssels oder Indexes an. Wenn ein neuer Index erstellt wird, erhält dieser einen Standardnamen, der auf der Tabelle im aktiven Fenster des Tabellen-Designers basiert. Sie können den Namen jederzeit ändern.  
  
 **Beschreibung**  
 Ermöglicht die Eingabe einer Beschreibung des Schlüssels oder Index. Klicken Sie zum Erstellen einer detaillierteren Beschreibung auf **Beschreibung**, und klicken Sie dann rechts neben dem Eigenschaftenfeld auf die Schaltfläche mit den Auslassungspunkten (**...**). Dadurch wird ein größerer Bereich verfügbar, in den Sie Text eingeben können.  
  
 **Kategorie Tabellen-Designer**  
 Wenn diese Kategorie erweitert ist, werden Informationen zu **Als CLUSTERED erstellen**angezeigt.  
  
 **Als Clustered erstellen**  
 Erstellen Sie den Schlüssel oder Index als CLUSTERED. Pro Tabelle ist nur ein gruppierter Index zulässig. Die Daten in der Tabelle werden in der Reihenfolge des gruppierten Indexes gespeichert. Weitere Informationen finden Sie unter [Erstellen gruppierter Indizes](../../relational-databases/indexes/indexes.md) und [Erstellen nicht gruppierter Indizes](../../relational-databases/indexes/create-nonclustered-indexes.md).  
  
 **Angabe des Datenraums**  
 Wird dieses Element erweitert, werden Informationen für **(Datenbereichstyp)**, **Schemaname der Dateigruppe oder Partition**und **Partitionsspaltenliste**angezeigt.  
  
 **(Daten leertyp)**  
 Gibt an, ob dieser Index oder Schlüssel zu einer Dateigruppe oder einem Partitionsschema gehört.  
  
 **Schema Name der Datei Gruppe oder Partition**  
 Zeigt den Namen der Dateigruppe oder des Partitionsschemas an, zu dem er gespeichert wird.  
  
 **Partitions Spaltenliste**  
 Zeigt eine durch Trennzeichen getrennte Liste mit Spalten an, die an der Partitionsspaltenfunktion beteiligt sind. Ist nicht verfügbar, wenn im Feld **(Datenbereichstyp)** die Option „Dateigruppe“ ausgewählt ist.  
  
 **Füll Spezifikation**  
 Wenn dieses Element erweitert ist, werden Informationen für **Füllfaktor** und **Index mit Leerstellen auffüllen**angezeigt.  
  
 **Füllfaktor**  
 Gibt an, welcher Prozentsatz der Indexseiten auf Blattebene vom System ausgefüllt werden kann. Sobald eine Seite gefüllt ist, müssen beim Hinzufügen neuer Daten die Seiten vom System geteilt werden, wobei die Leistung beeinträchtigt wird.  
  
-   Ein Wert von 100 bedeutet, dass die Seiten gefüllt sind. Das erfordert die Mindestmenge des Speicherplatzes. Diese Einstellung sollte nur verwendet werden, wenn keine Änderungen an den Daten vorgenommen werden, zum Beispiel in einer schreibgeschützten Tabelle.  
  
-   Bei einem niedrigeren Wert bleiben mehr leere Bereiche auf den Datenseiten übrig. Dadurch wird die Notwendigkeit des Teilens von Datenseiten beim Vergrößern des Indexes verringert. Es ist dadurch aber mehr Speicherplatz erforderlich.  
  
 **Index Auffüllung**  
 Geben Sie an, ob für größer werdende Zwischenseiten in diesem Index der gleiche Prozentwert für leere Bereiche (Auffüllung) gilt, der unter **Füllfaktor** angegeben ist.  
  
 **Doppelte Schlüssel ignorieren**  
 Geben Sie an, was geschieht, wenn eine Zeile, deren Schlüsselwert mit einem vorhandenen Schlüsselwert identisch ist, im Rahmen eines Masseneinfügevorgangs eingefügt wird. Wenn Sie Folgendes auswählen:  
  
-   **Ja** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gibt eine Warnung aus, ignoriert die eingehende Zeile und versucht, die übrigen Zeilen einzufügen.  
  
-   **Nein** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gibt eine Fehlermeldung aus und führt einen Rollback für den gesamten BULK INSERT-Vorgang aus.  
  
 **Enthaltene Spalten**  
 Zeigt eine durch Trennzeichen getrennte Liste der Namen aller Spalten an, die den Indexschlüssel bilden. Unterschlüsselspalten können nur für nicht gruppierte Indizes angegeben werden. Diese Eigenschaft ist bei XML-Indizes ausgeblendet.  
  
 **Ist deaktiviert**  
 Gibt an, ob dieser Index deaktiviert ist. Dies ist eine schreibgeschützte Eigenschaft. Diese Eigenschaft ist nur dann auf **Ja** festgelegt, wenn der Index außerhalb von Visual Database Tools deaktiviert wurde.  
  
 **Ist voll Text Schlüssel**  
 Geben Sie an, ob der Index ein Volltextschlüssel ist. Weitere Informationen über Volltextschlüssel finden Sie in der SQL Server-Onlinedokumentation. Diese Eigenschaft ist bei XML-Indizes ausgeblendet.  
  
 **Seiten Sperren sind zulässig.**  
 Geben Sie an, ob Sperren auf Seitenebene für diesen Index zugelassen sind. Das Zulassen oder Untersagen von Sperren auf Seitenebene wirkt sich auf die Datenbankleistung aus. Die empfohlene Einstellung lautet **Ja**.  
  
 **Statistiken neu berechnen**  
 Geben Sie an, ob das zugrunde liegende [!INCLUDE[ssDE](../../includes/ssde-md.md)] neue Statistiken berechnet, wenn der Index erstellt wird. Durch das Neuberechnen der Statistiken wird das Erstellen der Indizes verlangsamt, die Abfrageleistung wird jedoch wahrscheinlich erhöht.  
  
 **Zeilen Sperren sind zulässig.**  
 Geben Sie an, ob das Sperren auf Zeilenebene für diesen Index zugelassen ist. Das Zulassen oder Untersagen von Sperren auf Zeilenebene wirkt sich auf die Datenbankleistung aus. Die empfohlene Einstellung lautet **Ja**.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Unique-Einschränkungen und Check-Einschränkungen](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Primärschlüssel- und Fremdschlüsseleinschränkungen](../../relational-databases/tables/primary-and-foreign-key-constraints.md)  
  
  
