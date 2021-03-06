---
title: Entladen einer DLL für eine erweiterte gespeicherte Prozedur | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2772c8d6470f9ad6eb5e8b7cadb6dedd136bd48b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63137581"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Entfernen der DLL einer erweiterten gespeicherten Prozedur aus dem Arbeitsspeicher
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Verwenden Sie stattdessen die CLR-Integration.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lädt eine DLL für eine erweiterte gespeicherte Prozedur, sobald ein-Vorgang an eine der Funktionen der dll erfolgt. Die DLL bleibt so lange im Arbeitsspeicher, bis der Server heruntergefahren wird oder der Systemadministrator die DLL mit der DBCC-Anweisung aus dem Arbeitsspeicher entfernt. Beispielsweise entlädt dieser Befehl die Datei " **xp_hello. dll**" und ermöglicht dem Systemadministrator, eine neuere Version dieser Datei in das Verzeichnis zu kopieren, ohne den Server herunterzufahren:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [DBCC dllname &#40;frei&#41; &#40;Transact-SQL-&#41;](/sql/t-sql/database-console-commands/dbcc-dllname-free-transact-sql)  
  
  
