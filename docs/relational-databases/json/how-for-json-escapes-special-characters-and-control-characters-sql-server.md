---
title: Schutz von Sonderzeichen und Steuerzeichen durch FOR JSON
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5654a27a5457fe1d89fe76241c576f831dc9bf55
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "74095785"
---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>Schutz von Sonderzeichen und Steuerzeichen durch FOR JSON (SQL Server)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Dieses Thema beschreibt, wie die **FOR JSON**-Klausel einer **SELECT**-Anweisung von SQL Server Sonderzeichen schützt und Steuerzeichen in der JSON-Ausgabe darstellt.  

> [!IMPORTANT]
> Diese Seite beschreibt die integrierte Unterstützung für JSON in Microsoft SQL Server. Allgemeine Informationen zum Maskieren und Codierung in JSON finden Sie in Abschnitt 2.5 der JSON-Referenz unter [https://www.ietf.org/rfc/rfc4627.txt](https://www.ietf.org/rfc/rfc4627.txt).

## <a name="escaping-of-special-characters"></a>Schutz von Sonderzeichen  
Wenn die Quelldatei Sonderzeichen enthält, umgeht die **FOR JSON**-Klausel diese in der JSON-Ausgabe mit `\`, wie in der folgenden Tabelle dargestellt. Dieser Schutz tritt in den Namen von Eigenschaften und in ihren Werte auf.  
  
|**Sonderzeichen**|**Ausgabe mit Escapezeichen**|  
|---------------------------|--------------------------|  
|Anführungszeichen (")|\\"|  
|Umgekehrter Schrägstrich (\\)|\\\\|  
|Schrägstrich (/)|\\/|  
|Rücktaste|\b|  
|Seitenvorschub|\f|  
|Neue Zeile|\n|  
|Wagenrücklauf|\r|  
|Horizontaler Tabstopp|\t|  
  
## <a name="control-characters"></a>Steuerzeichen  
Wenn die Quelldatei Steuerzeichen enthält, kodiert die **FOR JSON**-Klausel diese in der JSON-Ausgabe im `\u<code>`-Format, wie in der folgenden Tabelle dargestellt.  
  
|**Steuerzeichen**|**Codierte Ausgabe**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>Beispiel  
 Hier ist ein Beispiel für die **FOR JSON**-Ausgabe von Quelldaten, die Sonderzeichen und Steuerelement enthält.  
  
 Abfrage:  
  
```sql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 Ergebnis:  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Weitere Informationen zu JSON in SQL Server und Azure SQL-Datenbank  
  
### <a name="microsoft-videos"></a>Microsoft-Videos

Eine visuelle Einführung in die JSON-Unterstützung, die in SQL Server und Azure SQL-Datenbank integriert ist, finden Sie in den folgenden Videos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Weitere Informationen  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Formatieren von Abfrageergebnissen als JSON mit FOR JSON [SQL Server])](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[FOR-Klausel](../../t-sql/queries/select-for-clause-transact-sql.md)
