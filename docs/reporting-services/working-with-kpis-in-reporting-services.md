---
title: Arbeiten mit KPIs in Reporting Services | Microsoft-Dokumentation
author: markingmyname
ms.author: maghan
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.date: 07/02/2017
ms.openlocfilehash: 4e6a5bbf2d744475ca49e3917f6539e81e6439ea
ms.sourcegitcommit: d6ef87a01836738b5f7941a68ca80f98c61a49d4
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2019
ms.locfileid: "57572803"
---
# <a name="working-with-kpis-in-reporting-services"></a>Arbeiten mit KPIs in Reporting Services

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Ein *Key Performance Indicator (KPI)* ist ein sichtbarer Hinweis, der Auskunft über den Fortschritt im Hinblick auf das Erreichen eines Ziels gibt.  Key Performance Indicators sind wertvoll für Teams, Manager und Unternehmen, um schnell den bei messbaren Zielen erzielten Fortschritt zu evaluieren.
  
Mit KPIs in SQL Server Reporting Services können Sie einfach Antworten für die folgenden Fragen visualisieren:  
  
- Womit bin ich weit vorangekommen, oder womit hänge ich hinterher?  
  
- Wie weit habe ich vorausgearbeitet, oder wie weit hänge ich hinterher?  
  
- Was sind die minimale Speichergröße, die ich abgeschlossen habe?  
  
## <a name="creating-a-dataset"></a>Erstellen eines Dataset

Eine KPI wird nur die erste Zeile der Daten aus einem freigegebenen Dataset verwenden. Stellen Sie sicher, dass sich die Daten, die Sie verwenden möchten, in dieser ersten Zeile befinden. Um ein freigegebenes Dataset zu erstellen, können Sie entweder den Berichts-Generator oder SQL Server Data Tools verwenden.  
  
> **Hinweis**: Das Dataset muss sich nicht im selben Ordner wie die KPI befinden.  
  
## <a name="placement-of-kpis"></a>Platzierung von KPIs  
  
KPIs können in einem beliebigen Ordner auf Ihrem Berichtsserver erstellt werden.  Bevor Sie eine KPI erstellen, sollten Sie überlegen, wo der richtige Speicherort dafür wäre. Sie können sie in einem Ordner ablegen, der für Benutzer sichtbar ist. Gleichzeitig sollte der Ordner auch relevant für andere Berichte sowie KPIs in der Umgebung sein.  
## <a name="adding-a-kpi"></a>Hinzufügen einer KPI
  
Nachdem Sie den Speicherort der KPI bestimmt haben, wechseln Sie zu dem Ordner, und wählen Sie **Neu** > **KPI** im oberen Menü aus.  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
Dies zeigt Ihnen den Bildschirm **Neue KPI** an.  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
Sie können entweder statische Werte zuweisen oder Daten aus einem freigegebenen Dataset verwenden. Wenn Sie eine neue KPI erstellen, wird diese mit zufälligen manuellen Daten aufgefüllt.  
  
| Feld | und Beschreibung |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Wertformat | Wird verwendet, um das Format des angezeigten Werts zu ändern. |
| value | Der für die KPI anzuzeigender Wert. |
| Ziel | Wird als Vergleich mit einem numerischen Wert verwendet und als prozentuale Differenz angezeigt. |
| Status | Zum Bestimmen der KPI-Kachelfarbe verwendete und durch Komma getrennte numerische Werte. Gültige Werte sind 1 (Grün), 0 (gelb) und-1 (Rot). |
| Trendsatz | Für Diagrammvisualisierungen verwendete durch Komma getrennte numerische Werte. Dies kann auch für eine Spalte eines Dataset mit Werten festgelegt werden, die den Trend darstellen. |
| Verwandte Inhalte | Die Fähigkeit, einen Drillthrough-Link festgelegt. Dieser Link kann entweder mit einem mobilen Bericht, der auf das Portal oder eine benutzerdefinierte URL veröffentlicht sein. |
  
