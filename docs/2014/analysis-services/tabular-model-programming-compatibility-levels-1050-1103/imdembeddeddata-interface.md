---
title: IMDEmbedded-Schnittstelle | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 9dba8c68-4bef-4c2b-815c-c286f1a1939b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 83e46e9b62359623093415ca456ecadd72f847cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757778"
---
# <a name="imdembedded-interface"></a>IMDEmbedded-Schnittstelle
  Die IMDEmbedded-Schnittstelle ist eine öffentliche Schnittstelle, die verwendet wurde, um eine eingebettete PowerPivot-Datenbank oder eine tabellarische Modelldatenbank zu verwalten. Die Schnittstelle erbt von der `IPersistStream`-Schnittstelle. Die Schnittstelle lässt folgende Vorgänge zu:  
  
-   Ruft einen Bezeichner in den eingebetteten Datenstrom im Containerdokument ab.  
  
-   Legt die URL des Containerdokuments fest.  
  
-   Legt ein Flag fest, das angibt, ob sich die Einbettungsanwendung in einer gehosteten Umgebung befindet.  
  
-   Legt den Pfad zu den von der Einbettungsanwendung verwendeten temporären Dateien fest.  
  
-   Bricht den aktuellen Einbettungsvorgang ab.  
  
-   Rufen Sie die geschätzte Größe (in Byte) des Datenstroms um das eingebettete Objekt zu speichern. Wird von `IPersistStream` geerbt.  
  
-   Überprüfen Sie, wenn die eingebettete Datenbank seit der letzten Speicherung geändert hat. Wird von `IPersistStream` geerbt.  
  
-   Laden Sie die eingebettete Datenbank in die lokale oder prozessinterne Engine. Wird von `IPersistStream` geerbt.  
  
-   Speichert die lokale oder prozessinterne Datenbank im eingebetteten Datenstrom im Containerdokument. Wird von `IPersistStream` geerbt.  
  
## <a name="reference"></a>Referenz  
 Die folgenden verweisen auf Dokumente, die `IMDEmbedded` Schnittstelle wie in **msmd.h** Headerdatei.  
  
### <a name="source-file-pxoembeddeddataidl"></a>Quelldatei: PXOEmbeddedData.idl  
  
```  
[  
  local,                            
  object,                           
  uuid(6B6691CF-5453-41c2-ADD9-4F320B7FD421),                       
  pointer_default(unique)           
]  
interface IMDEmbeddedData : IPersistStream  
{  
 [id(1), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in] BOOL in_fIsHosted);  
  
 [id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
  
 [id(3), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
  
 [id(4), helpstring("Set the path used by the embedding application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
  
 [id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
};  
```  
  
### <a name="imdembeddeddatagetstreamidentifier"></a>IMDEmbeddedData::GetStreamIdentifier  
  
```  
HRESULT GetStreamIdentifier (  
    [out, retval] BSTR * out_pbstrStreamId  
    )  
```  
  
#### <a name="description"></a>Description  
 Ruft den von der Hostanwendung verwendeten Bezeichner in den eingebetteten Datenstrom im Containerdokument ab.  
  
#### <a name="parameters"></a>Parameter  
 *out_pbstrStreamId*  
 Gibt die Position des Datenstrombezeichners an.  
  
#### <a name="return-value"></a>Rückgabewert  
 `S_OK`  
 Der Datenstrombezeichner wurde erfolgreich zurückgegeben.  
  
 `S_FALSE`  
 Es ist kein Datenstrombezeichner vorhanden.  
  
 `E_FAIL`  
 Beim Zugriff auf den Datenstrombezeichner ist ein Fehler aufgetreten.  
  
#### <a name="remarks"></a>Hinweise  
 Um zu überprüfen, ob die aktuelle Verbindung eine eingebettete Datenbank enthält, sollte der Benutzer den Wert der DBPROP_MSMD_EMBEDDED_DATA-Eigenschaft in den OLE DB-Verbindungseigenschaften überprüfen.  
  
 Die möglichen Werte für DBPROP_MSMD_EMBEDDED_DATA lauten wie folgt:  
  
