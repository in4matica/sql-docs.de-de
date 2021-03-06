---
title: 'SQL: Relationship und die Schlüssel Bestellungs Regel (SQLXML)'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- key ordering rules [SQLXML]
- relationship annotation
ms.assetid: 914cb152-09f5-4b08-b35d-71940e4e9986
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c04b14f474e2afc0e6feb18eaa0bd321fdbb5e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246769"
---
# <a name="annotation-interpretation---sqlrelationship-and-key-ordering-rule"></a>Interpretation von Anmerkungen – sql:relationship und Schlüsselsortierregel
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Da das XML-Massenladen Datensätze generiert, wenn ihre Knoten in den Bereich gelangen, und diese Datensätze an Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sendet, wenn ihre Knoten den Bereich verlassen, müssen die Daten für den Datensatz im Bereich des Knotens vorhanden sein.  
  
 Beachten Sie das folgende XSD-Schema, in dem die 1: n-Beziehung ** \<** zwischen den Elementen "Customer>" und ** \<"Order>** " (ein Kunde kann viele Aufträge platzieren) mithilfe des ** \<SQL: Relationship>** -Elements angegeben wird:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"<>   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Wenn der ** \<Customer->** Elementknoten in den Bereich gelangt, generiert XML-Massen laden einen Kundendaten Satz. Dieser Datensatz bleibt, bis das XML-Massen laden ** \</Customer>** liest. Beim Verarbeiten des ** \<Order>** Element-Knotens verwendet ** \<** ** \<** ** \<XML-Massen laden SQL: Relationship>** , um den Wert der CustomerID-Fremdschlüssel Spalte der CustOrder-Tabelle vom Customer->Parent-Element abzurufen, da das Order>-Element das **CustomerID-** Attribut nicht angibt. Dies bedeutet, dass Sie beim Definieren des ** \<Customer>** -Elements das **CustomerID-** Attribut im Schema angeben müssen, bevor Sie ** \<SQL: Relationship>** angeben. Andernfalls generiert das XML-Massen laden einen Datensatz für die CustOrder-Tabelle, wenn das XML-Massen laden das ** \</Order->** Endtag [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erreicht, wenn ein ** \<Order>** -Element in den Gültigkeitsbereich gelangt.  
  
 Speichern Sie das in diesem Beispiel bereitgestellte Schema unter dem Dateinamen SampleSchema.xml.  
  
### <a name="to-test-a-working-sample"></a>So testen Sie ein funktionstüchtiges Beispiel  
  
1.  Erstellen Sie die folgenden Tabellen:  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
               CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
               CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
2.  Speichern Sie die folgenden Beispieldaten unter dem Dateinamen SampleXMLData.xml:  
  
    ```  
    <ROOT>    
      <Customers>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
        <CustomerID>1111</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>    
        <Order OrderID="3" />  
        <CustomerID>1112</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
        <CustomerID>1113</CustomerID>  
      </Customers>  
    </ROOT>  
    ```  
  
3.  Speichern Sie folgendes [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript)-Beispiel unter dem Dateinamen MySample.vbs, und führen Sie es aus, um das XML-Massenladen auszuführen:  

    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
     Als Ergebnis fügt das XML-Massenladen einen NULL-Wert in die CustomerID-Fremdschlüsselspalte der CustOrder-Tabelle ein. Wenn Sie die XML-Beispiel Daten so überarbeiten, dass das unter ** \<** ** \<geordnete Element "CustomerID">** vor dem Order>untergeordneten Element angezeigt wird, erhalten Sie das erwartete Ergebnis: das XML-Massen laden fügt den angegebenen Fremdschlüssel Wert in die Spalte ein.  
  
 Dies ist das entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID"  />  
   <ElementType name="CompanyName" />  
   <ElementType name="City"        />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
                 <sql:relationship  
                        key-relation    ="Cust"  
                        key             ="CustomerID"  
                        foreign-key     ="CustomerID"  
                        foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
  
