---
title: Authentifizierung beim Berichtsserver | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- connections [Reporting Services], accounts
- Windows authentication [Reporting Services]
- authentication [Reporting Services]
- Forms authentication
ms.assetid: 753c2542-0e97-4d8f-a5dd-4b07a5cd10ab
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 687193b79cdf0bee179062bb40bd49b23ada60d1
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947176"
---
# <a name="authentication-with-the-report-server"></a>Authentifizierung mit dem Berichtsserver
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) bietet mehrere konfigurierbare Optionen zum Authentifizieren von Benutzern und Clientanwendungen am Berichtsserver. Standardmäßig verwendet der Berichtsserver die integrierte Windows-Authentifizierung und geht von vertrauenswürdigen Beziehungen aus, wenn sich Client- und Netzwerkressourcen in der gleichen Domäne oder einer vertrauenswürdigen Domäne befinden. Abhängig von der Netzwerktopologie und den Anforderungen der Organisation können Sie das für die integrierte Windows-Authentifizierung verwendete Authentifizierungsprotokoll anpassen, die Standardauthentifizierung verwenden oder eine selbst bereitgestellte und auf einem benutzerdefinierten Formular basierende Authentifizierungserweiterung nutzen. Jeder dieser Authentifizierungstypen kann individuell aktiviert oder deaktiviert werden. Sie können mehrere Authentifizierungstypen aktivieren, wenn der Berichtsserver mehrere Arten von Anforderungen akzeptieren soll.  
  
> [!NOTE]  
>  In vorherigen Versionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]wurde die gesamte Authentifizierungsunterstützung von IIS bereitgestellt. Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wird IIS nicht mehr verwendet. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verarbeitet alle Authentifizierungsanfragen intern.  
  
 Alle Benutzer oder Anwendungen, die Zugriff auf Berichtsserverinhalte oder -vorgänge anfordern, müssen vor Gewähren des Zugriffs authentifiziert werden.  
  
## <a name="authentication-types"></a>Authentifizierungstypen  
 Alle Benutzer oder Anwendungen, die Zugriff auf Berichtsserverinhalte oder -vorgänge anfordern, müssen vor Gewähren des Zugriffs mit dem Authentifizierungstyp authentifiziert werden, der auf dem Berichtsserver konfiguriert ist. In der folgenden Tabelle werden die von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]unterstützten Authentifizierungstypen beschrieben.  
  
