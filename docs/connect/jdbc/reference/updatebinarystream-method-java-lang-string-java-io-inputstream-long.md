---
title: updateBinaryStream-Methode (java.io.InputStream, long) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3c0fb5d-ca05-43f7-9f38-fba6cf3705c6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4dd548fcd6342e4c69ea9acc1614d0bc899f7d4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "67985323"
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-long"></a>updateBinaryStream-Methode (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Binärdatenstromwert mit der angegebenen Anzahl von Bytes.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               long length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnLabel*  
  
 Eine Zeichenfolge, die die Spaltenbezeichnung enthält.  
  
 *x*  
  
 Dies ist ein InputStream-Objekt.  
  
 *length*  
  
 Ein Wert vom Typ **long** zum Angeben der Streamlänge.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Bemerkungen  
 Diese updateBinaryStream-Methode wird von der updateBinaryStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Von dieser Methode werden Bytes aus einem InputStream-Objekt an ausgewählte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Binärspalten wie „binary“, „varbinary“, „varbinary(max)“, „image“, „xml“ oder „udt“ übergeben. Das Aktualisieren von Zeichenspalten wird für diese Methode nicht unterstützt. Verwenden Sie die [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)-Methode, um Zeichenspalten mit InputStream zu aktualisieren.  
  
 Entspricht die Länge des Streams nicht der Angabe im *length*-Parameter, wird vom JDBC-Treiber beim Aktualisieren oder Einfügen der Zeile eine Ausnahme ausgelöst.  
  
 Ist die Länge des Streams nicht bekannt, kann der *length*-Parameter auf „–1“ festgelegt werden, um anzugeben, dass der Stream unabhängig von seiner Länge akzeptiert werden soll. Bei „sqljdbc4.jar“ empfiehlt sich die Verwendung der JDBC 4.0-Methode [updateBinaryStream &#40;java.lang.String, java.io.InputStream&#41;](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md), wenn von der Anwendung versucht wird, die Spalte aus einem Stream mit unbekannter Länge zu aktualisieren.  
  
## <a name="see-also"></a>Weitere Informationen  
 [updateBinaryStream-Methode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
