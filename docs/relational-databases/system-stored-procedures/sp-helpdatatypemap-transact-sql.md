---
title: Sp_helpdatatypemap (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf42231158f646e34c63bd148ba66c9780b14785
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529592"
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu den definierten datentypzuordnungen zwischen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und nicht- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank-Managementsysteme (DBMS). Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpdatatypemap [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @defaults_only = ] defaults_only ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @source_dbms = ] 'source_dbms'` Ist der Name des DBMS aus dem die Datentypen zugeordnet werden. *Source_dbms* ist **Sysname**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Die Quelle ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
|**ORACLE**|Die Quelle ist eine Oracle-Datenbank.|  
  
`[ @source_version = ] 'source_version'` Ist die Produktversion des Quell-DBMS. *Source_version*ist **varchar(10)**, wenn nicht angegeben, die datentypzuordnungen für alle Versionen des Quell-DBMS zurückgegeben. Ermöglicht das Filtern des Resultsets nach der Quellversion des DBMS.  
  
`[ @source_type = ] 'source_type'` Im Quell-DBMS aufgelistete Datentyp. *Source_type* ist **Sysname**, und wenn nicht angegeben, werden die Zuordnungen für alle Datentypen im Quell-DBMS zurückgegeben. Ermöglicht das Filtern des Resultsets nach dem Datentyp im Quell-DBMS.  
  
`[ @destination_dbms = ] 'destination_dbms'` Ist der Name des Ziel-DBMS. *Destination_dbms* ist **Sysname**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Das Ziel ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
|**ORACLE**|Das Ziel ist eine Oracle-Datenbank.|  
|**DB2**|Das Ziel ist eine IBM DB2-Datenbank.|  
|**SYBASE**|Das Ziel ist eine Sybase-Datenbank.|  
  
`[ @destination_version = ] 'destination_version'` Ist die Produktversion des Ziel-DBMS. *Destination_version*ist **varchar(10)**, und wenn nicht angegeben, werden die Zuordnungen für alle Versionen des Ziel-DBMS zurückgegeben. Ermöglicht das Filtern des Resultsets nach der Zielversion des DBMS.  
  
`[ @destination_type = ] 'destination_type'` Im Ziel-DBMS aufgelistete Datentyp. *Destination_type*ist **Sysname**, und wenn nicht angegeben, werden die Zuordnungen für alle Datentypen im Ziel-DBMS zurückgegeben. Ermöglicht das Filtern des Resultsets nach dem Datentyp im Ziel-DBMS.  
  
`[ @defaults_only = ] defaults_only` Wird nur die standardmäßigen datentypzuordnungen zurückgegeben werden. *Defaults_only* ist **Bit**, hat den Standardwert **0**. **1** bedeutet, dass nur die standardmäßigen datentypzuordnungen zurückgegeben werden. **0** bedeutet, dass die standardmäßige und benutzerdefinierte Daten datentypzuordnungen zurückgegeben werden.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**mapping_id**|Identifiziert eine Datentypzuordnung.|  
|**source_dbms**|Der Name und die Versionsnummer des Quell-DBMS.|  
|**source_type**|Der Datentyp im Quell-DBMS.|  
|**destination_dbms**|Der Name des Ziel-DBMS.|  
|**destination_type**|Der Datentyp im Ziel-DBMS.|  
|**is_default**|Gibt an, ob die Zuordnung eine Standardzuordnung oder eine alternative Zuordnung ist. Der Wert **0** gibt an, dass diese Zuordnung Benutzerdefiniert ist.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpdatatypemap** definiert datentypzuordnungen von nicht - SQL Server-Verlegern und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verlegern zu nicht- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten.  
  
 Wenn die angegebene Kombination aus Quelle und Ziel-DBMS nicht unterstützt wird, **Sp_helpdatatypemap** wird ein leeres Resultset zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** auf dem Verteiler oder Mitglieder der festen Serverrolle die **Db_owner** -Datenbankrolle in der Verteilungsdatenbank kann ausführen **Sp_helpdatatypemap**.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
