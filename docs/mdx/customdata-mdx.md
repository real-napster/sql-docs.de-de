---
title: Die CustomData-Funktion (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXISTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Exists function
ms.assetid: 61d9f5a2-6f56-4179-a39b-317c8e0a2cdd
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 47f1f10a7636a2c53dc897d9e6858ac214281e73
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="customdata-mdx"></a>CustomData (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Wert der **CustomData** Verbindungszeichenfolgeneigenschaft, falls definiert; andernfalls, **null**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Die **CustomData** Funktion abrufen kann die **CustomData** Verbindung Zeichenfolgeneigenschaft und übergeben Sie eine Konfigurationseinstellung, die von MDX (Multidimensional Expressions)-Funktionen und Anweisungen, die verwendet werden, z. B. [UserName (MDX)](../mdx/username-mdx.md) und [aufrufen-Anweisung (MDX)](../mdx/mdx-data-manipulation-call.md). Diese Funktion kann z. B. in einem dynamischen Sicherheitsausdruck verwendet werden, wählen Sie die zulässigen/verweigerten Mengenelemente für den Zeichenfolgenwert in den **CustomData** Verbindungszeichenfolgen-Eigenschaft.  
  
## <a name="example"></a>Beispiel  
 Die folgende Abfrage zeigt den Rückgabewert von der **CustomData** Funktion in einem berechneten Measure:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
