---
title: Notify an Operator of Job Status
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ab19f300a05e61d2f008e4d1cf246e803f990a4c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252391"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie Benachrichtigungsoptionen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder SQL Server Management Objects festlegen können, damit der [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent den Operatoren Benachrichtigungen über Aufträge senden kann.  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Sicherheit  
Ausführliche Informationen finden Sie unter [Implementieren der SQL Server-Agent-Sicherheit](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>So benachrichtigen Sie einen Operator über einen Auftragsstatus  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**, erweitern Sie **Aufträge**, klicken Sie mit der rechten Maustaste auf den Auftrag, den Sie bearbeiten möchten, und wählen Sie **Eigenschaften**aus.  
  
3.  Wählen Sie im Dialogfeld **Auftragseigenschaften** die Seite **Benachrichtigungen** aus.  
  
4.  Wenn ein Operator per E-Mail benachrichtigt werden soll, aktivieren Sie die Option **E-Mail**, wählen Sie aus der Liste einen Operator aus, und wählen Sie dann eine der folgenden Optionen aus:  
  
    -   **Bei erfolgreicher Auftragsausführung** , um den Operator zu benachrichtigen, wenn der Auftrag erfolgreich abgeschlossen wurde.  
  
    -   **Bei Auftragsfehler** , um den Operator zu benachrichtigen, wenn der Auftrag fehlgeschlagen ist.  
  
    -   **Beim Abschluss des Auftrags** , um den Operator unabhängig vom Abschlussstatus zu benachrichtigen.  
  
5.  Wenn ein Operator per Pager benachrichtigt werden soll, aktivieren Sie die Option **Pager**, wählen Sie aus der Liste einen Operator aus, und wählen Sie dann eine der folgenden Optionen aus:  
  
    -   **Bei erfolgreicher Auftragsausführung** , um den Operator zu benachrichtigen, wenn der Auftrag erfolgreich abgeschlossen wurde.  
  
    -   **Bei Auftragsfehler** , um den Operator zu benachrichtigen, wenn der Auftrag fehlgeschlagen ist.  
  
    -   **Beim Abschluss des Auftrags** , um den Operator unabhängig vom Abschlussstatus zu benachrichtigen.  
  
6.  Wenn ein Operator per NET SEND benachrichtigt werden soll, aktivieren Sie die Option **NET SEND**, wählen Sie aus der Liste einen Operator aus, und wählen Sie dann eine der folgenden Optionen aus:  
  
    -   **Bei erfolgreicher Auftragsausführung** , um den Operator zu benachrichtigen, wenn der Auftrag erfolgreich abgeschlossen wurde.  
  
    -   **Bei Auftragsfehler** , um den Operator zu benachrichtigen, wenn der Auftrag fehlgeschlagen ist.  
  
    -   **Beim Abschluss des Auftrags** , um den Operator unabhängig vom Abschlussstatus zu benachrichtigen.  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>So benachrichtigen Sie einen Operator über einen Auftragsstatus  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists
    --  and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd).  
  
## <a name="SMO"></a>Verwendung von SQL Server Management Objects  
**So benachrichtigen Sie einen Operator über einen Auftragsstatus**  
  
Verwenden Sie die **Job** -Klasse in einer von Ihnen ausgewählten Programmiersprache, z. B. Visual Basic, Visual C# oder PowerShell. Weitere Informationen finden Sie unter [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
