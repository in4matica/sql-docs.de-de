---
title: prepareCall-Methode (java.lang.String, int, int, int) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 81104fd5-75b0-4540-9f48-c3dbf59a8564
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0839fb735431adcdc4d1e3d0e7820ca2253cc121
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976243"
---
# <a name="preparecall-method-javalangstring-int-int-int"></a>prepareCall-Methode (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt ein [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)-Objekt von dem [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)-Objekte mit dem angegebenen Typ der Parallelität und der Haltbarkeit generiert werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int nType,  
                                              int nConcur,  
                                              int nHold)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sql*  
  
 Eine **Zeichenfolge**, die eine SQL-Anweisung enthält.  
  
 *nType*  
  
 Ein Wert vom Typ **int** zur Angabe des Resultsettyps.  
  
 *nConcur*  
  
 Ein Wert vom Typ **int** zur Angabe des Parallelitätstyps des Resultsets.  
  
 *nHold*  
  
 Ein Wert vom Typ **int** zum Angeben der Resultsethaltbarkeit.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein CallableStatement-Objekt  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Bemerkungen  
 Diese prepareCall-Methode wird von der prepareCall-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Weitere Informationen  
 [prepareCall-Methode &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
