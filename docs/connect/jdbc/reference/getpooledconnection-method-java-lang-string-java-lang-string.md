---
title: getPooledConnection-Methode (java.lang.String, java.lang.String) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2e6391d-9aaf-4b09-ae1c-a27c1ada6301
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69a9db6da093341264953e698cdbb1145093d9a5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980872"
---
# <a name="getpooledconnection-method-javalangstring-javalangstring"></a>getPooledConnection-Methode (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt eine physische Datenbankverbindung her, die auf Grundlage des angegebenen Benutzernamens und Kennworts als Poolverbindung verwendet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public javax.sql.PooledConnection getPooledConnection(java.lang.String user,  
                                                      java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parameter  
 *user*  
  
 Ein **String-Objekt**, das den Benutzernamen enthält.  
  
 *passwword*  
  
 Eine **Zeichenfolge**, die das Kennwort enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Bemerkungen  
 Diese getPooledConnection-Methode wird von der getPooledConnection-Methode in der javax.sql.ConnectionPoolDataSource-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Weitere Informationen  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource-Methoden](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource-Elemente](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource-Klasse](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
