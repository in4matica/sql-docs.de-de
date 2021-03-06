---
title: sqlservr-Anwendung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], sqlservr
- command prompt [SQL Server], pausing/resuming instance of SQL Server
- starting instance of SQL Server
- command prompt [SQL Server], continuing instance of SQL Server
- sqlservr utility
- pausing instance of SQL Server
- stopping instance of SQL Server
- resuming SQL Server
- command prompt [SQL Server], stopping instance of SQL Server
- command prompt [SQL Server], starting instance of SQL Server
- continuing instance of SQL Server
ms.assetid: 60e8ef0a-0851-41cf-a6d8-cca1e04cbcdb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 23f45c0a2e47381b60fe8f6852f24fd8f5f200fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211018"
---
# <a name="sqlservr-application"></a>sqlservr (Anwendung)
  Die **sqlservr** -Anwendung startet, beendet, hält eine Instanz von [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] an einer Eingabeaufforderung an und setzt Sie fort.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      sqlservr [-sinstance_name] [-c] [-dmaster_path] [-f]   
     [-eerror_log_path] [-lmaster_log_path] [-m]  
     [-n] [-Ttrace#] [-v] [-x] [-gnumber]  
```  
  
## <a name="arguments"></a>Argumente  
 **-s** _instance_name_  
 Gibt die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz an, mit der eine Verbindung hergestellt wird. Wenn keine benannte Instanz angegeben wird, startet **sqlservr** die Standardinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Wenn Sie eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz starten, müssen Sie die **sqlservr** -Anwendung verwenden, die sich im entsprechenden Verzeichnis für diese Instanz befindet. Bei der Standardinstanz führen Sie **sqlservr** aus dem Verzeichnis „\MSSQL\Binn“ aus. Bei einer benannten Instanz führen Sie **sqlservr** aus dem Verzeichnis „\MSSQL$*instance_name*\Binn“ aus.  
  
 **-c**  
 Gibt an, dass eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz unabhängig vom Windows-Dienstkontroll-Manager gestartet wird. Diese Option wird verwendet, wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] von einer Eingabeaufforderung gestartet wird, um die erforderliche Zeit für das Starten von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zu verkürzen.  
  
> [!NOTE]  
>  Wenn Sie diese Option verwenden, ist es nicht möglich, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Dienst-Managers oder des Befehls **net stop** zu beenden. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wird beendet, wenn Sie sich vom Computer abmelden.  
  
 **-d** _master_path_  
 Gibt den vollqualifizierten Pfad für die **master** -Datenbankdatei an. Zwischen **-d** und *master_path*darf sich kein Leerzeichen befinden. Wenn diese Option nicht bereitgestellt wird, werden die vorhandenen Registrierungsparameter verwendet.  
  
 **-f**  
 Startet eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz mit Minimalkonfiguration. Dies ist hilfreich, wenn der Server aufgrund der Einstellung eines Konfigurationswerts (z. B. aufgrund von Arbeitsspeichermangel) nicht gestartet werden kann.  
  
 **-e** _error_log_path_  
 Gibt den vollqualifizierten Pfad der Fehlerprotokolldatei an. Wenn nicht angegeben, lautet** * \< *der Standard Speicherort Laufwerk>: \Programme\Microsoft SQL Server\MSSQL\Log\Errorlog für die Standard Instanz und * \<Laufwerk>*: \Programme\Microsoft SQL Server\MSSQL $ instance_name \log\errorlog für eine benannte Instanz. Zwischen **-e** und *error_log_path*darf sich kein Leerzeichen befinden.  
  
 **-l** _master_log_path_  
 Gibt den vollqualifizierten Pfad für die Transaktionsprotokolldatei der **master** -Datenbank an. Zwischen **-l** und *master_log_path*darf sich kein Leerzeichen befinden.  
  
 **-m**  
 Gibt an, dass eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz im Einzelbenutzermodus gestartet werden soll. Wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] im Einzelbenutzermodus gestartet wurde, kann nur ein Benutzer eine Verbindung herstellen. Der CHECKPOINT-Mechanismus, der sicherstellt, dass abgeschlossene Transaktionen regelmäßig aus dem Datenträgercache auf die Datenbankmedien geschrieben werden, wird nicht gestartet. (Diese Option wird normalerweise verwendet, wenn Sie Probleme mit Systemdatenbanken erkennen, die eine Reparatur erfordern.) Diese Option aktiviert die Option **sp_configure allow updates** (Updates zulassen). Standardmäßig ist **allow updates** deaktiviert.  
  
 **-n**  
 Ermöglicht es Ihnen, eine benannte [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz zu starten. Wurde der **-s** -Parameter nicht festgelegt, versucht die Standardinstanz zu starten. Sie müssen an der Eingabeaufforderung in das entsprechende BINN-Verzeichnis für die Instanz wechseln, bevor Sie **sqlservr.exe**starten. Wenn Instance1 beispielsweise das Verzeichnis „\mssql$Instance1“ für die zugehörigen Binärdateien verwendet wird, muss der Benutzer zum Verzeichnis „\mssql$Instance1\binn“ wechseln, um **sqlservr.exe -s instance1**starten zu können. Wenn Sie eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz mit der Option **-n** starten, sollten Sie auch die Option **-e** verwenden, da sonst keine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Ereignisse protokolliert werden.  
  
 **-T** Ablauf _Verfolgung #_  
 Gibt an, dass eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz so gestartet werden soll, dass ein bestimmtes Ablaufverfolgungsflag (*trace#*) wirksam wird. Ablaufverfolgungsflags werden verwendet, um den Server mit nicht standardmäßigem Verhalten zu starten. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
> [!IMPORTANT]  
>  Wenn Sie ein Ablaufverfolgungsflag angeben, sollten Sie **-T** verwenden, um die Nummer des Ablaufverfolgungsflags zu übergeben. Der Kleinbuchstabe „t“ (**-t**) wird von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]akzeptiert. Mit **-t** werden jedoch andere interne Ablaufverfolgungsflags festgelegt, die von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Supporttechnikern benötigt werden.  
  
 **-v**  
 Zeigt die Serverversionsnummer an.  
  
 **-x**  
 Deaktiviert die Kontrolle der CPU-Zeit und die Statistik für die Cachetrefferquote. Ermöglicht die maximale Leistung.  
  
 **-g** _memory_to_reserve_  
 Gibt in Form einer ganzen Zahl an, wie viele Megabytes (MB) des Arbeitsspeichers [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für Speicherbelegungen innerhalb des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Prozesses, jedoch außerhalb des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Speicherpools übrig lässt. Der Arbeitsspeicher außerhalb des Speicherpools ist der Bereich, der von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zum Laden von Elementen, z. B. `.dll` -Dateien von erweiterten gespeicherten Prozeduren, den OLE DB-Anbietern, auf die in verteilten Abfragen verwiesen wird, und Automatisierungsobjekten, auf die in [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen verwiesen wird, verwendet wird. Die Standardeinstellung ist 256 MB.  
  
 Diese Option kann Ihnen helfen, die Speicherbelegung zu optimieren. Dies gilt jedoch nur, wenn der physische Speicher die konfigurierte Grenze überschreitet, die vom Betriebssystem für den virtuellen Arbeitsspeicher, der für Anwendungen verfügbar ist, festgelegt wird. Die Verwendung dieser Option kann für Konfigurationen mit sehr viel Arbeitsspeicher geeignet sein, bei denen die Anforderungen an die Speicherauslastung von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] untypisch sind und der virtuelle Adressraum des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Prozesses vollständig verwendet wird. Eine falsche Verwendung dieser Option kann dazu führen, dass eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz nicht gestartet werden kann oder dass Laufzeitfehler auftreten.  
  
 Verwenden Sie den Standardwert für den **-g** -Parameter, es sei denn, das [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Fehlerprotokoll enthält eine der folgenden Warnungen:  
  
-   „Failed Virtual Allocate Bytes: FAIL_VIRTUAL_RESERVE \<size>“  
  
-   „Failed Virtual Allocate Bytes: FAIL_VIRTUAL_COMMIT <Größe\<“  
  
 Diese Meldungen können darauf hinweisen, dass [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] versucht, Teile des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Speicherpools freizugeben, um Speicherplatz für Elemente wie DLL-Dateien von erweiterten gespeicherten Prozeduren oder Automatisierungsobjekte zu erhalten. In diesem Fall sollten Sie erwägen, den durch den Schalter **-g**reservierten Umfang an Arbeitsspeicher zu erhöhen.  
  
 Wenn Sie einen Wert verwenden, der niedriger als der Standardwert ist, erhöht sich dadurch der Umfang des Arbeitsspeichers, der für den Pufferpool und die Threadstapel zur Verfügung steht. Dies kann wiederum eine gewisse Verbesserung der Leistung für arbeitsspeicherintensive Arbeitsauslastungen in Systemen bedeuten, die nicht viele erweiterte gespeicherte Prozeduren, verteilte Abfragen oder Automatisierungsobjekte verwenden.  
  
## <a name="remarks"></a>Bemerkungen  
 In den meisten Fällen wird das Programm sqlserver.exe nur zur Problembehandlung oder für größere Wartungsarbeiten verwendet. Wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe von „sqlservr.exe“ von der Eingabeaufforderung aus gestartet wird, wird [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nicht als Dienst gestartet. Es ist daher nicht möglich, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe von **net** -Befehlen zu beenden. Benutzer können eine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]herstellen, aber die Tools von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zeigen den Status des Dienstes an. Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konfigurations-Manager gibt daher vollkommen richtig an, dass der Dienst beendet wurde. 
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] kann eine Verbindung zum Server herstellen, gibt jedoch ebenfalls an, dass der Dienst beendet wurde.  
  
## <a name="compatibility-support"></a>Kompatibilitätsunterstützung  
 Der **-h**  -Parameter wird in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]nicht unterstützt. Dieser Parameter wurde in früheren Versionen der 32-Bit-Instanzen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet, um virtuellen Adressraum für Metadaten zum Hinzufügen von Speicher im laufenden Systembetrieb (Hot Add Memory) zu reservieren, wenn AWE aktiviert ist. Weitere Informationen finden Sie unter [Nicht mehr unterstützte SQL Server-Funktionen in SQL Server 2014](../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md).  
  
## <a name="see-also"></a>Weitere Informationen  
 [Startoptionen für den Datenbank-Engine-Dienst](../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
