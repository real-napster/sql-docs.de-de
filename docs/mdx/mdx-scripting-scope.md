---
title: SCOPE-Anweisung (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 497fdfb11ec186ffba56470f2b0ede2ed2f4221a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741769"
---
# <a name="mdx-scripting---scope"></a>MDX-Skripts - Bereich


  Beschränkt den Bereich angegebener MDX-Anweisungen (Multidimensional Expressions) auf einen angegebenen Teilcube.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SCOPE(Subcube_Expression)   
   [ MDX_Statement ]  
END SCOPE  
  
Subcube_Expression ::=(Auxiliary_Subcube [, Auxiliary_Subcube,...n])  
  
Auxiliary_Subcube ::=   
        Limited_Set   
    | Root([dimension_name])   
    | Leaves([dimension_name])  
  
Limited_Set ::=   
        single_tuple   
    | member   
    | Common_Grain_Members   
    | hierarchy.members   
    | level.members   
    | {}   
    | Descendants  
            (  
                  Member  
         , [level  
         [  
            , SELF   
             | AFTER   
                          | BEFORE   
                          | SELF_AND_AFTER   
                          | SELF_AND_BEFORE   
                          | SELF_BEFORE_AFTER   
                          | LEAVES  
                  ]  
            )   
[* <limited set>]  
```  
  
## <a name="arguments"></a>Argumente  
 *Subcube_Expression*  
 Ein gültiger MDX-Teilcubeausdruck.  
  
 *MDX_Statement*  
 Eine gültige MDX-Anweisung.  
  
 *Common_Grain_Members*  
 Eine gültige MDX-Anweisung, die zu Elementen derselben Granularität ausgewertet wird.  
  
 *single_tuple*  
 Ein einzelnes Tupel.  
  
## <a name="remarks"></a>Hinweise  
 Die SCOPE-Anweisung bestimmt den Teilcube, auf den sich die Ausführung mindestens einer MDX-Anweisung auswirkt. Wenn eine MDX-Anweisung nicht in eine SCOPE-Anweisung eingeschlossen ist, besteht der implizite Bereich der MDX-Anweisung im gesamten Cube.  
  
> [!NOTE]  
>  Ausgeblendete Elemente werden in SCOPE-Anweisungen verfügbar gemacht.  
  
 SCOPE-Anweisungen erstellen Teilcubes, die unabhängig von "Löcher" verfügbar machen die **MDX Compatibility** Einstellung. So kann z. B. die Anweisung `Scope( Customer.State.members )` die Staaten in Ländern oder Regionen einschließen, die keine Staaten enthalten, für die jedoch unsichtbare Platzhalterelemente eingefügt wurden.  
  
 Berechnete Elemente und benannte Mengen, die in einer SCOPE-Anweisung erstellt wurden, sind von der SCOPE-Anweisung nicht betroffen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel, aus der MDX-berechnungsskript in der Adventure Works-Beispielprojektmappe wird den aktuellen Bereich als Geschäftsquartal im Geschäftsjahr 2005 sowie das sales Amount Quota-Measure definiert, und weist dann einen Wert für die Zellen im aktuellen Bereich mithilfe der **ParallelPeriod** Funktion. Im Beispiel ändert dann den Bereich mit einem anderen SCOPE-Anweisung und führt dann eine weitere Zuweisung mithilfe der [This (MDX)](../mdx/this-mdx.md) Funktion.  
  
```  
Scope   
 (   
    [Date].[Fiscal Year].&[2005],  
    [Date].[Fiscal].[Fiscal Quarter].Members,  
    [Measures].[Sales Amount Quota]  
 ) ;     
  
   This = ParallelPeriod                               
          (   
             [Date].[Fiscal].[Fiscal Year], 1,  
             [Date].[Fiscal].CurrentMember   
          ) * 1.35 ;  
  
/*-- Allocate equally to months in FY 2002 -----------------------------*/  
  
  Scope   
  (   
     [Date].[Fiscal Year].&[2002],  
     [Date].[Fiscal].[Month].Members   
  ) ;     
  
    This = [Date].[Fiscal].CurrentMember.Parent / 3 ;     
  
  End Scope ;     
End Scope ;     
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Skriptanweisungen &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
