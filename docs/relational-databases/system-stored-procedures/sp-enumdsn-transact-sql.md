---
title: sp_enumdsn (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: stevestein
ms.author: sstein
ms.openlocfilehash: d84d366483cd5a887eb299b0f8d9208998e835c1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124589"
---
# <a name="sp_enumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Liste aller definierten ODBC- und OLE DB-Datenquellennamen für einen Server zurück, der unter einem bestimmten [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Benutzerkonto ausgeführt wird. Diese gespeicherte Prozedur wird auf dem Verleger für jede Datenbank ausgeführt.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol für Themenlink") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**Datenquellen Name**|**sysname**|Name der Datenquelle.|  
|**Beschreibung**|**varchar (255)**|Beschreibung der Datenquelle.|  
|**Typ**|**int**|Typ der Datenquelle:<br /><br /> **1** = ODBC-DSN<br /><br /> **3** = OLE DB Datenquelle|  
|**Anbieter Name**|**varchar (255)**|Name des OLE DB-Anbieters. Der Wert ist NULL für einen ODBC-DSN.|  
  
## <a name="remarks"></a>Bemerkungen  
 Jeder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Dienst verfügt über einen Benutzer Kontext. Dabei handelt es sich um eine Gruppe von Registrierungseinträgen, die Definitionen der ODBC-Datenquellen für den Benutzer enthält. Der Benutzerkontext ergibt sich aus dem Benutzernamen, unter dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.  
  
 Wenn beispielsweise der Server unter dem Benutzerkontext des Systemkontos ausgeführt wird, werden alle diesem Konto zugeordneten System-DSNs gemeldet. Wird der Server unter einem privaten Benutzerkonto ausgeführt, so werden nur die für dieses Konto definierten DSNs zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Server Rolle **sysadmin** können **sp_enumdsn**ausführen.  
  
## <a name="see-also"></a>Weitere Informationen  
 [sp_dsninfo &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
