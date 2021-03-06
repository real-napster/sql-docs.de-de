---
title: Erstellen des Datenbankassistenten (Konfigurations-Manager für Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ce2b909ea7853a0a77d42f8c14a510b529f4ae88
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62765873"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>Datenbank erstellen (Assistent im Konfigurations-Manager für Master Data Services)
  Verwenden Sie den Assistenten **Datenbank erstellen** , um eine [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank anzulegen.  
  
## <a name="database-server"></a>Datenbankserver  
 Geben Sie Informationen für die Verbindung mit einer lokalen oder Remoteinstanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] an, auf der die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank gehostet werden soll. Um eine Verbindung mit einer Remoteinstanz herzustellen, müssen Sie diese für Remoteverbindungen einrichten.  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**SQL Server-Instanz**|Geben Sie den Namen der [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] -Instanz an, auf der die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank gehostet werden soll. Dies kann eine Standardinstanz oder eine benannte Instanz auf einem lokalen oder Remotecomputer sein. Geben Sie die Informationen wie folgt an:<br /><br /> Einen Punkt (.) für die Verbindung mit der Standardinstanz auf dem lokalen Computer.<br /><br /> Den Servernamen oder die IP-Adresse für die Verbindung mit der Standardinstanz auf dem angegebenen lokalen oder Remotecomputer.<br /><br /> Der Servername oder die IP-Adresse und der Instanzname für die Verbindung mit der benannten Instanz auf dem angegebenen lokalen oder Remotecomputer. Geben Sie diese Informationen im Format *Servername*\\*Instanzname*an.|  
|**Authentifizierungstyp**|Wählen Sie den Authentifizierungstyp aus, der für die Verbindung mit der angegebenen SQL Server-Instanz verwendet werden soll. Die Anmeldeinformationen, mit denen Sie die Verbindung herstellen, müssen der Serverrolle **sysadmin** der angegebenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz angehören. Weitere Informationen zur Rolle „sysadmin“ finden Sie unter [Rollen auf Serverebene](../relational-databases/security/authentication-access/server-level-roles.md). Mögliche Authentifizierungstypen:<br /><br /> **Aktueller Benutzer – Integrierte Sicherheit** Verwendet die integrierte Windows-Authentifizierung, um eine Verbindung mit den Anmeldeinformationen des aktuellen Windows-Benutzerkontos herzustellen. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] verwendet die Windows-Anmeldeinformationen des Benutzers, der am Computer angemeldet ist und die Anwendung geöffnet hat. Sie können keine anderen Windows-Anmeldeinformationen in der Anwendung angeben. Wenn Sie die Verbindung mit anderen Windows-Anmeldeinformationen herstellen möchten, müssen Sie sich als der betreffende Benutzer am Computer anmelden und [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]öffnen.<br /><br /> **SQL Server-Konto:** Verwendet ein SQL Server-Konto für die Verbindung. Wenn Sie diese Option auswählen, sind die Felder **Benutzername** und **Kennwort** aktiviert, und Sie müssen Anmeldeinformationen für ein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konto auf der betreffenden [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz angeben.|  
|**Benutzername**|Geben Sie den Namen des Benutzerkontos an, unter dem eine Verbindung mit der angegebenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz hergestellt wird. Das Konto muss der Rolle **sysadmin** auf der angegebenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz angehören:<br /><br /> Wenn der **Authentifizierungstyp** auf **Aktueller Benutzer – Integrierte Sicherheit**festgelegt wurde, ist das Feld **Benutzername** schreibgeschützt und zeigt den Namen des Windows-Benutzerkontos an, das auf dem Computer angemeldet ist.<br /><br /> Wenn der **Authentifizierungstyp** auf **SQL Server-Konto**festgelegt wurde, ist das Feld **Benutzername** aktiviert, und Sie müssen Anmeldeinformationen für ein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konto auf der betreffenden [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz angeben.|  
|**Kennwort**|Geben Sie das Kennwort ein, das dem Benutzerkonto zugeordnet ist.<br /><br /> Wenn der **Authentifizierungstyp** auf **Aktueller Benutzer – Integrierte Sicherheit** festgelegt wurde, ist das Feld **Kennwort** schreibgeschützt, und die Verbindung wird mit Anmeldeinformationen des angegebenen Windows-Benutzerkontos hergestellt.<br /><br /> Wenn der **Authentifizierungstyp** auf **SQL Server-Konto**festgelegt wurde, ist das Feld **Kennwort** aktiviert, und Sie müssen das Kennwort angeben, das dem betreffenden Benutzerkonto zugeordnet ist.|  
|**Verbindung testen**|Überprüfen Sie, ob unter dem angegebenen Benutzerkonto eine Verbindung mit der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz hergestellt werden kann und ob das Konto über eine Berechtigung zum Erstellen der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank für diese Instanz verfügt. Wenn Sie **Verbindung testen**nicht aktivieren, wird der Test ausgeführt, sobald Sie auf **Weiter**klicken.|  
  
## <a name="database"></a>Datenbank  
 Geben Sie einen Datenbanknamen und Sortierungsoptionen für die neue Datenbank an. Sortierungen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bieten Sortierregeln und die Berücksichtigung von Groß-/Kleinschreibung und Akzenten für die Daten. Sortierungen, die mit Zeichendatentypen wie char und varchar verwendet werden, geben die Codepage und die entsprechenden Zeichen vor, die für den jeweiligen Datentyp dargestellt werden können. Weitere Informationen zur Datenbanksortierung finden Sie unter [Sortierung und Unicode-Unterstützung](../relational-databases/collations/collation-and-unicode-support.md).  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Datenbankname**|Geben Sie einen Namen für die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank an.|  
|**SQL Server-Standardsortierung**|Aktivieren Sie diese Option, um die aktuelle Datenbanksortierungseinstellung der angegebenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz für die neue Datenbank zu verwenden.|  
|**Windows-Sortierung**|Geben Sie die Einstellungen der Windows-Sortierung an, die für die neue Datenbank verwendet werden sollen. Windows-Sortierungen definieren Regeln zum Speichern von Zeichendaten, wobei das zugeordnete Windows-Gebietsschema berücksichtigt wird. Weitere Informationen zu Windows-Sortierungen und den zugehörigen Optionen finden Sie unter [Name der Windows-Sortierung&#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql).<br /><br /> Hinweis: Die Liste **Windows-Sortierung** und zugehörige Optionen werden erst aktiviert, nachdem Sie das Kontrollkästchen **SQL Server-Standardsortierung** deaktiviert haben.|  
  
## <a name="administrator-account"></a>Administratorkonto  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Benutzername**|Geben Sie ein Domänenbenutzerkonto an, das als [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Systemadministrator konfiguriert werden soll. Für alle [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Webanwendungen, die diese Datenbank, die diesem Benutzer zugeordnete können alle Modelle und alle Daten in sämtlichen Funktionsbereichen aktualisieren. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](administrators-master-data-services.md)zuzugreifen.|  
  
## <a name="summary"></a>Zusammenfassung  
 Zeigt eine Zusammenfassung der ausgewählten Optionen an. Überprüfen Sie die Auswahl, und klicken Sie dann auf **Weiter** , um die Datenbank mit den angegebenen Einstellungen zu erstellen.  
  
## <a name="progress-and-finish"></a>Status und Fertig stellen  
 Zeigt den Status des Erstellungsprozesses an. Nachdem die Datenbank erstellt wurde, klicken Sie auf **Fertig stellen** , um den Datenbank-Assistenten zu schließen und zur Seite **Datenbanken** zurückzukehren. Die neue Datenbank ist ausgewählt, und Sie können ihre Systemeinstellungen anzeigen und ändern.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankkonfiguration &#40;Seite im Konfigurations-Manager für Master Data Services&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Einrichten der Datenbank und Website für Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Datenbankanforderungen &#40;Master Data Services&#41;](install-windows/database-requirements-master-data-services.md)  
  
  
