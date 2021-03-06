---
title: Verwenden von benutzerdefinierten Typen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [SQL Server Native Client]
- user-defined types [SQL Server], SQL Server Native Client
- SQL Server Native Client OLE DB provider, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- SQLNCLI, user-defined types
- SQL Server Native Client, user-defined types
- data access [SQL Server Native Client], user-defined types
- ISSCommandWithParameters interface
ms.assetid: e15d8169-3517-4323-9c9e-0f5c34aff7df
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2adbf40b3fe0b0e079198087a47f525d464a41b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68206613"
---
# <a name="using-user-defined-types"></a>Verwenden von benutzerdefinierten Typen
  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] wurden benutzerdefinierte Typen (User-Defined Types, UDTs) eingeführt. UDTs erweitern das SQL-Typsystem, indem sie es ermöglichen, Objekte und benutzerdefinierte Datenstrukturen in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbank zu speichern. UDTs können mehrere Datentypen enthalten und Verhalten zeigen, das sie von den herkömmlichen Aliasdatentypen aus einem einzelnen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Systemdatentyp unterscheidet. UDTs werden in einer beliebigen, von .NET CLR (Common Language Runtime) unterstützten Sprache definiert, die überprüfbaren Code generiert. Dies umfasst Microsoft Visual c#<sup>?</sup> und Visual Basic<sup>??</sup> Investitions. Die Daten werden in Feldern und Eigenschaften einer .NET-Klasse oder -Struktur verfügbar gemacht. Das Verhalten wird durch die Methoden der Klasse oder Struktur definiert.  
  
 Ein UDT kann als Spaltendefinition einer Tabelle, als Variable in einem [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Batch oder als Argument einer [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Funktion oder gespeicherten Prozedur verwendet werden.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB-Anbieter  
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt UDTs als binäre Typen mit Metadateninformationen, die es Ihnen ermöglichen, UDTs als Objekte zu verwalten. UDT-Spalten werden als DBTYPE_UDT verfügbar gemacht, und ihre Metadaten werden über die OLE DB-Kernschnittstelle **IColumnRowset** und die neue [ISSCommandWithParameters](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)-Schnittstelle bereitgestellt.  
  
> [!NOTE]  
>  Die **IRowsetFind::FindNextRow**-Methode funktioniert nicht mit dem UDT-Datentyp. DB_E_BADCOMPAREOP wird zurückgegeben, wenn der UDT als Suchspaltentyp verwendet wird.  
  
### <a name="data-bindings-and-coercions"></a>Datenbindungen und -umwandlungen  
 Die folgende Tabelle veranschaulicht die Bindung und Umwandlung bei Verwendung der aufgeführten Datentypen mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-UDT. UDT-Spalten werden über den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter als DBTYPE_UDT verfügbar gemacht. Die Metadaten können Sie über die entsprechenden Schemarowsets abrufen und so Ihre benutzerdefinierten Typen als Objekte verwalten.  
  
|Datentyp|Zu Server<br /><br /> **UDT**|Zu Server<br /><br /> **nicht-UDT**|Von Server<br /><br /> **UDT**|Von Server<br /><br /> **nicht-UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|Unterstützt<sup>6</sup>|Fehler<sup>1</sup>|Unterstützt<sup>6</sup>|Fehler<sup>5</sup>|  
|DBTYPE_BYTES|Unterstützt<sup>6</sup>|N/V<sup>2</sup>|Unterstützt<sup>6</sup>|N/V<sup>2</sup>|  
|DBTYPE_WSTR|Unterstützt<sup>3, 6</sup>|N/V<sup>2</sup>|Unterstützt<sup>4, 6</sup>|N/V<sup>2</sup>|  
|DBTYPE_BSTR|Unterstützt<sup>3, 6</sup>|N/V<sup>2</sup>|Unterstützt<sup>4</sup>|N/V<sup>2</sup>|  
|DBTYPE_STR|Unterstützt<sup>3, 6</sup>|N/V<sup>2</sup>|Unterstützt<sup>4, 6</sup>|N/V<sup>2</sup>|  
|DBTYPE_IUNKNOWN|Nicht unterstützt|N/V<sup>2</sup>|Nicht unterstützt|N/V<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Unterstützt<sup>6</sup>|N/V<sup>2</sup>|Unterstützt<sup>4</sup>|N/V<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Unterstützt<sup>3, 6</sup>|N/V<sup>2</sup>|–|N/V<sup>2</sup>|  
  
 <sup>1</sup> Wenn ein anderer Servertyp als DBTYPE_UDT mit **ICommandWithParameters:: SetParameterInfo** angegeben wird und der Accessortyp DBTYPE_UDT ist, tritt ein Fehler auf, wenn die Anweisung ausgeführt wird (DB_E_ERRORSOCCURRED, der Parameter Status DBSTATUS_E_BADACCESSOR). Andernfalls werden die Daten an den Server gesendet, der Server gibt jedoch einen Fehler zurück und zeigt an, dass keine implizite Umwandlung des UDT in den Parameterdatentyp erfolgt.  
  
 <sup>2</sup> Über den Rahmen dieses Themas hinaus.  
  
 <sup>3</sup> Datenkonvertierung von hexadezimal Zeichenfolge in binäre Daten erfolgt.  
  
 <sup>4</sup> Datenkonvertierungen von Binärdaten in eine hexadezimale Zeichenfolge.  
  
 <sup>5</sup> Die Validierung kann zum Zeitpunkt der Erstellung der Zugriffsmethode oder zum Abruf Zeitpunkt erfolgen. der Fehler wird DB_E_ERRORSOCCURRED, der Bindungs Status ist auf DBBINDSTATUS_UNSUPPORTEDCONVERSION festgelegt.  
  
 <sup>6</sup> BY_REF können verwendet werden.  
  
 DBTYPE_NULL und DBTYPE_EMPTY können für Eingabeparameter gebunden werden, aber nicht für Ausgabeparameter oder Ergebnisse. Ist der Status für Eingabeparameter gebunden, muss er auf DBSTATUS_S_ISNULL oder DBSTATUS_S_DEFAULT festgelegt werden.  
  
 DBTYPE_UDT kann auch in DBTYPE_EMPTY und DBTYPE_NULL umgewandelt werden, DBTYPE_NULL und DBTYPE_EMPTY können jedoch nicht in DBTYPE_UDT umgewandelt werden. Dies stimmt mit DBTYPE_BYTES überein.  
  
> [!NOTE]  
>  Für den Umgang mit UDTs als Parametern wird eine neue Schnittstelle, **ISSCommandWithParameters**, verwendet, die von **ICommandWithParameters** erbt. Anwendungen müssen diese Schnittstelle verwenden, um mindestens SSPROP_PARAM_UDT_NAME der DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe für UDT-Parameter festzulegen. Andernfalls gibt **ICommand::Execute** DB_E_ERRORSOCCURRED zurück. Diese Schnittstelle und Eigenschaftengruppe werden im weiteren Verlauf dieses Themas erläutert.  
  
 Wird ein UDT in eine Spalte eingefügt, die nicht groß genug für alle Daten ist, gibt **ICommand::Execute** S_OK mit dem Status DB_E_ERRORSOCCURRED zurück.  
  
 Datenkonvertierungen durch OLE DB-Basisdienste (**IDataConvert**) sind nicht auf DBTYPE_UDT anwendbar. Es werden keine weiteren Bindungen unterstützt.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Hinzufügungen und Änderungen am OLE DB-Rowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen an vielen der Kern OLE DB Schemarowsets hinzu.  
  
#### <a name="the-procedure_parameters-schema-rowset"></a>Das PROCEDURE_PARAMETERS-Schemarowset  
 Die folgenden Hinzufügungen wurden am PROCEDURE_PARAMETERS-Schemarowset vorgenommen.  
  
|Spaltenname|type|BESCHREIBUNG|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_NAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Der qualifizierte Name der Assembly mit dem Typnamen und allen zur CLR-Referenzierung erforderlichen Angaben zur Assembly-ID.|  
  
#### <a name="the-sql_assemblies-schema-rowset"></a>Das SQL_ASSEMBLIES-Schemarowset  
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht ein neues Anbieter spezifisches Schemarowset verfügbar, das die registrierten UDTs beschreibt. Der ASSEMBLY-Server wird möglicherweise als DBTYPE_WSTR angegeben, ist aber nicht im Rowset vorhanden. Ohne Angabe wird das Rowset standardmäßig für den aktuellen Server festgelegt. Das SQL_ASSEMBLIES-Schemarowset wird in der folgenden Tabelle definiert.  
  
|Spaltenname|type|BESCHREIBUNG|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Der Katalogname der Assembly, die den Typ enthält.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Der Name des Schemas oder der Eigentümername der Assembly, die den Typ enthält. Obwohl der Bereich einer Assembly durch die Datenbank und nicht durch ein Schema definiert wird, hat sie einen Eigentümer, der hier angegeben wird.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|Der Name der Assembly, die den Typ enthält.|  
|ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der Assembly, die den Typ enthält.|  
|PERMISSION_SET|DBTYPE_WSTR|Ein Wert, der den Zugriffsbereich für die Assembly angibt. Zulässige Werten sind "SAFE", "EXTERNAL_ACCESS" und "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|Die Binärdarstellung der Assembly.|  
  
#### <a name="the-sql_assemblies_-dependencies-schema-rowset"></a>Das SQL_ASSEMBLIES_ DEPENDENCIES-Schemarowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Der Native Client OLE DB-Anbieter macht ein neues Anbieter spezifisches Schemarowset verfügbar, das die Assemblyabhängigkeiten für einen angegebenen Server beschreibt. ASSEMBLY_SERVER wird möglicherweise vom Aufrufer als DBTYPE_WSTR angegeben, ist aber nicht im Rowset vorhanden. Ohne Angabe wird das Rowset standardmäßig für den aktuellen Server festgelegt. Das SQL_ASSEMBLY_DEPENDENCIES-Schemarowset wird in der folgenden Tabelle definiert.  
  
|Spaltenname|type|BESCHREIBUNG|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Der Katalogname der Assembly, die den Typ enthält.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Der Name des Schemas oder der Eigentümername der Assembly, die den Typ enthält. Obwohl der Bereich einer Assembly durch die Datenbank und nicht durch ein Schema definiert wird, hat sie einen Eigentümer, der hier angegeben wird.|  
|ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der Assembly.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der referenzierten Assembly.|  
  
#### <a name="the-sql_user_types-schema-rowset"></a>Das SQL_USER_TYPES-Schemarowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Der Native Client OLE DB-Anbieter macht ein neues Schemarowset, SQL_USER_TYPES, verfügbar, das beschreibt, wann die registrierten UDTs für einen bestimmten Server hinzugefügt werden. UDT_SERVER muss vom Aufrufer als DBTYPE_WSTR angegeben werden, ist aber nicht im Rowset vorhanden. Das SQL_USER_TYPES-Schemarowset wird in der folgenden Tabelle definiert.  
  
|Spaltenname|type|BESCHREIBUNG|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|UDT_NAME|DBTYPE_WSTR|Der Name der Assembly, die die UDT-Klasse enthält.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Vollständiger Typname (AQN) einschließlich Typname mit Namespace als Präfix (falls zutreffend).|  
  
#### <a name="the-columns-schema-rowset"></a>Das COLUMNS-Schemarowset  
 Dem COLUMNS-Schemarowset wurden unter anderem die folgenden Spalten hinzugefügt.  
  
|Spaltenname|type|BESCHREIBUNG|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|SS_UDT_NAME|DBTYPE_WSTR|Der Name des UDT.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Vollständiger Typname (AQN) einschließlich Typname mit Namespace als Präfix (falls zutreffend).|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Hinzufügungen und Änderungen an der OLE DB-Eigenschaftengruppe  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen zu vielen der Kern OLE DB-Eigenschafts Sätzen hinzu.  
  
#### <a name="the-dbpropset_sqlserverparameter-property-set"></a>Die DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe  
 Um UDTs über OLE DB zu unterstützen, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] implementiert Native Client den neuen DBPROPSET_SQLSERVERPARAMETER-Eigenschaften Satz, der die folgenden Werte enthält.  
  
|Name|type|BESCHREIBUNG|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Parametern ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Parametern ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den einteiligen Namen des UDT angibt.|  
  
 SSPROP_PARAM_UDT_NAME ist erforderlich. SSPROP_PARAM_UDT_CATALOGNAME und SSPROP_PARAM_UDT_SCHEMANAME sind optional. Wenn Eigenschaften falsch angegeben werden, wird DB_E_ERRORSINCOMMAND zurückgegeben. Werden weder SSPROP_PARAM_UDT_CATALOGNAME noch SSPROP_PARAM_UDT_SCHEMANAME angegeben, muss der UDT in derselben Datenbank und im selben Schema definiert werden wie die Tabelle. Befindet sich der UDT nicht im selben Schema wie die Tabelle (aber in derselben Datenbank), muss SSPROP_PARAM_UDT_SCHEMANAME angegeben werden. Befindet sich die UDT-Definition in einer anderen Datenbank, müssen SSPROP_PARAM_UDT_CATALOGNAME und SSPROP_PARAM_UDT_SCHEMANAME angegeben werden.  
  
#### <a name="the-dbpropset_sqlservercolumn-property-set"></a>Die DBPROPSET_SQLSERVERCOLUMN-Eigenschaftengruppe  
 Um die Erstellung von Tabellen in der **ITableDefinition** -Schnittstelle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zu unterstützen, fügt Native Client die folgenden drei neuen Spalten dem DBPROPSET_SQLSERVERCOLUMN-Eigenschaften Satz hinzu.  
  
|Name|BESCHREIBUNG|type|BESCHREIBUNG|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|Bei Spalten vom Typ DBTYPE_UDT ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|Bei Spalten vom Typ DBTYPE_UDT ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|Bei Spalten vom Typ DBTYPE_UDT ist diese Eigenschaft eine Zeichenfolge, die den einteiligen Namen des UDT angibt. Für andere Spaltentypen gibt diese Eigenschaft eine leere Zeichenfolge zurück.|  
  
> [!NOTE]  
>  UDTs werden nicht im PROVIDER_TYPES Schemarowset angezeigt. Alle Spalten haben Lese- und Schreibzugriff.  
  
 ADO verweist mit dem entsprechenden Eintrag aus der Beschreibungsspalte auf diese Eigenschaften.  
  
 SSPROP_COL_UDTNAME ist erforderlich. SSPROP_COL_UDT_CATALOGNAME und SSPROP_COL_UDT_SCHEMANAME sind optional. Wenn Eigenschaften falsch angegeben werden, wird `DB_E_ERRORSINCOMMAND` zurückgegeben.  
  
 Werden weder SSPROP_COL_UDT_CATALOGNAME noch SSPROP_COL_UDT_SCHEMANAME angegeben, muss der UDT in derselben Datenbank und im selben Schema definiert werden wie die Tabelle.  
  
 Befindet sich der UDT nicht im selben Schema wie die Tabelle (aber in derselben Datenbank), muss SSPROP_COL_UDT_SCHEMANAME angegeben werden.  
  
 Befindet sich die UDT-Definition in einer anderen Datenbank, müssen SSPROP_COL_UDT_CATALOGNAME und SSPROP_COL_UDT_SCHEMANAME angegeben werden.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Hinzufügungen und Änderungen an der OLE DB-Schnittstelle  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen an vielen der Kern OLE DB-Schnittstellen hinzu.  
  
#### <a name="the-isscommandwithparameters-interface"></a>Die ISSCommandWithParameters-Schnittstelle  
 Um UDTs durch OLE DB zu unter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stützen, implementiert Native Client eine Reihe von Änderungen, einschließlich des Hinzufügens der **ISSCommandWithParameters** -Schnittstelle. Diese neue Schnittstelle erbt von der OLE DB-Kernschnittstelle **ICommandWithParameters**. Zusätzlich zu den drei von **ICommandWithParameters**geerbten Methoden **GetParameterInfo**, **MapParameterNames**und **SetParameterInfo**; **ISSCommandWithParameters** stellt die **GetParameterProperties** -Methode und die **SetParameterProperties** -Methode bereit, die zur Behandlung von serverspezifischen Datentypen verwendet werden.  
  
> [!NOTE]  
>  Die **ISSCommandWithParameters**-Schnittstelle nutzt auch die neue SSPARAMPROPS-Struktur.  
  
#### <a name="the-icolumnsrowset-interface"></a>Die IDBColumnsRowset-Schnittstelle  
 Zusätzlich zur **ISSCommandWithParameters** -Schnittstelle fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client dem Rowset, das durch Aufrufen der **IColumnsRowset:: GetColumnRowset** -Methode zurückgegeben wird, auch neue Werte hinzu, einschließlich der folgenden.  
  
|Spaltenname|type|BESCHREIBUNG|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Ein UDT-Katalognamensbezeichner.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Ein UDT-Schemanamensbezeichner.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Ein UDT-Namensbezeichner.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Der qualifizierte Name der Assembly mit dem Typnamen und allen zur CLR-Referenzierung erforderlichen Angaben zur Assembly-ID.|  
  
 Ist DBCOLUMN_TYPE auf DBTYPE_UDT festgelegt, können Sie eine Server-UDT-Spalte von anderen Binärtypen unterscheiden, indem Sie die oben genannten neuen UDT-Metadaten betrachten. Sind diese Daten teilweise vollständig, handelt es sich bei dem Servertyp um einen UDT. Für Nicht-UDT-Servertypen werden diese Spalten immer als NULL zurückgegeben.  
  
## <a name="sql-server-native-client-odbc-driver"></a>ODBC-Treiber für SQL Server Native Client  
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber hat eine Reihe von Änderungen vorgenommen, um UDTs zu unterstützen. Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ordnet den UDT SQL_SS_UDT treiberspezifischen SQL-Datentyp Bezeichner zu. UDT-Spalten werden als SQL_SS_UDT angegeben. Wenn Sie eine UDT-Spalte explizit einem anderen Typ in einer SQL-Anweisung zuordnen, indem Sie die Methoden " **atstring** " oder " **ToXmlString** " des UDT oder über die **Cast/Convert-** Funktion verwenden, spiegelt der Typ der Spalte im Resultset den tatsächlichen Typ wider, in den die Spalte konvertiert wurde.  
  
### <a name="sqlcolattribute-sqldescribeparam-sqlgetdescfield"></a>SQLColAttribute, SQLDescribeParam, SQLGetDescField  
 Es wurden vier neue Treiber spezifische Deskriptorfelder hinzugefügt, um zusätzliche Informationen für eine UDT-Spalte eines Resultsets oder einen UDT-Parameter der gespeicherten Prozedur/parametrisierten Abfrage bereitzustellen, die über die Funktionen [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md), [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)und [SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md) abgerufen werden sollen.  
  
 Die vier neuen Deskriptorfelder sind SQL_CA_SS_UDT_CATALOG_NAME, SQL_CA_SS_UDT_SCHEMA_NAME, SQL_CA_SS_UDT_TYPE_NAME und SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="sqlcolumns-sqlprocedurecolumns"></a>SQLColumns, SQLProcedureColumns  
 Außerdem werden dem von den Funktionen [SQLColumns](../../native-client-odbc-api/sqlcolumns.md) und [sqlprocedurecolrens](../../native-client-odbc-api/sqlprocedurecolumns.md) zurückgegebenen Resultset drei neue Treiber spezifische Spalten hinzugefügt, um zusätzliche Informationen zu einer UDT-Resultsetspalte oder einem UDT-Parameter bereitzustellen. Diese drei neuen Spalten sind SS_UDT_CATALOG_NAME, SS_UDT_SCHEMA_NAME und SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="supported-conversions"></a>Unterstützte Umwandlungen  
 Bei der Umwandlung von SQL- in C-Datentypen können SQL_C_WCHAR, SQL_C_BINARY und SQL_C_CHAR in SQL_SS_UDT umgewandelt werden. Beachten Sie jedoch, dass Binärdaten bei der Umwandlung der SQL-Datentypen SQL_C_WCHAR und SQL_C_CHAR in eine hexadezimale Zeichenfolge umgewandelt werden.  
  
 Bei der Umwandlung von C- in SQL-Datentypen können SQL_C_WCHAR, SQL_C_BINARY und SQL_C_CHAR in SQL_SS_UDT umgewandelt werden. Beachten Sie jedoch, dass Binärdaten in eine hexadezimale Zeichenfolge konvertiert werden, wenn Sie die SQL-Datentypen SQL_C_WCHAR und SQL_C_CHAR konvertieren.  
  
## <a name="see-also"></a>Weitere Informationen  
 [SQL Server Native Client-Funktionen](sql-server-native-client-features.md)   
 [' ISSCommandWithParameters ' &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
