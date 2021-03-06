---
title: Angeben der Anmelde- und Verbindungsinformationen für Berichtsdatenquellen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- Windows authentication [Reporting Services]
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- unattended report processing [Reporting Services]
- reports [Reporting Services], security
- remote data sources [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- prompted credentials [Reporting Services]
- multiple connections
- stored credentials [Reporting Services]
- security [Reporting Services], data sources
- Windows integrated security [Reporting Services]
ms.assetid: fee1a663-a313-424a-aed2-5082bfd114b3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3eab390eb43d41d89bc5cf3b1cefe84c121ce9f5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2019
ms.locfileid: "59945466"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen
  Ein Berichtsserver verwendet Anmeldeinformationen zum Herstellen einer Verbindung zu externen Datenquellen, die Inhalt für Berichte oder Empfängerinformationen für ein datengesteuertes Abonnement bereitstellen. Sie können Anmeldeinformationen angeben, die die Windows-Authentifizierung, Datenbankauthentifizierung, keine Authentifizierung oder benutzerdefinierte Authentifizierung verwenden. Beim Senden einer Verbindungsanforderung über das Netzwerk nimmt der Berichtsserver entweder die Identität eines Benutzerkontos oder des Kontos für die unbeaufsichtigte Ausführung an. Weitere Informationen zum Sicherheitskontext, in dem eine Verbindungsanforderung gestellt wird, finden Sie unter [Datenquellenkonfiguration und Netzwerkverbindungen](#DataSourceConfigurationConnections) weiter unten in diesem Thema.  
  
> [!NOTE]  
>  Anmeldeinformationen werden ebenfalls zum Authentifizieren von Benutzern verwendet, die auf einen Berichtsserver zugreifen. Informationen zum Authentifizieren von Benutzern für einen Berichtsserver finden Sie in einem anderen Thema.  
  
 Die Verbindung mit einer externen Datenquelle wird beim Erstellen des Berichts definiert. Sie kann nach Veröffentlichen des Berichts getrennt verwaltet werden. Sie können eine statische Verbindungszeichenfolge angeben oder einen Ausdruck, über den Benutzer eine Datenquelle aus einer dynamische Liste auswählen können. Weitere Informationen zum Data Source und der Verbindungszeichenfolge angeben, finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
## <a name="using-remote-data-sources"></a>Verwenden von Remotedatenquellen  
 Wenn der Bericht Daten von einem Remote-Datenbankserver abruft, überprüfen Sie Folgendes:  
  
-   Die für den Datenbankserver bereitgestellten Anmeldeinformationen sind gültig. Wenn Sie Windows-Benutzeranmeldeinformationen verwenden, stellen Sie sicher, dass der Benutzer über Berechtigungen zum Zugreifen auf den Server und die Datenbank verfügt.  
  
-   Vom Datenbankserver verwendete Ports sind offen. Wenn Sie auf relationale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken auf externen Computern zugreifen oder wenn sich die Berichtsserver-Datenbank auf einer externen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz befindet, müssen Sie Port 1433 und Port 1434 auf dem externen Computer öffnen. Stellen Sie sicher, den Server nach dem Öffnen von Ports neu zu starten. Weitere Informationen zur Windows-Firewall finden Sie unter [Konfigurieren einer Windows-Firewall für Datenbank-Engine-Zugriff](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
-   Remoteverbindungen müssen aktiviert sein. Wenn Sie auf relationale SQL Server-Datenbanken auf externen Computern zugreifen, können Sie das SQL Server-Konfigurations-Manager-Tool verwenden, um sicherzustellen, dass Remoteverbindungen über TCP aktiviert sind.  
  
## <a name="ways-to-specify-credentials-for-connecting-to-remote-data-sources"></a>Möglichkeiten zum Festlegen von Anmeldeinformationen zur Verbindungsherstellung mit Remotedatenquellen  
 Die Datenquellen, die Inhalt für Berichte liefern, werden normalerweise auf Remoteservern gehostet. Um Daten für einen Bericht abzurufen, muss ein Berichtsserver mithilfe von Anmeldeinformationen, die Sie vorher bereitstellen oder die zur Laufzeit eingegeben werden, eine Verbindung mit diesem Server herstellen. Beim Konfigurieren einer Datenquelle stehen Ihnen zum Angeben der Anmeldeinformationen folgende Möglichkeiten zur Verfügung:  
  
-   Aufforderung zur Eingabe der Anmeldeinformationen.  
  
-   Anmeldeinformationen speichern  
  
-   Integrierte Sicherheit von Windows verwenden  
  
-   Kein Verwenden von Anmeldeinformationen  
  
 Die Netzwerkumgebung bestimmt die unterstützten Verbindungen. Wenn z. B. das Kerberos-Protokoll, Version 5, aktiviert ist, können Sie mithilfe der Delegierungs- und Identitätswechselfunktionen der Windows-Authentifizierung möglicherweise Verbindungen über mehrere Server hinweg unterstützen. Falls Ihr Netzwerk diese Sicherheitsfunktionen nicht unterstützt, müssen Sie diese Verbindungseinschränkungen umgehen. Wenn Identitätswechsel und Delegierung nicht aktiviert sind, können Windows-Anmeldeinformationen über eine Computerverbindung weitergegeben werden, bevor sie ablaufen. Eine Benutzerverbindung von einem Clientcomputer zu einem Berichtsservercomputer zählt als erste Verbindung. Wenn der Benutzer einen Bericht öffnet, der Daten von einem Remoteserver abruft, zählt diese Anmeldung als zweite Verbindung und erzeugt einen Fehler, wenn für die Verbindung bei nicht aktivierter Delegierung integrierte Sicherheit verwendet wird.  
  
 Wenn mehrere Verbindungen erforderlich sind, um einen Roundtrip vom Clientcomputer zu einer externen Berichtsdatenquelle abzuschließen, wählen Sie eine der folgenden Strategien aus, um die Verbindungen erfolgreich herzustellen.  
  
-   Aktivieren Sie die Identitätswechsel- und Delegierungsfunktionen in der Domäne, damit Anmeldeinformationen unbegrenzt an andere Computer delegiert werden können.  
  
-   Verwenden Sie gespeicherte Anmeldeinformationen oder eine Aufforderung zur Eingabe von Anmeldeinformationen, um externe Datenquellen für Berichtsdaten abzufragen. Bei den Anmeldeinformationen kann es sich entweder um ein Windows-Domänenkonto oder um eine Datenbank-Anmeldung handeln.  
  
### <a name="prompted-credentials"></a>Aufforderung zur Eingabe der Anmeldeinformationen  
 Wenn Sie eine Berichtsdatenquellen-Verbindung für die Verwendung von Aufforderungen zur Eingabe der Anmeldeinformationen konfigurieren, muss jeder Benutzer, der auf den Bericht zugreift, einen Benutzernamen und ein Kennwort zum Abrufen der Daten eingeben. Diese Vorgehensweise wird für Berichte mit vertraulichen Daten empfohlen. Aufforderungen zur Eingabe der Anmeldeinformationen können nur für Berichte verwendet werden, die bei Bedarf ausgeführt werden. Bei den angeforderten Anmeldeinformationen kann es sich um ein Windows-Konto oder um eine Datenbank-Anmeldung handeln. Sie müssen **Als Windows-Anmeldeinformationen verwenden, wenn eine Verbindung zur Datenquelle hergestellt wird**auswählen, um die Windows-Authentifizierung zu verwenden. Andernfalls werden die Anmeldeinformationen vom Berichtsserver an den Datenbankserver zur Authentifizierung übergeben. Wenn der Datenbankserver die bereitgestellten Anmeldeinformationen nicht authentifizieren kann, kommt es bei der Verbindung zu einem Fehler.  
  
### <a name="windows-integrated-security"></a>Integrierte Sicherheit von Windows  
 Mit der Option **Integrierte Sicherheit von Windows** übergibt der Berichtsserver den Sicherheitstoken des Benutzers, der auf den Bericht zugreift, an den Server, der die externe Datenquelle hostet. In diesem Fall wird der Benutzer nicht aufgefordert, einen Benutzernamen oder ein Kennwort einzugeben. Dieser Ansatz wird empfohlen, wenn Identitätswechsel- und Delegierungsfunktionen aktiviert sind. Wenn diese Funktionen nicht aktiviert sind, sollten Sie diese Vorgehensweise nur verwenden, wenn sich alle Server, auf die Sie zugreifen möchten, auf demselben Computer befinden.  
  
### <a name="stored-credentials"></a>Gespeicherte Anmeldeinformationen  
 Die Anmeldeinformationen für den Zugriff auf eine externe Datenquelle können gespeichert werden. Anmeldeinformationen werden mit umkehrbarer Verschlüsselung in der Berichtsserver-Datenbank gespeichert. Pro Datenquelle, die in einem Bericht verwendet wird, können Sie einen Satz gespeicherter Anmeldeinformationen angeben. Die bereitgestellten Anmeldeinformationen rufen für jeden Benutzer, der den Bericht ausführt, dieselben Daten ab.  
  
 Gespeicherte Anmeldeinformationen werden im Rahmen einer Strategie für den Zugriff auf Remote-Datenbankserver empfohlen. Gespeicherte Anmeldeinformationen sind erforderlich, um Abonnements zu unterstützen oder um das Generieren des Berichtsverlaufs oder das Aktualisieren von Berichtsmomentaufnahmen zeitlich zu planen. Wird ein Bericht als Hintergrundprozess ausgeführt, dient der Berichtsserver als Agent für die Berichtsausführung. Da kein Benutzerkontext vorhanden ist, benötigt der Berichtsserver Anmeldeinformationen aus der Berichtsserver-Datenbank, um die Verbindung zu einer Datenquelle herzustellen.  
  
 Der Benutzername und das Kennwort, die Sie angeben, können Windows-Anmeldeinformationen oder eine Datenbank-Anmeldung sein. Wenn Sie Windows-Anmeldeinformationen angeben, übergibt der Berichtsserver die Anmeldeinformationen für die nachfolgende Authentifizierung an Windows. Andernfalls werden die Anmeldeinformationen an den Datenbankserver für die Authentifizierung übergeben.  
  
#### <a name="how-to-grant-allow-log-on-locally-permissions-to-domain-user-accounts"></a>Gewähren der Berechtigung 'Lokal anmelden zulassen' für Domänenbenutzerkonten  
 Wenn Sie gespeicherte Anmeldeinformationen für die Verbindung mit einer externen Datenquelle verwenden, muss das Windows-Domänenbenutzerkonto über Berechtigungen für die lokale Anmeldung verfügen. Diese Berechtigung ermöglicht dem Berichtsserver, die Identität des Berichtsserverbenutzers anzunehmen und die Anforderung an die externe Datenquelle als dieser Benutzer zu senden.  
  
 Gehen Sie zum Gewähren dieser Berechtigung wie folgt vor:  
  
1.  Öffnen Sie auf dem Berichtsservercomputer unter **Verwaltung**die Option **Lokale Sicherheitsrichtlinie**.  
  
2.  Erweitern Sie unter **Sicherheitseinstellungen**die Option **Lokale Richtlinien**, und klicken Sie dann auf **Zuweisen von Benutzerrechten**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **Lokal anmelden zulassen** , und klicken Sie dann mit der rechten Maustaste auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**.  
  
5.  Klicken Sie auf **Speicherorte**, geben Sie eine Domäne oder einen anderen Speicherort an, der durchsucht werden soll, und klicken Sie dann auf **OK**.  
  
6.  Geben Sie das Windows-Konto ein, für das die interaktive Anmeldung zugelassen werden soll, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie im Dialogfeld **Eigenschaften von Lokal anmelden zulassen** auf **OK**.  
  
8.  Stellen Sie sicher, dass das von Ihnen ausgewählte Konto nicht gleichzeitig eine Zugriffsverweigerung aufweist.  
  
    1.  Klicken Sie mit der rechten Maustaste auf **Lokal anmelden verweigern** , und klicken Sie dann mit der rechten Maustaste auf **Eigenschaften**.  
  
    2.  Wenn das Konto aufgelistet ist, markieren Sie es, und klicken Sie dann auf **Entfernen**.  
  
#### <a name="using-impersonation-with-stored-credentials"></a>Verwenden des Identitätswechsels mit gespeicherten Anmeldeinformationen  
 Sie können auch Anmeldeinformationen für den Identitätswechsel verwenden. Bei SQL Server-Datenbanken wird durch die Identitätswechseloptionen die [SETUSER](/sql/t-sql/statements/setuser-transact-sql) -Funktion festgelegt.  
  
> [!IMPORTANT]  
>  Verwenden Sie den Identitätswechsel nicht für Berichte, die Abonnements unterstützen oder die Zeitpläne zum Generieren des Berichtsverlaufs oder zum Aktualisieren einer Berichtsausführungs-Momentaufnahme verwenden.  
  
### <a name="no-credentials"></a>Keine Anmeldeinformationen  
 Eine Datenquellenverbindung können Sie so konfigurieren, dass keine Anmeldeinformationen verwendet werden. Microsoft empfiehlt, stets Anmeldeinformationen für den Zugriff auf Datenquellen zu verwenden, von der Verwendung keiner Anmeldeinformationen wird abgeraten. Sie können jedoch in folgenden Fällen einen Bericht ohne Anmeldeinformationen ausführen:  
  
-   Die Remotedatenquelle erfordert keine Anmeldeinformationen.  
  
-   Die Anmeldeinformationen werden mithilfe der Verbindungszeichenfolge übergeben (nur für sichere Verbindungen empfohlen).  
  
-   Der Bericht ist ein Unterbericht, der die Anmeldeinformationen des übergeordneten Berichts verwendet.  
  
 Unter diesen Bedingungen stellt der Berichtsserver eine Verbindung zu einer Remotedatenquelle mithilfe des Kontos für die unbeaufsichtigte Ausführung her, das Sie vorher definieren müssen. Da der Berichtsserver die Verbindung zu einem Remoteserver nicht mit seinen Dienstanmeldeinformationen herstellt, müssen Sie ein Konto angeben, mit dem der Berichtsserver die Verbindung herstellen kann. Weitere Informationen zum Erstellen dieses Kontos finden Sie unter [Konfigurieren des unbeaufsichtigten Ausführungskontos (SSRS-Konfigurations-Manager)](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
##  <a name="DataSourceConfigurationConnections"></a> Datenquellenkonfiguration und Netzwerkverbindungen  
 Die folgende Tabelle zeigt, wie bei bestimmten Kombinationen von Anmeldeinformationstypen und Datenverarbeitungserweiterungen Verbindungen hergestellt werden. Wenn Sie eine benutzerdefinierte Datenverarbeitungserweiterung verwenden, lesen Sie unter [Angeben von Verbindungen für benutzerdefinierte Datenverarbeitungserweiterungen](specify-connections-for-custom-data-processing-extensions.md)nach.  
  
|**Typ**|**Kontext für Netzwerkverbindung**|**Datenquellentypen**<br /><br /> **(SQL Server, Oracle, ODBC, OLE DB, Analysis Services, XML, SAP NetWeaver BI, Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|Integrierte Sicherheit|Annehmen der Identität des aktuellen Benutzers|Stellen Sie für alle Datenquellentypen die Verbindung mithilfe des aktuellen Benutzerkontos her.|  
|Windows-Anmeldeinformationen|Annehmen der Identität des angegebenen Benutzers|Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC und OLE DB: Herstellen von Verbindungen mithilfe des Benutzerkontos, dessen Identität angenommen wurde.|  
|Datenbank-Anmeldeinformationen|Nehmen Sie die Identität des Kontos für die unbeaufsichtigte Ausführung oder des Dienstkontos an.<br /><br /> (Reporting Services entfernt die Administratorberechtigungen, wenn die Verbindungsanforderung mit der Dienstidentität gesendet wird.)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: Oracle, ODBC und OLE DB:<br /><br /> Fügen Sie den Benutzernamen und das Kennwort an die Verbindungszeichenfolge an.<br /><br /> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:<br /><br /> Die Verbindung wird nur bei Verwendung des TCP/IP-Protokolls hergestellt, andernfalls wird ein Fehler erzeugt.<br /><br /> Für XML:<br /><br /> Lassen Sie bei Verwendung von Datenbank-Anmeldeinformationen die Verbindung auf dem Berichtsserver fehlschlagen.|  
|None|Nehmen Sie die Identität des Kontos für die unbeaufsichtigte Ausführung an.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: Oracle, ODBC und OLE DB:<br /><br /> Verwenden Sie die in der Verbindungszeichenfolge definierten Anmeldeinformationen. Wenn das Konto für die unbeaufsichtigte Ausführung nicht definiert ist, schlägt die Verbindung auf dem Berichtsserver fehl.<br /><br /> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:<br /><br /> Lassen Sie die Verbindung immer fehlschlagen, wenn keine Anmeldeinformationen angegeben werden, und zwar auch dann, wenn das Konto für die unbeaufsichtigte Ausführung definiert ist.<br /><br /> Für XML:<br /><br /> Stellen Sie die Verbindung als anonymer Benutzer her, wenn das Konto für die unbeaufsichtigte Ausführung definiert ist; lassen Sie andernfalls die Verbindung fehlschlagen.|  
  
## <a name="setting-credentials-programmatically"></a>Programmgesteuertes Festlegen von Anmeldeinformationen  
 Sie können Anmeldeinformationen im Code festlegen, um den Zugriff auf Berichte und den Berichtsserver zu steuern. Weitere Informationen finden Sie unter [Data Sources and Connection Methods](../report-server-web-service/methods/data-sources-and-connection-methods.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Verwalten von Berichtsdatenquellen](../../integration-services/connection-manager/data-sources.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../report-manager-ssrs-native-mode.md)   
 [Erstellen, Löschen oder Ändern einer freigegebenen Datenquelle &#40;Berichts-Manager&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Konfigurieren von Datenquelleneigenschaften für einen Bericht &#40;Berichts-Manager&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