|Name|Wert|Definition|  
|----------|-----------|----------------|  
|DBPROPVAL_EMBED_NONE|0x00|Es ist keine eingebettete Datenbank verfügbar.|  
|DBPROPVAL_EMBED_EMBEDDED|0x01|Die aktuelle Anwendung enthält die eingebettete Datenbank.|  
|DBPROPVAL_EMBED_LINKED|0x02|Die eingebettete Datenbank wird in einer remote-Anwendung (z. B. SharePoint-Server) gehostet.|  
  
#### <a name="source"></a>Source  
  
```  
[id(1), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
```  
  
### <a name="imdembeddeddatasetcontainerurl"></a>IMDEmbeddedData::SetContainerURL  
  
```  
HRESULT SetContainerURL (  
    [in] BSTR in_bstrURL  
    )  
```  
  
#### <a name="description"></a>Description  
 Legt die URL für die Datei fest, die den eingebetteten Datenstrom enthält.  
  
#### <a name="parameters"></a>Parameter  
 *in_bstrURL*  
 Gibt die URL für das Containerdokument an.  
  
#### <a name="return-value"></a>Rückgabewert  
 `S_OK`  
 Die Container-URL wurde erfolgreich festgelegt.  
  
 `E_FAIL`  
 Beim Festlegen der Container-URL ist ein Fehler aufgetreten.  
  
#### <a name="source"></a>Source  
  
```  
[id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
```  
  
### <a name="imdembeddeddatasethosted"></a>IMDEmbeddedData::SetHosted  
  
```  
HRESULT SetHosted (  
    [in] BOOL in_fIsHosted  
    )  
```  
  
#### <a name="description"></a>Description  
 Legt ein Flag fest, das angibt, ob sich die Einbettungsanwendung in einer gehosteten Umgebung befindet.  
  
#### <a name="parameters"></a>Parameter  
 *in_ftHosted*  
 TRUE für Aufrufer in einer gehosteten Dienstanwendung (wie IIS)  
  
#### <a name="return-value"></a>Rückgabewert  
 `S_OK`  
 Das Flag wurde erfolgreich festgelegt.  
  
 `E_FAIL`  
 Beim Festlegen des Flags ist ein Fehler aufgetreten.  
  
#### <a name="source"></a>Source  
  
```  
[id(5), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in]  BOOL in_fIsHosted);  
```  
  
### <a name="imdembeddeddatasettempdirpath"></a>IMDEmbeddedData::SetTempDirPath  
  
```  
HRESULT SetTempDirPath (  
    [in] BSTR in_bstrPath  
    )  
```  
  
#### <a name="description"></a>Description  
 Legt den Pfad zu den von der Einbettungsanwendung verwendeten temporären Dateien fest.  
  
#### <a name="parameters"></a>Parameter  
 *in_bstrPath*  
 Der Pfad, der von der Hostanwendung für temporäre Dateien verwendet wird.  
  
#### <a name="return-value"></a>Rückgabewert  
 `S_OK`  
 Das Verzeichnis für temporäre Dateien wurde erfolgreich festgelegt.  
  
 `E_FAIL`  
 Beim Festlegen des Pfads ist ein Fehler aufgetreten.  
  
#### <a name="source"></a>Source  
  
```  
[id(4), helpstring("Set the path used by the host application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
```  
  
### <a name="imdembeddeddatacancel"></a>IMDEmbeddedData::Cancel  
  
```  
HRESULT Cancel ( void )  
```  
  
#### <a name="description"></a>Description  
 Bricht den aktuellen Vorgang für die eingebettete Datenbank ab.  
  
#### <a name="parameters"></a>Parameter  
 Keine.  
  
#### <a name="return-value"></a>Rückgabewert  
 `S_OK`  
 Der Vorgang wurde erfolgreich abgebrochen.  
  
 `DB_E_CANTCANCEL`  
 Es wird aktuell kein abbrechbarer Vorgang ausgeführt.  
  
 `E_FAIL`  
 Beim Abbrechen des eingebetteten Vorgangs ist ein Fehler aufgetreten.  
  
#### <a name="source"></a>Source  
  
```  
[id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
```  
  
