---
title: Hinzufügen eines Ausdrucks (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a60ee091-b4ed-41e1-9b6a-032c316cd03f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 54505266a77c8baee7f39633ebccd0a5ab5708a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106741"
---
# <a name="add-an-expression-report-builder-and-ssrs"></a>Hinzufügen eines Ausdrucks (Berichts-Generator und SSRS)
  Ausdrücke werden überall in einem Bericht zum Definieren von Berichtselementeigenschaften, Filtern, Gruppen, Sortierreihenfolgen, Verbindungszeichenfolgen und Parameterwerten verwendet. Ausdrücke beginnen mit einem Gleichheitszeichen (=) und werden in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]geschrieben. Sie werden zur Laufzeit vom Berichtsprozessor ausgewertet, der das Auswertungsergebnis mit den Berichtslayoutelementen kombiniert.  
  
 Ausdrücke können einfach oder komplex sein. Einfache Ausdrücke verweisen auf ein einzelnes Element in einer integrierten Auflistung. Komplexe Ausdrücke können Konstanten, Operatoren, globale Auflistungselemente und Funktionsaufrufe enthalten. Weitere Informationen finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-expression-to-a-text-box"></a>So fügen Sie einem Textfeld einen Ausdruck hinzu  
  
-   Klicken Sie in der Ansicht **Entwurf** auf das Textfeld auf der Entwurfsoberfläche, dem Sie einen Ausdruck hinzufügen möchten.  
  
    -   Geben Sie den Anzeigetext für den Ausdruck in das Textfeld ein, um einen einfachen Ausdruck zu erstellen. Geben Sie zum Beispiel für das Datasetfeld Sales den Text `[Sales]`ein.  
  
    -   Klicken Sie mit der rechten Maustaste auf das Textfeld, und wählen Sie den Befehl **Ausdruck**aus, um einen komplexen Ausdruck einzugeben. Das Dialogfeld **Ausdruck** wird geöffnet. Geben Sie den Ausdruck im Ausdrucksbereich hinter '=' ein, bzw. erstellen Sie den Ausdruck interaktiv, und klicken Sie dann auf OK.  
  
         Der Ausdruck wird auf der Entwurfsoberfläche als `<<Expr>>`angezeigt.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Formatieren von Text und Platzhaltern &#40;Berichts-Generator und SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Textfelder &#40;Berichts-Generator und SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Filter Gleichungen &#40;Berichts-Generator und SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [Beispiele für Gruppierungsausdrücke (Berichts-Generator und SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [Dialog Feld ' Ausdruck ' &#40;Berichts-Generator&#41;](../expression-dialog-box-report-builder.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Hinzufügen von Code zu einem Bericht &#40;SSRS&#41;](add-code-to-a-report-ssrs.md)  
  
  
