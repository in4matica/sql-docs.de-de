---
title: Bewährte Methoden für den Abfragespeicher | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: carlrab
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
author: pmasl
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c07131e3991fd7cceb77e1874b7150184345b546
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338883"
---
# <a name="best-practices-with-query-store"></a>Bewährte Methoden für den Abfragespeicher

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

In diesem Artikel werden die bewährten Methoden für den Einsatz des SQL Server-Abfragespeichers mit Ihrer Arbeitsauslastung vorgestellt.

## <a name="SSMS"></a> Verwenden des neuesten [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügt über mehrere Benutzeroberflächen, die zum Konfigurieren des Abfragespeichers und zur Nutzung der gesammelten Daten über Ihre Arbeitsauslastung konzipiert wurden. Laden Sie die neueste Version von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] [hier](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) herunter.

Eine kurze Beschreibung zur Verwendung des Abfragespeichers bei Fehlerbehebungen finden Sie in den [@AzureBlogs zu Abfragespeichern](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

## <a name="Insight"></a> Verwenden von Query Performance Insight in Azure SQL-Datenbank

Wenn Sie Abfragespeicher in Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ausführen, können Sie [Query Performance Insight](https://docs.microsoft.com/azure/sql-database/sql-database-query-performance) verwenden, um den Ressourcenverbrauch im Laufe der Zeit zu analysieren. Obwohl Sie und [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) verwenden können, um einen detaillierten Ressourcenverbrauch für alle Abfragen zu erhalten, wie z. b. CPU, Arbeitsspeicher und e/a, bietet Query Performance Insight eine schnelle und effiziente Möglichkeit, um ihre Auswirkungen auf den gesamten DTU-Verbrauch für Ihre Datenbank zu ermitteln. Weitere Informationen finden Sie unter [Query Performance Insight für Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/).

In diesem Abschnitt werden optimale Konfigurations Standardwerte beschrieben, die entworfen wurden, um den zuverlässigen Betrieb der Abfragespeicher und der abhängigen Features sicherzustellen. Die Standardkonfiguration ist für die fortlaufende Datensammlung optimiert. Dies bedeutet, dass möglichst wenig Zeit im Status OFF bzw. READ_ONLY verbracht wird.

| Konfiguration | BESCHREIBUNG | Standard | Comment |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Gibt das Limit für den Datenspeicherplatz an, den der Abfragespeicher in der Kundendatenbank belegt. |100 |Für neue Datenbanken erzwungen |
| INTERVAL_LENGTH_MINUTES |Definiert die Größe des Zeitfensters, in dem gesammelte Laufzeitstatistiken für Abfragepläne aggregiert und dauerhaft gespeichert werden. Jeder aktive Abfrageplan verfügt über maximal eine Zeile für einen mit dieser Konfiguration definierten Zeitraum. |60 |Für neue Datenbanken erzwungen |
| STALE_QUERY_THRESHOLD_DAYS |Zeitbasierte Bereinigungsrichtlinie, mit der der Aufbewahrungszeitraum für dauerhaft gespeicherte Laufzeitstatistiken und inaktive Abfragen gesteuert wird. |30 |Für neue Datenbanken und Datenbanken mit vorheriger Standardeinstellung erzwungen (367) |
| SIZE_BASED_CLEANUP_MODE |Gibt an, ob die automatische Datenbereinigung durchgeführt wird, wenn der Datenumfang des Abfragespeichers sich dem Grenzwert nähert. |AUTO |Für alle Datenbanken erzwungen |
| QUERY_CAPTURE_MODE |Gibt an, ob die Gesamtmenge aller Abfragen oder nur eine Teilmenge der Abfragen nachverfolgt wird. |AUTO |Für alle Datenbanken erzwungen |
| FLUSH_INTERVAL_SECONDS |Gibt an, wie lange gesammelte Laufzeitstatistiken maximal im Arbeitsspeicher aufbewahrt werden, bevor eine Leerung auf einen Datenträger erfolgt. |900 |Für neue Datenbanken erzwungen |
| | | | |

> [!IMPORTANT]
> Diese Standardeinstellungen werden in der letzten Phase der Abfragespeicheraktivierung automatisch auf alle Azure SQL-Datenbanken angewendet (siehe wichtigen Hinweis oben). Nach dieser Beleuchtung werden von der Azure SQL-Datenbank keine von Kunden festgelegten Konfigurationswerte geändert, es sei denn, Sie wirken sich negativ auf die primäre Arbeitsauslastung oder den zuverlässigen Betrieb des Abfragespeicher aus.

Wenn Sie weiterhin Ihre benutzerdefinierten Einstellungen nutzen möchten, helfen Ihnen die Informationen unter [ALTER DATABASE SET-Optionen (Transact-SQL)](https://msdn.microsoft.com/library/bb522682.aspx) weiter, um die Konfiguration wieder in den vorherigen Zustand zu versetzen. Lesen Sie den Artikel [Bewährte Methoden für den Abfragespeicher](https://msdn.microsoft.com/library/mt604821.aspx) , um zu erfahren, wie Sie die optimalen Konfigurationsparameter auswählen.

## <a name="use-query-store-with-elastic-pool-databases"></a>Verwenden des Abfragespeichers mit Pools für elastische Datenbanken

Sie können den Abfragespeicher bedenkenlos in allen Datenbanken verwenden, selbst in dicht gepackten Pools. Alle mit übermäßiger Ressourcennutzung zusammenhängenden Probleme, die bei der Aktivierung des Abfragespeichers für die große Anzahl Datenbanken in Pools für elastische Datenbanken auftreten konnten, wurden behoben.

## <a name="Configure"></a>Halten Sie Abfragespeicher an ihre Arbeitsauslastung angepasst.

Konfigurieren Sie Abfragespeicher basierend auf den Anforderungen hinsichtlich der Arbeitsauslastung und der Behandlung von Leistungsproblemen.
Die Standardparameter sind für den Einstieg ausreichend, Sie sollten jedoch das Verhalten des Abfragespeichers im Verlauf der Zeit überwachen und die Konfiguration entsprechend anpassen.

 ![Eigenschaften von Abfragespeicher](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")

 Hier sind einige Richtlinien zum Festlegen der Parameterwerte:

**Max size (MB)**: gibt den Grenzwert für den Datenbereich an, der von Abfragespeicher in der Datenbank benötigt wird. Dies ist die wichtigste Einstellung, die sich direkt auf den Betriebsmodus des Abfragespeichers auswirkt.

Während der Abfragespeicher Abfragen, Ausführungspläne und Statistiken sammelt, wächst die Datenbank an, bis dieser Grenzwert erreicht ist. In diesem Fall ändert der Abfragespeicher automatisch den Betriebsmodus in schreibgeschützt und beendet die Erfassung von neuen Daten, sodass die Leistungsanalyse nicht mehr korrekt ist.

Der Standardwert in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ist 100 MB. Diese Größe reicht möglicherweise nicht aus, wenn die Arbeitsauslastung eine große Anzahl unterschiedlicher Abfragen und Pläne generiert oder wenn der Abfrageverlauf einen längeren Zeitraum aufbewahrt werden soll. Ab [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] beträgt der Standardwert 1 GB. Verfolgen Sie den aktuellen Speicherplatz und erhöhen Sie den Wert für **Maximale Größe (MB)**, um zu verhindern, dass der Abfragespeicher in den schreibgeschützten Modus übergeht.

> [!IMPORTANT]
> Der Grenzwert **Maximale Größe (MB)** wird nicht erzwungen. Die Speichergröße wird nur überprüft, wenn der Abfragespeicher Daten auf einen Datenträger schreibt. Das Intervall wird durch die Option **Datenleerungsintervall (Minuten)** festgelegt. Wenn der Abfragespeicher die maximale Größe zwischen Speichergrößenüberprüfungen überschritten hat, geht er in den schreibgeschützten Modus über. Bei Aktivierung von **Größenbasierter Bereinigungsmodus** wird auch der Bereinigungsmechanismus zum Erzwingen der maximalen Größe ausgelöst.

Verwenden Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , oder führen Sie das folgende Skript aus, um aktuelle Informationen zur Größe des Abfragespeichers zu erhalten:

```sql
USE [QueryStoreDB];
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
 max_storage_size_mb, readonly_reason
FROM sys.database_query_store_options;
```

Im folgenden Skript wird ein neuer Wert für **Maximale Größe (MB)** festgelegt:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);
```

 **Daten Leerungs Intervall (Minuten)**: definiert die Häufigkeit, mit der gesammelte Lauf Zeit Statistiken auf dem Datenträger persistent gespeichert werden. In der grafischen Benutzeroberfläche wird sie in Minuten ausgedrückt, in [!INCLUDE[tsql](../../includes/tsql-md.md)] wird sie jedoch in Sekunden angegeben. Der Standardwert ist 900 Sekunden, d.h. 15 Minuten in der grafischen Benutzeroberfläche. Ziehen Sie in Betracht, einen höheren Wert zu verwenden, wenn Ihre Arbeitsauslastung keine große Anzahl verschiedener Abfragen und Pläne generiert oder Sie längere Zeit warten können, bevor Daten vor dem Herunterfahren der Datenbank persistent gespeichert werden.

> [!NOTE]
> Mit dem Ablaufverfolgungsflag 7745 wird verhindert, dass Abfragespeicherdaten bei einem Failover oder Befehl zum Herunterfahren auf den Datenträger geschrieben werden. Weitere Informationen finden Sie im Abschnitt [Verwenden von Ablaufverfolgungsflags für unternehmenskritische Server](#Recovery) .

Verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)], um verschiedene Werte für das **Datenleerungsintervall** festzulegen:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS = 900);
```

**Statistik Sammlungs Intervall**: definiert den Grad der Granularität für die gesammelte Lauf Zeit Statistik (ausgedrückt in Minuten). Der Standardwert ist 60 Minuten. Es ist ratsam, einen niedrigeren Wert zu verwenden, wenn Sie eine höhere Granularität benötigen oder weniger Zeit zum Erkennen und Verringern von Problemen haben. Denken Sie daran, dass der Wert die Größe der Abfragespeicherdaten direkt beeinflusst. Verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)], um einen anderen Wert für das **Statistiksammlungsintervall** festzulegen:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);
```

**Schwellenwert für veraltete Abfragen (Tage)**: zeitbasierte Bereinigungs Richtlinie, mit der die Beibehaltungs Dauer von beibehaltenen Lauf Zeit Statistiken und inaktiven Abfragen (in Tagen) gesteuert wird. Standardmäßig ist der Abfragespeicher so konfiguriert, dass Daten 30 Tage lang gespeichert werden. Dies ist möglicherweise für Ihr Szenario unnötig lange.

Vermeiden Sie es, Verlaufsdaten aufzubewahren, die Sie nicht mehr verwenden möchten. Dies reduziert die Wahrscheinlichkeit für Änderungen in den schreibgeschützten Status. Die Größe der Abfragespeicherdaten sowie die Zeit, um Probleme zu erkennen und zu mindern, lassen sich besser vorhersagen. Verwenden Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder das folgende Skript, um die zeitbasierte Cleanuprichtlinie zu konfigurieren:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));
```