|Name Authentifizierungstyp|Wert HTTP-Authentifizierungsebene|Standardmäßig verwendet|Description|  
|-----------------------------|-------------------------------------|---------------------|-----------------|  
|RSWindowsNegotiate|Aushandeln|Ja|Versucht für die integrierte Windows-Authentifizierung zunächst eine Kerberos-Authentifizierung zu verwenden, greift jedoch auf NTLM zurück, wenn Active Directory kein Ticket für die Client-Anforderung auf den Berichtsserver gewähren kann. Negotiate greift nur auf NTLM zurück, wenn das Ticket nicht verfügbar ist. Wenn der erste Versuch zu einem Fehler (außer einem nicht verfügbaren Ticket) führt, unternimmt der Berichtsserver keinen zweiten Versuch.|  
|RSWindowsNTLM|NTLM|Ja|Verwendet für die integrierte Windows-Authentifizierung NTLM.<br /><br /> Die Anmeldeinformationen werden nicht delegiert oder durch einen Identitätswechsel für andere Anforderungen verwendet. Nachfolgende Anforderungen befolgen eine neue Abfrage-/Rückmeldungs-Sequenz. Je nach den Einstellungen für die Netzwerksicherheit können Benutzer aufgefordert werden, Anmeldeinformationen einzugeben, oder die Authentifizierungsanforderung wird transparent verarbeitet.|  
|RSWindowsKerberos|Kerberos|Nein|Verwendet für die integrierte Windows-Authentifizierung Kerberos. Sie müssen Kerberos konfigurieren, indem Sie Dienstprinzipalnamen (Service Principle Names, SPNs) für die Dienstkonten einrichten, die Domänenadministratorberechtigungen erfordern. Wenn Sie für Kerberos die Identitätsdelegierung aktivieren, kann das Token des den Bericht anfordernden Benutzers auch für eine zusätzliche Verbindung zu den externen Datenquellen verwendet werden, die Daten für Berichte liefern.<br /><br /> Bevor Sie RSWindowsKerberos angeben, stellen Sie sicher, dass der von Ihnen verwendete Browsertyp diesen Authentifizierungstyp unterstützt. Wenn Sie Internet Explorer verwenden, wird die Kerberos-Authentifizierung nur über Negotiate unterstützt. Internet Explorer formuliert keine Authentifizierungsanforderung, die Kerberos direkt angibt.|  
|RSWindowsBasic|Standard|Nein|Die Standardauthentifizierung wird im HTTP-Protokoll definiert und kann nur verwendet werden, um HTTP-Anforderungen an den Berichtsserver zu authentifizieren.<br /><br /> Anmeldeinformationen werden mithilfe der Base64-Codierung an die HTTP-Anforderung übergeben. Bei der Standardauthentifizierung können Sie SSL (Secure Sockets Layer) zum Verschlüsseln der Benutzerkontoinformationen verwenden, bevor diese über das Netzwerk gesendet werden. SSL bietet einen verschlüsselten Kanal zum Senden einer Verbindungsanforderung vom Client an den Berichtsserver über eine HTTP TCP/IP-Verbindung. Weitere Informationen finden Sie auf der [TechNet-Website unter](https://go.microsoft.com/fwlink/?LinkId=71123) Using SSL to Encrypt Confidential Data [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|  
|Benutzerdefiniert|(Anonym)|Nein|Die anonyme Authentifizierung weist den Berichtsserver an, den Authentifizierungsheader in einer HTTP-Anforderung zu ignorieren. Der Berichtsserver akzeptiert alle Anforderungen. Führen Sie den Aufruf jedoch mit einer benutzerdefinierten [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] Formularauthentifizierung aus, die Sie zur Authentifizierung des Benutzers bereitstellen.<br /><br /> Geben Sie `Custom` nur an, wenn Sie ein benutzerdefiniertes Authentifizierungsmodul bereitstellen, das alle Authentifizierungsanforderungen auf dem Berichtsserver verarbeitet. Sie können den benutzerdefinierten Authentifizierungstyp nicht mit der Standardauthentifizierungserweiterung von Windows verwenden.|  
  
## <a name="unsupported-authentication-methods"></a>Nicht unterstützte Authentifizierungsmethoden  
 Die folgenden Authentifizierungsmethoden und -anforderungen werden nicht unterstützt.  
  
|Authentifizierungsmethode|Erklärung|  
|---------------------------|-----------------|  
|Anonym|Der Berichtsserver akzeptiert nur die nicht authentifizierten Anforderungen anonymer Benutzer in Bereitstellungen, die eine benutzerdefinierte Authentifizierungserweiterung enthalten.<br /><br /> Berichts-Generator akzeptiert nicht authentifizierte Anforderungen, wenn Sie den Zugriff des Berichts-Generators auf einen Berichtsserver aktivieren, der für die Standardauthentifizierung konfiguriert ist.<br /><br /> In allen anderen Fällen werden die anonymen Anforderungen mit dem Fehler 'HTTP Status 401 Access Denied' abgelehnt, bevor die Anforderung [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]erreicht. Clients, die den Fehler '401 Access Denied' erhalten, müssen die Anforderung mit einem gültigen Authentifizierungstyp umformulieren.|  
|Technologie für einmaliges Anmelden (SSO, Single sign-on technologies)|In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]gibt es keine systemeigene Unterstützung der Technologien für einmaliges Anmelden. Wenn Sie eine Technologie für einmaliges Anmelden verwenden möchten, müssen Sie eine benutzerdefinierte Authentifizierungserweiterung erstellen.<br /><br /> Die Berichtsserver-Hostumgebung unterstützt keine ISAPI-Filter. Falls die verwendete SSO-Technologie als ISAPI-Filter implementiert ist, sollten Sie die in den ISA-Server integrierte Unterstützung für RSASecueID oder das RADIUS-Protokoll verwenden. Andernfalls können Sie eine ISA-Server-ISAPI oder ein HTTPModule für RS erstellen. Es wird jedoch die direkte Verwendung des ISA-Servers empfohlen.|  
|Passport|Wird in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]nicht unterstützt.|  
|Digest|Wird in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]nicht unterstützt.|  
  
