---
title: CHOOSE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHOOSE
- CHOOSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHOOSE function
ms.assetid: 1c382c83-7500-4bae-bbdc-c1dbebd3d83f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4538f270007508cea6b90a34388968ed886b4d36
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526143"
---
# <a name="logical-functions---choose-transact-sql"></a>Logische Funktionen: CHOOSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt das Element am angegebenen Index aus einer Werteliste in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CHOOSE ( index, val_1, val_2 [, val_n ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Index*  
 Dies ist ein ganzzahliger Ausdruck, der einen auf 1 basierenden Index in der nachfolgenden Elementliste darstellt.  
  
 Wenn der angegebene Indexwert einen anderen numerischen Datentyp als **int** hat, wird der Wert implizit in eine ganze Zahl konvertiert. Wenn der Indexwert die Grenzen des Wertarrays überschreitet, gibt CHOOSE Null zurück.  
  
 *val_1 ... val_n*  
 Liste von durch Trennzeichen getrennte Werten eines beliebigen Datentyps.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Datentyp mit der höchsten Rangfolge aus dem Satz von Typen zurück, der an die Funktion übergeben wurde. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 CHOOSE hat die gleiche Funktion wie ein Index in einem Array, wobei das Array aus den Argumenten besteht, die dem Indexargument folgen. Das Indexargument bestimmt, welcher der folgenden Werte zurückgegeben wird.  
  
## <a name="examples"></a>Beispiele  

### <a name="a-simple-choose-example"></a>A. Einfaches CHOOSE-Beispiel

 Im folgenden Beispiel wird das dritte Element aus der Liste der Werte zurückgegeben, die angegeben wurde.  
 
```  
SELECT CHOOSE ( 3, 'Manager', 'Director', 'Developer', 'Tester' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
-------------  
Developer  
  
(1 row(s) affected)  
```  

### <a name="b-simple-choose-example-based-on-column"></a>B. Einfaches CHOOSE-Beispiel, basierend auf einer Spalte

 Im folgenden Beispiel wird eine einfache Zeichenfolge zurückgegeben, die auf dem Wert in der Spalte `ProductCategoryID` basiert.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductCategoryID, CHOOSE (ProductCategoryID, 'A','B','C','D','E') AS Expression1  
FROM Production.ProductCategory;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductCategoryID Expression1  
----------------- -----------  
3                 C  
1                 A  
2                 B  
4                 D  
  
(4 row(s) affected)  
  
```  

### <a name="c-choose-in-combination-with-month"></a>C. CHOSSE in Kombination mit MONTH
  
 Im folgenden Beispiel wird die Jahreszeit zurückgegeben, in der ein Mitarbeiter eingestellt wurde. Die MONTH-Funktion wird verwendet, um den Monatswert aus der Spalte `HireDate` zurückzugeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, HireDate, CHOOSE(MONTH(HireDate),'Winter','Winter', 'Spring','Spring','Spring','Summer','Summer',   
                                                  'Summer','Autumn','Autumn','Autumn','Winter') AS Quarter_Hired  
FROM HumanResources.Employee  
WHERE  YEAR(HireDate) > 2005  
ORDER BY YEAR(HireDate);  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
JobTitle                                           HireDate   Quarter_Hired  
-------------------------------------------------- ---------- -------------  
Sales Representative                               2006-11-01 Autumn  
European Sales Manager                             2006-05-18 Spring  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2007-07-01 Summer  
Pacific Sales Manager                              2007-04-15 Spring  
Sales Representative                               2007-07-01 Summer  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [IIF &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)  
  
  
