---
title: Verwenden von Variablen in Paketen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined variables [Integration Services]
- variables [Integration Services], use scenarios
- system variables [Integration Services]
ms.assetid: 7742e92d-46c5-4cc4-b9a3-45b688ddb787
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96bfbf87789aa1d683b6368f210539a191f7ee95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054688"
---
# <a name="use-variables-in-packages"></a>Verwenden von Variablen in Paketen
  Variablen sind eine nützliche und flexible Erweiterung für [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakete. Sie können die Kommunikation zwischen Objekten innerhalb des Pakets und zwischen übergeordneten und untergeordneten Paketen ermöglichen. Variablen können außerdem in Ausdrücken und Skripts verwendet werden.  
  
## <a name="user-defined-variables-and-system-variables"></a>Benutzerdefinierte Variablen und Systemvariablen  
 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] bietet Systemvariablen und unterstützt benutzerdefinierte Variablen. Wenn Sie ein neues Paket erstellen, einem Paket einen Container oder einen Task hinzufügen oder einen Ereignishandler erstellen, schließt [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] eine Reihe von Systemvariablen für den Container ein. Systemvariablen enthalten nützliche Informationen zu einem Paket, einem Container, einem Task oder einem Ereignishandler. So enthält z. B. die Systemvariable **MachineName** zur Laufzeit den Namen des Computers, auf dem das Paket ausgeführt wird, und die Systemvariable **StartTime** enthält die Uhrzeit beim Start der Paketausführung. Systemvariablen sind schreibgeschützt. Weitere Informationen finden Sie unter [System Variables](system-variables.md).  
  
 Sie können benutzerdefinierte Variablen erstellen und diese in Paketen verwenden. Benutzerdefinierte Variablen können in [!INCLUDE[ssIS](../includes/ssis-md.md)]auf vielfältige Weise verwendet werden: in Skripts, in den von Rangfolgeeinschränkungen, vom For-Schleifencontainer, von der Transformation für abgeleitete Spalten und von der Transformation für bedingtes Teilen verwendeten Ausdrücken sowie in den Eigenschaftsausdrücken, die zum Aktualisieren von Eigenschaftswerten verwendet werden.  
  
 So können Sie z. B. eine benutzerdefinierte Variable in der Auswertungsbedingung für den For-Schleifen-Container verwenden. Sie können auch den Enumeratorauflistungswert in einem Foreach-Schleifen-Container einer Variablen zuordnen, und wenn ein Task "SQL ausführen" eine parametrisierte SQL-Anweisung verwendet, können Sie die Parameter für die Anweisung Variablen zuordnen. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](integration-services-ssis-variables.md).  
  
