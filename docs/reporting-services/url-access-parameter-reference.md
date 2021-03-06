---
title: Referenz für URL-Zugriffsparameter | Microsoft-Dokumentation
description: Verwenden Sie die Parameter in diesem Artikel in einer URL, um die Darstellung und das Verhalten Ihrer Reporting Services-Berichte zu konfigurieren.
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ac67de4831d1785f17029bc6c68fa6f7d8aeb16
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2020
ms.locfileid: "77147383"
---
# <a name="url-access-parameter-reference"></a>Referenz für URL-Zugriffsparameter

  Sie können die folgenden Parameter als Teil einer URL verwenden, um die Darstellung und das Verhalten Ihrer [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]-Berichte zu konfigurieren. In diesem Abschnitt sind die am häufigsten verwendeten Parameter aufgeführt. Bei Parametern muss keine Groß- und Kleinschreibung beachtet werden. Sie beginnen mit dem Präfix *rs:* , wenn sie an den Berichtsserver weitergeleitet werden, und mit *rs:* , wenn sie zu einem HTML-Viewer weitergeleitet werden. Sie können außerdem Parameter angeben, die für Geräte oder Renderingerweiterungen spezifisch sind. Weitere Informationen zu gerätespezifischen Parametern finden Sie unter [Angeben von Geräteinformationseinstellungen in einer URL](../reporting-services/specify-device-information-settings-in-a-url.md).
  
