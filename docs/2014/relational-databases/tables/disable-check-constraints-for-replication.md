---
title: Deaktivieren von CHECK-Einschränkungen für die Replikation | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: af98fc70-24dd-4bd3-a0a3-f701dfa67b2c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 957fcd77a6443cf2e23be8965a68823085db870c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62762196"
---
# <a name="disable-check-constraints-for-replication"></a>Deaktivieren von CHECK-Einschränkungen für die Replikation
  CHECK-Einschränkungen können in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]deaktiviert werden. Sie können CHECK-Einschränkungen für die Replikation auch explizit deaktivieren. Dies ist vor allem nützlich, wenn Sie Daten aus einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]veröffentlichen.  
  
> [!NOTE]  
>  Wenn eine Tabelle mittels Replikation veröffentlicht wird, werden CHECK-Einschränkungen automatisch für die von Replikations-Agents ausgeführten Vorgänge deaktiviert. Wenn ein Replikations-Agent eine Einfügung, ein Update oder eine Löschung auf einem Abonnenten ausführt, wird die Einschränkung nicht überprüft; wenn ein Benutzer eine Einfügung, ein Update oder eine Löschung ausführt, wird die Einschränkung überprüft. Die Einschränkung wird für den Replikations-Agent deaktiviert, da die Einschränkung bereits auf dem Verleger überprüft wurde, als die Daten ursprünglich eingefügt, aktualisiert oder gelöscht wurden. Weitere Informationen finden Sie unter [Angeben von Schemaoptionen](../replication/publish/specify-schema-options.md).  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>So deaktivieren Sie eine CHECK-Einschränkung für die Replikation  
  
1.  Erweitern Sie im **Objekt-Explorer**die Tabelle mit der zu ändernden Einschränkung, und erweitern Sie dann den Ordner **Einschränkungen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die zu ändernde CHECK-Einschränkung, und klicken Sie dann auf **Ändern**.  
  
3.  Wählen Sie im Dialogfeld **Einschränkungen überprüfen** unter **Tabellen-Designer**für die Option **Für Replikation erzwingen** den Wert **Nein**aus.  
  
4.  Klicken Sie auf **Schließen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>So deaktivieren Sie eine CHECK-Einschränkung für die Replikation  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im Beispiel wird eine Tabelle mit einer IDENTITY-Spalte und einer CHECK-Einschränkung für die Tabelle erstellt. Anschließend wird die Einschränkung gelöscht und mit der NOT FOR REPLICATION-Klausel neu erstellt.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.doc_exd (column_a int IDENTITY (1,1)   
    CONSTRAINT exd_check CHECK (column_a > 1))   
  
    ALTER TABLE dbo.doc_exd   
    DROP CONSTRAINT exd_check;   
    GO  
    ALTER TABLE dbo.doc_exd    
    ADD CONSTRAINT exd_check CHECK NOT FOR REPLICATION (column_a > 1);  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="TsqlExample"></a>   
## <a name="see-also"></a>Siehe auch  
 [Angeben von Schemaoptionen](../replication/publish/specify-schema-options.md)  
  
  
