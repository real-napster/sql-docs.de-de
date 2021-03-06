---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: pmasl
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fc06dca68c6b6a4cedc730433401076ca07b126b
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042339"
---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Zeigt die Anzahl von Reihen, den reservierten Speicherplatz und den durch eine bestimmte Tabelle oder durch alle Tabellen in einer [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]- oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Datenbank belegten Speicherplatz an.
  
![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol zum Themenlink") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 Der ein-, zwei- oder dreiteilige Name der Tabelle, die angezeigt werden soll. Bei zwei- oder dreiteiligen Tabellennamen muss der Name in doppelte Anführungszeichen ("") gesetzt werden. Einteilige Tabellennamen müssen nicht unbedingt in Anführungszeichen gesetzt werden. Wenn kein Tabellenname angegeben wird, werden die Informationen für die aktuelle Datenbank angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die VIEW SERVER STATE-Berechtigung.
  
## <a name="result-sets"></a>Resultsets  
Im Folgenden wird das Resultset für alle Tabellen aufgeführt.
  
|Spalte|Datentyp|und Beschreibung|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|Insgesamt durch die Datenbank belegter Speicherplatz in KB.|  
|data_space|BIGINT|Durch die Daten belegter Speicherplatz in KB.|  
|index_space|BIGINT|Durch die Daten belegter Speicherplatz in KB.|  
|unused_space|BIGINT|Speicherplatz in KB, der zum reservierten Speicherplatz gehört und nicht verwendet wird.|  
|pdw_node_id|ssNoversion|Computeknoten, der für die Daten verwendet wird.|  
  
Im Folgenden wird das Resultset für eine Tabelle aufgeführt.
  
|Spalte|Datentyp|und Beschreibung|Bereich|  
|------------|---------------|-----------------|-----------|  
|rows|BIGINT|Anzahl von Zeilen.||  
|reserved_space|BIGINT|Gesamtspeicherplatz in KB, der für das Objekt reserviert ist.||  
|data_space|BIGINT|Durch die Daten belegter Speicherplatz in KB.||  
|index_space|BIGINT|Durch die Daten belegter Speicherplatz in KB.||  
|unused_space|BIGINT|Speicherplatz in KB, der zum reservierten Speicherplatz gehört und nicht verwendet wird.||  
|pdw_node_id|ssNoversion|Computeknoten, der zum Erstellen von Berichten zum Speicherplatz verwendet wird.||  
|distribution_id|ssNoversion|Verteilung, die zum Erstellen von Berichten zum Speicherplatz verwendet wird.|Der Wert für replizierte Tabellen ist –1.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. Grundlegende DBCC-PDW_SHOWSPACEUSED-Syntax  
Das folgende Beispiel zeigt verschiedene Möglichkeiten zum Anzeigen der Anzahl von Reihen, des reservierten Speicherplatzes und des Speicherplatzes, der durch die FactInternetSales-Tabellen in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]-Datenbank belegt ist.
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. Anzeigen des durch alle Tabellen in der aktuellen Datenbank belegten Speicherplatzes  
 Das folgende Beispiel zeigt den Speicherplatz, der reserviert und durch sämtliche Benutzer- und Systemtabellen in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]-Datenbank belegt ist.  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>Siehe auch
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
