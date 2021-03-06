---
title: Löschen von Beziehungen in tabellarischen Modellen von Analysis Services | Microsoft-Dokumentation
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 360de0e85048a491f3cfc750ac5288de73c65c95
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072771"
---
# <a name="delete-relationships"></a>Löschen von Beziehungen 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Sie können vorhandene Beziehungen in der Diagrammsicht des Modell-Designers oder über das Dialogfeld Beziehungen verwalten löschen. Informationen, wie Beziehungen in tabellarischen Modellen verwendet werden, finden Sie unter [Beziehungen](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
## <a name="considerations-for-deleting-relationships"></a>Überlegungen zum Löschen von Beziehungen  
 Berücksichtigen Sie vor dem Löschen einer Beziehung die folgenden Aspekte:  
  
-   Es gibt keine Möglichkeit, das Löschen einer Beziehung rückgängig zu machen. Sie können die Beziehung neu erstellen, diese Aktion erfordert jedoch eine vollständige Neuberechnung der Formeln im Modell. Führen Sie daher immer zuerst eine Überprüfung durch, bevor Sie eine Beziehung löschen, die in Formeln verwendet wird.  
  
-   Wenn Sie eine Beziehung zwischen zwei Tabellen löschen, kann dies Fehler in Formeln verursachen, die auf diese Tabellen verweisen.  
  
-   Die Data Analysis Expression (DAX)-Funktion RELATED sucht anhand der Beziehungen zwischen Tabellen nach verknüpften Werten in anderen Tabellen. Die Funktion gibt andere Ergebnisse zurück, nachdem die Beziehung gelöscht wurde. Weitere Informationen finden Sie im Thema zur RELATED-Funktion (DAX).  
  
-   Das Erstellen und Löschen von Beziehungen ändert nicht nur die PivotTable und die Formelergebnisse, sondern führt auch dazu, dass die Arbeitsmappe neu berechnet wird. Dies kann einige Zeit in Anspruch nehmen.  
  
## <a name="delete-relationships"></a>Löschen von Beziehungen  
  
#### <a name="to-delete-a-relationship-by-using-diagram-view"></a>So löschen Sie eine Beziehung mithilfe der Diagrammsicht  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** , zeigen Sie auf **Modellansicht**, und klicken Sie dann auf **Diagrammsicht**.  
  
2.  Klicken Sie mit der rechten Maustaste zwischen zwei Tabellen auf eine Beziehungslinie, und klicken Sie dann auf **Löschen**.  
  
#### <a name="to-delete-a-relationship-by-using-the-manage-relationships-dialog-box"></a>So löschen Sie eine Beziehung über das Dialogfeld "Beziehungen verwalten"  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]im Menü **Tabelle** auf **Beziehungen verwalten**.  
  
2.  Wählen Sie im Dialogfeld **Beziehungen verwalten** mindestens eine Beziehung aus der Liste aus.  
  
     Um mehrere Beziehungen auszuwählen, halten Sie die STRG-TASTE gedrückt, während Sie auf die einzelnen Beziehungen klicken.  
  
3.  Klicken Sie auf **Beziehung löschen**.  
  
4.  Klicken Sie im Dialogfeld **Beziehungen verwalten** auf **Schließen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Beziehungen](../../analysis-services/tabular-models/relationships-ssas-tabular.md)   
 [Erstellen einer Beziehung](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)  
  
  
