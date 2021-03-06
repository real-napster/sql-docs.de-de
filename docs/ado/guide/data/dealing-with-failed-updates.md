---
title: Umgang mit fehlerhaften Updates | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9930e76c902080cb7df22bf2a28afc1ae18b3cfd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472372"
---
# <a name="dealing-with-failed-updates"></a>Umgang mit fehlerhaften Updates
Wenn ein Update mit Fehlern abgeschlossen ist, hängt wie Sie die Fehler beheben von der Art und Schweregrad der Fehler und die Logik Ihrer Anwendung. Wenn die Datenbank für andere Benutzer freigegeben ist, ist ein typischer Fehler jedoch, dass eine andere Person auf das Feld ändert, vor dem Ausführen. Diese Art von Fehler ist einen Konflikt wird aufgerufen. ADO erkennt dies und meldet einen Fehler.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Update-Fehler vorliegen, werden sie in einer Fehlerbehandlungsroutine aufgefangen werden. Filtern Sie das Recordset mit der Konstante vorliegt, sodass nur die in Konflikt stehende Zeilen angezeigt werden. In diesem Beispiel die Fehlerbehebung Strategie ist es lediglich des Autors des ersten und letzten Namen (Au_fname und Au_lname).  
  
 Der Code aus, um dem Benutzer, die Update-Konflikt aufmerksam sieht folgendermaßen aus:  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Batchmodus](../../../ado/guide/data/batch-mode.md)
