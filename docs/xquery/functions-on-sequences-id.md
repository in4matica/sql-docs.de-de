---
title: ID-Funktion (XQuery) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 21bf98ac97c9a695b7b9576412d43c832011322d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68004666"
---
# <a name="functions-on-sequences---id"></a>Funktionen für Sequenzen – id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die Sequenz von Elementknoten mit xs: ID-Werten zurück, die den Werten eines oder mehrerer der xs: IDREF-Werte entsprechen, die in *$arg*bereitgestellt werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Ein oder mehrere xs:IDREF-Werte.  
  
## <a name="remarks"></a>Bemerkungen  
 Das Ergebnis der Funktion ist eine Sequenz von Elementen in der XML-Instanz in der Dokumentreihenfolge, die einen xs:ID-Wert gleich einem oder mehreren xs:IDREF-Werten in der Liste der xs:IDREF-Kandidaten besitzt.  
  
 Wenn der xs:IDREF-Wert keinem Element entspricht, gibt die Funktion die leere Sequenz zurück.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen bereit, die **** in verschiedenen Spalten vom Typ [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] XML in der-Datenbank gespeichert sind.  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. Abrufen von Elementen anhand des Werts des IDREF-Attributs  
 Im folgenden Beispiel wird FN: ID verwendet, um die `employee` <>-Elemente basierend auf dem IDREF-Manager-Attribut abzurufen. In diesem Beispiel ist das Manager-Attribut ein Attribut vom Typ IDREF, und das eid-Attribut ist ein Attribut vom Typ ID.  
  
 Bei einem bestimmten Manager-Attribut Wert sucht die **ID ()** -Funktion die `employee` <> Elements, dessen ID-Attribut Wert mit dem eingegebenen IDREF-Wert übereinstimmt. Anders ausgedrückt: für einen bestimmten Mitarbeiter gibt die **ID ()** -Funktion den Employee Manager zurück.  
  
 Im Beispiel geschieht Folgendes:  
  
-   Es wird eine XML-Schemaauflistung erstellt.  
  
-   Eine typisierte **XML** -Variable wird mithilfe der XML-Schema Auflistung erstellt.  
  
-   Die Abfrage ruft das Element mit einem ID-Attribut Wert ab, auf den durch das IDREF- **Manager** - `employee` Attribut des <>-Elements verwiesen wird.  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 Die Abfrage gibt "Dave" als Wert zurück. Dies gibt an, dass Dave Joes Manager ist.  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. Abrufen von Elementen anhand des Werts des IDREFS-Attributs von OrderList  
 Im folgenden Beispiel ist das OrderList-Attribut des <`Customer`>-Elements ein Attribut vom Typ IDREFS. Es listet die Bestellungs-IDs für diesen bestimmten Kunden auf. Für jede Bestell-ID ist ein untergeordnetes `Order` <>-Element unter dem `Customer` <> der den Bestellwert bereitstellt.  
  
 Der Abfrageausdruck `data(CustOrders:Customers/Customer[1]/@OrderList)[1]` ruft den ersten Wert aus der IDRES-Liste für den ersten Kunden ab. Dieser Wert wird dann an die **ID ()** -Funktion weitergegeben. Die-Funktion findet dann die `Order` <>-Elements, dessen OrderID-Attribut Wert mit der Eingabe der **ID ()** -Funktion übereinstimmt.  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]die zwei-Argument-Version der **ID ()** wird von nicht unterstützt.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]erfordert, dass der Argumenttyp von **ID ()** ein Untertyp von xs: IDREF * ist.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Funktionen für Sequenzen](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
