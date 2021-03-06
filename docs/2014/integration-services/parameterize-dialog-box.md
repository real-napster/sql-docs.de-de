---
title: Parametrisieren Sie das Dialogfeld | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0c6391e739f4a7f2556ad75acf377a2e68db8151
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382479"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  Im Dialogfeld **Parametrisieren** können Sie einen neuen oder vorhandenen Parameter der Eigenschaft eines Tasks zuordnen. Sie öffnen das Dialogfeld, indem Sie mit der rechten Maustaste auf einen Task oder die Registerkarte „Ablaufsteuerung“ im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer klicken und dann auf **Parametrisieren** klicken. Die folgende Liste beschreibt Benutzeroberflächenelemente im Dialogfeld. Weitere Informationen zu Parametern finden Sie unter [Integration Services-Parameter &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Eigenschaft**  
 Wählen Sie die Eigenschaft der Aufgabe aus, der Sie einem Parameter zuordnen möchten. Diese Liste wird mit allen Eigenschaften aufgefüllt, die parametrisiert werden können.  
  
 **Vorhandenen Parameter verwenden**  
 Aktivieren Sie diese Option, um die Eigenschaft der Aufgaben einem vorhandenen Parameter zuzuordnen und dann den Parameter aus Dropdownliste auszuwählen.  
  
 **Keinen Parameter verwenden**  
 Wählen Sie diese Option aus, um einen Verweist auf einen Parameter zu entfernen. Der Parameter wurde nicht gelöscht.  
  
 **Neuen Parameter erstellen**  
 Aktivieren Sie diese Option, um einen neuen Parameter zu erstellen, den Sie der Eigenschaft der Aufgabe zuordnen möchten.  
  
 **Name**  
 Geben Sie den Namen des Parameters an, den Sie erstellen möchten.  
  
 **Beschreibung**  
 Geben Sie die Beschreibung für den Parameter an.  
  
 **Wert**  
 Geben Sie den Standardwert für den Parameter an. Dies wird auch als der Entwurfsstandard bezeichnet, der später zur Bereitstellungszeit überschrieben werden kann.  
  
 **Bereich**  
 Geben Sie den Bereich des Parameters an, indem Sie die Option **Projekt** oder die Option **Paket** aktivieren. Projektparameter werden verwendet, um jegliche externen Eingaben bereitzustellen, die das Projekt für ein oder mehrere Pakete im Projekt empfängt. Mit Paketparametern können Sie die Paketausführung ändern, ohne das Paket bearbeiten und erneut bereitstellen zu müssen.  
  
 **Vertraulich**  
 Geben Sie an, ob der Parameter vertraulich ist, indem Sie das Kontrollkästchen aktivieren oder deaktivieren. Vertrauliche Parameterwerte werden im Katalog verschlüsselt und in Transact-SQL oder SQL Server Management Studio als NULL-Wert angezeigt.  
  
 **Erforderlich**  
 Geben Sie an, ob für den Parameter ein anderer als der Entwurfsstandardwert angegeben werden muss, bevor das Paket ausgeführt werden kann.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
  
