---
title: Ausführen von Befehlen, die Tabellenwertparameter enthalten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
ms.assetid: 7ecba6f6-fe7a-462a-9aa3-d5115b6d4529
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae08a79bcfe1e4befcad8559e82bdfba5b347fc2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417851"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>Ausführen von Befehlen, die Tabellenwertparameter enthalten
  Die Ausführung eines Befehls, der Tabellenwertparameter enthält, erfordert zwei Phasen:  
  
1.  Angeben der Parametertypen  
  
2.  Binden der Parameterdaten  
  
## <a name="table-valued-parameter-specification"></a>Tabellenwertparameter-Spezifikation  
 Der Consumer kann den Typ des Tabellenwertparameters angeben. Diese Angabe enthält den Typnamen des Tabellenwertparameters. Sie umfasst auch den Schemanamen, wenn der benutzerdefinierte Tabellentyp für den Tabellenwertparameter nicht im aktuellen Standardschema für die Verbindung enthalten ist. Je nach Serverunterstützung kann der Consumer auch optionale Metadateninformationen angeben, wie beispielsweise die Sortierreihenfolge der Spalten. Zudem kann er angeben, dass alle Zeilen für bestimmte Spalten Standardwerte aufweisen sollen.  
  
 Um einen Tabellenwertparameter anzugeben, wird der Consumer ruft ISSCommandWithParameter::SetParameterInfo und ruft optional isscommandwithparameters:: SetParameterProperties. Für einen Tabellenwertparameter verfügt das *pwszDataSourceType*-Feld in der DBPARAMBINDINFO-Struktur über den Wert DBTYPE_TABLE. Die *UlParamSize* -Feld auf festgelegt wurde ~ 0, wenn diese Länge ist unbekannt. Bestimmte Eigenschaften für Tabellenwertparameter, wie z. B. Schemaname, Typname, Spaltenreihenfolge und Standardspalten, können über isscommandwithparameters:: SetParameterProperties festgelegt werden.  
  
## <a name="table-valued-parameter-binding"></a>Tabellenwertparameter-Bindung  
 Ein Tabellenwertparameter kann ein beliebiges Rowsetobjekt sein. Während der Ausführung liest der Anbieter beim Senden von Tabellenwertparametern an den Server aus diesem Objekt.  
  
 Um den Tabellenwertparameter zu binden, ruft der Consumer IAccessor:: CreateAccessor. Das *wType*-Feld der DBBINDING-Struktur für den Tabellenwertparameter wird auf DBTYPE_TABLE festgelegt. Das *pObject*-Element der DBBINDING-Struktur ist nicht NULL, und das *iid*-Element von *pObject* wird auf IID_IRowset oder jede beliebige andere Rowsetobjekt-Schnittstelle für Tabellenwertparameter festgelegt. Die verbleibenden Felder in der DBBINDING-Struktur können in der gleichen Weise festgelegt werden wie für gestreamte BLOBs.  
  
 Für die Bindungen des Tabellenwertparameters und des einem Tabellenwertparameter zugeordneten Rowsetobjekts gelten die folgenden Einschränkungen:  
  
-   Die einzigen Statuswerte, die für Rowsetspaltendaten von Tabellenwertparametern zulässig sind, lauten DBSTATUS_S_ISNULL und DBSTATUS_S_OK. DBSTATUS_S_DEFAULT führt zu einem Fehler, und der gebundene Statuswert wird auf DBSTATUS_E_BADSTATUS festgelegt.  
  
-   Ein Tabellenwertparameter kann mit dem Status DBSTATUS_S_DEFAULT markiert werden. Die einzigen gültigen Werte sind DBSTATUS_S_DEFAULT und DBSTATUS_S_OK. Wenn der Status auf DBSTATUS_S_DEFAULT festgelegt ist, entspricht der Wert des Tabellenwertparameters einer leeren Tabelle.  
  
-   Schreibgeschützte Spalten in Tabellenwertparametern (Identitätsspalte und berechnete Spalte) müssen mit der SSPROP_PARAM_TABLE_DEFAULT_COLUMNS-Eigenschaft als Standard markiert werden. Spalten, die einen Standardwert aufweisen, müssen ebenfalls mit der SSPROP_PARAM_TABLE_DEFAULT_COLUMNS-Eigenschaft als Standard markiert werden. Dann kann der Standardwert als Datenwert einer Spalte für einen bestimmten Tabellenwertparameter verwendet werden. Der Anbieter ignoriert die Datenwerte, die an als Standard markierte Spalten gebunden sind.  
  
-   Für Spalten mit DBPROP_COL_AUTOINCREMENT oder SSPROP_COL_COMPUTED werden Daten an den Server gesendet, sofern nicht auch SSPROP_PARAM_TABLE_DEFAULT festgelegt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenwertparameter &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [Verwenden von Tabellenwertparametern &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
