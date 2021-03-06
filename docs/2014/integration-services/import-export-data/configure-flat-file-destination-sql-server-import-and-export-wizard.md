---
title: Flatfileziel konfigurieren (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6504e4f5eee83d670b4843fb8d956b23a84d4aad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "62893031"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Flatfileziel konfigurieren (SQL Server-Import/Export-Assistent)
  Verwenden Sie die Seite **Flatfileziel konfigurieren** , um Formatierungsoptionen für die Zielflatfile anzugeben und die Vorschau der Ergebnisse anzuzeigen, bevor Sie fortfahren.  
  
 Weitere Informationen zu diesem Assistenten finden Sie unter [SQL Server-Import/Export-Assistenten](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Weitere Informationen zu den Optionen für das Starten des Assistenten sowie zu den Berechtigungen, die zum erfolgreichen Ausführen des Assistenten erforderlich sind, finden Sie unter [Ausführen des SQL Server-Import/Export-Assistenten](start-the-sql-server-import-and-export-wizard.md).  
  
 Mit dem SQL Server-Import/Export-Assistenten werden Daten aus einer Quelle in ein Ziel kopiert. Mit dem Assistenten können auch eine Zieldatenbank und Zieltabellen erstellt werden. Wenn Sie jedoch mehrere Datenbanken, Tabellen oder andere Datenbankobjekte kopieren müssen, verwenden Sie stattdessen den Assistenten zum Kopieren von Datenbanken. Weitere Informationen finden Sie unter [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Tastatur  
 **Quellflatfile**  
 Der Name der Zieldatei.  
  
 **Zeilen Trennzeichen**  
 Wählen Sie ein Trennzeichen für Zeilen aus der Liste aus.  
  
|value|BESCHREIBUNG|  
|-----------|-----------------|  
|**Programmiert Verlangt**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**Programmiert**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf.|  
|**Verlangt**|Als Trennzeichen für Zeilen dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Zeilen dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Zeilen dient ein Doppelpunkt.|  
|**Komma{,}**|Als Trennzeichen für Zeilen dient ein Komma.|  
|**Tab {t}**|Als Trennzeichen für Zeilen dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Zeilen dient ein senkrechter Strich.|  
  
 **Spalten Trennzeichen**  
 Wählen Sie ein Trennzeichen für Spalten aus der Liste aus.  
  
|value|BESCHREIBUNG|  
|-----------|-----------------|  
|**Programmiert Verlangt**|Die Spalten werden durch eine Kombination aus Wagen Rücklauf-Zeilenvorschub getrennt.|  
|**Programmiert**|Als Trennzeichen für Spalten dient ein Wagenrücklauf.|  
|**Verlangt**|Als Trennzeichen für Spalten dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Spalten dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Spalten dient ein Doppelpunkt.|  
|**Komma{,}**|Als Trennzeichen für Spalten dient ein Komma.|  
|**Tab {t}**|Als Trennzeichen für Spalten dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Spalten dient ein senkrechter Strich.|  
  
 **Vorschau**  
 Zeigen Sie im Dialogfeld **Vorschau Daten** die Ergebnisse der ausgewählten Formatierungsoptionen für die Zielflatfile an.  
  
 **Transformation bearbeiten**  
 Zeilen löschen, Zeilen anfügen und Spalten in der Zieldatei konfigurieren, indem Sie das Dialogfeld **Spalten** Zuordnungen verwenden.  
  
  
