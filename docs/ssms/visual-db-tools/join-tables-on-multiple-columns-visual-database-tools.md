---
title: Verknüpfen von Tabellen über mehrere Spalten
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiple column joins
- joins [SQL Server], multiple columns
ms.assetid: 56a158bc-a42a-4b78-baad-4721d2d22cd3
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 52884c4fb103f57e999d7a63d770181cf8cc8999
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "75224643"
---
# <a name="join-tables-on-multiple-columns-visual-database-tools"></a>Verknüpfen von Tabellen über mehrere Spalten (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Sie können Tabellen über mehrere Spalten verknüpfen. Dies bedeutet, dass Sie eine Abfrage erstellen können, die Übereinstimmungen von Zeilen aus den zwei Tabellen nur herstellt, wenn diese mehrere Bedingungen erfüllen. Wenn die Datenbank eine Beziehung enthält, in der mehrere Fremdschlüsselspalten einer Tabelle einem mehrspaltigen Primärschlüssel in der anderen Tabelle entsprechen, können Sie mit dieser Beziehung ein Join über mehrere Spalten erstellen. Ausführliche Informationen finden Sie unter [Automatisches Verknüpfen von Tabellen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md).  
  
Sie können den Join auch dann manuell erstellen, wenn die Datenbank keine mehrspaltige Fremdschlüsselbeziehung enthält.  
  
### <a name="to-manually-create-a-multicolumn-join"></a>So erstellen Sie manuell einen Join über mehrere Spalten  
  
1.  Fügen Sie dem [Diagrammbereich](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) die zu verknüpfenden Tabellen hinzu.  
  
2.  Ziehen Sie den Namen der ersten Joinspalte aus dem Fenster der ersten Tabelle, und legen Sie diesen auf der entsprechenden Spalte im Fenster der zweiten Tabelle ab. Einen Join kann nicht auf der Grundlage von text-, ntext- oder image-Spalten erstellt werden.  
  
    > [!NOTE]  
    > Im Allgemeinen müssen die Joinspalten denselben (oder einen kompatiblen) Datentyp aufweisen. Wenn z. B. die Joinspalte in der ersten Tabelle eine Datenspalte ist, müssen Sie diese mit einer Datenspalte in der zweiten Tabelle verknüpfen. Wenn es sich jedoch bei der ersten Joinspalte um eine Integer-Spalte handelt, muss die zu verknüpfende Spalte ebenfalls vom Integer-Datentyp sein, kann jedoch eine andere Größe aufweisen. In einzelnen Fällen ist ein Join scheinbar inkompatibler Spalten dank impliziter Datentypkonvertierungen jedoch möglich.  
    >   
    > Der [Abfrage- und Sicht-Designer](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) überprüft die Datentypen der für einen Join verwendeten Spalten nicht. Wenn Sie jedoch die Abfrage ausführen, zeigt die Datenbank bei nicht kompatiblen Datentypen einen Fehler an.  
  
3.  Ziehen Sie den Namen der zweiten Joinspalte aus dem Fenster der ersten Tabelle, und legen Sie diesen auf der entsprechenden Spalte im Fenster der zweiten Tabelle ab.  
  
4.  Wiederholen Sie Schritt drei für jedes weitere Paar von Joinspalten in den beiden Tabellen.  
  
5.  Führen Sie die Abfrage aus.  
  
## <a name="see-also"></a>Weitere Informationen  
[Erstellen von Abfragen mit Joins &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
