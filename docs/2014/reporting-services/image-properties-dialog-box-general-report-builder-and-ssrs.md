---
title: Bildeigenschaften (Dialog Feld), allgemein (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a66c424bfe5bd4a2587140a0f5238f46833a061
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109028"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>Bildeigenschaften (Dialogfeld), Allgemein (Berichts-Generator und SSRS)
  Wählen Sie im Dialogfeld **Bildeigenschaften** die Option **Allgemein** , um ein Bild hinzuzufügen, den Standardnamen des Bilds zu ändern und um QuickInfo-Text hinzuzufügen.  
  
## <a name="options"></a>Tastatur  
 **Name**  
 Geben Sie einen Namen für das Element ein. Der Name muss innerhalb des Berichts eindeutig sein. Standardmäßig wird ein allgemeiner Name zugewiesen, z. B. Image1 oder Image2.  
  
 **QuickInfo**  
 Geben Sie Text oder einen Ausdruck ein, der zu einer QuickInfo ausgewertet wird. Klicken Sie auf die Ausdrucks Schaltfläche (*FX*), um den Ausdruck zu bearbeiten. Die **QuickInfo** wird angezeigt, wenn der Benutzer den Zeiger über das Element in einem HTML-Bericht hält.  
  
 **Bildquelle auswählen**  
 Geben Sie den Speicherort des Bilds an, sodass der Berichtsprozessor dieses beim Rendern des Berichts abrufen kann.  
  
-   **Extern** Wählen Sie diese Option aus, wenn das Bild als Datei auf einem Berichts Server oder Webserver weiterhin vorhanden sein soll.  
  
-   **Eingebettet** Wählen Sie diese Option aus, wenn Sie das Bild in den Bericht einbetten möchten.  
  
-   **Datenbank** Wählen Sie diese Option aus, wenn Sie einen Daten Bank Feldnamen einschließen möchten, der die Bilder darstellt, die Sie in den Bericht einschließen möchten.  
  
 **Dieses Bild verwenden**  
 Diese Option wird angezeigt, wenn Sie die Option **Eingebettet** oder **Extern** auswählen.  
  
 Wenn Sie das Bild einbetten, wählen Sie das Bild, das Sie zum Bericht hinzufügen möchten, aus der Dropdownliste aus. Klicken Sie auf die Schaltfläche **Importieren** , um das Bild der Dropdownliste hinzuzufügen.  
  
 Wenn Sie die Option **Extern** aktivieren, geben Sie die URL des Bilds ein. Verwenden Sie für einen Bericht, der auf einem für den einheitlichen Modus konfigurierten Berichtsserver veröffentlicht werden soll, einen vollständigen oder relativen Pfad. Beispiel: http://\<Servername>/images/image1.jpg. Verwenden Sie für einen Bericht, der auf einem im integrierten SharePoint-Modus konfigurierten Berichtsserver veröffentlicht wird, eine vollqualifizierte URL. Beispiel: http://\<*SharePointServerName*>/\<*Site*>/Documents/images/image1.jpg).  
  
 **Importieren**  
 Klicken Sie auf diese Schaltfläche, um der Dropdownliste **Dieses Bild verwenden** ein Bild hinzuzufügen.  
  
 **Dieses Feld verwenden**  
 Diese Option wird angezeigt, wenn Sie die Option **Datenbank** aktivieren. Wählen Sie den Feldnamen aus.  
  
 **Diesen MIME-Typ verwenden**  
 Wählen Sie das entsprechende Format der in der Datenbank enthaltenen Bilder aus, z. B. BMP, JPEG, GIF, PNG und X-PNG.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Bilder &#40;Berichts-Generator und SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Berichts-Generator Hilfe zu Dialog Feldern, Bereichen und Assistenten](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
