---
title: Anzeigen des XML für eine Analysis-Projekt (SSDT Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1542c33d67c95c1c7154d08dbffd550b5f8cc72
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025137"
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Anzeigen des XML für ein Analysis Services-Projekt (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Wenn Sie eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank im Projektmodus verwenden, wird in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] eine XML-Definition für jedes im Projektordner enthaltene Objekt erstellt. Sie können die Inhalte der XML-Datei für jedes Objekt innerhalb von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]anzeigen. Die XML-Datei kann auch direkt bearbeitet werden, jedoch wird in den meisten Situationen davon abgeraten, da Sie Änderungen vornehmen können, die die Unlesbarkeit der XML-Datei in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]bewirken.  
  
> [!NOTE]  
>  Sie können den XML-Code nicht für ein Gesamtprojekt, sondern nur für die jeweiligen Objekte anzeigen, da für jedes Objekt eine eigene Datei vorhanden ist. Die einzige Möglichkeit, den Code anzuzeigen, für ein Gesamtprojekt besteht darin, das Projekt erstellen und Anzeigen der ASSL-code in die \<Projektname > .asdatabase-Datei.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>So zeigen Sie den XML-Code für ein Objekt an  
  
1.  Öffnen Sie das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Objekt, und klicken Sie dann auf **Code anzeigen**.  
  
     Der XML-Code des Objekts wird in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Analysis Services-Projekten & #40; SSDT & #41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  
