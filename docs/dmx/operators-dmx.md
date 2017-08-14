---
title: Operatoren (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- operators [DMX]
- DMX [Analysis Services], operators
- Data Mining Extensions [Analysis Services], operators
ms.assetid: e453e570-1ad1-4604-892f-6130308936ac
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 238b90116aadae4e56328995ac48624a67390fa6
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="operators-dmx"></a>Operatoren (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie Data Mining Extensions (DMX)-Operatoren, um in einer Abfrage im Arithmetik, Vergleich, Verkettung und logische Operationen auszuführen [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] werden Operatoren zum Ausführen folgender Aktionen verwendet:  
  
-   Suchen nach Werten oder Objekten, die mit einer bestimmten Bedingung übereinstimmen.  
  
-   Implementieren einer Entscheidung zwischen Werten oder Ausdrücken.  
  
 In DMX werden Operatoren aus verschiedenen Kategorien verwendet, die in den folgenden Abschnitten beschrieben sind. Weitere Informationen zu einzelnen Operatoren finden Sie unter [Data Mining-Erweiterungen &#40; DMX &#41; Operatorreferenz](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
|Operatorkategorie|Typ der Operation|  
|-----------------------|-----------------------|  
|[Arithmetische Operatoren &#40; DMX &#41;](../dmx/operators-arithmetic.md)|Ausführen einer Addition, Subtraktion, Multiplikation oder Division.|  
|[Vergleichsoperatoren &#40; DMX &#41;](../dmx/operators-comparison.md)|Vergleichen Sie einen Wert mit einem anderen Wert oder einen Ausdruck ein.|  
|[Logische Operatoren &#40; DMX &#41;](../dmx/operators-logical.md)|Testen, ob eine Bedingung wahr ist (z. B. AND, OR oder NOT).|  
|[Unäre Operatoren &#40; DMX &#41;](../dmx/operators-unary.md)|Ausführen einer Operation für einen einzelnen Operanden.|  
  
 Mit Operatoren können Sie kleinere Ausdrücke in DMX zu komplexeren Ausdrücken kombinieren. In solchen komplexen Ausdrücken werden die Operatoren in Abhängigkeit von der in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] definierten Operatorenrangfolge ausgewertet. Operatoren mit höherer Rangfolge werden vor Operatoren mit niedrigerer Rangfolge ausgeführt. Weitere Informationen zu Ausdrücken finden Sie unter [Ausdrücke &#40; DMX &#41;](../dmx/expressions-dmx.md).  
  
 Wenn Sie einfache Ausdrücke zu einem komplexen Ausdruck kombinieren, wird der Datentyp des sich ergebenden Ausdrucks durch Kombinieren der Regeln für die Operatoren mit den Regeln für die Rangfolge der Datentypen bestimmt. Wenn das Ergebnis ein Zeichen oder ein Unicode-Wert ist, bestimmt [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] die Sortierung des Ergebnisses durch Kombinieren der Regeln für die Operatoren mit den Regeln für die Sortierungsrangfolge. Es gibt auch Regeln, die die Genauigkeit, Dezimalstellen und Länge des Ergebnisses basierend auf der Genauigkeit, Dezimalstellen und Länge der einfachen Ausdrücke festlegen.  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Grundlegendes zur Select-Anweisung von DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
