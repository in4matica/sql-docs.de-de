---
title: Verknüpfte Measure-Gruppen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linked measure groups [Analysis Services]
- referencing measure groups
- Linked Measure Group Wizard
- measure groups [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: 7f838452-8669-4194-8e15-7afdc7f15251
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec38404a32751330d7fefd974fafe3d571d3b11b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074781"
---
# <a name="linked-measure-groups"></a>Verknüpfte Measuregruppen
  Eine verknüpfte Measuregruppe basiert auf einer anderen Measuregruppe in einem anderen Cube innerhalb derselben Datenbank oder einer anderen Analysis Services-Datenbank. Eine verknüpfte Measuregruppe kann z. B. verwendet werden, wenn Sie einen Satz von Measures und die entsprechenden Datenwerte in mehreren Cubes wiederverwenden möchten.  
  
 Microsoft empfiehlt, die ursprünglichen und verknüpften Measuregruppen in Projektmappen abzulegen, die auf dem gleichen Server ausgeführt werden. Das Verknüpfen mit einer Measure-Gruppe auf einem Remote Server wird in einer zukünftigen Version als veraltet eingestuft (siehe [Veraltete Analysis Services Features in SQL Server 2014](../deprecated-analysis-services-features-in-sql-server-2014.md)).  
  
> [!IMPORTANT]  
>  Verknüpfte Measuregruppen sind schreibgeschützt. Um die neuesten Änderungen zu übernehmen, müssen Sie alle auf dem geänderten Quellobjekt basierenden verknüpften Measuregruppen löschen und neu erstellen. Aus diesem Grund sollten Sie das Kopieren und Einfügen von Measuregruppen als alternative Methode berücksichtigen, wenn zukünftige Änderungen der Measuregruppe erforderlich sind.  
  
## <a name="usage-limitations"></a>Nutzungseinschränkungen  
 Wie bereits erwähnt, besteht eine wichtige Einschränkung bei der Verwendung von verknüpften Measures darin, dass ein verknüpftes Measure nicht direkt angepasst werden kann. Änderungen an Datentyp, Format, Datenbindung und Sichtbarkeit sowie an der Mitgliedschaft der Elemente in der Measuregruppe selbst sind Änderungen, die an der ursprünglichen Measuregruppe vorgenommen werden müssen.  
  
 Funktionell sind verknüpfte Measuregruppen identisch mit anderen Measuregruppen, wenn Clientanwendungen darauf zugreifen, und sie werden auf dieselbe Weise wie andere Measuregruppen abgefragt.  
  
 Bei der Abfrage eines Cubes, der eine verknüpfte Measuregruppe enthält, wird der Link beim ersten Berechnungsdurchlauf des Zielcubes eingerichtet und aufgelöst. Wegen dieses Verhaltens können Berechnungen, die in der verknüpften Measuregruppe gespeichert sind, nicht aufgelöst werden, bevor die Abfrage ausgewertet ist. Mit anderen Worten: Anstatt berechnete Measures und Zellen vom Quellcube zu erben, müssen diese im Zielcube neu berechnet werden.  
  
 In der folgenden Liste sind Nutzungseinschränkungen zusammengefasst.  
  
-   Sie können keine verknüpfte Measuregruppe aus einer anderen verknüpften Measuregruppe erstellen.  
  
-   Sie können in einer verknüpften Measuregruppe keine Measures hinzufügen oder entfernen. Die Mitgliedschaft wird nur in der ursprünglichen Measuregruppe definiert.  
  
-   Das Rückschreiben wird in verknüpften Measuregruppen nicht unterstützt.  
  
-   Verknüpfte Measuregruppen können nicht in mehreren m:n-Beziehungen verwendet werden, insbesondere wenn sich diese Beziehungen in verschiedenen Cubes befinden. Andernfalls können mehrdeutige Aggregationen entstehen. Weitere Informationen finden Sie unter [Falsche Mengen für verknüpfte Measures in Cubes mit m:n-Beziehungen](https://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx).  
  
 Die in einer verknüpften Measuregruppe enthaltenen Measures können nur anhand von verknüpften Dimensionen direkt organisiert werden, die aus derselben [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank abgerufen wurden. Mithilfe von berechneten Elementen können Sie jedoch Informationen aus verknüpften Measuregruppen mit anderen, nicht verknüpften Dimensionen im Cube verbinden. Sie können auch eine indirekte Beziehung wie einen Verweis oder eine m:n-Beziehung verwenden, um nicht verknüpfte Dimensionen mit einer verknüpften Measuregruppe zu verbinden.  
  
## <a name="create-or-modify-a-linked-measure"></a>Erstellen oder Ändern eines verknüpften Measures  
 Verwenden Sie [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] , um eine verknüpfte Measuregruppe zu erstellen.  
  
1.  Schließen Sie jetzt alle Änderungen an der ursprünglichen Measuregruppe im Quellcube ab, damit Sie die verknüpften Measuregruppen später in nachfolgenden Cubes nicht erneut erstellen müssen. Sie können ein verknüpftes Objekt umbenennen, aber keine anderen Eigenschaften ändern.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf den Cube, dem Sie die verknüpfte Measuregruppe hinzufügen. Durch diesen Schritt wird der Cube im Cube-Designer geöffnet.  
  
3.  Klicken Sie im Cube-Designer entweder im Bereich Measures oder im Bereich Dimensionen mit der rechten Maustaste auf eine beliebige Stelle, und wählen Sie dann **Neues verknüpftes Objekt**aus. Dadurch wird der Assistent für verknüpfte Objekte gestartet.  
  
4.  Geben Sie auf der ersten Seite die Datenquelle an. Durch diesen Schritt wird der Speicherort der ursprünglichen Measuregruppe angegeben. Dieser entspricht standardmäßig dem aktuellen Cube in der aktuellen Datenbank, Sie können jedoch auch eine andere Analysis Services-Datenbank auswählen.  
  
5.  Wählen Sie auf der nächsten Seite die Measuregruppe oder Dimension aus, die Sie verknüpfen möchten. Dimensionen und Cubeobjekte, wie Measuregruppen, werden separat aufgeführt. Es sind nur Objekte verfügbar, die noch nicht im aktuellen Cube enthalten sind.  
  
6.  Klicken Sie auf **Fertig stellen** , um das verknüpfte Objekt zu erstellen. Verknüpfte Objekte werden in den Bereichen Measures und Dimensionen angezeigt und sind durch das Linksymbol gekennzeichnet.  
  
## <a name="secure-a-linked-measure"></a>Schützen eines verknüpften Measures  
 Nachdem der Link definiert wurde, wird der Zugriff auf die Measures in einer verknüpften Measuregruppe auf dieselbe Weise wie andere Measuregruppen verwaltet. Ein verknüpftes Objekt wird im Rollen-Designer neben dessen nicht verknüpften Gegenstücken angezeigt. Weitere Informationen zum Verwalten der Sicherheit für eine Measuregruppe finden Sie unter [Erteilen von Cube- oder Modellberechtigungen &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md).  
  
 Um eine verknüpfte Measuregruppe zu definieren oder zu verwenden, muss das Windows-Dienstkonto für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz Mitglied einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbankrolle sein, die über `ReadDefinition`- und `Read`-Zugriffsrechte für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Quellinstanz auf den Quellcube und die Measuregruppe verfügt, oder es muss Mitglied der Rolle der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Administratoren für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Quellinstanz sein.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Definieren von verknüpften Dimensionen](define-linked-dimensions.md)  
  
  
