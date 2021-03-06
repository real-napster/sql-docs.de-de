---
title: Sys. resource_usage (Azure SQL-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_usage_TSQL
- resource_usage
- sys.resource_usage
- resource_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- resource_usage
- sys.resource_usage
ms.assetid: b90147a3-fd8e-408e-961d-5c7000e068ad
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 9b0e16279615bf102c916793439d440211939839
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013761"
---
# <a name="sysresourceusage-azure-sql-database"></a>sys.resource_usage (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]
>  Diese Funktion befindet sich in einem Vorschauzustand. Erstellen Sie keine Abhängigkeit von der spezifischen Implementierung dieser Funktion, da die Funktion in zukünftigen Versionen ggf. geändert oder entfernt werden kann.  
> 
>  Im Vorschauzustand kann das [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]-Vorgangsteam die Datensammlung für diese DMV deaktivieren und aktivieren:  
> 
>  -   Wenn sie aktiviert ist, gibt die DMV aktuelle Daten zurück, während diese aggregiert werden.  
> -   Bei einer Deaktivierung gibt die DMV Vergangenheitsdaten zurück, die möglicherweise veraltet sind.  
  
 Stellt eine stündliche Zusammenfassung der Ressourcenverwendungsdaten für die Benutzerdatenbanken auf dem aktuellen Server bereit. Vergangenheitsdaten werden 90 Tage lang beibehalten.  
  
 Für jede Benutzerdatenbank gibt es fortlaufend eine Zeile für jede Stunde. Auch wenn die Datenbank während dieser Stunde im Leerlauf war, ist eine Zeile vorhanden. Der Wert usage_in_seconds für diese Datenbank ist dann 0. Für die Speicherplatzverwendung und die SKU-Informationen wird entsprechend ein Rollup für die Stunde ausgeführt.  
  
|Spalte|Datentyp|Description|  
|-------------|---------------|-----------------|  
|Uhrzeit|**datetime**|Uhrzeit (UTC) in Stundeninkrementen.|  
|database_name|**nvarchar**|Name der Benutzerdatenbank.|  
|sku|**nvarchar**|Name der SKU Folgende Werte sind möglich:<br /><br /> Web<br /><br /> Business<br /><br /> Standard<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|Summe der in der Stunde verwendeten CPU-Zeit.<br /><br /> Hinweis: Diese Spalte ist für V11 veraltet und gilt nicht für V12. **Wert ist immer auf 0 festgelegt.**|  
|storage_in_megabytes|**decimal**|Die maximale Speichergröße für die Stunde, einschließlich von Datenbankdaten, Indizes, gespeicherten Prozeduren und Metadaten.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzerrollen, die berechtigt sind, eine Verbindung mit der virtuellen **master** -Datenbank herzustellen, haben Zugriff auf diese Sicht.  
  
  
