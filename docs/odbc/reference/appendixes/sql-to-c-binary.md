---
title: 'SQL zu C: binär | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16112ca3b66e0218efd54d3bf385e04cb654e3e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622588"
---
# <a name="sql-to-c-binary"></a>SQL zu C: binär
Der Bezeichner für die binäre ODBC-SQL-Datentypen sind:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 Die folgende Tabelle zeigt die ODBC-C-Datentypen, die in denen binäre SQL-Daten konvertiert werden können. Eine Erläuterung der Spalten und Ausdrücke in der Tabelle, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Bytelänge der Daten) \* 2 < *Pufferlänge*<br /><br /> (Bytelänge der Daten) \* 2 > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes|–<br /><br /> 01004|  
|SQL_C_WCHAR|(Zeichenlänge der Daten) \* 2 < *Pufferlänge*<br /><br /> (Zeichenlänge der Daten) \* 2 > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in Zeichen<br /><br /> Länge der Daten in Zeichen|–<br /><br /> 01004|  
|SQL_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes|–<br /><br /> 01004|  
  
 Wenn SQL-Binärdaten in C-Zeichendaten konvertiert werden, wird jedes Byte (8 Bit) der Quelldaten als zwei ASCII-Zeichen dargestellt. Diese Zeichen sind die ASCII-Darstellung der Zahl in die hexadezimale Form. Z. B. eine binäre 00000001 "01" konvertiert wird, und eine binäre 11111111 "FF" konvertiert wird.  
  
 Der Treiber immer einzelnen Bytes auf Paare von hexadezimalen Ziffern konvertiert und beendet die Zeichenfolge mit null Byte. Aus diesem Grund Wenn *Pufferlänge* ist sogar und kleiner als die Länge der konvertierten Daten, das letzte Byte der **TargetValuePtr* Puffer wird nicht verwendet. (Die konvertierten Daten müssen eine gerade Anzahl von Bytes, die weiter bis letzten Byte ist ein null-Byte und das letzte Byte kann nicht verwendet werden.)  
  
> [!NOTE]  
>  Anwendungsentwickler, die Bindung des binären SQL-Daten in einem C-Zeichendatentyp davon abgeraten. Diese Konvertierung ist in der Regel ineffizient und zeitaufwändig.
