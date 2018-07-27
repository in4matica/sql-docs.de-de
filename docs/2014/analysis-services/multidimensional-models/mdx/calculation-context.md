---
title: Berechnungskontext | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aec8aa98-b77d-4f8f-9684-2618b1d8e970
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 854e53962dcc1b206d20b441b56b7746650aaf94
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202140"
---
# <a name="calculation-context"></a>Berechnungskontext
  Als Berechnungskontext wird der bekannte Teilbereich des Cubes bezeichnet, in dem ein Ausdruck ausgewertet wird und in dem alle Koordinaten entweder explizit bekannt sind oder vom Ausdruck abgeleitet werden können.  
  
## <a name="determining-the-calculation-context"></a>Bestimmen des Berechnungskontexts  
 Alle Mengen, Elemente, Tupel und numerischen Funktionen werden im Kontext des gesamten MDX-Ausdrucks bzw. der gesamten MDX-Anweisung ausgeführt. Beim Übergeben eines Arguments, z. B. eines Tupels, an eine Funktion werden nur einige Koordinaten im Cuberaum explizit bereitgestellt. Die anderen Koordinaten werden basierend auf dem aktuellen Berechnungskontext ermittelt.  
  
 Der Berechnungskontext für nicht angegebene Zellenkoordinaten und Attributelemente wird in der folgenden Reihenfolge bestimmt:  
  
1.  Die FROM-Klausel (ggf.) – Diese Klausel kann entweder einen gesamten Cube oder einen Teilcube in Form einer SELECT-Anweisung angeben.  
  
2.  Die WHERE-Klausel (ggf.) – Über diese Klausel, die auch *Slicerachse*genannt wird, werden Mengen, Tupel oder Elemente angegeben, die die von der Abfrage zurückgegebenen Elemente auf der Spalten- und Zeilenachse einschränken. Prinzipiell sind die Standardelemente aller Attributhierarchien, die nicht explizit auf der Spalten- oder Zeilenachse angegeben werden, Teil der Slicerachse.  
  
    > [!NOTE]  
    >  Wenn Zellenkoordinaten für ein bestimmtes Attribut sowohl auf der Slicerachse als auch auf einer weiteren Achse angegeben sind, werden die in der Funktion angegebenen Koordinaten möglicherweise vorrangig zur Bestimmung der Elemente der Menge auf der Achse verwendet. Die Funktionen [Filter (MDX)](/sql/mdx/filter-mdx) und [Order (MDX)](/sql/mdx/order-mdx) sind Beispiele für solche Funktionen – Sie können ein Ergebnis nach Attributelementen filtern oder sortieren, die von der WHERE-Klausel oder der SELECT-Anweisung in der FROM-Klausel aus dem Berechnungskontext ausgeschlossen sind.  
  
3.  Die in der Abfrage oder im Ausdruck definierten benannten Mengen und berechneten Elemente  
  
4.  Die auf der Zeilen- und Spaltenachse angegebenen Tupel und Mengen, die die Standardelemente der Attribute verwenden, die nicht auf der Zeilen-, Spalten oder Slicerachse angezeigt werden  
  
5.  Die Cube- oder die Teilcubezellen auf jeder Achse unter Entfernung leerer Tupel von der Achse und Anwendung der HAVING-Klausel  
  
6.  Weitere Informationen finden Sie unter [Establishing Cube Context in a Query &#40;MDX&#41;](establishing-cube-context-in-a-query-mdx.md).  
  
 In der folgenden Abfrage ist der Berechnungskontext für die Zeilenachse durch die in der WHERE-Klausel angegebenen Attributelemente Country und Calendar Year eingeschränkt.  
  
```  
SELECT Customer.City.City.Members ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France, [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 Wenn Sie jedoch diese Abfrage ändern, indem Sie die `FILTER`-Funktion auf der Zeilenachse angeben und ein Element der Calendar Year-Attributhierarchie in der `FILTER`-Funktion verwenden, kann das Attributelement der Calendar Year-Attributhierarchie, das zum Bereitstellen des Berechnungskontexts für die Elemente der Menge auf der Spaltenachse verwendet wird, geändert werden.  
  
```  
SELECT FILTER  
   (  
      Customer.City.City.Members,   
         ([Date].[Calendar].[Calendar Year].[CY 2003],  
            Measures.[Internet Order Quantity]) > 75   
   ) ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France,  
   [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 In der vorherigen Abfrage wird der Berechnungskontext für die Zellen in den Tupeln, die auf der Spaltenachse angezeigt werden, vom CY 2003-Element der Calendar Year-Attributhierarchie gefiltert, auch wenn CY 2004 der nominelle Berechnungskontext für die Calendar Year-Attributhierarchie ist. Es wird weiterhin nach dem Measure Internetbestellmenge gefiltert. Sobald jedoch die Elemente der Menge auf der Spaltenachse festgelegt sind, wird der Berechnungskontext für die Werte der Elemente, die auf der Achse angezeigt werden, wieder über die WHERE-Klausel bestimmt.  
  
> [!IMPORTANT]  
>  Zur Verbesserung der Abfrageleistung sollten Elemente und Tupel beim Auflösungsvorgang so früh wie möglich entfernt werden. Auf diese Weise werden komplexe Abfragezeitberechnungen für die endgültige Menge der Elemente mit minimaler Zellenanzahl durchgeführt.  
  
## <a name="see-also"></a>Siehe auch  
 [Des Cubekontexts in einer Abfrage &#40;MDX&#41;](establishing-cube-context-in-a-query-mdx.md)   
 [Grundlegendes zu MDX-Abfrage &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)   
 [Grundlegende Konzepte in MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)  
  
  