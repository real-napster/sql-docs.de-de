---
title: Definieren einer Statusvariablen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45d66152-883a-49a7-a877-2e8ab45f8f79
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b0dcc3c1709943207834aab6ef4b39453b2d89d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387428"
---
# <a name="define-a-state-variable"></a>Definieren einer Statusvariablen
  In diesem Verfahren wird beschrieben, wie Sie eine Paketvariable definieren, in der der CDC-Status gespeichert wird.  
  
 Die CDC-Statusvariable wird geladen, initialisiert und vom CDC-Steuerungstask aktualisiert. Anschließend wird sie von der CDC-Quelldatenflusskomponente verwendet, um den aktuellen Verarbeitungsbereich für Änderungsdatensätze zu bestimmen. Die CDC-Statusvariable kann für beliebige Containerelemente definiert werden, die vom CDC-Steuerungstask und der CDC-Quelle gemeinsam verwendet werden. Dies ist auf Paketebene möglich, aber auch in anderen Containern, z. B. einem Schleifencontainer.  
  
 Das manuelle Ändern des Werts von CDC-Statusvariablen ist nicht zu empfehlen, aber es kann zum Verständnis des Inhalts von Variablen beitragen.  
  
 Die folgende Tabelle enthält eine allgemeine Beschreibung der Komponenten von CDC-Statusvariablenwerten.  
  
|Komponente|Description|  
|---------------|-----------------|  
|`<state-name>`|Der Name des aktuellen CDC-Status.|  
|`CS`|Kennzeichnet den aktuellen Startpunkt für den Verarbeitungsbereich (aktueller Start).|  
|`<cs-lsn>`|Die letzte in der vorangehenden CDC-Ausführung verarbeitete Protokollfolgenummer (LSN).|  
|`CE`|Kennzeichnet den aktuellen Endpunkt für den Verarbeitungsbereich (aktuelles Ende). Das Vorhandensein der CE-Komponente im CDC-Status zeigt an, dass entweder gerade ein CDC-Paket verarbeitet wird oder dass ein CDC-Paketfehler aufgetreten ist, bevor der zugehörige CDC-Verarbeitungsbereich vollständig verarbeitet wurde.|  
|`<ce-lsn>`|Die letzte in der aktuellen CDC-Ausführung zu verarbeitende Protokollfolgenummer (LSN). Es wird immer vorausgesetzt, dass die letzte zu verarbeitende Protokollfolgenummer der höchsten Nummer (0xFFF…) entspricht.|  
|`IR`|Kennzeichnet den anfänglichen Verarbeitungsbereich.|  
|`<ir-start>`|Eine Protokollfolgenummer einer Änderung unmittelbar vor Beginn des erstmaligen Ladevorgangs.|  
|`<ir-end>`|Eine Protokollfolgenummer einer Änderung unmittelbar nach Ende des erstmaligen Ladevorgangs.|  
|`TS`|Kennzeichnet den Zeitstempel des letzten CDC-Statusupdates.|  
|**\<Zeitstempel>**|Dezimale 64-Bit-Darstellung der System.DateTime.UtcNow-Eigenschaft.|  
|`ER`|Wird angezeigt, wenn der letzte Vorgang fehlerhaft war, und enthält eine kurze Beschreibung der Fehlerursache. Wenn diese Komponente vorhanden ist, wird sie immer zuletzt angezeigt.|  
|`<short-error-text>`|Eine kurze Fehlerbeschreibung.|  
  
 Die LSNs und Folgenummern sind jeweils als hexadezimale Zeichenfolge von bis zu 20 Ziffern codiert, die den LSN-Wert "Binary(10)" darstellen.  
  
 In der folgenden Tabelle werden die möglichen CDC-Statuswerte beschrieben.  
  
