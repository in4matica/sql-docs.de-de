---
title: Vorlage zur Ebenenbenennung (Dialog Feld) (Analysis Services Mehrdimensionale Daten) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.levelnamingtemplatedialog.f1
helpviewer_keywords:
- Level Naming Template dialog box
ms.assetid: 96cad715-213e-4eac-9003-130a2f5fc985
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: febaae6051e8428d3fed2bb6533ce2c4d972950f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078058"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>Dialogfeld 'Vorlage zur Ebenenbenennung' (Analysis Services – Mehrdimensionale Daten)
  Mithilfe des Dialogfelds **Vorlage zur Ebenenbenennung** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] können Sie eine Vorlage zur Ebenenbenennung für ein übergeordnetes Attribut in einer Dimension erstellen. Weitere Informationen über Vorlagen zur Ebenenbenennung finden Sie unter [NamingTemplate Element &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/namingtemplate-element-assl). Sie können das Dialog **Feld Vorlage zur Ebenenbenennung** anzeigen, indem Sie im **Dimensions-Designer**auf der Registerkarte `NamingTemplate` **Übersetzungen** im Bereich **Übersetzungs Details** auf die Schaltfläche mit den Auslassungs Punkten (**...**) klicken.  
  
## <a name="options"></a>Tastatur  
  
|Begriff|Definition|  
|----------|----------------|  
|**Ebenenvorlage definieren**|Zeigt ein Raster an, in dem Sie die Hierarchie der Ebenen in dem übergeordneten Attribut gestalten können. Das Raster enthält die folgenden Spalten:<br /><br /> **Level**: zeigt die Ordnungsposition der Ebene an, für die der in **Name** angegebene Name verwendet wird. Wählen Sie die Option **Name** in der Zeile aus, die ein Sternchen (\*) unter **Ebene** enthält, um eine neue Vorlage für die Benennung einer Ebene hinzuzufügen.<br /><br /> **Name**: enthält die Benennungs Vorlage für die Ebene, die unter **Ebene**angegeben wird. Als Platzhalter für die Ordnungsposition der Ebene in der Vorlage zur Benennung fügen Sie ein einzelnes Sternchen (*) hinzu. Wenn Sie ein Sternchen als Teil des Namens hinzufügen möchten, der von der Benennungs Vorlage erstellt wurde,\*\*fügen Sie zwei Sternchen () hinzu.|  
|**Alle löschen**|Entfernt alle Zeilen unter **Ebenenvorlage definieren**.|  
|**Ergebnis**|Zeigt die im Dialogfeld erstellte Vorlage zur Ebenenbenennung an.|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Analysis Services Designer und Dialog Felder &#40;Mehrdimensionale Daten&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Übersetzungen &#40;Dimensions-Designer&#41; &#40;Analysis Services Mehrdimensionale Daten&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
