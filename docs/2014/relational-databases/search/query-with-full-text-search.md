---
title: Abfragen mit Volltextsuche | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
caps.latest.revision: 79
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 78351b4f710d84d6d8cb7f29d1de89d05ee763b8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229010"
---
# <a name="query-with-full-text-search"></a>Abfragen mit Volltextsuche
  Zum Definieren von Volltextsuchen verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Volltextabfragen Volltextprädikate (CONTAINS und FREETEXT) und -funktionen (CONTAINSTABLE und FREETEXTTABLE). Diese unterstützen eine umfangreiche [!INCLUDE[tsql](../../includes/tsql-md.md)] -Syntax, die eine Vielzahl verschiedener Abfrageausdrücke gestattet. Zum Schreiben von Volltextabfragen müssen Sie wissen, wie diese Prädikate und Funktionen verwendet werden.  
  
##  <a name="OV_ft_predicates"></a> Übersicht über die Volltext-Volltextprädikate (CONTAINS und FREETEXT)  
 Die Prädikate CONTAINS und FREETEXT geben den Wert TRUE oder FALSE zurück. Sie können nur verwendet werden, um Auswahlkriterien anzugeben, anhand ermittelt wird, ob eine angegebene Zeile mit der Volltextabfrage übereinstimmt. Übereinstimmende Zeilen werden im Resultset zurückgegeben. CONTAINS und FREETEXT werden in der WHERE-Klausel oder der HAVING-Klausel einer SELECT-Anweisung angegeben. Sie können mit beliebigen anderen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prädikaten kombiniert werden, wie z. B. LIKE und BETWEEN.  
  
> [!NOTE]  
>  Weitere Informationen zur Syntax und zu den Argumenten dieser Prädikate finden Sie unter [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql) und [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql).  
  
 Bei der Verwendung von CONTAINS oder FREETEXT können Sie entweder eine einzelne Spalte, eine Liste mit Spalten oder alle Spalten der Tabelle für die Suche auswählen. Optional können Sie die Sprache angeben, deren Ressourcen bei der Volltextabfrage für die Wörtertrennung, die Wortstammerkennung und Thesaurus-Suchen sowie die Entfernung von Füllwörtern verwendet werden.  
  
 CONTAINS und FREETEXT eignen sich jeweils für unterschiedliche Arten von Übereinstimmungen:  
  
