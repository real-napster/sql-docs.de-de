---
title: Festlegen oder Ändern der Spaltensortierung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a16794bb2cd61829058d9fac7be11438f563d44
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795072"
---
# <a name="set-or-change-the-column-collation"></a>Festlegen oder Ändern der Spaltensortierung
  Sie können die Datenbanksortierung für `char`-, `varchar`-, `text`-, `nchar`-, `nvarchar`- und `ntext`-Daten überschreiben, indem Sie eine andere Sortierung für eine bestimmte Spalte einer Tabelle angeben und dann eine der folgenden Optionen verwenden:  
  
-   Die COLLATE-Klausel von [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) und [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql). Zum Beispiel:  
  
    ```  
    CREATE TABLE dbo.MyTable  
      (PrimaryKey   int PRIMARY KEY,  
       CharCol      varchar(10) COLLATE French_CI_AS NOT NULL  
      );  
    GO  
    ALTER TABLE dbo.MyTable ALTER COLUMN CharCol  
                varchar(10)COLLATE Latin1_General_CI_AS NOT NULL;  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Weitere Informationen finden Sie unter [Collation and Unicode Support](collation-and-unicode-support.md).  
  
-   Mithilfe der `Column.Collation` -Eigenschaft in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
 Sie können die Sortierung einer Spalte nicht ändern, wenn folgende Objekte aktuell auf die Spalte verweisen:  
  
-   Eine berechnete Spalte.  
  
-   Ein Index.  
  
-   Verteilungsstatistiken, die entweder automatisch oder mithilfe der CREATE STATISTICS-Anweisung generiert wurden.  
  
-   Eine CHECK-Einschränkung.  
  
-   Eine FOREIGN KEY-Einschränkung.  
  
 Wenn Sie **tempdb**verwenden, enthält die [COLLATE](/sql/t-sql/statements/collations) -Klausel eine *database_defauls* -Option, mit der angegeben werden kann, dass für eine Spalte einer temporären Tabelle anstelle der Sortierung von **tempdb**die Standardsortierung der aktuellen Benutzerdatenbank für die Verbindung verwendet wird.  
  
## <a name="collations-and-text-columns"></a>Sortierungen und text-Spalten  
 Sie können Werte in einer `text`-Spalte einfügen und aktualisieren, deren Sortierung sich von der Codepage der Standardsortierung der Datenbank unterscheidet. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die Werte implizit in die Sortierung der Spalte konvertiert.  
  
## <a name="collations-and-tempdb"></a>Sortierungen und tempdb  
 Die **tempdb** -Datenbank wird bei jedem Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und weist die gleiche Standardsortierung wie die **model** -Datenbank auf. Dabei handelt es sich normalerweise um die gleiche Sortierung wie die Standardsortierung der Instanz. Wenn Sie eine Benutzerdatenbank erstellen und eine andere Standardsortierung als für die **model**-Datenbank angeben, verwendet die Benutzerdatenbank eine andere Standardsortierung als die **tempdb**-Datenbank. Alle temporären gespeicherten Prozeduren oder temporären Tabellen werden in **tempdb**erstellt und gespeichert. Dies bedeutet, dass alle impliziten Spalten in temporären Tabellen und alle Konstanten, Variablen und Parameter mit erzwingbaren Standards in temporär gespeicherten Prozeduren andere Sortierungen aufweisen als die vergleichbaren Objekte, die in dauerhaften Tabellen und gespeicherten Prozeduren erstellt werden.  
  
 Dies kann zu Problemen hinsichtlich einer Nichtübereinstimmung in Sortierungen zwischen benutzerdefinierten Datenbanken und Systemdatenbankobjekten führen. Eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet z. B. die Latin1_General_CS_AS-Sortierung, und Sie führen die folgenden Anweisungen aus:  
  
```  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 In diesem System verwendet die **tempdb** -Datenbank die Latin1_General_CS_AS-Sortierung mit Codepage 1252, und `TestDB` und `TestPermTab.Col1` verwenden die `Estonian_CS_AS` -Sortierung mit Codepage 1257. Zum Beispiel:  
  
```  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 Im vorherigen Beispiel verwendet die **tempdb** -Datenbank die Latin1_General_CS_AS-Sortierung, und `TestDB` und `TestTab.Col1` verwenden die `Estonian_CS_AS` -Sortierung. Zum Beispiel:  
  
```  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 Da **Tempdb** die standardserversortierung und `TestPermTab.Col1` verwendet eine andere Sortierung, SQL Server folgende Fehler zurückgegeben: "Kann nicht ein Sortierungskonflikt zwischen 'Latin1_General_CI_AS_KS_WS' und 'Estonian_CS_AS' im gleich Vorgang aufgelöst."  
  
 Sie können den Fehler vermeiden, indem Sie stattdessen eine der folgenden Alternativen verwenden:  
  
-   Geben Sie an, dass für die Spalte der temporären Tabelle die Standardsortierung der Benutzerdatenbank und nicht die Standardsortierung von **tempdb**verwendet wird. Auf diese Weise kann die temporäre Tabelle mit ähnlich formatierten Tabellen in mehreren Datenbanken arbeiten, wenn dies in dem System erforderlich ist.  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   Geben Sie die richtige Sortierung für die `#TestTempTab` -Spalte an:  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen oder Ändern der Serversortierung](set-or-change-the-server-collation.md)   
 [Festlegen oder Ändern der Datenbanksortierung](set-or-change-the-database-collation.md)   
 [Collation and Unicode Support](collation-and-unicode-support.md)  
  
  
