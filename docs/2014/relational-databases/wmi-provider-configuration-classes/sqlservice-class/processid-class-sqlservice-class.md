---
title: ProcessId-Klasse (SqlService-Klasse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProcessId Class (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b9e6c04a0ae0000284f3550d39e47c973adbe8ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63061918"
---
# <a name="processid-class-sqlservice-class"></a>ProcessId-Klasse (SqlService-Klasse)
  Ruft die Systemprozess-ID ab, die einen Dienst eindeutig identifiziert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object  
.ProcessId [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [SqlService-Klassen](sqlservice-class.md) Objekt, das den Dienst darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein `uint32`-Wert, der die ID zur eindeutigen Kennzeichnung des Prozesses angibt.  
  
## <a name="remarks"></a>Bemerkungen  
  
## <a name="example"></a>Beispiel  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Starten und Beenden von Diensten](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
