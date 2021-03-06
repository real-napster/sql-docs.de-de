---
title: Konfigurieren der Schwellenwerte für Bereinigung und Abgleich | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: fdab2d77dddf565e2d94b27b2b7b46c70aafa4f0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010561"
---
# <a name="configure-threshold-values-for-cleansing-and-matching"></a>Konfigurieren der Schwellenwerte für Bereinigung und Abgleich

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Thema wird beschrieben, wie Schwellenwerte, die während den computerunterstützten Bereinigungs- und Abgleichsaktivitäten in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) verwendet werden, konfiguriert werden.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen die Rolle „dqs_administrator“ in der DQS_MAIN-Datenbank haben, um diese Schwellenwerte zu konfigurieren.  
  
##  <a name="Configure"></a> Konfigurieren der Schwellenwerte  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Konfiguration**.  
  
3.  Klicken dann auf die Registerkarte **Allgemeine Einstellungen** . Diese Registerkarte ermöglicht es Ihnen, Schwellenwerte für die Bereinigungs- und Abgleichsaktivitäten anzugeben.  
  
4.  Um Schwellenwerte für die Bereinigungsaktivität anzugeben, geben Sie entsprechende Werte in den folgenden Feldern im Bereich **Interaktive Bereinigung** an:  
  
    -   **Mindestergebnis für Vorschläge:** Das Mindestergebnis oder der Vertrauensgrad, der von DQS zum Vorschlagen von Ersetzungen für einen Wert während des computerunterstützten Bereinigungsprozesses verwendet wird. Geben Sie einen Wert in der Dezimalnotation des entsprechenden Prozentwerts ein. Geben Sie beispielsweise 0,75 für 75 % ein. Dieser Wert sollte kleiner oder gleich dem Wert sein, der im Feld **Mindestergebnis für automatische Korrekturen** angegeben wurde. Der Standardwert ist 0,7.  
  
    -   **Mindestergebnis für automatische Korrekturen:** Das Mindestergebnis oder der Vertrauensgrad, der von DQS zum automatischen Korrigieren eines Werts während des computerunterstützten Bereinigungsprozesses verwendet wird. Geben Sie einen Wert in der Dezimalnotation des entsprechenden Prozentwerts ein. Geben Sie beispielsweise 0,9 für 90 % ein. Der Standardwert ist 0,8.  
  
5.  Um einen Schwellenwert für die Abgleichsaktivität anzugeben, geben Sie einen Wert im Feld **Mindestergebnis für Datensätze** unter dem Bereich **Abgleich** an. Dieser Wert gibt das minimale Ergebnis für einen Datensatz an, das als Übereinstimmung mit einem anderen Datensatz betrachtet werden soll. Der Standardwert ist 80 %.  
  
6.  Klicken Sie auf **Schließen**.  
  
  
