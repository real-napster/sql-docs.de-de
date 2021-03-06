---
title: Fehlermeldungen (Visual FoxPro-ODBC-Treiber) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b24db48d6a76c221e72944e8e5e6826cb8d5d55
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804418"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Fehlermeldungen (Visual FoxPro-ODBC-Treiber)
Wenn ein Fehler auftritt, wird von der Visual FoxPro-Treiber die folgenden Informationen zurückgegeben:  
  
-   Die systemeigene Fehlernummer und der Text der Fehlermeldung  
  
-   SQLSTATE (ODBC-Fehlercode) und Text der Fehlermeldung  
  
 Sie können diese Fehlerinformationen an, durch den Aufruf [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Systemeigene Fehler  
 Für Fehler, die in der Datenquelle auftreten, gibt der Visual FoxPro-Treiber zurück, die systemeigene Fehlernummer und Fehlermeldung angezeigt. Eine Liste mit systemeigenen Fehlernummern finden Sie [Visual FoxPro-ODBC-Treiber Native Fehlermeldungen](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC-Fehlercodes)  
 Für Fehler, die erkannt und zurückgegeben, die von der Visual FoxPro-Treiber ordnet der Treiber die zurückgegebene systemeigene Fehlernummer dem entsprechenden SQLSTATE zu. Wenn eine systemeigene Fehlernummer keine ODBC-Fehlercode zuordnen, gibt der Visual FoxPro-Treiber SQLSTATE S1000 (Allgemeine Fehler).  
  
 Eine Liste der SQLSTATE-Werten, die von der Visual FoxPro-ODBC-Treiber für die entsprechende Visual FoxPro-Fehler generiert, finden Sie unter [ODBC-Fehlercodes](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Syntax  
 Fehlermeldungen weisen folgendes Format:  
  
 **[** *Hersteller* **] [** *ODBC_component* **]** *Error_message*  
  
 Die Präfixe in eckige Klammern ([]) ermitteln die Ursache des Fehlers, wie in der folgenden Tabelle definiert.  
  
|Datenquelle|Präfix|value|  
|-----------------|------------|-----------|  
|Treiber-Manager|[Hersteller]<br />[ODBC_component]<br />[Data_source]|[Microsoft]<br />[ODBC-Treiber-Manager]<br />–|  
|Visual FoxPro-Treiber|Hersteller]<br />[ODBC_component]<br />[Data_source]|[Microsoft]<br />[Visual FoxPro-ODBC-Treiber]<br />–|  
  
 Wenn die Datei nützlich in der Visual FoxPro-ODBC-Treiber nicht finden konnte, kann es z. B. die folgende Fehlermeldung zurück:  
  
 "[*Microsoft*] [*ODBC-Visual FoxPro-Treiber*] Datei"nützlich"ist nicht vorhanden."
