---
title: Spalten (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMNS
- COLUMNS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS view
- INFORMATION_SCHEMA.COLUMNS view
ms.assetid: bbf7ac4a-7444-4351-a590-a9f71e0bc495
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 021e9e66b281a8bbca6d5c9e21e78ffa4069c5c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "67950797"
---
# <a name="columns-transact-sql"></a>COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jede Spalte zurück, auf die vom aktuellen Benutzer in der aktuellen Datenbank zugegriffen werden kann.  
  
 Zum Abrufen von Informationen aus diesen Sichten geben Sie den voll qualifizierten Namen **INFORMATION_SCHEMA**_. view_name_an.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Tabellenqualifizierer|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Der Name des Schemas, das die Tabelle enthält.<br /><br /> **&#42;&#42; wichtige &#42;&#42;** Verwenden Sie INFORMATION_SCHEMA Sichten nicht, um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|Tabellenname.|  
|**COLUMN_NAME**|**nvarchar (** 128 **)**|Spaltenname.|  
|**ORDINAL_POSITION**|**int**|Identifikationsnummer der Spalte|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|Standardwert der Spalte|  
|**IS_NULLABLE**|**varchar (** 3 **)**|NULL-Zulässigkeit der Spalte. Ist NULL in dieser Spalte zulässig, wird für diese Spalte YES zurückgegeben. Andernfalls wird NO zurückgegeben.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|Vom System bereitgestellter Datentyp|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Maximale Länge (in Zeichen) für binäre Daten, Zeichendaten, Text- und Tmage-Daten<br /><br /> -1 für **XML** -Daten und Daten mit umfangreichen Werten. Andernfalls wird NULL zurückgegeben. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Maximale Länge (in Bytes) für binäre Daten, Zeichendaten, Text- und Image-Daten.<br /><br /> -1 für **XML** -Daten und Daten mit umfangreichen Werten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_PRECISION**|**tinyint**|Genauigkeit für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Basis der Genauigkeit für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_SCALE**|**int**|Anzahl der Dezimalstellen für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**DATETIME_PRECISION**|**smallint**|Untertyp Code für **DateTime** -und ISO- **Intervall** Datentypen. Für andere Datentypen wird NULL zurückgegeben.|  
|**CHARACTER_SET_CATALOG**|**nvarchar (** 128 **)**|Gibt **Master**zurück. Gibt die Datenbank an, in der sich der Zeichensatz befindet, wenn die Spalte Zeichendaten oder **Text** Datentyp ist. Andernfalls wird NULL zurückgegeben.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar (** 128 **)**|Gibt immer NULL zurück.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|Gibt den eindeutigen Namen für den Zeichensatz zurück, wenn diese Spalte Zeichendaten oder **Text** Datentyp ist. Andernfalls wird NULL zurückgegeben.|  
|**COLLATION_CATALOG**|**nvarchar (** 128 **)**|Gibt immer NULL zurück.|  
|**COLLATION_SCHEMA**|**nvarchar (** 128 **)**|Gibt immer NULL zurück.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|Gibt den eindeutigen Namen für die Sortierung zurück, wenn die Spalte Zeichendaten oder **Text** Datentyp ist. Andernfalls wird NULL zurückgegeben.|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|Falls die Spalte Daten des Aliastyps enthält, wird in dieser Spalte der Name der Datenbank angezeigt, in der der benutzerdefinierte Datentyp erstellt wurde. Andernfalls wird NULL zurückgegeben.|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|Falls die Spalte Daten eines benutzerdefinierten Typs enthält, gibt diese Spalte den Namen des Schemas des benutzerdefinierten Datentyps zurück. Andernfalls wird NULL zurückgegeben.<br /><br /> **&#42;&#42; wichtige &#42;&#42;** Verwenden Sie INFORMATION_SCHEMA Sichten nicht, um das Schema eines Datentyps zu bestimmen. Die einzige zuverlässige Möglichkeit zum Finden des Schemas eines Typs besteht darin, die TYPEPROPERTY-Funktion zu verwenden.|  
|**DOMAIN_NAME**|**nvarchar (** 128 **)**|Falls die Spalte Daten eines benutzerdefinierten Typs enthält, wird in dieser Spalte der Name des benutzerdefinierten Datentyps angezeigt. Andernfalls wird NULL zurückgegeben.|  
  
## <a name="remarks"></a>Bemerkungen  
 Die **ORDINAL_POSITION** Spalte des **INFORMATION_SCHEMA. Die Spalten** Ansicht ist nicht mit dem Bitmuster von Spalten kompatibel, die von der COLUMNS_UPDATED-Funktion zurückgegeben werden. Wenn Sie ein Bitmuster abrufen möchten, das mit COLUMNS_UPDATED kompatibel ist, müssen Sie beim Abfragen der INFORMATION_SCHEMA auf die **ColumnID** -Eigenschaft der COLUMNPROPERTY-Systemfunktion verweisen **. Spalten** Ansicht. Beispiel:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [System Sichten &#40;Transact-SQL-&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informations Schema Sichten &#40;Transact-SQL-&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys. syscharsets &#40;Transact-SQL-&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys. Columns &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys. Konfigurationen &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. types &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact-SQL-&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
  
