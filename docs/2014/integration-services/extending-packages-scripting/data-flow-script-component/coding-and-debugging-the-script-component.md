---
title: Programmieren und Debuggen der Skriptkomponente | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d12dbcdf49fc34bdd37fca21635cbcd416efc36b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176226"
---
# <a name="coding-and-debugging-the-script-component"></a>Codieren und Debuggen der Skriptkomponente
  Im [!INCLUDE[ssIS](../../../includes/ssis-md.md)]-Designer weist die Skriptkomponente zwei Modi auf: Metadatenentwurfsmodus und Codeentwurfsmodus. Wenn Sie den **Transformations-Editor für Skripterstellung** öffnen, befindet sich die Komponente im Metadatenentwurfsmodus, in dem Metadaten konfiguriert und Komponenteneigenschaften festgelegt werden. Nachdem Sie die Eigenschaften der Skriptkomponente festgelegt und die Eingaben und Ausgaben im Metadatenentwurfsmodus konfiguriert haben, können Sie zum Schreiben des benutzerdefinierten Skripts in den Codeentwurfsmodus wechseln. Weitere Informationen zum Metadatenentwurfsmodus und zum Codeentwurfsmodus finden Sie unter [Configuring the Script Component in the Script Component Editor (Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor)](configuring-the-script-component-in-the-script-component-editor.md).

## <a name="writing-the-script-in-code-design-mode"></a>Schreiben des Skripts im Codeentwurfsmodus

