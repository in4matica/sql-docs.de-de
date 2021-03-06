---
title: Schließen des Cursors | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de22797bdcf4ff526a8c17aee313567da3114b60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036542"
---
# <a name="closing-the-cursor"></a>Schließen des Cursors
Wenn eine Anwendung die Verwendung eines Cursors beendet hat, ruft Sie **SQLCloseCursor** auf, um den Cursor zu schließen. Beispiel:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Bis die Anwendung den Cursor schließt, kann die Anweisung, für die der Cursor geöffnet wird, nicht für die meisten anderen Vorgänge verwendet werden, wie z. b. das Ausführen einer anderen SQL-Anweisung. Eine komplette Liste der Funktionen, die aufgerufen werden können, während ein Cursor geöffnet ist, finden Sie unter [Anhang B: ODBC-Status Übergangs Tabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Um einen Cursor zu schließen, sollte eine Anwendung **SQLCloseCursor**, nicht **SQLCancel**, abrufen.  
  
 Cursor bleiben geöffnet, bis Sie explizit geschlossen werden, außer wenn für eine Transaktion ein Commit oder ein Rollback ausgeführt wird. in diesem Fall schließen einige Datenquellen den Cursor. Insbesondere das Erreichen des Endes des Resultsets, wenn **SQLFetch** SQL_NO_DATA zurückgibt, schließt einen Cursor nicht. Auch Cursor für leere Resultsets (Resultsets, die erstellt wurden, als eine Anweisung erfolgreich ausgeführt wurde, die jedoch keine Zeilen zurück gab) müssen explizit geschlossen werden.
