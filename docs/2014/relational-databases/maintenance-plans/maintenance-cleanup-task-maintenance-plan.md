---
title: Task 'Wartungscleanup' (Wartungsplan) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.cleanup.f1
helpviewer_keywords:
- Maintenance Cleanup Task dialog box
ms.assetid: 022b679c-6799-4c13-9185-814224a20412
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 175998d210bec502199922831adc3508cc9171a6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63035722"
---
# <a name="maintenance-cleanup-task-maintenance-plan"></a>Task 'Wartungscleanup' (Wartungsplan)
  Mit dem **Task 'Wartungscleanup'** können Sie alte Dateien für Wartungspläne löschen, u. a. von Wartungsplänen und Datenbanksicherungsdateien erstellte Textberichte.  
  
> [!NOTE]  
>  Dateien in den Unterordnern des angegebenen Verzeichnisses werden vom Task Wartungscleanup nicht automatisch gelöscht. Diese Funktion reduziert die Möglichkeit eines bösartigen Angriffs, der den Task Wartungscleanup zum Löschen von Dateien verwendet. Wenn Sie Dateien in Unterordnern auf oberster Ebene löschen möchten, müssen Sie **Unterordner auf oberster Ebene einschließen**auswählen.  
  
## <a name="options"></a>Tastatur  
 **Connection**  
 Zeigt die aktuelle Verbindung an.  
  
 **Neu**  
 Erstellen Sie eine neue Serververbindung, die bei der Ausführung dieses Tasks verwendet werden soll. Das Dialogfeld **Neue Verbindung** wird im Folgenden beschrieben.  
  
 **Sicherungsdateien**  
 Löscht Sicherungsdateien.  
  
 **Textberichte für Wartungsplan**  
 Löscht Textberichte über zuvor ausgeführte Wartungspläne.  
  
 **Bestimmte Datei löschen**  
 Löscht die im Feld **Dateiname** angegebene Datei.  
  
 **Dateiname**  
 Pfad und Name der zu löschenden Datei.  
  
 **Ordner durchsuchen und Dateien anhand einer Erweiterung löschen**  
 Löscht alle Dateien mit der angegebenen Erweiterung im angegebenen Ordner. Mithilfe dieser Option können Sie mehrere Dateien gleichzeitig löschen, z. B. alle Sicherungsdateien mit der Erweiterung .bak im ausgewählten Ordner.  
  
 **Ordner**  
 Pfad und Name des Ordners, in dem die zu löschenden Dateien enthalten sind.  
  
 **Dateierweiterung**  
 Geben Sie die Dateierweiterung der zu löschenden Dateien an.  
  
 **Unterordner der ersten Ebene einschließen**  
 Löscht Dateien mit der für **Dateierweiterung** angegebenen Erweiterung aus den Unterordnern der obersten Ebene unter **Ordner**.  
  
 **Dateien basierend auf dem Alter der Datei zur Task Laufzeit löschen**  
 Geben Sie das Mindestalter der zu löschenden Dateien an, indem Sie im Feld **Dateien löschen, die älter sind als** eine Zahl und eine Zeiteinheit festlegen.  
  
 **Dateien löschen, die älter sind als die folgenden**  
 Geben Sie das Mindestalter der zu löschenden Dateien an, in dem Sie eine Nummer und eine Zeiteinheit (Tag, Woche, Monat oder Jahr) festlegen. Dateien, die älter sind als der angegebene Zeitrahmen, werden gelöscht.  
  
 **T-SQL anzeigen**  
 Zeigt die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen an, die für diesen Task auf dem Server auf Basis der ausgewählten Optionen ausgeführt werden.  
  
> [!NOTE]  
>  Wenn die Anzahl der betroffenen Objekte groß ist, kann die Anzeige erhebliche Zeit in Anspruch nehmen.  
  
## <a name="new-connection-dialog-box"></a>Neue Verbindung (Dialogfeld)  
 **Verbindungs Name**  
 Geben Sie einen Namen für die neue Verbindung ein.  
  
 **Servernamen auswählen oder eingeben**  
 Wählen Sie den Server aus, zu dem bei der Ausführung dieses Tasks eine Verbindung hergestellt werden soll.  
  
 **...**  
 Wählen Sie diese Option aus, um die Liste der verfügbaren Server anzuzeigen.  
  
 **Geben Sie Informationen ein, um sich beim Server anzumelden.**  
 Legt fest, wie die Authentifizierung gegenüber dem Server stattfindet.  
  
 **Integrierte Sicherheit von Windows verwenden**  
 Stellt mithilfe der Microsoft Windows-Authentifizierung eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her.  
  
 **Einen bestimmten Benutzernamen und ein bestimmtes Kennwort verwenden**  
 Stellt mithilfe der SQL Server-Authentifizierung eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her. Diese Option ist nicht verfügbar.  
  
 **Benutzername**  
 Stellt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung für den Gebrauch bei der Authentifizierung bereit. Diese Option ist nicht verfügbar.  
  
 **Kennwort**  
 Stellt ein Kennwort für den Gebrauch bei der Authentifizierung bereit. Diese Option ist nicht verfügbar.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Wartungspläne](maintenance-plans.md)  
  
  
