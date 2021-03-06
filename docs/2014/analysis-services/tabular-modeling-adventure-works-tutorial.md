---
title: Tabellen Modellierung (Adventure Works-Tutorial) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af4d5dfa6d59338fb9640143b387b78421375e05
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067803"
---
# <a name="tabular-modeling-adventure-works-tutorial"></a>Tabellenmodellierung (Adventure Works-Lernprogramm)
  Dieses Tutorial enthält Lektionen zum Erstellen eines tabellarischen [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Analysis Services-Modells unter Verwendung von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="what-you-will-learn"></a>Lernziele  
 Im Rahmen dieses Lernprogramms führen Sie die folgenden Aufgaben aus:  
  
-   Erstellen eines neuen Tabellenmodellprojekts in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Importieren von Daten von einer relationalen SQL Server-Datenbank in ein Tabellenmodellprojekt.  
  
-   Wie Sie Beziehungen zwischen den einzelnen Tabellen im Modell verwalten können.  
  
-   Erstellen und Verwalten von Berechnungen, Measures und Key Performance Indicators, mit denen Benutzer Modelldaten analysieren können.  
  
-   Erstellen und Verwalten von Perspektiven und Hierarchien, mit denen Benutzer durch die Bereitstellung von geschäfts- und anwendungsspezifischen Blickpunkten einfacher Modelldaten durchsuchen können.  
  
-   Wie Sie Partitionen erstellen können, die Tabellendaten in kleiner logische Teile aufteilen, die unabhängig von anderen Partitionen verarbeitet werden können.  
  
-   Wie Sie Modellobjekte und -daten sichern können, indem Sie Rollen mit Benutzern erstellen.  
  
-   Bereitstellen eines tabellarischen Models für einen Sandkasten oder eine Produktionsinstanz von Analysis Services im tabellarischen Modus.  
  
## <a name="tutorial-scenario"></a>Lernprogrammszenario  
 Dieses Lernprogramm basiert auf [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], einem fiktiven Unternehmen. 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ist ein großes, multinationales Herstellungsunternehmen, das Fahrräder aus Metall und Verbundwerkstoffen für kommerzielle Märkte in Nordamerika, Europa und Asien produziert und vertreibt. Die Zentrale von [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] befindet sich in Bothell, Washington (USA), wo das Unternehmen 500 Arbeiter beschäftigt. Zusätzlich beschäftigt [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] eine Reihe von regionalen Verkaufsteams für die gesamte Marktbasis.  
  
 Um die Datenanalyseanforderungen von Verkaufs- und Marketingteams sowie des Senior Managements besser zu unterstützen, werden Sie damit beauftragt, ein Tabellenmodell für Benutzer zu erstellen, um Internetumsatzdaten in der AdventureWorksDW-Beispieldatenbank zu analysieren.  
  
 Um das Lernprogramm und das Tabellenmodell für die Adventure Works-Internetverkäufe abzuschließen, ist eine Reihe von Lektionen auszuführen. Jede Lektion setzt sich aus verschiedenen Aufgaben zusammen. Sie müssen die Aufgaben nacheinander durchführen, um die Lektion abzuschließen. In einer bestimmten Lektion können mehrere Aufgaben enthalten sein, die zu einem ähnlichen Ergebnis führen. Die Ausführung der jeweiligen Aufgabe unterscheidet sich jedoch leicht. Dadurch soll vermittelt werden, dass oftmals mehrere Möglichkeiten zum Ausführen einer bestimmten Aufgabe bestehen. Zudem soll dies für Sie eine Herausforderung darstellen, indem Sie in vorherigen Aufgaben erlernte Fähigkeiten einsetzen.  
  
 In den Lektionen werden Sie durch die Erstellung eines grundlegenden tabellarischen Modells, das im InMemory-Modus ausgeführt wird, unter Verwendung zahlreicher in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] enthaltener Funktionen geführt. Da jede Lektion auf der vorherigen aufbaut, sollten Sie diese in der richtigen Reihenfolge abschließen. Nach dem Abschließen aller Lektionen haben Sie das Beispieltabellenmodell für die Adventure Works-Internetverkäufe auf einem Analysis Services-Server erstellt und bereitgestellt.  
  
