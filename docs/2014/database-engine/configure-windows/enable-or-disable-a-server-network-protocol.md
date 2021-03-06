---
title: Aktivieren oder Deaktivieren eines Servernetzwerkprotokoll | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], disabling
- remote connections [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], disabling using Configuration Manager
- disabling network protocols, Configuration Manager
- network protocols [SQL Server], enabling
- enabling network protocols, Configuration Manager
- surface area configuration [SQL Server], connection protocols
- connections [SQL Server], enabling remote using Configuration Manager
ms.assetid: ec5ccb69-61c9-4576-8843-014b976fd46e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 17b4052b8842225d729bc8de996a7b0649f85a59
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640513"
---
# <a name="enable-or-disable-a-server-network-protocol"></a>Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls
  Alle Netzwerkprotokolle werden vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup installiert, sie können jedoch aktiviert oder nicht aktiviert werden. In diesem Thema wird beschrieben, wie mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Configuration Manager oder PowerShell ein Servernetzwerkprotokoll in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert oder deaktiviert wird. [!INCLUDE[ssDE](../../includes/ssde-md.md)] muss beendet und neu gestartet werden, damit die Änderung wirksam wird.  
  
> [!IMPORTANT]  
>  Während des Setups von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] wird eine Anmeldung für die Gruppe BUILTIN\Users hinzugefügt. Dies ermöglicht allen authentifizierten Benutzern des Computers den Zugriff auf die Instanz von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] als Element der öffentlichen Rolle. Die BUILTIN\Users-Anmeldung kann sicher entfernt werden, um den [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Zugriff auf Computerbenutzer zu beschränken, die eigene Logins besitzen oder Mitglieder anderer Windows-Gruppen mit Logins sind.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- und [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen TLS 1.0 und SSL 3.0. Wenn Sie ein anderes Protokoll (beispielsweise TLS 1.1 oder TLS 1.2) erzwingen, indem Sie Änderungen an der SChannel-Betriebssystemebene vornehmen, können Sie möglicherweise keine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen.  
  
 **In diesem Thema**  
  
-   **So aktivieren oder deaktivieren Sie ein Servernetzwerkprotokoll mit:**  
  
     [SQL Server-Konfigurations-Manager](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### <a name="to-enable-a-server-network-protocol"></a>So aktivieren Sie ein Server-Netzwerkprotokoll  
  
1.  Erweitern Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager im Konsolenbereich **SQL Server-Netzwerkkonfiguration**.  
  
2.  Klicken Sie im Konsolenbereich auf **Protokolle für** *\<Instanzname>*.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf das zu ändernde Protokoll, und klicken Sie dann auf **Aktivieren** oder **Deaktivieren**.  
  
4.  Klicken Sie im Konsolenbereich auf **SQL Server-Dienste**.  
  
5.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server (***\<Instanzname>***)**, und klicken Sie dann auf **Neu starten**, um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst zu beenden und neu zu starten.  
  
##  <a name="PowerShellProcedure"></a> SQL Server PowerShell  
  
#### <a name="to-enable-a-server-network-protocol-using-powershell"></a>So aktivieren Sie ein Server-Netzwerkprotokoll mit PowerShell  
  
1.  Öffnen Sie eine Eingabeaufforderung unter Administratorberechtigungen.  
  
2.  Starten Sie Windows PowerShell 2.0 aus der Taskleiste, oder klicken Sie auf "Start", auf "Alle Programme", auf "Zubehör", auf "Windows PowerShell" und dann auf "Windows PowerShell".  
  
3.  Importieren der **Sqlps** -Modul durch eingeben `Import-Module "sqlps"`  
  
4.  Führen Sie die folgenden Anweisungen aus, um die Protokolle für TCP und Named Pipes zu aktivieren. Ersetzen Sie `<computer_name>` mit dem Namen des Computers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wird. Wenn Sie eine benannte Instanz konfigurieren, ersetzen Sie `MSSQLSERVER` durch den Namen der Instanz.  
  
     Um die Protokolle zu deaktivieren, legen Sie die `IsEnabled` -Eigenschaften auf `$false`fest.  
  
    ```  
    $smo = 'Microsoft.SqlServer.Management.Smo.'  
    $wmi = new-object ($smo + 'Wmi.ManagedComputer').  
  
    # List the object properties, including the instance names.  
    $Wmi  
  
    # Enable the TCP protocol on the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    $Tcp = $wmi.GetSmoObject($uri)  
    $Tcp.IsEnabled = $true  
    $Tcp.Alter()  
    $Tcp  
  
    # Enable the named pipes protocol for the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Np']"  
    $Np = $wmi.GetSmoObject($uri)  
    $Np.IsEnabled = $true  
    $Np.Alter()  
    $Np  
    ```  
  
#### <a name="to-configure-the-protocols-for-the-local-computer"></a>So konfigurieren Sie die Protokolle für den lokalen Computer  
  
-   Wenn das Skript lokal ausgeführt wird und den lokalen Computer konfiguriert, kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell das Skript flexibler gestalten, indem der lokale Computernamen dynamisch festgelegt wird. Um den lokalen Computernamen abzurufen, ersetzen Sie die Zeile, die die `$uri` -Variable festlegt, mit der folgenden Zeile.  
  
    ```  
    $uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    ```  
  
#### <a name="to-restart-the-database-engine-by-using-sql-server-powershell"></a>So starten Sie die Datenbank-Engine mit SQL Server PowerShell neu  
  
-   Nachdem Sie Protokolle aktiviert oder deaktiviert haben, müssen Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)] beenden und neu starten, damit die Änderung wirksam wird. Führen Sie die folgenden Anweisungen aus, um die Standardinstanz mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell zu beenden und zu starten. Um eine benannte Instanz zu beenden und zu starten, ersetzen Sie `'MSSQLSERVER'` durch `'MSSQL$<instance_name>'`.  
  
    ```  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\<computer_name>  
    $Wmi = (get-item .).ManagedComputer  
    # Get a reference to the default instance of the Database Engine.  
    $DfltInstance = $Wmi.Services['MSSQLSERVER']  
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Start the service again.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache and display the state of the service.  
    $DfltInstance.Refresh(); $DfltInstance  
    ```  
  
  
