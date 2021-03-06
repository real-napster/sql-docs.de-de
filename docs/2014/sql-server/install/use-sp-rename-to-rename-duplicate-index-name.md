---
title: Verwenden Sie Sp_rename, benennen Sie die doppelten Indexnamen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- table names [SQL Server]
- duplicate table names
- index names [SQL Server]
- sp_rename
- duplicate index names
ms.assetid: ee66c7a5-eb6d-4fcf-970c-ab099d78c8d9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc6b4ec763457996309caf1884829638367e9b18
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582853"
---
# <a name="use-sprename-to-rename-duplicate-index-name"></a>Verwenden Sie bei doppelten Indexnamen 'sp_rename' zum Umbenennen
  Der Upgrade Advisor hat doppelte Tabellen- oder Sichtindexnamen erkannt. Vor dem Upgrade müssen Sie die Indizes umbenennen, um Duplikate zu entfernen.  
  
## <a name="component"></a>Komponente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Korrekturmaßnahme  
  
1.  Suchen Sie die doppelten Indizes durch Ausführen der folgenden Abfrage.  
  
    ```  
    SELECT DISTINCT OBJECT_NAME(o.id), name  
    FROM sysindexes as o  
    WHERE EXISTS   
        (SELECT name FROM sysindexes  as i  
          WHERE i.id = o.id  
          AND i.name = o.name and i.indid < o.indid);  
    ```  
  
2.  Verwendung **Sp_rename** ändern Sie einen der Indexnamen. Da die Indexnamen identisch sind, können Sie nicht bestimmen, welcher Index umbenannt wird. Durch diesen Schritt können Sie die Indizes unterscheiden.  
  
    ```  
    EXEC sp_rename N'table_name.index_name', N'new_index_name', N'INDEX'  
    ```  
  
3.  Überprüfen Sie durch Ausführen der folgenden Abfrage, welcher Index umbenannt wurde. Diese Abfrage gibt alle Indizes (einschließlich der Schlüsselspaltennamen) für die angegebene Tabelle oder Sicht zurück.  
  
    ```  
    SELECT i.name AS IndexName, c.name AS ColumnName, ik.colid, ik.keyno  
    FROM sysindexes i  
    JOIN sysindexkeys ik ON i.id = ik.id and i.indid = ik.indid   
    JOIN syscolumns c ON c.id = ik.id and ik.colid = c.colid  
    WHERE i.id = OBJECT_ID('table_or_view_name')  
    ```  
  
4.  Verwenden Sie bei Bedarf **Sp_rename** erneut aus, um die Indexnamen zu korrigieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-Engine-Upgrade-Probleme](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;neu&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
