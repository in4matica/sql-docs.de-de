---
title: Erstellen von Berichten (sybasedesql) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,generating reports
- Sybase Console,refresh-from-database report
- Sybase Console,synchronize-target report
ms.assetid: 19278f6a-6d58-4867-9d71-c6228040466e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a63ad1dad1a1dcab28e2a8ffb5c96d9564210475
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029136"
---
# <a name="generating-reports-sybasetosql"></a>Generieren von Berichten (SybaseToSQL)
Die Berichte bestimmter Aktivitäten, die mithilfe von Befehlen ausgeführt werden, werden in der SSMA-Konsole auf Objektstruktur Ebene generiert.  
  
Verwenden Sie das folgende Verfahren, um Berichte zu generieren:  
  
1.  Geben Sie den Parameter " **Write-Summary-Report-to" an** . Der zugehörige Bericht wird als Dateiname (sofern angegeben) oder in dem von Ihnen angegebenen Ordner gespeichert. Der Dateiname ist vom System vordefiniert, wie in der folgenden Tabelle ** &lt;erwähnt&gt; ** , wobei n die eindeutige Dateinummer ist, die bei jeder Ausführung desselben Befehls mit einer Ziffer schrittweise erhöht wird.  
  
    Die Berichte vis-a-vis-Befehle lauten:  
  
    ||||  
    |-|-|-|  
    |**SL. Nein.**|**Befehl**|**Berichtstitel**|  
    |1|generieren-Assessment-Bericht|Gutamentreport&lt;n&gt;. Basi|  
    |2|Convert-Schema|Schemaconversionreport&lt;n&gt;. Basi|  
    |3|Migrieren von Daten|Datamigrationreport&lt;n&gt;. Basi|  
    |4|Convert-SQL-Anweisung|Conversqlreport&lt;n&gt;. Basi|  
    |5|Synchronisieren-Ziel|Targetsynchronizationreport&lt;n&gt;. Basi|  
    |6|Refresh-from-Database|Sourcedbrefreshreport&lt;n&gt;. Basi|  
  
    > [!IMPORTANT]  
    > Ein Ausgabebericht unterscheidet sich vom Bewertungsbericht. Bei der ersten handelt es sich um einen Bericht zur Leistung eines ausgeführten Befehls, bei dem es sich um einen XML-Bericht für die programmgesteuerte Nutzung handelt.  
  
    Für die Befehlsoptionen für Ausgabe Berichte (von SL. Nein. 2-4 oben) lesen Sie den Abschnitt [Ausführen der SSMA-Konsole &#40;sybasedesql&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) .  
  
2.  Geben Sie den Umfang der im Ausgabebericht gewünschten Details mithilfe der berichtsausführlichkeits-Einstellungen an:  
  
    ||||  
    |-|-|-|  
    |**SL. Nein.**|**Befehl und Parameter**|**Ausgabe Beschreibung**|  
    |1|Verbose = "false"|Generiert einen zusammengefassten Bericht der Aktivität.|  
    |2|Verbose = "true"|Generiert einen zusammengefassten und detaillierten Statusbericht für jede Aktivität.|  
  
    > [!NOTE]  
    > Die oben angegebenen berichtsausführlichkeits-Einstellungen gelten für die Befehle Generate-Assessment-Report, Convert-Schema, Migration-Data, Convert-SQL-Statement.  
  
3.  Geben Sie den Umfang der von Ihnen gewünschten Details in den Fehlerberichten mithilfe der Einstellungen für die Fehlerberichterstattung an:  
  
    ||||  
    |-|-|-|  
    |**SL. Nein.**|**Befehl und Parameter**|**Ausgabe Beschreibung**|  
    |1|Report-Errors = "false"|Keine Details zu Fehler-/Warnungs-/Information-Meldungen.|  
    |2|Report-Errors = "true"|Ausführliche Fehler-/Warnungs-/Information-Meldungen.|  
  
    > [!NOTE]  
    > Die oben angegebenen Einstellungen für die Fehlerberichterstattung gelten für die Befehle "Generate-Assessment-Report", "Convert-Schema", "Migration-Data" und "Convert-SQL-Statement".  
  
```xml  
<generate-assessment-report  
  
    object-name="<object-name>"  
  
    object-type="<object-type>"  
  
    verbose="<true/false>"  
  
    report-erors="<true/false>"  
  
    write-summary-report-to="<file-name/folder-name>"  
  
    assessment-report-folder="<folder-name>"  
  
    assessment-report-overwrite="<true/false>"  
  
/>  
```  
  
### <a name="synchronize-target"></a>Synchronisieren-Ziel:  
Der Befehl " **Synchronisieren-Target** " weist einen **Report-Errors-to-Parameter auf** , der den Speicherort des Fehlerberichts für den Synchronisierungs Vorgang angibt. Anschließend wird eine Datei namens **targetsynchronizationreport&lt;&gt;n angezeigt. XML** wird an der angegebenen Position erstellt, wobei ** &lt;n&gt; ** die eindeutige Dateinummer ist, die mit jeder Ausführung desselben Befehls mit einer Ziffer Inkrementen erhöht.  
  
**Hinweis:** Wenn der Ordner Pfad angegeben ist, wird der Parameter "Report-Errors-to" ein optionales Attribut für den Befehl "Synchronisieren-Ziel".  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="<object-name>"  
  
    on-error="<object-type>"  
  
    report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**Objektname:** Gibt die für die Synchronisierung berücksichtigten Objekte an (Sie kann auch individuellen-Objektnamen oder einen Gruppen Objektnamen aufweisen).  
  
**bei Fehler:** Gibt an, ob Synchronisierungs Fehler als Warnungen oder Fehler angegeben werden sollen. Verfügbare Optionen für "bei Fehler":  
  
-   Bericht-gesamt-als-Warnung  
  
-   Bericht-jeder-als-Warnung  
  
-   Fehler-Skript  
  
### <a name="refresh-from-database"></a>Refresh-from-Database:  
Der Befehl **Refresh-from-Database** weist einen **Report-Errors-to-Parameter auf** , der den Speicherort des Fehlerberichts für den Aktualisierungs Vorgang angibt. Anschließend wird eine Datei namens **&lt;sourcedbrefreshreport&gt;n angezeigt. XML** wird an der angegebenen Position erstellt, wobei ** &lt;n&gt; ** die eindeutige Dateinummer ist, die mit jeder Ausführung desselben Befehls mit einer Ziffer Inkrementen erhöht.  
  
**Hinweis:** Wenn der Ordner Pfad angegeben ist, wird der Parameter "Report-Errors-to" ein optionales Attribut für den Befehl "Synchronisieren-Ziel".  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="<object-name>"  
  
    object-type ="<object-type>"  
  
    on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
    report-errors-to="<file-name/folder-name> "  
  
/>  
```  
**Objektname:** Gibt die Objekte an, die für die Aktualisierung berücksichtigt werden (Sie können auch individuellen-Objektnamen oder ein Gruppen Objektname aufweisen).  
  
**bei Fehler:** Gibt an, ob Aktualisierungs Fehler als Warnungen oder Fehler angegeben werden sollen. Verfügbare Optionen für "bei Fehler":  
  
-   Bericht-gesamt-als-Warnung  
  
-   Bericht-jeder-als-Warnung  
  
-   Fehler-Skript  
  
## <a name="see-also"></a>Weitere Informationen  
[Ausführen der SSMA-Konsole (Sybase)](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
