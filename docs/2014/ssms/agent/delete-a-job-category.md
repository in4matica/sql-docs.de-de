---
title: Löschen einer Auftragskategorie | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bb392991afbb3707fafdb18a28cc3de53f97c78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783203"
---
# <a name="delete-a-job-category"></a>Löschen einer Auftragskategorie
  In diesem Thema wird beschrieben, wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sie eine-Agent [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Auftrags [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Kategorie [!INCLUDE[tsql](../../includes/tsql-md.md)] in mithilfe von, oder SQL Server Management Objects löschen.  
  
 Auftragskategorien helfen Ihnen dabei, Ihre Aufträge zum einfachen Filtern und Gruppieren zu organisieren. Sie können z. B. alle Aufträge für die Datenbanksicherung in der Datenbankwartungskategorie organisieren.  

##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Wenn Sie eine benutzerdefinierte Auftragskategorie löschen, werden sie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgefordert, die Aufträge neu zuzuweisen, die in einer anderen Auftragskategorie zugewiesen wurden. Sie können nur benutzerdefinierte Auftragskategorien löschen.  
  
###  <a name="Security"></a> Sicherheit  
 Ausführliche Informationen finden Sie unter [Implementieren der SQL Server-Agent-Sicherheit](implement-sql-server-agent-security.md).  

##  <a name="SSMS"></a> Verwenden von SQL Server Management Studio  
  
### <a name="to-delete-a-job-category"></a>So löschen Sie eine Auftragskategorie  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, auf dem Sie eine Auftragskategorie löschen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Aufträge** , und wählen Sie **Auftragskategorien verwalten**aus.  
  
4.  Wählen Sie im Dialogfeld **Auftrags Kategorien verwalten**_server_name_ die zu löschende Auftrags Kategorie aus.  
  
5.  Klicken Sie auf **Löschen**.  
  
6.  Klicken Sie im Dialogfeld **Auftragskategorien** auf **Ja**.  
  
7.  Schließen Sie das Dialogfeld **Auftrags Kategorien verwalten**_server_name_ .  
  
##  <a name="TSQL"></a> Verwenden von Transact-SQL  
  
### <a name="to-delete-a-job-category"></a>So löschen Sie eine Auftragskategorie  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```sql
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sp_delete_category &#40;Transact-SQL-&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-category-transact-sql).  

  
##  <a name="SMO"></a>Verwenden von SQL Server Management Objects  

### <a name="to-delete-a-job-category"></a>So löschen Sie eine Auftragskategorie
  
 Rufen Sie die `JobCategory`-Klasse in einer Programmiersprache Ihrer Wahl auf, z. B. Visual Basic, Visual C# oder PowerShell.  