**Größen basierter Bereinigungs Modus**: gibt an, ob eine automatische Datenbereinigung stattfindet, wenn Abfragespeicher Datengröße den Grenzwert erreicht. Aktivieren Sie die größenbasierte Bereinigung, um sicherzustellen, dass der Abfragespeicher immer im Lese-/ Schreibmodus ausgeführt wird und die neuesten Daten erfasst.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);
```

**Abfragespeicher Erfassungs Modus**: gibt die Abfrage Erfassungs Richtlinie für Abfragespeicher an.

- **All**: erfasst alle Abfragen. Diese Option ist die Standardeinstellung in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].
- **Auto**: seltene Abfragen und Abfragen mit unbedeutender Kompilierungs-und Ausführungsdauer werden ignoriert. Die Schwellenwerte für die Dauer der Ausführungsanzahl, Kompilierung und Laufzeit werden intern bestimmt. Ab [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] ist dies die Standardoption.
- **None**: Abfragespeicher beendet die Erfassung neuer Abfragen.
- **Custom**: ermöglicht eine zusätzliche Steuerung und die Möglichkeit, die Richtlinie zur Datenerfassung zu optimieren. Die neuen benutzerdefinierten Einstellungen definieren, was während des Zeitschwellenwerts für die interne Erfassungsrichtlinie geschieht. Hierbei handelt es sich um eine Zeitbegrenzung, in der die konfigurierbaren Bedingungen ausgewertet werden, und trifft eine davon zu, ist die Abfrage geeignet, von Abfragespeicher aufgezeichnet zu werden.

> [!IMPORTANT]
> Cursor, Abfragen in gespeicherten Prozeduren und nativ kompilierte Abfragen werden immer erfasst, wenn der Erfassungsmodus für den Abfragespeicher auf **Alle** (ALL), **Automatisch** (AUTO) oder **Benutzerdefiniert** (CUSTOM) festgelegt ist. Zum Erfassen von nativ kompilierten Abfragen aktivieren Sie die Sammlung von Statistiken pro Abfrage mithilfe von [sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).

 Das folgende Skript legt QUERY_CAPTURE_MODE auf AUTO fest:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);
```

