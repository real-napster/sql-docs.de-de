---
title: Entitätsberechtigungen (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], permissions
- permissions [Master Data Services], entities
ms.assetid: 22785062-4faf-46ee-bffa-01cbd6d5a5b3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4030351db122190636292ccc84c574af95df76fe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62517162"
---
# <a name="entity-permissions-master-data-services"></a>Entitätsberechtigungen (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Entitätsberechtigungen gelten für:  
  
-   Alle Attribute der Entität, einschließlich **Name** und **Code**für Blatt- und konsolidierte Elemente.  
  
-   Alle Collections der Entität.  
  
-   Explizite Hierarchiemitgliedschaften und Beziehungen.  
  
 Wenn Sie über eine Berechtigung für eine Entität verfügen, können Sie der Entität, ihren expliziten Hierarchien und ihren Auflistungen Elemente hinzufügen bzw. Elemente daraus entfernen.  
  
> [!NOTE]  
>  Diese Berechtigungen gelten nur für den Funktionsbereich **Explorer** der Benutzeroberfläche.  
  
|Berechtigung|Description|  
|----------------|-----------------|  
|**Lesen**|Der Benutzer kann Elemente, Attribute, Hierarchiemitgliedschaften oder Sammlungszugehörigkeiten anzeigen.|  
|**Erstellen**|Der Benutzer kann Elemente erstellen und während der Erstellung Attributwerte zuweisen.|  
|**Update**|Der Benutzer kann Elemente, Attribute, Hierarchiemitgliedschaften oder Sammlungszugehörigkeiten aktualisieren.|  
|**Delete**|Der Benutzer kann Elemente löschen.|  
|**Verweigern**|Der Zugriff auf die Entität wird vollständig verweigert.|  
  
 Die Berechtigungen zum Lesen, Erstellen, Aktualisieren und Löschen können miteinander kombiniert werden. Wenn Berechtigungen zum Erstellen, Aktualisieren und Löschen zugewiesen werden, wird die Leseberechtigung automatisch zugewiesen.  
  
## <a name="see-also"></a>Siehe auch  
 [Zuweisen von Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
