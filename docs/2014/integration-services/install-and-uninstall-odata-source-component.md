---
title: Installieren und Deinstallieren der OData-Quellkomponente | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 34a71ed768c49436a4dba4ecf225bdd009132866
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385259"
---
# <a name="install-and-uninstall-odata-source-component"></a>Installieren und Deinstallieren der OData-Quellkomponente
  Dieses Thema enthält Anweisungen zum Installieren oder Entfernen der OData-Quellkomponente auf dem Computer.  
  
## <a name="installation"></a>Installation  
 Die folgenden Komponenten müssen auf dem Computer installiert sein, um die OData-Quellkomponente installieren zu können.  
  
-   SQL Server Data Tools (zum Entwerfen von Paketen)  
  
-   SQL Server Integration Services (zum Ausführen von Paketen außerhalb von Visual Studio)  
  
 Um die OData-Quellkomponente zu installieren, laden [SQL Server 2014 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkId=391999) und führen Sie einen der folgenden MSI-Dateien.  
  
-   ODataSourceForSQLServer2014-amd64.msi für 64-Bit-Plattformen  
  
-   ODataSourceForSQLServer2014-x86.msi für 32-Bit-Plattformen  
  
> [!IMPORTANT]  
>  Mit dem 64-Bit-Installationsprogramm installieren Sie sowohl die 32-Bit- als auch die 64-Bit-Version der OData-Quellkomponente. Das 32-Bit-Installationsprogramm müssen Sie nur ausführen, wenn Sie ein 32-Bit-Betriebssystem verwenden.  
  
## <a name="uninstallation"></a>Deinstallation  
 Die OData-Quellkomponente deinstalliert werden kann, aus der **Programme und Funktionen** Menü. Suchen der **Microsoft SQL Server SSIS OData-Quellkomponente (x64)** Eintrag und klicken Sie auf **Deinstallieren**.  
  
  
