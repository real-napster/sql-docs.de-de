---
title: Sp_help (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f5e514307e1427cea0ea1bb4d75e7bf0806fd516
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537112"
---
# <a name="sphelp-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu einem Datenbankobjekt (alle Objekte aufgelistet, die der **sys.sysobjects** -kompatibilitätssicht angezeigt), einen benutzerdefinierten Datentyp oder einen Datentyp.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @objname = ] 'name'` Ist der Name eines beliebigen Objekts im **Sysobjects** , oder geben Sie eine benutzerdefinierte Daten die **Systypes** Tabelle. *Namen* ist **Nvarchar (** 776 **)**, hat den Standardwert NULL. Datenbanknamen sind nicht zulässig.  Zwei bis drei Teilnamen müssen eingeschränkt werden, z.B. „Person.AddressType“ oder [Person.AddressType].   
   
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Das Resultset mit Vorwärtscursor, die zurückgegeben werden, hängt davon ab, ob *Namen* wird angegeben, wenn er angegeben wird, und welche Datenbankobjekt kann.  
  
1.  Wenn **Sp_help** erfolgt keine Argumente, zusammenfassende Informationen zu aller Objekttypen, die in der aktuellen Datenbank vorhanden sind zurückgegeben wird.  
  
    |Spaltenname|Datentyp|Description|  
    |-----------------|---------------|-----------------|  
    |**Name**|**nvarchar(** 128 **)**|Objektname|  
    |**Besitzer**|**nvarchar(** 128 **)**|Objektbesitzer (Dies ist der Datenbankprinzipal, der das Objekt besitzt. Wird standardmäßig auf den Besitzer des Schemas festgelegt, das das Objekt enthält.)|  
    |**Object_type**|**nvarchar(** 31 **)**|Objekttyp|  
  
2.  Wenn *Namen* ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp oder den benutzerdefinierten Datentyp **Sp_help** gibt dieses Resultset zurück.  
  
    |Spaltenname|Datentyp|Description|  
    |-----------------|---------------|-----------------|  
    |**Type_name**|**nvarchar(** 128 **)**|Name des Datentyps.|  
    |**Storage_type**|**nvarchar(** 128 **)**|Name des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Typs|  
    |**Länge**|**smallint**|Physische Länge des Datentyps (in Bytes)|  
    |**prec**|**int**|Genauigkeit (Gesamtzahl der Ziffern)|  
    |**Dezimalstellen**|**int**|Anzahl der Stellen nach dem Dezimaltrennzeichen|  
    |**NULL zulassen**|**varchar(** 35 **)**|Zeigt an, ob NULL-Werte zulässig sind: "Yes" oder "No".|  
    |**Default_name**|**nvarchar(** 128 **)**|Name eines an diesen Typ gebundenen Standards.<br /><br /> NULL = Es ist kein Standard gebunden.|  
    |**Rule_name**|**nvarchar(** 128 **)**|Name einer an diesen Typ gebundenen Regel.<br /><br /> NULL = Es ist kein Standard gebunden.|  
    |**Sortierung**|**sysname**|Sortierung des Datentyps. NULL für Nicht-Zeichen-Datentypen|  
  
3.  Wenn *Namen* beliebiges Datenbankobjekt außer einem Datentyp **Sp_help** dieses Ergebnis und zusätzliche Resultsets, basierend auf dem Typ des angegebenen Objekts zurück.  
  
    |Spaltenname|Datentyp|Description|  
    |-----------------|---------------|-----------------|  
    |**Name**|**nvarchar(** 128 **)**|Tabellenname|  
    |**Besitzer**|**nvarchar(** 128 **)**|Tabellenbesitzer|  
    |**Typ**|**nvarchar(** 31 **)**|Tabellentyp|  
    |**Created_datetime**|**datetime**|Erstellungsdatum der Tabelle|  
  
     Je nach der angegebenen Datenbankobjekt **Sp_help** zusätzliche Resultsets zurück.  
  
     Wenn *Namen* ist eine Systemtabelle, Benutzertabelle oder Sicht **Sp_help** gibt die folgenden Resultsets zurück. Das Resultset, das beschreibt, wo sich die Datendateien in einer Dateigruppe befinden, wird jedoch nicht für eine Sicht zurückgegeben.  
  
    -   Zusätzliches Resultset, das für Spaltenobjekte zurückgegeben wird:  
  
        |Spaltenname|Datentyp|Description|  
        |-----------------|---------------|-----------------|  
        |**Spaltenname**|**nvarchar(** 128 **)**|Name der Spalte.|  
        |**Typ**|**nvarchar(** 128 **)**|Datentyp der Spalte.|  
        |**Computed**|**varchar(** 35 **)**|Zeigt an, ob die Werte in der Spalte berechnet werden: "Yes" oder "No".|  
        |**Länge**|**int**|Spaltenlänge in Bytes<br /><br /> Hinweis: Wenn der Datentyp der Spalte einen Typ mit umfangreichen Werten ist (**varchar(max)**, **nvarchar(max)**, **'varbinary(max)'**, oder **Xml**), wird der Wert als-1 angezeigt.|  
        |**prec**|**char(** 5 **)**|Spaltengenauigkeit|  
        |**Dezimalstellen**|**char(** 5 **)**|Dezimalstellen einer Spalte|  
        |**NULL zulassen**|**varchar(** 35 **)**|Zeigt an, ob in der Spalte NULL-Werte zulässig sind: "Yes" oder "No".|  
        |**TrimTrailingBlanks**|**varchar(** 35 **)**|Nachfolgende Leerzeichen entfernen. Gibt Yes oder No zurück.|  
        |**FixedLenNullInSource**|**varchar(** 35 **)**|Nur aus Gründen der Abwärtskompatibilität beibehalten|  
        |**Sortierung**|**sysname**|Sortierung der Spalte. NULL für Nicht-Zeichen-Datentypen.|  
  
    -   Zusätzliches Resultset, das für Identitätsspalten zurückgegeben wird:  
  
        |Spaltenname|Datentyp|Description|  
        |-----------------|---------------|-----------------|  
        |**Identität**|**nvarchar(** 128 **)**|Name der Spalte, deren Datentyp als Identität deklariert wird|  
        |**Startwert**|**numeric**|Startwert für die Identitätsspalte|  
        |**Increment**|**numeric**|Schrittweite für Werte in dieser Spalte|  
        |**Not For Replication**|**int**|IDENTITY-Eigenschaft wird nicht erzwungen, wenn eine replikationsanmeldung wie z. B. **Sqlrepl**, fügt Daten in der Tabelle:<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   Zusätzliches Resultset, das für Spalten zurückgegeben wird:  
  
        |Spaltenname|Datentyp|Description|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|Name der GUID-Spalte|  
  
    -   Zusätzliches Resultset, das für Dateigruppen zurückgegeben wird:  
  
        |Spaltenname|Datentyp|Description|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar(** 128 **)**|Die Dateigruppe, in der sich die Daten befinden: primäre oder sekundäre Dateigruppe oder Transaktionsprotokoll|  
  
    -   Zusätzliches Resultset, das für Indizes zurückgegeben wird:  
  
        |Spaltenname|Datentyp|Description|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|Name des Indexes.|  
        |**Index_description**|**Varchar (** 210 **)**|Beschreibung des Index.|  
        |**index_keys**|**nvarchar(** 2078 **)**|Namen der Spalten, die für den Index verwendet werden. Gibt für speicheroptimierte xVelocity-columnstore-Indizes NULL zurück.|  
  
    -   Zusätzliches Resultset, das für Einschränkungen zurückgegeben wird:  
  
        |Spaltenname|Datentyp|Description|  
        |-----------------|---------------|-----------------|  
        |**constraint_type**|**nvarchar(** 146 **)**|Einschränkungstyp|  
        |**constraint_name**|**nvarchar(** 128 **)**|Der Name der Einschränkung.|  
        |**delete_action**|**nvarchar(** 9 **)**|Zeigt den Wert der DELETE-Aktion an: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT oder N/A.<br /><br /> Gilt nur für FOREIGN KEY-Einschränkungen.|  
        |**update_action**|**nvarchar(** 9 **)**|Zeigt den Wert der UPDATE-Aktion an: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT oder N/A.<br /><br /> Gilt nur für FOREIGN KEY-Einschränkungen.|  
        |**status_enabled**|**varchar(** 8 **)**|Zeigt an, ob die Einschränkung aktiviert ist: Enabled (aktiviert), Disabled (deaktiviert) oder N/A (NV).<br /><br /> Gilt nur für CHECK- und FOREIGN KEY-Einschränkungen.|  
        |**status_for_replication**|**Varchar (** 19 **)**|Zeigt an, ob die Einschränkung für die Replikation gilt.<br /><br /> Gilt nur für CHECK- und FOREIGN KEY-Einschränkungen.|  
        |**constraint_keys**|**nvarchar(** 2078 **)**|Die Namen der Spalten für die Einschränkung oder bei Standards und Regeln der Text, der den Standard oder die Regel definiert.|  
  
    -   Zusätzliches Resultset, das für verweisende Objekte zurückgegeben wird:  
  
        |Spaltenname|Datentyp|Description|  
        |-----------------|---------------|-----------------|  
        |**Die Tabelle wird durch verwiesen.**|**nvarchar(** 516 **)**|Identifiziert andere Datenbankobjekte, die auf die Tabelle verweisen.|  
  
    -   Zusätzliches Resultset, das für gespeicherte Prozeduren, Funktionen oder erweiterte gespeicherte Prozeduren zurückgegeben wird.  
  
        |Spaltenname|Datentyp|Description|  
        |-----------------|---------------|-----------------|  
        |**Parameter_name**|**nvarchar(** 128 **)**|Name des Parameters der gespeicherten Prozedur|  
        |**Typ**|**nvarchar(** 128 **)**|Datentyp des Parameters der gespeicherten Prozedur|  
        |**Länge**|**smallint**|Maximale physische Speicherlänge in Bytes|  
        |**prec**|**int**|Genauigkeit oder Gesamtzahl der Ziffern|  
        |**Dezimalstellen**|**int**|Die Anzahl der Ziffern rechts vom Dezimalzeichen|  
        |**Param_order**|**smallint**|Reihenfolge der Parameter|  
  
## <a name="remarks"></a>Hinweise  
 Die **Sp_help** für ein Objekt nur in der aktuellen Datenbank sucht.  
  
 Wenn *Namen* nicht angegeben ist, **Sp_help** Listen Objekt Objektnamen, Besitzer und Objekttypen für alle Objekte in der aktuellen Datenbank. **Sp_helptrigger** stellt Informationen zu Triggern bereit.  
  
 **Sp_help** macht nur Indexspalten; aus diesem Grund macht es keine Informationen über XML-Indizes oder räumliche Indizes verfügbar.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle. Der Benutzer muss mindestens eine Berechtigung verfügen, auf *Objname*. Um Spalteneinschränkungsschlüssel, Standards oder Regeln anzuzeigen, müssen Sie über die VIEW DEFINITION-Berechtigung für die Tabelle verfügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-information-about-all-objects"></a>A. Zurückgeben von Informationen zu allen Objekten  
 Das folgende Beispiel führt Informationen zu jedem Objekt in der `master`-Datenbank auf.  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>B. Zurückgeben von Informationen zu einem einzelnen Objekt  
 Das folgende Beispiel zeigt Informationen zur `Person`-Tabelle an.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-Engine gespeicherten Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sysobjects &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
