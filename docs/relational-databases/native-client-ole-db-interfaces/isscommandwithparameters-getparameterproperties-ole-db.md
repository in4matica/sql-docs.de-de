---
title: "'ISSCommandWithParameters::GetParameterProperties' (OLE DB)"
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f7aed4457df4f262b485147a4d370812eefd7547
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "75252659"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>'ISSCommandWithParameters::GetParameterProperties' (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Gibt ein Array aus SSPARAMPROPS-Eigenschaftensatzstrukturen zurück – einen SSPARAMPROPS-Eigenschaftensatz für jeden UDT- oder XML-Parameter.  
  
## <a name="syntax"></a>Syntax  
  
```cpp
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argumente  
 *pcparser*[out] [in]  
 Ein Zeiger auf den Arbeitsspeicher, der die Anzahl von SSPARAMPROPS-Strukturen enthält, die in *prgParamProperties*zurückgegeben werden.  
  
 *prgParamProperties*[out]  
 Ein Zeiger auf den Arbeitsspeicher, in den ein Array aus SSPARAMPROPS-Strukturen zurückgegeben wird. Der Anbieter ordnet Speicher für die Strukturen zu und gibt die Adresse zu diesem Arbeitsspeicher zurück. der Consumer gibt diesen Speicher mit **imbelegc:: Free** frei, wenn er die Strukturen nicht mehr benötigt. Vor dem Aufrufen von **imbelegc:: Free** für *prgParamProperties*muss der Consumer auch **VariantClear** für die *vValue* -Eigenschaft jeder DBPROP-Struktur aufrufen, um einen Speicher Verlust zu verhindern, wenn die Variante einen Verweistyp (z. b. BSTR) enthält. Wenn *pcparameams* bei der Ausgabe 0 (null) ist oder ein anderer Fehler als DB_E_ERRORSOCCURRED auftritt, weist der Anbieter keinen Speicher zu und stellt sicher, dass *prgParamProperties* bei der Ausgabe ein NULL-Zeiger ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Die **GetParameterProperties** -Methode gibt dieselben Fehlercodes zurück wie die OLE DB **ICommandProperties::GetProperties** -Methode, allerdings können DB_S_ERRORSOCCURRED und DB_E_ERRORSOCCURED nicht ausgelöst werden.  
  
## <a name="remarks"></a>Bemerkungen  
 **ISSCommandWithParameters:: GetParameterProperties** verhält sich in Bezug auf **GetParameterInfo**konsistent. Wenn [ISSCommandWithParameters::SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) und **SetParameterInfo** nicht aufgerufen wurden oder mit einem Wert von 0 (null) für **cParams** aufgerufen wurden, leitet GetParameterInfo Parameterinformationen ab und gibt diese zurück. Wenn **ISSCommandWithParameters::SetParameterProperties** oder **SetParameterInfo** für mindestens einen Parameter aufgerufen wurde, gibt **ISSCommandWithParameters::GetParameterProperties** Eigenschaften nur für die Parameter zurück, für die **ISSCommandWithParameters::SetParameterProperties** aufgerufen wurde. Wenn **ISSCommandWithParameters::SetParameterProperties** nach **ISSCommandWithParameters::GetParameterProperties** oder **GetParameterInfo**aufgerufen wird, geben nachfolgende Aufrufe von **ISSCommandWithParameters::GetParameterProperties** die überschriebenen Werte für jene Parameter zurück, für die **ISSCommandWithParameters::SetParameterProperties** aufgerufen wurde.  
  
 Die SSPARAMPROPS-Struktur ist folgendermaßen definiert:  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|Mitglied|BESCHREIBUNG|  
|------------|-----------------|  
|*iOrdinal*|Die Ordnungszahl des übergebenen Parameters|  
|*cpropertysets*|Die Anzahl von DBPROPSET-Strukturen in *rgPropertySets*|  
|*rgPropertySets*|Ein Zeiger auf den Speicher, in den ein Array aus DBPROPSET-Strukturen zurückgegeben werden soll|  
|||

## <a name="see-also"></a>Weitere Informationen  
 [' ISSCommandWithParameters ' &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
