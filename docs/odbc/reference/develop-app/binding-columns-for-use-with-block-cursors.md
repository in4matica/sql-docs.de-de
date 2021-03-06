---
title: Binden von Spalten für die Verwendung mit Block Cursorn | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 827f6ddca12f15ce0bce1773b9cbe26fae5069dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106231"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Binden von Spalten für die Verwendung mit Blockcursorn
Da Block Cursor mehrere Zeilen zurückgeben, müssen Anwendungen, die Sie verwenden, anstelle einer einzelnen Variablen ein Array von Variablen an jede Spalte binden. Diese Arrays werden zusammen als *rowsetpuffer*bezeichnet. Im folgenden sind die beiden Bindungsarten aufgeführt:  
  
-   Binden Sie ein Array an jede Spalte. Dies wird *spaltenweise Bindung* genannt, da jede Datenstruktur (Array) Daten für eine einzelne Spalte enthält.  
  
-   Definieren Sie eine Struktur, in der die Daten für eine ganze Zeile enthalten sind, und binden Sie ein Array dieser Strukturen. Dies wird *zeilenweise Bindung* genannt, da jede Datenstruktur die Daten für eine einzelne Zeile enthält.  
  
 Wenn die Anwendung einzelne Variablen an Spalten bindet, ruft Sie **SQLBindCol** auf, um Arrays an Spalten zu binden. Der einzige Unterschied besteht darin, dass es sich bei den bestandenen Adressen um Array Adressen handelt, nicht um einzelne Variablen Die Anwendung legt das SQL_BIND_BY_COLUMN-Anweisungs Attribut fest, um anzugeben, ob die spaltenweise oder zeilenweise Bindung verwendet wird. Ob spaltenweise oder zeilenweise Bindung verwendet werden soll, ist größtenteils eine Frage der Anwendungs Einstellung. Die zeilenweise Bindung kann dem Layout von Daten der Anwendung genauer entsprechen. in diesem Fall würde Sie eine bessere Leistung bieten.  
  
 Dieser Abschnitt enthält die folgenden Themen:  
  
-   [Spaltenbezogenes Binden](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Zeilenbezogenes Binden](../../../odbc/reference/develop-app/row-wise-binding.md)
