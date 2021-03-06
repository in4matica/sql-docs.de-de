---
title: GUID-Escapesequenzen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a74ed9d4dfe0afb8bf59abb11220a0677d000bfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947587"
---
# <a name="guid-escape-sequences"></a>GUID-Escapesequenzen
ODBC verwendet Escapesequenzen für GUID-Literale. Die Syntax dieser Escapesequenz lautet wie folgt:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Bemerkungen  
 In der BNF-Notation lautet die Syntax wie folgt:  
  
 *ODBC-GUID-Escape* :: =  
     *ODBC-ESC-Initiator-GUID* '*GUID-Wert*' *ODBC-ESC-Terminator*  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 *GUID-value* :: = *Clock-Low-Value GUID-Separator Clock-Middle-Value GUID-Separator Clock-High-Value GUID-Separator Clock-SQ-Value GUID-Separator Knoten-Value*  
  
 *GUID-Separator* :: =-  
  
 *Clock-Low-Value* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit hex_digit  
  
 *Clock-Middle-Value* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *Clock-High-Value* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *Clock-*-Wert* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *Clock-Node-Value* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 Die Literale GUID-Escapesequenz wird unterstützt, wenn der GUID-Datentyp von der Datenquelle unterstützt wird. Eine Anwendung sollte **SQLGetTypeInfo** aufrufen, um zu bestimmen, ob dieser Datentyp unterstützt wird.
