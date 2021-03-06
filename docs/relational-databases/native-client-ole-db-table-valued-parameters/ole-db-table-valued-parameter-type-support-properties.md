---
title: OLE DB-Unterstützung für Tabellenwertparameter-Typen (Eigenschaften) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (properties)
ms.assetid: b9c4e6ed-fe4f-4ef8-9bc8-784d80d44039
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 372a4859c80fc58dff37080e9383ffeebc1721a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465602"
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>OLE DB-Unterstützung von Tabellenwertparameter-Typen (Eigenschaften)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Dieses Thema stellt Informationen zu OLE DB-Eigenschaften und -Eigenschaftensätzen bereit, die Tabellenwertparameter-Rowsetobjekten zugeordnet werden.  
  
## <a name="properties"></a>Eigenschaften  
 Im Folgenden werden die Eigenschaften aufgelistet, die durch die IRowsetInfo::GetProperties-Methode für Tabellenwertparameter-Rowsetobjekte verfügbar gemacht werden. Beachten Sie, dass alle Tabellenwertparameter-Rowseteigenschaften schreibgeschützt sind. Aus diesem Grund versucht, Festlegen der Eigenschaften über IOpenRowset:: OPENROWSET oder ITableDefinitionWithConstraints::CreateTableWithConstraints Methoden auf die Standardwerte, führt zu einem Fehler und kein Objekt erstellt werden.  
  
 Im Tabellenwertparameter-Rowsetobjekt nicht implementierte Eigenschaften werden hier nicht aufgelistet. Eine vollständige Liste von Eigenschaften finden Sie in der OLE DB-Dokumentation in den Windows Data Access Components.  
  
|Eigenschafts-ID|Wert|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|R/W: Schreibgeschützt<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Lesezeichen sind für Tabellenwertparameter-Rowsetobjekte nicht zulässig.|  
|DBPROP_BOOKMARKSKIPPED|VARIANT_FALSE|  
|DBPROP_BOOKMARKTYPE|DBPROPVAL_BMK_NUMERIC|  
|DBPROP_CANHOLDROWS|VARIANT_FALSE|  
|DBPROP_CHANGEINSERTEDROWS|VARIANT_TRUE|  
|DBPROP_COLUMNRESTRICT|VARIANT_FALSE|  
|DBPROP_COMMANDTIMEOUT|0|  
|DBPROP_COMMITPRESERVE|VARIANT_TRUE|  
|DBPROP_DEFERRED|VARIANT_FALSE|  
|DBPROP_DELAYSTORAGEOBJECTS|VARIANT_FALSE|  
|DBPROP_IAccessor<br /><br /> DBPROP_IColumnsInfo<br /><br /> DBPROP_IConvertType<br /><br /> DBPROP_IRowset<br /><br /> DBPROP_IRowsetInfo,<br /><br /> DBPROP_IColumnsRowset|VARIANT_TRUE|  
|DBPROP_IConnectionPointContainer<br /><br /> DBPROP_IMultipleResults<br /><br /> DBPROP_IRowsetUpdate<br /><br /> DBPROP_IRowsetIdentity<br /><br /> DBPROP_IRowsetLocate<br /><br /> DBPROP_IRowsetScroll<br /><br /> DBPROP_IRowsetResynch|VARIANT_FALSE|  
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> Hinweis: Das Tabellenwertparameter-Rowsetobjekt unterstützt die IRowsetChange-Schnittstellen.<br /><br /> Ein mit DBPROP_IRowsetChange gleich VARIANT_TRUE erstelltes Rowset zeigt Verhaltensweisen des Sofortupdatemodus.<br /><br /> Wenn BLOB-Spalten allerdings als ISequentialStream-Objekte gebunden werden, wird vom Consumer erwartet, dass er sie für die Lebenszeit des Tabellenwertparameter-Rowsetobjekts beibehält.|  
|DBPROP_ISupportErrorInfo|VARIANT_TRUE|  
|DBPROP_ISequentialStream|VARIANT_TRUE|  
|DBPROP_IMMOBILEROWS|VARIANT_TRUE|  
|DBPROP_LITERALIDENTITY|VARIANT_TRUE|  
|DBPROP_LOCKMODE|DBPROPVAL_LM_NONE|  
|DBPROP_MAXOPENROWS|0|  
|DBPROP_MAXPENDINGROWS|0|  
|DBPROP_MAXROWS|0|  
|DBPROP_NOTIFICATIONPHASES|0|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|0|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE|VARIANT_FALSE|  
|DBPROP_OWNINSERT<br /><br /> DBPROP_OWNUPDATEDELETE|VARIANT_TRUE|  
|DBPROP_QUICKRESTART|VARIANT_TRUE|  
|DBPROP_REENTRANTEVENTS|VARIANT_FALSE|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|  
|DBPROP_RETURNPENDINGINSERTS|VARIANT_TRUE|  
|DBPROP_ROWRESTRICT|VARIANT_FALSE|  
|DBPROP_ROWTHREADMODEL|DBPROPVAL_RT_FREETHREAD|  
|DBPROP_SERVERCURSOR|VARIANT_FALSE|  
|DBPROP_SERVERDATAONINSERT|VARIANT_FALSE|  
|DBPROP_STRONGIDENTITY|VARIANT_TRUE|  
|DBPROP_TRANSACTEDOBJECT|VARIANT_FALSE|  
|DBPROP_UNIQUEROWS|VARIANT_FALSE|  
|DBPROP_UPDATABILITY|DBPROPVAL_UP_CHANGE &#124; DBPROPVAL_UP_DELETE &#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>Eigenschaftensätze  
 Die folgenden Eigenschaftensätze unterstützen Tabellenwertparameter.  
  