> [!NOTE]  
>  Dieses Lernprogramm enthält keine Lektionen oder Informationen zum Verwalten einer Datenbank für Tabellenmodelle unter Verwendung von SQL Server Management Studio oder das Verwenden einer Berichterstellungs-Clientanwendung zur Herstellung einer Verbindung mit einem bereitgestellten Modell zum Durchsuchen von Modelldaten.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Um dieses Lernprogramm abzuschließen, müssen die folgenden Komponenten installiert sein:  
  
-   Im tabellarischen Modus ausgeführte [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Analysis Services-Instanz.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   AdventureWorksDW-Beispieldatenbank. Diese Beispieldatenbank beinhaltet die für den Abschluss dieses Tutorials erforderlichen Daten. Informationen zum Herunterladen der Beispieldatenbank [https://go.microsoft.com/fwlink/?LinkID=335807](https://go.microsoft.com/fwlink/?LinkID=335807)finden Sie unter.  
  
-   
  [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 oder höher (zur Verwendung mit der Funktion In Excel analysieren in Lektion 11).  
  
## <a name="lessons"></a>Lektionen  
 Dieses Lernprogramm enthält die folgenden Lektionen:  
  
|Lektion|Geschätzter Zeitaufwand|  
|------------|--------------------------------|  
|[Lektion 1: Erstellen eines neuen Tabellenmodellprojekts](lesson-1-create-a-new-tabular-model-project.md)|10 Minuten|  
|[Lektion 2: Hinzufügen von Daten](lesson-2-add-data.md)|20 Minuten|  
|[Lektion 3: Umbenennen von Spalten](rename-columns.md)|20 Minuten|  
|[Lektion 4: Markieren als Datumstabelle](lesson-3-mark-as-date-table.md)|3 Minuten|  
|[Lektion 5: Erstellen von Beziehungen](lesson-4-create-relationships.md)|10 Minuten|  
|[Lektion 6: Erstellen von berechneten Spalten](lesson-5-create-calculated-columns.md)|15 Minuten|  
|[Lektion 7: Erstellen von Measures](lesson-6-create-measures.md)|30 Minuten|  
|[Lektion 8: Erstellen von Leistungskennzahlen](lesson-7-create-key-performance-indicators.md)|15 Minuten|  
|[Lektion 9: Erstellen von Perspektiven](lesson-8-create-perspectives.md)|5 Minuten|  
|[Lektion 10: Erstellen von Hierarchien](lesson-9-create-hierarchies.md)|20 Minuten|  
|[Lektion 11: Erstellen von Partitionen](lesson-10-create-partitions.md)|15 Minuten|  
|[Lektion 12: Erstellen von Rollen](lesson-11-create-roles.md)|15 Minuten|  
|[Lektion 13: Analysieren in Excel](lesson-12-analyze-in-excel.md)|20 Minuten|  
|[Lektion 14: Bereitstellen](lesson-13-deploy.md)|5 Minuten|  
  
## <a name="supplemental-lessons"></a>Ergänzende Lektionen  
 Dieses Tutorial umfasst außerdem [ergänzende Lektionen](../tutorials/supplemental-lessons.md). Die Themen in diesem Abschnitt sind nicht erforderlich, um das Lernprogramm abzuschließen, aber sie können das Verständnis der erweiterten Funktionen zum Erstellen eines Tabellenmodells erleichtern.  
  
 Dieses Lernprogramm umfasst die folgenden ergänzenden Lektionen:  
  
|Lektion|Geschätzter Zeitaufwand|  
|------------|--------------------------------|  
|[Implementieren von dynamischer Sicherheit mithilfe von Zeilenfiltern](../tutorials/implement-dynamic-security-by-using-row-filters.md)|30 Minuten|  
|[Konfigurieren von Bericht Erstellungs Eigenschaften für Power View Berichte](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md) Konfigurieren von Bericht Erstellungs Eigenschaften für Power View Berichte|30 Minuten|  
  
## <a name="next-step"></a>Nächster Schritt  
 Um das Tutorial zu starten, gehen Sie zur ersten Lektion über: [Lektion 1: Erstellen eines neuen Tabellenmodellprojekts](lesson-1-create-a-new-tabular-model-project.md).  
  
  
