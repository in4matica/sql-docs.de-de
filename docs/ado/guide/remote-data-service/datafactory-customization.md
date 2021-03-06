---
title: DataFactory-Anpassung | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bdc406778bea0d6355e747998d2517b841fc17b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922770"
---
# <a name="datafactory-customization"></a>DataFactory-Anpassung
Remote Data Service (RDS) bietet eine Möglichkeit, auf einfache Weise Datenzugriff in einem Client/Server-System mit drei Ebenen auszuführen. Ein Client Daten Steuerelement gibt Verbindungs-und Befehls Zeichenfolgen-Parameter an, um eine Abfrage für eine Remote Datenquelle oder Verbindungs [Zeichenfolgen-und Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt Parameter zum Ausführen eines Updates auszuführen.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012 sind RDS-Server Komponenten nicht mehr im Windows-Betriebssystem enthalten (weitere Details finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) ). RDS-Client Komponenten werden in einer zukünftigen Version von Windows entfernt. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden, sollten zu [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)migriert werden.  
  
 Die Parameter werden an ein Serverprogramm weitergeleitet, das den Datenzugriffs Vorgang für die Remote Datenquelle ausführt. RDS bietet ein Standardmäßiges Serverprogramm, das als [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) -Objekt bezeichnet wird. Das **RDSServer. DataFactory** -Objekt gibt ein beliebiges **Recordset** -Objekt zurück, das von einer Abfrage an den Client erzeugt wurde.  
  
 **RDSServer. DataFactory** ist jedoch auf die Durchführung von Abfragen und Updates beschränkt. Es kann keine Validierung oder Verarbeitung der Verbindungs-oder Befehls Zeichenfolgen ausführen.  
  
 Mit ADO können Sie angeben, dass das **DataFactory** in Verbindung mit einem anderen Typ von Serverprogramm funktioniert, das als " *Handler*" bezeichnet wird. Der Handler kann die Client Verbindung und Befehls Zeichenfolgen ändern, bevor Sie für den Zugriff auf die Datenquelle verwendet werden. Außerdem kann der Handler Zugriffsrechte erzwingen, die die Fähigkeit des Clients steuern, Daten in der Datenquelle zu lesen und zu schreiben.  
  
 Die Parameter, die der Handler zum Ändern von Client Parametern und Zugriffsrechten verwendet, werden in Abschnitten einer Anpassungs Datei angegeben.  
  
 Die folgenden Themen enthalten weitere Informationen zum Anpassen des **DataFactory** -Objekts.  
  
-   [Grundlegendes zur Anpassungsdatei](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Connect-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [SQL-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [UserList-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Logs-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Erforderliche Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Schreiben Ihres eigenen benutzerdefinierten Handlers](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


