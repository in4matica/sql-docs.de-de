---
title: supportsResultSetHoldability-Methode (SQLServerDatabaseMetaData) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsResultSetHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ab575792-fd11-4ff3-8847-1368e7a322c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 766c09aca5256d369ebad98cb1c002f4498dda7a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "67968940"
---
# <a name="supportsresultsetholdability-method-sqlserverdatabasemetadata"></a>supportsResultSetHoldability-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob von dieser Datenbank die angegebene Resultsethaltbarkeit unterstützt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean supportsResultSetHoldability(int holdability)  
```  
  
#### <a name="parameters"></a>Parameter  
 *holdability*  
  
 Ein Wert vom Typ **int** zum Angeben der Resultsethaltbarkeit. Mögliche Werte:  
  
 ResultSet.HOLD_CURSORS_OVER_COMMIT  
  
 ResultSet.CLOSE_CURSORS_AT_COMMIT  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** unterstützt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Bemerkungen  
 Diese supportsResultSetHoldability-Methode wird von der supportsResultSetHoldability-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Weitere Informationen  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
