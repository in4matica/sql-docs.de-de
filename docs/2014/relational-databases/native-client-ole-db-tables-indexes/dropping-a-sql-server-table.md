---
title: Löschen einer SQL Server Tabelle | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7af3d096d9e58b1cb75e2d7cab15988183578fdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046465"
---
# <a name="dropping-a-sql-server-table"></a>Löschen einer SQL Server-Tabelle
  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht die **ITableDefinition::D roptable** -Funktion verfügbar. Dies ermöglicht es Consumern, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Tabelle aus einer Datenbank zu entfernen.  
  
 Consumer geben den Tabellennamen als Unicode-Zeichenfolge in das Element *pwszName* der Vereinigung *uName* des Parameters *pTableID* ein. Das Element *eKind* von *pTableID* muss DBKIND_NAME sein.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Tabellen und Indizes](tables-and-indexes.md)  
  
  
