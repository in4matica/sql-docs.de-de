---
title: Gleich geordnete Elemente (MDX) | Microsoft-Dokumentation
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9d8ba2dd26575ebd41f4a6c275a2668b1421dee6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036955"
---
# <a name="siblings-mdx"></a>Siblings (MDX)


  Gibt die gleichgeordneten Elemente eines angegebenen Elements zurück, einschließlich des Elements selbst.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.Siblings   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das Standardmeasure für die gleichgeordneten Elemente von March 2003 (January 2003, February 2003 und March 2003) zurückgegeben.  
  
```  
SELECT [Date].[Calendar].[Month].[March 2003].Siblings ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [MDX-Funktionsreferenz &#40;MDX-&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
