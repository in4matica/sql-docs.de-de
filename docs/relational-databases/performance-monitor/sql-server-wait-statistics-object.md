---
title: SQL Server, Wartestatistik-Objekt | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Wait Statistics object
- SQLServer:Wait Statistics
ms.assetid: cb7f917d-4291-4115-9b78-ee7692ebbb2d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: c690c2cd19acae2fb3a6bde8b2dcd6d72b3acf18
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "67947886"
---
# <a name="sql-server-wait-statistics-object"></a>SQL Server, Wartestatistik-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das **SQLServer:Wartestatistik** -Leistungsobjekt enthält Leistungsindikatoren mit Informationen zum Wartestatus.  
  
 In der folgenden Tabelle werden die im Wartestatistik-Objekt enthaltenen Leistungsindikatoren aufgelistet.  
  
|Leistungsindikatoren des SQLServer:Wartestatistik-Objekts|BESCHREIBUNG|  
|-----------------------------------------|-----------------|  
|**Sperrenwartevorgänge**|Statistik für Prozesse, die auf eine Sperre warten|  
|**Protokollpuffer-Wartevorgänge**|Statistik für Prozesse, die auf die Verfügbarkeit des Protokollpuffers warten|  
|**Wartevorgänge für Schreiben des Protokolls**|Statistik für Prozesse, die darauf warten, dass der Protokollpuffer geschrieben wird|  
|**Speicherzuweisungs-Wartevorgänge**|Statistik für Prozesse, die auf die Verfügbarkeit einer Speicherzuweisung warten|  
|**Netzwerk-E/A-Wartevorgänge**|Statistik für Wartevorgänge bezüglich Netzwerk-E/A|  
|**Nichtseiten-Latchwartevorgänge**|Statistik für Nichtseitenlatches|  
|**Seiten-E/A-Latchwartevorgänge**|Statistik für Seiten-E/A-Latches|  
|**Seitenlatch-Wartevorgänge**|Statistik für Seitenlatches, ohne E/A-Latches|  
|**Thread-sichere Speicherobjekt-Wartevorgänge**|Statistik für Prozesse, die auf Thread-sichere Speicherzuordnungen warten|  
|**Transaktionsbesitzer-Wartevorgänge**|Statistik für Prozesse, die den Zugriff auf Transaktionen synchronisieren|  
|**Warten auf den Arbeitsthread**|Statistik für Prozesse, die auf die Verfügbarkeit des Arbeitsthreads warten|  
|**Wartevorgänge für Arbeitsbereichssynchronisierung**|Statistik für Prozesse, die den Zugriff auf den Arbeitsbereich synchronisieren|  
  
 Jeder Leistungsindikator in dem Objekt enthält die folgenden Instanzen:  
  
|Element|BESCHREIBUNG|  
|----------|-----------------|  
|**Durchschnittliche Wartezeit (ms)**|Durchschnittliche Zeit für den ausgewählten Wartetyp|  
|**Kumulierte Wartezeit (ms) pro Sekunde**|Aggregierte Wartezeit für den ausgewählten Typ pro Sekunde|  
|**Aktuell ausgeführte Wartevorgänge**|Anzahl der Prozesse, die zurzeit auf den folgenden Typ warten|  
|**Gestartete Wartevorgänge pro Sekunde**|Anzahl der pro Sekunde gestarteten Wartevorgänge des ausgewählten Wartetyps|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
