---
title: Verbindungs Zeichenfolgen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to driver [ODBC], connection strings
- functions [ODBC], data source or driver connections
- connection strings [ODBC], about connection strings
- connecting to data source [ODBC], connection strings
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: 724c7b86-300a-4fa9-ad96-4afa0fdcb3e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f68a87db729df2f4a27e2766a9de60e8c75a71a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036423"
---
# <a name="connection-strings"></a>Verbindungszeichenfolgen
Eine Verbindungs Zeichenfolge enthält Informationen, die zum Herstellen einer Verbindung verwendet werden. Eine vollständige Verbindungs Zeichenfolge enthält alle Informationen, die zum Herstellen einer Verbindung erforderlich sind. Die Verbindungs Zeichenfolge ist eine Reihe von Schlüsselwort-Wert-Paaren, die durch Semikolons getrennt sind. (Die gesamte Syntax einer Verbindungs Zeichenfolge finden Sie in der Beschreibung der [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) -Funktion.) Die Verbindungs Zeichenfolge wird verwendet von:  
  
-   **SQLDriverConnect**: schließt die Verbindungs Zeichenfolge durch Interaktion mit dem Benutzer ab.  
  
-   **Sqlbrowseconnetct**, das die Verbindungs Zeichenfolge iterativ mit der Datenquelle vervollständigt.  
  
 **SQLCONNECT** verwendet keine Verbindungs Zeichenfolge. die Verwendung von **SQLCONNECT** entspricht der Verbindung mithilfe einer Verbindungs Zeichenfolge mit genau drei Schlüsselwort-Wert-Paaren (für den Datenquellen Namen und, optional, Benutzer-ID und Kennwort).
