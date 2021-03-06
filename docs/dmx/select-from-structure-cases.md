---
title: Wählen Sie &lt;eine&gt;Struktur aus. Fälle | Microsoft-Dokumentation
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 041d6ade2363b4a33528bd44438a2fcb440d61ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928294"
---
# <a name="select-from-ltstructuregtcases"></a>Wählen Sie &lt;eine&gt;Struktur aus. Denen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Fälle zurück, die zum Erstellen der Miningstruktur verwendet wurden.  
  
 Wenn Drillthrough nicht für die Struktur aktiviert ist, erzeugt die Anweisung einen Fehler. Die Anweisung schlägt auch fehl, wenn der Benutzer keine Drillthroughberechtigungen für die Miningstruktur hat.  
  
 In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]ist der Drillthrough für neue Mining Strukturen standardmäßig aktiviert. Um zu überprüfen, ob Drillthrough für eine bestimmte Struktur aktiviert ist, überprüfen Sie, ob der Wert der **CacheMode** -Eigenschaft auf **KeepTrainingCases**festgelegt ist.  
  
 Wenn der Wert von **CacheMode** in **ClearAfterProcessing**geändert wird, werden die Struktur Fälle aus dem Cache gelöscht, und Sie können keinen Drillthrough verwenden.  
  
> [!NOTE]  
>  Sie können Drillthrough in der Miningstruktur nicht mit Data Mining-Erweiterungen (DMX) aktivieren oder deaktivieren.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SELECT [TOP n] <expression list> FROM <structure>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumente  
 *n*  
 Optional. Eine ganze Zahl, die angibt, wie viele Zeilen zurückgegeben werden sollen.  
  
 *Ausdrucks Liste*  
 Eine Liste von Ausdrücken, die durch Trennzeichen voneinander getrennt sind.  
  
 Ein Ausdruck kann Spaltenbezeichner, benutzerdefinierte Funktionen und VBA-Funktionen einschließen.  
  
 *Werks*  
 Der Name der Struktur.  
  
 *Bedingungs Ausdruck*  
 Eine Bedingung, die die Werte einschränkt, die für die Spaltenliste zurückgegeben werden.  
  
 *Begriff*  
 Optional. Ein Ausdruck, der einen Skalarwert zurückgibt.  
  
## <a name="remarks"></a>Bemerkungen  
 Wenn Sie Drillthrough sowohl für das Modell als auch für die Struktur aktivieren, kann jedes Mitglied einer Rolle mit Drillthroughberechtigungen für die Miningstruktur und das Modell mit der folgenden Syntax Strukturspalten zurückgeben, die nicht Teil des Modells sind:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Daher sollten Sie zum Schutz sensibler Daten oder persönlicher Informationen die Datenquellen Sicht so erstellen, dass persönliche Informationen maskiert werden, und die **AllowDrillThrough** -Berechtigung für eine Mining Struktur oder ein Mining Modell nur bei Bedarf erteilen.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele basieren auf der Mining Struktur based Mailing, die auf der [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] -Datenbank basiert, und den zugehörigen Mining Modellen. Weitere Informationen finden Sie unter [Tutorial zu Data Mining-Grundlagen](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drill-through-to-structure-cases"></a>Beispiel 1: Ausführen eines Drillthrough zu Strukturfällen  
 Im folgenden Beispiel wird eine Liste der 500 ältesten Kunden in der Miningstruktur Targeted Mailing zurückgegeben. Die Abfrage gibt alle Spalten im Miningmodell zurück, beschränkt die Zeilen jedoch auf die Kunden, die ein Fahrrad gekauft haben, und sortiert diese nach Alter. Sie können die Ausdrucksliste auch so bearbeiten, dass nur die benötigten Spalten zurückgegeben werden.  
  
```  
SELECT TOP 500 *  
FROM [Targeted Mailing].Cases  
WHERE [Bike Buyer] = 1  
ORDER BY Age DESC;  
```  
  
### <a name="example-2-drillthrough-to-test-or-training-cases-only"></a>Beispiel 2: Nur Drillthrough zu Test- oder Trainingsfällen  
 Im folgenden Beispiel wird eine Liste der zum Testen reservierten Strukturfälle für Targeted Mailing zurückgegeben. Wenn die Miningstruktur keinen Zurückhaltungstestsatz enthält, werden alle Fälle standardmäßig als Trainingsfälle behandelt, und bei dieser Abfrage würden 0 Fälle zurückgegeben werden.  
  
```  
SELECT [Customer Key], Gender, Age  
FROM [Targeted Mailing].Cases  
WHERE IsTestCase();  
```  
  
 Um die Trainingsfälle zurückzugeben, ersetzen Sie die Funktion `IsTrainingCase()`.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Wählen Sie &#40;DMX-&#41;](../dmx/select-dmx.md)   
 [Data Mining-Erweiterungen &#40;DMX-&#41; Daten Definitions Anweisungen](../dmx/dmx-statements-data-definition.md)   
 [Data Mining-Erweiterungen &#40;DMX-&#41; Daten Bearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining-Erweiterungen &#40;DMX-&#41;-Anweisungs Referenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
