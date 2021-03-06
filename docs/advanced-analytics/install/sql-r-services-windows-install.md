---
title: Installieren von SQL Server 2016 R Services (datenbankintern)
description: Hier erfahren Sie, wie Sie unter Windows Unterstützung für die Programmiersprache R zu einer Datenbank-Engine in SQL Server 2016 R Services hinzufügen.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6fcb4245d4efff00002dea9b490312792e0d83d6
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338927"
---
# <a name="install-sql-server-2016-r-services"></a>Installieren von SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Artikel wird die Installation und Konfiguration von **SQL Server 2016 R Services** erläutert. Wenn Sie SQL Server 2016 besitzen, müssen Sie dieses Feature installieren, um R-Code in SQL Server ausführen zu können.

In SQL Server 2017 ist die R-Integration in [Machine Learning Services](../r/r-server-standalone.md) enthalten. Auch Python wurde hinzugefügt. Wenn Sie R integrieren möchten und ein Installationsmedium für SQL Server 2017 besitzen, finden Sie weitere Informationen zum Hinzufügen des Features unter [Installation von SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md). 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Prüfliste vor der Installation

+ Es ist eine Datenbank-Engine-Instanz erforderlich. Sie können R nicht einfach installieren, aber Sie können die Sprache inkrementell zu einer vorhandenen Instanz hinzufügen.

+ Für die Aufrechterhaltung der Geschäftskontinuität werden [Always On-Verfügbarkeitsgruppen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) für R Services unterstützt. Sie müssen auf jedem Knoten R Services installieren und Pakete konfigurieren.

+ Installieren Sie R Services nicht auf einem Failovercluster. Der Sicherheitsmechanismus, der zum Isolieren von R-Prozessen verwendet wird, ist mit einer Windows Server-Failoverclusterumgebung nicht kompatibel.

+ Installieren Sie R Services nicht auf einem Domänencontroller. Das Setup für R Services schlägt in diesem Fall fehl.

+ Installieren Sie **Freigegebene Funktionen** > **R Server (eigenständig)** nicht auf einem Computer, auf dem eine datenbankinterne Instanz ausgeführt wird. 

  Die parallele Installation anderer R- und Python-Versionen ist möglich, da die SQL Server-Instanz eigene Kopien der Open-Source-Verteilungen von R und Anaconda verwendet. Das Ausführen von Code, der R und Python auf dem SQL Server-Computer außerhalb von SQL Server verwendet, kann jedoch zu unterschiedlichen Problemen führen:
    
  + Da Sie eine andere Bibliothek und eine andere ausführbare Datei verwenden, erhalten Sie andere Ergebnisse als bei der Ausführung in SQL Server.
  + R- und Python-Skripts, die in externen Bibliotheken ausgeführt werden, können nicht von SQL Server verwaltet werden, was zu Ressourcenkonflikten führt.
  
