---
title: Aktivieren von verschlüsselten Verbindungen zur Datenbank-Engine | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/09/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 28a2c9bd527fb4996730630a6121d205fbaebf04
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2019
ms.locfileid: "59429346"
---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>Aktivieren von verschlüsselten Verbindungen zur Datenbank-Engine
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie verschlüsselte Verbindungen für eine Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] durch Angeben eines Zertifikats für die [!INCLUDE[ssDE](../../includes/ssde-md.md)] mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers aktivieren können. Für den Servercomputer muss ein Zertifikat bereitgestellt worden sein, und der Clientcomputer muss so eingerichtet sein, dass er die Stammzertifizierungsstelle des Zertifikats als vertrauenswürdig einstuft. Zertifikate werden bereitgestellt, indem sie mithilfe eines Importvorgangs in Windows installiert werden.  
  
 Das Zertifikat muss für die **Serverauthentifizierung**ausgegeben sein. Der Name des Zertifikats muss der vollqualifizierte Domänenname (FQDN) des Computers sein.  
  
 Zertifikate werden lokal für diesen Benutzer auf dem Computer gespeichert. Sie müssen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Configuration Manager mit einem Konto mit lokalen Administratorberechtigungen ausführen, um ein Zertifikat zu installieren, das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden soll.

 Der Client muss in der Lage sein, den Besitzer des vom Server verwendeten Zertifikats zu überprüfen. Wenn der Client über das Zertifikat für öffentliche Schlüssel der Zertifizierungsstelle verfügt, die das Serverzertifikat signiert hat, sind keine weiteren Konfigurationsschritte erforderlich. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows enthält die Zertifikate für öffentliche Schlüssel von vielen Zertifizierungsstellen. Wenn das Serverzertifikat von einer öffentlichen oder privaten Zertifizierungsstelle signiert wurde, für die der Client kein öffentliches Schlüsselzertifikat besitzt, müssen Sie das Zertifikat für öffentliche Schlüssel der Zertifizierungsstelle installieren, die das Serverzertifikat signiert hat.  
  
> [!NOTE]  
> Wenn Sie die Verschlüsselung bei einem Failovercluster verwenden möchten, müssen Sie das Serverzertifikat mit dem vollqualifizierten DNS-Namen des virtuellen Servers auf allen Knoten im Failovercluster installieren. Wenn Sie z.B. über einen Cluster mit zwei Knoten verfügen, wobei die Knotennamen test1.*\<Ihr_Unternehmen>*.com und test2.*\<Ihr_Unternehmen>*.com lauten, und ein virtueller Server den Namen „virtsql“ trägt, müssen Sie ein Zertifikat für virtsql.*\<Ihr_Unternehmen>*.com auf beiden Knoten installieren. Sie können den Wert der Option **ForceEncryption** auf **Yes** (Ja) festlegen.

> [!NOTE]
> Wenn Sie eine verschlüsselte Verbindung für einen Azure Search-Indexer zu SQL Server auf einer Azure-VM erstellen wollen, finden Sie weitere Informationen unter [Konfigurieren einer Verbindung eines Azure Search-Indexers mit SQL Server auf einer Azure-VM](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/). 

## <a name="certificate-requirements"></a>Zertifikatanforderungen

Damit in SQL Server ein SSL-Zertifikat geladen wird, müssen für das Zertifikat folgende Bedingungen erfüllt sein:

- Das Zertifikat muss sich im Zertifikatspeicher des lokalen Computers oder im Zertifikatspeicher des aktuellen Benutzers befinden.
- Das SQL Server-Dienstkonto muss über die erforderliche Berechtigung für den Zugriff auf das SSL-Zertifikat verfügen.
- Die aktuelle Systemzeit muss nach der **Valid from**-Eigenschaft und vor der „Valid to“-Eigenschaft des Zertifikats liegen.
- Das Zertifikat muss für die Serverauthentifizierung vorgesehen sein. Dazu muss für die **Enhanced Key Usage**-Eigenschaft des Zertifikats **Server Authentification (1.3.6.1.5.5.7.3.1)** angegeben sein.
- Das Zertifikat muss mit der **KeySpec**-Option von **AT_KEYEXCHANGE** erstellt werden. Normalerweise enthält die Schlüsselverwendungseigenschaft (**KEY_USAGE**) des Zertifikats auch die Schlüsselverschlüsselung (**CERT_KEY_ENCIPHERMENT_KEY_USAGE**).
- Mit der **Subject**-Eigenschaft des Zertifikats muss angegeben werden, dass der allgemeine Name (Common Name, CN) mit dem Hostnamen oder dem vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des Servercomputers übereinstimmt. Wenn SQL Server in einem Failovercluster ausgeführt wird, muss der allgemeine Name mit dem Hostnamen oder FQDN des virtuellen Servers übereinstimmen, und die Zertifikate müssen auf allen Knoten im Failovercluster bereitgestellt werden.
- SQL Server 2008 R2 und SQL Server 2008 R2 Native Client unterstützen Platzhalterzertifikate. Andere Clients unterstützen möglicherweise keine Platzhalterzertifikate. Weitere Informationen finden Sie in der Clientdokumentation und in [KB258858](http://support.microsoft.com/kb/258858).

## <a name="to-provision-install-a-certificate-on-the-server"></a>So stellen Sie ein Zertifikat auf dem Server bereit bzw. installieren Sie ein Zertifikat  

> [!NOTE]
> Informationen zum Hinzufügen eines Zertifikats auf einem einzelnen Server finden Sie unter [Certificate Management (SQL Server Configuration Manager) (Zertifikatverwaltung (SQL Server-Konfigurations-Manager))](manage-certificates.md).
  
1. Klicken Sie im Menü **Start** auf **Ausführen**, geben Sie in das Feld **Öffnen** den Wert **MMC** ein, und klicken Sie dann auf **OK**.  
  
2. Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3. Klicken Sie im Dialogfeld **Snap-In hinzufügen/entfernen** auf **Hinzufügen**.  
  
4. Klicken Sie im Dialogfeld **Eigenständiges Snap-In hinzufügen** auf **Zertifikate**, und klicken Sie dann auf **Hinzufügen**.  
  
5. Klicken Sie im **Dialogfeld Zertifikate-Snap-In** auf **Computerkonto**, und klicken Sie dann auf **Fertig stellen**.  
  
6. Klicken Sie im Dialogfeld **Eigenständiges Snap-In hinzufügen** auf **Schließen**.  
  
7. Klicken Sie im Dialogfeld **Snap-In hinzufügen/entfernen** auf **OK**.  
  
8. Erweitern Sie im Dialogfeld **Zertifikate-Snap-In** die Option **Zertifikate**, erweitern Sie **Eigene Zertifikate**, und klicken Sie dann mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie anschließend auf **Importieren**.  

9. Klicken Sie mit der rechten Maustaste auf das importierte Zertifikat, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Privatschlüssel verwalten**. Fügen Sie im Dialogfeld **Sicherheit** die Leseberechtigung für das Benutzerkonto hinzu, das vom SQL Server-Dienstkonto verwendet wird.  
  
10. Ergänzen Sie die Angaben im **Zertifikatimport-Assistenten**, um dem Computer ein Zertifikat hinzuzufügen, und schließen Sie dann die MMC-Konsole. Weitere Informationen zum Hinzufügen von Zertifikaten zu einem Computer finden Sie in der Windows-Dokumentation.  
  
## <a name="to-provision-install-a-certificate-across-multiple-servers"></a>So stellen Sie ein Zertifikat auf mehreren Servern bereit bzw. installieren Sie ein Zertifikat

> [!NOTE]
> Informationen zum Hinzufügen eines Zertifikats auf mehreren Servern finden Sie unter [Certificate Management (SQL Server Configuration Manager) (Zertifikatverwaltung (SQL Server-Konfigurations-Manager))](manage-certificates.md).

## <a name="to-export-the-server-certificate"></a>So exportieren Sie das Serverzertifikat  
  
1. Erweitern Sie im **Zertifikate** -Snap-In den Ordner **Zertifikate** / **Eigene Zertifikate** , klicken Sie mit der rechten Maustaste auf das **Zertifikat**, zeigen Sie auf **Alle Tasks**, und klicken Sie dann auf **Exportieren**.  
  
2. Führen Sie den **Zertifikatexport-Assistenten**aus, und speichern Sie die Zertifikatsdatei in einem geeigneten Speicherort.  
  
## <a name="to-configure-the-server-to-force-encrypted-connections"></a>So konfigurieren Sie den Server zum Erzwingen verschlüsselter Verbindungen  
  
1. Erweitern Sie im **SQL Server Configuration Manager** den Eintrag **SQL Server-Netzwerkkonfiguration**, klicken Sie mit der rechten Maustaste auf **Protokolle für** _\<Serverinstanz>_, und wählen Sie dann **Eigenschaften**.  
  
2. Wählen Sie im Dialogfeld **Eigenschaften** von **Protokolle für** _\<Instanzname>_ auf der Registerkarte **Zertifikat** das gewünschte Zertifikat aus der Dropdownliste für das Feld **Zertifikat** aus, und klicken Sie dann auf **OK**.  
  
3. Aktivieren Sie auf der Registerkarte **Flags** im Feld **ForceEncryption** die Option **Ja**, und klicken Sie dann auf **OK** , um das Dialogfeld zu schließen.  
  
4. Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst neu.  

> [!NOTE]
> Konfigurieren Sie den Client so, dass verschlüsselte Verbindungen angefordert werden, um eine sichere Verbindung zwischen Client und Server zu gewährleisten. Weitere Informationen finden Sie [weiter unten in diesem Artikel](#to-configure-the-client-to-request-encrypted-connections).

### <a name="wildcard-certificates"></a>Platzhalterzertifikate

Ab [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 unterstützen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Platzhalterzertifikate. Andere Clients unterstützen möglicherweise keine Platzhalterzertifikate. Weitere Informationen finden Sie in der Clientdokumentation. Platzhalterzertifikate können nicht mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ausgewählt werden. Sie müssen den Registrierungsschlüssel `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` bearbeiten und den Fingerabdruck des Zertifikats ohne Leerraum zum Wert des **Zertifikats** hinzufügen, um ein Platzhalterzertifikat zu verwenden.  

> [!WARNING]  
> [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry-md.md)]  

## <a name="to-configure-the-client-to-request-encrypted-connections"></a>So konfigurieren Sie den Client zum Anfordern verschlüsselter Verbindungen  

1. Kopieren Sie entweder das Originalzertifikat oder die exportierte Zertifikatsdatei auf den Clientcomputer.  
  
2. Installieren Sie auf dem Clientcomputer mithilfe des **Zertifikate** -Snap-Ins entweder das Stammzertifikat oder die exportierte Zertifikatsdatei.  
  
3. Klicken Sie im Konsolenbereich mit der rechten Maustaste auf **SQL Server Native Client-Konfiguration**, und klicken Sie dann auf **Eigenschaften**.  
  
4. Klicken Sie auf der Seite **Flags** im Feld **Protokollverschlüsselung erzwingen** auf **Ja**.  
  
## <a name="to-encrypt-a-connection-from-sql-server-management-studio"></a>So verschlüsseln Sie eine Verbindung in SQL Server Management Studio  
  
1. Klicken Sie auf der Symbolleiste des Objekt-Explorers auf **Verbinden**, und klicken Sie dann auf **Datenbank-Engine**.  
  
2. Vervollständigen Sie im Dialogfeld **Verbindung mit Server herstellen** die Verbindungseinstellungen, und klicken Sie dann auf **Optionen**.  
  
3. Klicken Sie auf der Registerkarte **Verbindungseigenschaften** auf **Verbindung verschlüsseln**.  
  
## <a name="see-also"></a>Weitere Informationen

[TLS 1.2-Unterstützung für Microsoft SQL Server](https://support.microsoft.com/kb/3135244)