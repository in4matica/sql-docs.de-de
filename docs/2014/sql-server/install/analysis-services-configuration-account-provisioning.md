---
title: Analysis Services Konfiguration-Konto Bereitstellung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services configuration
- account provisioning
ms.assetid: 169b1af2-6fe2-467f-8ca4-919f24c620ce
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 033c1ec1b0ad478e525f3ea9e8f172c5e5e31eef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096797"
---
# <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services-Konfiguration - Kontobereitstellung
  Verwenden Sie diese Seite zum Einrichten des Servermodus und zum Zuweisen von administrativen Berechtigungen an Benutzer oder Dienste, die uneingeschränkten Zugriff auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] benötigen. Während des Setups wird die lokale Windows-Gruppe „BUILTIN\Administrators“ der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Serveradministratorrolle der Instanz, die Sie installieren, nicht automatisch hinzugefügt. Wenn Sie der Serveradministratorrolle die lokale Gruppe "Administratoren" hinzufügen möchten, müssen Sie diese Gruppe explizit angeben.  
  
 Bei der Installation von [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sollten Sie Administratoren von SharePoint-Farmen oder -Diensten, die für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Serverbereitstellung in einer [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]-Farm zuständig sind, Administratorrechte gewähren. Weitere Informationen zu den [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] Anforderungen an die Installation und die Dienst Konten finden Sie unter [Installieren von SQL Server BI-Funktionen mit SharePoint &#40;Power Pivot und Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md).  
  
## <a name="options"></a>Tastatur  
 **Server Modus** -der Server Modus gibt den Typ der Analysis Services Datenbanken an, die auf dem Server bereitgestellt werden können. Servermodi werden während des Setups bestimmt und können später nicht mehr geändert werden. Die einzelnen Modi schließen einander aus. Das bedeutet, dass Sie zwei Instanzen von Analysis Services benötigen, die jeweils für einen anderen Modus konfiguriert sind, um beide klassische Lösungen - das OLAP- und das tabellarische Modell - zu unterstützen.  
  
 **Administratoren angeben** : Sie müssen mindestens einen Server Administrator für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angeben. Die Benutzer oder die Gruppen, die Sie angeben, werden Mitglieder der Serveradministratorrolle der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz, die Sie installieren. Diese müssen Windows-Domänenbenutzerkonten in der gleichen Domäne wie der Computer sein, auf dem Sie die Software installieren.  
  
> [!NOTE]  
>  Die Benutzerkontensteuerung (User Account Control, UAC) ist eine Windows-Sicherheitsfunktion, bei der ein Administrator administrative Aktionen oder Anwendungen einzeln genehmigen muss, bevor diese ausgeführt werden können. Da die Benutzerkontensteuerung in den Standardeinstellungen aktiviert ist, werden Sie aufgefordert, einzelne Vorgänge, für die erhöhte Berechtigungen erforderlich sind, zu genehmigen. Sie können die Benutzerkontensteuerung konfigurieren, um das Standardverhalten zu ändern, oder sie für bestimmte Programme anpassen. Weitere Informationen über die Benutzerkontensteuerung und deren Konfiguration finden Sie unter [Schritt-für-Schritt-Anleitung zur Benutzerkontensteuerung](https://go.microsoft.com/fwlink/?linkid=196350) und [Benutzerkontensteuerung (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351).  
  
## <a name="see-also"></a>Weitere Informationen  
 [Dienst Konten &#40;Analysis Services konfigurieren&#41;](../../../2014/analysis-services/instances/configure-service-accounts-analysis-services.md)   
 [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
