---
title: MSSQLSERVER_21893 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fcf093c5560313487be60d854c880de526f7a525
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "68056661"
---
# <a name="mssqlserver_21893"></a>MSSQLSERVER_21893
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21893|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQLErrorNum21893|  
|Meldungstext|Die Abonnenten (%s) des ursprünglichen Verlegers '%s' werden bei dem umgeleitetem Verleger '%s' nicht als Remoteserver angezeigt. Führen Sie **sp_addlinkedserver** auf dem umgeleiteten Verleger aus, um diese Abonnenten als Remoteserver hinzuzufügen.|  
  
## <a name="explanation"></a>Erklärung  
**sp_validate_redirected_publisher** verwendet die Abonnement-Metadatentabellen von der Verlegerdatenbank beim Remoteserver, um seine zugeordneten Abonnenten zu identifizieren, und überprüft, ob für die Abonnenten zugehörige Einträge in „master.dbo.sysservers“ vorhanden sind. Dieser Fehler wird zurückgegeben, wenn einer der identifizierten Abonnenten nicht vorhanden ist.  
  
Dies wird jedoch nicht als schwerwiegender Fehler angesehen. Agents, in denen dieser Fehler auftritt, protokollieren den Fehler als Information, werden aber nicht beendet, da sich das Nichtvorhandensein entsprechender Abonnenteneinträge beim neuen Verleger nur beschränkt auf die Replikation auswirkt. Ohne einen entsprechenden Eintrag für einen Abonnenten in „sysservers“ schlagen einige Abonnementverwaltungsaktivitäten möglicherweise fehl, wenn sie über [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ausgeführt werden. Diese gleichen Aktivitäten können jedoch erfolgreich ausgeführt werden, indem die gespeicherten Verwaltungsprozeduren explizit ausgeführt werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie **sp_addlinkedserver** für jeden identifizierten Abonnenten auf dem umgeleiteten Verleger aus, um diese Abonnenten als Remoteserver hinzuzufügen. Führen Sie anschließend **sp_serveroption** aus, um das Abonnentenbit für den Server festzulegen.  
  
