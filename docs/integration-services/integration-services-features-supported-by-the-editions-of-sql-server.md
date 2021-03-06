---
title: Von den SQL Server-Editionen unterstützte Integration Services-Funktionen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4d1b99431f48d9bbf9b53bb57f1b0bcf2291a6c1
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276221"
---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>Von den SQL Server-Editionen unterstützte Integration Services-Funktionen
 Dieses Thema bietet detaillierte Informationen zu den von den verschiedenen [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]-Editionen unterstützten SQL Server Integration Services-Funktionen (SSIS).  

Von Evaluation und Developer Edition unterstützte Funktionen finden Sie in den Funktionen der Enterprise Edition in den folgenden Tabellen.
  
Die neuesten Anmerkungen zu dieser Version und Informationen zu Neuigkeiten finden Sie in folgenden Artikeln:
-   [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Neuigkeiten in Integration Services in SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [Neues in Integration Services in SQL Server 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**SQL Server 2016 R2 ausprobieren!**    

Die SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
    
> [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a> Neue Integration Services-Funktionen in SQL Server 2017
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Scale Out-Master|Ja|||||
|Scale Out-Worker|Ja|Ja <sup>1</sup>|TBD|TBD|TBD|
|Unterstützung für Microsoft Dynamics AX und Microsoft Dynamics CRM in OData-Komponenten <sup>2</sup>|Ja|Ja||||

<sup>1</sup> Wenn Sie Pakete ausführen, für die nur Enterprise-Funktionen in Scale Out erforderlich ist, müssen die Scale Out-Worker ebenfalls auf Instanzen von SQL Server Enterprise ausgeführt werden.

<sup>2</sup> Diese Funktion wird auch in SQL Server 2016 mit Service Pack 1 unterstützt.

## <a name="IEWiz"></a> SQL Server-Import/Export-Assistent

|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Server-Import/Export-Assistent|Ja|Ja|Ja|Ja|Ja|  

## <a name="IS"></a> Integration Services  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integrierte Datenquellenkonnektoren|Ja|Ja|||| 
|Integrierte Tasks und Transformationen|Ja|Ja||||  
|ODBC-Quelle und -Ziel |Ja|Ja|||| 
|Azure-Datenquellenkonnektoren und Tasks|Ja|Ja||||  
|Hadoop-/HDFS-Connectors und -Tasks|Ja|Ja||||  
|Grundlegende Datenprofilerstellungs-Tools|Ja|Ja|||| 

## <a name="ISAA"></a>Integration Services – Erweiterte Quellen und Ziele  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Oracle-Quelle und -Ziel für eine leistungsstarke Ausführung von Attunity|Ja|||||  
|Teradata-Quelle und -Ziel für eine leistungsstarke Ausführung von Attunity|Ja|||||  
|SAP BW-Quelle und -Ziel|Ja|||||  
|Ziel für Data Mining-Modelltraining|Ja|||||  
|Ziel für Dimensionsverarbeitung|Ja|||||  
|Ziel für Partitionsverarbeitung|Ja|||||  
  
## <a name="ISAT"></a> Integration Services – Erweiterte Tasks und Transformationen  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Change Data Capture-Komponenten von Attunity <sup>1</sup>|Ja|||||  
|Transformation für Data Mining-Abfragen|Ja|||||  
|Transformationen für Fuzzygruppierung und Fuzzysuche|Ja|||||  
|Transformationen für Ausdrucksextrahierung und Ausdruckssuche|Ja|||||  

<sup>1</sup> Für die Change Data Capture-Komponenten von Attunity ist Enterprise Edition erforderlich. Die Enterprise Edition ist jedoch nicht für den Change Data Capture Service und Change Data Capture-Designer notwendig. Sie können den Designer und den Dienst auf einem Computer verwenden, auf dem SSIS nicht installiert ist.
