---
title: REPLACENULL (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e7f931a95981ae15fe98c80770e91d370fe0a6b0
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290116"
---
# <a name="replacenull-ssis-expression"></a>REPLACENULL (SSIS-Ausdruck)
  Gibt den Wert des zweiten Ausdrucksparameters zurück, wenn der erste Ausdrucksparameter NULL ist; andernfalls wird der Wert des ersten Ausdrucks zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## <a name="arguments"></a>Argumente  
 *expression 1*  
 Das Ergebnis dieses Ausdrucks wird mit NULL verglichen.  
  
 *expression 2*  
 Das Ergebnis dieses Ausdrucks wird zurückgegeben, wenn der erste Ausdruck NULL ergibt.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
  
-   Die Länge von *expression 2* darf Null sein.  
  
-   REPLACENULL gibt ein NULL-Ergebnis zurück, wenn eines der Argumente NULL ist.  
  
-   BLOB-Spalten (DT_TEXT, DT_NTEXT, DT_IMAGE) werden von keimen der beiden Parameter unterstützt.  
  
-   Es wird davon ausgegangen, dass die zwei Ausdrücke den gleichen Rückgabetyp haben. Andernfalls versucht die Funktion, den 2. Ausdruck in den Rückgabetyp des 1. Ausdrucks umzuwandeln, was möglicherweise zu einem Fehler führt, wenn die Datentypen nicht kompatibel sind.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Im folgenden Beispiel wird ein beliebiger NULL-Wert in einer Datenbankspalte durch eine Zeichenfolge (1900-01-01) ersetzt. Diese Funktion wird vor allem in häufigen Mustern für abgeleitete Spalten verwendet, in denen Sie NULL-Werte durch andere Werte ersetzen möchten.  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]
>  Im folgenden Beispiel wird gezeigt, wie in [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]/ [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]vorgegangen wurde.  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? "1900-01-01" : MyColumn)   
```  
  
  
