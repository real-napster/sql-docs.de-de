---
title: Reporting Services-Konfigurationsdateien | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63d2dff214ed1125450ec319dff4ad7f7dc36990
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2019
ms.locfileid: "59939806"
---
# <a name="reporting-services-configuration-files"></a>Reporting Services-Konfigurationsdateien
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] speichert Komponenteninformationen in der Registrierung und in Konfigurationsdateien, die bei der Installation in das Dateisystem kopiert werden. Konfigurationsdateien enthalten eine Kombination aus nur intern verwendeten und benutzerdefinierten Werten. Werte werden vom Benutzer durch die Konfigurationstools, die Befehlszeilen-Hilfsprogramme und manuelles Bearbeiten der Konfigurationsdateien definiert.  
  
 Die Konfigurationsdateien müssen nur dann geändert werden, wenn Sie erweiterte Einstellungen hinzufügen oder konfigurieren. Konfigurationseinstellungen werden als XML-Elemente oder -Attribute angegeben. Wenn Sie sich mit XML und Konfigurationsdateien auskennen, können Sie mit einem Text- oder Code-Editor benutzerdefinierbare Einstellungen ändern. Weitere Informationen über die Vorgehensweise zur Änderung einer Konfigurationsdatei, oder darüber, wie der Berichtsserver neue und aktualisierte Konfigurationseinstellungen liest, finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei („RSreportserver.config“)](modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
> [!NOTE]  
>  In früheren Versionen wies der Berichts-Manager seine eigene Konfigurationsdatei mit dem Namen RSWebApplication.config auf. Diese Datei ist jetzt veraltet. Haben Sie eine frühere Installation aktualisiert, wird diese Datei nicht gelöscht, der Berichtsserver kann jedoch keine Einstellungen aus dieser Datei lesen. Wenn die Datei auf dem Computer vorhanden ist, sollten Sie sie löschen. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen werden alle Berichts-Manager-Konfigurationseinstellungen in der Datei RSReportServer.config gespeichert und aus ihr gelesen. Eine Liste der Einstellungen gelöscht oder verschoben wurden, finden Sie unter [wichtige Änderungen in SQL Server Reporting Services in SQL Server 2014](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
 In diesem Thema:  
  
-   [Überblick über Konfigurationsdateien (einheitlicher Modus)](#bkmk_config_file_Summary_native_mode)  
  
-   [Überblick über Konfigurationsdateien (SharePoint-Modus)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> Überblick über Konfigurationsdateien (einheitlicher Modus)  
 Die nachstehende Tabelle enthält eine Beschreibung der Speicherorte von Konfigurationseinstellungen. Die meisten Konfigurationseinstellungen werden in Konfigurationsdateien gespeichert, die in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]enthalten sind. Standardmäßig wird folgendes Installationsverzeichnis verwendet:  
  
```  
C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER  
```  
  
|Gespeichert in:|Description|Speicherort|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Speichert Konfigurationseinstellungen für Funktionsbereiche des berichtsserverdiensts an: Berichts-Manager, Berichtsserver-Webdienst und hintergrundverarbeitung. Weitere Informationen zu den einzelnen Einstellungen finden Sie unter [RSReportServer Configuration File](rsreportserver-config-configuration-file.md).|\<Installationsverzeichnis>\Reporting Services\ReportServer|  
|RSSrvPolicy.config|Speichert die Codezugriffs-Sicherheitsrichtlinien für die Servererweiterungen. Weitere Informationen zu dieser Datei finden Sie unter [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installationsverzeichnis>\Reporting Services\ReportServer|  
|RSMgrPolicy.config|Speichert die Codezugriffs-Sicherheitsrichtlinien für den Berichts-Manager. Weitere Informationen zu dieser Datei finden Sie unter [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installationsverzeichnis>\Reporting Services\ReportManager|  
|Web.config für den Report Server-Webdienst.|Enthält nur Einstellungen, die für ASP.NET erforderlich sind.|\<Installationsverzeichnis>\Reporting Services\ReportServer|  
|Web.config für den Berichts-Manager.|Enthält nur Einstellungen, die für ASP.NET erforderlich sind.|\<Installationsverzeichnis>\Reporting Services\ReportManager|  
|ReportingServicesService.exe.config|Speichert Konfigurationseinstellungen, die die Ablaufverfolgungsebenen und Protokolloptionen für den Berichtsserverdienst angeben. Weitere Informationen zu den Elementen in dieser Datei finden Sie unter [ReportingServicesService Configuration File](reportingservicesservice-configuration-file.md).|\<Installationsverzeichnis>\Reporting Services\ReportServer\Bin|  
|Registrierungseinstellungen|Speichert den Konfigurationsstatus und andere Einstellungen für die Deinstallation von Reporting Services. Wenn Sie ein Installations- oder Konfigurationsproblem beheben möchten, liefern diese Einstellungen Informationen darüber, wie der Berichtsserver konfiguriert ist.<br /><br /> Ändern Sie diese Einstellungen nicht direkt, da dies die Installation ungültig machen kann.|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceID\>\Setup<br /><br /> **- und -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Speichert Konfigurationseinstellungen für den Berichts-Designer. Weitere Informationen finden Sie unter [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md).|\<Laufwerk>:\Programme\Microsoft Visual Studio 10\Common7\IDE\PrivateAssemblies.|  
|RSPreviewPolicy.config|Speichert die Codezugriffs-Sicherheitsrichtlinien für die Servererweiterungen, die während der Berichtsvorschau verwendet werden. Weitere Informationen zu dieser Datei finden Sie unter [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Programme\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Überblick über Konfigurationsdateien (SharePoint-Modus)  
 Die folgende Tabelle enthält eine Beschreibung der Konfigurationsdateien, die für einen Berichtsserver im SharePoint-Modus verwendet werden. Die meisten Konfigurationseinstellungen werden in Datenbanken der SharePoint-Dienstanwendung gespeichert. Weitere Informationen finden Sie unter [Reporting Services-SharePoint-Dienst und -Dienstanwendungen](../reporting-services-sharepoint-service-and-service-applications.md).  
  
 Standardmäßig wird das folgende Installationsverzeichnis für den SharePoint-Modus verwendet:  
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|Gespeichert in:|Description|Speicherort|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Speichert Konfigurationseinstellungen für Funktionsbereiche des berichtsserverdiensts an: Berichts-Manager, Berichtsserver-Webdienst und hintergrundverarbeitung. Weitere Informationen zu den einzelnen Einstellungen finden Sie unter [RSReportServer Configuration File](rsreportserver-config-configuration-file.md).|\<Installationsverzeichnis>\Reporting Services\ReportServer|  
|RSSrvPolicy.config|Speichert die Codezugriffs-Sicherheitsrichtlinien für die Servererweiterungen. Weitere Informationen zu dieser Datei finden Sie unter [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installationsverzeichnis>\Reporting Services\ReportServer|  
|Web.config für den Report Server-Webdienst.|Enthält nur Einstellungen, die für ASP.NET erforderlich sind.|\<Installationsverzeichnis>\Reporting Services\ReportServer|  
|Registrierungseinstellungen|Speichert den Konfigurationsstatus und andere Einstellungen für die Deinstallation von Reporting Services. Speichert darüber hinaus auch Informationen zu jeder [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung.<br /><br /> Ändern Sie diese Einstellungen nicht direkt, da dies die Installation ungültig machen kann.|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceID\>\Setup<br /><br /> Beispiel-Instanz-ID: MSSQL12.MSSQLSERVER<br /><br /> **- und -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|Speichert Konfigurationseinstellungen für den Berichts-Designer. Weitere Informationen finden Sie unter [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md).|\<Laufwerk>:\Programme\Microsoft Visual Studio 10\Common7\IDE\PrivateAssemblies.|  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](reporting-services-report-server-native-mode.md)   
 [Erweiterungen für Reporting Services](../extensions/reporting-services-extensions.md)   
 [rsconfig-Hilfsprogramm (SSRS)](../tools/rsconfig-utility-ssrs.md)   
 [Start and Stop the Report Server Service (Starten und Beenden des Berichtsserverdiensts)](start-and-stop-the-report-server-service.md)  
  
  
