---
title: Distributed Replay Client Konfiguration | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ccf03e32-6bd9-43c0-b9b6-9fe0d9163339
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3eb00922b4f6e21dd4cfc8a46d8c0c27ed9a5be1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095478"
---
# <a name="distributed-replay-client-configuration"></a>Distributed Replay Client-Konfiguration
  Verwenden Sie die Seite für die **Distributed Replay Client-Konfiguration** des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installations-Assistenten, um die Benutzer anzugeben, denen Sie Administratorberechtigungen für den Distributed Replay Client-Dienst gewähren möchten.  
  
 Benutzer, die über Administratorberechtigungen verfügen, besitzen unbeschränkten Zugriff auf den Distributed Replay Client-Dienst.  
  
## <a name="options"></a>Tastatur  
 **Controllername**  
 Dies ist ein optionaler Parameter, und der Standardwert \<ist *leer*>.  
  
 Geben Sie den Namen des Controllers ein, mit dem der Clientcomputer für den Distributed Replay Client-Dienst kommuniziert. Beachten Sie Folgendes:  
  
-   Der Name muss ein vollqualifizierter Domänenname sein. Ein Host mit dem Namen "server1" kann in der Produkthierarchie von Microsoft z. B. den vollqualifizierten Domänennamen "server1.products.microsoft.com" haben.  
  
-   Wenn Sie bereits einen Controller eingerichtet haben, geben Sie den Namen des Controllers beim Konfigurieren jedes Clients ein.  
  
-   Wenn Sie noch keinen Controller eingerichtet haben, können Sie das Feld für den Controllernamen leer lassen. Sie müssen den Controllernamen jedoch in der **Clientkonfigurationsdatei** manuell eingeben.  
  
 **Arbeitsverzeichnis**  
 Geben Sie das Arbeitsverzeichnis für den Distributed Replay Client-Dienst an.  
  
 Das Standard Arbeitsverzeichnis ist \< *Laufwerk Buchstabe*>: \Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\dreplayclient\workingdir\\.  
  
 **Ergebnisverzeichnis**  
 Geben Sie das Ergebnisverzeichnis für den Distributed Replay Client-Dienst an.  
  
 Das Standard Ergebnis Verzeichnis ist \< *Laufwerk Buchstabe*>: \Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\dreplayclient\resultdir\\.  
  
  
