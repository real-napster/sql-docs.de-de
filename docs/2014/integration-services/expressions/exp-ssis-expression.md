---
title: EXP (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 366a938b2e90ce448cbcba2775f0eb7f327aab61
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393793"
---
# <a name="exp-ssis-expression"></a>EXP (SSIS-Ausdruck)
  Gibt den Exponenten für die Basis e eines numerischen Ausdrucks zurück. Die EXP-Funktion ergänzt die Aktion der LN-Funktion und wird auch als Antilogarithmus bezeichnet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein gültiger numerischer Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_R8  
  
## <a name="remarks"></a>Hinweise  
 Der numerische Ausdruck wird in den DT_R8-Datentyp umgewandelt, bevor der Exponent berechnet wird. Weitere Informationen finden Sie unter [Integration Services Datentypen](../data-flow/integration-services-data-types.md).  
  
 Als Ergebnis wird immer eine positive Zahl zurückgegeben.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Diese Beispiele wenden die EXP-Funktion auf positive und negative Werte und auf Null an.  
  
```  
EXP(74)  
```  
  
 Gibt 1.373382979540176E+32 zurück.  
  
```  
EXP(-27)  
```  
  
 Gibt 1.879528816539083E-12 zurück.  
  
```  
EXP(0)  
```  
  
 Gibt 1 zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [LOG &#40;SSIS-Ausdruck&#41;](log-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](functions-ssis-expression.md)  
  
  
