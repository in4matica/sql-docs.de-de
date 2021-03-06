---
title: Löschen von Zeilen im Rowset mit SQLSetPos | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e39b70f92f7b239b011cdd4fdd6abd36c27561c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076801"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Löschen von Zeilen im Rowset mit SQLSetPos
Der DELETE-Vorgang von **SQLSetPos** bewirkt, dass die Datenquelle eine oder mehrere ausgewählte Zeilen einer Tabelle löscht. Zum Löschen von Zeilen mit **SQLSetPos**Ruft die Anwendung **SQLSetPos** auf, wobei *Operation* auf SQL_DELETE und *RowNumber* auf die Nummer der zu löschenden Zeile festgelegt ist. Wenn *RowNumber* 0 ist, werden alle Zeilen im Rowset gelöscht.  
  
 Nach dem zurückkehren von **SQLSetPos** ist die gelöschte Zeile die aktuelle Zeile, und Ihr Status ist SQL_ROW_DELETED. Die Zeile kann nicht in anderen positionierten Vorgängen verwendet werden, z. b. bei Aufrufen von **SQLGetData** oder **SQLSetPos**.  
  
 Wenn alle Zeilen des Rowsets gelöscht werden (*RowNumber* ist gleich 0), kann die Anwendung verhindern, dass der Treiber bestimmte Zeilen mit dem Zeilen Vorgangs Array löscht, und zwar auf dieselbe Weise wie für den Aktualisierungs Vorgang von **SQLSetPos**. (Weitere Informationen finden Sie unter [Aktualisieren von Zeilen im Rowset mit SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Jede Zeile, die gelöscht wird, sollte eine Zeile sein, die im Resultset vorhanden ist. Wenn die Anwendungs Puffer durch Abrufen und ein Zeilen Status Array beibehalten wurden, sollten die Werte an den einzelnen Zeilen Positionen nicht SQL_ROW_DELETED, SQL_ROW_ERROR oder SQL_ROW_NOROW sein.
