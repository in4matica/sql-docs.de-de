---
title: Drucken von Berichten in einem Browser mit dem Drucksteuerelement (Berichts-Generator) | Microsoft-Dokumentation
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 10054250-d915-4bcb-8a1d-26837db4e932
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bc5eabd755bec6c25c16b3974efe267cf3e27c72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "77082542"
---
# <a name="print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs"></a>Drucken von Berichten in einem Browser mit dem Drucksteuerelement (Berichts-Generator und SSRS)
  Ein Browser ist zwar die am häufigsten verwendete Clientanwendung zum Anzeigen von Berichten, die Druckfunktionen des Browsers sind jedoch für das Drucken von Berichten nicht ideal. Die Druckfunktionen eines Browsers sind zum Drucken von Webseiten konzipiert. In der Regel enthalten die von einem Browser gedruckten Seiten alle visuellen Elemente einer Webseite, dazu Kopf- und Fußzeileninformationen zur Identifikation der Seite oder Website. Beim Drucken über einen Browser wird der Inhalt des aktuellen Fensters gedruckt. Bei mehrseitigen Berichten wird maximal die erste Seite gedruckt, möglicherweise sogar weniger, wenn die Berichtsseite die Dimensionen der gedruckten Seite übersteigt.  
  
 Wenn Sie die Druckqualität der in einem Browser angezeigten Berichte verbessern und mehrere Seiten drucken möchten, können Sie die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]bereitgestellte clientseitige Druckfunktion verwenden. Die clientseitige Druckfunktion stellt ein Standarddialogfeld **Drucken** bereit, das zum Auswählen eines Druckers, Angeben von Seiten und Rändern sowie zum Anzeigen einer Vorschau des Berichts vor dem Drucken verwendet wird. Verwenden Sie die clientseitige Druckfunktion anstelle des Befehls **Drucken** im Menü **Datei** des Browsers. Beim Verwenden dieser Funktion wird der Bericht gemäß seines Entwurfs gedruckt, ohne zusätzliche Elemente, die im Ausdruck einer Webseite zu finden sind.  
  
 Für den clientseitigen Druck müssen Sie ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] -ActiveX-Steuerelement installieren. Weitere Informationen finden Sie unter [Aktivieren und Deaktivieren des clientseitigen Drucks für Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="print-options"></a>Druckoptionen  
 Sie können Druckeigenschaften für Ihren Bericht konfigurieren, indem Sie im Dialogfeld **Drucken** auf die Schaltfläche **Eigenschaften** klicken. Der Wert für**Papierformat** wird durch die Standardhöhe und -breite der Berichtsseitengröße gemäß Berichtsdefinition bestimmt. Die verfügbaren Werte sind vom Druckertyp und seinen Funktionen abhängig. Für Breite und Höhe werden Standardwerte angezeigt, die durch die auf dem Computer konfigurierten Druckertreiber bestimmt werden. Nach dem Ändern dieser Werte wird der Bericht mit den neuen Abmessungen gedruckt. Die Seitenbreite und -höhe wird durch **Ausrichtung**bestimmt. Mögliche Werte sind **Hochformat** oder **Querformat**. Die angezeigte Standardausrichtung ist von der Seitenbreite und Seitenhöhe des Berichts abhängig.  
  
> [!NOTE]  
>  Das Dialogfeld **Drucken** und die Standarddruckereinstellungen für Breite, Höhe und Seitenausrichtung werden von der Berichtsdefinition bestimmt.  
  
### <a name="print-preview"></a>Seitenansicht  
 Sie können die Vorschau eines Berichts anzeigen, indem Sie im Dialogfeld **Drucken** auf die Schaltfläche **Vorschau** klicken. Durch Klicken auf Vorschau wird die erste Seite des Berichts in einem separaten Vorschaufenster geöffnet. Weitere Seiten werden beim Rendern des Berichts auf dem Berichtsserver verfügbar. Ein als Vorschau angezeigter Bericht wird im EMF-Format gerendert. Sie können zur vorherigen oder nächsten Seite navigieren, bis die letzte Seite erreicht ist. Dann ist die Schaltfläche **Weiter** deaktiviert.  
  
### <a name="adjusting-print-margins"></a>Anpassen der Druckränder  
 Sie können die Druckränder im gerenderten EMF-Bericht vor dem Drucken des Berichts ändern. Klicken Sie hierzu im Dialogfeld **Drucken** auf die Schaltfläche **Vorschau** . Klicken Sie oben auf der Vorschauseite auf die Schaltfläche **Ränder** . Das Dialogfeld Ränder wird angezeigt. Konfigurieren Sie bei Bedarf den oberen, unteren, rechten und linken Rand. [!INCLUDE[clickOK](../../includes/clickok-md.md)] Das Dialogfeld wird geschlossen, und die Einstellungen werden für die Renderingvorschau und den Druckvorgang gespeichert.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Drucken von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Drucken eines Berichts &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
  
  
