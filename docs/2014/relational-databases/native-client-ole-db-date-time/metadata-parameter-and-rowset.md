---
title: Parameter und Rowsetmetadaten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
ms.assetid: 31b318a4-20e7-4db0-b367-eb9938859029
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b96876a050f9ba46363792eec22d76640ee6fc2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818115"
---
# <a name="parameter-and-rowset-metadata"></a>Metadaten für Parameter und Rowsets
  Dieses Thema enthält Informationen über den folgenden Typ und die folgenden Typelemente in Verbindung mit den OLE DB-Datums- und Uhrzeitverbesserungen.  
  
-   DBBINDING-Struktur  
  
-   `ICommandWithParameters::GetParameterInfo`  
  
-   `ICommandWithParameters::SetParameterInfo`  
  
-   `IColumnsRowset::GetColumnsRowset`  
  
-   `IColumnsInfo::GetColumnInfo`  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 Die folgenden Informationen werden in der DBPARAMINFO-Struktur durch *prgParamInfo* zurückgegeben:  
  
|Parametertyp|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Löschen|  
|Uhrzeit|DBTYPE_DBTIME2|10|8, 10..16|0..7|Legen Sie|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Löschen|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Löschen|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19,21..27|0..7|Legen Sie|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26,28..34|0..7|Legen Sie|  
  
 Beachten Sie, dass in einigen Fällen Wertbereiche nicht kontinuierlich sind. Der Grund dafür ist das Hinzufügen eines Dezimaltrennzeichens, wenn die Genauigkeit von Bruchteilen größer als 0 (NULL) ist.  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE ist nur gültig, wenn eine Verbindung mit einem [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-Server (oder höher) besteht. Bei einer Verbindung mit einem Downlevelserver ist DBPARAMFLAGS_SS_ISVARIABLESCALE nie festgelegt.  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo und implizite Parametertypen  
 Die in der DBPARAMBINDINFO-Struktur bereitgestellten Informationen müssen Folgendem entsprechen:  
  
|*pwszDataSourceType*<br /><br /> (anbieterspezifisch)|*pwszDataSourceType*<br /><br /> (OLE DB-generisch)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|Wird ignoriert.|  
|date|DBTYPE_DBDATE|6|Wird ignoriert.|  
||DBTYPE_DBTIME|10|Wird ignoriert.|  
|Uhrzeit|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|Wird ignoriert.|  
|DATETIME||16|Wird ignoriert.|  
|datetime2 oder DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 Die *bPrecision* Parameter wird ignoriert.  
  
 Beim Senden von Daten an den Server wird DBPARAMFLAGS_SS_ISVARIABLESCALE ignoriert. Anwendungen können die Verwendung von älteren TDS-Typen (Tabular Data Stream) durch Verwenden der anbieterspezifischen Typnamen "`datetime`" und "`smalldatetime`" erzwingen. Beim Verbinden mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (oder höher)-Server "`datetime2`"-Format verwendet und eine implizite serverkonvertierung wird durchgeführt, sofern erforderlich, wenn der Typname"`datetime2`" oder "DBTYPE_DBTIMESTAMP lautet". *bScale* wird ignoriert, wenn der anbieterspezifische Typname "`datetime`"oder"`smalldatetime`" verwendet werden. Andernfalls müssen Anwendungen sicherstellen, die *bScale* korrekt festgelegt ist. Anwendungen, die ein Upgrade von MDAC und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] verwenden "DBTYPE_DBTIMESTAMP" fehl schlägt, wenn sie nicht festlegen *bScale* ordnungsgemäß. Bei Verbindung mit Serverinstanzen vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tritt für einen anderen *bscale*-Wert als 0 oder 3 mit DBTYPE_DBTIMESTAMP ein Fehler auf und E_FAIL wird zurückgegeben.  
  
 ICommandWithParameters:: SetParameterInfo nicht aufgerufen wird, geben Sie nach der Anbieter Imples den Server aus dem Bindungstyp gemäß IAccessor:: CreateAccessor wie folgt:  
  
|Bindungstyp|*pwszDataSourceType*<br /><br /> (anbieterspezifisch)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|date|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 `IColumnsRowset::GetColumnsRowset` gibt die folgenden Spalten zurück.  
  
|Spaltentyp|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Löschen|  
|Uhrzeit|DBTYPE_DBTIME2|10|8, 10..16|0..7|Legen Sie|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Löschen|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Löschen|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Legen Sie|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Legen Sie|  
  
 In DBCOLUMN_FLAGS hat DBCOLUMNFLAGS_ISFIXEDLENGTH für Datum-/Uhrzeit-Typen stets den Wert TRUE, und die folgenden Flags haben immer den Wert FALSE:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 Die übrigen Flags (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE und DBCOLUMNFLAGS_WRITEUNKNOWN) können festgelegt werden. Dies hängt von der Definition der Spalte und von der eigentlichen Abfrage ab.  
  
 Ein DBCOLUMNFLAGS_SS_ISVARIABLESCALE-Flag wird in DBCOLUMN_FLAGS zur Verfügung gestellt, damit eine Anwendung den Servertyp der Spalten bestimmen kann, wobei DBCOLUMN_TYPE DBTYPE_DBTIMESTAMP ist. DBCOLUMN_SCALE oder DBCOLUMN_DATETIMEPRECISION muss auch verwendet werden, um den Servertyp zu identifizieren.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE ist nur gültig, wenn eine Verbindung mit einem [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-Server (oder höher) besteht. DBPARAMFLAGS_SS_ISVARIABLESCALE ist nicht definiert, wenn eine Verbindung mit einem Downlevelserver besteht.  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 Die DBCOLUMNINFO-Struktur gibt die folgenden Informationen zurück:  
  
|Parametertyp|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Löschen|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|Legen Sie|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Löschen|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Löschen|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Legen Sie|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Legen Sie|  
  
 In *dwFlags* hat DBCOLUMNFLAGS_ISFIXEDLENGTH für Datum-/Uhrzeit-Typen stets den Wert TRUE, und die folgenden Flags haben immer den Wert FALSE:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER, MAYDEFER  
  
 Die übrigen Flags (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE und DBCOLUMNFLAGS_WRITEUNKNOWN) können festgelegt werden.  
  
 In *dwFlags* wird das neue Flag DBCOLUMNFLAGS_SS_ISVARIABLESCALE bereitgestellt, mit dem eine Anwendung den Servertyp von Spalten bestimmen kann, wobei *wType* DBTYPE_DBTIMESTAMP ist. *bScale* muss ebenfalls verwendet werden, um den Servertyp zu identifizieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Metadaten &#40;OLE-DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
  
  