|Status|Description|  
|-----------|-----------------|  
|(INITIAL)|Der ursprüngliche Status, bevor ein Paket für die aktuelle CDC-Gruppe ausgeführt wurde. Dieser Status liegt auch vor, wenn der CDC-Status leer ist.|  
|ILSTART (Initial Load Started)|Der Status beim Start des anfänglich geladenen Pakets, nachdem der CDC-Steuerungstask durch den `MarkInitialLoadStart`-Vorgang aufgerufen wurde.|  
|ILEND (Initial Load Ended)|Der Status nach erfolgreicher Beendigung des anfänglich geladenen Pakets, nachdem der CDC-Steuerungstask durch den `MarkInitialLoadEnd`-Vorgang aufgerufen wurde.|  
|ILUPDATE (Initial Load Update)|Der Status bei der Ausführung des Trickle-Feed-Updatepakets im Anschluss an den erstmaligen Ladevorgang, während der anfängliche Verarbeitungsbereich noch verarbeitet wird. Dieser Schritt erfolgt nach dem Aufruf des CDC-Steuerungstasks durch den `GetProcessingRange`-Vorgang.<br /><br /> Wenn die __$reprocessing-Spalte verwendet wird, wird sie auf 1 festgelegt, um anzugeben, dass das Paket möglicherweise Zeilen erneut verarbeitet, die bereits im Ziel vorhanden sind.|  
|TFEND (Trickle-Feed Update Ended)|Der für reguläre CDC-Ausführungen erwartete Status. Er gibt an, dass die vorherige Ausführung erfolgreich abgeschlossen wurde und eine neue Ausführung mit einem neuen Verarbeitungsbereich gestartet werden kann.|  
|TFSTART|Der Status bei nachfolgenden Ausführungen des Trickle-Feed-Updatepakets nach dem Aufruf des CDC-Steuerungstasks durch den `GetProcessingRange`-Vorgang.<br /><br /> Gibt an, dass eine reguläre CDC-Ausführung gestartet, aber noch nicht einwandfrei beendet wurde (`MarkProcessedRange`).|  
|TFREDO (Reprocessing Trickle-Feed Updates)|Der Status bei einem `GetProcessingRange`-Vorgang, der nach TFSTART stattfindet. Er gibt an, dass die vorherige Ausführung nicht erfolgreich abgeschlossen wurde.<br /><br /> Wenn die __$reprocessing-Spalte verwendet wird, wird sie auf 1 festgelegt, um anzugeben, dass das Paket möglicherweise Zeilen erneut verarbeitet, die bereits im Ziel vorhanden sind.|  
|ERROR|Die CDC-Gruppe befindet sich in einem Fehlerstatus.|  
  
 Nachfolgend finden Sie Beispiele für Werte von CDC-Statusvariablen.  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   TFEND/CS/0x0000025B000001BC0003/TS/2011-07-17T12:05:58.1001145/  
  
-   TFSTART/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:43.9344900/  
  
-   TFREDO/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:59.5544900/  
  
### <a name="to-define-a-cdc-state-variable"></a>So definieren Sie eine CDC-Statusvariable  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das über den CDC-Fluss verfügt, in dem Sie die Variable definieren müssen.  
  
2.  Klicken Sie auf die Registerkarte **Paket-Explorer** , und fügen Sie eine neue Variable hinzu.  
  
3.  Geben Sie der Variablen einen aussagekräftigen Namen, damit sie als Statusvariable erkennbar ist.  
  
4.  Geben Sie der Variablen den Datentyp **Zeichenfolge** .  
  
 Weisen Sie der Variablen als Teil ihrer Definition keinen Wert zu. Der Wert muss vom CDC-Steuerungstask festgelegt werden.  
  
 Wenn Sie den CDC-Steuerungstask mit der Option **Automatic State Persistence**verwenden möchten, wird die CDC-Statusvariable aus der von Ihnen angegebenen Datenbankstatustabelle gelesen. Wenn sich der Wert ändert, wird die Aktualisierung dann ebenfalls für diese Tabelle durchgeführt. Weitere Informationen zur Statustabelle finden Sie unter [CDC Control Task](../control-flow/cdc-control-task.md)und [CDC Control Task Editor](../cdc-control-task-editor.md).  
  
 Wenn Sie den CDC-Steuerungstask nicht mit der Option Automatic State Persistence verwenden, müssen Sie den Variablenwert aus dem persistentem Speicher laden, in dem der Wert bei der letzten Ausführung des Pakets gespeichert wurde. In diesen persistenten Speicher wird der Wert auch zurückgeschrieben, nachdem die Verarbeitung des aktuellen Verarbeitungsbereichs abgeschlossen wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [CDC Control Task](../control-flow/cdc-control-task.md)   
 [CDC Control Task Editor](../cdc-control-task-editor.md)  
  
  
