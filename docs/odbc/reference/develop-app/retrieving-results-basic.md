---
title: Abrufen von Ergebnissen (Basic) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abe4dd2f0bfb0b5302022d8e50cddc7df84f192
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020472"
---
# <a name="retrieving-results-basic"></a>Abrufen von Ergebnissen (Standard)
Ein *Resultset* ist ein Satz von Zeilen in der Datenquelle, der bestimmten Kriterien entspricht. Es handelt sich um eine konzeptionelle Tabelle, die sich aus einer Abfrage ergibt und die für eine Anwendung in tabellarischer Form verfügbar ist. **Select** -Anweisungen, Katalog Funktionen und einige Prozeduren erstellen Resultsets. Im folgenden Beispiel erstellt die erste SQL-Anweisung ein Resultset, das alle Zeilen und alle Spalten in der Orders-Tabelle enthält, und die zweite SQL-Anweisung erstellt ein Resultset mit den Spalten OrderID, SalesPerson und Status für die Zeilen in der Orders-Tabelle. , in dem der Status "offen" lautet:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Ein Resultset kann leer sein, was sich von keinem Resultset unterscheidet. Beispielsweise erstellt die folgende SQL-Anweisung ein leeres Resultset:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Ein leeres Resultset unterscheidet sich nicht von einem anderen Resultset, mit dem Unterschied, dass es keine Zeilen enthält. Die Anwendung kann z. b. Metadaten für das Resultset abrufen, versuchen, Zeilen abzurufen, und muss den Cursor über dem Resultset schließen.  
  
 Das Abrufen von Zeilen aus der Datenquelle und deren Rückgabe an die Anwendung wird als *Abruf bezeichnet.* In diesem Abschnitt werden die grundlegenden Teile dieses Prozesses erläutert. Informationen zu komplexeren Themen, wie [z. b](../../../odbc/reference/develop-app/scrollable-cursors.md). Block-und Bild lauffähigen Cursorn, finden Sie unter Blockieren von [Cursorn](../../../odbc/reference/develop-app/block-cursors.md) und Weitere Informationen zum Aktualisieren, löschen und Einfügen von Zeilen finden Sie unter Übersicht über das [Aktualisieren von Daten](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Dieser Abschnitt enthält die folgenden Themen:  
  
-   [Wurde ein Resultset erstellt?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Resultsetmetadaten](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Binden von Spalten](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Abrufen von Daten](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Schließen des Cursors](../../../odbc/reference/develop-app/closing-the-cursor.md)
