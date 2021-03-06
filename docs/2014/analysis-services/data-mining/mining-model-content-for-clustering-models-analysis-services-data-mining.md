---
title: Mining Modell Inhalt von Clustering-Modellen (Analysis Services-Data Mining) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- nearest neighbor [Data Mining]
- clustering [Data Mining]
- mining model content, clustering models
- clustering algorithms [Analysis Services]
ms.assetid: aed1b7d3-8f20-4eeb-b156-0229f942cefd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a733b434e428f7486c235f4efc923adfa4b14949
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083682"
---
# <a name="mining-model-content-for-clustering-models-analysis-services---data-mining"></a>Mingingmodellinhalt von Clustermodellen (Analysis Services - Data Mining)
  In diesem Thema wird der Miningmodellinhalt beschrieben, der Modellen eigen ist, die den Microsoft Clustering-Algorithmus verwenden. Eine allgemeine Erläuterung der Miningmodellinhalte für alle Modelltypen finden Sie unter [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-a-clustering-model"></a>Grundlegendes zur Struktur von Clusteringmodellen  
 Ein Clusteringmodell besitzt eine einfache Struktur. Jedes Modell verfügt über einen einzigen übergeordneten Knoten, der das Modell und seine Metadaten darstellt, und jeder übergeordnete Knoten enthält eine einfache Liste der Cluster (NODE_TYPE = 5). Dieser Aufbau wird in der folgenden Abbildung dargestellt.  
  
 ![Struktur des Modellinhalts für Clustering](../media/modelcontentstructure-clust.gif "Struktur des Modellinhalts für Clustering")  
  
 Jeder untergeordnete Knoten stellt ein einzelnes Cluster dar und enthält detaillierte Statistiken zu den Attributen der in diesem Cluster enthaltenen Fälle. Hierzu zählen die Anzahl der zum Cluster gehörigen Fälle und die Verteilung der Werte, durch die sich das betreffende Cluster von anderen Clustern unterscheidet.  
  
> [!NOTE]  
>  Sie müssen nicht alle Knoten durchsuchen, um die Anzahl der Cluster zu ermitteln und deren Beschreibung zu erhalten. Im übergeordneten Knoten des Modells wird auch die Anzahl und eine Auflistung der Knoten verzeichnet.  
  
 Der übergeordnete Knoten enthält nützliche statistische Daten, die die tatsächliche Verteilung aller Trainingsfälle beschreiben. Diese statistischen Daten befinden sich in der geschachtelten Tabellenspalte NODE_DISTRIBUTION. Beispielsweise enthält die folgende Tabelle einige Zeilen der Tabelle NODE_DISTRIBUTION, die die Verteilung der demografischen Kundendaten aus dem Clustermodell `TM_Clustering`beschreibt, das Sie im [Tutorial zu Data Mining-Grundlagen](../../tutorials/basic-data-mining-tutorial.md)erstellen:  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|SUPPORT|PROBABILITY|Varianz|VALUE_TYPE|  
|---------------------|---------------------|-------------|-----------------|--------------|-----------------|  
|Alter|Missing|0|0|0|1 (Missing)|  
|Alter|44.9016152716593|12939|1|125.663453102554|3 (Continuous)|  
|Geschlecht|Missing|0|0|0|1 (Missing)|  
|Geschlecht|F|6350|0.490764355823479|0|4 (Discrete)|  
|Geschlecht|M|6589|0.509235644176521|0|4 (Discrete)|  
  
 Aus diesen Ergebnissen geht hervor, dass 12.939 Fälle zur Erstellung des Modells verwendet wurden, dass das Verhältnis zwischen männlichen und weiblichen Kunden etwa 50:50 war und dass das durchschnittliche Alter 44 Jahre betrug. Die beschreibenden Statistikdaten unterscheiden sich, je nachdem, ob das berechnete Attribut einen kontinuierlichen numerischen Datentyp oder einen diskreten Werttyp aufweist, wie beispielsweise Geschlecht. Die statistischen Measures *Mittelwert* und *Varianz* werden für kontinuierliche Datentypen berechnet, während *Wahrscheinlichkeit* und *Unterstützung* für diskrete Datentypen berechnet werden.  
  
> [!NOTE]  
>  Die Varianz repräsentiert die Gesamtvarianz des Clusters. Wenn der Varianzwert klein ist, bedeutet dies, dass die meisten Werte der Spalte relativ nah am Mittelwert liegen. Um die Standardabweichung zu erhalten, berechnen Sie die Quadratwurzel der Varianz.  
  
 Beachten Sie, dass jedes Attribut den Werttyp `Missing` enthält, der anzeigt, in wie vielen Fällen kein Wert für das Attribut gegeben war. Fehlende Daten können signifikant sein und die Berechnungen je nach Datentyp auf verschiedene Weise beeinflussen. Weitere Informationen finden Sie unter [Fehlende Werte &#40;Analysis Services – Data Mining&#41;](missing-values-analysis-services-data-mining.md)vordefinierten Modellierungsflags können Plug-Ins eines Drittanbieters über eigene Modellierungsflags verfügen.  
  
## <a name="model-content-for-a-clustering-model"></a>Modellinhalt eines Clusteringmodells  
 In diesem Abschnitt werden nur diejenigen Spalten des Miningmodellinhalts detaillierter und anhand von Beispielen erläutert, die für Clusteringmodelle relevant sind.  
  
 Informationen zu den allgemeinen Spalten im Schemarowset, z.B. MODEL_CATALOG und MODEL_NAME, finden Sie unter [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
 MODEL_CATALOG  
 Name der Datenbank, in der das Modell gespeichert wird.  
  
 MODEL_NAME  
 Name des Modells.  
  
 ATTRIBUTE_NAME  
 Ist in Clusteringmodellen immer leer, da es in diesem Modell kein vorhersagbares Attribut gibt.  
  
 NODE_NAME  
 Entspricht immer NODE_UNIQUE_NAME.  
  
 NODE_UNIQUE_NAME  
 Ein innerhalb des Modells eindeutiger Bezeichner für den Knoten. Dieser Wert kann nicht geändert werden.  
  
 NODE_TYPE  
 Ein Clusteringmodell gibt die folgenden Knotentypen aus:  
  
|Knoten-ID und Name|BESCHREIBUNG|  
|----------------------|-----------------|  
|1 (Model)|Stammknoten des Modells|  
|5 (Cluster)|Enthält die Anzahl der im Cluster enthaltenen Fälle, die Merkmale der im Cluster enthaltenen Fälle und Statistiken, welche die Werte des Clusters beschreiben.|  
  
 NODE_CAPTION  
 Ein beschreibender Name, der angezeigt wird. Wenn Sie ein Modell erstellen, wird der Wert von NODE_UNIQUE_NAME automatisch als Beschriftung verwendet. Sie können den Wert von NODE_CAPTION jedoch im Programmcode oder im Viewer ändern, um den Anzeigenamen des Clusters zu aktualisieren.  
  
> [!NOTE]  
>  Wenn Sie das Modell erneut verarbeiten, werden alle Namensänderungen durch die neuen Werte überschrieben. Die Namen können nicht im Modell persistent gespeichert werden, und Sie können Änderungen in der Clustermitgliedschaft nicht über verschiedene Versionen eines Modells hinweg verfolgen.  
  
 CHILDREN_CARDINALITY  
 Eine Schätzung der Anzahl untergeordneter Elemente des Knotens.  
  
 Über **geordneter Knoten** Gibt die Anzahl der Cluster im Modell an.  
  
 **Cluster Knoten** Immer 0.  
  
 PARENT_UNIQUE_NAME  
 Der eindeutige Name des dem Knoten übergeordneten Elements.  
  
 Über **geordneter Knoten** Immer NULL  
  
 **Cluster Knoten** Normalerweise 000.  
  
 NODE_DESCRIPTION  
 Eine Beschreibung des Knotens.  
  
 Über **geordneter Knoten** Immer **(alle)**.  
  
 **Cluster Knoten** Eine durch Trennzeichen getrennte Liste der primären Attribute, die den Cluster von anderen Clustern unterscheiden.  
  
 NODE_RULE  
 Wird für Clusteringmodelle nicht verwendet.  
  
 MARGINAL_RULE  
 Wird für Clusteringmodelle nicht verwendet.  
  
 NODE_PROBABILITY  
 Die diesem Knoten zugeordnete Wahrscheinlichkeit. Über **geordneter Knoten** Immer 1.  
  
 **Cluster Knoten** Die Wahrscheinlichkeit repräsentiert die zusammengesetzte Wahrscheinlichkeit der Attribute, wobei einige Anpassungen vorgenommen werden, abhängig vom Algorithmus, der zum Erstellen des Clustering-Modells verwendet wird.  
  
 MARGINAL_PROBABILITY  
 Die Wahrscheinlichkeit für das Erreichen des Knotens vom übergeordneten Knoten aus. In einem Clusteringmodell entspricht die marginale Wahrscheinlichkeit immer der Knotenwahrscheinlichkeit.  
  
 NODE_DISTRIBUTION  
 Eine Tabelle, die das Wahrscheinlichkeitshistogramm des Knotens enthält.  
  
 Über **geordneter Knoten** Weitere Informationen finden Sie in der Einführung zu diesem Thema.  
  
 **Cluster Knoten** Stellt die Verteilung von Attributen und Werten für Fälle dar, die in diesem Cluster enthalten sind.  
  
 NODE_SUPPORT  
 Die Anzahl der Fälle, die diesen Knoten unterstützen. Über **geordneter Knoten** Gibt die Anzahl der Trainings Fälle für das gesamte Modell an.  
  
 **Cluster Knoten** Gibt die Größe des Clusters als Anzahl von Fällen an.  
  
 **Hinweis** Wenn das Modell K-Means-Clustering verwendet, kann jeder Fall nur zu einem Cluster gehören. Verwendet das Modell dagegen die EM-Clusteringmethode, kann jeder Fall zu verschiedenen Clustern gehören, und jedem Fall wird für jedes Cluster, zu dem er gehört, ein gewichteter Abstand zugewiesen. Daher ist bei EM-Modellen die Summe der Unterstützungswerte für ein einzelnes Cluster größer als der Unterstützungswert für das Gesamtmodell.  
  
 MSOLAP_MODEL_COLUMN  
 Wird für Clusteringmodelle nicht verwendet.  
  
 MSOLAP_NODE_SCORE  
 Zeigt die dem Knoten zugeordnete Bewertung an.  
  
 Über **geordneter Knoten** Die BIC-Bewertung (bayyesian Information Kriterium) für das Clustering-Modell.  
  
 **Cluster Knoten** Immer 0.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 Eine zu Anzeigezwecken verwendete Beschriftung. Diese Beschriftung kann nicht geändert werden.  
  
 Über **geordneter Knoten** Der Modelltyp: Cluster Modell  
  
 **Cluster Knoten** Der Name des Clusters. Beispiel: Cluster 1.  
  
## <a name="remarks"></a>Bemerkungen  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt mehrere Methoden zum Erstellen eines Clusteringmodells bereit. Wenn Sie nicht wissen, mithilfe welcher Methode das Modell, mit dem Sie arbeiten, erstellt wurde, können Sie die Modellmetadaten entweder programmgesteuert über einen ADOMD-Client oder über AMO oder durch Abfragen des Data Mining-Schemarowsets abrufen. Weitere Informationen finden Sie unter [Abfragen der Parameter, mit denen ein Miningmodell erstellt wird](query-the-parameters-used-to-create-a-mining-model.md).  
  
> [!NOTE]  
>  Struktur und Inhalt des Modells werden weder durch die verwendete Clusteringmethode noch die Parameter beeinflusst.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Mining Modell Inhalt &#40;Analysis Services Data Mining-&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Viewer für Data Mining-Modelle](data-mining-model-viewers.md)   
 [Microsoft Clustering-Algorithmus](microsoft-clustering-algorithm.md)   
 [Data Mining-Abfragen](data-mining-queries.md)  
  
  