### <a name="examples"></a>Beispiele

Im folgenden Beispiel wird QUERY_CAPTURE_MODE auf AUTO gesetzt und es werden weitere empfohlene Optionen in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] festgelegt:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60
    );
```

Im folgenden Beispiel wird QUERY_CAPTURE_MODE auf AUTO gesetzt und es werden weitere empfohlene Optionen in [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] zum Einschließen von Wartezeitstatistiken festgelegt:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

Im folgenden Beispiel wird QUERY_CAPTURE_MODE auf AUTO gesetzt und es werden weitere empfohlene Optionen in [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] festgelegt. *Optional* wird anstelle des neuen Erfassungsmodus AUTO die benutzerdefinierte (CUSTOM) Erfassungsrichtlinie mit den zugehörigen Standardeinstellungen festgelegt:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100
      )
    );
```

## <a name="start-with-query-performance-troubleshooting"></a>Erste Schritte bei der Behandlung von Leistungsproblemen

Der Workflow zur Behandlung von Problemen mit dem Abfragespeicher ist einfach, wie im folgenden Diagramm dargestellt:

![Abfragespeicher Problembehandlung](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")

Aktivieren Sie den Abfragespeicher mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], wie im vorherigen Abschnitt beschrieben, oder führen Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung aus:

```sql
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;
```

