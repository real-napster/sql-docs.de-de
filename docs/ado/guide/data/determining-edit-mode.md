---
title: Bestimmen des Bearbeitungsmodus | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e638cda03d7dc0f0bd580c3ca29c126568d1595a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472341"
---
# <a name="determining-edit-mode"></a>Bestimmen des Bearbeitungsmodus
ADO verwaltet einen Bearbeitung Puffer mit den aktuellen Datensatz verknüpft ist. Die **EditMode** Eigenschaft gibt an, ob Änderungen an diesen Puffer vorgenommen wurden, oder gibt an, ob ein neuer Datensatz erstellt wurde. Verwendung **EditMode** auf den Bearbeitungsstatus des aktuellen Datensatzes zu bestimmen. Sie können für ausstehende Änderungen testen, wenn ein Bearbeitungsprozess unterbrochen wurde und zu bestimmen, ob Sie benötigen die **Update** oder **CancelUpdate** Methode.  
  
 **EditMode** gibt eines der **EditModeEnum** Konstanten, die in der folgenden Tabelle aufgeführt sind.  
  
|Konstante|Description|  
|--------------|-----------------|  
|**adEditNone**|Gibt an, dass keine Bearbeitungsvorgang ausgeführt wird.|  
|**adEditInProgress**|Gibt an, dass die Daten im aktuellen Datensatz geändert, aber nicht gespeichert wurde.|  
|**adEditAdd**|Gibt an, dass die **AddNew** Methode aufgerufen wurde, und der aktuelle Datensatz in der Kopierpuffer ist ein neuer Datensatz, der nicht mit der Datenbank gespeichert wurde.|  
|**adEditDelete**|Gibt an, dass der aktuelle Datensatz gelöscht wurde.|  
  
 **EditMode** kann einen gültigen Wert zurückgeben, nur dann, wenn ein aktueller Datensatz vorhanden ist. **EditMode** gibt einen Fehler zurück, wenn **BOF** oder **EOF** ist **"true"** oder wenn der aktuelle Datensatz gelöscht wurde.
