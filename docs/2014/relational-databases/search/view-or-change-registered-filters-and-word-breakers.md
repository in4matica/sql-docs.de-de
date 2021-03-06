---
title: Anzeigen oder Ändern von registrierten Filtern und Wörtertrennungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], word breakers
- full-text search [SQL Server], filters
- filters [full-text search]
- word breakers [full-text search]
ms.assetid: f88c54df-b1aa-4701-807f-dc92c32363fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 97bf5b2f1838531c305cf663d050201d5f34ce82
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66010930"
---
# <a name="view-or-change-registered-filters-and-word-breakers"></a>Anzeigen oder Ändern von registrierten Filtern und Wörtertrennungen
  Nach dem Installieren oder Deinstallieren von Wörtertrennungen oder Filtern werden die Änderungen nicht automatisch auf Serverinstanzen wirksam. In diesem Thema wird beschrieben, wie die zurzeit registrierte Wörtertrennung oder die Filter angezeigt werden und wie neu installierte Wörtertrennungen und Filter auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]registriert werden.  
  
### <a name="to-view-a-list-of-languages-whose-word-breakers-are-currently-registered"></a>So zeigen Sie eine Liste der Sprachen an, deren Wörtertrennungen derzeit registriert sind.  
  
1.  Verwenden Sie die [sys.fulltext_languages](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) -Katalogsicht wie folgt:  
  
    ```  
    SELECT * FROM sys.fulltext_languages;   
    ```  
  
### <a name="to-view-a-list-of-the-filters-that-are-currently-registered"></a>So zeigen Sie eine Liste der Filter an, die derzeit registriert sind  
  
1.  Verwenden Sie die gespeicherte Systemprozedur [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) wie folgt:  
  
    ```  
    EXEC sp_help_fulltext_system_components 'filter';    
    ```  
  
### <a name="to-register-newly-installed-word-breakers-and-filters"></a>So registrieren Sie neu installierte Wörtertrennungen und Filter  
  
1.  Verwenden Sie zum Aktualisieren der Liste mit den Sprachen die gespeicherte Systemprozedur [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql) wie folgt:  
  
    ```  
    exec sp_fulltext_service 'update_languages';   
    ```  
  
### <a name="to-unregister-uninstalled-word-breakers-and-filters"></a>So heben Sie die Registrierung deinstallierter Wörtertrennungen und Filter auf  
  
1.  Verwenden Sie zum Aktualisieren der Liste mit den Sprachen **sp_fulltext_service** wie folgt:  
  
    ```  
    exec sp_fulltext_service 'update_languages'  
    ```  
  
2.  Verwenden Sie zum Neustarten der Filterdaemon-Hostprozesse (fdhost.exe) **sp_fulltext_service** wie folgt:  
  
    ```  
    exec sp_fulltext_service 'restart_all_fdhosts';  
    ```  
  
### <a name="to-replace-existing-word-breakers-or-filters-when-installing-new-ones"></a>So ersetzen Sie vorhandene Wörtertrennungen oder Filter beim Installieren neuer Wörtertrennungen und Filter  
  
1.  Vergewissern Sie sich bei der Vorbereitung zur Installation einer DLL-Datei, die neue Wörtertrennungen oder Filter enthält, dass diese nicht den gleichen Namen einer DLL-Datei hat, die bereits auf Ihrer Serverinstanz installiert ist.  
  
2.  Kopieren Sie die neue DLL-Datei in das Verzeichnis, das die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard-DLL-Dateien für die Serverinstanz enthält. Dies ist der Standardspeicherort:  
  
     C:\Programme\Microsoft SQL Server\MSSQL.*Instanzname*\MSSQL\Binn  
  
    > [!IMPORTANT]  
    >  Es wird dringend empfohlen, nur signierte und überprüfte Komponenten zu laden. Außerdem sollten Sie den FDHOST-Startprogrammdienst (MSSQLFDLauncher) mit den geringstmöglichen Privilegien ausführen.  
  
3.  Installieren Sie die neue Wörtertrennung oder die Filter.  
  
     **So installieren und laden Sie Microsoft Filter Pack IFilters**  
  
    -   [So registrieren Sie Microsoft Filter Pack IFilters bei SQL Server](https://go.microsoft.com/fwlink/?LinkId=130439)  
  
4.  Verwenden Sie zum Laden neu installierter Wörtertrennungen und Filter in die Serverinstanz **sp_fulltext_service** wie folgt:  
  
    ```  
    EXEC sp_fulltext_service @action='load_os_resources', @value=1;  
    ```  
  
5.  Verwenden Sie zum Aktualisieren der Liste mit den Sprachen **sp_fulltext_service** wie folgt:  
  
    ```  
    EXEC sp_fulltext_service 'update_languages';  
    ```  
  
6.  Verwenden Sie zum Neustarten der Filterdaemon-Hostprozesse (fdhost.exe) **sp_fulltext_service** wie folgt:  
  
    ```  
    EXEC sp_fulltext_service 'restart_all_fdhosts';   
    ```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Festlegen des Dienstkontos für das Startprogramm des Volltextfilterdaemon](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Konfigurieren und Verwalten von Filtern für die Suche](configure-and-manage-filters-for-search.md)   
 [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
