---
title: Benutzerdefinierte Eigenschaften der Flatfile | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 18b1fd7ce88d7b9be5dfa8440a9675945e99837c
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58280454"
---
# <a name="flat-file-custom-properties"></a>Benutzerdefinierte Eigenschaften der Flatfile
  **Benutzerdefinierte Eigenschaften von Quellen**  
  
 Die Flatfilequelle verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften der Flatfilequelle beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|und Beschreibung|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|Zeichenfolge|Der Name einer Ausgabespalte, die den Dateinamen enthält. Wenn kein Name angegeben wird, wird keine Ausgabespalte generiert, die den Dateinamen enthält.<br /><br /> Hinweis: Diese Eigenschaft ist nicht im **Quellen-Editor für Flatfiles** verfügbar, kann jedoch im Dialogfeld **Erweiterter Editor** festgelegt werden.|  
|RetainNulls|Boolean|Ein Wert, der angibt, ob NULL-Werte aus der Quelldatei als NULL-Werte beibehalten werden sollen, wenn die Daten von der Data Transformation-Pipeline-Engine verarbeitet werden. Der Standardwert dieser Eigenschaft ist **False**.|  
  
 Die Ausgabe der Flatfilequelle verfügt nicht über benutzerdefinierte Eigenschaften.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Flatfilequelle. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|und Beschreibung|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|Ein Wert, der angibt, ob die Spalte die schnelleren gebietsschemaneutralen Analyseroutinen von DTS oder die gebietsschemabezogenen Standardanalyseroutinen verwendet. Weitere Informationen finden Sie unter [Fast Parse](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) und [Standard Parse](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013). Der Standardwert dieser Eigenschaft ist **False**.<br /><br /> Hinweis: Diese Eigenschaft ist nicht im **Quellen-Editor für Flatfiles** verfügbar, kann jedoch im Dialogfeld **Erweiterter Editor** festgelegt werden.|  
  
 Weitere Informationen finden Sie unter [Flat File Source](../../integration-services/data-flow/flat-file-source.md).  
  
 **Benutzerdefinierte Eigenschaften von Zielen**  
  
 Das Flatfileziel verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften des Flatfileziels. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|und Beschreibung|  
|-------------------|---------------|-----------------|  
|Header|Zeichenfolge|Ein Textblock, der in die Datei eingefügt wird, bevor Daten geschrieben werden.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
|Overwrite|Boolean|Ein Wert, der angibt, ob eine vorhandene Zieldatei mit demselben Namen überschrieben werden soll oder ob an diese Datei angehängt werden soll. Der Standardwert dieser Eigenschaft ist **True**.|  
  
 Die Eingabe und die Eingabespalten des Flatfileziels verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Flat File Destination](../../integration-services/data-flow/flat-file-destination.md).  
  
## <a name="see-also"></a>Weitere Informationen  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
