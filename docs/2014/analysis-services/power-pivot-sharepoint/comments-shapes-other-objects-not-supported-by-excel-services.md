---
title: 'Die folgenden Funktionen werden von Excel Services nicht unterstützt und möglicherweise nur teilweise angezeigt: Kommentare, Formen oder andere Objekte | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 03411134eb1350adcd37badd458e7f7a0198a9ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071921"
---
# <a name="the-following-features-are-not-supported-by-excel-services-and-may-not-display-or-may-display-only-partially-comments-shapes-or-other-objects"></a>Die folgenden Funktionen werden von Excel Services nicht unterstützt und möglicherweise nur teilweise oder überhaupt nicht angezeigt: Kommentare, Formen oder andere Objekte
  Dieser Fehler tritt auf, wenn Sie einer PowerPivot-Arbeitsmappe Slicer aus einer PowerPivot-Feldliste hinzufügen.  
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Anwendungsbereich|PowerPivot für SharePoint|  
|Produktversion|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Ursache|Das Shape-Objekt, mit dem die Positionierung und Formatierung von Slicern gesteuert wird, die einer Arbeitsmappe aus der PowerPivot-Feldliste hinzugefügt wurden, kann von Excel Web Access nicht gerendert werden.|  
|Meldungstext|Die folgenden Funktionen werden von Excel Services nicht unterstützt und möglicherweise nur teilweise oder überhaupt nicht angezeigt:<br /><br /> Kommentare, Formen oder andere Objekte<br /><br /> Einige Funktionen z. B. externe Datenabfragen, zeigen zwischengespeicherte Daten an, die nur in Microsoft Excel aktualisiert werden können.|  
  
## <a name="explanation"></a>Erklärung  
 Excel Webzugriff zeigt diesen Fehler an, wenn Sie eine Power Pivot-Arbeitsmappe in einem Browser öffnen und auf die Schaltfläche **Details** für die Meldung, **nicht unterstützte Funktionen, die diese Arbeitsmappe möglicherweise nicht wie vorgesehen anzeigt**.  
  
 Dieser Fehler tritt auf, weil die PowerPivot-Arbeitsmappe Slicer enthält, deren Layout über ein ausgeblendetes Shape-Objekt in Excel gesteuert wird. Das Shape-Objekt steuert die Formatierung und Positionierung der Slicer in horizontalen und vertikalen Platzierungen.  
  
 Shape-Objekte können von Excel Services nicht gerendert werden, dies ist jedoch kein Problem, weil es sich um ein ausgeblendetes Objekt handelt.  
  
## <a name="user-action"></a>Benutzeraktion  
 Dieser Fehler kann ignoriert werden. Klicken Sie auf **OK** , um die Fehlermeldung zu schließen und die Verwendung von Arbeitsmappe und Slicern ohne Probleme fortzusetzen.  
  
  
