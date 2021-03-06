---
title: Sysmail_update_profileaccount_sp (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profileaccount_sp_TSQL
- sysmail_update_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profileaccount_sp
ms.assetid: 92ca7488-29db-414e-8e36-08b0a8f542bb
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 96dc0a33c15f1547088c3fe7c79824da55cd1d35
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538122"
---
# <a name="sysmailupdateprofileaccountsp-transact-sql"></a>sysmail_update_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert die Sequenznummer eines Kontos innerhalb eines Datenbank-E-Mail-Profils.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_update_profileaccount_sp  { [ @profile_id = ] profile_id   
| [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' } ,  
    [ @sequence_number = ] sequence_number  
```  
  
## <a name="arguments"></a>Argumente  
`[ @profile_id = ] profile_id` Die Profil-ID des Profils aktualisiert. *profile_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es muss entweder *profile_id* oder *profile_name* angegeben werden.  
  
`[ @profile_name = ] 'profile_name'` Der Profilname des Profils, das aktualisiert werden soll. *profile_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es muss entweder *profile_id* oder *profile_name* angegeben werden.  
  
`[ @account_id = ] account_id` Die Konto-ID aktualisieren. *account_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es muss entweder *account_id* oder *account_name* angegeben werden.  
  
`[ @account_name = ] 'account_name'` Der Name des zu aktualisierenden Kontos. *account_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es muss entweder *account_id* oder *account_name* angegeben werden.  
  
`[ @sequence_number = ] sequence_number` Die neue Sequenznummer für das Konto. *sequence_number* ist vom Datentyp **int**und hat keinen Standardwert. Über die Sequenznummer wird die Reihenfolge festgelegt, in der Konten im Profil verwendet werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 None  
  
## <a name="remarks"></a>Hinweise  
 Gibt einen Fehler zurück, wenn das angegebene Konto dem angegebenen Profil nicht zugeordnet ist.  
  
 Über die Sequenznummer wird die Reihenfolge festgelegt, in der Konten im Profil von Datenbank-E-Mail verwendet werden. Für eine neue E-Mail-Nachricht beginnt Datenbank-E-Mail mit dem Konto mit der niedrigsten Sequenznummer. Wenn dieses Konto fehlschlägt, verwendet Datenbank-E-Mail das Konto mit der nächsthöheren Sequenznummer usw., bis entweder Datenbank-E-Mail die Nachricht erfolgreich versendet oder das Konto mit der höchsten Sequenznummer fehlschlägt. Wenn das Konto mit der höchsten Sequenznummer einen Fehler erzeugt, dann wird die E-Mail-Nachricht nicht versandt.  
  
 Sind mehrere Konten mit der gleichen Sequenznummer vorhanden, verwendet Datenbank-E-Mail nur eines dieser Konten für eine bestimmte E-Mail-Nachricht. In diesem Fall kann Datenbank-E-Mail nicht sicherstellen, welches der Konten für diese Sequenznummer verwendet wird oder dass für die einzelnen Nachrichten jeweils dasselbe Konto verwendet wird.  
  
 Die gespeicherte Prozedur **sysmail_update_profileaccount_sp** wird in der **msdb** -Datenbank gespeichert und befindet sich im Besitz des **dbo** -Schemas. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Sequenznummer des Kontos `Admin-BackupServer` innerhalb des Profils `AdventureWorks Administrator` in der **msdb** -Datenbank geändert. Nach der Ausführung dieses Codes lautet die Sequenznummer für das Konto `3`, was bedeutet, dass es verwendet wird, wenn die beiden ersten Konten einen Fehler erzeugen.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@account_name = 'Admin-BackupServer',  
    ,@sequence_number = 3;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines e-Mail-Datenbankkontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail Configuration Objects](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Datenbank-e-Mails gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
