---
title: Deaktivieren des Lightweightpoolings | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 481bb43d-6fe5-497c-9096-971fb6bf733b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d5bc9651433cc0940732d4818f5d9b8c0f011ad1
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2018
ms.locfileid: "51511975"
---
# <a name="disable-lightweight-pooling"></a>Deaktivieren des Lightweightpoolings
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Diese Regel überprüft, ob Lightweightpooling auf dem Server deaktiviert ist. Wenn Lightweightpooling auf 1 festgelegt wird, wechselt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Fibermodusplanung. Der Fibermodus ist für bestimmte Situationen vorgesehen, in denen der Kontextwechsel der UMS-Arbeitsthreads kritische Engpässe bei der Leistung verursacht. Da dies nur selten auftritt, verbessert der Fibermodus auch nur selten die Leistung oder die Skalierbarkeit auf einem typischen System.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Die Lightweightpooling-Option darf nur nach gründlichen Tests aktiviert werden, nachdem alle anderen Möglichkeiten zur Leistungsoptimierung ausgewertet wurden und der Kontextwechsel ein bekanntes Problem in Ihrer Umgebung darstellt.  
  
 Es wird empfohlen, die Fibermodusplanung nicht für Routinevorgänge zu verwenden, da sie die Leistung verringern kann, indem die normalen Vorteile des Kontextwechsels unterdrückt werden, und da einige Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die den lokalen Threadspeicher (TLS) verwenden, oder Thread-eigene Objekte, z. B. Mutexe (eine Art Win32-Kernel-Objekt), im Fibermodus nicht ordnungsgemäß arbeiten können.  
  
 Um Lightweightpooling zu entfernen, führen Sie die folgende Anweisung aus, und starten Sie dann [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]neu.  
  
```sql  
sp_configure 'show advanced options', 1;  
GO  
sp_configure 'lightweight pooling', 0;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Lightweightpooling (Serverkonfigurationsoption)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