> **Warnung**: Bei der Verwendung des Wordwerts für das **Status** -Feld zur Entwurfszeit, sollten Sie den Zahlenwert verwenden, wenn Sie ein Dataset aktualisieren. Wenn Sie ein Dataset mit dem Wortwert anstelle des Zahlenwerts aktualisieren, könnten die KPIs auf Ihrem Server beschädigt werden.  
>
> **Hinweis:**: Die Felder **Wert**, **Ziel** und **Status** können nur einen Wert aus der ersten Zeile des Ergebnisses eines Datasets auswählen. Das Feld **Trendsatz** kann jedoch wählen, welche Spalte den Trend widerspiegelt.  
  
Um Daten aus einem freigegebenen Dataset zu verwenden, können Sie die folgenden Schritte durchführen.
  
1. Ändern Sie das Dropdownfeld des Felds von **Manuell festlegen**oder **Nicht festgelegt**auf **Datasetfeld**.  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2. Klicken Sie im Datenfeld auf die **Auslassungspunkte (…)**. Hierdurch erscheint der Bildschirm **Wählen Sie ein Dataset** .  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3. Wählen Sie das Dataset aus, das die Daten enthält, die Sie anzeigen möchten.  
  
4. Wählen Sie das Feld aus, das Sie verwenden möchten. Wählen Sie **OK**.  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5. Ändern Sie das **Wertformat** , damit es mit dem Format Ihres Werts übereinstimmt. In diesem Beispiel ist der Wert einer Währung.  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6. Wählen Sie **Anwenden**aus.  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)

## <a name="configuring-related-content"></a>Konfigurieren verwandten Inhalte

Bei der Auswahl **mobiler Bericht**, Sie können das Ziel in einem Dialogfeld auswählen.

   ![Mobilgerätebericht](media/rscreatekpi-related-content-mobile-report.png)

Wenn Sie sich jetzt auf den KPI im Portal klicken, wird eine Miniaturansicht des mobilen Berichts in der Dropdownliste "Verwandte Inhalte" gezeigt. Auf dieser Miniaturansicht können Sie direkt zu diesem Bericht navigieren.

Sie können auch eine benutzerdefinierte URL angeben. Diese Aufgabe kann alles sein: eine Website, einer SharePoint-Website, eine URL zu einem SSRS-Bericht (sodass Sie hartcodierter Parameter übergeben wird).

![Benutzerdefinierte URL](media/rscreatekpi-related-content-custom-url.png)

Wenn Sie sich jetzt auf den KPI klicken, zeigt die URL, unter verwandten Inhalten.

Es ist nur möglich, einen mobilen Bericht oder eine benutzerdefinierte URL hinzufügen.
  
## <a name="removing-a-kpi"></a>Entfernen einer KPI  
  
Um eine KPI zu entfernen, können Sie die folgenden Schritte durchführen.
  
1. Klicken Sie bei der KPI, die Sie entfernen möchten, auf die **Auslassungspunkte (…)**. Wählen Sie **Verwalten**aus.  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2. Wählen Sie **Löschen**aus. Wählen Sie **Löschen** erneut im Bestätigungsdialogfeld aus.  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>Aktualisieren einer KPI  
  
Um eine KPI zu aktualisieren, müssen Sie eine Zwischenspeicherung für das freigegebene Dataset konfigurieren. Weitere Informationen zu Cacheaktualisierungsplänen finden Sie unter [Arbeiten mit freigegebenen Datasets – Webportal](../reporting-services/work-with-shared-datasets-web-portal.md).  
  
## <a name="next-steps"></a>Nächste Schritte
  
[Web portal (Webportal)](../reporting-services/web-portal-ssrs-native-mode.md)  
[Work with shared datasets (Arbeiten mit freigegebenen Datasets)](../reporting-services/work-with-shared-datasets-web-portal.md)

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](https://go.microsoft.com/fwlink/?LinkId=620231)
