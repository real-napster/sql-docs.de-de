---
title: Benutzerdefinierte Eigenschaften des Ziels für Dimensionsverarbeitung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8c14320079573ffe63980a4ee0d27a0562b45333
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58283058"
---
# <a name="dimension-processing-destination-custom-properies"></a>Benutzerdefinierte Eigenschaften des Ziels für Dimensionsverarbeitung
  Das Ziel für Dimensionsverarbeitung verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften des Ziels für Dimensionsverarbeitung. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|und Beschreibung|  
|--------------|---------------|-----------------|  
|ASConnectionString|Zeichenfolge|Die Verbindungszeichenfolge zu einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt.|  
|KeyDuplicate|Ganze Zahl (Enumeration)|Wenn UseDefaultConfiguration **FALSE**ist; ein Wert, der angibt, wie Fehler aufgrund doppelter Schlüssel behandelt werden. Die möglichen Werte sind **IgnoreError** (0), **ReportAndContinue** (1) und **ReportAndStop** (2). Der Standardwert dieser Eigenschaft ist **IgnoreError** (0).|  
|KeyErrorAction|Ganze Zahl (Enumeration)|Wenn UseDefaultConfiguration **FALSE**ist; ein Wert, der angibt, wie Fehler aufgrund von Schlüsseln behandelt werden sollen. Die möglichen Werte sind **ConvertToUnknown** (0) und **DiscardRecord** (1). Der Standardwert dieser Eigenschaft ist **ConvertToUnknown** (0).|  
|KeyErrorLimit|Integer|Wenn UseDefaultConfiguration **FALSE**ist; die Obergrenze von aktivierten Schlüsselfehlern.|  
|KeyErrorLimitAction|Ganze Zahl (Enumeration)|Wenn UseDefaultConfiguration **FALSE**ist; ein Wert, der angibt, welche Aktion aufgeführt werden soll, wenn **KeyErrorLimit** erreicht wird. Die möglichen Werte sind **StopLogging** (1) und **StopProcessing** (0). Der Standardwert dieser Eigenschaft ist **StopProcessing** (0).|  
|KeyErrorLogFile|Zeichenfolge|Wenn UseDefaultConfiguration **FALSE**ist; der Pfad und Dateiname der Fehlerprotokolldatei.|  
|KeyNotFound|Ganze Zahl (Enumeration)|Wenn UseDefaultConfiguration **FALSE**ist; ein Wert, der angibt, wie Fehler aufgrund fehlender Schlüssel behandelt werden sollen. Die möglichen Werte sind **IgnoreError** (0), **ReportAndContinue** (1) und **ReportAndStop** (2). Der Standardwert dieser Eigenschaft ist **IgnoreError** (0).|  
|NullKeyConvertedToUnknown|Ganze Zahl (Enumeration)|Wenn UseDefaultConfiguration **FALSE**ist; ein Wert, der angibt, wie NULL-Schlüssel behandelt werden sollen, die in den unbekannten Wert konvertiert wurden. Die möglichen Werte sind **IgnoreError** (0), **ReportAndContinue** (1) und **ReportAndStop** (2). Der Standardwert dieser Eigenschaft ist **IgnoreError** (0).|  
|NullKeyNotAllowed|Ganze Zahl (Enumeration)|Wenn UseDefaultConfiguration **FALSE**ist; ein Wert, der angibt, wie nicht erlaubte Nullwerte behandelt werden sollen. Die möglichen Werte sind **IgnoreError** (0), **ReportAndContinue** (1) und **ReportAndStop** (2). Der Standardwert dieser Eigenschaft ist **IgnoreError** (0).|  
|ProcessType|Ganze Zahl (Enumeration)|Der Typ der von der Transformation verwendeten Dimensionsverarbeitung. Die Werte sind **ProcessAdd** (1) (inkrementell), **ProcessFull** (0) und **ProcessUpdate** (2).|  
|UseDefaultConfiguration|Boolean|Ein Wert, der angibt, ob die Transformation die Standardfehlerkonfiguration verwendet. Wenn diese Eigenschaft **False**ist, schließt die Transformation Informationen über Fehlerverarbeitung ein.|  
  
 Die Eingabe und die Eingabespalten des Ziels für Dimensionsverarbeitung verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## <a name="see-also"></a>Weitere Informationen  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