### <a name="dbpropsetsqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 Diese Eigenschaft wird vom Consumer ggf. beim Erstellen einer Tabellenwertparameter-Rowsetobjekt mit ITableDefinitionWithConstraints::CreateTableWithConstraints für jede Spalte über DBCOLUMNDESC-Struktur, bei Bedarf verwendet.  
  
|Eigenschafts-ID|Eigenschaftswert|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|R/W: Lese-/Schreibzugriff<br /><br /> Standard: VARIANT_FALSE<br /><br /> Typ: VT_BOOL<br /><br /> Beschreibung: Bei Festlegung auf VARIANT_TRUE gibt an, dass die Spalte eine berechnete Spalte ist. VARIANT_FALSE gibt an, dass sie keine berechnete Spalte ist.|  
  
### <a name="dbpropsetsqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 Diese Eigenschaften sind vom Consumer beim Erkennen des Tabellenwertparameter-Typinformationen in Aufrufen von isscommandwithparameters:: Getparameterproperties gelesen und vom Consumer festlegen bestimmte Eigenschaften zu den Tabellenwertparameter festgelegt über isscommandwithparameters:: SetParameterProperties.  
  
 In der folgenden Tabelle werden detaillierte Beschreibungen dieser Eigenschaften bereitgestellt.  
  
|Eigenschafts-ID|Eigenschaftswert|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|R/W: Lese-/Schreibzugriff<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_BSTR<br /><br /> Beschreibung: Consumer verwenden diese Eigenschaft, um den Namen des Tabellenwertparameter-Typs abzurufen oder festzulegen.<br /><br /> Diese Eigenschaft kann auch mit CLR-benutzerdefinierten Typen verwendet werden.<br /><br /> Diese Eigenschaft kann optional angegeben werden, um einen Tabellentypnamen für einen Tabellenwertparameter bereitzustellen (im Falle eines ODBC-Abruf-Syntaxbefehls). Diese Eigenschaft ist für parametrisierte Ad-hoc-SQL-Abfragen erforderlich.|  
|SSPROP_PARAM_TYPE_SCHEMANAME|R/W: Lese-/Schreibzugriff<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_BSTR<br /><br /> Beschreibung: Consumer verwenden diese Eigenschaft zum Abrufen oder Festlegen von den Schemanamen des Tabellenwertparameter-Typs.<br /><br /> Diese Eigenschaft kann auch mit CLR-benutzerdefinierten Typen verwendet werden.|  
|SSPROP_PARAM_TYPE_CATALOGNAME|R/W: Schreibgeschützt<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_BSTR<br /><br /> Beschreibung: Consumer verwenden diese Eigenschaft, um den Katalognamen des Tabellenwertparameter-Typs abzurufen.<br /><br /> Diese Eigenschaft kann auch mit CLR-benutzerdefinierten Typen verwendet werden. Das Festlegen dieser Eigenschaft resultiert in einem Fehler. Benutzerdefinierte Tabellentypen müssen sich in derselben Datenbank wie die Tabellenwertparameter befinden, die die Tabellentypen verwenden.|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|R/W: Lese-/Schreibzugriff<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_UI2 &#124; VT_ARRAY<br /><br /> Beschreibung: Consumer verwenden diese Eigenschaft angegeben sind, dass die Gruppe von Spalten im Rowset als Standard behandelt werden können. Für diese Spalten werden keine Werte gesendet. Während Daten aus dem Consumerrowsetobjekt abgerufen werden, benötigt der Provider keine Bindung für diese Spalten.<br /><br /> Jedes Element des Arrays sollte eine Ordinalzahl einer Spalte im Rowsetobjekt sein. Ungültige Ordinalzahlen führen beim Ausführen des Befehls zu Fehlern.|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|R/W: Lese-/Schreibzugriff<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_UI2 &#124; VT_ARRAY<br /><br /> Beschreibung: Diese Eigenschaft wird vom Consumer verwendet, um einen Hinweis an den Server an, dass die Sortierung Bereitstellen der Spaltendaten. Der Provider führt keinerlei Überprüfung durch und nimmt an, dass der Consumer der bereitgestellten Spezifikation entspricht. Der Server verwendet diese Eigenschaft, um Optimierungen durchzuführen.<br /><br /> Spaltenreihenfolgeninformationen für jede Spalte werden durch ein Paar von Elementen im Array dargestellt. Das erste Element im Paar ist die Nummer der Spalte. Das zweite Element im Paar ist 1 für eine aufsteigende Reihenfolge oder 2 für eine absteigende Reihenfolge.|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Unterstützung für Tabellenwertparameter-Typen](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [Verwenden von Tabellenwertparametern &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
