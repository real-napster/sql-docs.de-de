---
title: Kopieren von Paketobjekten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- control flow [Integration Services], copying objects
- copying package objects [Integration Services]
- data flow [Integration Services], copying objects
- connection managers [Integration Services], copying
ms.assetid: 99b85e5c-d6bd-4e7c-afe4-51f6ce151c2f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 46fc751556c7e9e1ca9fc122bf8c80a2f5056fc8
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276360"
---
# <a name="copy-package-objects"></a>Kopieren von Paketobjekten
  In diesem Thema wird beschrieben, wie Sie Ablaufsteuerungs- und Datenflusselemente sowie Verbindungs-Manager innerhalb eines Pakets bzw. von einem Paket in ein anderes kopieren.  
  
### <a name="to-copy-control-and-data-flow-items"></a>So kopieren Sie Ablaufsteuerungs- und Datenflusselemente  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, mit dem Sie arbeiten möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf die Pakete, die untereinander kopiert werden sollen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer auf die Registerkarte des Pakets, in dem die zu kopierenden Elemente enthalten sind, und klicken Sie auf die Registerkarte **Ablaufsteuerung**, **Datenfluss**oder **Ereignishandler** .  
  
4.  Wählen Sie die zu kopierenden Ablaufsteuerungs- oder Datenflusselemente aus. Sie können jeweils ein Element auswählen, indem Sie die UMSCHALTTASTE drücken und auf das Element klicken, oder die Elemente als eine Gruppe auswählen, indem Sie den Zeiger über die auszuwählenden Elemente ziehen.  
  
    > [!IMPORTANT]  
    >  Die die Elemente verbindenden Rangfolgeneinschränkungen und Pfade werden bei Auswahl zwei verbundener Elemente nicht automatisch ausgewählt. Stellen Sie sicher, dass Sie auch die Rangfolgeneinschränkungen und Pfade kopieren, damit ein geordneter Workflow, also ein Ablaufsteuerungs- oder Datenflusssegment, kopiert wird.  
  
5.  Klicken Sie mit der rechten Maustaste auf ein ausgewähltes Element, und klicken Sie auf **Kopieren**.  
  
6.  Wenn Sie Elemente in ein anderes Paket kopieren, klicken Sie auf das Paket, in das kopiert werden soll, und klicken Sie dann auf die entsprechende Registerkarte des jeweiligen Elementtyps.  
  
    > [!IMPORTANT]  
    >  Sie können einen Datenfluss nur in ein Paket kopieren, wenn das Paket mindestens einen Datenflusstask enthält.  
  
7.  Klicken Sie auf die rechte Maustaste, und klicken Sie auf **Einfügen**.  
  
### <a name="to-copy-connection-managers"></a>So kopieren Sie Verbindungs-Manager  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, mit dem Sie arbeiten möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer auf die Registerkarte **Ablaufsteuerung**, **Datenfluss**oder **Ereignishandler** .  
  
4.  Klicken Sie im Bereich **Verbindungs-Manager** mit der rechten Maustaste auf den Verbindungs-Manager, und klicken Sie anschließen auf **Kopieren**. Sie können jeweils nur einen Verbindungs-Manager kopieren.  
  
5.  Wenn Sie Elemente in ein anderes Paket kopieren, klicken Sie auf das Paket, in das kopiert werden soll, und klicken Sie dann auf die Registerkarte **Ablaufsteuerung**, **Datenfluss**oder **Ereignishandler** .  
  
6.  Klicken Sie mit der rechten Maustaste in den Bereich **Verbindungs-Manager** , und klicken Sie auf **Einfügen**.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Ablaufsteuerung](../integration-services/control-flow/control-flow.md)   
 [Datenfluss](../integration-services/data-flow/data-flow.md)   
 [Integration Services-Verbindungen &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Kopieren von Projektelementen](https://msdn.microsoft.com/library/1606c54d-20f9-49f3-a4ef-caad83a772aa)  
  
  
