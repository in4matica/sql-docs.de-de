---
title: DENY (Schemaberechtigungen) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [SQL Server], schemas
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
- DENY statement, schemas
ms.assetid: 300a67c4-d226-4653-9e9f-7ae4d53fcf33
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bd439e528cc30c0971d1b4c824ab2375856d26e3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "68114789"
---
# <a name="deny-schema-permissions-transact-sql"></a>DENY-Schemaberechtigungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Verweigert die Berechtigungen für ein Schema.  
  

![Artikellinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Artikellinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql
DENY permission  [ ,...n ] } ON SCHEMA :: schema_name  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
*permission*  
Gibt eine Berechtigung an, die für ein Schema verweigert werden kann. Eine Liste dieser Berechtigungen finden Sie unter „Hinweise“ weiter unten in diesem Artikel.  
  
ON SCHEMA **::** schema *_name*  
Gibt das Schema an, für das die Berechtigung verweigert wird. Der Bereichsqualifizierer **::** ist erforderlich.  
  
*database_principal*  
Gibt den Prinzipal an, für den die Berechtigung verweigert wird. *database_principal* kann die folgenden Prinzipale aufweisen:  
  
-   Datenbankbenutzer  
-   Datenbankrolle  
-   Anwendungsrolle  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
CASCADE  
verweigert die Berechtigung für andere Prinzipale, für die das angegebene Argument *database_principal* die Berechtigung erteilt hat.
  
*denying_principal*  
Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, das Recht zum Verweigern der Berechtigung ableitet. *denying_principal* kann die folgenden Prinzipale aufweisen:  
  
-   Datenbankbenutzer  
-   Datenbankrolle  
-   Anwendungsrolle  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
## <a name="remarks"></a>Bemerkungen  
Ein Schema ist ein sicherungsfähiges Element auf Datenbankebene. Es ist in der Datenbank enthalten, die in der Berechtigungshierarchie übergeordnet ist. Die spezifischsten und restriktivsten Berechtigungen, die für ein Schema verweigert werden können, sind in der folgenden Tabelle aufgeführt. Die Tabelle zeigt allgemeinere Berechtigungen, die andere Berechtigungen implizit enthalten.  
  
|Schemaberechtigung|Impliziert durch die Schemaberechtigung|Impliziert durch Datenbankberechtigung|  
|-----------------------|----------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SCHEMA|  
|CONTROL|CONTROL|CONTROL|  
|CREATE SEQUENCE|ALTER|ALTER ANY SCHEMA|  
|Delete|CONTROL|Delete|  
|Führen Sie|CONTROL|Führen Sie|  
|INSERT|CONTROL|INSERT|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|CONTROL|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die CONTROL-Berechtigung für das Schema. Falls die AS-Option verwendet wird, muss der angegebene Prinzipal das Schema besitzen.  
  
## <a name="see-also"></a>Weitere Informationen  
[CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
[DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
[Berechtigungen &#40;Datenbank-Engine&#41;](../../relational-databases/security/permissions-database-engine.md)   
[Prinzipale &#40;Datenbank-Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
[sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
[HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
