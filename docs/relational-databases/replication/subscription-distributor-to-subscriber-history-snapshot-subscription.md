---
title: Verlauf Verteiler zu Abonnent (Momentaufnahme)
description: In diesem Artikel wird die Registerkarte „Verlauf Verteiler zu Abonnent“ des Replikationsmonitors für eine Momentaufnahmeveröffentlichung in SQL Server Management Studio (SSMS) erläutert.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.pubtodist.snapshot.f1
ms.assetid: d3575964-f287-4bcf-8d2e-f81a33141b25
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 8cd2a4ad7ce605139133b29fed6b2acee3b63c5c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287087"
---
# <a name="subscription-distributor-to-subscriber-history-snapshot-subscription"></a>Abonnement, Verlauf Verteiler zu Abonnent (Momentaufnahmeabonnement)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Die Registerkarte **Verlauf Verteiler zu Abonnent** zeigt detaillierte Informationen zum Verteilungs-Agent an, u. a. Status, Verlauf, Informationsmeldungen und alle Fehlermeldungen.  
  
## <a name="options"></a>Tastatur  
 Wählen Sie im Menü **Sicht** aus, welche Sitzungen des Verteilungs-Agents angezeigt werden, und wählen Sie dann eine bestimmte Sitzung aus dem Raster mit der Bezeichnung **Sitzungen des Verteilungs-Agents**aus. Detaillierte Informationen zu dieser Sitzung werden im Raster mit der Bezeichnung **Aktionen in der ausgewählten Sitzung**angezeigt. Wenn die ausgewählte Sitzung mit einem Fehler beendet wurde, wird auch der Textbereich mit der Bezeichnung **Fehlerdetails oder Meldung der ausgewählten Sitzung** angezeigt.  
  
 **Ansicht**  
 Wählen Sie aus, welche Sitzungen des Verteilungs-Agents angezeigt werden.  
  
 **Status**  
 Der Status des Verteilungs-Agents. In der folgenden Liste sind die möglichen Statuswerte aufgeführt:  
  
-   Fehler  
  
-   Abgeschlossen  
  
-   Wird wiederholt  
  
-   Wird ausgeführt  
  
 **Startzeit**  
 Startzeit der Sitzung.  
  
 **Beendigungszeit**  
 Beendigungszeit der Sitzung. Wenn der Agent noch nicht beendet wurde, ist dieses Feld leer.  
  
 **Duration**  
 Zeitspanne, für die der Verteilungs-Agent in dieser Sitzung ausgeführt wurde. Die Zeit stellt die bisher abgelaufene Zeit dar, wenn der Agent immer noch ausgeführt wird, und die Gesamtzeit, wenn die Agentsitzung beendet ist.  
  
 **Fehlermeldung**  
 Wenn eine Sitzung mit einem Fehler beendet wurde, wird in diesem Feld die Fehlermeldung angezeigt, die vom Verteilungs-Agent protokolliert wurde. Wurde die Sitzung nicht mit einem Fehler beendet, ist dieses Feld leer.  
  
 **Aktionsmeldung**  
 Alle Informationsmeldungen und Fehlermeldungen, die der Verteilungs-Agent während der ausgewählten Sitzung protokolliert hat.  
  
 **Aktionszeit**  
 Zeit, zu der die unter **Aktionsmeldung** beschriebene Aktion ausgeführt wurde.  
  
 **Fehlerdetails oder Meldung der ausgewählten Sitzung**  
 Wird nur angezeigt, wenn in der ausgewählten Sitzung in der **Status** -Spalte der Wert **Fehler** angezeigt wird. Dieser Textbereich zeigt detaillierte Fehlerinformationen sowie den Befehl an, der zum Zeitpunkt des Fehlers auszuführen versucht wurde. Er enthält außerdem Links zu weiteren Informationen, die sich auf den Fehler beziehen.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [View information and perform tasks using Replication Monitor (Anzeigen von Informationen und Ausführen von Aufgaben mit dem Replikationsmonitor)](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Übersicht über Replikations-Agents](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
