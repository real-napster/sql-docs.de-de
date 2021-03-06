---
title: Sp_set_firewall_rule (Azure SQL-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: a096814c7d037fe517614e2701d5a821edcaa053
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024691"
---
# <a name="spsetfirewallrule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Erstellt oder aktualisiert die Firewalleinstellungen auf Serverebene für den [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server. Diese gespeicherte Prozedur ist nur verfügbar, in der master-Datenbank in die prinzipalanmeldung auf Serverebene oder die zugewiesene Azure Active Directory-Dienstprinzipal.  
  
  
## <a name="syntax"></a>Syntax  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 In der folgende Tabelle veranschaulicht die unterstützten Argumente und Optionen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Name|Datatype|Description|  
|----------|--------------|-----------------|  
|[@name =] 'Name'|**NVARCHAR(128)**|Der verwendete Name, um die Firewalleinstellung auf Serverebene zu beschreiben und von anderen zu unterscheiden.|  
|[@start_ip_address =] "Start_ip_address"|**VARCHAR(50)**|Die niedrigste IP-Adresse im Bereich der Firewalleinstellung auf Serverebene. IP-Adressen, die gleich oder größer dieser IP-Adresse sind, können versuchen, eine Verbindung mit dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server herzustellen. Die niedrigste mögliche IP-Adresse ist `0.0.0.0`.|  
|[@end_ip_address =] "End_ip_address"|**VARCHAR(50)**|Die höchste IP-Adresse im Bereich der Firewalleinstellung auf Serverebene. IP-Adressen, die kleiner oder gleich dieser IP-Adresse sind, können versuchen, eine Verbindung mit dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server herzustellen. Die höchste mögliche IP-Adresse ist `255.255.255.255`.<br /><br /> Hinweis: Azure-Verbindungsversuche sind zulässig, wenn sowohl dieses Feld und die *Start_ip_address* Feld `0.0.0.0`.|  
  
## <a name="remarks"></a>Hinweise  
 Die Namen der Firewalleinstellungen auf Serverebene müssen eindeutig sein. Wenn der Name der für die gespeicherte Prozedur bereitgestellten Einstellung bereits in der Tabelle mit den Firewalleinstellungen vorhanden ist, werden die Start- und End-IP-Adressen aktualisiert. Andernfalls wird eine neue Firewalleinstellung auf Serverebene erstellt.  
  
 Beim Hinzufügen, in dem die erste und letzte IP-Adressen gleich sind, einer firewalleinstellung auf Serverebene `0.0.0.0`, aktivieren Sie den Zugriff auf Ihre [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Server von Azure. Geben Sie einen Wert für die *Namen* Parameter, mit denen Sie denken Sie daran, welchem Zweck die firewalleinstellung auf Serverebene dient.  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] werden Anmeldedaten, die für die Authentifizierung einer Verbindung und Firewallregeln auf Serverebene erforderlich sind, über einen gewissen Zeitraum in jeder Datenbank gespeichert. Dieser Cache wird regelmäßig aktualisiert. Führen Sie [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md) aus, um das Aktualisieren der Authentifizierungsdatenbank zu erzwingen und sicherzustellen, dass die Datenbank über die aktuelle Version der Anmeldungstabelle verfügt.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur die Server serverebenenprinzipal-Anmeldung während des Bereitstellungsprozesses erstellt oder ein Azure Active Directory-Dienstprinzipal, der als Administrator erstellen oder Ändern von Firewallregeln auf Serverebene zugewiesen. Der Benutzer muss mit der master-Datenbank, führen Sie "Sp_set_firewall_rule" verbunden werden.  
  
## <a name="examples"></a>Beispiele  
 Der folgende Code erstellt eine Firewall auf Serverebene, die Einstellung `Allow Azure` , die Zugriff über Azure ermöglicht. Führen Sie die folgenden, in der virtuellen Masterdatenbank her.  
  
```  
-- Enable Windows Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 Der folgende Code erstellt eine Firewalleinstellung auf Serverebene namens `Example setting 1` nur für die IP-Adresse `0.0.0.2`. Anschließend wird die `sp_set_firewall_rule` gespeicherte Prozedur erneut aufgerufen, um die End-IP-Adresse zu aktualisieren `0.0.0.4`, Firewall-Einstellungen. Erstellt einen Bereich der IP-Adressen ermöglichen `0.0.0.2`, `0.0.0.3`, und `0.0.0.4` Zugriff auf den Server.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Azure SQL-Datenbankfirewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Vorgehensweise: Konfigurieren der Firewalleinstellungen (Azure SQL-Datenbank)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [Sys. firewall_rules &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