Es dauert einige Zeit, bis der Abfragespeicher das Dataset erfasst, das Ihre Arbeitsauslastung präzise darstellt. In der Regel reicht ein Tag, selbst bei sehr komplexen Arbeitsauslastungen. Sie können jedoch unmittelbar nach Aktivierung der Funktion damit beginnen, die Daten zu untersuchen und Abfragen zu identifizieren, die Ihre Aufmerksamkeit erfordern. Navigieren Sie zu dem Abfragespeicher-Unterordner unter dem Datenbankknoten im Objekt-Explorer von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], um Problembehandlungsansichten für bestimmte Szenarios zu öffnen.


  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] -Abfragespeicheransichten arbeiten mit dem Satz von Ausführungsmetriken, die alle als eine der folgenden Statistikfunktionen ausgedrückt werden:

|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version|Ausführungsmetrik|Statistikfunktion|
|----------------------|----------------------|------------------------|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|CPU-Zeit, Dauer, Ausführungsanzahl, logische Lesevorgänge, logische Schreibvorgänge, Speicherverbrauch, physische Lesevorgänge, CLR-Zeit, Parallelitätsgrad (Degree of Parallelism, DOP) und Zeilenanzahl|Durchschnitt, Maximum, Minimum, Standardabweichung, Gesamt|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|CPU-Zeit, Dauer, Ausführungsanzahl, logische Lesevorgänge, logische Schreibvorgänge, Speicherverbrauch, physische Lesevorgänge, CLR-Zeit, Parallelitätsgrad, Zeilenanzahl, Protokollspeicher, TempDB-Speicher und Wartezeiten|Durchschnitt, Maximum, Minimum, Standardabweichung, Gesamt|

Die folgende Grafik veranschaulicht, wie Sie die Abfragespeicheransichten suchen:

![Ansichten von Abfragespeichern](../../relational-databases/performance/media/objectexplorerquerystore_sql17.png "Ansichten von Abfragespeichern")

In der folgenden Tabelle wird erläutert, wann Sie die einzelnen Abfragespeicheransichten verwenden sollten:

