---
title: PDO::rollback | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d37145856da6c4b3ff6def1620de443b20faebfb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "67936197"
---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Verwirft Datenbankbefehle, die nach dem Aufrufen von [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) ausgegeben wurden, und setzt die Verbindung in den Autocommit-Modus zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>Rückgabewert  
„true“, bei erfolgreichem Aufruf der Methode; andernfalls „false“.  
  
## <a name="remarks"></a>Bemerkungen  
PDO::rollback ist nicht betroffen von (und hat keinen Einfluss auf) den Wert von PDO::ATTR_AUTOCOMMIT.  
  
Unter [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) finden Sie ein Beispiel, das PDO::rollback verwendet.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="see-also"></a>Weitere Informationen  
[PDO-Klasse](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
