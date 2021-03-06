---
title: ObjectStateEnum | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 560e95bdafe3f5bbae82b200d8f7db0dcb121911
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713738"
---
# <a name="objectstateenum"></a>ObjectStateEnum
Gibt an, ob ein Objekt offen oder geschlossen ist, Herstellen einer Verbindung mit einer Datenquelle Ausführen eines Befehls oder Abrufen von Daten.  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Gibt an, dass das Objekt beendet wird.|  
|**adStateOpen**|1|Gibt an, dass das Objekt geöffnet ist.|  
|**adStateConnecting**|2|Gibt an, dass das Objekt eine Verbindung herstellt.|  
|**adStateExecuting**|4|Gibt an, dass das Objekt einen Befehl ausgeführt wird.|  
|**adStateFetching**|8|Gibt an, dass die Zeilen des Objekts abgerufen werden.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-äquivalent  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[State-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[State-Eigenschaft (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
