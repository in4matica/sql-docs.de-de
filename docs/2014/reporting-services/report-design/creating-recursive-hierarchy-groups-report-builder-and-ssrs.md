---
title: Erstellen von rekursiven Hierarchiegruppen (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: af5b0d3159dd8cae1fb33933b93bc0a92a2b20a5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189967"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>Erstellen von rekursiven Hierarchiegruppen (Berichts-Generator und SSRS)
  Um rekursive Daten anzuzeigen, in dem die Beziehung zwischen übergeordnetem und untergeordnetem durch Felder im Dataset dargestellt wird, können Sie den Region Gruppenausdruck basierend auf dem untergeordneten Feld festgelegt und die übergeordnete Eigenschaft basierend auf dem übergeordneten Feld festlegen.  
  
 Eine hierarchische Anzeige von Daten wird häufig für rekursive Hierarchiegruppen verwendet, z. B. für Angestellte in einem Unternehmensdiagramm. Das Dataset enthält eine Liste mit Mitarbeitern und Managern, wobei die Namen der Manager auch in der Mitarbeiterliste enthalten sind.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>Erstellen von rekursiven Hierarchien  
 Sie müssen den Gruppenausdruck auf das Feld festlegen, das die untergeordneten Daten enthält, und die übergeordnete Eigenschaft der Gruppe auf das Feld, das die übergeordneten Daten enthält, um eine rekursive Hierarchie in einem Tablix-Datenbereich zu erstellen. Legen Sie z.B. für ein Dataset, das Felder für die Mitarbeiter-ID und die Manager-ID enthält (wobei die Mitarbeiter an die Manager berichten) den Gruppenausdruck auf die Mitarbeiter-ID und die übergeordnete Eigenschaft auf die Manager-ID fest.  
  
 Eine Gruppe, die als rekursive Hierarchie definiert ist (also eine Gruppe, die die übergeordnete Eigenschaft verwendet), kann nur über einen einzelnen Gruppenausdruck verfügen. Mit der `Level`-Funktion können Sie die Auffüllung in Textfeldern bestimmen, um die Mitarbeiternamen entsprechend ihrer Ebene in der Hierarchie einzurücken.  
  
 Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich (Berichts-Generator und SSRS)](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) und [Erstellen einer rekursiven Hierarchiegruppe (Berichts-Generator und SSRS)](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>Aggregatfunktionen zur Unterstützung der Rekursion  
 Sie können Reporting Services-Aggregatfunktionen verwenden, die den Parameter *Rekursiv* akzeptieren, um Zusammenfassungsdaten für eine rekursive Hierarchie zu berechnen. Die folgenden Funktionen akzeptieren `Recursive` als Parameter: [Summe](report-builder-functions-sum-function.md), [Avg](report-builder-functions-avg-function.md), [Anzahl](report-builder-functions-count-function.md), [CountDistinct](report-builder-functions-countdistinct-function.md), [ CountRows](report-builder-functions-countrows-function.md), [Max](report-builder-functions-max-function.md), [Min](report-builder-functions-min-function.md), [StDev](report-builder-functions-stdev-function.md), [StDevP](report-builder-functions-stdevp-function.md), [Summe](report-builder-functions-sum-function.md), [Var](report-builder-functions-var-function.md), und [VarP](report-builder-functions-varp-function.md). Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Referenz zu Aggregatfunktionen &#40;Berichts-Generator und SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Tabellen (Berichts-Generator und SSRS)](tables-report-builder-and-ssrs.md)   
 [Matrizen (Berichts-Generator und SSRS)](create-a-matrix-report-builder-and-ssrs.md)   
 [Listen (Berichts-Generator und SSRS)](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  