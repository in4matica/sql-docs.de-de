---
title: Verwaltung und Wartung von Failoverclusterinstanzen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- user accounts [SQL Server], failover clustering
- clusters [SQL Server], maintaining
- nodes [Faillover Clustering]
- failover clustering [SQL Server], maintaining
- adding nodes
- virtual servers [SQL Server], removing nodes
- clustered instance of SQL Server
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- service accounts [SQL Server]
- removing nodes
- virtual servers [SQL Server], adding nodes
ms.assetid: 2d5c63e9-8061-45c3-94db-8dd3100b8a91
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 402e9e0d787d6f60e069625e908faee4fbecaeca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63049439"
---
# <a name="failover-cluster-instance-administration-and-maintenance"></a>Verwaltung und Wartung von Failoverclusterinstanzen
  Wartungsaufgaben wie das Hinzufügen oder Entfernen von Knoten aus einer vorhandenen AlwaysOn-Failoverclusterinstanz (FCI) werden mithilfe des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Setupprogramms ausgeführt. Andere Verwaltungsaufgaben wie das Ändern der IP-Adressressource oder das Wiederherstellen nach bestimmten FCI-Szenarien werden mit dem Failovercluster-Manager-Snap-In ausgeführt, welches das Verwaltungs-Snap-In für den WSFC (Windows Server Failover Clustering)-Dienst darstellt.  
  
## <a name="maintaining-a-failover-cluster-instance"></a>Warten einer Failoverclusterinstanz  
 Nachdem Sie eine FCI installiert haben, können Sie sie mithilfe des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setupprogramms ändern oder reparieren. Beispielsweise können Sie einer FCI zusätzliche Knoten hinzufügen, eine FCI als eigenständige Instanz ausführen oder einen Knoten aus einer FCI-Konfiguration entfernen.  
  
### <a name="adding-a-node-to-an-existing-failover-cluster-instance"></a>Hinzufügen eines Knotens zu einer vorhandenen Failoverclusterinstanz  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup bietet Ihnen die Möglichkeit, eine vorhandene FCI zu warten. Bei Auswahl dieser Option können Sie der FCI weitere Knoten hinzufügen, indem Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup auf dem Computer ausführen, den Sie der FCI hinzufügen möchten. Weitere Informationen finden Sie unter [Erstellen eines neuen SQL Server-Failoverclusters &#40;Setup&#41;](../install/create-a-new-sql-server-failover-cluster-setup.md) und [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
### <a name="removing-a-node-from-an-existing-failover-cluster-instance"></a>Entfernen eines Knotens aus einer vorhandenen Failoverclusterinstanz  
 Sie können einen Knoten aus einer FCI entfernen, indem Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup auf dem Computer ausführen, den Sie aus der FCI entfernen möchten. Jeder Knoten in einer FCI wird als Peer ohne Abhängigkeiten von anderen Knoten in der FCI angesehen und kann beliebig entfernt werden. Ein beschädigter Knoten muss nicht verfügbar sein, um entfernt zu werden. Beim Entfernen werden keine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Binärdateien von dem nicht verfügbaren Knoten deinstalliert. Ein entfernter Knoten kann einer FCI jederzeit wieder hinzugefügt werden. Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
### <a name="changing-service-accounts"></a>Ändern von Dienstkonten  
 Die Kennwörter der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonten sollten nicht geändert werden, während ein FCI-Knoten heruntergefahren wurde oder offline ist. Wenn dies doch erforderlich ist, müssen Sie die Kennwörter mithilfe des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfigurations-Managers wieder zurücksetzen, sobald alle Knoten wieder online sind.  
  
 Wenn es sich bei dem Dienstkonto für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht um das Konto eines Administrators im Cluster handelt, können die administrativen Freigaben auf den Knoten des Clusters nicht gelöscht werden. Die administrativen Freigaben müssen in einem Cluster verfügbar sein, damit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] funktionsfähig ist.  
  
> [!IMPORTANT]  
>  Verwenden Sie nicht dasselbe Konto für das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonto und das WSFC-Dienstkonto. Wenn das Kennwort für das WSFC-Dienstkonto geändert wird, verursacht die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installation einen Fehler.  
  
 Unter [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]werden Dienst-SIDs für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonten verwendet. Weitere Informationen finden Sie unter [Konfigurieren von Windows-Dienst Konten und-Berechtigungen](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="administering-a-failover-cluster-instance"></a>Verwalten einer Failoverclusterinstanz  
  
|Taskbeschreibung|Themenlink|  
|----------------------|----------------|  
|Beschreibt, wie Abhängigkeiten zu einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource hinzugefügt werden.|[Hinzufügen von Abhängigkeiten zu einer Ressource von SQL Server](add-dependencies-to-a-sql-server-resource.md)|  
|Kerberos ist ein Netzwerkauthentifizierungsprotokoll, das entwickelt wurde, um strenge Authentifizierung für Client/Server-Anwendungen bereitzustellen. Kerberos bietet die Grundlagen für Interoperabilität und verbessert gleichzeitig die Sicherheit der unternehmensweiten Netzwerkauthentifizierung. Sie können die Kerberos-Authentifizierung mit eigenständigen Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder mit AlwaysOn-FCIs verwenden.|[Registrieren Sie einen Dienst Prinzipal Namen für Kerberos-Verbindungen](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).|  
|Stellt Links zu Inhalten mit Beschreibungen dazu bereit, wie die Kerberos-Authentifizierung aktiviert wird.||  
|Beschreibt das Verfahren zum Wiederherstellen nach einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster-Fehler.|[Wiederherstellen nach einem Fehler der Failoverclusterinstanz](recover-from-failover-cluster-instance-failure.md)|  
|Beschreibt das Verfahren zum Ändern der IP-Adressressource für eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz.|[Ändern der IP-Adresse einer Failoverclusterinstanz](change-the-ip-address-of-a-failover-cluster-instance.md)|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Konfigurieren der healthchecktimeout-Eigenschaften Einstellungen](configure-healthchecktimeout-property-settings.md)   
 [Konfigurieren von failureconditionlevel-Eigenschaften Einstellungen](configure-failureconditionlevel-property-settings.md)   
 [Anzeigen und Lesen des Failoverclusterinstanz-Diagnoseprotokolls](view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  
