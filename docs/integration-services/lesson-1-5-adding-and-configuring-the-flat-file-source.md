---
title: 'Schritt 5: Hinzufügen und Konfigurieren der Flatfilequelle | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c28ee5f1ca3e5202cb62cef3b1a0f79ee3fcd69b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58280024"
---
# <a name="lesson-1-5-add-and-configure-the-flat-file-source"></a>Lektion 1.5: Hinzufügen und Konfigurieren der Flatfilequelle
In dieser Aufgabe fügen Sie Ihrem Paket eine Flatfilequelle hinzu und konfigurieren diese. Eine Flatfilequelle ist eine Datenflusskomponente, die vom Verbindungs-Manager für Flatfiles definierte Metadaten verwendet. Diese Metadaten geben das Format und die Struktur der Daten an, die durch einen Transformationsprozess aus der Flatfile extrahiert werden können. Die Flatfilequelle kann zum Extrahieren von Daten aus einer einzigen Flatfile konfiguriert werden, indem die Formatdefinition des Verbindungs-Managers für Flatfiles verwendet wird.  
  
Für diese Aufgabe konfigurieren Sie die Flatfilequelle zum Verwenden von der Verbindungs-Manager-Instanz **Sample Flat File Source Data** (Beispieldaten aus der Flatfilequelle), die Sie vorher erstellt haben.  
  
## <a name="add-a-flat-file-source-component"></a>Hinzufügen einer Flatfilequellenkomponente  
  
1.  Öffnen Sie den **Datenfluss**-Designer, indem Sie entweder auf den Datenflusstask **Extract Sample Currency Data** (Währungsdaten aus dem Beispiel extrahieren) doppelklicken oder auf die Registerkarte **Datenfluss** klicken.  
  
2.  Erweitern Sie in der **SSIS-Toolbox**die Option **Weitere Quellen**, und ziehen Sie anschließend **Flatfilequelle** auf die Entwurfsoberfläche der Registerkarte **Datenfluss** .  
  
3.  Klicken Sie auf der **Datenfluss**-Entwurfsoberfläche mit der rechten Maustaste auf die neu hinzugefügte **Flatfilequelle**, klicken Sie auf **Umbenennen**, und ändern Sie den Namen in **Extract Sample Currency Data** (Währungsdaten aus dem Beispiel extrahieren).  
  
4.  Doppelklicken Sie auf die Flatfilequelle, um das Dialogfeld **Quellen-Editor für Flatfiles** zu öffnen.  
  
5.  Klicken Sie im Feld **Verbindungs-Manager für Flatfiles** auf den Eintrag **Sample Flat File Source Data** (Beispieldaten aus der Flatfilequelle).  
  
6.  Klicken Sie auf **Spalten**, und überprüfen Sie, ob die Namen der Spalten richtig sind.  
  
7.  Wählen Sie **OK**.  
  
8.  Klicken Sie erst mit der rechten Maustaste auf die Flatfilequelle, und klicken Sie anschließend auf **Eigenschaften**.  
  
9. Überprüfen Sie im Fenster **Eigenschaften**, ob die Eigenschaft **LocaleID** auf **Englisch (USA)** festgelegt ist.  
  
## <a name="go-to-next-task"></a>Weiter zur nächsten Aufgabe
[Schritt 6: Hinzufügen und Konfigurieren von Suchtransformationen](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Siehe auch  
[Flatfilequelle](../integration-services/data-flow/flat-file-source.md)  
[Verbindungs-Manager für Flatfiles](../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
  
