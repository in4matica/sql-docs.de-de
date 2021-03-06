---
title: Verwenden der SOAP-API in einer Webanwendung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], Web applications
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- report servers [Reporting Services], SOAP
- Web applications [Reporting Services]
ms.assetid: e8ca4455-0dc3-4741-8872-3636114938ad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5a90135c634e45f3fb4e3ff9c780347caaea24f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "63126267"
---
# <a name="using-the-soap-api-in-a-web-application"></a>Verwenden der SOAP-API in einer Webanwendung
  Über die Reporting Services-SOAP-API können Sie auf alle Funktionen des Berichtsservers zugreifen. Da es sich um einen Webdienst handelt, kann problemlos auf die SOAP-API zugegriffen werden, um Funktionen zur Unternehmensberichterstellung für Ihre benutzerdefinierten Geschäftsanwendungen bereitzustellen. Wenn Sie über eine Webanwendung auf den Report Server-Webdienst zugreifen, gehen Sie ganz ähnlich vor, als würden Sie über eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anwendung auf die SOAP-API zugreifen. Mithilfe von können Sie eine Proxy Klasse generieren, die die Eigenschaften und Methoden des Report Server-Webdiensts verfügbar macht und es Ihnen ermöglicht, eine vertraute Infrastruktur und Tools zum Erstellen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Geschäftsanwendungen auf der Technologie zu verwenden. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]  
  
 Von einer Webanwendung aus kann auf die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Funktionen für die Berichterstellung ebenso leicht wie von einer Windows-Anwendung aus zugegriffen werden. Wenn Sie mit einer Webanwendung arbeiten, können Sie unter anderem Elemente zur Berichtsserver-Datenbank hinzufügen oder daraus entfernen, Einstellungen für die Elementsicherheit festlegen, Elemente in der Berichtsserver-Datenbank ändern und die Zeitplanung und Übermittlung verwalten.  
  
## <a name="enabling-impersonation"></a>Aktivieren des Identitätswechsels  
 Der erste Schritt beim Konfigurieren der Webanwendung besteht darin, den Identitätswechsel vom Webdienstclient aus zu aktivieren. Mit Identitätswechsel können [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]-Anwendungen mit der Identität des Clients ausgeführt werden, in dessen Namen sie verwendet werden. 
  [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] nutzt [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internetinformationsdienste (Internet Information Services, IIS), um den Benutzer zu authentifizieren und ein authentifiziertes Token an die [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]-Anwendung zu übergeben oder ein nicht authentifiziertes Token zu übergeben, falls der Benutzer nicht authentifiziert werden kann. In jedem dieser Fälle nimmt die [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]-Anwendung die Identität des jeweils empfangenen Tokens an, wenn der Identitätswechsel aktiviert ist. Sie können den Identitätswechsel auf dem Client aktivieren, indem Sie die Datei Web.config der Clientanwendung folgendermaßen ändern:  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  Der Identitätswechsel ist standardmäßig deaktiviert.  
  
 Weitere Informationen [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] zum Identitätswechsel finden Sie in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
## <a name="managing-the-report-server-using-soap-api"></a>Verwalten des Berichtsservers mit der SOAP-API  
 Sie können die Webanwendung auch verwenden, um einen Berichtsserver und seinen Inhalt zu verwalten. Der mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] gelieferte Berichts-Manager ist ein Beispiel für eine Webanwendung, die komplett mit [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] und der Reporting Services-SOAP-API erstellt wurde. Sie können den benutzerdefinierten Webanwendungen die Berichtsverwaltungsfunktionalität des Berichts-Managers hinzufügen. Beispielsweise können Sie eine Liste der verfügbaren Berichte in der Berichts Server-Datenbank zurückgeben und diese in einem [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] `Listbox` -Steuerelement anzeigen, in dem die Benutzer auswählen können. Der folgende Code stellt eine Verbindung zur Berichtsserver-Datenbank her und gibt eine Liste der Elemente in der Berichtsserver-Datenbank zurück. Die verfügbaren Berichte werden dann zu einem ListBox-Steuerelement hinzugefügt, das für jeden Bericht eine Pfadangabe anzeigt.  
  
```vb  
Private Sub Page_Load(sender As Object, e As System.EventArgs)  
   ' Create a Web service proxy object and set credentials  
   Dim rs As New ReportingService2005()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return a list of catalog items in the report server database  
   Dim items As CatalogItem() = rs.ListChildren("/", True)  
  
   ' For each report, display the path of the report in a Listbox  
   Dim ci As CatalogItem  
   For Each ci In  items  
      If ci.Type = ItemTypeEnum.Report Then  
         catalogListBox.Items.Add(ci.Path)  
      End If  
   Next ci  
End Sub ' Page_Load   
```  
  
```csharp  
private void Page_Load(object sender, System.EventArgs e)  
{  
   // Create a Web service proxy object and set credentials  
   ReportingService2005 rs = new ReportingService2005();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return a list of catalog items in the report server database  
   CatalogItem[] items = rs.ListChildren("/", true);  
  
   // For each report, display the path of the report in a Listbox  
   foreach(CatalogItem ci in items)  
   {  
      if (ci.Type == ItemTypeEnum.Report)  
         catalogListBox.Items.Add(ci.Path);  
   }  
}  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Integrieren von Reporting Services in Anwendungen](../application-integration/integrating-reporting-services-into-applications.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../report-manager-ssrs-native-mode.md)   
 [Verwenden der SOAP-API in einer Windows-Anwendung](integrating-reporting-services-using-soap-windows-application.md)  
  
  
