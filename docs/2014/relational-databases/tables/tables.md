---
title: Tabellen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server]
- table components [SQL Server]
ms.assetid: 82d7819c-b801-4309-a849-baa63083e83f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7a456d68283d81cf7eb4f879d76f086484c5e052
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211787"
---
# <a name="tables"></a>Tabellen
  Tabellen sind Datenbankobjekte, die sämtliche in einer Datenbank enthaltenen Daten umfassen. Die Daten in den Tabellen sind, ähnlich wie in einer Kalkulationstabelle, logisch in Zeilen und Spalten angeordnet. Jede Zeile stellt einen eindeutigen Datensatz und jede Spalte ein Feld im Datensatz dar. Eine Tabelle, die z. B. die Angestelltendaten für ein Unternehmen enthält, könnte eine Zeile für jeden Angestellten sowie Spalten enthalten, die Informationen zu einzelnen Angestellten angeben, wie z. B. die Mitarbeiternummer, den Namen, die Adresse, die Berufsbezeichnung und die private Telefonnummer.  
  
-   Die Anzahl der Tabellen in einer Datenbank ist nur durch die in einer Datenbank zulässige Anzahl an Objekten beschränkt (2.147.483.647). Eine standardmäßige benutzerdefinierte Tabelle kann bis zu 1.024 Spalten enthalten. Die Anzahl der Zeilen in der Tabelle wird nur durch die Speicherkapazität des Servers beschränkt.  
  
-   Sie können der Tabelle und jeder Spalte in der Tabelle Eigenschaften zuweisen, um die zulässigen Daten und weitere Eigenschaften zu steuern. Sie können z. B. Einschränkungen für eine Spalte erstellen, um keine NULL-Werte zuzulassen, oder einen Standardwert bereitstellen, wenn ein Wert nicht angegeben wird. Sie können außerdem eine Schlüsseleinschränkung für die Tabelle zuweisen, die Eindeutigkeit erzwingt oder eine Beziehung zwischen Tabellen definiert.  
  
