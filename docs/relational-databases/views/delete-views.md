---
title: Löschen von Sichten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- dropping views
- deleting views
- views [SQL Server], deleting
- removing views
ms.assetid: 6823c7f8-06ca-4bda-8482-7092f03d52a0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a0b11b2d6fa897b99276f75fb74e2c41e25db904
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "68123473"
---
# <a name="delete-views"></a>Löschen von Sichten
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  Sie können Sichten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] löschen, indem Sie Folgendes verwenden: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Security](#Security)  
  
-   **So löschen Sie eine Sicht aus einer Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie eine Sicht löschen, werden die Definition der Sicht sowie weitere Informationen zur Sicht aus dem Systemkatalog entfernt. Alle Berechtigungen für die Sicht werden ebenfalls gelöscht.  
  
-   Eine mithilfe von `DROP TABLE` gelöschte Sicht in einer Tabelle muss explizit mit `DROP VIEW`gelöscht werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert entweder die ALTER-Berechtigung für SCHEMA oder die CONTROL-Berechtigung für OBJECT.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-delete-a-view-from-a-database"></a>So löschen Sie eine Sicht aus einer Datenbank  
  
1.  Erweitern Sie im **Objekt-Explorer**die Datenbank mit der Sicht, die Sie löschen möchten, und erweitern Sie dann den Ordner **Sichten** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Sicht, die Sie löschen möchten, und klicken Sie auf **Löschen**.  
  
3.  Klicken Sie im Dialogfeld **Objekt löschen** auf **OK**.  
  
    > [!IMPORTANT]  
    >  Klicken Sie im Dialogfeld **Objekt löschen** auf **Abhängigkeiten anzeigen**, um das Dialogfeld _Sichtname_ **-Abhängigkeiten** zu öffnen. Es werden alle Objekte angezeigt, die von der Sicht abhängig sind, und alle Objekte, von denen die Sicht abhängig ist.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-delete-a-view-from-a-database"></a>So löschen Sie eine Sicht aus einer Datenbank  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im Beispiel wird die angegebene Sicht nur gelöscht, wenn die Sicht bereits vorhanden ist.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    IF OBJECT_ID ('HumanResources.EmployeeHireDate', 'V') IS NOT NULL  
    DROP VIEW HumanResources.EmployeeHireDate;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md).  
  
  
