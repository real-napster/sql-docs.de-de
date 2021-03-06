---
title: Herunterladen von SQL Server Management Studio (SSMS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/29/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
ms.technology: ssms
ms.topic: conceptual
keywords:
- Installieren von SSMS, Herunterladen von SSMS, neueste SSMS-Version
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- sql management studio install
- download sql management studio
- ms sql management studio
- install sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dnethi
ms.author: dinethi
manager: craigg
ms.openlocfilehash: 9bc678f69df60ec07e1cca6eddbb337aab8ed8ff
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042027"
---
# <a name="download-sql-server-management-studio-ssms"></a>Herunterladen von SQL Server Management Studio (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server Management Studio (SSMS) ist eine integrierte Umgebung zum Verwalten jeder beliebigen SQL-Infrastruktur, von SQL Server bis hin zur Azure SQL-Datenbank. SSMS stellt Tools zum Konfigurieren, Überwachen und Verwalten von Instanzen von SQL Server und Datenbanken zur Verfügung. Verwenden Sie SSMS, um Abfragen und Skripts zu erstellen sowie die Datenebenenkomponenten bereitzustellen, zu überwachen und zu aktualisieren, die von Ihren Anwendungen verwendet werden.

Verwenden Sie SSMS zum Abfragen, Entwerfen und Verwalten Ihrer Datenbanken und Data Warehouses, unabhängig davon, ob sich diese auf Ihrem lokalen Computer oder in der Cloud befinden.

SSMS ist kostenlos!

[SSMS 18.0 Release Candidate 1 (RC1) ist jetzt verfügbar](#ssms-180-rc1) und stellt die neueste Generation von *SQL Server Management Studio* dar, die Unterstützung für [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] bietet.

## <a name="ssms-1791-is-the-current-general-availability-ga-version-of-ssms"></a>SSMS 17.9.1 ist die aktuelle Version von SSMS mit allgemeiner Verfügbarkeit (GA, General Availability)

[![Download](../ssdt/media/download.png) SQL Server Management Studio 17.9.1 herunterladen](https://go.microsoft.com/fwlink/?linkid=2043154)

[![Download](../ssdt/media/download.png) Upgradepaket für SQL Server Management Studio 17.9.1 (Upgrades 17.x bis 17.9.1) herunterladen](https://go.microsoft.com/fwlink/?linkid=2043430)

**Versionsinformationen**

- Releasenummer: 17.9.1<br>
- Buildnummer: 14.0.17289.0<br>
- Releasedatum: 21. November 2018

### <a name="available-languages-ssms-1791"></a>Verfügbare Sprachen (SSMS 17.9.1)

> [!NOTE]
> In andere Sprachen als Englisch lokalisierte Releases von SSMS 17.x benötigen das [KB 2862966-Sicherheitsupdatepaket](https://support.microsoft.com/kb/2862966) für die Installation unter den folgenden Windows-Systemen: Windows 8, Windows 7, Windows Server 2012 und Windows Server 2008 R2.

[Chinesisch (vereinfacht)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804) | [Chinesisch (traditionell)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

Weitere Informationen zu SSMS 17.9.1 finden Sie im [Änderungsprotokoll für SSMS 17.9.1](release-notes-ssms.md#1791-latest-ga-release).

## <a name="ssms-installation-tips-and-issues-ssms-1791"></a>Tipps und Probleme bei der Installation von SSMS (SSMS 17.9.1)

### <a name="minimize-installation-reboots"></a>Minimieren von Installationsneustarts

* Führen Sie die folgenden Aktionen durch, um zu verhindern, dass das SSMS-Setup einen Neustart am Ende der Installation benötigt:
  * Stellen Sie sicher, dass Sie eine aktuelle Version von Microsoft Visual C++ 2013 Redistributable Package ausführen. Die Version 12.0.40649.5 (oder höher) ist erforderlich. Es wird nur die x64-Version benötigt.
  * Überprüfen Sie, ob die .NET Framework-Version auf dem Computer 4.6.1 (oder höher) ist.
  * Schließen Sie alle Instanzen von Visual Studio, die auf dem Computer geöffnet sind.
  * Stellen Sie sicher, dass die neuesten Betriebssystemupdates auf dem Computer installiert sind.
  * Die registrierten Aktionen werden normalerweise nur einmal benötigt. Es gibt einige Fälle, in denen ein Neustart während zusätzlichen Upgrades auf dieselbe Hauptversion von SSMS notwendig sind. Für kleinere Upgrades sind alle Voraussetzungen für SSMS bereits auf dem Computer vorhanden.

## <a name="ssms-180-rc1"></a>SSMS 18.0 (RC1)

**SSMS 18.0 Release Candidate 1 (RC1) ist jetzt verfügbar und stellt die neueste Generation von *SQL Server Management Studio* dar, die Unterstützung für [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] bietet.**

**[![Download](../ssdt/media/download.png) SQL Server Management Studio 18.0 (RC1) herunterladen](https://go.microsoft.com/fwlink/?linkid=2085742)**

*RC1* ist die neueste Public Preview von SSMS 18.0. Wenn Sie eine ältere Version von SSMS 18.0 Preview installiert haben, deinstallieren Sie diese, bevor Sie SSMS 18.0 RC1 installieren.

**Versionsinformationen**

- Releasenummer: 18.0 (RC1)<br>
- Buildnummer: 15.0.18098.0<br>
- Releasedatum: 28. März 2019

Wenn Sie Kommentare oder Vorschläge haben oder Probleme melden möchten, erreichen Sie das SSMS-Team am besten über [UserVoice](https://aka.ms/sqlfeedback).

Durch die Installation von SSMS 18.x erfolgt weder ein Upgrade noch eine Ersetzung der SSMS-Version 17.x oder früher Versionen. SSMS 18.x wird parallel zu früheren Versionen installiert, damit beide Versionen zur Verfügung stehen.

Wenn ein Computer parallele SSMS-Installationen enthält, sollten Sie sich vergewissern, dass Sie die richtige Version für Ihre speziellen Anforderungen starten. Die neueste Version heißt **Microsoft SQL Server Management Studio 18**.
 
## <a name="available-languages-ssms-180-rc1"></a>Verfügbare Sprachen (SSMS 18.0 RC1)

Diese Version von SSMS kann in folgenden Sprachen installiert werden:

SQL Server Management Studio 18.0 (RC1):<br>
[Chinesisch (vereinfacht)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x804) | [Chinesisch (traditionell)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x40a)

Upgradepaket für SQL Server Management Studio 18.0 (Upgrades auf 18.0):<br>
Zurzeit ist keine Upgradeoption verfügbar. Wenn Sie eine ältere Version von SSMS 18.0 Preview installiert haben, deinstallieren Sie diese, bevor Sie SSMS 18.0 RC1 installieren.

> [!NOTE]
> Das SQL Server PowerShell-Modul ist eine separate Installation über den PowerShell-Katalog. Weitere Informationen finden Sie unter [Download SQL Server PowerShell Module](download-sql-server-ps-module.md) (Herunterladen des SQL Server PowerShell-Moduls).

## <a name="new-in-this-release-ssms-180-rc1"></a>Neues in diesem Release (SSMS 18.0 RC1)

SSMS 18.0 (RC1) ist die neueste Version von SQL Server Management Studio. Die Generation 18.x von SSMS bietet Unterstützung für beinahe alle Featurebereiche unter SQL Server 2008 bis SQL Server 2019 Preview.

Ausführliche Informationen zu Neuerungen in dieser Version finden Sie in den [SSMS-Versionshinweisen](release-notes-ssms.md).

## <a name="supported-sql-offerings-ssms-180-rc1"></a>Unterstützte SQL-Angebote (SSMS 18.0 RC1)

* Diese Version von SSMS funktioniert mit allen [unterstützten Versionen von SQL Server 2008 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) und bietet das höchste verfügbare Maß an Unterstützung für die Arbeit mit den neuesten Cloudfunktionen in Azure SQL-Datenbank und Azure SQL Data Warehouse.
* Zusätzlich kann SSMS 18.x parallel zu SSMS 17.x, SSMS 16.x oder SQL Server 2014 SSMS und früheren Versionen installiert werden.
* SQL Server Integration Services (SSIS): SSMS Version 17.x oder höher unterstützt das Herstellen von Verbindungen zum veralteten Dienst SQL Server Integration Services nicht. Verwenden Sie die Version von SSMS, die auf die Version von SQL Server ausgerichtet ist, um eine Verbindung zu einer früheren Version von Integration Services herzustellen. Verwenden Sie beispielsweise SSMS 16.x, um eine Verbindung zum veralteten Dienst SQL Server 2016 Integration Services herzustellen. SSMS 17.x und SSMS 16.x können parallel auf demselben Computer installiert sein. Seit dem Release von SQL Server 2012 wird empfohlen, Integration Services-Pakete mithilfe der SSIS-Katalogdatenbank (SSISDB) zu speichern, zu verwalten, auszuführen und zu überwachen. Weitere Informationen finden Sie unter [SSIS-Katalog](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-180-rc1"></a>Unterstützte Betriebssysteme (SSMS 18.0 RC1)

Dieses Release von SSMS unterstützt die folgenden 64-Bit-Plattformen, wenn sie mit dem aktuellen Service Pack ausgestattet sind:

- Windows 10 (64-Bit) <sup>*</sup>
- Windows Server 2016 <sup>*</sup>
- Windows Server 2012 R2 (64-Bit)
- Windows Server 2012 (64-Bit)
- Windows Server 2008 R2 (64-Bit)

<sup>*</sup> Erfordert Version 1607 (10.0.14939) oder höher

> [!NOTE]
> SSMS wird nur unter Windows ausgeführt. Wenn Sie ein Tool benötigen, das auf anderen Plattformen als Windows ausgeführt wird, sehen Sie sich Azure Data Studio an. Azure Data Studio ist ein neues plattformübergreifendes Tool, das unter macOS, Linux sowie Windows ausgeführt werden kann. Weitere Informationen finden Sie unter [Azure Data Studio](../azure-data-studio/what-is.md).
  
## <a name="release-notes-ssms-180-rc1"></a>Versionshinweise (SSMS 18.0 RC1)

–

## <a name="previous-releases"></a>Vorgängerversionen

[Vorgängerversionen von SQL Server Management Studio](../ssms/release-notes-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>Feedback

![Hilfe_benötigt_Person_Symbol](../ssms/media/needhelp_person_icon.png) [SQL Clienttools-Forum](https://social.msdn.microsoft.com/Forums/home?forum=sqltools)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>Weitere Informationen

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Dokumentation zu SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Weitere Updates und Service Packs](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Herunterladen von SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

Wenn Sie Kommentare oder Vorschläge haben oder Probleme melden möchten, erreichen Sie das SSMS-Team am besten über [UserVoice](https://aka.ms/sqlfeedback).
