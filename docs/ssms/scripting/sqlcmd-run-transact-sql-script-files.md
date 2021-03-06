---
title: Ausführen von Transact-SQL-Skriptdateien mithilfe von sqlcmd
ms.custom: seo-lt-2019
ms.date: 07/15/2016
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed85470d8e054ba60ae0b2525f773f83d70d0da3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253209"
---
# <a name="sqlcmd---run-transact-sql-script-files"></a>Ausführen von Transact-SQL-Skriptdateien mithilfe von „sqlcmd“
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 Verwenden Sie zum Ausführen einer Transact-SQL-Skriptdatei den Befehl **sqlcmd** . Eine Transact-SQL-Skriptdatei ist eine Textdatei, die eine Kombination aus Transact-SQL-Anweisungen, **sqlcmd** -Befehlen und Skriptvariablen enthalten kann.  

## <a name="create-a-script-file"></a>Erstellen einer Skriptdatei  
 Führen Sie die folgenden Schritte aus, um eine einfache Transact-SQL-Skriptdatei mithilfe des Editors zu erstellen:  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, zeigen Sie auf **Zubehör**, und klicken Sie dann auf **Editor**.  
  
2.  Kopieren Sie den folgenden Transact-SQL-Code, und fügen Sie ihn im Editor ein:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  Speichern Sie die Datei auf dem Laufwerk C unter dem Namen **myScript.sql** .  
  
## <a name="run-the-script-file"></a>Ausführen der Skriptdatei  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie im Eingabeaufforderungsfenster Folgendes ein: **sqlcmd -S myServer\instanceName -i C:\myScript.sql**  
  
3.  Drücken Sie die EINGABETASTE.  
  
 Eine Liste mit Namen und Adressen von Mitarbeitern aus [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] wird in das Eingabeaufforderungsfenster geschrieben.  

## <a name="save-the-output-to-a-text-file"></a>Speichern der Ausgabe in einer Textdatei
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie im Eingabeaufforderungsfenster Folgendes ein: **sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt**  
  
3.  Drücken Sie die EINGABETASTE.  
  
 In diesem Fall erfolgt keine Ausgabe im Eingabeaufforderungsfenster. Stattdessen erfolgt die Ausgabe in die Datei EmpAdds.txt. Sie können diese Ausgabe prüfen, indem Sie die Datei EmpAdds.txt öffnen.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Starten des Hilfsprogramms „sqlcmd“](../../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [SQLCMD-Hilfsprogramm](../../tools/sqlcmd-utility.md)  
  
  
