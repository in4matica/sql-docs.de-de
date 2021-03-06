---
title: Oracle CDC-Instanz | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ed71e8c4-e013-4bf2-8b6c-1e833ff2a41d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0152594c213196860e80ff5d5267356977404b7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771190"
---
# <a name="the-oracle-cdc-instance"></a>Oracle CDC-Instanz
  Die Oracle CDC-Instanz ist ein vom Oracle CDC Service erstellter Prozess zur Verarbeitung der Änderungen, die aus einer einzelnen Oracle-Quelldatenbank aufgezeichnet wurden. Die Oracle CDC-Instanz ruft ihre Konfiguration aus der Tabelle **cdc.xdbcdc_config** ab und verwaltet ihren Status in der Tabelle **cdc.xdbcdc_state** . Diese Tabellen sind Teil der CDC-Datenbank, über die die Oracle CDC-Instanz definiert wird. Weitere Informationen zur Datenbank xdbcdc und zu Tabellen finden Sie unter [The CDC Databases](the-oracle-cdc-service.md).  
  
 Im Folgenden werden die Tasks beschrieben, die von der Oracle CDC-Instanz ausgeführt werden:  
  
-   **Durchführen der Startüberprüfung für den Dienst:** Nach dem Starten lädt die CDC-Instanz ihre Konfiguration aus der Tabelle **xdbcdc_config** und führt eine Reihe von Statusüberprüfungen aus. So wird sichergestellt, dass der permanente Status der CDC-Instanz einheitlich ist und dass mit der Verarbeitung der Änderungen begonnen werden kann.  
  
-   **Vorbereiten auf die Änderungsaufzeichnung**: Wenn die Überprüfung erfolgreich ist, scannt die Oracle CDC-Instanz alle momentan definierten Aufzeichnungsinstanzen und bereitet die Oracle LogMiner-Abfragen und andere Unterstützungsstrukturen vor, die für die Änderungsaufzeichnung erforderlich sind. Außerdem lädt die Oracle-Instanz den internen Aufzeichnungsstatus neu, der bei der letzten Ausführung der Oracle CDC-Instanz gespeichert wurde.  
  
-   **Aufzeichnen von Änderungen aus Oracle**: Die Oracle CDC-Instanz fasst Änderungen aus Oracle mithilfe der Oracle LogMiner-Funktion in einem Pool zusammen, sortiert diese nach Transaktionscommit und ändert dann die Uhrzeit in einer Transaktion und schreibt sie in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Änderungstabellen in der CDC-Datenbank.  
  
-   **Herunterfahren des Diensts**: Der Lebenszyklus der Oracle CDC-Instanz wird vom Oracle CDC Service verwaltet. Wenn für die Oracle CDC-Instanz das Herunterfahren angefordert wird, werden die folgenden Tasks ausgeführt:  
  
    -   Das Lesen von Daten aus dem Oracle-Transaktionsprotokoll wird beendet.  
  
    -   Das Schreiben abgeschlossener Oracle-Transaktionen in die CDC-Datenbank wird beendet.  
  
    -   Es wird (falls erforderlich) bis zu 30 Sekunden gewartet, bis die aktuelle Transaktion in die CDC-Datenbank geschrieben wurde. Wenn mehr als 30 Sekunden vergehen, wird der Schreibvorgang abgebrochen und für die Transaktion ein Rollback ausgeführt (um den Vorgang nach dem Neustart der CDC-Instanz wiederholen zu können).  
  
    -   In einem separaten Thread werden so viele im Arbeitsspeicher zwischengespeicherte Datensätze wie möglich für bis zu 30 Sekunden in die Tabelle mit den bereitgestellten Transaktionen geschrieben (von der ältesten bis zur neuesten Transaktion). Anschließend wird die Tabelle **xdbcdc_state** aktualisiert und für alle Änderungen ein Commit ausgeführt.  
  
-   **Durchführen von Konfigurationsänderungen:** Die Oracle CDC-Instanz wird entweder vom CDC Service oder bei Erkennung einer neuen Version in der Tabelle **cdc.xdbcdc_config** über Konfigurationsänderungen benachrichtigt. Für die meisten Änderungen ist kein Neustart der Oracle CDC-Instanz erforderlich (z. B. beim Hinzufügen oder Entfernen von Aufzeichnungsinstanzen). Bei einigen anderen Änderungen, z. B. beim Ändern der Oracle-Verbindungszeichenfolge oder der Anmeldeinformationen, muss jedoch ein Neustart der CDC-Instanz ausgeführt werden.  
  
-   **Durchführen der Wiederherstellung:** Beim Starten einer Oracle CDC-Instanz wird ihr interner Status aus den Tabellen **xdbcdc_state** und **xdbcdc_staged_transactions** wiederhergestellt. Nachdem der Status wiederhergestellt wurde, fährt die CDC-Instanz normal fort.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Fehlerbehandlung](error-handling.md)  
  
  
