---
title: Analysieren von Daten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fd52b851d4ff35fe1fc9a3a9fed05be0b8098fa9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381989"
---
# <a name="parsing-data"></a>Analysieren von Daten
  Mit Datenflüssen in Paketen werden Daten zwischen heterogenen Datenspeichern extrahiert und geladen, die eine Reihe von standardmäßigen und benutzerdefinierten Datentypen verwenden können. In einem Datenfluss werden mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Quellen Daten extrahiert, Zeichenfolgendaten analysiert und Daten in einen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentyp konvertiert. Nachfolgende Transformationen können Daten analysieren, um sie in einen anderen Datentyp zu konvertieren oder um Spaltenkopien mit anderen Datentypen zu erstellen. Mit Ausdrücken in Komponenten können außerdem Argumente und Operanden in andere Datentypen umgewandelt werden. Wenn die Daten in einen Datenspeicher geladen werden, kann schließlich das Ziel die Daten analysieren, um sie in einen vom Ziel verwendeten Datentyp zu konvertieren. Weitere Informationen finden Sie unter [Integration Services Datentypen](integration-services-data-types.md).  
  
## <a name="types-of-parsing"></a>Analysetypen  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bietet zwei Arten der Analyse von Daten zu konvertieren: Die schnelle Analyse und Standardanalyse.  
  
-   Die schnelle Analyse besteht aus schnellen, einfachen Analyseroutinen, die keine gebietsschemaspezifischen Datentypkonvertierungen unterstützen, sondern nur die am häufigsten verwendeten Datums- und Zeitformate. Weitere Informationen finden Sie unter [Fast Parse](../fast-parse.md).  
  
-   Die Standardanalyse enthält viele Analyseroutinen, die alle Datentypkonvertierungen der APIs für die automatische Datentypkonvertierung in Oleaut32.dll und Ole2dsip.dll unterstützen. Weitere Informationen finden Sie unter [Standard Parse](../standard-parse.md).  
  
  
