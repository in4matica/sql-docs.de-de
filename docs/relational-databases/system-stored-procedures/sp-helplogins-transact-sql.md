---
title: sp_helplogins (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
author: stevestein
ms.author: sstein
ms.openlocfilehash: b4c3d6ded5d85e5d38556792aaa7ea71dd9f42fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68122452"
---
# <a name="sp_helplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt Informationen zu Anmeldenamen und den zugeordneten Benutzern in jeder Datenbank bereit.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol für Themenlink") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @LoginNamePattern = ] 'login'`Ein Anmelde Name. *Login* ist vom **Datentyp vom Datentyp sysname**und hat den Standardwert NULL. der *Anmelde* Name muss vorhanden sein, wenn angegeben. Falls *login* nicht angegeben wird, werden Informationen zu allen Anmeldenamen zurückgegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 „0“ (erfolgreich) oder „1“ (fehlerhaft)  
  
## <a name="result-sets"></a>Resultsets  
 Der erste Bericht enthält Informationen zu allen angegebenen Anmeldenamen (siehe folgende Tabelle).  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Benutzername|  
|**SID**|**varbinary(85)**|Sicherheits-ID (SID) für den Anmeldenamen.|  
|**DefDBName**|**sysname**|Standarddatenbank, die **LoginName** beim Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet.|  
|**DefLangName**|**sysname**|Von **LoginName**verwendete Standardsprache.|  
|**Auser**|**char (5)**|Yes = **LoginName** ist ein Benutzername in einer Datenbank zugeordnet.<br /><br /> No = **LoginName** ist kein Benutzername zugeordnet.|  
|**ARemote**|**char (7)**|Yes = **LoginName** ist ein Remoteanmeldename zugeordnet.<br /><br /> No = **LoginName** ist kein Anmeldename zugeordnet.|  
  
 Der zweite Bericht enthält Informationen zu den Benutzern, die den jeweiligen Anmeldenamen zugeordnet sind, und zu den Rollenmitgliedschaften des Anmeldenamens, wie in der folgenden Tabelle dargestellt.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Benutzername|  
|**DBName**|**sysname**|Standarddatenbank, die **LoginName** beim Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet.|  
|**User**|**sysname**|Benutzerkonto, dem **LoginName** in **DBName**zugeordnet ist, und die Rollen, denen **LoginName** in **DBName**angehört.|  
|**UserOrAlias**|**char (8)**|MemberOf = **UserName** ist eine Rolle.<br /><br /> User = **UserName** ist ein Benutzerkonto.|  
  
## <a name="remarks"></a>Bemerkungen  
 Bestimmen Sie mithilfe von **sp_helplogins** die Benutzerkonten, die dem Anmeldenamen zugeordnet sind, bevor Sie Anmeldenamen entfernen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Server Rolle **securityadmin** .  
  
 
  **sp_helplogins** muss alle Datenbanken auf dem Server überprüfen, um alle Benutzerkonten zu identifizieren, die einem bestimmten Anmeldenamen zugeordnet sind. Deshalb muss für jede Datenbank auf dem Server mindestens eine der folgenden Bedingungen zutreffen:  
  
-   Der Benutzer, der **sp_helplogins** ausführt, verfügt über die Berechtigung für den Zugriff auf die Datenbank.  
  
-   Das Benutzerkonto **guest** ist in der Datenbank aktiviert.  
  
 Falls **sp_helplogins** nicht auf eine Datenbank zugreifen kann, gibt **sp_helplogins** so viele Informationen wie möglich zurück und zeigt die Fehlermeldung 15622 an.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zum Anmeldenamen `John`zurückgegeben.  
  
```  
EXEC sp_helplogins 'John';  
GO  
  
LoginName SID                        DefDBName DefLangName AUser ARemote   
--------- -------------------------- --------- ----------- ----- -------   
John      0x23B348613497D11190C100C  master    us_english  yes   no  
  
(1 row(s) affected)  
  
LoginName   DBName   UserName   UserOrAlias   
---------   ------   --------   -----------   
John        pubs     John       User          
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Gespeicherte Sicherheits Prozeduren &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
