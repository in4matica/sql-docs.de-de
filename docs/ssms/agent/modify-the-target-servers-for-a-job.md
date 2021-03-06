---
title: Modify the Target Servers for a Job
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- modifying target servers
- SQL Server Agent jobs, target servers
- target servers [SQL Server], modifying
ms.assetid: 9dbe24f2-acec-4aa2-920c-e8e96efa18e4
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a5300935cdbffc501996c7e68ba44b73b2964fa4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252377"
---
# <a name="modify-the-target-servers-for-a-job"></a>Modify the Target Servers for a Job

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Artikel wird beschrieben, wie Sie die Zielserver für [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agentaufträge in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] ändern.

## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Sicherheit  
  
#### <a name="Permissions"></a>Berechtigungen  
Standardmäßig können Mitglieder der festen Serverrolle „sysadmin“ diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder einer der folgenden festen SQL Server-Agent-Datenbankrollen in der msdb-Datenbank sein:  
  
1.  **SQLAgentUserRole**  
  
2.  **SQLAgentReaderRole**  
  
3.  SQLAgentOperatorRole  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>So ändern Sie die Zielserver für einen Auftrag  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**, erweitern Sie **Aufträge**, klicken Sie mit der rechten Maustaste auf einen Auftrag, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie im Dialogfeld **Auftragseigenschaften** die Seite **Ziele**aus, und klicken Sie auf **Ziel: Lokaler Server**oder auf **Ziel: Mehrere Server**.  
  
    Wenn Sie **Ziel: Mehrere Server**auswählen, geben Sie Server an, die Ziele für den Auftrag sind, indem Sie das Kästchen links neben dem Servernamen aktivieren. Stellen Sie sicher, dass die Kästchen für die Server, die nicht Ziel für den Auftrag sind, deaktiviert sind.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>So ändern Sie die Zielserver für einen Auftrag  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde_md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird der Multiserverauftrag „Weekly Sales Backups“ dem Server SEATTLE2 zugewiesen.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',   
    @server_name = N'SEATTLE2' ;   
GO  
```  
  
Weitere Informationen finden Sie unter [sp_add_jobserver (Transact-SQL)](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286).  
  
## <a name="see-also"></a>Weitere Informationen  
[Automatisierte Verwaltung in einem Unternehmen](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
