---
title: NAVIGIEREN Sie in Sichten im Kompatibilitätsmodus 90 oder höher nicht zulässig ist | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 360208afdc5dddbd1795ba7aa47c2c05b7006b64
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506921"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>FOR BROWSE ist in Sichten im Kompatibilitätsmodus 90 oder höher nicht zulässig
  Upgrade Advisor hat die Verwendung der FOR BROWSE-Klausel in einer Sicht erkannt. Die FOR BROWSE-Klausel ist in Sichten zulässig (und wird ignoriert), wenn der Datenbank-Kompatibilitätsmodus auf 80 festgelegt ist. Die FOR BROWSE-Klausel ist nicht in Sichten zulässig, wenn der Datenbank-Kompatibilitätsmodus auf 90 oder höher festgelegt ist.  
  
## <a name="component"></a>Komponente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Korrekturmaßnahme  
 Beim Upgrade behalten die Benutzerdatenbanken ihren Kompatibilitätsmodus bei. Bevor Sie den Datenbank-Kompatibilitätsmodus in 90 oder höher ändern, entfernen Sie die FOR BROWSE-Klausel aus den Sichtdefinitionen. Weitere Informationen finden Sie unter "sp_dbcmptlevel" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-Engine-Upgrade-Probleme](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;neu&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
