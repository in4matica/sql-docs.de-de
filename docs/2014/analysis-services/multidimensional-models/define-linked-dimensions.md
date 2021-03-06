---
title: Verknüpfte Dimensionen definieren | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: d5ad5eae-5dde-46a6-91c3-c8766d016dec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca4b3c0b2f2a6c63e62a44499d6e33e651ca9bae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075574"
---
# <a name="define-linked-dimensions"></a>Definieren von verknüpften Dimensionen
  Eine verknüpfte Dimension basiert auf einer Dimension, die in einer anderen Analysis Services-Datenbank mit derselben Version und demselben Kompatibilitätsgrad erstellt und gespeichert wurde. Mithilfe einer verknüpften Dimension können Sie eine Dimension in einer Datenbank erstellen, speichern und verwalten und gleichzeitig Benutzern mehrerer Datenbanken zur Verfügung stellen. Für Benutzer sieht eine verknüpfte Dimension genauso aus wie jede andere Dimension.  
  
 Verknüpfte Dimensionen sind schreibgeschützt. Wenn Sie die Dimension ändern oder neue Beziehungen erstellen möchten, müssen Sie die Quelldimension ändern und anschließend die verknüpfte Dimension und deren Beziehungen löschen und neu erstellen. Es ist nicht möglich, eine verknüpfte Dimension zu aktualisieren, um Änderungen aus dem Quellobjekt zu übernehmen.  
  
 Alle verwandten Measuregruppen und Dimensionen müssen aus derselben Quelldatenbank stammen. Sie können keine neuen Beziehungen zwischen lokalen Measuregruppen und den verknüpften Dimensionen erstellen, die Sie dem Cube hinzufügen. Nach dem Hinzufügen verknüpfter Dimensionen und Measuregruppen zum aktuellen Cube müssen die Beziehungen zwischen ihnen in ihrer Quelldatenbank verwaltet werden.  
  
> [!NOTE]  
>  Da keine Aktualisierungsfunktion verfügbar ist, werden Dimensionen von den meisten Analysis Services-Entwicklern kopiert und nicht verknüpft. Sie können Dimensionen zwischen Projekten innerhalb derselben Projektmappe kopieren. Weitere Informationen finden Sie unter [Aktualisieren einer verknüpften Dimension in SSAS](http://sqlblog.com/blogs/marco_russo/archive/2006/09/12/refresh-of-a-linked-dimension-in-ssas.aspx).  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Die Quelldatenbank, die die Dimension enthält, und die aktuelle Datenbank, von der sie verwendet wird, müssen über die gleiche Version und den gleichen Kompatibilitätsgrad verfügen. Weitere Informationen finden Sie unter [Festlegen des Kompatibilitäts Grad einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
 Die Quelldatenbank muss bereitgestellt und online geschaltet sein. Server, die verknüpfte Objekte veröffentlichen oder nutzen, müssen so konfiguriert werden, dass der Vorgang zulässig ist (siehe unten).  
  
 Die Dimension, die Sie verwenden möchten, darf selbst keine verknüpfte Dimension sein.  
  
## <a name="configure-server-to-allow-linked-objects"></a>Konfigurieren des Servers, sodass verknüpfte Objekte zulässig sind  
  
1.  Stellen Sie in SQL Server Management Studio eine Verbindung mit einem Analysis Services-Server her. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Servernamen, und wählen Sie **Facets**aus.  
  
2.  Legen Sie **LinkedObjectsLinksFromOtherInstancesEnabled** auf **True** fest, damit der Server Anforderungen für verknüpfte Objekte ausgeben kann, die sich in Datenbanken befinden, die in anderen Instanzen ausgeführt werden.  
  
3.  Legen Sie **LinkedObjectsLinksToOtherInstances** auf **True** fest, damit der Server Daten für verknüpfte Objekte in Datenbanken anfordern kann, die in anderen Instanzen ausgeführt werden.  
  
## <a name="create-a-linked-dimension-in-sql-server-data-tools"></a>Erstellen einer verknüpften Dimension in SQL Server-Datentools  
  
1.  Starten Sie den Assistenten. Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]mit der rechten Maustaste auf den Ordner **Dimensionen** in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank oder einem -Projekt, und klicken Sie dann auf **Neue verknüpfte Dimension**.  
  
