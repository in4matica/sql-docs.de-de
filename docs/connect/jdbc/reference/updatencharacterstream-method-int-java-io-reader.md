---
title: updateNCharacterStream-Methode (int, java.io.Reader) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fc746413-bdbf-4109-aee0-385a1270c847
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ce089832227a9f44cd1adfd0a4682b53002a2fc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "67998714"
---
# <a name="updatencharacterstream-method-int-javaioreader"></a>updateNCharacterStream-Methode (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Zeichendatenstromwert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateNCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **ganzzahliger** Wert, der den Spaltenindex angibt.  
  
 *x*  
  
 Ein Reader-Objekt  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Bemerkungen  
 Diese updateNCharacterStream-Methode wird von der updateNCharacterStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode übergibt Unicode-Zeichen aus einem Reader-Objekt an ausgewählte Spalten vom Typ **nchar**-, **nvarchar(max)** -, **ntext**- und **xml**. Bei Verwendung dieser Methode für andere Datentypspalten wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Weitere Informationen  
 [updateNCharacterStream-Methode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
