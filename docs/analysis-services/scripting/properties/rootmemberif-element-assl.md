---
title: RootMemberIf-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- RootMemberIf Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9c312a638544071697a59bf1a7ddfb44ce9c5746
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="rootmemberif-element-assl"></a>RootMemberIf-Element (ASSL)
  Bestimmt, wie das Stammelement oder die Elemente eines übergeordneten Attributs identifiziert werden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <RootMemberIf>...</RootMemberIf>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*ParentIsBlankSelfOrMissing*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Den Wert des der **RootMemberIf** Element wird nur von übergeordneten Attributen verwendet (also der Wert der der [Verwendung](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) Element von der **DimensionAttribute** übergeordnete Element ist Legen Sie auf *übergeordneten*) um die Stammelemente (höchsten) Elemente einer über-/ unterordnungshierarchie zu bestimmen.  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|Nur Elemente, die mindestens eine der für *ParentIsBlank*, *ParentIsSelf*oder *ParentIsMissing* geltenden Bedingungen erfüllen, werden als Stammelemente behandelt.|  
|*ParentIsBlank*|Nur Elemente mit Null, eine 0 (null) oder eine leere Zeichenfolge in den Schlüsselspalten, dargestellt durch die [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) Auflistung von **DimensionAttribute** werden als Stammelemente behandelt.|  
|*ParentIsSelf*|Es werden nur Elemente als Stammelemente behandelt, die für sich selbst als übergeordnetes Element festgelegt wurden.|  
|*ParentIsMissing*|Es werden nur Elemente als Stammelemente behandelt, deren übergeordnete Elemente nicht gefunden werden.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **RootMemberIf** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.RootIfValue>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  