---
title: Bestimmen eines Ausfallsicherheitsoperators | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54ec71df8efab1f60bfb7a5b9af448705e349d28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211422"
---
# <a name="designate-a-fail-safe-operator"></a>Bestimmen eines Ausfallsicherheitsoperators
  Ein Ausfallsicherheitsoperator ist ein Benutzer, der die Warnungen empfängt, wenn der vorgesehene Operator nicht erreichbar ist. In diesem Thema wird beschrieben, wie Sie einen Ausfall Sicherheits Operator zum [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Empfang von-Agent [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Warn [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Benachrichtigungen in mithilfe von festlegen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So bestimmen Sie einen Ausfall Sicherheits Operator mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Pager-und **net send** -Optionen werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einer zukünftigen Version von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aus dem-Agent entfernt. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktionen zurzeit verwenden.  
  
-   Beachten Sie, dass E-Mail- und Pagerbenachrichtigungen an Operatoren nur versendet werden können, wenn der SQL Server-Agent für die Verwendung von Datenbank-E-Mail konfiguriert ist. Weitere Informationen finden Sie unter [Zuweisen von Warnungen zu einem Operator](assign-alerts-to-an-operator.md).  
  
-   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Aufträge problemlos mithilfe einer grafischen Oberfläche verwaltet werden. Dies ist die empfohlene Vorgehensweise für die Erstellung und Verwaltung der Auftragsinfrastruktur.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können Ausfallsicherheitsoperatoren bestimmen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-designate-a-fail-safe-operator"></a>So bestimmen Sie einen Ausfallsicherheitsoperator  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, der den SQL Server-Agent-Operator enthält, den Sie als ausfallsicher bestimmen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste **SQL Server-Agent** und wählen Sie **Eigenschaften**.  

3.  Wählen Sie im Dialogfeld **SQL Server-Agent Eigenschaften**_server_name_ unter **Seite auswählen**die Option Warnungs **System**aus.  
 
4.  Aktivieren Sie unter **Ausfallsicherheitsoperator**die Option **Ausfallsicherheitsoperator aktivieren**.  
  
5.  Wählen Sie in der Liste **Operator** den Operator aus, den Sie als ausfallsicher bestimmen möchten.  
  
6.  Aktivieren Sie entweder eines oder alle der folgenden Kontrollkästchen – **E-Mail**, **Pager**oder **NET SEND**–, um zu bestimmen, wie der Operator benachrichtigt wird.  
  
7.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
  
