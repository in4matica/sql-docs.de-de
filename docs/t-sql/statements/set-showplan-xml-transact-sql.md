---
title: SET SHOWPLAN_XML (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 890c84330005c3d9f6c4b30a06662d67dfef46f2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "67941651"
---
# <a name="set-showplan_xml-transact-sql"></a>SET SHOWPLAN_XML (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Bewirkt, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht ausführt. Stattdessen gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detaillierte Informationen zur Ausführung der Anweisungen in Form eines definierten XML-Dokuments zurück.

![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol für Themenlink") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Syntax

```
SET SHOWPLAN_XML { ON | OFF }
```

## <a name="remarks"></a>Bemerkungen

Die Einstellung von SET SHOWPLAN_XML wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.

Wenn SET SHOWPLAN_XML auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Informationen zum Ausführungsplan jeder Anweisung zurück, ohne sie auszuführen, und [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen werden nicht ausgeführt. Wenn diese Option auf ON festgelegt ist, werden Ausführungsplaninformationen zu allen weiteren [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen zurückgegeben, bis die Option auf OFF festgelegt wird. Wenn beispielsweise eine CREATE TABLE-Anweisung ausgeführt wird, während SET SHOWPLAN_XML auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei einer darauf folgenden SELECT-Anweisung, die dieselbe Tabelle betrifft, die Fehlermeldung zurück, dass diese Tabelle nicht vorhanden ist. Daher schlagen spätere Verweise auf diese Tabelle fehl. Wenn SET SHOWPLAN_XML auf OFF festgelegt ist, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anweisungen aus, ohne einen Bericht zu generieren.

SET SHOWPLAN_XML soll die Ausgabe als **nvarchar(max)** für Anwendungen zurückgeben, wie z.B. das Hilfsprogramm **sqlcmd**, wobei die XML-Ausgabe nachfolgend von weiteren Tools für die Anzeige und Verarbeitung der Abfrageplaninformationen verwendet wird.

> [!NOTE]
> Die dynamische Verwaltungssicht **sys.dm_exec_query_plan** gibt dieselben Informationen wie SET SHOWPLAN XML im Datentyp **XML** zurück. Diese Informationen werden aus der Spalte **query_plan** von **sys.dm_exec_query_plan** zurückgegeben. Weitere Informationen finden Sie unter [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).

SET SHOWPLAN_XML kann innerhalb einer gespeicherten Prozedur nicht angegeben werden. Sie muss die einzige Anweisung in einem Batch sein.

SET SHOWPLAN_XML gibt Informationen als eine Gruppe von XML-Dokumenten zurück. Jeder Batch nach der SET SHOWPLAN_XML ON-Anweisung ist in der Ausgabe als einzelnes Dokument enthalten. Jedes Dokument enthält den Text der Anweisungen im Batch gefolgt von den Details der Ausführungsschritte. Das Dokument zeigt die geschätzten Kosten, Anzahl von Zeilen, Indexzugriffe und Typen der ausgeführten Operatoren, Joinreihenfolge und weitere Informationen zu den Ausführungsplänen.

> [!NOTE]
> Wenn **Tatsächlichen Ausführungsplan einschließen** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ausgewählt ist, generiert diese SET-Option keine XML-Showplanausgabe mehr. Deaktivieren Sie das Kontrollkästchen **Tatsächlichen Ausführungsplan einschließen**, bevor Sie diese SET-Option verwenden.

### <a name="location-of-showplan-output"></a>Speicherort der SHOWPLAN-Ausgabe

Das Dokument mit dem XML-Schema für die XML-Ausgabe von SET SHOWPLAN_XML wird beim Setup in ein lokales Verzeichnis auf dem Computer kopiert, auf dem Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist. Das Dokument findet sich auf dem Laufwerk, das die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installationsdateien enthält, und ist unter einem Pfad ähnlich dem folgenden zugänglich:

- `\Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd`

Im vorherigen Pfad wird der Knoten `130\` von SQL Server 2016 verwendet. Die Zahl 130 wird vom ersten Knoten des von `SELECT @@VERSION` zurückgegebenen Werts abgeleitet, also 13. Für SQL Server 2017 würde der Pfad `140\` verwenden, da der erste Knoten des @@VERSION-Werts 14 ist. Bei SQL Server 2019 ist der erste Wert von @@VERSION 15.

Das Showplanschema kann auf [dieser Website](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409) gefunden werden.

## <a name="permissions"></a>Berechtigungen

Für die Verwendung von SET SHOWPLAN_XML benötigen Sie für die Ausführung der Anweisungen, auf die SET SHOWPLAN_XML angewendet wird, ausreichende Berechtigungen sowie die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die verwiesen wird.

Damit die Anweisungen SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure* und EXEC *user_defined_function* einen Showplan erstellen, benötigt der Benutzer Folgendes:

- Berechtigungen für die Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.

- SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die in den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen verwiesen wird, wie z.B. Tabellen, Sichten usw.

Für alle anderen Anweisungen, z.B. DDL, USE *database_name*, SET, DECLARE, dynamische SQL-Anweisungen usw., werden nur die entsprechenden Berechtigungen für die Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen benötigt.

## <a name="examples"></a>Beispiele

In den beiden folgenden Anweisungen werden die SET SHOWPLAN_XML-Einstellungen verwendet, um zu zeigen, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Verwendung von Indizes in Abfragen analysiert und optimiert.

In der ersten Abfrage wird der Vergleichsoperator (=) in der WHERE-Klausel auf eine indizierte Spalte angewendet. In der zweiten Abfrage wird der LIKE-Operator in der WHERE-Klausel verwendet. Deshalb muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Scan des gruppierten Indexes ausführen, um die Daten zu finden, die der Bedingung in der WHERE-Klausel entsprechen. Die Werte in den Attributen **EstimateRows** und **EstimatedTotalSubtreeCost** sind bei der ersten indizierten Abfrage kleiner, was auf eine deutlich schnellere Verarbeitung und die Verwendung weniger Ressourcen als bei der nicht indizierten Abfrage hinweist.

```sql
USE AdventureWorks2012;
GO
SET SHOWPLAN_XML ON;
GO
-- First query.
SELECT BusinessEntityID
FROM HumanResources.Employee
WHERE NationalIDNumber = '509647174';
GO
-- Second query.
SELECT BusinessEntityID, JobTitle
FROM HumanResources.Employee
WHERE JobTitle LIKE 'Production%';
GO
SET SHOWPLAN_XML OFF;
```

## <a name="see-also"></a>Weitere Informationen

[SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)
