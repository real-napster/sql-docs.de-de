---
title: Azure Storage-Verbindungs-Manager | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a46945b7c7725d680fb303a451327dc2733642aa
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277829"
---
# <a name="azure-storage-connection-manager"></a>Azure Storage-Verbindungs-Manager
  Der **Azure Storage-Verbindungs-Manager** ermöglicht es, eine Verbindung zwischen einem SSIS-Paket und einem Azure Storage-Konto mithilfe der Werte zu erstellen, die Sie für die folgenden Eigenschaften angeben: „Speicherkontoname“ und „Kontoschlüssel“.  
   
 Der **Azure Storage-Verbindungs-Manager** ist eine Komponente des [SQL Server Integration Services-Feature Packs (SSIS) für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
1.  Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** die Option **AzureStorage**aus, und klicken Sie auf **Hinzufügen**.  
  
2.  Wählen Sie im Editor-Dialogfeld „Azure Storage-Verbindungs-Manager“ **Azure-Konto verwenden** aus, um eine Verbindung zu einem Azure Storage-Dienst über das Internet herzustellen, oder wählen Sie **Lokales Entwicklerkonto verwenden** aus, um eine Verbindung zum lokalen Dienst herzustellen, der vom Azure Storage-Emulator gehostet wird.  
  
3.  Gehen Sie bei Auswahl von **Azure-Konto verwenden** folgendermaßen vor:  
  
    1.  Geben Sie Werte in die Felder **Speicherkontoname** und **Kontoschlüssel** an. Diese Werte werden als vertrauliche Daten im SSIS-Paket gespeichert.  
  
    2.  Wählen Sie **HTTPS verwenden** aus, wenn Sie HTTPS anstelle von HTTP für die Verbindung mit dem Azure Storage-Dienst verwenden möchten.  
  
4.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
5.  Die Eigenschaften des Verbindungs-Managers, die Sie im Fenster **Eigenschaften** erstellt haben, werden angezeigt.  
  
  
