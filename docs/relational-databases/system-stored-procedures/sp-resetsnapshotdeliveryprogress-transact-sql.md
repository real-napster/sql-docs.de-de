---
title: Sp_resetsnapshotdeliveryprogress (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c791fedcd483024c2bc6d564ce3f774fa2fded77
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530192"
---
# <a name="spresetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Setzt den Momentaufnahme-Übermittlungsprozess für ein Pullabonnement zurück, damit die Übermittlung der Momentaufnahme neu gestartet werden kann. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @verbose_level = ] verbose_level` Gibt die Menge der zurückgegebenen Informationen. *Verbose_level*ist **Int**, hat den Standardwert **1**. Der Wert **1** bedeutet, dass ein Fehler zurückgegeben, wenn auf die erforderlichen Sperren abgerufen werden können die **MSsnapshotdeliveryprogress** Tabelle und **0** bedeutet, die kein Fehler zurückgegeben wird.  
  
`[ @drop_table = ] 'drop_table'` Ist Sie, ob zu löschen oder Abschneiden der Tabelle, das Informationen über den Status der Momentaufnahme. *Drop_table* ist **nvarchar(5)**, hat den Standardwert **"false"**. Bei false wird die Tabelle abgeschnitten, und bei true wird die Tabelle gelöscht.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_resetsnapshotdeliveryprogress** entfernt alle Zeilen in der **MSsnapshotdeliveryprogress** Tabelle. Auf diese Weise werden alle Metadaten entfernt, die in der Abonnementdatenbank durch vorherige Momentaufnahme-Übermittlungsprozesse zurückgeblieben sind.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** -Serverrolle sein oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_resetsnapshotdeliveryprogress**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
