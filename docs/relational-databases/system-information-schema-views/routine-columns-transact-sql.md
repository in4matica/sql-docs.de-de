---
title: ROUTINE_COLUMNS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- ROUTINE_COLUMNS_TSQL
- ROUTINE_COLUMNS
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINE_COLUMNS view
- INFORMATION_SCHEMA.ROUTINE_COLUMNS view
ms.assetid: 91dbc61b-e4c0-4826-976c-b2fce88b7793
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b0ed500b1217ae70dca72ab6eab64ab661c22ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078527"
---
# <a name="routine_columns-transact-sql"></a>ROUTINE_COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Spalte, die von den Tabellenwertfunktionen zurückgegeben wird, auf die der aktuelle Benutzer in der aktuellen Datenbank zugreifen kann.  
  
 Zum Abrufen von Informationen aus dieser Ansicht geben Sie den voll qualifizierten Namen **INFORMATION_SCHEMA an.** _view_name_.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Katalog- oder Datenbankname der Tabellenwertfunktion|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Name des Schemas, das die Tabellenwertfunktion enthält<br /><br /> <strong> \* Wichtig \* \* </strong> Verwenden Sie INFORMATION_SCHEMA Sichten nicht, um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|Name der Tabellenwertfunktion|  
|**COLUMN_NAME**|**nvarchar (** 128 **)**|Spaltenname.|  
|**ORDINAL_POSITION**|**int**|Identifikationsnummer der Spalte|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|Standardwert der Spalte|  
|**IS_NULLABLE**|**varchar (** 3 **)**|Ist NULL in dieser Spalte zulässig, wird YES zurückgegeben. Andernfalls wird No zurückgegeben.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|Vom System bereitgestellter Datentyp|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Maximale Länge (in Zeichen) für binäre Daten, Zeichendaten, Text- und Tmage-Daten<br /><br /> -1 für **XML** -Daten und Daten mit umfangreichen Werten. Andernfalls wird NULL zurückgegeben. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Maximale Länge (in Bytes) für binäre Daten, Zeichendaten, Text- und Image-Daten.<br /><br /> -1 für **XML** -Daten und Daten mit umfangreichen Werten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_PRECISION**|**tinyint**|Genauigkeit für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Basis der Genauigkeit für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_SCALE**|**tinyint**|Anzahl der Dezimalstellen für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**DATETIME_PRECISION**|**smallint**|Untertyp Code für **DateTime** -und ISO-**ganzzahlige** Datentypen. Bei anderen Datentypen wird NULL zurückgegeben.|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|Gibt **Master**zurück. Dies gibt die Datenbank an, in der sich der Zeichensatz befindet, wenn die Spalte Zeichendaten oder **Text** Datentyp ist. Andernfalls wird NULL zurückgegeben.|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|Gibt immer NULL zurück.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|Gibt den eindeutigen Namen für den Zeichensatz zurück, wenn diese Spalte Zeichendaten oder **Text** Datentyp ist. Andernfalls wird NULL zurückgegeben.|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|Gibt immer NULL zurück.|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|Gibt immer NULL zurück.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|Gibt den eindeutigen Namen für die Sortierreihenfolge zurück, wenn die Spalte Zeichendaten oder **Text** Datentyp ist. Andernfalls wird NULL zurückgegeben.|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|Falls die Spalte Daten des Aliastyps enthält, wird in dieser Spalte der Name der Datenbank angezeigt, in der der benutzerdefinierte Datentyp erstellt wurde. Andernfalls wird NULL zurückgegeben.|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|Falls die Spalte Daten eines benutzerdefinierten Typs enthält, wird in dieser Spalte der Name des Schemas angezeigt, das den benutzerdefinierten Datentyp enthält. Andernfalls wird NULL zurückgegeben.<br /><br /> <strong> \* Wichtig \* \* </strong> Verwenden Sie INFORMATION_SCHEMA Sichten nicht, um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**DOMAIN_NAME**|**nvarchar (** 128 **)**|Falls die Spalte Daten eines benutzerdefinierten Typs enthält, wird in dieser Spalte der Name des benutzerdefinierten Datentyps angezeigt. Andernfalls wird NULL zurückgegeben.|  
  
## <a name="see-also"></a>Weitere Informationen  
 [System Sichten &#40;Transact-SQL-&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informations Schema Sichten &#40;Transact-SQL-&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys. Columns &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
