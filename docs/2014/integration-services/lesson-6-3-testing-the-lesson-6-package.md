---
title: 'Schritt 3: Testen des Pakets aus Lektion 6 | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c69c75c9dff4bf8d0542dae71cddcf1a431ab063
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "62890862"
---
# <a name="step-3-testing-the-lesson-6-package"></a>Schritt 3: Testen des Pakets aus Lektion 6
  Zur Laufzeit erhält Ihr Paket den Wert für die Eigenschaft "Verzeichnis" vom VarFolderName-Parameter.  
  
 Um zu überprüfen, ob vom Paket die Directory-Eigenschaft während der Laufzeit auf den neuen Wert aktualisiert wird, führen Sie das Paket einfach aus. Weil nur drei Beispieldatendateien in das neue Verzeichnis kopiert werden, wird der Datenfluss nur drei Mal ausgeführt, statt durch 14 Dateien im ursprünglichen Ordner zu iterieren.  
  
## <a name="checking-the-package-layout"></a>Überprüfen des Paketlayouts  
 Bevor Sie das Paket testen, sollten Sie überprüfen, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 6 die in den folgenden Diagrammen gezeigten Objekte enthalten. Die Ablaufsteuerung sollte mit der Ablaufsteuerung in Lektion 5 übereinstimmen. Der Datenfluss sollte mit dem Datenfluss in Lektion 5 übereinstimmen.  
  
 **Ablaufsteuerung**  
  
 ![Ablaufsteuerung](../../2014/tutorials/media/task3lesson6control.jpg "Ablaufsteuerung")  
  
 **Datenfluss**  
  
 ![Datenfluss](../../2014/tutorials/media/task3lesson6data.jpg "Datenfluss")  
  
### <a name="to-test-the-lesson-6-tutorial-package"></a>So testen Sie das Lektion 6-Lernprogrammpaket  
  
1.  Klicken Sie im Menü "Debuggen" auf "Debuggen starten".  
  
2.  Klicken Sie nach Ausführen des Pakets im Menü "Debuggen" auf "Debuggen beenden".  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
 [Schritt 4: Bereitstellen des Pakets aus Lektion 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