### <a name="imdembeddeddatagetsizemax-ipersiststreamgetsizemax"></a>IMDEmbeddedData::GetSizeMax (IPersistStream::GetSizeMax)  
  
```  
HRESULT GetSizeMax (  
    [out] ULARGE_INTEGER * out_pcbSize  
    )  
```  
  
#### <a name="description"></a>Description  
 Ruft die geschätzte Größe des Datenstroms (in Byte) zum Speichern des eingebetteten Objekts ab. Wird von `IPersistStream` geerbt.  
  
#### <a name="parameters"></a>Parameter  
 *in_bstrPath*  
 Die geschätzte Größe des eingebetteten Datenbankbilds (in Byte).  
  
#### <a name="return-value"></a>Rückgabewert  
 `S_OK`  
 Die Größe wurde erfolgreich abgerufen.  
  
 `E_FAIL`  
 Beim Abrufen der Größe ist ein Fehler aufgetreten.  
  
### <a name="imdembeddeddataisdirty-ipersiststreamisdirty"></a>IMDEmbeddedData::IsDirty (IPersistStream::IsDirty)  
  
```  
HRESULT IsDirty ( void )  
```  
  
#### <a name="description"></a>Description  
 Überprüft, ob sich die eingebettete Datenbank seit der letzten Speicherung geändert hat. Wird von `IPersistStream` geerbt.  
  
#### <a name="parameters"></a>Parameter  
 none  
  
#### <a name="return-values"></a>Rückgabewert(e)  
 `S_OK`  
 Die Datenbank wurde seit der letzten Speicherung geändert.  
  
 `S_FALSE`  
 Die Datenbank wurde seit der letzten Speicherung nicht geändert.  
  
 `E_FAIL`  
 Beim Abrufen des Datenbankstatus ist ein Fehler aufgetreten.  
  
### <a name="imdembeddeddataload-ipersiststreamload"></a>IMDEmbeddedData::Load (IPersistStream::Load)  
  
```  
HRESULT Load (   
    [in] IStream * in_pStm   
    )  
```  
  
#### <a name="description"></a>Description  
 Lädt die eingebettete Datenbank in die lokale oder prozessinterne Engine. Wird von `IPersistStream` geerbt.  
  
#### <a name="parameters"></a>Parameter  
 *in_pStm*  
 Ein Zeiger auf eine Datenstromschnittstelle, von der die eingebettete Datenbank geladen werden soll.  
  
#### <a name="return-values"></a>Rückgabewert(e)  
 `S_OK`  
 Die Datenbank wurde erfolgreich geladen.  
  
 `E_OUTOFMEMORY`  
 Der Arbeitsspeicher reicht zum Laden der Datenbank nicht aus.  
  
 `E_FAIL`  
 Beim Laden der Datenbank ist ein anderer Fehler als `E_OUTOFMEMORY` aufgetreten.  
  
### <a name="imdembeddeddatasave-ipersiststreamsave"></a>IMDEmbeddedData::Save (IPersistStream::Save)  
  
```  
HRESULT Save (   
    [in] IStream * in_pStm,  
    [in] BOOL in_fClearDirty  
    )  
```  
  
#### <a name="description"></a>Description  
 Speichert die lokale oder prozessinterne Datenbank in den eingebetteten Datenstrom im Containerdokument an. Wird von `IPersistStream` geerbt.  
  
#### <a name="parameters"></a>Parameter  
 *in_pStm*  
 Ein Zeiger auf eine Datenstromschnittstelle, in der die eingebettete Datenbank gespeichert werden soll.  
  
 *in_fClearDirty*  
 Ein Flag, das angibt, ob das modifizierte Flag nach diesem Vorgang gelöscht werden soll.  
  
#### <a name="return-values"></a>Rückgabewert(e)  
 `S_OK`  
 Die Datenbank wurde erfolgreich gespeichert.  
  
 `STG_E_CANTSAVE`  
 Beim Speichern der Datenbank ist ein anderer Fehler als `STG_E_MEDIUMFULL` aufgetreten.  
  
 `STG_E_MEDIUMFULL`  
 Die Datenbank konnte nicht gespeichert werden, da auf dem Speichergerät kein Speicherplatz mehr verfügbar ist.  
  
  
