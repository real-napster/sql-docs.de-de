---
title: Sp_helppullsubscription (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppullsubscription_TSQL
- sp_helppullsubscription
helpviewer_keywords:
- sp_helppullsubscription
ms.assetid: a0d9c3f1-1fe9-497c-8e2f-5b74f47a7346
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10a8184fdad0c25c2377c5ed9df0a318aba736a2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527772"
---
# <a name="sphelppullsubscription-transact-sql"></a>sp_helppullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt Informationen zu einem oder mehreren Abonnements auf dem Abonnenten an. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helppullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @show_push = ] 'show_push' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @publisher = ] 'publisher'` Ist der Name des Remoteservers. *Publisher* ist **Sysname**, hat den Standardwert **%**, womit Informationen zu allen Verlegern zurückgegeben werden.  
  
`[ @publisher_db = ] 'publisher_db'` Ist der Name der Verlegerdatenbank. *Publisher_db* ist **Sysname**, hat den Standardwert **%**, dem alle Verlegerdatenbanken zurückgegeben.  
  
`[ @publication = ] 'publication'` Ist der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert **%**, die alle Veröffentlichungen zurückgegeben. Wenn dieser Parameter allen nur Pullabonnements mit Independent_agent entspricht = **0** zurückgegeben werden.  
  
`[ @show_push = ] 'show_push'` Ist, ob alle Pushabonnements sind, zurückgegeben werden. *Show_push*ist **nvarchar(5)**, Standardwert "false" ist, wird die keine Pushabonnements zurückgegeben.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Name des Verlegers.|  
|**Verlegerdatenbank**|**sysname**|Name der Verlegerdatenbank.|  
|**publication**|**sysname**|Name der Veröffentlichung.|  
|**independent_agent**|**bit**|Zeigt an, ob ein Verteilungs-Agent im Einzelplatzmodus für diese Veröffentlichung vorhanden ist.|  
|**Abonnementtyp**|**int**|Abonnementtyp für die Veröffentlichung.|  
|**Verteilungs-agent**|**nvarchar(100)**|Verteilungs-Agent für die Verarbeitung des Abonnements.|  
|**veröffentlichungsbeschreibung**|**nvarchar(255)**|Beschreibung der Veröffentlichung.|  
|**Zeitpunkt der letzten Aktualisierung**|**Datum**|Zeitpunkt, zu dem die Abonnementinformationen aktualisiert wurden. Dies ist eine UNICODE-Zeichenfolge aus ISO-Datum (114) + ODBC-Zeit (121). Das Format ist yyyymmdd hh:mi:sss.mmm, wobei yyyy das Jahr, mm den Monat, dd den Tag, hh die Stunde, mi die Minute, sss die Sekunden und mmm die Millisekunden angibt.|  
|**Abonnementname**|**varchar(386)**|Name des Abonnements.|  
|**transaktionszeitstempel der letzten**|**varbinary(16)**|Timestamp der letzten replizierten Transaktion.|  
|**Updatemodus**|**tinyint**|Zulässige Updatetypen.|  
|**Job_id der Verteilungs-agent**|**int**|Auftrags-ID des Verteilungs-Agents.|  
|**enabled_for_synmgr**|**int**|Zeigt an, ob das Abonnement über die Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] synchronisiert werden kann.|  
|**Abonnement-guid**|**binary(16)**|Globaler Bezeichner für die Version des Abonnements für die Veröffentlichung.|  
|**subid**|**binary(16)**|Globaler Bezeichner für ein anonymes Abonnement.|  
|**immediate_sync**|**bit**|Gibt an, ob die Synchronisierungsdateien bei jeder Ausführung des Momentaufnahme-Agents erstellt oder neu erstellt werden.|  
|**publisher login**|**sysname**|Auf dem Verleger für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendete Anmelde-ID.|  
|**das Kennwort des Verlegers**|**nvarchar(524)**|Das Kennwort (verschlüsselt), das auf dem Verleger für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendet wird.|  
|**publisher security_mode**|**int**|Auf dem Verleger implementierter Sicherheitsmodus:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1** = Windows-Authentifizierung<br /><br /> **2** = der Synchronisierungstrigger verwenden einen statischen **Sysservers** -Eintrag für einen Remoteprozeduraufruf (RPC), und *Verleger* muss definiert werden, der **Sysservers**-Tabelle als Remoteserver oder Verbindungsserver.|  
|**distributor**|**sysname**|Name des Verteilers.|  
|**distributor_login**|**sysname**|Auf dem Verteiler für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendete Anmelde-ID.|  
|**distributor_password**|**nvarchar(524)**|Kennwort (verschlüsselt) verwendet, auf dem Verteiler für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**distributor_security_mode**|**int**|Auf dem Verteiler implementierter Sicherheitsmodus:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1** = Windows-Authentifizierung|  
|**ftp_address**|**sysname**|Nur aus Gründen der Abwärtskompatibilität beibehalten|  
|**ftp_port**|**int**|Nur aus Gründen der Abwärtskompatibilität beibehalten|  
|**ftp_login**|**sysname**|Nur aus Gründen der Abwärtskompatibilität beibehalten|  
|**ftp_password**|**nvarchar(524)**|Nur aus Gründen der Abwärtskompatibilität beibehalten|  
|**alt_snapshot_folder**|**nvarchar(255)**|Der Speicherort des Momentaufnahmeordners, wenn dies nicht der standardmäßige Speicherort ist oder ein zusätzlicher Speicherort zum Standardspeicherort vorhanden ist.|  
|**working_directory**|**nvarchar(255)**|Der vollgekennzeichnete Pfad zum Verzeichnis, in das die Momentaufnahmedateien mit File Transfer Protocol (FTP) übertragen werden, wenn diese Option angegeben ist.|  
|**use_ftp**|**bit**|Abonnement abonniert die Veröffentlichung über die konfigurierten Internet- und FTP-Adressierungseigenschaften. Wenn **0**, Abonnement nicht FTP verwendet. Wenn **1**, FTP verwendet.|  
|**publication_type**|**int**|Gibt den Replikationstyp der Veröffentlichung an.<br /><br /> **0** = Transaktionsreplikation<br /><br /> **1** = momentaufnahmereplikation<br /><br /> **2** = Mergereplikation|  
|**dts_package_name**|**sysname**|Gibt den Namen des DTS-Pakets (Data Transformation Services) an.|  
|**dts_package_location**|**int**|Der Speicherort des DTS-Pakets:<br /><br /> **0** = Verteiler<br /><br /> **1** = Subscriber|  
|**offload_agent**|**bit**|Gibt an, ob der Agent remote aktiviert werden kann. Wenn **0**, der Agent nicht remote aktiviert werden.|  
|**offload_server**|**sysname**|Gibt den Netzwerknamen des Servers an, der für die Remoteaktivierung verwendet wird.|  
|**last_sync_status**|**int**|Abonnementstatus:<br /><br /> **0** = alle Aufträge werden für den start bereit.<br /><br /> **1** = ein oder mehrere Aufträge werden gestartet<br /><br /> **2** = alle Aufträge wurden erfolgreich ausgeführt.<br /><br /> **3** = mindestens ein Auftrag wird ausgeführt<br /><br /> **4** = alle Aufträge sind geplant und im Leerlauf<br /><br /> **5** = mindestens ein Auftrag versucht, führen Sie nach einem vorherigen Fehler<br /><br /> **6** = mindestens ein Auftrag konnte nicht erfolgreich ausgeführt|  
|**last_sync_summary**|**sysname**|Beschreibung der letzten Synchronisierungsergebnisse.|  
|**last_sync_time**|**datetime**|Zeitpunkt, zu dem die Abonnementinformationen aktualisiert wurden. Dies ist eine UNICODE-Zeichenfolge aus ISO-Datum (114) + ODBC-Zeit (121). Das Format ist yyyymmdd hh:mi:sss.mmm, wobei yyyy das Jahr, mm den Monat, dd den Tag, hh die Stunde, mi die Minute, sss die Sekunden und mmm die Millisekunden angibt.|  
|**job_login**|**nvarchar(512)**|Ist das Windows-Konto unter dem der Verteilungs-Agent ausgeführt wird, der zurückgegeben wird, im Format *Domäne*\\*Benutzername*.|  
|**job_password**|**sysname**|Aus Sicherheitsgründen den Wert "**\*\*\*\*\*\*\*\*\*\***" ist immer zurückgegeben.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helppullsubscription** wird bei der Momentaufnahme- und Transaktionsreplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** -Serverrolle sein oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_helppullsubscription** .  
  
## <a name="see-also"></a>Siehe auch  
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
