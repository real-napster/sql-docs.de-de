---
title: Sysmail_delete_account_sp (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_account_sp
- sysmail_delete_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_account_sp
ms.assetid: 2adcac78-4a4a-407e-9666-1d9c43c73cc2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96fb6d88431e0740f17db8c00c0e3e490220561c
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537095"
---
# <a name="sysmaildeleteaccountsp-transact-sql"></a>sysmail_delete_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht ein SMTP-gestütztes Datenbank-E-Mail-Konto. Sie können ein Konto auch mithilfe des Assistenten zum Konfigurieren von Datenbank-E-Mail löschen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_delete_account_sp { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }   
```  
  
## <a name="arguments"></a>Argumente  
`[ @account_id = ] account_id` Die ID des zu löschenden Kontos. *account_id* ist vom Datentyp **int**und hat keinen Standardwert. Es muss entweder *account_id* oder *account_name* angegeben werden.  
  
`[ @account_name = ] 'account_name'` Der Name des zu löschenden Kontos. *account_name* ist vom Datentyp **sysname**und hat keinen Standardwert. Es muss entweder *account_id* oder *account_name* angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 None  
  
## <a name="remarks"></a>Hinweise  
 Diese Prozedur löscht das angegebene Konto, unabhängig davon, ob das Konto von einem Profil verwendet wird. Ein Profil, das keine Konten enthält, kann E-Mail nicht erfolgreich senden.  
  
 Die gespeicherte Prozedur **sysmail_delete_account_sp** wird in der **msdb** -Datenbank gespeichert und befindet sich im Besitz des **dbo** -Schemas. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das Löschen des Datenbank-E-Mail-Kontos `AdventureWorks Administrator`veranschaulicht.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines e-Mail-Datenbankkontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail Configuration Objects](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [sysmail_add_account_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)   
 [sysmail_delete_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-profile-sp-transact-sql.md)   
 [sysmail_delete_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-profileaccount-sp-transact-sql.md)   
 [sysmail_help_account_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-account-sp-transact-sql.md)   
 [sysmail_help_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-profile-sp-transact-sql.md)   
 [sysmail_help_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-profileaccount-sp-transact-sql.md)   
 [sysmail_update_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)  
  
  
