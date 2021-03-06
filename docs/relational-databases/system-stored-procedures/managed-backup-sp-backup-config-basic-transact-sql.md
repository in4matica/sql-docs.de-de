---
title: managed_backup. sp_backup_config_basic (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e3b3c547453c41dff6d32d1cafcd62746a2f194f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "72305260"
---
# <a name="managed_backupsp_backup_config_basic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Konfiguriert die [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] grundlegenden Einstellungen für eine bestimmte Datenbank oder für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Diese Prozedur kann eigenständig aufgerufen werden, um eine grundlegende verwaltete Sicherungs Konfiguration zu erstellen. Wenn Sie jedoch erweiterte Features oder einen benutzerdefinierten Zeitplan hinzufügen möchten, konfigurieren Sie diese Einstellungen zuerst mithilfe von [managed_backup. sp_backup_config_advanced &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) und [managed_backup. sp_backup_config_schedule &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) , bevor Sie die verwaltete Sicherung mit diesem Verfahren aktivieren.  
   
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol für Themenlink") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a>Argumente  
 @enable_backup  
 Aktiviert oder deaktiviert [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für die angegebene Datenbank. Der @enable_backup ist **Bit**. Erforderlicher Parameter beim [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] Konfigurieren von für die erste [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Instanz von. Wenn Sie eine vorhandene [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] Konfiguration ändern, ist dieser Parameter optional. In diesem Fall behalten alle nicht angegebenen Konfigurationswerte Ihre vorhandenen Werte bei.  
  
 @database_name  
 Der Datenbankname für die Aktivierung der verwalteten Sicherung für eine bestimmte Datenbank.  
  
 @container_url  
 Eine URL, die den Speicherort der Sicherung angibt. Wenn @credential_name NULL ist, ist diese URL eine SAS-URL (Shared Access Signature) für einen BlobContainer in Azure Storage, und die Sicherungen verwenden die neue Sicherung zum Blockieren der blobfunktionalität. Weitere Informationen finden Sie Untergrund Legendes zu [SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Wenn @credential_name angegeben wird, handelt es sich hierbei um eine Speicherkonto-URL, und für die Sicherungen wird die veraltete Sicherung auf seitenblob-Funktionalität verwendet.  
  
> [!NOTE]  
>  Zurzeit wird nur eine SAS-URL für diesen Parameter unterstützt.  
  
 @retention_days  
 Die Beibehaltungsdauer für die Sicherungsdateien in Tagen. Ist @storage_url vom Datentyp int. Dies ist ein erforderlicher Parameter, [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] Wenn Sie zum ersten Mal für die- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Instanz konfigurieren. Wenn Sie die [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] Konfiguration ändern, ist dieser Parameter optional. Wenn der Parameter nicht angegeben ist, werden die vorhandenen Konfigurationswerte beibehalten.  
  
 @credential_name  
 Der Name der SQL-Anmelde Informationen, die für die Authentifizierung beim Azure Storage-Konto verwendet werden. @credentail_nameist vom **Datentyp sysname**. Wenn angegeben, wird die Sicherung in einem seitenblob gespeichert. Wenn dieser Parameter NULL ist, wird die Sicherung als blockblob gespeichert. Die Sicherung im seitenblob ist veraltet. Daher wird empfohlen, die neue blockblob-Sicherungsfunktion zu verwenden. Bei Verwendung zum Ändern der [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Konfiguration ist dieser Parameter optional. Wenn kein Wert angegeben ist, werden die vorhandenen Konfigurationswerte beibehalten.  
  
> [!WARNING]
>  Der ** \@credential_name** -Parameter wird zurzeit nicht unterstützt. Es wird nur eine Sicherung in blockblob unterstützt, für die dieser Parameter NULL sein muss.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 „0“ (erfolgreich) oder „1“ (fehlerhaft)  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in **db_backupoperator** Daten Bank Rolle mit **ALTER ANY CREDENTIAL** -Berechtigungen und **Execute** -Berechtigungen für die gespeicherte Prozedur **sp_delete_backuphistory** .  
  
## <a name="examples"></a>Beispiele  
 Sie können den Speicherkonto Container und die SAS-URL erstellen, indem Sie die neuesten Azure PowerShell Befehle verwenden. Im folgenden Beispiel wird der neue Container MyContainer im Speicherkonto mystorageaccount erstellt und anschließend eine SAS-URL mit vollständigen Berechtigungen abgerufen.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 Im folgenden Beispiel wird [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für die Instanz von aktiviert, SQL Server Sie ausgeführt wird, die Aufbewahrungs Richtlinie auf 30 Tage festlegt und das Ziel auf einen Container namens "MyContainer" in einem Speicherkonto mit dem Namen "mystorageaccount" festlegt.  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 Im folgenden Beispiel wird [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für die Instanz von SQL Server deaktiviert, in der es ausgeführt wird.  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [managed_backup. sp_backup_config_advanced &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup. sp_backup_config_schedule &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
