---
title: Definieren einer Dimension. | Microsoft-Dokumentation
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 38185df9928286acf184fbad21fd75839856d017
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62467924"
---
# <a name="lesson-2-1---defining-a-dimension"></a>Lektion 2-1: Definieren einer Dimension.
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

In der folgenden Aufgabe verwenden Sie den Dimensions-Assistenten, um eine Date-Dimension zu erstellen.  
  
> [!NOTE]  
> Für diese Lektion ist es erforderlich, dass Sie alle Prozeduren in Lektion 1 abgeschlossen haben.  
  
### <a name="to-define-a-dimension"></a>So definieren Sie eine Dimension  
  
1.  Klicken Sie im Projektmappen-Explorer (auf der rechten Seite von Microsoft Visual Studio) mit der rechten Maustaste auf **Dimensionen**, und klicken Sie anschließend auf **Neue Dimension**. Der Dimensions-Assistent wird angezeigt.  
  
2.  Klicken Sie auf der Seite **Willkommen beim Dimensions-Assistenten** auf **Weiter**.  
  
3.  Überprüfen Sie, ob die Option **Vorhandene Tabelle verwenden** auf der Seite **Erstellungsmethode auswählen** ausgewählt ist, und klicken Sie anschließend auf **Weiter**.  
  
4.  Überprüfen Sie auf der Seite **Quellinformationen angeben** , ob die **Adventure Works DW 2012** -Datenquellensicht ausgewählt ist.  
  
5.  Wählen Sie in der Liste **Haupttabelle** den Eintrag **Date**aus.  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Aktivieren Sie auf der Seite **Dimensionsattribute auswählen** die Kontrollkästchen neben den folgenden Attributen:  
  
    -   **Date Key**  
  
    -   **Full Date Alternate Key**  
  
    -   **English Month Name**  
  
    -   **Calendar Quarter**  
  
    -   **Calendar Year**  
  
    -   **Calendar Semester**  
  
8.  Ändern Sie die Einstellung von der Spalte **Attributtyp** des **Full Date Alternate Key** -Attributs von **Regulär** in **Datum**. Klicken Sie hierzu auf **Regulär** in der Spalte **Attributtyp** . Klicken Sie anschließend auf den Pfeil, um die Optionen zu erweitern. Klicken Sie anschließend auf **Datum** > **Kalender** > **Datum**. Klicken Sie auf **OK**. Wiederholen Sie diese Schritte, um den Attributtyp der Attribute wie folgt zu ändern:  
  
    -   **English Month Name** in **Monat**  
  
    -   **Calendar Quarter** in **Quartal**  
  
    -   **Calendar Year** zu **Jahr**  
  
    -   **Calendar Semester** zu **Halbjahr**  
  
9. Klicken Sie auf **Weiter**.  
  
10. Auf der Seite **Assistenten abschließen** können Sie im Bereich Vorschau die **Date** -Dimension und ihre Attribute sehen.  
  
11. Klicken Sie auf **Fertig stellen** , um den Assistenten abzuschließen.  
  
    Im Projektmappen-Explorer wird im [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial-Projekt die Date-Dimension im Ordner **Dimensionen** angezeigt. Im Zentrum der Entwicklungsumgebung zeigt der Dimensions-Designer die Date-Dimension an.  
  
12. Klicken Sie im Menü **Datei** auf **Alle speichern**.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Definieren eines Cubes](../analysis-services/lesson-2-2-defining-a-cube.md)  
  
## <a name="see-also"></a>Siehe auch  
[Dimensionen in mehrdimensionalen Modellen](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
[Erstellen einer Dimension anhand einer vorhandenen Tabelle](../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
[Erstellen einer Dimension mit dem Dimensions-Assistenten](../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)  
  
  
  