> [!IMPORTANT]  
>  Für einen Berichtsserver im SharePoint-Modus ist es wichtig, dass die URL die `_vti_bin`-Proxysyntax zur Weiterleitung der Anforderung über SharePoint sowie den [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-HTTP-Proxy enthält. Durch den Proxy wird der HTTP-Anforderung Kontext hinzugefügt, der erforderlich ist, damit der Bericht auf Berichtsservern im SharePoint-Modus ordnungsgemäß ausgeführt wird. Beispiele finden Sie unter [Zugreifen auf Berichtsserverelemente über den URL-Zugriff](../reporting-services/access-report-server-items-using-url-access.md).
> 
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.
  

##  <a name="bkmk_htmlviewer"></a> Befehle des HTML-Viewers (rc:)
 - HTML-Viewer-Befehle werden verwendet, um den HTML-Viewer auszuwählen, und sind mit dem Präfix *rc:* versehen:
  
-   **Toolbar**: Zeigt die Symbolleiste an oder blendet sie aus. Wenn der Wert dieses Parameters **FALSE**ist, werden alle verbleibenden Optionen ignoriert. Wenn Sie diesen Parameter weglassen, wird die Symbolleiste automatisch für Renderingformate angezeigt, die sie unterstützen. Der Standardwert dieses Parameters ist **true**.
  
    > [!IMPORTANT]  
    >  *rc:Toolbar*=**false** funktioniert nicht für URL-Zugriffszeichenfolgen, die eine IP-Adresse anstelle eines Domänennamens verwenden, um einen auf einer SharePoint-Website gehosteten Bericht anzuzielen.
  
-   **Parameter**: Zeigt den Parameterbereich der Symbolleiste an oder blendet ihn aus. Wenn Sie diesen Parameter auf **TRUE**festlegen, wird der Parameterbereich der Symbolleiste angezeigt. Wenn Sie diesen Parameter auf **false** festlegen, wird der Parameterbereich nicht angezeigt und kann auch nicht vom Benutzer angezeigt werden. Wenn Sie diesen Parameter auf den Wert **Collapsed** festlegen, wird der Parameterbereich nicht angezeigt, kann aber vom Endbenutzer ein- oder ausgeschaltet werden. Der Standardwert dieses Parameters ist **true**.  
  
     Beispiel im einheitlichen Modus:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Parameters=Collapsed  
    ```  
  
     Beispiel im SharePoint-Modus:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Parameters=Collapsed  
    ```  
  
-   **Zoom**: Legt den Zoomfaktor für den Bericht als ganzzahligen Prozentsatz oder Zeichenfolgenkonstante fest. Standardwerte für die Zeichenfolge sind **Page Width** und **Whole Page**. Dieser Parameter wird von Internet Explorer-Versionen vor Internet Explorer 5.0 sowie allen nicht von[!INCLUDE[msCoName](../includes/msconame-md.md)] bereitgestellten Browsern ignoriert. Der Standardwert dieses Parameters ist **100**.
  
     Beispiel im einheitlichen Modus:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Zoom=Page Width  
    ```  
  
     Beispiel im SharePoint-Modus:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Zoom=Page Width  
    ```  
  
-   **Section**: Legt fest, welche Seite im Bericht angezeigt werden soll. Bei Eingabe eines Werts, der über der Gesamtzahl der Seiten im Bericht liegt, wird die letzte Seite angezeigt. Bei jedem Wert unter **0** (null) wird Seite 1 des Berichts angezeigt. Der Standardwert dieses Parameters ist **1**.
  
     Beispiel zum Anzeigen von Berichtsseite 2 im einheitlichen Modus:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Section=2  
    ```  
  
     Beispiel zum Anzeigen von Berichtsseite 2 im SharePoint-Modus:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Section=2  
    ```  
  
-   **FindString**: Durchsuchen eines Berichts nach einem bestimmten Textteil.
  
     Beispiel im einheitlichen Modus:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:FindString=Mountain-400  
    ```  
  
     Beispiel im SharePoint-Modus:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:FindString=Mountain-400  
    ```  
  
-   **StartFind**: Legt den letzten Abschnitt für die Suche fest. Der Standardwert dieses Parameters ist die letzte Seite des Berichts.  
  
     Beispiel im einheitlichen Modus, in dem nach dem ersten Vorkommen des Texts „Mountain-400“ im Beispielbericht „Product Catalog“ gesucht wird. Die Suche beginnt auf Seite 1 und endet auf Seite 5:
  
    ```  
    https://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
    ```  
  
-   **EndFind**: Legt die Seitenzahl der letzten Seite für die Suche fest. Beispiel: Der Wert **5** gibt an, dass Seite 5 des Berichts die letzte zu durchsuchende Seite ist. Der Standardwert ist die Seitenzahl der aktuellen Seite. Verwenden Sie diesen Parameter in Verbindung mit dem *StartFind* -Parameter. Sehen Sie sich dazu das vorherige Beispiel an.
  
-   **FallbackPage**: Legt die Seitenzahl der Seite fest, die bei einer fehlgeschlagenen Suche oder Dokumentstrukturauswahl angezeigt wird. Der Standardwert ist die Seitenzahl der aktuellen Seite.
  
-   **GetImage**: Ruft ein bestimmtes Symbol für die Benutzeroberfläche des HTML-Viewers ab.
  
-   **Icon**: Ruft ein Symbol einer bestimmten Renderingerweiterung ab.
  
-   **Stylesheet**: Legt ein Stylesheet fest, das auf den HTML-Viewer angewendet wird.
  
-   **Geräteinformationseinstellungen:** Hiermit wird eine Geräteinformationseinstellung im Format `rc:tag=value` festgelegt, wobei *tag* dem Namen einer für die gerade verwendete Renderingerweiterung spezifischen Geräteinformationseinstellung entspricht. (Informationen finden Sie in der Beschreibung des Parameters *Format*.) Sie können z. B. die Geräteinformationseinstellung *OutputFormat* für die IMAGE-Renderingerweiterung verwenden, um den Bericht mithilfe der folgenden Parameter in der URL-Zugriffszeichenfolge in ein JPEG-Bild zu rendern: `...&rs:Format=IMAGE&rc:OutputFormat=JPEG`. Weitere Informationen zu allen erweiterungsspezifischen Geräteinformationseinstellungen finden Sie im Artikel [Geräteinformationseinstellungen für Renderingerweiterungen &#40;Reporting Services&#41;](../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md).
  
##  <a name="bkmk_reportserver"></a> Befehle des Berichtsservers (rs:)
 Befehle des Berichtsservers werden mit dem Präfix *rs:* versehen und zum Auswählen des Berichtsservers verwendet:
  
-   **Befehl**: Führt eine Aktion auf einem Katalogelement aus. Dies ist abhängig von dessen Elementtyp. Der Standardwert wird vom Typ des Katalogelements bestimmt, auf den in der URL-Zugriffszeichenfolge verwiesen wird. Gültige Werte sind:
  
    -   **ListChildren** und **GetChildren**: Zeigt den Inhalt eines Ordners an. Die Ordnerelemente werden in einer generischen Seite zur Elementnavigation angezeigt.
  
         Beispiel im einheitlichen Modus:
  
        ```  
        https://myrshost/reportserver?/Sales&rs:Command=GetChildren  
        ```  
  
         Beispiel einer benannten Instanz im einheitlichen Modus:
  
        ```  
        https://myssrshost/Reportserver_THESQLINSTANCE?/reportfolder&rs:Command=listChildren  
        ```  
  
         Beispiel im SharePoint-Modus:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rs:Command=GetChildren  
        ```  
  
    -   **Render**: Der Bericht wird im Browser gerendert, sodass Sie ihn anzeigen können.
  
         Beispiel im einheitlichen Modus:
  
        ```  
        https://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
         Beispiel im SharePoint-Modus:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
    -   **GetSharedDatasetDefinition**: Zeigt die einem freigegebenen Dataset zugeordnete XML-Definition an. Eigenschaften freigegebener Datasets, einschließlich der Abfrage, Datasetparameter, Standardwerte, Datasetfilter und Datenoptionen z. B. zur Sortierung und Berücksichtigung der Groß-/Kleinschreibung, werden in der Definition gespeichert. Sie müssen zum **Lesen von Berichtsdefinitionen** eines freigegebenen Datasets berechtigt sein, um diesen Wert verwenden zu können.
  
         Beispiel im einheitlichen Modus:
  
        ```  
        https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
        ```  
  
    -   **GetDataSourceContents**: Zeigt die Eigenschaften einer bestimmten freigegebenen Datenquelle als XML-Datei an. Wenn Ihr Browser XML unterstützt und Sie ein für die Datenquelle authentifizierter Benutzer mit der Berechtigung **Read Contents** (Inhalte lesen) sind, wird die Datenquellendefinition angezeigt.
  
         Beispiel im einheitlichen Modus:
  
        ```  
        https://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
         Beispiel im SharePoint-Modus:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
    -   **GetResourceContents**: Rendert eine Ressource und zeigt sie auf einer HTML-Seite an, wenn die Ressource mit dem Browser kompatibel ist. Andernfalls werden Sie aufgefordert, die Datei oder Ressource zu öffnen oder auf dem Datenträger zu speichern.  
  
         Beispiel im einheitlichen Modus:
  
        ```  
        https://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents  
        ```  
  
         Beispiel im SharePoint-Modus:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents  
        ```  
  
    -   **GetComponentDefinition**: Zeigt die einem veröffentlichten Berichtselement zugeordnete XML-Definition an. Sie müssen zum **Lesen von Inhalten** eines veröffentlichten Berichtselements berechtigt sein, um diesen Wert verwenden zu können.
  
-   **Format**: Legt das Format fest, in dem der Bericht gerendert und angezeigt wird. Häufig verwendete Werte sind:
  
    -   **HTML5**  
  
    -   **PPTX**  
  
    -   **ATOM**  
  
    -   **HTML4.0**  
  
    -   **MHTML**  
  
    -   **IMAGE**  
  
    -   **EXCEL** (für XLX-Dateien)
    
    -   **EXCELOPENXML** (für .xlsx)
  
    -   **WORD** (für .doc)
    
    -   **WORDOPENXML** (für .docx)
  
    -   **CSV**  
  
    -   **PDF**  
  
    -   **XML**  
  
     Der Standardwert ist **HTML5**. Weitere Informationen finden Sie unter [Exportieren von Berichten über URL-Zugriff](../reporting-services/export-a-report-using-url-access.md).
  
     Eine vollständige Liste finden Sie im Abschnitt **\<Render>** -Erweiterung der Datei „rsreportserver.config“ auf dem Berichtsserver. Weitere Informationen zum Auffinden der Datei finden Sie unter [RSReportServer.config-Konfigurationsdatei](../reporting-services/report-server/rsreportserver-config-configuration-file.md).
  
     Um beispielsweise von einem im einheitlichen Modus ausgeführten Berichtsserver direkt eine PDF-Kopie eines Berichts abzurufen, geben Sie Folgendes an:
  
    ```  
    https://myrshost/ReportServer?/myreport&rs:Format=PDF  
    ```  
  
     Beispiel, um eine PDF-Kopie eines Berichts direkt von einem Berichtsserver im SharePoint-Modus abzurufen:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
    ```  
  
-   **ParameterLanguage**: Bietet eine Sprache für in einer URL übergebene Parameter, die von der Browsersprache unabhängig ist. Der Standardwert ist die Browsersprache. Der Wert kann ein Kulturwert sein, z.B. **en-us** oder **de-de**.
  
     Beispiel im einheitlichen Modus, in dem die Browsersprache überschrieben und der Kulturwert „de-DE“ angegeben wird:
  
    ```  
    https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
    ```  
  
-   **Momentaufnahme**: Rendert einen Bericht anhand einer Berichtsverlaufs-Momentaufnahme. Weitere Informationen finden Sie unter [Rendern von Berichtsverlaufs-Momentaufnahmen mit URL-Zugriff](../reporting-services/render-a-report-history-snapshot-using-url-access.md).
  
     Beispiel im einheitlichen Modus, um eine Berichtsverlaufs-Momentaufnahme vom 7.4.2003 mit dem Zeitstempel 13:40:02 abzurufen:
  
    ```  
    https://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
    ```  
  
-   **PersistStreams**: Rendert einen Bericht in einem einzelnen permanenten Datenstrom. Dieser Parameter wird vom Bildrenderer verwendet, um den gerenderten Bericht segmentweise zu senden. Nachdem Sie diesen Parameter in einer URL-Zugriffszeichenfolge verwendet haben, verwenden Sie diese URL-Zugriffszeichenfolge mit dem *GetNextStream* -Parameter anstelle des *PersistStreams* -Parameters, um das nächste Segment im permanenten Datenstrom abzurufen. Dieser URL-Befehl gibt schließlich einen 0-Byte-Datenstrom zurück, um das Ende des permanenten Datenstroms anzugeben. Der Standardwert ist **false**.
  
-   **GetNextStream**: Ruft das nächste Datensegment in einem permanenten Datenstrom ab, auf den mit dem *PersistStreams*-Parameter zugegriffen wird. Weitere Informationen finden Sie in der Beschreibung für *PersistStreams*. Der Standardwert ist **false**.
  
-   **SessionID**: Gibt eine feststehende aktive Berichtssitzung zwischen der Clientanwendung und dem Berichtsserver an. Der Wert dieses Parameters wird auf die Sitzungs-ID festgelegt.
  
     Sie können die Sitzungs-ID als Cookie oder als Teil der URL angeben. Wenn der Berichtsserver nicht für die Verwendung von Cookies konfiguriert wurde, führt die erste Anforderung ohne eine bestimmte Sitzungs-ID zu einer Umleitung mit einer Sitzungs-ID. Weitere Informationen finden Sie unter [Identifizieren des Ausführungsstatus](../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md).
  
-   **ClearSession**: Ein **TRUE** -Wert weist den Berichtsserver an, einen Bericht aus der Berichtssitzung zu löschen. Alle zu einem authentifizierten Benutzer gehörigen Berichtsinstanzen werden aus der Berichtssitzung entfernt. (Eine Berichtsinstanz wird als derselbe Bericht definiert, der mehrmals mit unterschiedlichen Berichtsparameterwerten ausgeführt wurde.) Der Standardwert ist **false**.
  
-   **ResetSession**: Ein **TRUE** -Wert weist den Berichtsserver an, die Berichtssitzung zurückzusetzen, indem die Zuordnung der Berichtssitzung zu allen Berichtsmomentaufnahmen entfernt wird. Der Standardwert ist **false**.
  
-   **ShowHideToggle**: Schaltet das Ein-/Ausblenden eines Abschnitts im Bericht um. Geben Sie eine positive ganze Zahl an, um den Abschnitt anzugeben, der umgeschaltet werden soll.
  
##  <a name="bkmk_webpart"></a> Befehle des Berichts-Viewer-Webparts (rv:)
 Die folgenden reservierten Berichtsparameternamen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] werden zum Auswählen des in SharePoint integrierten Berichts-Viewer-Webparts verwendet. Diese Parameternamen haben das Präfix *rv:* . Für Berichts-Viewer-Webparts kann auch der Parameter *rs:ParameterLanguage* verwendet werden.
  
-   **Toolbar**: Steuert die Symbolleistenanzeige des Bericht-Viewer-Webparts. Der Standardwert ist **Full**. Mögliche Werte:
  
    -   **Full:** Zeigt die vollständige Symbolleiste an.
  
    -   **Navigation**: Zeigt nur die Paginierung auf der Symbolleiste an.
  
    -   **Keine:** Die Symbolleiste wird nicht angezeigt.
  
     Beispiel im SharePoint-Modus, wenn nur die Paginierung auf der Symbolleiste angezeigt werden soll:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation  
    ```  
  
-   **HeaderArea**: Steuert die Anzeige der Kopfzeile des Bericht-Viewer-Webparts. Der Standardwert ist **Full**. Mögliche Werte:
  
    -   **Full:** Zeigt die vollständige Kopfzeile an.
  
    -   **BreadCrumbsOnly**: Zeigt nur einen Teil (Breadcrumb) der Navigation in der Kopfzeile an, um die Benutzer über ihre Position in der Anwendung zu informieren.
  
    -   **Keine:** Zeigt die Kopfzeile nicht an.
  
     Beispiel im SharePoint-Modus, wenn nur ein Teil (Breadcrumb) der Navigation in der Kopfzeile angezeigt werden soll:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly  
    ```  
  
-   **DocMapAreaWidth**: Steuert die Anzeigebreite (in Pixel) des Parameterbereichs im Bericht-Viewer-Webpart. Der Standardwert entspricht dem Standardwert des Bericht-Viewer-Webparts. Der Wert muss eine nicht negative ganze Zahl sein.
  
-   **AsyncRender**: Steuert, ob ein Bericht asynchron gerendert wird. Der Standardwert ist **TRUE**. Er gibt an, dass ein Bericht asynchron gerendert wird. Der Wert muss ein boolescher Wert **TRUE** oder **FALSE**sein.
  
-   **ParamMode**: Mit diesem Befehl wird gesteuert, wie der Eingabeaufforderungsbereich für Parameter des Berichts-Viewer-Webparts in der Ganzseitenansicht angezeigt wird. Der Standardwert ist **Full**. Gültige Werte sind:
  
    -   **Full:** Zeigt den Eingabeaufforderungsbereich für Parameter an.
  
    -   **Collapsed**: Reduziert den Eingabeaufforderungsbereich für Parameter.
  
    -   **Hidden**: Blendet den Eingabeaufforderungsbereich für Parameter aus.
  
     Beispiel im SharePoint-Modus, wenn der Eingabeaufforderungsbereich für Parameter reduziert werden soll:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed  
    ```  
  
-   **DocMapMode**: Mit diesem Befehl wird gesteuert, wie der Dokumentstrukturbereich des Berichts-Viewer-Webparts in der Ganzseitenansicht angezeigt wird. Der Standardwert ist **Full**. Gültige Werte sind:
  
    -   **Full:** Zeigt den Dokumentstrukturbereich an.
  
    -   **Collapsed**: Reduziert den Dokumentstrukturbereich.
  
    -   **Hidden**: Blendet den Dokumentstrukturbereich aus.
  
-   **DockToolBar**: Mit diesem Befehl wird gesteuert, ob die Symbolleiste des Berichts-Viewer-Webparts oben oder unten angedockt wird. Gültige Werte sind **Top** und **Bottom**. Der Standardwert ist **Top**.
  
     Beispiel im SharePoint-Modus, wenn die Symbolleiste unten angedockt werden soll:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom  
    ```  
  
-   **ToolBarItemsDisplayMode**: Steuert, welche Symbolleistenelemente angezeigt werden. Hierbei handelt es sich um einen bitweisen Enumerationswert. Um ein Symbolleistenelement einzuschließen, fügen Sie dem Gesamtwert den Wert des Elements hinzu. Verwenden Sie beispielsweise *rv:ToolBarItemsDisplayMode=63* (oder 0x3F), was 1 + 2 + 4 + 8 + 16 + 32 entspricht, um kein **Aktionen**-Menü anzuzeigen. Verwenden Sie *rv:ToolBarItemsDisplayMode=960* (oder 0x3C0), wenn nur Elemente des **Aktionen**-Menüs angezeigt werden sollen. Der Standardwert, der alle Symbolleistenelemente einschließt, ist **-1**. Gültige Werte sind:
  
    -   **1 (0x1)** : Die Schaltfläche **Zurück**  
  
    -   **2 (0x2)** : Die Steuerelemente für die Textsuche  
  
    -   **4 (0x4)** : Die Steuerelemente für die Seitennavigation  
  
    -   **8 (0x8)** : Die Schaltfläche **Aktualisieren**  
  
    -   **16 (0x10)** : Das Listenfeld **Zoom**  
  
    -   **32 (0x20)** : Die Schaltfläche **Atom-Feed**  
  
    -   **64 (0x40)** : Die Menüoption **Drucken** in **Aktionen**  
  
    -   **128 (0x80)** : Das Untermenü **Exportieren** in **Aktionen**  
  
    -   **256 (0x100)** : Die Menüoption **Mit dem Berichts-Generator öffnen** in **Aktionen**  
  
    -   **512 (0x200)** : Die Menüoption **Abonnieren** in **Aktionen**  
  
    -   **1024 (0x400)** : Die Menüoption **Neue Datenwarnung** in **Aktionen**  
  
     Beispiel im SharePoint-Modus, wenn nur die Schaltfläche **Zurück**, Steuerelemente für die Textsuche, Steuerelemente für die Seitennavigation und die Schaltfläche **Aktualisieren** angezeigt werden sollen:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15  
    ```  
  
## <a name="see-also"></a>Weitere Informationen
 - [URL-Zugriff &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)
 - [Exportieren von Berichten über URL-Zugriff](../reporting-services/export-a-report-using-url-access.md)
  
  