## <a name="variables-usage-scenarios"></a>Verwendungsszenarien für Variablen  
 Variablen werden auf verschiedene Weisen in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paketen verwendet. Sie werden möglicherweise der Meinung sein, dass die Paketentwicklung nicht voranschreitet, bis Sie die benutzerdefinierten Variablen einem Paket hinzugefügt haben, um die benötigte Flexibilität und Verwaltbarkeit der Lösung zu implementieren. Abhängig von dem Szenario, werden die Systemvariablen gemeinsam verwendet.  
  
 **Eigenschafts Ausdrücke** Verwenden Sie Variablen, um Werte in den Eigenschafts Ausdrücken anzugeben, mit denen die Eigenschaften von Paketen und Paket Objekten festgelegt werden. Beispielsweise schließt der Ausdruck `SELECT * FROM @varTableName` die `varTableName` -Variable ein, die die SQL-Anweisung aktualisiert, die der Task SQL ausführen ausführt. Der `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`-Ausdruck aktualisiert das Paket, das der Task Paket ausführen ausführt. Dies erfolgt durch Ausführen des angegebenen Pakets in der `varPackageFirst` -Variablen am ersten Tag des Monats, und das angegebene Paket in der `varPackageOther` -Variable wird an anderen Tagen ausgeführt. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](expressions/use-property-expressions-in-packages.md).  
  
 **Datenfluss Ausdrücke** Verwenden Sie Variablen, um Werte in den Ausdrücken bereitzustellen, die von den Transformationen für abgeleitete Spalten und bedingtes Teilen zum Auffüllen von Spalten verwendet werden, oder um Daten Zeilen an verschiedene Transformations Ausgaben weiterzuleiten. Beispielsweise verkettet der `@varSalutation + LastName`-Ausdruck den Wert in der `VarSalutation` -Variablen und der `LastName` -Spalte. Der `Income < @HighIncome`-Ausdruck leitet Datenzeilen, in denen der Wert der `Income` -Spalte niedriger ist als der Wert in der `HighIncome` -Variablen an eine Ausgabe weiter. Weitere Informationen finden Sie unter [Transformation für abgeleitete Spalten](data-flow/transformations/derived-column-transformation.md), [Transformation für bedingtes Teilen](data-flow/transformations/conditional-split-transformation.md) und [Integration Services-Ausdrücke &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 **Ausdrücke** für Rang folgen Einschränkungen Geben Sie Werte für Rang folgen Einschränkungen an, um zu bestimmen, ob eine eingeschränkte ausführbare Datei ausgeführt wird. Die Ausdrücke können entweder gemeinsam mit einem Ausführungsergebnis (Erfolg, Fehler, Beendigung) oder stattdessen mit einem Ausführungsergebnis verwendet werden. Wenn der Ausdruck `@varMax > @varMin` beispielsweise `true` auswertet, werden die ausführbaren Dateien ausgeführt. Weitere Informationen finden Sie unter [Hinzufügen von Ausdrücken zu Rangfolgeneinschränkungen](control-flow/precedence-constraints.md).  
  
 **Parameter und Rückgabe Codes** Geben Sie Werte für Eingabeparameter an, oder speichern Sie die Werte von Ausgabeparametern und Rückgabecodes. Dies erfolgt durch Zuordnen der Variablen zu Parametern und Rückgabewerten. Wenn sie beispielsweise die `varProductId` -Variable auf 23 festlegen und die `SELECT * from Production.Product WHERE ProductID = ?`-SQL-Anweisung ausführen, ruft die Abfrage das Produkt mit einer `ProductID` von 23 ab. Weitere Informationen finden Sie unter [SQL ausführen (Task)](control-flow/execute-sql-task.md) und [Parameter und Rückgabecodes im Task „SQL ausführen“](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
 **For-Schleifen Ausdrücke** Geben Sie Werte an, die für die Initialisierungs-, Auswertungs-und Zuweisungs Ausdrücke der for-Schleife verwendet werden sollen. Wenn der Wert für die `varCount` -Variable beispielsweise 2 und der Wert für `varMaxCount` 10, der Initialisierungsausdruck `@varCount`, der Auswertungsausdruck  `@varCount < @varMaxCount`und der Zuordnungsausdruck `@varCount =@varCount +1`lautet, dann wiederholt sich die Schleife acht Mal. Weitere Informationen finden Sie unter [For-Schleifencontainer](control-flow/for-loop-container.md)ausgewertet wird.  
  
 **Variablen Konfigurationen für übergeordnete Pakete** Übergibt Werte von übergeordneten Paketen an untergeordnete Pakete. Untergeordnete Pakete können auf Variablen in übergeordneten Paketen mithilfe der Variablenkonfiguration für übergeordnete Pakete zugreifen. Wenn beispielsweise ein untergeordnetes Paket die gleichen Daten wie das übergeordnete Paket verwenden muss, kann das untergeordnete Paket eine Variablenkonfiguration definieren, die eine Variable angibt, die durch die GETDATE-Funktion in dem übergeordneten Paket festgelegt wurde. Weitere Informationen finden Sie unter [Execute Package Task](control-flow/execute-package-task.md) und [Package Configurations](../../2014/integration-services/package-configurations.md).  
  
 **Skript Task und Skript Komponente** Geben Sie eine Liste von schreibgeschützten und Lese-/Schreib-Variablen für den Skript Task oder die Skript Komponente an, aktualisieren Sie die Lese-/Schreib-Variablen innerhalb des Skripts, und verwenden Sie dann die aktualisierten Werte in oder außerhalb des Skripts. Beispielsweise im `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`-Code wird die `numberOfCars` -Skriptvariable durch den Wert in der `NumberOfCars`-Variable aktualisiert. Weitere Informationen finden Sie unter [Using Variables in the Script Task](control-flow/script-task.md).  
  
## <a name="configurations-and-variables"></a>Konfigurationen und Variablen  
 Zum dynamischen Aktualisieren von Variablen können Sie Konfigurationen für die Variablen erstellen, die Konfigurationen zusammen mit dem Paket bereitstellen und dann die Variablenwerte in der Konfigurationsdatei aktualisieren, wenn Sie die Pakete bereitstellen. Zur Laufzeit verwendet das Paket die aktualisierten Variablenwerte. Weitere Informationen finden Sie unter [Erstellen von Paketkonfigurationen](../../2014/integration-services/create-package-configurations.md).  
  
### <a name="to-add-modify-and-delete-user-defined-variables"></a>So fügen Sie benutzerdefinierte Variablen hinzu und ändern oder löschen diese  
  
-   [Hinzufügen, Löschen, Ändern des Bereichs von benutzerdefinierten Variablen in einem Paket](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
-   [Festlegen der Eigenschaften von benutzerdefinierten Variablen](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
  
