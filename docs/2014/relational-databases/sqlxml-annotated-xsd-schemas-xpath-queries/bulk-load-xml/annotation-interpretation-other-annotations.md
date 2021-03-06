---
title: Andere Anmerkungen (SQLXML 4.0) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 668e26430e97a1e7d34e0e420966b975874224c0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750032"
---
# <a name="other-annotations-sqlxml-40"></a>Andere Anmerkungen (SQLXML 4.0)
  Neben den in den vorherigen Themen in diesem Abschnitt beschriebenen Anmerkungen interpretiert XML-Massenladen diese anderen Anmerkungen folgendermaßen:  
  
 `sql:id-prefix`  
 Wenn das Schema Präfixe für die XML-Daten festlegt, entfernt XML-Massenladen die Präfixe, bevor die Daten an Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]gesendet werden.  
  
 `sql:use-cdata`  
 XML-Massenladen liest den Text, der in den CDATA-Abschnitten gespeichert wird, und sendet ihn an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 `sql:url-encode`  
 XML-Massenladen unterstützt diese Anmerkung nicht. Eine in der XML-Dateneingabe angegebene URL wird beispielsweise von XML-Massenladen an diesem Speicherort nicht gelesen, sodass sie in der Datenbank gespeichert werden kann.  
  
 `sql:is-mapping-schema`  
 XML-Massenladen unterstützt weder diese Anmerkung noch `sql:id`.  
  
> [!NOTE]  
>  XML-Massenladen unterstützt keine Inlinezuordnungsschemas.  
  
 `sql:key-fields`  
 XML-Massenladen ignoriert stets diese Anmerkung.  
  
## <a name="see-also"></a>Siehe auch  
 [Interpretation von Anmerkungen &#40;SQLXML 4.0&#41;](annotation-interpretation-sqlxml-4-0.md)  
  
  
