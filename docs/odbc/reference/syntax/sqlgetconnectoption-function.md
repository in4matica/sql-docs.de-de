---
title: SQLGetConnectOption-Funktion | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7461304a9aa015eac223dc726e669ad5c4ecd4ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103836"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption-Funktion
**Konformitäts**  
 Eingeführte Version: ODBC 1,0 Standards Compliance: deprecated  
  
 **Zusammenfassung**  
 In ODBC *3. x*wurde die ODBC *2. x* -Funktion **SQLGetConnectOption** durch **SQLGetConnectAttr**ersetzt. Weitere Informationen finden Sie unter [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]
>  Weitere Informationen dazu, was der Treiber-Manager diese Funktion zuordnet, wenn eine ODBC *2. x* -Anwendung mit einem ODBC *3. x* -Treiber arbeitet, finden Sie unter [Mapping Deprecated Functions](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) in Anhang G: Driver Guidelines for abwärts Compatibility.  
> 
> [!NOTE]
>  Das in ODBC 3,8 eingeführte Attribut SQL_ASYNC_DBC_FUNCTION_ENABLE wird von **SQLGetConnectOption**nicht unterstützt. Anwendungen, die den asynchronen Vorgang für ein Verbindungs Handle verwenden, müssen **SQLGetConnectAttr**verwenden.  
  
## <a name="see-also"></a>Weitere Informationen  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
