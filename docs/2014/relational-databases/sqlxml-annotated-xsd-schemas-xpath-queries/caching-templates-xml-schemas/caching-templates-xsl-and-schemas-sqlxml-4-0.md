---
title: Zwischenspeichern von Vorlagen, XSL und Schemas (SQLXML 4.0) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 86777a00c7382ce9a1b8d67f06a6cd222f983a11
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754372"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>Zwischenspeichern von Vorlagen, XSL und Schemas (SQLXML 4.0)
  Um die Leistung zu verbessern, unterstützt [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 das Zwischenspeichern von Vorlagen, XSL und Schemas.  
  
 Alle Schemas, Vorlagen und XSL-Dateien (außer den Dateien von einem http://- oder ftp://-Speicherort) werden zwischengespeichert. Die zwischengespeicherten Dateien bleiben im Arbeitsspeicher, während der Prozess ausgeführt wird. Wenn der Prozess beendet wird, geht der gesamte Cacheinhalt verloren. Wenn Sie nur einen Prozess pro Abfrage ausführen, ist der Vorteil der Zwischenspeicherung möglicherweise nicht erkennbar.  
  
 Die Themen in diesem Abschnitt liefern weitere Informationen über das Zwischenspeichern:  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Zwischenspeichern von Vorlagen &#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)  
 Beschreibt einen Registrierungsschlüssel zum Zwischenspeichern von Vorlagen und stellt ihn bereit.  
  
 [XSL-zwischenspeichern &#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
 Beschreibt einen Registrierungsschlüssel zum Zwischenspeichern von XSL und stellt ihn bereit.  
  
 [Das Zwischenspeichern von Schemas &#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
 Erläutert Probleme der parallelen Installation in SQLXML, die beim Zwischenspeichern von Schemas auftreten können, und stellt Registrierungsschlüssel für das Zwischenspeichern von Schemas bereit.  
  
  
