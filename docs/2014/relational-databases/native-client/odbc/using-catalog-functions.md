---
title: Verwenden von Katalog Funktionen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQLLinkedCatalogs function
- SQL Server Native Client ODBC driver, catalog functions
- SQLLinkedServers function
- catalog functions [ODBC]
- functions [ODBC]
ms.assetid: 7773fb2e-06b5-4c4b-88e9-0ad9132ad273
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 263df9986df0297c8bf1afdb35d70841835cef4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "62667378"
---
# <a name="using-catalog-functions"></a>Verwenden von Katalogfunktionen
  Alle Datenbanken verfügen über eine Struktur, die die in der Datenbank gespeicherten Daten enthält. Eine Definition dieser Struktur ist zusammen mit anderen Informationen, wie beispielsweise Berechtigungen, in einem Katalog gespeichert, der als Satz Systemtabellen implementiert und auch als Datenwörterbuch bezeichnet wird.  
  
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber ermöglicht einer Anwendung die Bestimmung der Datenbankstruktur durch Aufrufe von ODBC-Katalog Funktionen. Katalogfunktionen geben Informationen in Resultsets zurück und werden mithilfe von gespeicherten Katalogprozeduren implementiert, um die Systemtabellen im Katalog abzufragen. Beispielsweise könnte eine Anwendung ein Resultset mit Informationen über alle Tabellen im System oder alle Spalten in einer bestimmten Tabelle anfordern. Die standardmäßigen ODBC-Katalogfunktionen dienen dazu, Kataloginformationen von der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz abzurufen, mit der die Anwendung verbunden ist.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt verteilte Abfragen, in denen auf Daten aus mehreren heterogenen OLE DB-Datenquellen in einer einzigen Abfrage zugegriffen wird. Eine Methode des Zugriffs auf eine OLE DB-Datenquelle ist die Definition der Datenquelle als Verbindungsserver. Dies kann mit [sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)erfolgen. Nachdem der Verbindungsserver definiert wurde, kann in Transact-SQL-Anweisungen auf Objekte dieses Servers verwiesen werden. Dazu wird ein vierteiliger Name verwendet:  
  
 *linked_server_name. catalog. Schema. object_name*.  
  
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt zwei treiberspezifische Funktionen, die dazu dienen, Kataloginformationen von Verbindungsservern abzurufen:  
  
-   **SQLLinkedServers**  
  
     Gibt eine Liste der auf den lokalen Servern definierten Verbindungsserver zurück.  
  
-   **SQLLinkedCatalogs**  
  
     Gibt eine Liste der in einem Verbindungsserver enthaltenen Kataloge zurück.  
  
 Nachdem Sie einen Verbindungs Servernamen und einen Katalognamen haben, unter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stützt der Native Client-ODBC-Treiber das erhalten von Informationen aus dem Katalog mithilfe eines zweiteiligen namens _linked_server_name_**.** _Katalog_ für *CatalogName* in den folgenden ODBC-Katalog Funktionen:  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **'SQLStatistics'**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 Der zweiteilige _linked_server_name_**.** _catalog_ wird auch für " *f-CatalogName* " und " *PKCatalogName* " in " [sqlfremdnkeys](../../native-client-odbc-api/sqlforeignkeys.md)" unterstützt.  
  
 Zur Verwendung von SQLLinkedServers und SQLLinkedCatalogs sind die folgenden Dateien erforderlich:  
  
-   sqlncli.h  
  
     Enthält Funktionsprototypen und Konstantendefinitionen für die Verbindungsserverkatalogfunktionen. sqlncli.h muss in der ODBC-Anwendung enthalten sein und im Includepfad angegeben werden, wenn die Anwendung kompiliert wird.  
  
-   sqlncli11.lib  
  
     Muss im Bibliothekspfad des Linkers enthalten sein und als zu verknüpfende Datei angegeben werden. sqlncli11.lib wird zusammen mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber bereitgestellt.  
  
-   sqlncli11.dll  
  
     Muss zur Ausführungszeit verfügbar sein. sqlncli11. dll wird mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC-Treiber von Native Client verteilt.  
  
## <a name="see-also"></a>Weitere Informationen  
 [SQL Server Native Client &#40;ODBC-&#41;](sql-server-native-client-odbc.md)   
 [SQLColumnPrivileges](../../native-client-odbc-api/sqlcolumnprivileges.md)   
 [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)   
 [SQLPrimaryKeys](../../native-client-odbc-api/sqlprimarykeys.md)   
 [SQLTablePrivileges](../../native-client-odbc-api/sqltableprivileges.md)   
 [SQLTables](../../native-client-odbc-api/sqltables.md)   
 ['SQLStatistics'](../../statistics/statistics.md)  
  
  
