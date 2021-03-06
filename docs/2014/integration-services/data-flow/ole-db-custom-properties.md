---
title: Benutzerdefinierte Eigenschaften für OLE DB | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 996acc5f8e9b47af683c8d8376515f7f59e63120
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374917"
---
# <a name="ole-db-custom-properties"></a>Benutzerdefinierte Eigenschaften für OLE DB
  **Benutzerdefinierte Eigenschaften von Quellen**  
  
 Die OLE DB-Quelle verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften der OLE DB-Quelle beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Der zum Zugreifen auf die Datenbank verwendete Modus. Die möglichen Werte sind **geöffnetes Rowset**, **geöffnetes Rowset aus Variable**, `SQL Command`, und **SQL-Befehl aus Variable**. Der Standardwert ist **Geöffnetes Rowset**.|  
|AlwaysUseDefaultCodePage|Boolean|Ein Wert, der angibt, ob der Wert der `DefaultCodePage`-Eigenschaft für jede Spalte verwendet werden soll, oder ob versucht werden soll, die Codepage aus dem Gebietsschema der einzelnen Spalten abzuleiten. Der Standardwert dieser Eigenschaft ist `False`.|  
|CommandTimeout|Integer|Die Anzahl der Sekunden, nach denen ein Befehl wegen eines Timeouts abgebrochen wird. Der Wert 0 steht für ein unbegrenztes Timeout.<br /><br /> Hinweis: Diese Eigenschaft ist nicht verfügbar, in der **Quellen-Editor für OLE DB**, jedoch können festgelegt werden, mithilfe der **Erweiterter Editor**.|  
|DefaultCodePage|Integer|Die zu verwendende Codepage, wenn keine Codepageinformationen aus der Datenquelle verfügbar sind.|  
|OpenRowset|Zeichenfolge|Der Name des Datenbankobjekts, das zum Öffnen eines Rowsets verwendet wird.|  
|OpenRowsetVariable|Zeichenfolge|Die Variable, die den Namen des Datenbankobjekts enthält, das zum Öffnen eines Rowsets verwendet wird.|  
|ParameterMapping|Zeichenfolge|Die Zuordnung von Parametern im SQL-Befehl zu Variablen.|  
|SqlCommand|Zeichenfolge|Der auszuführende SQL-Befehl.|  
|SqlCommandVariable|Zeichenfolge|Die Variable, die den auszuführenden SQL-Befehl enthält.|  
  
 Die Ausgabe und die Ausgabespalten der OLE DB-Quelle verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [OLE DB Source](ole-db-source.md).  
  
 **Benutzerdefinierte Eigenschaften von Zielen**  
  
 Das OLE DB-Ziel verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften des OLE DB-Ziels beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
