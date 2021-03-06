---
title: sp_dropextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3690d4c954ae3cde5159100280597af14a796d3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529762"
---
# <a name="spdropextendedproc-transact-sql"></a>sp_dropextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht eine erweiterte gespeicherte Prozedur.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen die [CLR-Integration](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>Argumente  
`[ @functname = ] 'procedure'` Ist der Name der erweiterten gespeicherten Prozedur zu löschen. *Prozedur* ist **nvarchar(517)**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 None  
  
## <a name="remarks"></a>Hinweise  
 Ausführen von **Sp_dropextendedproc** löscht den Namen der benutzerdefinierten erweiterten gespeicherten Prozedur aus der [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) Katalogsicht und entfernt den Eintrag aus der [extended_procedures ](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) -Katalogsicht angezeigt. Diese gespeicherte Prozedur kann nur in ausgeführt werden die **master** Datenbank.  
  
**Sp_dropextendedproc** erweiterte gespeicherte Systemprozeduren nicht gelöscht. Stattdessen sollte der Systemadministrator EXECUTE-Berechtigung für die erweiterte gespeicherte Prozedur zum Verweigern der **öffentliche** Rolle.  
  
 **Sp_dropextendedproc** kann nicht innerhalb einer Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** feste Serverrolle **Sp_dropextendedproc**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die erweiterte gespeicherte Prozedur `xp_hello` gelöscht.  
  
> [!NOTE]  
>  Diese erweiterte gespeicherte Prozedur muss bereits vorhanden sein; andernfalls gibt das Beispiel eine Fehlermeldung zurück.  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