-   Die Daten in der Tabelle können entweder nach Zeile oder Seite komprimiert werden. Durch die Datenkomprimierung können mehrere Zeilen auf einer Seite gespeichert werden. Weitere Informationen finden Sie unter [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
## <a name="types-of-tables"></a>Typen von Tabellen  
 Neben der Standardrolle der grundlegenden benutzerdefinierten Tabellen bietet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die folgenden Typen von Tabellen, die innerhalb einer Datenbank speziellen Zwecken dienen:  
  
 Partitionierte Tabellen  
 Partitionierte Tabellen sind Tabellen, deren Daten horizontal in Einheiten aufgeteilt sind, die über mehrere Dateigruppen innerhalb einer Datenbank verteilt sein können. Durch die Partitionierung sind große Tabellen oder Indizes leichter zu verwalten, denn Sie können dadurch schnell und effizient auf Datenteilmengen zugreifen und sie verwalten, während die Integrität der gesamten Sammlung erhalten bleibt. Standardmäßig unterstützt [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bis zu 15.000 Partitionen. Weitere Informationen finden Sie unter [partitionierte Tabellen und Indizes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Temporäre Tabellen  
 Temporäre Tabellen werden in `tempdb` gespeichert. Es gibt zwei Arten von temporären Tabellen: lokale und globale temporäre Tabellen. Sie unterscheiden sich hinsichtlich ihrer Namen, ihrer Sichtbarkeit und ihrer Verfügbarkeit. Lokale temporäre Tabellen weisen als erstes Zeichen ihres Namens ein einzelnes Nummernzeichen (#) auf. Sie sind nur im Rahmen der aktuellen Verbindung des Benutzers sichtbar und werden gelöscht, sobald der Benutzer die Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]trennt. Globale temporäre Tabellen weisen als erste Zeichen ihres Namens zwei Nummernzeichen (##) auf. Nachdem sie erstellt wurden, sind sie für jeden Benutzer sichtbar, und sie werden gelöscht, nachdem alle Benutzer, die auf diese Tabelle verweisen, die Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]getrennt haben.  
  
 Systemtabellen  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichert die Daten, welche die Konfiguration des Servers sowie alle seine Tabellen definieren, in einem bestimmten Satz von Tabellen, die als Systemtabellen bezeichnet werden. Benutzer können die Systemtabellen nicht direkt abfragen oder aktualisieren. Die in den Systemtabellen enthaltenen Informationen werden über die Systemsichten zur Verfügung gestellt. Weitere Informationen finden Sie unter [Systemsichten &#40;Transact-SQL&#41;](/sql/t-sql/language-reference).  
  
 Breite Tabellen  
 Breite Tabellen verwenden [Sparsespalten](use-sparse-columns.md) , um die möglichen Spalten einer Tabelle auf 30.000 zu erhöhen. Spalten mit geringer Dichte sind gewöhnliche Spalten, die einen optimierten Speicher für NULL-Werte haben. Spalten mit geringer Dichte reduzieren die Speicherplatzanforderungen von NULL-Werten auf Kosten eines erhöhten Aufwands, um Werte ungleich NULL abzurufen. Eine breite Tabelle besitzt einen definierten [Spaltensatz](use-column-sets.md), bei dem es sich um eine nicht typisierte XML-Darstellung handelt, die alle Sparsespalten einer Tabelle in einer strukturierten Ausgabe kombiniert. Die Anzahl der Indizes und Statistiken wird ebenfalls auf 1.000 bzw. 30.000 erhöht. Die maximale Größe einer breiten Tabelle beträgt normalerweise 8.019 Byte. Deshalb sollten die meisten Daten einer Zeile NULL sein. Für eine breite Tabelle beträgt die maximale Anzahl von Spalten ohne geringe Dichte zuzüglich der berechneten Spalten weiterhin 1.024.  
  
 Bei breiten Tabellen treten folgende Leistungsauswirkungen auf:  
  
-   Breite Tabellen können die Kosten für die Verwaltung der Indizes in der Tabelle erhöhen. Es ist ratsam, die Anzahl an Indizes für eine breite Tabelle auf die Indizes zu beschränken, die für die Geschäftslogik erforderlich sind. Wenn die Anzahl von Indizes zunimmt, gilt dies auch für die Anforderungen an DML-Kompilierzeit und Arbeitsspeicher. Bei nicht gruppierten Indizes sollte es sich um gefilterte Indizes handeln, die auf Datenteilmengen angewendet werden. Weitere Informationen finden Sie unter [erstellen gefilterter Indizes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
-   Anwendungen können breiten Tabellen dynamisch Spalten hinzufügen und daraus entfernen. Wenn Spalten hinzugefügt oder entfernt werden, werden kompilierte Abfragepläne ebenfalls als ungültig erklärt. Es ist ratsam, eine Anwendung gemäß der vorhergesagten Arbeitsauslastung zu entwerfen, damit Schemaänderungen minimiert werden.  
  
-   Wenn Daten einer breiten Tabelle hinzugefügt oder daraus entfernt werden, kann dies die Leistung beeinträchtigen. Anwendungen müssen für die vorhergesagte Arbeitsauslastung entworfen werden, damit Änderungen an den Tabellendaten minimiert werden.  
  
-   Beschränken Sie die Ausführung von DML-Anweisungen für eine breite Tabelle, bei denen mehrere Zeilen eines Gruppierungsschlüssels aktualisiert werden. Diese Anweisungen können für die Kompilierung und Ausführung beträchtliche Speicherressourcen erfordern.  
  
-   Partitionswechselvorgänge für breite Tabellen können langsam sein und für die Verarbeitung ggf. eine große Menge an Arbeitsspeicher erfordern. Die Leistungs- und Arbeitsspeicheranforderungen sind proportional zur Gesamtzahl der Spalten in der Quell- und Zielpartition.  
  
-   Updatecursor, die bestimmte Spalten in einer breiten Tabelle aktualisieren, sollten die Spalten explizit in der FOR UPDATE-Klausel aufführen. Dies trägt zur Optimierung der Leistung bei der Verwendung von Cursorn bei.  
  
## <a name="common-table-tasks"></a>Allgemeine Tabellentasks  
 Die folgende Tabelle enthält Links zu häufigen Tasks, die dem Erstellen oder Ändern einer Tabelle zugeordnet sind.  
  
|Tabellentasks|Thema|  
|-----------------|-----------|  
|Beschreibt, wie eine Tabelle erstellt wird.|[Erstellen von Tabellen &#40;Datenbank-Engine&#41;](create-tables-database-engine.md)|  
|Beschreibt, wie eine Tabelle gelöscht wird.|[Tabellen &#40;Datenbank-Engine löschen&#41;](delete-tables-database-engine.md)|  
|Beschreibt, wie eine neue Tabelle erstellt wird, die einige oder alle Spalten einer vorhandenen Tabelle enthalten.|[Duplizieren von Tabellen](duplicate-tables.md)|  
|Beschreibt, wie eine Tabelle umbenannt wird.|[Tabellen &#40;Datenbank-Engine umbenennen&#41;](rename-tables-database-engine.md)|  
|Beschreibt, wie die Eigenschaften der Tabelle angezeigt werden.|[Anzeigen der Tabellendefinition](view-the-table-definition.md)|  
|Beschreibt, wie ermittelt wird, ob andere Objekte, z. B. eine Sicht oder gespeicherte Prozedur, von einer Tabelle abhängen.|[Anzeigen der Abhängigkeiten einer Tabelle](view-the-dependencies-of-a-table.md)|  
  
 Die folgende Tabelle enthält Links zu häufigen Tasks, die dem Erstellen oder Ändern von Spalten in einer Tabelle zugeordnet sind.  
  
|Spaltentasks|Thema|  
|------------------|-----------|  
|Beschreibt, wie einer vorhandenen Tabelle Spalten hinzugefügt werden.|[Hinzufügen von Spalten zu einer Tabelle &#40;Datenbank-Engine&#41;](add-columns-to-a-table-database-engine.md)|  
|Beschreibt, wie Spalten aus einer Tabelle gelöscht werden.|[Spalten aus einer Tabelle löschen](delete-columns-from-a-table.md)|  
|Beschreibt, wie der Name einer Spalte geändert wird.|[Spalten &#40;Datenbank-Engine umbenennen&#41;](rename-columns-database-engine.md)|  
|Beschreibt, wie Spalten einer Tabelle in eine andere Tabelle kopiert werden. Sie können entweder nur die Spaltendefinition oder die Definition und Daten kopieren.|[Spalten aus einer Tabelle in eine andere &#40;Datenbank-Engine kopieren&#41;](copy-columns-from-one-table-to-another-database-engine.md)|  
|Beschreibt, wie eine Spaltendefinition durch Ändern des Datentyps oder anderer Eigenschaften geändert wird.|[Ändern von Spalten &#40;Datenbank-Engine&#41;](modify-columns-database-engine.md)|  
|Beschreibt, wie die Reihenfolge, in der die Spalten angezeigt werden, geändert wird.|[Ändern der Spaltenreihenfolge einer Tabelle](change-column-order-in-a-table.md)|  
|Beschreibt, wie eine berechnete Spalte in einer Tabelle erstellt wird.|[Angeben von berechneten Spalten in einer Tabelle](specify-computed-columns-in-a-table.md)|  
|Beschreibt, wie ein Standardwert für eine Spalte angegeben wird. Dieser Wert wird verwendet, wenn kein anderer Wert angegeben wird.|[Angeben von Standardwerten für Spalten](specify-default-values-for-columns.md)|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Primary-und FOREIGN KEY-Einschränkungen](primary-and-foreign-key-constraints.md)   
 [UNIQUE- und CHECK-Einschränkungen](unique-constraints-and-check-constraints.md)  
  
  