> [!NOTE]  
>  Die hier aufgelisteten FastLoad-Optionen (FastLoadKeepIdentity, FastLoadKeepNulls und FastLoadOptions) entsprechen den Eigenschaften mit ähnlichen Bezeichnungen der `IRowsetFastLoad`-Schnittstelle, die vom Microsoft OLE DB Provider for SQL Server (SQLOLEDB) bereitgestellt wird. Weitere Informationen finden Sie unter IRowsetFastLoad in der MSDN Library.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Ganze Zahl (Enumeration)|Ein Wert, der angibt, wie das Ziel auf seine Zieldatenbank zugreift.<br /><br /> Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> `OpenRowset` (0): Sie geben Sie den Namen einer Tabelle oder Sicht.<br />`OpenRowset from Variable` (1): Sie geben Sie den Namen einer Variablen, die den Namen einer Tabelle oder Sicht enthält.<br />`OpenRowset Using Fastload` (3): Sie geben Sie den Namen einer Tabelle oder Sicht.<br />`OpenRowset Using Fastload from Variable` (4): Sie geben Sie den Namen einer Variablen, die den Namen einer Tabelle oder Sicht enthält.<br />`SQL Command` (2): Sie können SQL-Anweisung angeben.|  
|AlwaysUseDefaultCodePage|Boolean|Ein Wert, der angibt, ob der Wert der `DefaultCodePage`-Eigenschaft für jede Spalte verwendet werden soll, oder ob versucht werden soll, die Codepage aus dem Gebietsschema der einzelnen Spalten abzuleiten. Der Standardwert dieser Eigenschaft ist `False`.|  
|CommandTimeout|Integer|Die maximale Ausführungsdauer in Sekunden, bevor ein Timeout für den SQL-Befehl eintritt. Der Wert 0 steht für eine unbegrenzte Dauer. Der Standardwert dieser Eigenschaft ist 0.<br /><br /> Hinweis: Diese Eigenschaft ist nicht verfügbar, in der **Ziel-Editor für OLE DB**, jedoch können festgelegt werden, mithilfe der **Erweiterter Editor**.|  
|DefaultCodePage|Integer|Die dem OLE DB-Ziel zugeordnete Standardcodepage.|  
|FastLoadKeepIdentity|Boolean|Ein Wert, der angibt, ob Identitätswerte beim Laden von Daten kopiert werden sollen. Diese Eigenschaft ist nur verfügbar, wenn eine der Optionen für das schnelle Laden verwendet wird. Der Standardwert dieser Eigenschaft ist `False`. Diese Eigenschaft entspricht der OLE DB [IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) Eigenschaft `SSPROP_FASTLOADKEEPIDENTITY`.|  
|FastLoadKeepNulls|Boolean|Ein Wert, der angibt, ob NULL-Werte beim Laden von Daten kopiert werden sollen. Diese Eigenschaft ist nur verfügbar, wenn eine der Optionen für das schnelle Laden verwendet wird. Der Standardwert dieser Eigenschaft ist `False`. Diese Eigenschaft entspricht der OLE DB [IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) Eigenschaft `SSPROP_FASTLOADKEEPNULLS`.|  
|FastLoadMaxInsertCommitSize|Integer|Ein Wert, der die Batchgröße angibt, für die das OLE DB-Ziel bei schnellen Ladevorgängen die Durchführung eines Commits versucht. Der Standardwert **0**gibt einen einzelnen Commitvorgang an, wenn alle Zeilen verarbeitet wurden.|  
|FastLoadOptions|Zeichenfolge|Eine Auflistung von Optionen für schnelles Laden. Die Optionen für schnelles Laden beinhalten das Sperren von Tabellen und die Überprüfung von Einschränkungen. Sie können eines, beides oder keines von beiden angeben. Diese Eigenschaft entspricht der OLE DB-IRowsetFastLoad-Eigenschaft `SSPROP_FASTLOADOPTIONS` und akzeptiert Zeichenfolgenoptionen wie z. B. `CHECK_CONSTRAINTS` und `TABLOCK`.<br /><br /> Hinweis: Einige Optionen für diese Eigenschaft sind nicht verfügbar, in der **Ziel-Editor für Excel**, jedoch können festgelegt werden, mithilfe der **Erweiterter Editor**.|  
|OpenRowset|Zeichenfolge|Wenn AccessMode ist `OpenRowset`, den Namen der Tabelle oder Sicht, die das OLE DB-Ziel zugreift.|  
|OpenRowsetVariable|Zeichenfolge|Wenn AccessMode ist `OpenRowset from Variable`, den Namen der Variablen mit dem Namen der Tabelle oder Sicht, die das OLE DB-Ziel zugreift.|  
|SqlCommand|Zeichenfolge|Wenn AccessMode ist `SQL Command`, die Transact-SQL-Anweisung, OLE DB-Ziel die Zielspalten für die Daten angibt.|  
  
 Die Eingabe und die Eingabespalten des OLE DB-Ziels verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [OLE DB Destination](ole-db-destination.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Common Properties](../common-properties.md)  
  
  
