---
title: FOR XML-Unterstützung für Zeichenfolgen-Datentypen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e56377044abe7377f110e534ea7c1e08144b76c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512547"
---
# <a name="for-xml-support-for-string-data-types"></a>FOR XML-Unterstützung für Zeichenfolgen-Datentypen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Für das XML, das von den FOR XML-Leerzeichen in den Daten generiert wird, werden Entitäten erstellt.  
  
 Im folgenden Beispiel wird eine Beispieltabelle **T** erstellt und als Beispieldaten Zeilenvorschub-, Wagenrücklauf- und Tabstoppzeichen eingefügt. Die SELECT-Anweisung ruft die Daten aus der Tabelle ab.  
  
```  
CREATE TABLE T  
(  
  c1 int identity primary key,  
  c2 varchar(100)  
);  
go  
  
INSERT T (c2) VALUES ('Special character 0xD for carriage return ' + convert(varchar(10), 0xD) + ' after carriage return');  
INSERT T (c2) VALUES ('Special character 0x9 for tab ' + convert(varchar(10), 0x9) + ' after tab' );  
INSERT T (c2) VALUES ('Special character 0xA for line feed ' + convert(varchar(10), 0xA) + ' after line feed');  
go  
SELECT *   
FROM T  
FOR XML AUTO;  
go  
```  
  
 Dies ist das Ergebnis:  
  
```  
 <T c1="1" c2="Special character 0xD for carriage return   
 after carriage return" />  
 <T c1="2" c2="Special character 0x9 for tab     after tab" />  
 <T c1="3" c2="Special character 0xA for line feed   
after line feed" />  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Der Wagenrücklauf in der ersten Zeile wird in die Entität &#xD geändert.  
  
-   Das Tabstoppzeichen in der zweiten Zeile wird in die Entität &#x09 geändert.  
  
-   Das Zeilenvorschubzeichen in der dritten Zeile wird in die Entität &#xA geändert.  
  
## <a name="see-also"></a>Weitere Informationen  
 [FOR XML-Unterstützung für verschiedene SQL Server-Datentypen](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
