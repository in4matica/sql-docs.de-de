---
title: Konfigurieren der Serverkonfigurationsoption„Remote Data Archive“ | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
author: rothja
ms.author: jroth
ms.openlocfilehash: fda2594b2dc61a78eb5900ef6d1b735dac5b44e4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012328"
---
# <a name="configure-the-remote-data-archive-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption "Remote Data Archive"
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Geben Sie mit der Option **Remotedatenarchiv** an, ob Datenbanken und Tabellen auf dem Server für Stretch aktiviert werden können. Weitere Informationen finden Sie unter [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 Die Option **Remotedatenarchiv** kann die folgenden Werte enthalten.  
  
|value|BESCHREIBUNG|  
|-----------|-----------------|  
|0|Datenbanken und Tabellen auf dem Server können nicht für Stretch aktiviert werden.|  
|1|Datenbanken und Tabellen auf dem Server können für Stretch aktiviert werden.|  
  
 Um **sp_configure** auszuführen und den Wert der Option **Remotedatenarchiv** festzulegen, sind sysadmin- oder serveradmin-Berechtigungen erforderlich.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel zeigt zunächst die aktuelle Einstellung der Option **Remotedatenarchiv** . Danach aktiviert das Beispiel die Option **Remotedatenarchiv** , indem ihr Wert auf 1 festgelegt wird.  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 Wenn Sie die Option deaktivieren möchten, legen Sie den Wert auf 0 fest.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Aktivieren von Stretch Database für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
