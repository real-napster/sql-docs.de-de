---
title: Kopie des Pakets speichern | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.savecopyas.f1
helpviewer_keywords:
- Save Copy of Package dialog box
ms.assetid: 7b44c0d7-d8fa-4491-8836-0899f621d3a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e28fec1fb562c5ba6ed28ad615f40ada5fc2db9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766792"
---
# <a name="save-copy-of-package"></a>Kopie des Pakets speichern
  Verwenden Sie das in **verfügbare Dialogfeld** Kopie des Pakets speichern [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], um eine Kopie eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakets aus [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] an einem anderen Speicherort zu speichern und dabei optional die Schutzebene des Pakets zu ändern.  
  
## <a name="options"></a>Optionen  
 **Paketspeicherort**  
 Wählen Sie den Typ des Speicherortes aus, an dem das Paket gespeichert werden soll. Die folgenden Optionen stehen zur Verfügung:  
  
 **SQL Server**  
  
 **Dateisystem**  
  
 **SSIS-Paketspeicher**  
  
 **Server**  
 Geben Sie einen Servernamen ein, oder wählen Sie einen Server aus der Liste aus. Diese Option ist nur verfügbar, wenn der Speicherort **SQL Server** oder **SSIS-Paketspeicher**ist.  
  
 **Authentifizierung**  
 Wählen Sie die Windows-Authentifizierung oder die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung aus. Diese Option ist nur verfügbar, wenn der Speicherort [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ist.  
  
> [!IMPORTANT]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung.  
  
 **Authentifizierungstyp**  
 Wählen Sie einen Authentifizierungstyp aus.  
  
 **Benutzername**  
 Wenn Sie die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwenden, stellen Sie einen Benutzernamen bereit.  
  
 **Kennwort**  
 Geben Sie ein Kennwort an, falls Sie die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwenden.  
  
 **Paketpfad**  
 Geben Sie den Paketpfad ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(...)**  Schaltfläche, und suchen Sie den Ordner, in dem das Paket gespeichert.  
  
 **Schutzebene**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen **(...)**  und Aktualisieren der Schutzebene in die **Paketschutzebene** Dialogfeld. Weitere Informationen finden Sie unter [Dialogfeld „Paket- und Projektschutzebene“](../../2014/integration-services/package-and-project-protection-level-dialog-box.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Referenz zur Benutzeroberfläche für Dialogfeld "Paket importieren"](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [Referenz zur Benutzeroberfläche des Dialogfelds Paket exportieren](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [Speichern von Paketen](save-packages.md)   
 [Importieren und Exportieren von Paketen &#40;SSIS-Dienst&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
