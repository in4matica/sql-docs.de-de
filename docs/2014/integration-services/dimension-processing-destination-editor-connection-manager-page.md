---
title: Ziel-Editor für Dimensions Verarbeitung (Seite Verbindungs-Manager) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.connection.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2259b19cec6674cdb1f5f4a0064334f78aa5300f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059438"
---
# <a name="dimension-processing-destination-editor-connection-manager-page"></a>Ziel-Editor für Dimensionsverarbeitung (Seite Verbindungs-Manager)
  Geben Sie im Dialogfeld **Ziel-Editor für Dimensionsverarbeitung** auf der Seite **Verbindungs-Manager** eine Verbindung mit einem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Projekt oder einer Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]an.  
  
 Weitere Informationen zum Ziel für Dimensionsverarbeitung finden Sie unter [Dimension Processing Destination](data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Tastatur  
 **Connection manager**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus der Liste aus, oder klicken Sie auf **Neu** , um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Analysis Services-Verbindungs-Manager hinzufügen** eine neue Verbindung.  
  
 **Liste der verfügbaren Dimensionen**  
 Wählen Sie die zu verarbeitende Dimension aus.  
  
 **Verarbeitungsmethode**  
 Wählen Sie die Verarbeitungsmethode aus, die auf die in der Liste ausgewählte Dimension angewendet werden soll. Der Standardwert für diese Option ist **Vollständig**.  
  
|value|BESCHREIBUNG|  
|-----------|-----------------|  
|**Add (inkrementell)**|Führt eine inkrementelle Verarbeitung der Dimension aus.|  
|**Vollständig**|Führt eine vollständige Verarbeitung der Dimension aus.|  
|**Alisierungs**|Führt eine Verarbeitung der Updates für die Dimension aus.|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Fehler- und Meldungsreferenz von Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Ziel-Editor für Dimensions Verarbeitung &#40;Seite Zuordnungen&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)   
 [Ziel-Editor für Dimensions Verarbeitung &#40;Seite "Erweitert"&#41;](../../2014/integration-services/dimension-processing-destination-editor-advanced-page.md)  
  
  
