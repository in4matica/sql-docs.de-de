---
title: Sicherheit für den Protokolllese-Agent (Peer-zu-Peer-Replikation) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.LRA.f1
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6bcf7d78fd550404f81f9cc303414303ad82504
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63000357"
---
# <a name="log-reader-agent-security-peer-to-peer-replication"></a>Sicherheit für den Protokolllese-Agent (Peer-zu-Peer-Replikation)
  Auf der **Protokolllese-Agent Seite Sicherheit** können Sie die Konten angeben, unter denen die Protokolllese-Agent auf jedem Peer ausgeführt wird und Verbindungen herstellt. Weitere Informationen zu den für Agents erforderlichen Berechtigungen und zu bewährten Methoden der Replikationssicherheit finden Sie unter [Sicherheitsmodell des Replikations-Agents](security/replication-agent-security-model.md) und [Bewährte Methoden für die Replikationssicherheit](security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Es gibt einen Protokolllese-Agent für jede Datenbank, die mithilfe der Transaktionsreplikation veröffentlicht wird. Wenn der Protokolllese-Agent für eine Datenbank bereits konfiguriert wurde (entweder für eine Veröffentlichung bei einer vorherigen Ausführung dieses Assistenten oder für eine andere Transaktionsveröffentlichung in derselben Datenbank), können Sie die bestehenden Anmeldeinformationen mit diesem Assistenten nicht ändern. Von Ihnen neu angegebene Anmeldeinformationen werden ignoriert. Sie können die Anmeldeinformationen im Dialogfeld **Veröffentlichungseigenschaften** ändern. Weitere Informationen finden Sie unter [anzeigen und Ändern von Replikations Sicherheitseinstellungen](security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>Tastatur  
 Klicken Sie in der Zeile für jeden Peer auf die Eigenschaftenschaltfläche (**die Schaltfläche mit den drei Punkten**), um auf das Dialogfeld **Sicherheit für den Protokolllese-Agent** zuzugreifen. Klicken Sie im geöffneten Dialogfeld **Sicherheit für den Protokolllese-Agent** auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die von den Agents verwendeten Konten erforderlich sind.  
  
 Wenn Sie die Einstellungen im Dialogfeld eingegeben haben, werden im Raster die Verbindungsinformationen zu dem Abonnenten angezeigt.  
  
 **Agents für Verleger**  
 Der Name jeder Peerserverinstanz.  
  
 **Peer Datenbank**  
 Die Datenbank, die auf jedem Peer als Veröffentlichungs- und Abonnementdatenbank dient.  
  
 **Verbindung mit Verteiler**  
 Der Kontext, unter dem die Verbindung mit dem Verteiler hergestellt wird. Die lokale Verbindung mit dem Verteiler wird immer mithilfe des Kontexts des [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Windows-Kontos hergestellt, unter dem der Agent ausgeführt wird. In diesem Feld wird daher immer **Identität von „\<Domain>\\<Login\>“ annehmen** oder **Identität von „\<Computer>\\<Login\>“ annehmen** angezeigt.  
  
 **Verbindung mit Verleger**  
 Der Kontext, unter dem die Verbindung mit dem Verleger hergestellt wird. Die Verbindung mit dem Verleger kann mithilfe einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung oder mithilfe des Kontexts des Windows-Kontos hergestellt werden, unter dem der Agent ausgeführt wird. Das Feld zeigt eine der folgenden Angaben: **Use login '\<Login>'**, **Impersonate '\<Domain>\\<Login\>'** oder **Impersonate '\<Computer>\\<Login\>'**. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, alle Verbindungen unter dem Kontext des Windows-Kontos herzustellen.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Verwalten einer Peer-zu-Peer-Topologie &#40;Replikationsprogrammierung mit Transact-SQL&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)  
  
  
