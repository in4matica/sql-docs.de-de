---
title: Filter-und RecordCount-Eigenschaften (Beispiel) (VB) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RecordCount property [ADO], Visual Basic example
- Filter property [ADO], Visual Basic example
ms.assetid: e8bc63c7-8967-438a-9a49-512478a87a15
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f94440d9ddd0d0b5091f2a106f603397147ebda
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918641"
---
# <a name="filter-and-recordcount-properties-example-vb"></a>Filter- und RecordCount-Eigenschaft – Beispiel (VB)
In diesem Beispiel wird ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) für die Verleger Tabelle in der ***Pubs*** -Datenbank geöffnet. Anschließend wird die [Filter](../../../ado/reference/ado-api/filter-property.md) -Eigenschaft verwendet, um die Anzahl der sichtbaren Datensätze auf die Verleger in einem bestimmten Land/einer bestimmten Region zu begrenzen. Die **RecordCount** -Eigenschaft wird verwendet, um den Unterschied zwischen den gefilterten und ungefilterten Recordsets anzuzeigen.  
  
```  
'BeginFilterVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    ' recordset variables  
    Dim rstPublishers As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim SQLPublishers As String  
  
     ' criteria variables  
    Dim intPublisherCount As Integer  
    Dim strCountry As String  
    Dim strMessage As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset with data from Publishers table  
    Set rstPublishers = New ADODB.Recordset  
    SQLPublishers = "publishers"  
    rstPublishers.Open SQLPublishers, strCnxn, adOpenStatic, , adCmdTable  
  
    intPublisherCount = rstPublishers.RecordCount  
  
    ' get user input  
    strCountry = Trim(InputBox("Enter a country to filter on (e.g. USA):"))  
  
    If strCountry <> "" Then  
        ' open a filtered Recordset object  
        rstPublishers.Filter = "Country ='" & strCountry & "'"  
  
        If rstPublishers.RecordCount = 0 Then  
            MsgBox "No publishers from that country."  
        Else  
           ' print number of records for the original recordset  
           ' and the filtered recordset  
            strMessage = "Orders in original recordset: " & _  
                vbCr & intPublisherCount & vbCr & _  
                "Orders in filtered recordset (Country = '" & _  
                strCountry & "'): " & vbCr & _  
                rstPublishers.RecordCount  
            MsgBox strMessage  
        End If  
    End If  
  
    ' clean up  
    rstPublishers.Close  
    Cnxn.Close  
    Set rstPublishers = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstPublishers Is Nothing Then  
        If rstPublishers.State = adStateOpen Then rstPublishers.Close  
    End If  
    Set rstPublishers = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndFilterVB  
```  
  
> [!NOTE]
>  Wenn Sie die Daten kennen, die Sie auswählen möchten, ist es in der Regel effizienter, ein **Recordset** mit einer SQL-Anweisung zu öffnen. Dieses Beispiel zeigt, wie Sie nur ein **Recordset** erstellen und Datensätze aus einem bestimmten Land abrufen können.  
  
```  
Attribute VB_Name = "Filter"  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Filter-Eigenschaft](../../../ado/reference/ado-api/filter-property.md)   
 [RecordCount-Eigenschaft (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
