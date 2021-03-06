---
title: Sp_helppublication_snapshot (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0154f155c82554ba30ce71c9e7091fdc7565f587
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526622"
---
# <a name="sphelppublicationsnapshot-transact-sql"></a>sp_helppublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zum Momentaufnahme-Agent einer gegebenen Veröffentlichung zurück. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @publication = ] 'publication'` Ist der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
`[ @publisher = ] 'publisher'` Gibt einen nicht- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, wenn ein Artikel hinzugefügt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID des Momentaufnahme-Agents|  
|**name**|**nvarchar(100)**|Name des Momentaufnahme-Agents|  
|**publisher_security_mode**|**smallint**|Sicherheitsmodus, der vom Agent für die Verbindung mit dem Verleger verwendet wird. Folgende Werte sind möglich:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1** = Windows-Authentifizierung.|  
|**publisher_login**|**sysname**|Anmeldename, der für die Verbindung mit dem Verleger verwendet wird.|  
|**publisher_password**|**nvarchar(524)**|Aus Sicherheitsgründen Wert **\* \* \* \* \* \* \* \* \* \*** ist immer zurückgegeben.|  
|**job_id**|**uniqueidentifier**|Eindeutige ID des Agentauftrags.|  
|**job_login**|**nvarchar(512)**|Ist das Windows-Konto unter dem der Momentaufnahme-Agent ausgeführt wird, der zurückgegeben wird, im Format *Domäne*\\*Benutzername*.|  
|**job_password**|**sysname**|Aus Sicherheitsgründen Wert **\* \* \* \* \* \* \* \* \* \*** ist immer zurückgegeben.|  
|**schedule_name**|**sysname**|Name des für diesen Agentauftrag verwendeten Zeitplans|  
|**frequency_type**|**int**|Die Häufigkeit, mit der der Agent planmäßig ausgeführt wird. Die folgenden Werte sind möglich:<br /><br /> **1** = einmalige Ausführung<br /><br /> **2** = bedarfsgesteuert<br /><br /> **4** = täglich<br /><br /> **8** = wöchentlich<br /><br /> **16** = monatlich<br /><br /> **32** = mit relativem Monatsintervall<br /><br /> **64** = Autostart<br /><br /> **128** = wiederholt|  
|**frequency_interval**|**int**|Die Tage, an denen der Agent ausgeführt wird. Die folgenden Werte sind möglich.<br /><br /> **1** = Sonntag<br /><br /> **2** = Montag<br /><br /> **3** = Dienstag<br /><br /> **4** = Mittwoch<br /><br /> **5** = Thursday<br /><br /> **6** = Freitag<br /><br /> **7** = Samstag<br /><br /> **8** = Tag<br /><br /> **9** = Arbeitstage<br /><br /> **10** = Wochenendtage|  
|**frequency_subday_type**|**int**|Ist der Typ, der definiert, wie oft der Agent ausgeführt wird, wenn *Frequency_type* ist **4** (täglich), und kann einen der folgenden Werte sein.<br /><br /> **1** = zum angegebenen Zeitpunkt<br /><br /> **2** = Sekunden<br /><br /> **4** = Minuten<br /><br /> **8** = Stunden|  
|**frequency_subday_interval**|**int**|Anzahl der Intervalle von *Frequency_subday_type* , die zwischen der geplanten Ausführung des Agents auftreten.|  
|**frequency_relative_interval**|**int**|Ist der Woche, an dem der Agent in einem bestimmten Monat ausgeführt wird. wenn *Frequency_type* ist **32** (mit relativem Monatsintervall) und kann einen der folgenden Werte sein.<br /><br /> **1** = erster<br /><br /> **2** = Sekunde<br /><br /> **4** = Dritter<br /><br /> **8** = vierter<br /><br /> **16** = Last|  
|**frequency_recurrence_factor**|**int**|Anzahl der Wochen oder Monate zwischen der geplanten Ausführung der Momentaufnahme.|  
|**active_start_date**|**int**|Datum, an dem die Ausführung der Momentaufnahme zum ersten Mal geplant ist (Format: YYYYMMDD).|  
|**active_end_date**|**int**|Datum, an dem die Ausführung der Momentaufnahme zum letzten Mal geplant ist (Format: YYYYMMDD).|  
|**active_start_time**|**int**|Uhrzeit, zu der die Ausführung der Momentaufnahme zum ersten Mal geplant ist (Format: HHMMSS).|  
|**active_end_time**|**int**|Uhrzeit, zu der die Ausführung der Momentaufnahme zum letzten Mal geplant ist (Format: HHMMSS).|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_publication_snapshot** wird in allen Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** auf dem Verleger oder Mitglieder der festen Serverrolle die **Db_owner** festen Datenbankrolle für die Veröffentlichungsdatenbank können ausführen **Sp_help_publication_snapshot** .  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
