---
title: TRIM (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azure-sqldw-latest||=azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9707f0b23d9461418536c2b9f9015623124d5436
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "70059841"
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-asdw-xxx-md.md)]

Entfernt das Leerzeichen `char(32)` oder andere am Beginn und Ende einer Zeichenfolge angegebene Zeichen.  

## <a name="syntax"></a>Syntax

```
-- Syntax for SQL Server and Azure SQL Database
TRIM ( [ characters FROM ] string )
```

```
-- Syntax for Azure SQL Data Warehouse
TRIM ( string )
```

## <a name="arguments"></a>Argumente

Bei „characters“ handelt es sich um ein Literal, eine Variable oder ein Funktionsaufruf eines beliebigen Zeichentyps, der sich nicht auf eine Branchenanwendung bezieht (`nvarchar`, `varchar`, `nchar` oder `char`), mit Zeichen, die entfernt werden sollten. Die Typen `nvarchar(max)` und `varchar(max)` sind nicht zulässig.

„string“ ist ein Ausdruck eines beliebigen Zeichentyps (`nvarchar`, `varchar`, `nchar` oder `char`), aus dem Zeichen entfernt werden sollten.

## <a name="return-types"></a>Rückgabetypen

Gibt einen Zeichenausdruck mit einem Zeichenargumenttyp zurück, aus dem das Leerzeichen `char(32)` oder andere angegebene Zeichenfolgen auf beiden Seiten entfernt werden sollen. Gibt `NULL` zurück, wenn die Eingabezeichenfolge `NULL` ist.

## <a name="remarks"></a>Bemerkungen

Standardmäßig entfernt die `TRIM`-Funktion das Leerzeichen sowohl am Anfang als auch am Ende der Zeichenfolge. Dieses Verhalten entspricht `LTRIM(RTRIM(@string))`.

## <a name="examples"></a>Beispiele

### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  Entfernt die Leerzeichen auf beiden Seiten der Zeichenfolge.

Das folgende Beispiel entfernt Leerzeichen vor und nach dem Wort `test`.

```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

```
test
```

### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  Entfernt angegebene Zeichen von beiden Seiten der Zeichenfolge

Das folgende Beispiel entfernt einen nachstehenden Punkt und Leerzeichen vor `#` und nach dem Wort `test`.

```sql
SELECT TRIM( '.,! ' FROM  '     #     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
#     test
```

## <a name="see-also"></a>Weitere Informationen

 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/string-functions-transact-sql.md)