### <a name="script-component-development-environment"></a>Skriptkomponenten-Entwicklungsumgebung
 Klicken Sie zum Schreiben des Skripts im **Transformations-Editor für Skripterstellung** auf der Seite **Skript** auf **Skript bearbeiten**, um die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications-IDE (VSTA) zu öffnen. Die VSTA IDE enthält alle Standardfunktionen der [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET-Umgebung wie den [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]-Editor mit Farbcodierung, IntelliSense und den Objektkatalog.

 Skriptcode wird in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# geschrieben. Sie geben die Skriptsprache an, indem Sie die **ScriptLanguage**-Eigenschaft im **Transformations-Editor für Skripterstellung** festlegen. Falls Sie lieber eine andere Programmiersprache verwenden möchten, können Sie in Ihrer bevorzugten Sprache eine benutzerdefinierte Assembly entwickeln und ihre Funktionen aus dem Code in der Skriptkomponente aufrufen.

 Das in der Skriptkomponente erstellte Skript wird in der Paketdefinition gespeichert. Es gibt keine separate Skriptdatei. Deshalb hat die Verwendung der Skriptkomponente keinen Einfluss auf die Paketbereitstellung.

> [!NOTE]
>  Beim Entwurf des Pakets wird der Skriptcode vorübergehend in eine Projektdatei geschrieben. Da das Speichern vertraulicher Informationen in einer Datei ein Sicherheitsrisiko darstellt, sollte der Skriptcode keine vertraulichen Daten wie Kennwörter enthalten.

 Standardmäßig ist `Option Strict` in der IDE deaktiviert.

### <a name="script-component-project-structure"></a>Skriptkomponenten-Projektstruktur
 Die Leistungsfähigkeit der Skriptkomponente rührt daher, dass Infrastrukturcode erstellt werden kann, mit dem der erforderliche Codeumfang reduziert werden kann. Für diese Funktion ist es erforderlich, dass Eingaben und Ausgaben mit den zugehörigen Spalten und Eigenschaften festgelegt und im Voraus bekannt sind. Aus diesem Grund können nachträgliche Änderungen an den Metadaten der Komponente dazu führen, dass der von Ihnen geschriebene Code ungültig wird. Dies verursacht während der Ausführung des Pakets Kompilierungsfehler.

#### <a name="project-items-and-classes-in-the-script-component-project"></a>Projektelemente und -klassen im Skriptkomponentenprojekt
 Wenn Sie in den Codeentwurfsmodus wechseln, wird die VSTA IDE geöffnet und zeigt das `ScriptMain`-Projektelement an. Das `ScriptMain`-Projektelement enthält die bearbeitbare `ScriptMain`-Klasse, die als Einstiegspunkt für das Skript dient und in die der Code geschrieben wird. Die Codeelemente in der Klasse variieren abhängig davon, welche Programmiersprache Sie für den Skripttask gewählt haben.

 Das Skriptprojekt enthält zwei zusätzliche, automatisch generierte und schreibgeschützte Projektelemente:

-   Das `ComponentWrapper`-Projektelement enthält drei Klassen:

    -   Die `UserComponent`-Klasse, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> erbt und die Methoden und Eigenschaften enthält, die Sie verwenden, um Daten zu verarbeiten und mit dem Paket zu interagieren. Die `ScriptMain`-Klasse erbt von der `UserComponent`-Klasse.

    -   Eine `Connections`-Auflistungsklasse mit Verweisen zu den im Transformations-Editor für Skripterstellung auf der Seite Verbindungs-Manager ausgewählten Verbindungen.

    -   Eine `Variables` Auflistungs Klasse, die Verweise auf die Variablen enthält `ReadOnlyVariable` , `ReadWriteVariables` die auf der Seite **Skript** des Transformations- **Editors für Skript**Erstellung in den Eigenschaften und eingegeben wurden.

-   Das `BufferWrapper` -Projekt Element enthält eine Klasse, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> für jede auf der Seite **Eingaben und Ausgaben** des **Transformations-Editors für Skript**Erstellung konfigurierte Eingabe und Ausgabe erbt. Jede dieser Klassen enthält typisierte Accessoreigenschaften, die mit den konfigurierten Eingabe- und Ausgabespalten übereinstimmen, sowie die Datenflusspuffer, in denen sich diese Spalten befinden.

 Weitere Informationen zur Verwendung dieser Objekte, Methoden und Eigenschaften finden Sie unter [Understanding the Script Component Object Model (Grundlegendes zum Objektmodell der Skriptkomponente)](understanding-the-script-component-object-model.md). Informationen darüber, wie die Methoden und Eigenschaften dieser Klassen in einem bestimmten Skriptkomponententyp zu verwenden sind, finden Sie unter [Additional Script Component Examples (Zusätzliche Skriptkomponentenbeispiele)](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Die Beispielthemen enthalten auch vollständige Codebeispiele.

 Bei der Konfiguration der Skriptkomponente als Transformation enthält das `ScriptMain`-Projektelement den folgenden automatisch generierten Code. Die Codevorlage bietet auch eine Übersicht über die Skriptkomponente und zusätzliche Informationen über das Abrufen und Bearbeiten von SSIS-Objekten, z. B. Variablen, Ereignisse und Verbindungen.

```vb
' Microsoft SQL Server Integration Services Script Component
' Write scripts using Microsoft Visual Basic 2008.
' ScriptMain is the entry point class of the script.

Imports System
Imports System.Data
Imports System.Math
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper

<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _
<CLSCompliant(False)> _
Public Class ScriptMain
    Inherits UserComponent

    Public Overrides Sub PreExecute()
        MyBase.PreExecute()
        '
        ' Add your code here for preprocessing or remove if not needed
        '
    End Sub

    Public Overrides Sub PostExecute()
        MyBase.PostExecute()
        '
        ' Add your code here for postprocessing or remove if not needed
        ' You can set read/write variables here, for example:
        ' Me.Variables.MyIntVar = 100
        '
    End Sub

    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)
        '
        ' Add your code here
        '
    End Sub

End Class
```

```csharp
/* Microsoft SQL Server Integration Services user script component
*  Write scripts using Microsoft Visual C# 2008.
*  ScriptMain is the entry point class of the script.*/

using System;
using System.Data;
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;
using Microsoft.SqlServer.Dts.Runtime.Wrapper;

[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]
public class ScriptMain : UserComponent
{

    public override void PreExecute()
    {
        base.PreExecute();
        /*
          Add your code here for preprocessing or remove if not needed
        */
    }

    public override void PostExecute()
    {
        base.PostExecute();
        /*
          Add your code here for postprocessing or remove if not needed
          You can set read/write variables here, for example:
          Variables.MyIntVar = 100
        */
    }

    public override void Input0_ProcessInputRow(Input0Buffer Row)
    {
        /*
          Add your code here
        */
    }

}
```

#### <a name="additional-project-items-in-the-script-component-project"></a>Zusätzliche Projektelemente im Skriptkomponentenprojekt
 Das Skriptkomponentenprojekt kann neben dem Standardelement `ScriptMain` noch weitere Elemente enthalten. Sie können dem Projekt Klassen, Module, Codedateien und Ordner hinzufügen und die Ordner zum Organisieren von Elementgruppen verwenden.

 Alle Elemente, die Sie hinzufügen, werden im Paket beibehalten.

#### <a name="references-in-the-script-component-project"></a>Verweise im Skriptkomponentenprojekt
 Sie können Verweise auf verwaltete Assemblys hinzufügen, indem Sie im **Projektexplorer** mit der rechten Maustaste auf das Skripttaskprojekt und anschließend auf **Verweis hinzufügen** klicken. Weitere Informationen finden Sie unter [Verweisen auf andere Assemblys in Skriptlösungen](../referencing-other-assemblies-in-scripting-solutions.md).

> [!NOTE]
>  Sie können Projektverweise in der VSTA-IDE in der **Klassenansicht** oder im **Projektexplorer** anzeigen. Diese Fenster öffnen Sie über das Menü **Ansicht**. Einen neuen Verweis können Sie über das Menü **Projekt**, den **Projektexplorer** oder die **Klassenansicht** hinzufügen.

## <a name="interacting-with-the-package-in-the-script-component"></a>Interagieren mit Paketen in der Skriptkomponente
 Das benutzerdefinierte Skript, das in der Skriptkomponente geschrieben wird, kann mithilfe von stark typisierten  Accessoren in automatisch generierten Basisklassen auf Variablen und Verbindungs-Manager aus dem entsprechenden Paket zugreifen und diese verwenden. Die Variablen und Verbindungs-Manager müssen vor dem Wechseln in den Codeentwurfsmodus konfiguriert werden, wenn sie für das Skript zur Verfügung stehen sollen. Sie können auch Ereignisse auslösen und die Protokollierung von Ihrem Skriptkomponentencode ausführen.

 Die automatisch generierten Projektelemente im Skriptkomponentenprojekt stellen die folgenden Objekte, Methoden und Eigenschaften zum Interagieren mit dem Paket bereit.

|Funktion des Pakets|Zugriffsmethode|
|---------------------|-------------------|
|Variables|Verwenden Sie die benannten, typisierten Accessoreigenschaften in der `Variables`-Auflistungsklasse im `ComponentWrapper`-Projektelement, die über die `Variables`-Eigenschaft der `ScriptMain`-Klasse bereitgestellt werden.<br /><br /> Die `PreExecute`-Methode kann nur auf schreibgeschützte Variablen zugreifen. Die `PostExecute`-Methode kann sowohl auf schreibgeschützte als auch auf Lese-/Schreibvariablen zugreifen.|
|Verbindungen|Verwenden Sie die benannten, typisierten Accessoreigenschaften in der `Connections`-Auflistungsklasse im `ComponentWrapper`-Projektelement, die über die `Connections`-Eigenschaft der `ScriptMain`-Klasse bereitgestellt werden.|
|Events|Lösen Sie Ereignisse mithilfe der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> -Eigenschaft der `ScriptMain` -Klasse und **der\<Fire X>** -Methoden <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> der-Schnittstelle aus.|
|Protokollierung|Protokollierungen werden mit der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>-Methode der `ScriptMain`-Klasse ausgeführt.|

## <a name="debugging-the-script-component"></a>Debuggen der Skriptkomponente
 Legen Sie zum Debuggen des Codes in der Skriptkomponente mindestens einen Breakpoint fest, und schließen Sie dann die VSTA IDE, um das Paket in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] auszuführen. Wenn die Ausführung der Skriptkomponente beginnt, wird die VSTA IDE erneut geöffnet und der Code schreibgeschützt angezeigt. Nachdem die Ausführung den Breakpoint erreicht hat, können Sie die Variablenwerte untersuchen und den übrigen Code schrittweise durchgehen.

> [!NOTE]
>  Sie können eine Skriptkomponente nicht debuggen, wenn sie als Teil eines untergeordneten Pakets in einem Task Paket ausführen ausgeführt wird. Breakpoints, die Sie in der Skriptkomponente im untergeordneten Paket festlegen, werden unter diesen Umständen ignoriert. Sie können das untergeordnete Paket normalerweise debuggen, indem Sie es getrennt ausführen.

> [!NOTE]
>  Wenn Sie ein Paket debuggen, das mehrere Skriptkomponenten enthält, debuggt der Debugger eine Skriptkomponente. Das System kann eine andere Skriptkomponente debuggen, wenn der Debugger wie im Fall eines Foreach- oder For-Schleifencontainers abgeschlossen wird.

 Sie können die Ausführung der Skriptkomponente auch mit den folgenden Methoden überwachen:

-   Unterbrechen Sie die Ausführung, und zeigen Sie mithilfe `MessageBox.Show` der-Methode im **System. Windows. Forms** -Namespace eine modale Meldung an. (Entfernen Sie diesen Code, nachdem der Debugprozess abgeschlossen wurde.)

-   Lösen Sie Ereignisse für Informationsmeldungen, Warnungen und Fehler aus. Die Methoden FireInformation, FireWarning und FireError zeigen die Ereignisbeschreibung im Fenster **Ausgabe** von Visual Studio an. Die Methoden FireProgress, Console.Write und Console.WriteLine zeigen hingegen keine Informationen im Fenster **Ausgabe** an. Meldungen des FireProgress-Ereignisses werden auf der Registerkarte **Status** des [!INCLUDE[ssIS](../../../includes/ssis-md.md)]-Designers angezeigt. Weitere Informationen finden Sie unter [Raising Events in the Script Component (Auslösen von Ereignissen in der Skriptkomponente)](../../data-flow/transformations/script-component.md).

-   Protokollieren Sie Ereignisse oder benutzerdefinierte Meldungen an aktivierte Protokollanbieter. Weitere Informationen finden Sie unter [Logging in the Script Component (Protokollieren in der Skriptkomponente)](logging-in-the-script-component.md).

 Wenn Sie lediglich die Ausgabe einer Skriptkomponente überprüfen möchten, die als Quelle oder Transformation konfiguriert ist, und die Daten nicht in einem Ziel speichern möchten, können Sie den Datenfluss mit einer [Transformation für Zeilenanzahl](../../data-flow/transformations/row-count-transformation.md) unterbrechen und der Ausgabe der Skriptkomponente einen Daten-Viewer anfügen. Informationen zu Daten-Viewern finden Sie unter [Debugging Data Flow (Debuggen des Datenflusses)](../../troubleshooting/debugging-data-flow.md).

## <a name="in-this-section"></a>In diesem Abschnitt
 Weitere Informationen zum Codieren der Skriptkomponente finden Sie in den folgenden Themen in diesem Abschnitt.

 Grundlegendes [zum Skript Component Object Model](understanding-the-script-component-object-model.md) Erläutert, wie die in der Skript Komponente verfügbaren Objekte, Methoden und Eigenschaften verwendet werden.

 [Verweisen auf andere Assemblys in Skript Lösungen](../referencing-other-assemblies-in-scripting-solutions.md) Erläutert, wie auf-Objekte aus [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] der-Klassenbibliothek in der Skript Komponente verwiesen wird.

 [Simulieren einer Fehlerausgabe für die Skript Komponente](../../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md) Erläutert das Simulieren einer Fehlerausgabe für Zeilen, die während der Verarbeitung von der Skript Komponente Fehler ausgeben.

## <a name="external-resources"></a>Externe Ressourcen

-   Blogeintrag: [VSTA setup and configuration troubles for SSIS 2008 and R2 installations (Probleme mit der VSTA-Einrichtung und -Konfiguration bei SSIS 2008- und R2-Installationen)](https://go.microsoft.com/fwlink/?LinkId=215661) (auf blogs.msdn.com).

![Integration Services Symbol (klein)](../../media/dts-16.gif "Integration Services (kleines Symbol)")immer auf**dem neuesten Stand bleiben mit Integration Services**  <br /> Die neuesten Downloads, Artikel, Beispiele und Videos von Microsoft sowie ausgewählte Lösungen aus der Community finden Sie auf MSDN auf der [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Seite:<br /><br /> [Besuchen Sie die Integration Services-Seite auf MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Abonnieren Sie die auf der Seite verfügbaren RSS-Feeds, um automatische Benachrichtigungen zu diesen Updates zu erhalten.

## <a name="see-also"></a>Weitere Informationen
 [Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor](configuring-the-script-component-in-the-script-component-editor.md)


