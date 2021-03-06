---
title: Verwenden von "Where"-und WHERE-Klauseln in derselben Abfrage (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- search conditions [SQL Server], HAVING clause
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- HAVING clause, search criteria
- search conditions [SQL Server], WHERE clause
- WHERE clause, search criteria
- excluding rows
ms.assetid: 1e07cf56-b4b7-4c49-8ddd-c276812a7148
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7aafcd72eff1d21dfe02c8957496398d327cf38
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204628"
---
# <a name="use-having-and-where-clauses-in-the-same-query-visual-database-tools"></a>Verwenden von HAVING- und WHERE-Klauseln in derselben Abfrage (Visual Database Tools)
  In einigen Fällen kann es sinnvoll sein, einzelne Zeilen aus Gruppen auszuschließen (mit einer WHERE-Klausel), bevor eine Bedingung auf Gruppen als Ganzes (mithilfe der HAVING-Klausel) angewendet wird.  
  
 Die HAVING-Klausel ähnelt der WHERE-Klausel, gilt jedoch nur für Gruppen als Ganzes (d. h. für die Zeilen im Resultset, die Gruppen darstellen), während die WHERE-Klausel auf einzelne Zeilen angewendet wird. Eine Abfrage kann sowohl eine WHERE-Klausel als auch eine HAVING-Klausel enthalten. Dabei trifft Folgendes zu:  
  
-   Zuerst wird die WHERE-Klausel auf die einzelnen Zeilen der Tabellen bzw. Objekte mit Tabellenwert im Diagrammbereich angewendet. Gruppiert werden nur die Zeilen, die die Bedingungen der WHERE-Klausel erfüllen.  
  
-   Die HAVING-Klausel wird dann im Resultset auf die Zeilen angewendet. Nur die Gruppen werden in das Abfrageergebnis aufgenommen, die die HAVING-Bedingungen erfüllen. Die HAVING-Klausel kann nur auf Spalten angewendet werden, die auch Teil einer GROUP BY-Klausel oder einer Aggregatfunktion sind.  
  
 Angenommen, Sie verknüpfen die Tabellen `titles` und `publishers` , um eine Abfrage zu erstellen, in der der durchschnittliche Buchpreis für eine Gruppe von Herstellern angezeigt wird. Der Durchschnittspreis soll jedoch nur für eine bestimmte Gruppe von Herausgebern angezeigt werden, beispielsweise nur für die Herausgeber in Kalifornien. Außerdem sollen nur Durchschnittspreise über 10,00 $ in der Ausgabe angezeigt werden.  
  
 Die erste Bedingung können Sie mithilfe einer WHERE-Klausel aufbauen, durch die Hersteller, die nicht aus Kalifornien stammen, vor der Berechnung der Durchschnittspreise verworfen werden. Die zweite Bedingung erfordert eine HAVING-Klausel, da sie auf den Ergebnissen einer Gruppierung und Zusammenfassung von Daten aufbaut. Die resultierende SQL-Anweisung könnte folgendermaßen aussehen:  
  
```  
SELECT titles.pub_id, AVG(titles.price)  
FROM titles INNER JOIN publishers  
   ON titles.pub_id = publishers.pub_id  
WHERE publishers.state = 'CA'  
GROUP BY titles.pub_id  
HAVING AVG(price) > 10  
```  
  
 Sie können im Kriterienbereich sowohl HAVING-Klauseln als auch WHERE-Klauseln erstellen. Wenn Sie eine Suchbedingung für eine Spalte angeben, wird diese Bedingung standardmäßig zu einem Bestandteil der HAVING-Klausel. Sie können die Bedingung jedoch auch in eine WHERE-Klausel ändern.  
  
 Für dieselbe Spalte kann sowohl eine WHERE-Klausel als auch eine HAVING-Klausel erstellt werden. Dazu müssen Sie die Spalte zunächst zweimal im Kriterienbereich einfügen und dann eine Instanz als Teil der HAVING-Klausel und die andere Instanz als Teil der WHERE-Klausel angeben.  
  
### <a name="to-specify-a-where-condition-in-an-aggregate-query"></a>So legen Sie eine WHERE-Bedingung in einer Aggregatabfrage fest  
  
1.  Geben Sie die Gruppen für die Abfrage an. Weitere Informationen finden Sie unter [Gruppieren von Zeilen in Abfrageergebnissen &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
2.  Fügen Sie dem Kriterienbereich die Spalte hinzu, auf der die WHERE-Bedingung basieren soll, sofern diese dort nicht bereits vorhanden ist.  
  
3.  Löschen Sie die Spalte **Ausgabe** , es sei denn, die Datenspalte ist in die GROUP BY-Klausel oder eine Aggregatfunktion eingebunden.  
  
4.  Geben Sie die WHERE-Bedingung in der Spalte **Filter** an. Der Abfrage- und Sicht-Designer fügt der HAVING-Klausel der SQL-Anweisung die Bedingung hinzu.  
  
    > [!NOTE]  
    >  In der im Beispiel für diese Prozedur dargestellten Abfrage werden die beiden Tabellen `titles` und `publishers`miteinander verknüpft.  
  
     An dieser Stelle der Abfrage enthält die SQL-Anweisung eine HAVING-Klausel:  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    GROUP BY titles.pub_id  
    HAVING publishers.state = 'CA'  
    ```  
  
5.  Wählen Sie in der Spalte **Gruppieren nach** aus der Liste von Gruppierungs- und Zusammenfassungsoptionen die Option **Where** aus. Der Abfrage- und Sicht-Designer entfernt die Bedingung aus der HAVING-Klausel in der SQL-Anweisung und fügt sie der WHERE-Klausel hinzu.  
  
     Daraufhin wird stattdessen eine WHERE-Klausel in die SQL-Anweisung eingebunden:  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    WHERE publishers.state = 'CA'  
    GROUP BY titles.pub_id  
    ```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Sortieren und Gruppieren von Abfrage Ergebnissen &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Zusammenfassen von Abfrageergebnissen &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)  
  
  