|SQL Server Management Studio-Ansicht|Szenario|
|---------------|--------------|
|**Zurück gestellte Abfragen**|Identifizieren von Abfragen, bei denen die Ausführungsmetriken vor kurzem rückläufig waren (z.B. sich verschlechtert haben). <br />Verwenden Sie diese Ansicht, um beobachtete Leistungsprobleme in Ihrer Anwendung mit den tatsächlichen Abfragen zu korrelieren, die korrigiert oder verbessert werden müssen.|
|**Gesamter Ressourcenverbrauch**|Analysieren Sie den Gesamtressourcenverbrauch für die Datenbank für eine der Ausführungsmetriken.<br />Verwenden Sie diese Ansicht, um Ressourcenmuster zu identifizieren (tägliche im Vergleich zu nächtlichen Arbeitsauslastungen), und optimieren Sie den Gesamtverbrauch für Ihre Datenbank.|
|**Abfragen mit dem höchsten Ressourcenverbrauch**|Wählen Sie die gewünschte Ausführungsmetrik, und identifizieren Sie Abfragen mit den extremsten Werten für ein angegebenes Zeitintervall. <br />Verwenden Sie diese Ansicht, um sich auf die relevantesten Abfragen zu konzentrieren, die die größte Auswirkung auf den Ressourcenverbrauch der Datenbank haben.|
|**Abfragen mit erzwungenen Plänen**|Zeigt vorherige erzwungene Pläne durch Verwendung des Abfragespeichers an. <br />Verwenden Sie diese Ansicht, um schnell auf alle aktuell erzwungenen Pläne zuzugreifen.|
|**Abfragen mit hoher Variation**|Analysieren Sie Abfragen mit hoher Ausführungsvariation in Verbindung mit allen verfügbaren Dimensionen wie Dauer, CPU-Zeit, E/A und Speicherauslastung im gewünschten Zeitintervall.<br />Verwenden Sie diese Ansicht, um Abfragen mit stark abweichender Leistung zu identifizieren, die die Benutzerfreundlichkeit in Ihren Anwendungen beeinträchtigen können.|
|**Statistik für Abfrage Wartezeit**|Analysieren Sie Wartekategorien, die in einer Datenbank am aktivsten sind, sowie welche Abfragen am meisten zur ausgewählten Wartekategorie beitragen.<br />Verwenden Sie diese Ansicht, um Wartezeitstatistiken zu analysieren und Abfragen zu identifizieren, die sich auf die Benutzerfreundlichkeit in Ihren Anwendungen auswirken können.<br /><br />Gilt für: ab [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v 18,0 und. [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|
|**Nach verfolgte Abfragen**|Verfolgen Sie die Ausführung der wichtigsten Abfragen in Echtzeit. In der Regel verwenden Sie diese Ansicht, wenn Sie über Abfragen mit erzwungenen Plänen verfügen und Sie sicherstellen möchten, dass die Abfrageleistung stabil ist.|

> [!TIP]
> Eine ausführliche Beschreibung dazu, wie Sie mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] die Abfragen mit dem größten Ressourcenverbrauch identifizieren und diejenigen Abfragen korrigieren können, die aufgrund der Änderung der Planauswahl zurückgestellt wurden, finden Sie in den [Blogs zu Abfragespeichern@Azure](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

Wenn Sie eine Abfrage mit nicht optimaler Leistung identifiziert haben, richtet sich das weitere Vorgehen nach der Art des Problems.

- Wenn die Abfrage mit mehreren Plänen ausgeführt wurde und der letzte Plan signifikant schlechter als der vorherige ist, können Sie den Planerzwingungsmechanismus verwenden, um diesen zu erzwingen. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht, den Plan im Optimierer zu erzwingen. Wenn das Erzwingen des Plans fehlschlägt, wird ein XEvent ausgelöst, und der Optimierer wird angewiesen, die Optimierung auf die übliche Weise durchzuführen.

  ![Abfragespeicher Force-Plan](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")

  > [!NOTE]
  > Die vorherige Abbildung kann verschiedene Formen für bestimmte Abfragepläne aufweisen, wobei die möglichen Status folgende Bedeutungen haben:<br />
  >
  > |Form|Bedeutung|
  > |-------------------|-------------|
  > |Circle|Abfrage abgeschlossen, d.h., dass eine reguläre Ausführung erfolgreich abgeschlossen wurde.|
  > |Quadrat|Abgebrochen, d.h., dass ein vom Client initiierter Abbruch der Ausführung erfolgte.|
  > |Triangle|Fehlerhaft, d.h., dass die Ausführung durch eine Ausnahme abgebrochen wurde.|
  >
  > Darüber hinaus gibt die Größe der Form Aufschluss über die Anzahl von Abfrageausführungen innerhalb des angegebenen Zeitintervalls. Die Größe der Form nimmt mit zunehmender Anzahl von Ausführungen zu.

- Sie können daraus schließen, dass der Abfrage ein Index für eine optimale Ausführung fehlt. Diese Informationen werden innerhalb des Abfrageausführungsplans eingeblendet. Erstellen Sie den fehlenden Index, und überprüfen Sie den Speicher Abfrageleistung nach usingquery.

   ![Abfragespeicher Plan anzeigen](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")

Wenn Sie Ihre Arbeitsauslastung auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ausführen, registrieren Sie sich für den [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Indexratgeber, um automatisch Indexempfehlungen zu erhalten.

- In einigen Fällen können Sie eine statistische Neukompilierung erzwingen, wenn Sie feststellen, dass der Unterschied zwischen der geschätzten und der tatsächlichen Anzahl der Zeilen im Ausführungsplan maßgeblich ist.
- Schreiben Sie problematische Abfragen neu, beispielsweise, um die Vorteile der Abfrageparametrisierung nutzen zu können oder um eine bessere Logik zu implementieren.

## <a name="Verify"></a>Überprüfen, ob Abfragespeicher kontinuierlich Abfrage Daten sammelt

Der Abfragespeicher kann den Betriebsmodus automatisch ändern. Überwachen Sie regelmäßig den Status des Abfragespeichers, um sicherzustellen, dass der Abfragespeicher funktioniert, und um Maßnahmen zu ergreifen, damit so Ausfälle aufgrund von vermeidbaren Ursachen verhindert werden. Führen Sie die folgende Abfrage aus, um den Betriebsmodus zu ermitteln und die wichtigsten Parameter anzuzeigen:

```sql
USE [QueryStoreDB];
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_desc
FROM sys.database_query_store_options;
```

Der Unterschied zwischen `actual_state_desc` und `desired_state_desc` weist darauf hin, dass automatisch eine Änderung des Betriebsmodus aufgetreten ist. Die häufigste Änderung besteht darin, dass der Abfragespeicher im Hintergrund in den schreibgeschützten Modus wechselt. In sehr seltenen Fällen kann sich der Abfragespeicher in einem fehlerhaften Zustand aufgrund von internen Fehlern befinden.

Wenn der tatsächliche Status schreibgeschützt ist, verwenden Sie die **readonly_reason** -Spalte, um die Ursache zu ermitteln. In der Regel werden Sie feststellen, dass der Abfragespeicher in den schreibgeschützten Modus gewechselt hat, da das Kontingent überschritten wurde. In diesem Fall wird **readonly_reason** auf 65536 festgelegt. Andere Gründe finden Sie unter [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).

Ziehen Sie die folgenden Schritte in Betracht, um den Abfragespeicher in den schreibgeschützten Modus zu schalten und die Datensammlung zu aktivieren:

- Erhöhen Sie die maximale Speichergröße mithilfe der **MAX_STORAGE_SIZE_MB** -Option von **ALTER DATABASE**.
- Bereinigen Sie die Abfragespeicherdaten mithilfe der folgenden Anweisung:

  ```sql
  ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;
  ```

Wenden Sie einen oder beide der folgenden Schritte an, indem Sie die folgende Anweisung ausführen, die den Betriebsmodus explizit wieder in den Lese-/ Schreibzugriff zurücksetzt:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
```

Gehen Sie proaktiv folgendermaßen vor:

- Sie können die automatischen Änderungen des Betriebsmodus durch Anwenden bewährter Methoden verhindern. Stellen Sie sicher, dass die Abfragespeichergröße immer unterhalb des maximal zulässigen Werts liegt, um so die Wahrscheinlichkeit des Übergangs in den schreibgeschützten Modus maßgeblich zu verringern. Aktivieren Sie die größenbasierte Richtlinie, wie im Abschnitt zum [Konfigurieren des Abfragespeichers](#Configure) beschrieben, sodass der Abfragespeicher die Daten automatisch bereinigt, wenn sich die Größe dem Grenzwert nähert.
- Um sicherzustellen, dass die neuesten Daten beibehalten werden, konfigurieren Sie die zeitbasierte Richtlinie, um regelmäßig veraltete Informationen zu entfernen.
- Nicht zuletzt sollten Sie es in Betracht ziehen, den **Erfassungsmodus für den Abfragespeicher** auf **Automatisch** einzustellen, da dadurch Abfragen herausgefiltert werden, die in der Regel weniger relevant für Ihre Arbeitsauslastung sind.

### <a name="error-state"></a>Fehlerzustand

Zum Wiederherstellen des Abfragespeichers versuchen Sie explizit den Lese-/Schreibmodus einzustellen, und prüfen Sie den tatsächlichen Status noch mal.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_desc
FROM sys.database_query_store_options;
```

Wenn das Problem weiterhin besteht, bedeutet dies, dass die beschädigten Abfragespeicherdaten auf dem Datenträger beibehalten werden.

Ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] kann der Abfragespeicher wiederhergestellt werden, indem die gespeicherte Prozedur **sp_query_store_consistency_check** in der betroffenen Datenbank ausgeführt wird. Der Abfragespeicher muss vor dem Wiederherstellungsvorgang deaktiviert werden. Für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] müssen Sie die Daten aus dem Abfragespeicher, wie gezeigt, löschen.

Wenn die Wiederherstellung nicht erfolgreich war, können Sie versuchen, den Abfragespeicher vor dem Aktivieren des Lese-/Schreibmodus zu löschen.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE CLEAR;
GO

ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_de
FROM sys.database_query_store_options;
```

## <a name="set-the-optimal-query-store-capture-mode"></a>Festlegen des optimalen Erfassungsmodus für den Abfragespeicher

Behalten Sie die relevantesten Daten im Abfragespeicher. Die folgende Tabelle beschreibt die typischen Szenarios für jeden Erfassungsmodus für den Abfragespeicher:

|Erfassungsmodus für den Abfragespeicher|Szenario|
|------------------------|--------------|
|**Alle**|Analysieren Sie Ihre Arbeitsauslastung sorgfältig im Hinblick auf alle Abfrageformen und deren Ausführungshäufigkeit und andere Statistiken.<br /><br /> Identifizieren Sie neue Abfragen in Ihrer Workload.<br /><br /> Erkennen Sie, ob Ad-hoc-Abfragen verwendet werden, um Möglichkeiten für Benutzer oder eine automatische Parametrisierung zu identifizieren.<br /><br />Hinweis: Dies ist der Standard Erfassungs Modus [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] in [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]und.|
|**Auto**|Konzentrieren Sie sich auf relevante und verwertbare Abfragen. Zum Beispiel auf jene Abfragen, die regelmäßig ausgeführt werden oder einen erheblichen Ressourcenverbrauch aufweisen.<br /><br />Hinweis: ab [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]ist dies der Standard Erfassungs Modus.|
|**None**|Sie haben bereits den Abfragesatz erfasst, den Sie während der Laufzeit überwachen möchten, und möchten nun Ablenkungen beseitigen, die durch andere Abfragen entstehen können.<br /><br /> „Keine“ ist für Testzwecke geeignet sowie für Vergleichsumgebungen.<br /><br /> „Keine“ eignet sich auch für Softwareanbieter, die bei Auslieferung die Abfragespeicherkonfiguration so festlegen, dass die Anwendungsauslastung überwacht wird.<br /><br /> „Keine“ sollte mit Bedacht verwendet werden, da Sie womöglich die Gelegenheit verpassen, wichtige neue Abfragen nachzuverfolgen und zu optimieren. Vermeiden Sie den Einsatz von „Keine“, es sei denn es ist für ein bestimmtes Szenario erforderlich.|
|**Benutzerdefiniert**|Mit [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] wurde ein benutzerdefinierter Erfassungsmodus für den `ALTER DATABASE SET QUERY_STORE`-Befehl eingeführt. Bei Aktivierung stehen zusätzliche Abfragespeicherkonfigurationen unter einer neuen Einstellung für die Erfassungsrichtlinie des Abfragespeichers zur Verfügung, um die Datensammlung auf einem bestimmten Server zu optimieren.<br /><br />Die neuen benutzerdefinierten Einstellungen definieren, was während des Zeitschwellenwerts für die interne Erfassungsrichtlinie geschieht. Hierbei handelt es sich um eine Zeitbegrenzung, in der die konfigurierbaren Bedingungen ausgewertet werden, und trifft eine davon zu, ist die Abfrage geeignet, von Abfragespeicher aufgezeichnet zu werden. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|

> [!NOTE]
> Cursor, Abfragen in gespeicherten Prozeduren und nativ kompilierte Abfragen werden immer erfasst, wenn der Erfassungsmodus für den Abfragespeicher auf **Alle** (ALL), **Automatisch** (AUTO) oder **Benutzerdefiniert** (CUSTOM) festgelegt ist. Zum Erfassen von nativ kompilierten Abfragen aktivieren Sie die Sammlung von Statistiken pro Abfrage mithilfe von [sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).

## <a name="keep-the-most-relevant-data-in-query-store"></a>Aufbewahren der relevantesten Daten im Abfragespeicher

Konfigurieren Sie den Abfragespeicher so, dass nur die relevanten Daten enthalten sind. Dann wird er kontinuierlich ausgeführt, was die Problembehandlung erheblich vereinfacht bei minimalen Auswirkungen auf die normale Arbeitsauslastung.
Die folgende Tabelle enthält bewährte Methoden:

|Bewährte Methode|Einstellung|
|-------------------|-------------|
|Begrenzen der Menge von beibehaltenen Verlaufsdaten.|Konfigurieren Sie die zeitbasierte Richtlinie, um die automatische Bereinigung zu aktivieren.|
|Filtern Sie nicht relevante Abfragen heraus.|Konfigurieren Sie den **Erfassungsmodus für den Abfragespeicher** als **Automatisch**.|
|Löschen Sie weniger relevanten Abfragen, wenn die maximale Größe erreicht ist.|Aktivieren Sie die größenbasierte Cleanuprichtlinie.|

## <a name="Parameterize"></a>Vermeiden Sie die Verwendung von nicht parametrisierten Abfragen.

Es wird nicht empfohlen, parametrisierte Abfragen zu verwenden, wenn dies nicht erforderlich ist. Ein Beispiel hierfür ist die Ad-hoc-Analyse. Zwischengespeicherte Pläne können nicht wiederverwendet werden, sodass der Abfrageoptimierer gezwungen ist, Abfragen für jeden eindeutigen Abfragetext zu kompilieren. Weitere Informationen finden Sie unter [Richtlinien für die Verwendung der erzwungenen Parametrisierung](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide).

Der Abfragespeicher kann darüber hinaus schnell die Kontingentgröße aufgrund einer potenziell großen Anzahl von verschiedenen Abfragetexten und somit einer großen Anzahl von verschiedenen Ausführungsplänen mit ähnlicher Form überschreiten. Daher wird die Leistung Ihrer Arbeitsauslastung suboptimal sein, und der Abfragespeicher wechselt möglicherweise in den schreibgeschützten Modus oder löscht kontinuierlich die Daten, um mit den eingehenden Abfragen Schritt zu halten.

Betrachten Sie die folgenden Optionen:

- Parametrisieren Sie Abfragen, sofern möglich. Beispielsweise indem Sie Abfragen innerhalb einer gespeicherten Prozedur oder sp_executesql umschließen. Weitere Informationen finden Sie unter [Parameter und Wiederverwendung von Ausführungsplänen](../../relational-databases/query-processing-architecture-guide.md#PlanReuse).
- Verwenden Sie die Option [Für Ad-hoc-Arbeitsauslastungen optimieren](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md), wenn Ihre Arbeitsauslastung viele einmalige Ad-hoc-Batches mit anderen Abfrageplänen enthält.
  - Vergleichen Sie die Anzahl der unterschiedlichen query_hash-Werte mit der Gesamtanzahl von Einträgen in sys.query_store_query. Ist das Verhältnis nahe 1, generiert Ihre Ad-hoc-Arbeitsauslastung verschiedene Abfragen.
- Wenden Sie die [erzwungene Parametrisierung](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) auf die Datenbank oder auf eine Teilmenge der Abfragen an, wenn die Anzahl der unterschiedlichen Abfragepläne nicht groß ist.
  - Verwenden Sie die [Planhinweisliste](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md), um die Parametrisierung nur für die ausgewählte Abfrage zu erzwingen.
  - Konfigurieren Sie die erzwungene Parametrisierung über den Befehl für die [Option zur Parametrisierung der Datenbank](../../relational-databases/databases/database-properties-options-page.md#miscellaneous), wenn Ihre Arbeitsauslastung eine kleine Anzahl von unterschiedlichen Abfragepläne umfasst. Ein Beispiel: Das Verhältnis zwischen der Anzahl der unterschiedlichen query_hash und der Gesamtanzahl der Einträge in sys.query_store_query ist wesentlich kleiner als 1.
- Legen Sie QUERY_CAPTURE_MODE auf AUTO fest, um Ad-hoc-Abfragen mit geringem Ressourcenverbrauch automatisch herauszufiltern.

## <a name="Drop"></a>Vermeiden eines Drop-und Create-Musters für enthaltende Objekte

Der Abfragespeicher ordnet einen Abfrageeintrag einem enthaltenen Objekt zu (gespeicherte Prozedur, Funktion und Trigger). Wenn Sie ein enthaltenes Objekt neu erstellen, wird ein neuer Abfrageeintrag für den gleichen Abfragetext generiert. Dies verhindert die Nachverfolgung der Leistungsstatistiken für diese Abfrage im Verlauf der Zeit und die Anwendung eines Mechanismus zur Nutzungsplanerzwingung. Damit dies vermieden wird, verwenden Sie den `ALTER <object>`-Prozess, um die Definition des enthaltenen Objekts nach Möglichkeit zu ändern.

## <a name="CheckForced"></a>Regelmäßiges Überprüfen des Status der erzwungenen Pläne

Die Planerzwingung ist ein nützlicher Mechanismus zur Behandlung von Leistungsproblemen für kritische Abfragen, um sie besser vorhersagbar zu machen. Wie bei Planhinweisen und Planhinweislisten ist das Erzwingen eines Plans keine Garantie dafür, dass er in späteren Ausführungen verwendet wird. Wenn das Datenbankschema sich derart ändert, dass Objekte, auf die der Ausführungsplan verweist, geändert oder gelöscht werden, wird das Erzwingen eines Plans in der Regel scheitern. In diesem Fall greift [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf eine Neukompilierung der Abfrage zurück, während die tatsächliche Ursache für den Fehler beim Erzwingen in [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) ersichtlich ist. Die folgende Abfrage gibt Informationen zu erzwungenen Plänen zurück:

```sql
USE [QueryStoreDB];
GO

SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,
    force_failure_count, last_force_failure_reason_desc
FROM sys.query_store_plan AS p
JOIN sys.query_store_query AS q on p.query_id = q.query_id
WHERE is_forced_plan = 1;
```

Eine vollständige Liste der Gründe finden Sie unter [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). Sie können auch das XEvent **query_store_plan_forcing_failed** verwenden, um Fehler bei der Planerzwingung nachzuverfolgen und zu beheben.

## <a name="Renaming"></a>Vermeiden der Umbenennung von Datenbanken für Abfragen mit erzwungenen Plänen

Ausführungspläne verweisen auf Objekte mithilfe von dreiteiligen Namen wie `database.schema.object`.

Wenn Sie eine Datenbank umbenennen, wird das Erzwingen eines Plans fehlschlagen, wodurch bei allen nachfolgenden Abfrageausführungen eine Neukompilierung durchgeführt wird.

## <a name="Recovery"></a>Verwenden von Ablaufverfolgungsflags auf unternehmenskritischen Servern

Die globalen Ablaufverfolgungsflags 7745 und 7752 können verwendet werden, um die Verfügbarkeit von Datenbanken mithilfe des Abfragespeichers zu verbessern. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

- Das Ablaufverfolgungsflag 7745 verhindert, dass der Abfragespeicher standardmäßig Daten auf den Datenträger schreibt, bevor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beendet werden kann. Dies bedeutet, dass Abfragespeicherdaten, die erfasst, aber noch nicht dauerhaft auf einem Datenträger gespeichert wurden, bis zu dem mit `DATA_FLUSH_INTERVAL_SECONDS` definierten Zeitfenster verloren gehen.
- Ablaufverfolgungsflag 7752 aktiviert asynchrones Laden von Abfragespeicher. Dadurch kann eine Datenbank online geschaltet und können Abfragen ausgeführt werden, bevor der Abfragespeicher vollständig wiederhergestellt wurde. Beim Standardverhalten erfolgt ein synchrones Laden des Abfragespeichers. Das Standardverhalten verhindert, dass Abfragen ausgeführt werden, bevor der Abfragespeicher wiederhergestellt wurde, verhindert aber auch, dass irgendwelche Abfragen in der Datensammlung ignoriert werden.

> [!NOTE]
> Ab [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] wird dieses Verhalten durch die Engine gesteuert, und das Ablaufverfolgungsflag 7752 hat keine Auswirkungen.

> [!IMPORTANT]
> Wenn Sie den Abfragespeicher für Erkenntnisse zu Just-In-Time-Arbeitsauslastungen in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] verwenden, planen Sie baldmöglichst die Installation der Fixes zur Leistungsskalierbarkeit in [KB 4340759](https://support.microsoft.com/help/4340759) ein.

## <a name="see-also"></a>Weitere Informationen

- [ALTER DATABASE SET-Optionen &#40;Transact-SQL-&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)
- [Abfragespeicher Katalog Sichten &#40;Transact-SQL-&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)
- [Abfragespeicher gespeicherter Prozeduren &#40;Transact-SQL-&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)
- [Verwenden von Abfragespeicher mit in-Memory-OLTP](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)
- [Überwachen der Leistung mithilfe Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Leitfaden zur Architektur der Abfrage Verarbeitung](../../relational-databases/query-processing-architecture-guide.md)