2.  Stellen Sie eine Verbindung mit der Analysis Services-Datenbank her, die die Dimension bereitstellt. Wählen Sie auf der Seite **Datenquelle auswählen** des Assistenten für verknüpfte Objekte die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle aus oder erstellen Sie eine neue.  
  
3.  Wählen Sie auf der Seite **Objekte auswählen** des Assistenten die Dimensionen aus, zu denen ein Link in der Remotedatenbank hergestellt werden soll.  
  
4.  Auf der Seite **Assistenten abschließen** können Sie eine Vorschau der verknüpften Objekte anzeigen. Wenn Sie einen Link zu einer Dimension herstellen, die denselben Namen wie eine bereits bestehende aufweist, wird eine Ordinalzahl (beginnend mit '1' für den ersten doppelten Namen) an den Namen angefügt. Beim Abschließen des Assistenten wird die Dimension dem Ordner **Dimensionen** hinzugefügt.  
  
##  <a name="bkmk_CreateNew"></a>Erstellen einer neuen Datenquellen Verbindung mit einer Analysis Services Datenbank  
 Verwenden Sie den Assistenten Neue Datenquelle, um dem Projekt Verbindungsinformationen zur Analysis Services-Datenbank hinzuzufügen, die die Dimension bereitstellt. Sie können den Assistenten starten, indem Sie auf der Seite Datenquelle auswählen des Assistenten für verknüpfte Objekte auf **Neue Datenquelle** klicken.  
  
1.  Klicken Sie im Datenquellen-Assistenten auf der Seite **Wählen Sie aus, wie die Verbindung definiert werden soll**auf Neu.  
  
2.  Überprüfen Sie im Verbindungs-Manager, ob der Anbieter auf **OLE DB systemeigen\Microsoft OLE DB-Anbieter für Analysis Services 11.0**festgelegt ist.  
  
3.  Geben Sie den Namen des Servers (Server *Name*\\*instanceName* für eine benannte Instanz)<sup>1 ein</sup> , oder geben Sie **localhost** ein, um eine Verbindung mit einem Analysis Services Server herzustellen, der auf demselben Computer ausgeführt wird.  
  
4.  Verwenden Sie die Windows-Authentifizierung für die Verbindung.  
  
5.  Klicken Sie in **Anfangskatalog**auf den Pfeil nach unten, um eine Datenbank auf diesem Server auszuwählen.  
  
6.  Klicken Sie im Datenquellen-Assistenten auf **Weiter** , um den Vorgang fortzusetzen.  
  
7.  Klicken Sie auf der Seite **Identitätswechselinformationen**auf Dienstkonto. Klicken Sie auf **Weiter**, und beenden Sie den Assistenten. Die gerade definierte Verbindung wird im Assistenten für verknüpfte Objekte ausgewählt.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie können die Struktur einer verknüpften Dimension nicht ändern; deshalb kann sie nicht mithilfe der Registerkarte **Dimensionsstruktur** des Dimensions-Designers angezeigt werden. Nachdem Sie die verknüpfte Dimension verarbeitet haben, können Sie Sie mit der Registerkarte **Browser** anzeigen. Sie können auch den Namen ändern und eine Übersetzung für den Namen erstellen.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Legen Sie den Kompatibilitäts Grad einer mehrdimensionalen Datenbank &#40;Analysis Services fest&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Verknüpfte Measure-Gruppen](linked-measure-groups.md)   
 [Dimensionsbeziehungen](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
  
  