Wenn Sie frühere Versionen der Revolution Analytics-Entwicklungsumgebung oder der RevoScaleR-Pakete verwendet oder Vorabversionen von SQL Server 2016 installiert haben, müssen Sie diese deinstallieren. Die Ausführung älterer und neuerer Versionen von RevoScaleR und anderen proprietären Paketen wird nicht unterstützt. Informationen zum Entfernen früherer Versionen finden Sie unter [Upgrade und Installation – häufig gestellte Fragen zu SQL Server Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Stellen Sie nach Abschluss des Setups sicher, dass Sie die in diesem Artikel beschriebenen zusätzlichen Schritte nach der Konfiguration durchführen. Zu diesen Schritten zählen das Aktivieren von SQL Server für die Verwendung externer Skripts und das Hinzufügen von Konten, die für SQL Server zum Ausführen Ihrer R-Aufträge erforderlich sind. Konfigurationsänderungen erfordern in der Regel einen Neustart der Instanz oder einen Neustart des Launchpad-Diensts.

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Installieren einer Patchanforderung 

Microsoft hat ein Problem bei der speziellen Version von Microsoft VC++ 2013 Runtime-Binärdateien erkannt, die von SQL Server als vorausgesetzte Komponenten installiert werden. Wenn dieses Update an den VC++ Runtime-Binärdateien nicht installiert wird, können bei SQL Server in bestimmten Szenarios Stabilitätsprobleme auftreten. Bevor Sie SQL Server installieren, sollten Sie entsprechend den Anweisungen unter [Versionsanmerkungen zu SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) vorgehen, um festzustellen, ob Ihr Computer einen Patch für die VC-Runtime-Binärdateien benötigt.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Ausführen von 'Setup'

Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.

1. Starten Sie den Setup-Assistenten für SQL Server 2016.

2. Klicken Sie auf der Registerkarte **Installation** auf **Neue eigenständige SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.
    
   ![Installation von R Services (datenbankintern)](media/2016-setup-installation-rsvcs.png "Einstieg in die Installation einer Datenbank-Engine mit R Services")
   
3. Wählen Sie folgende Optionen auf der Seite **Funktionsauswahl** aus:

   - Wählen Sie **Datenbank-Engine-Dienste** aus. Die Datenbank-Engine ist für jede Instanz erforderlich, in der Machine Learning verwendet wird.
   - Wählen Sie **R Services (datenbankintern)** aus. Durch diese Option wird die datenbankinterne Verwendung von R unterstützt.
    
     ![Featureauswahl für R Services](media/2016setup-rsvcs-features.png "Auswahl der Features für R Services (datenbankintern)")

    > [!IMPORTANT]
    > Installieren Sie R Server und R Services nicht gleichzeitig. In der Regel wird „R Server (eigenständig)“ installiert, um eine Umgebung zu schaffen, die ein Data Scientist oder Entwickler für die Herstellung einer Verbindung mit SQL Server oder die Bereitstellung von R-Lösungen verwenden kann. Daher besteht keine Notwendigkeit beide auf demselben Computer zu installieren.

4.  Klicken Sie auf der Seite **Zustimmung zur Installation von Microsoft R Open** auf **Annehmen**.
  
    Dieser Lizenzvertrag ist erforderlich, um Microsoft R Open herunterzuladen. Dort ist eine Verteilung der Open-Source-Basispakete und -Tools für R enthalten sowie erweiterte R-Pakete und Konnektivitätsanbieter des Microsoft-R-Entwicklungsteams.
  
5. Nachdem Sie den Lizenzvertrag akzeptiert haben, wird der Installer kurz vorbereitet. Klicken Sie auf **Weiter**, sobald die Schaltfläche verfügbar ist.

6. Stellen Sie auf der Seite **Installationsbereit** sicher, dass die folgenden Elemente ausgewählt sind, und klicken Sie auf **Installieren**.

   + -Datenbank-Engine-Dienste
   + R Services (In-Database)

    Notieren Sie sich den Speicherort des Ordners unter dem Pfad `..\Setup Bootstrap\Log`, in dem die Konfigurationsdateien gespeichert werden. Nach Abschluss des Setups können Sie die installierten Komponenten in der Zusammenfassungsdatei überprüfen.

7. Wenn Sie nach Abschluss des Setups dazu aufgefordert werden, starten Sie jetzt den Computer neu. Wenn Sie den Setupvorgang abgeschlossen haben, sollten Sie unbedingt die vom Installations-Assistenten angezeigte Meldung lesen. Weitere Informationen finden Sie unter [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Festlegen von Umgebungsvariablen

Wenn Sie nur das R-Feature integrieren möchten, sollten Sie die Umgebungsvariable **MKL_CBWR** über die Intel Math Kernel Library-Berechnungen auf [ensure consistent output](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) (Konsistente Ausgabe sicherstellen) festlegen.

1. Klicken Sie in der Systemsteuerung auf **System und Sicherheit** > **System** > **Erweiterte Systemeinstellungen** > **Umgebungsvariablen**.

2. Erstellen Sie eine neue Benutzer- oder Systemvariable. 

  + Legen Sie den Variablenname auf `MKL_CBWR` fest.
  + Legen Sie den Variablenwert auf `AUTO` fest.

Für diesen Schritt ist ein Neustart des Servers erforderlich. Wenn Sie im Begriff sind, die Skriptausführung zu aktivieren, können Sie den Neustart anhalten, bis die gesamte Konfiguration abgeschlossen ist.

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>Aktivieren der Skriptausführung

1. Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Sie können die entsprechende Version von folgender Seite herunterladen und installieren: [Herunterladen von SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)
    > 
    > Sie können auch [Azure Data Studio](../../azure-data-studio/what-is.md) verwenden, das administrative Aufgaben und Abfragen für SQL Server unterstützt.
  
2. Stellen Sie eine Verbindung mit der Instanz her, auf der Sie Machine Learning Services installiert haben. Klicken Sie auf **Neue Abfrage**, um ein Abfragefenster zu öffnen, und führen Sie den folgenden Befehl aus:

   ```sql
   sp_configure
   ```
    Der Wert für die Eigenschaft `external scripts enabled` sollte an diesem Punkt **0** betragen. Dies liegt daran, dass die Funktion standardmäßig deaktiviert ist. Die Funktion muss explizit von einem Administrator aktiviert werden, bevor Sie R- oder Python-Skripts ausführen können.
     
3. Führen Sie die folgende Anweisung aus, um die externe Funktion für die Skripterstellung zu aktivieren:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Starten Sie den Dienst neu.

Starten Sie nach Abschluss der Installation die Datenbank-Engine neu, bevor Sie mit dem nächsten Schritt fortfahren, und aktivieren Sie die Skriptausführung.

Durch den Neustart des Diensts wird auch der zugehörige [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienst automatisch neu gestartet.

Sie können den Dienst neu starten, indem Sie mit der rechten Maustaste auf den Befehl **Neu starten** für die Instanz in SSMS klicken, den Bereich **Dienste** in der Systemsteuerung oder den [SQL Server-Konfigurations-Manager](../../relational-databases/sql-server-configuration-manager.md) verwenden.

## <a name="verify-installation"></a>Überprüfen der Installation

Überprüfen Sie den Installationsstatus der Instanz über [benutzerdefinierte Berichte](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Gehen Sie folgendermaßen vor, um zu überprüfen, ob alle zum Starten eines externen Skripts verwendeten Komponenten ausgeführt werden.

1. Öffnen Sie in SQL Server Management Studio ein neues Abfragefenster, und führen Sie den folgenden Befehl aus:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    Der Wert **Run_value** sollte jetzt auf 1 festgelegt werden.

2. Öffnen Sie den Bereich **Dienste** oder den SQL Server-Konfigurations-Manager, und überprüfen Sie, ob der **SQL Server-Launchpad-Dienst** ausgeführt wird. Sie sollten über einen Dienst für jede Datenbank-Engine-Instanz verfügen, auf der R oder Python installiert ist. Weitere Informationen zu dem Dienst finden Sie unter [Erweiterbarkeitsframework](../concepts/extensibility-framework.md).

7. Wenn das Launchpad ausgeführt wird, sollten Sie einfache R-Skripts ausführen können, um zu überprüfen, ob externe Skriptruntimes mit SQL Server kommunizieren können. 

    Öffnen Sie ein neues **Abfragefenster** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und führen Sie ein Skript wie das folgende aus:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    Die Ausführung des Skripts kann einige Zeit in Anspruch nehmen, wenn die externe Skriptruntime zum ersten Mal geladen wird. Die Ergebnisse sollten etwa wie folgt aussehen:

    | Hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Anwenden von Updates

Es wird empfohlen, dass Sie das neueste kumulative Update sowohl auf die Datenbank-Engine als auch auf die Machine Learning-Komponenten anwenden.

Auf Geräten, die mit dem Internet verbunden sind, werden kumulative Updates in der Regel über Windows Update angewendet. Sie können jedoch auch die nachfolgenden Schritte für kontrollierte Updates verwenden. Wenn Sie das Update für die Datenbank-Engine anwenden, ruft das Setup die kumulativen Updates für alle R-Bibliotheken ab, die Sie auf derselben Instanz installiert haben. 

Auf getrennten Servern sind zusätzliche Schritte erforderlich. Weitere Informationen finden Sie unter [Installieren auf Computern ohne Internetzugriff > Kumulative Updates anwenden](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Beginnen Sie mit einer bereits installierten Baseline-Instanz: erstes Release von SQL Server 2016, SQL Server 2016 SP1 oder SQL Server 2016 SP2

2. Navigieren Sie zur kumulativen Updateliste: [SQL Server 2016-Updates](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Wählen Sie das neueste kumulative Update aus. Eine ausführbare Datei wird automatisch heruntergeladen und extrahiert.

4. Führen Sie das Setup aus. Akzeptieren Sie die Lizenzbedingungen, und überprüfen Sie auf der Seite für die Funktionsauswahl die Funktionen, für die kumulative Updates angewendet werden. Es sollte jedes für die aktuelle Instanz installierte Feature einschließlich R Services angezeigt werden. Das Setup lädt die CAB-Dateien herunter, die zum Aktualisieren aller Funktionen erforderlich sind.

5. Folgen Sie den weiteren Anweisungen des Assistenten, und akzeptieren Sie die Lizenzbedingungen für die R-Verteilung. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Zusätzliche Konfiguration

Wenn der Schritt zur externen Skriptüberprüfung erfolgreich war, können Sie Python-Befehle von SQL Server Management Studio, Visual Studio Code oder einem anderen Client ausführen, der T-SQL-Anweisungen an den Server senden kann.

Überprüfen Sie die zusätzlichen Konfigurationsschritte in diesem Abschnitt, wenn beim Ausführen des Befehls ein Fehler aufgetreten ist. Möglicherweise müssen Sie für den Dienst oder die Datenbank zusätzliche geeignete Konfigurationen vornehmen.

Auf Instanzebene kann eine zusätzliche Konfiguration Folgendes umfassen:

* [Firewallkonfiguration für SQL Server- Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Aktivieren zusätzlicher Netzwerkprotokolle](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Aktivieren von Remoteverbindungen](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Verwalten von Datenträgerkontingenten](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas), um das Ausführen externer Skripts zu vermeiden, die Speicherplatz verbrauchen

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

Für die Datenbank benötigen Sie möglicherweise die folgenden Konfigurationsupdates:

* [Benutzern die Berechtigung für SQL Server-Machine Learning Services erteilen](../../advanced-analytics/security/user-permission.md)
* [Hinzufügen der SQLRUserGroup als Datenbankbenutzer](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> Nicht alle aufgeführten Änderungen sind erforderlich. Es ist möglich, dass keine davon erforderlich ist. Die Anforderungen hängen vom Sicherheitsschema ab, in dem Sie SQL Server installiert haben, sowie von Ihren Erwartungen bezüglich des Herstellens einer Verbindung mit der Datenbank und dem Ausführen externer Skripts seitens der Benutzer. Hier finden Sie weitere Tipps zur Problembehandlung: [Häufig gestellte Fragen zu Upgrade und Installation](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Empfohlene Optimierungen

Da nun alles funktioniert, möchten Sie möglicherweise auch den Server für die Unterstützung von Machine Learning optimieren oder vorab trainierte Modelle installieren.

### <a name="add-more-worker-accounts"></a>Hinzufügen weiterer Geschäftskonten

Wenn Sie wissen, dass Sie R intensiv verwenden oder dass viele Benutzer gleichzeitig Skripts ausführen werden, können Sie die Anzahl der Workerkonten erhöhen, die dem Launchpad-Dienst zugewiesen sind. Weitere Informationen finden Sie unter [Ändern des Benutzerkontenpools für SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Optimieren des Servers für die Ausführung externer Skripts

Die Standardeinstellungen für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup dienen zur Optimierung des Lastenausgleichs des Servers für eine Vielzahl von Diensten, die von der Datenbank-Engine unterstützt werden, einschließlich ETL-Prozesse (Extrahieren, Transformieren und Laden), Reporting, Überwachung und Anwendungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Daten verwenden. Daher können in den Standardeinstellungen insbesondere für speicherintensive Vorgänge Ressourcen für Machine Learning-Vorgänge eingeschränkt oder gedrosselt sein.

Es wird empfohlen, dass Sie zum Konfigurieren eines externen Ressourcenpools den SQL Server-Resource Governor verwenden, um sicherzustellen, dass Machine Learning-Aufgaben über die entsprechende Priorität und die nötigen Ressourcen verfügen. Eventuell ist es auch sinnvoll, die Größe des Speichers zu ändern, der der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank-Engine zugewiesen ist, oder die Anzahl der Konten zu erhöhen, die unter dem [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienst ausgeführt werden.

- Informationen zum Konfigurieren eines Ressourcenpools zum Verwalten externer Ressourcen finden Sie unter [Erstellen eines externen Ressourcenpools](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Informationen zum Ändern des für die Datenbank reservierten Arbeitsspeichers finden Sie unter [Konfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Weitere Informationen zur Anzahl der R-Konten, die von [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] gestartet werden können, finden Sie unter [Ändern des Benutzerkontenpools für Machine Learning](../administration/modify-user-account-pool.md).

Wenn Sie die Standard Edition verwenden und nicht über Resource Governor verfügen, können Sie DMVs (dynamische Verwaltungssichten) und erweiterte Ereignisse sowie die Windows-Ereignisüberwachung verwenden, um Serverressourcen zu verwalten, die von R verwendet werden. Weitere Informationen finden Sie unter [Überwachen und Verwalten von R Services](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Installieren zusätzlicher R-Pakete

Die R-Lösungen, die Sie für SQL Server erstellen, können grundlegende Funktionen, Funktionen aus den proprietären mit SQL Server installierten Paketen sowie Funktionen aus Drittanbieterpaketen aufrufen, die mit der von SQL Server installierten Open-Source-Version von R kompatibel sind.

Pakete, die Sie von SQL Server verwenden möchten, müssen in der Standardbibliothek installiert sein, die von der Instanz verwendet wird. Wenn Sie eine separate Installation von R auf dem Computer haben oder Pakete in Benutzerbibliotheken installiert sind, werden Sie diese Pakete über T-SQL nicht verwenden können.

Der Installations- und Verwaltungsprozess für R-Pakete unterscheidet sich in SQL Server 2016 und SQL Server 2017. In SQL Server 2016 muss ein Datenbankadministrator die R-Pakete installieren, die die Benutzer benötigen. In SQL Server 2017 können Sie Benutzergruppen für die Freigabe von Paketen auf Datenbankebene einrichten oder Datenbankrollen so konfigurieren, dass Benutzer ihre eigenen Pakete installieren können. Weitere Informationen finden Sie unter [Installieren neuer R-Pakete](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Nächste Schritte

R-Entwickler können mit einigen einfachen Beispielen loslegen und die Grundlagen der Funktionen von R unter SQL Server kennenlernen. Informationen zu den nächsten Schritten finden Sie unter den folgenden Links:

+ [Tutorial: Ausführen von R in T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutorial: Datenbankinterne Analysen für R-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Praxisbeispiele für die Verwendung von Machine Learning finden Sie unter [Tutorials für Machine Learning](../tutorials/machine-learning-services-tutorials.md).