-   Verwenden Sie CONTAINS (oder CONTAINSTABLE) für genaue oder ungenaue (Fuzzy-)Übereinstimmungen mit einzelnen Wörtern und Satzteilen, für innerhalb einer bestimmten Entfernung angrenzende Wörter sowie für gewichtete Übereinstimmungen. Wenn Sie CONTAINS verwenden, müssen Sie mindestens eine Suchbedingung festlegen, die den zu suchenden Text und die Bedingungen für Übereinstimmungen angibt.  
  
     Sie können logische Operation zwischen Suchbedingungen verwenden. Weitere Informationen finden Sie unter [Verwenden von booleschen Operatoren – AND, OR, AND NOT (in CONTAINS und CONTAINSTABLE)](#Using_Boolean_Operators)weiter unten im vorliegenden Thema.  
  
-   Verwenden Sie FREETEXT (oder FREETEXTTABLE), um nach der Bedeutung ohne exakte Übereinstimmungen des Wortlauts, nach angegebenen Wörtern, Ausdrücken oder Sätzen (sogenannten *Freitextzeichenfolgen*) zu suchen. Übereinstimmungen werden dann generiert, wenn ein Begriff oder eine Form eines Begriffs im Volltextindex einer angegebenen Spalte gefunden wird.  
  
 Sie können einen vierteiligen Namen im CONTAINS- oder FREETEXT-Prädikat zum Abfragen von volltextindizierten Spalten der Zieltabellen auf einem Verbindungsserver verwenden. Erstellen Sie zum Vorbereiten eines Remoteservers für den Empfang von Volltextabfragen einen Volltextindex für die Zieltabellen und -spalten auf dem Remoteserver, und fügen Sie anschließend den Remoteserver als Verbindungsserver hinzu.  
  
> [!NOTE]  
>  Volltextprädikate sind in der [OUTPUT-Klausel](/sql/t-sql/queries/output-clause-transact-sql) nicht zulässig, wenn der Kompatibilitätsgrad der Datenbank auf 100 festgelegt ist.  
  
 
  
### <a name="examples"></a>Beispiele  
  
#### <a name="a-using-contains-with-simpleterm"></a>A. Verwenden von CONTAINS mit <simple_term>  
 Im folgenden Beispiel werden alle Produkte mit einem Preis von `$80.99` gesucht, die das Wort `"Mountain"` enthalten.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
#### <a name="b-using-freetext-to-search-for-words-containing-specified-character-values"></a>B. Verwenden von FREETEXT, um nach Wörtern zu suchen, die bestimmte Zeichenwerte enthalten  
 Im folgenden Beispiel wird nach allen Dokumenten gesucht, die Wörter im Zusammenhang mit wichtigen Sicherheitskomponenten enthalten.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```  
  
 
  
##  <a name="OV_ft_functions_CONTAINSTABLE_FREETEXTTABLE"></a> Übersicht über die Volltextfunktionen (CONTAINSTABLE und FREETEXTTABLE)  
 Auf die Funktionen CONTAINSTABLE und FREETEXTTABLE wird wie auf einen herkömmlichen Tabellennamen in der FROM-Klausel einer SELECT-Anweisung verwiesen. Sie geben eine Tabelle mit null, einer oder mehreren Zeilen zurück, die die Volltextabfrage erfüllen. Die zurückgegebene Tabelle enthält nur Zeilen der Basistabelle, die die angegebenen Auswahlkriterien in der Volltextsuchbedingung der Funktion erfüllen.  
  
> [!NOTE]  
>  Weitere Informationen zur Syntax und zu den Argumenten dieser Funktionen finden Sie unter [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql) und [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql).  
  
 Abfragen, die eine dieser Funktionen verwenden, geben einen Relevanzrangfolgenwert (RANK) und einen Volltextschlüssel für jede Zeile Zurück, wie im Folgenden dargestellt:  
  
-   KEY-Spalte  
  
     Die KEY-Spalte gibt eindeutige Werte der zurückgegebenen Zeilen zurück. Die KEY-Spalte kann verwendet werden, um Auswahlkriterien anzugeben.  
  
-   RANK-Spalte  
  
     Die RANK-Spalte gibt einen *Rangwert* für jede Zeile zurück, der angibt, wie gut die Zeilen mit den Auswahlkriterien übereinstimmen. Je höher der Rangwert des Textes oder Dokuments in einer Zeile ist, desto relevanter ist die Zeile für die betreffende Volltextabfrage. Beachten Sie, dass unterschiedliche Zeilen denselben Rang haben können. Sie können die Anzahl zurückgegebener Übereinstimmungen mit dem optionalen Parameter *top_n_by_rank* einschränken. Weitere Informationen finden Sie unter [Einschränken von Suchergebnissen mit RANK](limit-search-results-with-rank.md).  
  
 Beim Verwenden dieser Funktionen müssen Sie die Basistabelle angeben, in der die Volltextsuche durchgeführt werden soll. Wie bei den Prädikaten können Sie eine einzelne Spalte, eine Liste mit Spalten oder alle Spalten in der Tabelle für die Suche auswählen. Außerdem kann optional die Sprache angegeben werden, deren Ressourcen bei der Volltextabfrage verwendet werden sollen.  
  
 CONTAINSTABLE ist für dieselben Arten von Übereinstimmungen geeignet wie CONTAINS, FREETEXTTABLE eignet sich entsprechend für dieselben Übereinstimmungen wie FREETEXT. Weitere Informationen finden Sie weiter oben im vorliegenden Thema unter [Übersicht der Volltextprädikate (CONTAINS und FREETEXT)](#OV_ft_predicates). Bei der Ausführung von Abfragen, die die Funktionen CONTAINSTABLE und FREETEXTTABLE verwenden, müssen Sie die zurückgegebenen Zeilen explizit mit den Zeilen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Basistabelle verknüpfen.  
  
 Normalerweise müssen die Ergebnisse von CONTAINSTABLE oder FREETEXTTABLE mit der Basistabelle verknüpft werden. In solchen Fällen müssen Sie den Namen der eindeutigen Schlüsselspalte kennen. Mit dieser Spalte, die in jeder volltextfähigen Tabelle enthalten ist, wird die Eindeutigkeit von Zeilen für die Tabelle erzwungen (die *UNIQUE**KEY-Spalte*). Weitere Informationen finden Sie unter [Verwalten von Volltextindizes](../indexes/indexes.md).  
  
 
  
### <a name="examples"></a>Beispiele  
  
#### <a name="a-using-containstable"></a>A. Verwenden von CONTAINSTABLE  
 Im folgenden Beispiel werden die Beschreibungs-ID und die Beschreibung aller Produkte zurückgegeben, bei denen in der Spalte **Description** das Wort „aluminum“ in der Nähe des Worts „light“ oder „lightweight“ enthalten ist. Ausschließlich Zeilen mit einem Rangwert von mindestens 2 werden zurückgegeben.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
#### <a name="b-using-freetexttable"></a>B. Verwenden von FREETEXTTABLE  
 Das folgende Beispiel erweitert eine FREETEXTTABLE-Abfrage so, dass die Zeilen mit dem höchsten Rangfolgenwert zuerst zurückgegeben werden und die Rangfolge jeder Zeile zur Auswahlliste hinzugefügt wird. Um die Abfrage angeben zu können, müssen Sie kennen, die **ProductDescriptionID** ist die eindeutige Schlüsselspalte der `ProductDescription` Tabelle.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 Im Folgenden finden Sie eine Erweiterung derselben Abfrage, die nur Zeilen mit einem Rangfolgenwert von 10 oder höher zurückgibt:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 
  
##  <a name="Using_Boolean_Operators"></a> Verwenden von booleschen Operatoren – AND, OR und NOT – in CONTAINS und CONTAINSTABLE  
 Das CONTAINS-Prädikat und die CONTAINSTABLE-Funktion verwenden dieselben Suchbedingungen. Beide unterstützen das Kombinieren mehrerer Suchbegriffe mit booleschen Operatoren – AND, OR, AND NOT –, um logische Operationen auszuführen. Mit AND können Sie z. B. Zeilen suchen, die sowohl "latte" als auch "Croissants" enthalten. Mit AND NOT können Sie z. B. Zeilen suchen, die zwar "Croissants", aber nicht "rustikal" enthalten.  
  
> [!NOTE]  
>  Im Gegensatz dazu behandeln FREETEXT und FREETEXTTABLE die booleschen Begriffe als Wörter, nach denen gesucht werden soll.  
  
 Informationen zum Kombinieren von CONTAINS mit anderen Prädikaten, die die logischen Operatoren AND, OR und NOT unterstützen, finden Sie unter [Suchbedingung &#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql).  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die ProductDescription-Tabelle der [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] -Datenbank verwendet. In der Abfrage wird das CONTAINS-Prädikat für die Suche nach Beschreibungen verwendet, deren Beschreibungs-ID ungleich 5 ist und die das Wort "Aluminum" und das Wort "spindle" enthalten. In der Suchbedingung wird der boolesche AND-Operator verwendet.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
 
  
##  <a name="Additional_Considerations"></a> Zusätzliche Überlegungen zu Volltextabfragen  
 Berücksichtigen Sie beim Schreiben von Volltextabfragen auch Folgendes:  
  
-   Die LANGUAGE-Option  
  
     Viele Abfrageausdrücke hängen sehr vom Verhalten bei Wörtertrennungen ab. Um sicherzustellen, dass Sie die richtige Wörtertrennung (und Wortstammerkennung) sowie die richtige Thesaurusdatei verwenden, wird empfohlen, die LANGUAGE-Option anzugeben. Weitere Informationen finden Sie unter [Auswählen einer Sprache beim Erstellen eines Volltextindex](choose-a-language-when-creating-a-full-text-index.md).  
  
-   Stoppwörter  
  
     Wenn Sie eine Volltextabfrage definieren, ignoriert die Volltext-Engine Stoppwörter (auch als Füllwörter bezeichnet) in den Suchkriterien. Stoppwörter sind Wörter wie Artikel ("ein" oder "der"), Konjunktionen ("und") oder Hilfsverben ("ist"), die häufig vorkommen können, jedoch bei der Suche nach bestimmtem Text nicht hilfreich sind. Stoppwörter werden in einer Stoppliste aufgelistet. Jedem Volltextindex ist eine bestimmte Stoppliste zugeordnet, die festlegt, welche Stoppwörter bei Abfragen oder im Index während der Indizierung ignoriert werden. Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](full-text-search.md).  
  
-   Der Thesaurus  
  
     FREETEXT- und FREETEXTTABLE-Abfragen verwenden standardmäßig den Thesaurus. CONTAINS und CONTAINSTABLE unterstützen ein optionales THESAURUS-Argument.  
  
-   Unterscheidung nach Groß-/Kleinschreibung  
  
     Bei Volltextabfragen wird nicht nach Groß- und Kleinschreibung unterschieden. Im Japanischen gibt es allerdings mehrere phonetische Orthografien, bei denen das Konzept der orthografischen Normalisierung ähnlich der Nichtunterscheidung nach Groß-/Kleinschreibung ist (z. B. kana = keine Unterscheidung). Diese Art orthografischer Normalisierung wird nicht unterstützt.  
  

  
##  <a name="varbinary"></a> Abfragen von varbinary(max)- und XML-Spalten  
 Wenn ein Volltextindex einer Spalte `varbinary(max)`, `varbinary` oder `xml` erstellt wird, kann die Spalte mit den Volltextprädikaten (CONTAINS und FREETEXT) und -funktionen (CONTAINSTABLE und FREETEXTTABLE) wie jede andere volltextindizierte Spalte durchsucht werden.  
  
> [!IMPORTANT]  
>  Die Volltextsuche funktioniert auch bei image-Spalten. Allerdings die `image` -Datentyp wird in einer zukünftigen Version von entfernt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vermeiden Sie die Verwendung dieses Datentyps bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen er aktuell verwendet wird. Verwenden der `varbinary(max)` Datentyp stattdessen.  
  
### <a name="varbinarymax-or-varbinary-data"></a>varbinary(max)- oder varbinary-Daten  
 Ein einzelnes `varbinary(max)` oder `varbinary` -Spalte können viele Dokumenttypen gespeichert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt jeden Dokumenttyp, für den ein Filter im Betriebssystem installiert und verfügbar ist. Der Dokumenttyp jedes Dokuments wird durch die Dateierweiterung des Dokuments identifiziert. Zum Beispiel verwendet die Volltextsuche für die Dateierweiterung .doc den Filter für Microsoft Word-Dokumente. Eine Liste der verfügbaren Dokumenttypen erhalten Sie, indem Sie die [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) -Katalogsicht abfragen.  
  
 Beachten Sie, dass die Volltext-Engine vorhandene Filter nutzen kann, die im Betriebssystem installiert sind. Bevor die Filter, Wörtertrennungen und Wortstammerkennungen des Betriebssystems verwendet werden können, müssen Sie diese in der Serverinstanz laden. Dies wird im Folgenden beschrieben:  
  
```  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
 Zum Erstellen eines Volltextindexes für eine `varbinary(max)`-Spalte benötigt die Volltext-Engine Zugriff auf die Dateierweiterungen der Dokumente in der `varbinary(max)`-Spalte. Diese Informationen müssen in einer Tabellenspalte, der so genannten Typspalte, gespeichert werden. Die Spalte muss der `varbinary(max)`-Spalte im Volltextindex zugeordnet sein. Beim Indizieren eines Dokuments verwendet die Volltext-Engine die Dateierweiterung in der Typspalte, um den richtigen Filter zu ermitteln.  
  
 
  
### <a name="xml-data"></a>xml-Daten  
 Ein `xml` -Datentypspalte werden ausschließlich XML-Dokumente und-Fragmente gespeichert. und nur der XML-Filter für die Dokumente verwendet wird. Ein Typspalte ist daher nicht erforderlich. Auf `xml` Spalten, die der Volltextindex den Inhalt der XML-Elemente indiziert, aber ignoriert die XML-Markups. Attributwerte werden volltextindiziert, sofern es sich nicht um numerische Werte handelt. Elementtags werden als Tokenbegrenzungen verwendet. Wohlgeformte XML- oder HTML-Dokumente und -Fragmente in mehreren Sprachen werden unterstützt.  
  
 Weitere Informationen zum Abfragen einer `xml` Spalte finden Sie unter [verwenden Volltextsuche mit XML-Spalten](../xml/use-full-text-search-with-xml-columns.md).  
  
 
  
##  <a name="supported"></a> Unterstützte Formen von Abfrageausdrücken  
 Dieses Thema enthält eine Zusammenfassung zur Unterstützung der einzelnen Abfrageformen durch die Volltextprädikate und Rowsetwertfunktionen.  
  
> [!NOTE]  
>  Für die Syntax eines angegebenen Abfrageausdrucks klicken Sie auf die entsprechenden Links in der Spalte **Unterstützt durch** der folgenden Tabelle.  
  
|Form des Abfrageausdrucks|Description|Unterstützt durch|  
|----------------------|-----------------|------------------|  
|Mindestens ein Wort oder Ausdruck (*einfacher Begriff*)|Bei der Volltextsuche handelt es sich bei einem Wort (oder einem *Token*) um eine Zeichenfolge, deren Grenzen gemäß den linguistischen Regeln der angegebenen Sprache von entsprechenden Wörtertrennungen identifiziert werden. Ein gültiger Ausdruck besteht aus mehreren Wörtern mit oder ohne Satzzeichen dazwischen.<br /><br /> So ist z. B. "croissant" ein Wort, während "café au lait" ein Ausdruck ist. Solche Wörter und Ausdrücke werden als einfache Begriffe bezeichnet.<br /><br /> Weitere Informationen finden Sie unter [Suchen nach einem bestimmten Wort oder Ausdruck (einfacher Begriff)](#Simple_Term)weiter unten in diesem Thema.|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) und [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) suchen nach einer genauen Entsprechung für den Ausdruck.<br /><br /> [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) und [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) teilen den Ausdruck in separate Wörter auf.|  
|Ein Wort oder Ausdruck, bei dem die Wörter mit dem angegebenen Text beginnen (*Präfixbegriff*)|Ein Präfixbegriff ist eine Zeichenfolge, die einem Wort vorangestellt ist, um ein abgeleitetes Wort oder eine Flexionsform zu erhalten.<br /><br /> Bei einem einzelnen Präfixbegriff sind alle Wörter, die mit dem angegebenen Ausdruck beginnen, Teil des Resultsets. Der Ausdruck "Auto*" ergibt also Übereinstimmungen mit "automatisch", "Automobil" usw.<br /><br /> Im Falle eines Ausdrucks wird jedes Wort innerhalb des Ausdrucks als Präfixbegriff interpretiert. Der Begriff „auto tran\*“ entspricht z. B. „automatic transmission“ und „automobile transducer“, aber nicht „automatic motor transmission“.<br /><br /> Weitere Informationen finden Sie unter [Durchführen von Präfixsuchen (Präfixbegriff)](#Prefix_Term)weiter unten in diesem Thema.|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) und [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|Flexionsformen eines bestimmten Worts (*Generierungsbegriff – Flexion*)|Bei den Flexionsformen handelt es sich um die verschiedenen Tempora und Konjugationen eines Verbs oder die Singular- und Pluralformen eines Substantivs. Gehen wir davon aus, dass Sie nach der Flexionsform des Worts "drive" suchen. Wenn mehrere Zeilen in der Tabelle die Wörter "drive", "drives", "drove", "driving" und "driven" enthalten, werden alle in das Resultset aufgenommen, da jedes dieser Wörter durch Flexion aus dem Wort "drive" generiert werden kann.<br /><br /> Weitere Informationen finden Sie unter [Suchen nach Flexionsformen eines bestimmten Worts (Generierungsbegriff)](#Inflectional_Generation_Term)weiter unten in diesem Thema.|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) und [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) suchen standardmäßig nach den Flexionsformen aller angegebenen Wörter.<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) und [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) unterstützen ein optionales INFLECTIONAL-Argument.|  
|Synonyme Formen eines bestimmten Worts (*Generierungsbegriff – Thesaurus*)|Ein Thesaurus definiert vom Benutzer angegebene Synonyme für Ausdrücke. Wird einem Thesaurus beispielsweise ein Eintrag "{car, automobile, truck, van}" hinzugefügt, können Sie nach der Thesaurusform des Worts "car" suchen. Alle Zeilen in der abgefragten Tabelle, die die Wörter "automobile", "truck", "van" oder "car" enthalten, finden sich im Resultset, weil jedes dieser Wörter zum Synonymerweiterungssatz gehört, der das Wort "car" enthält.<br /><br /> Informationen zur Struktur von Thesaurusdateien finden Sie unter [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](configure-and-manage-thesaurus-files-for-full-text-search.md).|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) und [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) verwenden standardmäßig den Thesaurus.<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) und [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) unterstützen ein optionales THESAURUS-Argument.|  
|Ein Wort oder Ausdruck in der Nähe eines anderen Worts oder Ausdrucks (*NEAR-Begriff*)|Ein NEAR-Begriff gibt Wörter oder Ausdrücke an, die zu einander nah sind. Sie können auch die maximale Anzahl von Nicht-Suchbegriffen angeben, die die ersten und letzten Suchbegriffe trennen. Außerdem können Sie in einer beliebigen Reihenfolge oder in der angegebenen Reihenfolge nach Wörtern oder Ausdrücken suchen.<br /><br /> Sie suchen beispielsweise die Zeilen, in denen das Wort "ice" sich in der Nähe des Worts "hockey" oder der Ausdruck "ice skating" sich in der Nähe des Ausdrucks "ice hockey" befindet.<br /><br /> Weitere Informationen finden Sie unter [Suchen von Wörtern in der Nähe eines anderen Worts mit NEAR](search-for-words-close-to-another-word-with-near.md).|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) und [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|Wörter oder Ausdrücke mit gewichteten Werten (*gewichteter Begriff*)|Ein Gewichtungswert gibt für jedes Wort und jeden Ausdruck in einer Gruppe von Wörtern und Ausdrücken den Grad der Bedeutung an. Der Gewichtungswert 0,0 ist der niedrigste, und 1,0 ist der höchste mögliche Wert.<br /><br /> Sie können beispielsweise in einer Abfrage, in der nach mehreren Begriffen gesucht wird, jedem Suchwort einen Gewichtungswert zuweisen, der dessen Bedeutung im Vergleich zu den anderen Wörtern in der Suchbedingung angibt. In den Ergebnissen für diesen Abfragetyp werden die relevantesten Zeilen zuerst zurückgegeben, entsprechend der relativen Gewichtung, die Sie den Suchwörtern zugewiesen haben. Das Resultset enthält Dokumente oder Zeilen mit beliebigen angegebenen Ausdrücken (bzw. dem umgebenden Inhalt). Einige Ergebnisse werden jedoch als relevanter bewertet, weil den einzelnen Suchausdrücken verschiedene Gewichtungswerte zugeordnet sind.<br /><br /> Weitere Informationen finden Sie unter [Suchen nach Wörtern oder Ausdrücken mit gewichteten Werten (gewichteter Begriff)](#Weighted_Term)weiter unten in diesem Thema.|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
  

  
###  <a name="Simple_Term"></a> Suche nach bestimmten Wort oder Ausdruck (einfacher Begriff)  
 Sie können in eine Tabelle mithilfe von [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)oder [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) nach einem bestimmten Ausdruck suchen. Angenommen, Sie suchen möchten die `ProductReview` -Tabelle in der [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] Datenbank nach allen Kommentaren zu einem Produkt mit dem Begriff "Learning Curve," können Sie das CONTAINS-Prädikat wie folgt verwenden:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 Die Suchbedingung, in diesem Fall "learning curve", kann sehr komplex sein und aus einem oder mehreren Begriffen bestehen.  
  
 
  
###  <a name="Prefix_Term"></a> Durchführen von Präfixsuchen (Präfixbegriff)  
 Sie können [CONTAINS](/sql/t-sql/queries/contains-transact-sql) oder [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) verwenden, um nach Wörtern oder Ausdrücken mit einem angegebenen Präfix zu suchen. Alle Einträge in der Spalte, die Text enthalten und mit dem angegebenen Präfix beginnen, werden zurückgegeben. So suchen Sie beispielsweise nach allen Zeilen die das Präfix `top`enthalten, z. B. `top``ple`, `top``ping`und `top`. Die Abfrage lautet folgendermaßen:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 Es werden alle Textstellen zurückgegeben, die mit dem Text vor dem Sternchen (*) übereinstimmen. Wenn der Text und das Sternchen nicht in doppelte Anführungszeichen eingeschlossen sind, wie in `CONTAINS (DESCRIPTION, 'top*')`, wird das Sternchen von der Volltextsuche nicht als Platzhalter betrachtet.  
  
 Ist der Präfixbegriff ein Ausdruck, wird jedes Token, das Teil des Ausdrucks ist, als gesonderter Präfixbegriff behandelt. Es werden alle Zeilen mit Wörtern, die mit den Präfixbegriffen beginnen, zurückgegeben. So werden z. B. mit dem Präfixbegriff „light bread*“ Zeilen mit dem Text „light breaded“, „lightly breaded“ oder „light bread“ gefunden, aber nicht „lightly toasted bread“.  
  
 
  
###  <a name="Inflectional_Generation_Term"></a> Suchen nach Flexionsformen eines bestimmten Worts (Generierungsbegriff)  
 Sie können mithilfe von [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)oder [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) nach allen unterschiedlichen Zeiten und Konjugationen eines Verbs oder sowohl die Singular- als auch die Pluralform eines Substantivs (Flexionssuche) bzw. nach Synonymen eines bestimmten Worts (Thesaurussuche) suchen.  
  
 Im folgenden Beispiel wird beispielsweise nach einer Form von "foot" ("foot", "feet" usw.) in der `Comments` -Spalte der `ProductReview` -Tabelle in der `AdventureWorks` -Datenbank gesucht.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
> [!NOTE]  
>  Die Volltextsuche verwendet Wortstammerkennungen, über die Sie die unterschiedlichen Zeiten und Konjugationen eines Verbs suchen oder sowohl die Singular- als auch die Pluralform eines Substantivs suchen können. Weitere Informationen zur Wortstammerkennung finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  

  
###  <a name="Weighted_Term"></a> Suchen nach Wörtern oder Ausdrücken mit gewichteten Werten (gewichteter Begriff)  
 Sie können [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) verwenden, um nach Wörtern oder Ausdrücken zu suchen und einen Gewichtungswert anzugeben. Die Gewichtung, gemessen als eine Zahl von 0,0 bis 1,0, gibt die Bedeutung für jedes Wort und jeden Ausdruck in einer Gruppe von Wörtern und Ausdrücken an. Der Gewichtungswert 0.0 ist der niedrigste, und 1.0 ist der höchste mögliche Wert.  
  
 Im folgenden Beispiel ist eine Abfrage dargestellt, die mithilfe von Gewichtungen nach allen Kundenadressen sucht, in denen Text, der mit der Zeichenfolge "Bay" beginnt, entweder "Street" oder "View" enthält. Die Zeilen, die mehrere der angegebenen Wörter enthalten, erhalten einen höheren Rang in den Ergebnissen.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*",   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 Ein gewichteter Begriff kann in Verbindung mit jedem einfachen Begriff, einem Präfixbegriff, einem Generierungsbegriff oder einem NEAR-Begriff verwendet werden.  
  

  
##  <a name="tokens"></a> Anzeigen des Tokenisierungsergebnis einer Wörtertrennung, Thesaurus und Stoppliste Kombination  
 Nachdem Sie eine entsprechende Kombination aus Wörtertrennung, Thesaurus und Stoppliste auf eine eingegebene Abfragezeichenfolge angewendet haben, können Sie das Ergebnis der Tokenisierung anzeigen, indem Sie die dynamische Verwaltungssicht **sys.dm_fts_parser** verwenden. Weitere Informationen finden Sie unter [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql).  
  
 
  
## <a name="see-also"></a>Siehe auch  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [Erstellen von Volltextsuchabfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)   
 [Verbessern der Leistung von Volltextabfragen](improve-the-performance-of-full-text-queries.md)  
  
  