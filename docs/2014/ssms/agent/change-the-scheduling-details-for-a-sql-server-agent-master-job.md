---
title: Ändern der Zeitplandetails für einen Rasterauftrag für den SQL Server-Agent | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: f5414451-4d8e-464b-bd9e-f2b70c6899b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01f9e53c4ae42f981b1b579294954a965ef8c376
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63140676"
---
# <a name="change-the-scheduling-details-for-a-sql-server-agent-master-job"></a>Change the Scheduling Details for a SQL Server Agent Master Job
  In diesem Thema wird beschrieben, wie Sie Zeitplandetails mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)]ändern.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So ändern Sie die Zeit Plan Details für eine Auftrags Definition mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Ein Masterauftrag für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent kann nicht gleichzeitig lokale Server und Remoteserver als Ziel haben.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie können nur Aufträge ändern, die in Ihrem Besitz sind, es sei denn, Sie sind ein Mitglied der festen Serverrolle **sysadmin** . Ausführliche Informationen finden Sie unter [Implementieren der SQL Server-Agent-Sicherheit](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-change-the-scheduling-details-for-a-job-definition"></a>So ändern Sie die Zeitplandetails für eine Auftragsdefinition  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, in dem der Auftrag mit dem zu bearbeitenden Zeitplan enthalten ist.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um den Ordner **Aufträge** zu erweitern.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Auftrag, dessen Zeitplan Sie bearbeiten möchten, und wählen Sie **Eigenschaften**aus.  
  
5.  Wählen Sie im Dialogfeld **Auftrags Eigenschaften-**_job_name_ unter **Seite auswählen**die Option **Zeitpläne**aus. Weitere Informationen zu den verfügbaren Optionen auf dieser Seite finden Sie unter [Auftrags Eigenschaften: Seite "neue Aufträge &#40;Zeitpläne"&#41;](job-properties-new-job-schedules-page.md).  
  
6.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-change-the-scheduling-details-for-a-job-definition"></a>So ändern Sie die Zeitplandetails für eine Auftragsdefinition  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- changes the enabled status of the NightlyJobs schedule to 0   
    -- and sets the owner to terrid.   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_schedule  
        @name = 'NightlyJobs',  
        @enabled = 0,  
        @owner_login_name = 'terrid' ;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sp_update_schedule &#40;Transact-SQL-&#41;](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql).  
  
  
