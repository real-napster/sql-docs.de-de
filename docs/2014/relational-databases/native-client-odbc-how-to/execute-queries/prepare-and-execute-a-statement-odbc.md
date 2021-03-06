---
title: Vorbereiten und Ausführen von Anweisungen (ODBC) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statement execution
- statement preparation
ms.assetid: 0adecc63-4da5-486c-bc48-09a004a2fae6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcc1f6d1542928d534d31c6d64ef6130c0c7e04b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359912"
---
# <a name="prepare-and-execute-a-statement-odbc"></a>Vorbereiten und Ausführen von Anweisungen (ODBC)
    
### <a name="to-prepare-a-statement-once-and-then-execute-it-multiple-times"></a>So bereiten Sie eine Anweisung vor und führen sie dann mehrmals aus  
  
1.  Rufen Sie [SQLPrepare-Funktion](https://go.microsoft.com/fwlink/?LinkId=59360) , die Anweisung vorzubereiten.  
  
2.  Rufen Sie optional [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) um zu bestimmen, die Anzahl von Parametern in der vorbereiteten Anweisung.  
  
3.  Optional führen Sie für jeden Parameter in der vorbereiteten Anweisung Folgendes aus:  
  
    -   Rufen Sie [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) zum Abrufen von Informationen zu den Parametern.  
  
    -   Jeder Parameter an eine Programmvariable zu binden, indem [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md). Richten Sie alle Data-at-Execution-Parameter ein.  
  
4.  Für jede Ausführung einer vorbereiteten Anweisung gilt:  
  
    -   Wenn die Anweisung über Parametermarkierungen verfügt, fügen Sie die Datenwerte in den gebundenen Parameterpuffer ein.  
  
    -   Rufen Sie [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) zur Ausführung der vorbereiteten Anweisung.  
  
    -   Wenn Data-at-Execution-Eingabeparameter verwendet werden, [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) wird SQL_NEED_DATA zurückgegeben. Senden Sie die Daten in Blöcken mit [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405) und [SQLPutData](../../native-client-odbc-api/sqlputdata.md).  
  
### <a name="to-prepare-a-statement-with-column-wise-parameter-binding"></a>So bereiten Sie eine Anweisung mit spaltenweiser Parameterbindung vor  
  
1.  Rufen Sie [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) auf, um die folgenden Attribute festzulegen:  
  
    -   Legen Sie SQL_ATTR_PARAMSET_SIZE auf die Anzahl von Sätzen (S) von Parametern fest.  
  
    -   Legen Sie SQL_ATTR_PARAM_BIND_TYPE auf SQL_PARAMETER_BIND_BY_COLUMN fest.  
  
    -   Legen Sie das SQL_ATTR_PARAMS_PROCESSED_PTR-Attribut fest, um auf eine SQLUINTEGER-Variable zu zeigen und die Anzahl der verarbeiteten Parameter zu halten.  
  
    -   Legen Sie das SQL_ATTR_PARAMS_STATUS_PTR-Attribut fest, sodass es auf ein Array mit S SQLUSSMALLINT-Variablen zeigt, welche die Parameterstatusindikatoren enthalten.  
  
2.  Rufen Sie SQLPrepare, um die Anweisung vorzubereiten.  
  
3.  Rufen Sie optional [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) um zu bestimmen, die Anzahl von Parametern in der vorbereiteten Anweisung.  
  
4.  Rufen Sie optional für jeden Parameter in der vorbereiteten Anweisung SQLDescribeParam auf, um Parameterinformationen abzurufen.  
  
5.  Führen Sie folgende Aktionen für jeden Parametermarker durch:  
  
    -   Weisen Sie ein Array mit S-Parameterpuffern zu, um Datenwerte zu speichern.  
  
    -   Weisen Sie ein Array mit S-Parameterpuffern zu, um Datenlängen zu speichern.  
  
    -   Rufen Sie SQLBindParameter, um die Parameter Daten Wert und die datenlängenarrays an den Anweisungsparameter zu binden.  
  
    -   Falls der Parameter ein Data-at-Execution-Textparameter oder –Imageparameter ist, richten Sie ihn ein.  
  
    -   Wenn Data-at-Execution-Parameter verwendet werden, richten Sie sie ein.  
  
6.  Für jede Ausführung einer vorbereiteten Anweisung gilt:  
  
    -   Fügen Sie die S Datenwerte und S Datenlängen in die gebundenen Parameterarrays ein.  
  
    -   Rufen Sie SQLExecute auf, um die vorbereitete Anweisung auszuführen.  
  
    -   Wenn Data-at-Execution-Eingabeparameter verwendet werden, wird die SQLExecute SQL_NEED_DATA zurückgegeben. Senden Sie die Daten in Segmenten mit der SQLParamData und SQLPutData.  
  
### <a name="to-prepare-a-statement-with-row-wise-bound-parameters"></a>So bereiten Sie eine Anweisung mit zeilenweiser Parameterbindung vor  
  
1.  Ordnen Sie ein Array [S] von Strukturen zu, wobei S der Anzahl von Parametersätzen entspricht. Die Struktur verfügt über ein Element für jeden Parameter, und jedes Element verfügt über zwei Teile:  
  
    -   Der erste Teil ist eine Variable des entsprechenden Datentyps zum Speichern der Parameterdaten.  
  
    -   Der zweite Teil ist eine SQLINTEGER-Variable zum Speichern des Statusindikators.  
  
2.  Rufen Sie [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) auf, um die folgenden Attribute festzulegen:  
  
    -   Legen Sie SQL_ATTR_PARAMSET_SIZE auf die Anzahl von Sätzen (S) von Parametern fest.  
  
    -   Legen Sie SQL_ATTR_PARAM_BIND_TYPE auf die Größe der in Schritt 1 zugeordneten Struktur fest.  
  
    -   Legen Sie das SQL_ATTR_PARAMS_PROCESSED_PTR-Attribut fest, um auf eine SQLUINTEGER-Variable zu zeigen und die Anzahl der verarbeiteten Parameter zu halten.  
  
    -   Legen Sie das SQL_ATTR_PARAMS_STATUS_PTR-Attribut fest, sodass es auf ein Array mit S SQLUSSMALLINT-Variablen zeigt, welche die Parameterstatusindikatoren enthalten.  
  
3.  Rufen Sie SQLPrepare, um die Anweisung vorzubereiten.  
  
4.  Rufen Sie für jeden Parametermarker SQLBindParameter, um die Parameter Wert und den datenlängenzeigern zeigen Sie auf die Variablen im ersten Element des Arrays mit Strukturen, die in Schritt 1 zugewiesen wurden. Falls der Parameter ein Data-at-Execution-Parameter ist, richten Sie ihn ein.  
  
5.  Für jede Ausführung einer vorbereiteten Anweisung gilt:  
  
    -   Füllen Sie das gebundene Parameterpufferarray mit Datenwerten.  
  
    -   Rufen Sie SQLExecute auf, um die vorbereitete Anweisung auszuführen. Der Treiber führt die SQL-Anweisung S Mal aus, einmal für jeden Parametersatz.  
  
    -   Wenn Data-at-Execution-Eingabeparameter verwendet werden, wird die SQLExecute SQL_NEED_DATA zurückgegeben. Senden Sie die Daten in Segmenten mit der SQLParamData und SQLPutData.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Abfragen: Themen zur Vorgehensweise &#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
