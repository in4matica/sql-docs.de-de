---
title: sys. key_encryptions (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.key_encryptions
- key_encryptions_TSQL
- sys.key_encryptions_TSQL
- key_encryptions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_encryptions catalog view
ms.assetid: c39cecf8-af63-40b9-98e5-f84a5bf3ae54
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 61ad8e163eddb4875aad362c3090875bd450bc3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104592"
---
# <a name="syskey_encryptions-transact-sql"></a>sys.key_encryptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Verschlüsselung mit einem symmetrischen Schlüssel zurück, die mit der ENCRYPTION BY-Klausel der CREATE SYMMETRIC KEY-Anweisung angegeben ist.  

  
|Spaltennamen|Datentypen|BESCHREIBUNG|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|ID des verschlüsselten Schlüssels.|  
|**thumbprint**|**varbinary (32)**|SHA-1-Hash des Zertifikats, mit dem der Schlüssel verschlüsselt wird, oder der GUID des symmetrischen Schlüssels, mit dem der Schlüssel verschlüsselt wird.|  
|**crypt_type**|**char (4)**|Verschlüsselungstyp:<br /><br /> ESKS = Verschlüsselt mit symmetrischem Schlüssel<br /><br /> ESKP, ESP2 oder ESP3 = durch Kennwort verschlüsselt<br /><br /> EPUC = Verschlüsselt mit Zertifikat<br /><br /> EPUA = Verschlüsselt mit asymmetrischem Schlüssel<br /><br /> ESKM = Verschlüsselt mit Hauptschlüssel|  
|**crypt_type_desc**|**nvarchar (60)**|Beschreibung des Verschlüsselungstyps:<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(Ab enthält [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)]eine Versionsnummer, die von CSS verwendet werden kann.)<br /><br /> ENCRYPTION BY CERTIFICATE<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> Hinweis: Windows DPAPI wird verwendet, um den Dienst Hauptschlüssel zu schützen.|  
|**crypt_property**|**varbinary(max)**|Signierte oder verschlüsselte Bits.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Weitere Informationen  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