## <a name="configuration-of-authentication-settings"></a>Konfigurieren von Authentifizierungseinstellungen  
 Authentifizierungseinstellungen werden für die Standardsicherheit konfiguriert, wenn die Berichtsserver-URL reserviert ist. Wenn Sie diese Einstellungen inkorrekt bearbeiten, gibt der Berichtsserver für Anforderungen, die nicht authentifiziert werden können, die Fehler ' HTTP 401 Access Denied' zurück. Beim Auswählen eines Authentifizierungstyps müssen Sie bereits wissen, wie die Windows-Authentifizierung in Ihrem Netzwerk unterstützt wird. Sie müssen mindestens einen Authentifizierungstyp angeben. Für RSWindows können mehrere Authentifizierungstypen angegeben werden. RSWindows-Authentifizierungstypen (d.h. `RSWindowsBasic`, `RSWindowsNTLM`, `RSWindowsKerberos`, und **RSWindowsNegotiate**) mit benutzerdefinierten gegenseitig.  
  
> [!IMPORTANT]  
>  Reporting Services überprüft nicht, ob die von Ihnen angegebenen Einstellungen für die Computerumgebung korrekt sind. Es ist möglich, dass die Standardsicherheit für Ihre Installation nicht geeignet ist oder die von Ihnen angegebenen Konfigurationseinstellungen für Ihre Sicherheitsinfrastruktur nicht geeignet sind. Aus diesem Grund sollten Sie Ihre Berichtsserverbereitstellung in einer kontrollierten Testumgebung sorgfältig prüfen, bevor Sie sie Ihrer Organisation zur Verfügung stellen.  
  
 Der Berichtsserver-Webdienst und der Berichts-Manager verwenden stets denselben Authentifizierungstyp. Sie können keine anderen Authentifizierungstypen für die Funktionsbereiche des Berichtsserverdienstes konfigurieren. In einem Bereitstellungsmodell für horizontales Skalieren sollten Sie sicherstellen, dass alle Ihre Änderungen auf allen Knoten der Bereitstellung dupliziert werden. Sie können keine anderen Knoten in der gleichen Bereitstellung für horizontales Skalieren konfigurieren, um andere Authentifizierungstypen zu verwenden.  
  
 Die Hintergrundverarbeitung akzeptiert keine Anforderungen von Endbenutzern. Sie authentifiziert jedoch alle Anforderungen für unbeaufsichtigte Ausführungszwecke. Sie verwendet stets die Windows-Authentifizierung und authentifiziert Anforderungen mit dem Berichtsserverdienst oder dem Konto für die unbeaufsichtigte Ausführung, falls konfiguriert.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver](configure-windows-authentication-on-the-report-server.md)  
  
-   [Configure Basic Authentication on the Report Server (Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver)](configure-basic-authentication-on-the-report-server.md)  
  
-   [Konfiguration der benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver](configure-custom-or-forms-authentication-on-the-report-server.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibungen|Links|  
|-----------------------|-----------|  
|Konfigurieren Sie den integrierte Windows-Authentifizierungstyp.|[Configure Windows Authentication on the Report Server (Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver)](configure-windows-authentication-on-the-report-server.md)|  
|Konfigurieren Sie den Standardauthentifizierungstyp.|[Konfigurieren der Standardauthentifizierung auf dem Berichtsserver](configure-basic-authentication-on-the-report-server.md)|  
|Konfigurieren Sie die formularbasierte Authentifizierung oder andernfalls ein benutzerdefinierten Authentifizierungstyp.|[Configure Custom or Forms Authentication on the Report Server (Konfiguration der benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver)](configure-custom-or-forms-authentication-on-the-report-server.md)|  
|Ermöglichen Sie die Verarbeitung des benutzerdefinierte Authentifizierungsszenarios im Berichts-Manager.|[Konfigurieren des Berichts-Managers für die Übergabe von benutzerdefinierten Authentifizierungscookies](configure-the-web-portal-to-pass-custom-authentication-cookies.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](granting-permissions-on-a-native-mode-report-server.md)   
 [RSReportServer-Konfigurationsdatei](../report-server/rsreportserver-config-configuration-file.md)   
 (create-and-manage-role-assignments.md)   
 [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
 [Implementieren von Sicherheitserweiterungen](../extensions/security-extension/implementing-a-security-extension.md)   
 [Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](configure-ssl-connections-on-a-native-mode-report-server.md)   
 [Konfigurieren des Berichts-Generator-Zugriffs](../report-server/configure-report-builder-access.md)   
 [Übersicht über Sicherheitserweiterungen](../extensions/security-extension/security-extensions-overview.md)   
 [Authentifizierung in Reporting Services](../extensions/security-extension/authentication-in-reporting-services.md)   
 [Autorisierung in Reporting Services](../extensions/security-extension/authorization-in-reporting-services.md)  
  
  
