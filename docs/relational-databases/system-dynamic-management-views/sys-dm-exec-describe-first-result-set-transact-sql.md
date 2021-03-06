---
title: sys. dm_exec_describe_first_result_set (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_describe_first_result_set
- sys.dm_exec_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_describe_first_result_set catalog view
ms.assetid: 6ea88346-0bdb-4f0e-9f1f-4d85e3487d23
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 523a94718f123fab9d501de9497ca5ecc2b09c95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097816"
---
# <a name="sysdm_exec_describe_first_result_set-transact-sql"></a>sys.dm_exec_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Diese dynamische Verwaltungsfunktion übernimmt eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung als Parameter und beschreibt die Metadaten des ersten Resultsets für die-Anweisung.  
  
 **sys. dm_exec_describe_first_result_set** hat dieselbe resultsetdefinition wie [sys. dm_exec_describe_first_result_set_for_object &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md) und ähnelt [sp_describe_first_result_set &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  

 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol für Themenlink") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_exec_describe_first_result_set(@tsql, @params, @include_browse_information)  
```  
  
## <a name="arguments"></a>Argumente  
 *\@TSQL*  
 Eine oder mehrere [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen. *Transact-SQL_batch* kann vom Datentyp **nvarchar (***n***)** oder **nvarchar (max)** sein.  
  
 *\@params*  
 \@Parameter stellt eine Deklarations Zeichenfolge für Parameter [!INCLUDE[tsql](../../includes/tsql-md.md)] für den Batch bereit, ähnlich wie sp_executesql. Parameter können **nvarchar (n)** oder **nvarchar (max)** sein.  
  
 Ist eine Zeichenfolge, die die Definitionen aller Parameter enthält, die in die [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*eingebettet wurden. Die Zeichenfolge muss eine Unicode-Konstante oder eine Unicode-Variable sein. Jede Parameterdefinition besteht aus einem Parameternamen und einem Datentyp. *n* ist ein Platzhalter, der zusätzliche Parameter Definitionen angibt. Jeder in stmt angegebene Parameter muss in \@params definiert werden. Wenn die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung oder der-Batch in der Anweisung keine Parameter \@enthält, ist die Angabe von Parametern nicht erforderlich. Der Standardwert für diesen Parameter ist NULL.  
  
 *\@include_browse_information*  
 Bei 1 werden alle Abfragen so analysiert, als ob die FOR BROWSE-Option in der Abfrage enthalten wäre. Zusätzliche Schlüsselspalten und Quelltabelleninformationen werden zurückgegeben.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
 Diese gemeinsamen Metadaten werden als Resultset zurückgegeben. In den Ergebnismetadaten sind in einer Zeile pro Spalte der Typ und die NULL-Zulässigkeit der Spalte in dem in der folgenden Tabelle dargestellten Format beschrieben. Wenn die erste Anweisung nicht für alle Steuerelementpfade vorhanden ist, wird ein Resultset mit 0 Zeilen zurückgegeben.  
  
|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit**|Gibt an, dass es sich bei der Spalte um eine zusätzliche Spalte zum Suchen und für Informationszwecke handelt, die nicht im Resultset angezeigt wird.|  
|**column_ordinal**|**int**|Enthält die Ordnungsposition der Spalte im Resultset. Die Position der ersten Spalte wird mit 1 angegeben.|  
|**name**|**sysname**|Enthält den Namen der Spalte, wenn ein Name bestimmt werden kann. Enthält andernfalls NULL.|  
|**is_nullable**|**bit**|Enthält die folgenden Werte:<br /><br /> Wert 1, wenn die Spalte NULL-Werte zulässt.<br /><br /> Wert 0, wenn die Spalte keine NULL-Werte zulässt.<br /><br /> Wert 1, wenn nicht bestimmt werden kann, ob die Spalte NULL-Werte zulässt.|  
|**system_type_id**|**int**|Enthält die system_type_id des Spalten Datentyps, wie in sys. types angegeben. Bei CLR-Typen wird von dieser Spalte der Wert 240 zurückgegeben, obwohl von der system_type_name-Spalte NULL zurückgegeben wird.|  
|**system_type_name**|**nvarchar(256)**|Enthält den Namen und die Argumente (z. B. Länge, Genauigkeit oder Skala), die für den Datentyp der Spalte angegeben wurden.<br /><br /> Wenn es sich bei dem Datentyp um einen benutzerdefinierten Aliastyp handelt, wird hier der zugrunde liegende Systemtyp angegeben.<br /><br /> Wenn es sich bei dem Datentyp um einen benutzerdefinierten CLR-Typ handelt, wird in dieser Spalte NULL zurückgegeben.|  
|**max_length**|**smallint**|Maximale Länge (in Byte) für die Spalte.<br /><br /> -1 = der Spaltendatentyp ist **varchar (max)**, **nvarchar (max)**, **varbinary (max)** oder **XML**.<br /><br /> Bei **Text** Spalten ist der **max_length** Wert 16 oder der Wert, der durch **sp_tableoption ' Text in row '** festgelegt wird.|  
|**precision**|**tinyint**|Die Genauigkeit der Spalte, wenn sie auf numerischen Werten basiert. Andernfalls wird 0 zurückgegeben.|  
|**scale**|**tinyint**|Die Skalierung der Spalte, wenn sie auf numerischen Werten basiert. Andernfalls wird 0 zurückgegeben.|  
|**collation_name**|**sysname**|Name der Sortierung der Spalte, wenn diese zeichenbasiert ist. Andernfalls wird NULL zurückgegeben.|  
|**user_type_id**|**int**|Enthält bei CLR- und Aliastypen die user_type_id des Datentyps der Spalte, wie in sys.types angegeben. Andernfalls NULL.|  
|**user_type_database**|**sysname**|Enthält bei CLR- und Aliastypen den Namen der Datenbank, in der der Typ definiert wurde. Andernfalls NULL.|  
|**user_type_schema**|**sysname**|Enthält bei CLR- und Aliastypen den Namen des Schemas, in dem der Typ definiert wurde. Andernfalls NULL.|  
|**user_type_name**|**sysname**|Enthält bei CLR- und Aliastypen den Namen des Typs. Andernfalls NULL.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|Gibt bei CLR-Typen den Namen der Assembly und der Klasse zurück, die den Typ definieren. Andernfalls NULL.|  
|**xml_collection_id**|**int**|Enthält die xml_collection_id des Datentyps für die Spalte, wie in sys.columns angegeben. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML-Schemaauflistung zugeordnet ist.|  
|**xml_collection_database**|**sysname**|Enthält die Datenbank, in der die XML-Schemaauflistung definiert ist, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML-Schemaauflistung zugeordnet ist.|  
|**xml_collection_schema**|**sysname**|Enthält das Schema, in dem die XML-Schemaauflistung definiert ist, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML-Schemaauflistung zugeordnet ist.|  
|**xml_collection_name**|**sysname**|Enthält den Namen der XML-Schemaauflistung, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML-Schemaauflistung zugeordnet ist.|  
|**is_xml_document**|**bit**|Gibt 1 zurück, wenn der zurückgegebene Datentyp XML ist und für diesen Typ garantiert ist, dass es sich um ein vollständiges XML-Dokument (einschließlich eines Stammknotens) handelt, nicht um ein XML-Fragment. Andernfalls wird 0 zurückgegeben.|  
|**is_case_sensitive**|**bit**|Gibt 1 zurück, wenn die Spalte von einem string-Typ ist, bei dem die Groß-/Kleinschreibung beachtet wird. Andernfalls wird 0 zurückgegeben.|  
|**is_fixed_length_clr_type**|**bit**|Gibt 1 zurück, wenn die Spalte von einem CLR-Typ mit fester Länge ist. Andernfalls wird 0 zurückgegeben.|  
|**source_server**|**sysname**|Name des ursprünglichen Servers (bei Ursprung auf einem Remoteserver). Der Name wird wie in sys. Servers angezeigt. Gibt NULL zurück, wenn die Spalte vom lokalen Server stammt oder der ursprüngliche Server nicht ermittelt werden konnte. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**source_database**|**sysname**|Der Name der ursprünglichen Datenbank, die von der Spalte in diesem Ergebnis zurückgegeben wird. Gibt NULL zurück, wenn die Datenbank nicht ermittelt werden kann. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**source_schema**|**sysname**|Der Name des ursprünglichen Schemas, das von der Spalte in diesem Ergebnis zurückgegeben wird. Gibt NULL zurück, wenn das Schema nicht bestimmt werden kann. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**source_table**|**sysname**|Der Name der ursprünglichen Tabelle, die von der Spalte in diesem Ergebnis zurückgegeben wird. Gibt NULL zurück, wenn die Tabelle nicht bestimmt werden kann. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**source_column**|**sysname**|Der Name der ursprünglichen Spalte, die von der Ergebnisspalte zurückgegeben wird. Gibt NULL zurück, wenn die Spalte nicht bestimmt werden kann. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**is_identity_column**|**bit**|Gibt 1 zurück, wenn die Spalte eine Identitätsspalte ist, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte eine Identitätsspalte ist.|  
|**is_part_of_unique_key**|**bit**|Gibt 1 zurück, wenn die Spalte Teil eines eindeutigen Index (einschließlich UNIQUE- und PRIMARY-Einschränkungen) ist, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte Teil eines eindeutigen Indexes ist. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**is_updateable**|**bit**|Gibt 1 zurück, wenn die Spalte aktualisiert werden kann, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte aktualisiert werden kann.|  
|**is_computed_column**|**bit**|Gibt 1 zurück, wenn die Spalte eine berechnete Spalte, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob es sich um eine berechnete Spalte handelt.|  
|**is_sparse_column_set**|**bit**|Gibt 1 zurück, wenn die Spalte eine Sparsespalte ist, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte Teil eines Sparsespaltensatzes ist.|  
|**ordinal_in_order_by_list**|**smallint**|Die Position dieser Spalte ist in der ORDER BY-Liste. Gibt NULL zurück, wenn die Spalte nicht in der ORDER BY-Liste angezeigt wird oder die ORDER BY-Liste nicht eindeutig bestimmt werden kann.|  
|**order_by_list_length**|**smallint**|Die Länge der ORDER BY-Liste. NULL wird zurückgegeben, wenn keine ORDER BY-Liste vorhanden ist die ORDER BY-Liste nicht eindeutig bestimmt werden kann. Beachten Sie, dass dieser Wert für alle von sp_describe_first_result_set zurückgegebenen Zeilen gleich ist.|  
|**order_by_is_descending**|**smallint NULL**|Wenn ordinal_in_order_by_list nicht NULL ist, wird von der **order_by_is_descending**-Spalte die Richtung der ORDER BY-Klausel für diese Spalte gemeldet. Andernfalls wird NULL gemeldet.|  
|**error_number**|**int**|Enthält die von der Funktion zurückgegebene Fehlernummer. Wenn kein Fehler aufgetreten ist, enthält die Spalte NULL.|  
|**error_severity**|**int**|Enthält den von der Funktion zurückgegebenen Schweregrad. Wenn kein Fehler aufgetreten ist, enthält die Spalte NULL.|  
|**error_state**|**int**|Enthält die Statusmeldung, die von der Funktion zurückgegeben wird. Wenn kein Fehler aufgetreten ist, enthält die Spalte NULL.|  
|**error_message**|**nvarchar (4096)**|Enthält die von der Funktion zurückgegebene Meldung. Wenn kein Fehler aufgetreten ist, enthält die Spalte NULL.|  
|**error_type**|**int**|Enthält eine ganze Zahl, die den zurückgegebenen Fehler darstellt. Wird error_type_desc zugeordnet. Siehe Liste unter Hinweisen.|  
|**error_type_desc**|**nvarchar (60)**|Enthält eine kurze Zeichenfolge in Großbuchstaben, die den zurückgegebenen Fehler darstellt. Wird error_type zugeordnet. Siehe Liste unter Hinweisen.|  
  
## <a name="remarks"></a>Bemerkungen  
 Diese Funktion verwendet den gleichen Algorithmus wie **sp_describe_first_result_set**. Weitere Informationen finden Sie unter [sp_describe_first_result_set &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
 In der folgenden Tabelle werden die Fehlertypen und deren Beschreibungen aufgeführt.  
  
|error_type|error_type|BESCHREIBUNG|  
|-----------------|-----------------|-----------------|  
|1|MISC|Alle Fehler, die nicht anderweitig beschrieben sind.|  
|2|SYNTAX|Im Batch ist ein Syntaxfehler aufgetreten.|  
|3|CONFLICTING_RESULTS|Das Ergebnis konnte wegen eines Konflikts zwischen zwei möglichen ersten Anweisungen nicht ermittelt werden.|  
|4|DYNAMIC_SQL|Das Ergebnis konnte wegen einer dynamischen SQL-Abfrage nicht ermittelt werden, die potenziell das erste Ergebnis zurückgeben kann.|  
|5|CLR_PROCEDURE|Das Ergebnis konnte nicht ermittelt werden, da eine gespeicherte CLR-Prozedur potenziell das erste Ergebnis zurückgeben kann.|  
|6|CLR_TRIGGER|Das Ergebnis konnte wegen eines dynamischen CLR-Triggers nicht ermittelt werden, der potenziell das erste Ergebnis zurückgeben kann.|  
|7|EXTENDED_PROCEDURE|Das Ergebnis konnte nicht ermittelt werden, da eine erweiterte gespeicherte Prozedur potenziell das erste Ergebnis zurückgeben kann.|  
|8|UNDECLARED_PARAMETER|Das Ergebnis konnte nicht bestimmt werden, da der Datentyp von mindestens einer der Spalten des Resultsets potenziell von einem nicht deklarierten Parameter abhängt.|  
|9|RECURSION|Das Ergebnis konnte nicht ermittelt werden, da der Batch eine rekursive Anweisung enthält.|  
|10|TEMPORARY_TABLE|Das Ergebnis konnte nicht ermittelt werden, da der Batch eine temporäre Tabelle enthält und von **sp_describe_first_result_set** nicht unterstützt wird.|  
|11|UNSUPPORTED_STATEMENT|Das Ergebnis konnte nicht ermittelt werden, da der Batch eine Anweisung enthält, die von **sp_describe_first_result_set** (z. B., FETCH, REVERT usw.) nicht unterstützt wird.|  
|12|OBJECT_TYPE_NOT_SUPPORTED|Das \@an die Funktion über gegebene object_id wird nicht unterstützt (d. h. keine gespeicherte Prozedur).|  
|13|OBJECT_DOES_NOT_EXIST|Das \@an die Funktion über gegebene object_id wurde im System Katalog nicht gefunden.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigung zum Ausführen \@des "parql"-Arguments.  
  
## <a name="examples"></a>Beispiele  
 Weitere Beispiele im Thema [sp_describe_first_result_set &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) können für die Verwendung von **sys. dm_exec_describe_first_result_set**angepasst werden.  
  
### <a name="a-returning-information-about-a-single-transact-sql-statement"></a>A. Zurückgeben von Informationen zu einer einzelnen Transact-SQL-Anweisung  
 Im folgenden Code werden Informationen zu den Ergebnissen einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_exec_describe_first_result_set  
(N'SELECT object_id, name, type_desc FROM sys.indexes', null, 0) ;  
```  
  
### <a name="b-returning-information-about-a-procedure"></a>B. Zurückgeben von Informationen zu einer Prozedur  
 Im folgenden Beispiel wird eine gespeicherte Prozedur mit dem Namen pr_TestProc erstellt, die zwei Resultsets zurückgibt. Anschließend wird im Beispiel veranschaulicht, dass **sys.dm_exec_describe_first_result_set** Informationen zum ersten Resultset in der Prozedur zurückgibt.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE PROC Production.TestProc  
AS  
SELECT Name, ProductID, Color FROM Production.Product ;  
SELECT Name, SafetyStockLevel, SellStartDate FROM Production.Product ;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set  
('Production.TestProc', NULL, 0) ;  
```  
  
### <a name="c-returning-metadata-from-a-batch-that-contains-multiple-statements"></a>C. Zurückgeben von Metadaten von einem Batch mit mehreren Anweisungen  
 Im folgenden Beispiel wird ein Batch mit zwei [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen ausgewertet. Das Resultset beschreibt das erste zurückgegebene Resultset.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set(  
N'SELECT CustomerID, TerritoryID, AccountNumber FROM Sales.Customer WHERE CustomerID = @CustomerID;  
SELECT * FROM Sales.SalesOrderHeader;',  
N'@CustomerID int', 0) AS a;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [sp_describe_first_result_set &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sp_describe_undeclared_parameters &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys. dm_exec_describe_first_result_set_for_object &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
  
  
