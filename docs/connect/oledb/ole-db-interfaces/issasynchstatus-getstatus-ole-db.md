---
title: 'Issasynchstatus:: getStatus (OLE DB) | Microsoft-Dokumentation'
description: ISSAsynchStatus::GetStatus (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 1920ce001879baf01a337898c452493dccd430f3
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505076"
---
# <a name="issasynchstatusgetstatus-ole-db"></a>ISSAsynchStatus::GetStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Gibt den Status eines asynchron ausgeführten Vorgangs zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT GetStatus(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation,  
        DBCOUNTITEM *pulProgress,  
        DBCOUNTITEM *pulProgressMax,  
        DBASYNCHPHASE *peAsynchPhase,  
        LPOLESTR *ppwszStatusText);  
```  
  
## <a name="arguments"></a>Argumente  
 *hChapter*[in]  
 Das Kapitelhandle. Wenn das abgerufene Objekt wird nicht in einem Rowset-Objekt, oder der Vorgang nicht für ein Kapitel gilt, sollte er auf DB_NULL_HCHAPTER festgelegt werden die vom Anbieter ignoriert wird.  
  
 *eOperation*[in]  
 Der Vorgang, für den der asynchrone Status angefordert wird. Der folgende Wert sollte verwendet werden:  
  
 DBASYNCHOP_OPEN – Der Consumer fordert Informationen über das asynchrone Öffnen oder Auffüllen eines Rowsets oder über die asynchrone Initialisierung eines Datenquellobjekts an. Wenn der Anbieter OLE DB 2.5-kompatibel ist und die direkte URL-Bindung unterstützt, fordert der Consumer Informationen über die asynchrone Initialisierung oder Auffüllung einer Datenquelle, eines Rowsets, einer Zeile oder eines Datenstromobjekts an.  
  
 *pulProgress*[out]  
 Ein Zeiger auf den Arbeitsspeicher, in dem der aktuelle Status des asynchronen Vorgangs relativ zum erwarteten maximalen Wert, der im *pulProgress* -Parameter angegeben ist, zurückgegeben werden soll. Weitere Informationen über die Bedeutung von *pulProgress*finden Sie in der Beschreibung zu *peAsynchPhase*.  
  
 Wenn *pulProgress* ein NULL-Zeiger ist, wird kein Status zurückgegeben.  
  
 *pulProgressMax*[out]  
 Ein Zeiger auf den Arbeitsspeicher, in dem der erwartete maximale Wert des *pulProgress* -Parameters zurückgegeben werden soll. Dieser Wert ändert sich möglicherweise im Verlauf von Aufrufen für diese Methode. Weitere Informationen über die Bedeutung von *pulProgressMax*finden Sie in der Beschreibung zu *peAsynchPhase*.  
  
 Wenn es sich bei *pulProgressMax* um einen NULL-Zeiger handelt, wird kein erwarteter maximaler Wert zurückgegeben.  
  
 *peAsynchPhase*[out]  
 Ein Zeiger auf den Arbeitsspeicher, in dem weitere Informationen zum Status des asynchronen Vorgangs zurückgegeben werden sollen. Gültige Werte sind:  
  
 DBASYNCHPHASE_INITIALIZATION – Das Objekt befindet sich in einer Initialisierungsphase. Die Argumente *pulProgress* und *pulProgressMax* geben an, wie weit der Vorgang in etwa abgeschlossen ist. Das Objekt ist noch nicht vollständig materialisiert. Der Versuch, andere Schnittstellen aufzurufen, schlägt möglicherweise fehl, und die vollständige Gruppe von Schnittstellen ist möglicherweise für das Objekt nicht verfügbar. Wenn der asynchrone Vorgang die Folge eines Aufrufs von **ICommand::Execute** für einen Befehl zum Aktualisieren, Löschen oder Einfügen von Zeilen war und wenn *cParamSets* größer als 1 ist, zeigen *pulProgress* und *pulProgressMax* möglicherweise den Status für einen einzelnen Parametersatz oder für das gesamte Array von Parametersätzen an.  
  
 DBASYNCHPHASE_POPULATION – Das Objekt befindet sich in einer Auffüllungsphase. Obwohl das Rowset vollständig initialisiert ist und der gesamte Satz von Schnittstellen für das Objekt verfügbar ist, sind möglicherweise zusätzliche Zeilen noch nicht in das Rowset aufgefüllt. Während *pulProgress* und *pulProgressMax* auf die Anzahl der aufgefüllten Zeilen basiert werden kann, werden sie im Allgemeinen auf die Zeit oder den Aufwand basiert, der zum Auffüllen des Rowsets erforderlich ist. Ein Aufrufer sollte daher diese Information als grobe Schätzung ansehen, wie lang der Vorgang dauern könnte, nicht als Schätzung für die letztendliche Zeilenanzahl. Diese Phase wird nur während der Auffüllung eines Rowsets zurückgegeben. Sie wird nie bei der Initialisierung eines Datenquellobjekts oder durch die Ausführung eines Befehls zum Aktualisieren, Löschen oder Einfügen von Zeilen zurückgegeben.  
  
 DBASYNCHPHASE_COMPLETE – Alle asynchronen Verarbeitungsvorgänge für das Objekt sind abgeschlossen. Die **ISSAsynchStatus::GetStatus**-Methode gibt ein HRESULT zurück, das das Ergebnis des Vorgangs angibt. Normalerweise ist dies das HRESULT, das zurückgegeben worden wäre, wäre der Vorgang synchron aufgerufen worden. Wenn der asynchrone Vorgang die Folge eines Aufrufs von **ICommand::Execute** für einen Befehl zum Aktualisieren, Löschen oder Einfügen von Zeilen war, entsprechen *pulProgress* und *pulProgressMax* der Gesamtzahl der Zeilen, die von dem Befehl betroffen sind. Wenn *cParamSets* größer als 1 ist, ist dies die Gesamtanzahl der Zeilen, die von allen während der Ausführung angegebenen Parametersätzen betroffen sind. Wenn es sich bei *peAsynchPhase* um einen NULL-Zeiger handelt, wird kein Statuscode zurückgegeben.  
  
 DBASYNCHPHASE_CANCELED – Die asynchrone Verarbeitung des Objekts wurde abgebrochen. Die **ISSAsynchStatus::GetStatus**-Methode gibt DB_E_CANCELED zurück. Wenn der asynchrone Vorgang die Folge eines Aufrufs von **ICommand::Execute** für einen Befehl zum Aktualisieren, Löschen oder Einfügen von Zeilen war, entspricht *pulProgress* der Gesamtzahl der Zeilen für alle Parametersätze, die von dem Befehl vor dem Abbrechen betroffen wurden.  
  
 *ppwszStatusText*[in/out]  
 Ein Zeiger auf den Arbeitsspeicher, der weitere Informationen über den Vorgang enthält. Mit diesem Wert kann ein Anbieter zwischen verschiedenen Elementen eines Vorgangs unterscheiden, z.B. verschiedene Ressourcen, auf die zugegriffen wurde. Diese Zeichenfolge wird gemäß der DBPROP_INIT_LCID-Eigenschaft für das Datenquellobjekt lokalisiert.  
  
 Wenn *ppwszStatusText* bei Eingabe ungleich NULL ist, gibt der Anbieter den Status in Verbindung mit dem entsprechenden, durch *ppwszStatusText*identifizierten Element zurück. Gibt *ppwszStatusText* kein Element von *eOperation*an, gibt der Anbieter S_OK zurück, wobei *pulProgress* und *pulProgressMax* auf den gleichen Wert festgelegt sind. Wenn der Anbieter nicht zwischen Elementen basierend auf einer wörtlichen ID unterscheidet, setzt er *ppwszStatusText* auf NULL und gibt Informationen über den gesamten Vorgang zurück. Ist *ppwszStatusText* bei Eingabe ungleich NULL, lässt der Anbieter *ppwszStatusText* unverändert.  
  
 Ist *ppwszStatusText* bei Eingabe NULL, legt der Anbieter *ppwszStatusText* auf einen Wert fest, der mehr Informationen über den Vorgang angibt, oder auf NULL, wenn keine derartigen Informationen verfügbar sind oder wenn die **ISSAsynchStatus::GetStatus**-Methode einen Fehler zurückgibt. Wenn *ppwszStatusText* bei Eingabe NULL ist, weist der Anbieter Arbeitsspeicher für die Statuszeichenfolge zu und gibt die Adresse zu diesem Arbeitsspeicher zurück. Der Consumer gibt diesen Arbeitsspeicher mit **IMalloc::Free** frei, wenn die Zeichenfolge nicht mehr benötigt wird.  
  
 Wenn *ppwszStatusText* bei Eingabe NULL ist, wird keine Statuszeichenfolge zurückgegeben, und der Anbieter gibt Informationen über ein Element des Vorgangs oder über den Vorgang insgesamt zurück.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 S_OK  
 Die Methode wurde erfolgreich zurückgegeben.  
  
-   Wenn *peAsynchPhase* gleich DBASYNCHPHASE_INITIALIZATION ist, ist das Objekt noch nicht vollständig initialisiert. Der Versuch, andere Schnittstellen aufzurufen, schlägt möglicherweise fehl, und die vollständige Gruppe von Schnittstellen ist möglicherweise für das Objekt nicht verfügbar.  
  
-   Wenn *peAsynchPhase* gleich DBASYNCHPHASE_POPULATION ist, ist das Rowset vollständig initialisiert und der gesamte Satz von Schnittstellen ist für das Objekt verfügbar. Es sind möglicherweise jedoch zusätzliche Zeilen noch nicht in das Rowset aufgefüllt.  
  
-   Wenn *peAsynchPhase* DBASYNCHPHASE_COMPLETE ist, sind alle asynchronen Verarbeitungsvorgänge für das Objekt abgeschlossen. Das Objekt ist vollständig initialisiert und aufgefüllt.  
  
 DB_E_CANCELED  
 Die asynchrone Verarbeitung wurde während der Rowsetauffüllung abgebrochen. Die Auffüllung wird angehalten, das Rowset bleibt jedoch für die Zeilen, die bereits aufgefüllt wurden, gültig.  
  
 Die asynchrone Verarbeitung wurde während der Initialisierung des Datenquellobjekts abgebrochen. Das Datenquellobjekt befindet sich in einem noch nicht initialisierten Status.  
  
 E_INVALIDARG  
 Der *hChapter* -Parameter ist ungültig.  
  
 E_UNEXPECTED  
 Die **ISSAsynchStatus::GetStatus**-Methode wurde für ein Datenquellenobjekt aufgerufen, für das **IDBInitialize::Initialize** nicht aufgerufen wurde.  
  
 Die **ISSAsynchStatus::GetStatus**-Methode wurde für ein Rowset aufgerufen, **ITransaction::Commit** oder **ITransaction::Abort** wurde aufgerufen, und das Objekt befindet sich in einem Zombiezustand.  
  
 Die **ISSAsynchStatus::GetStatus**-Methode wurde für ein Rowset aufgerufen, das in seiner Initialisierungsphase asynchron abgebrochen wurde. Das Rowset befindet sich in einem Zombiezustand.  
  
 E_FAIL  
 Es ist ein anbieterspezifischer Fehler aufgetreten.  
  
## <a name="remarks"></a>Remarks  
 Die **ISSAsynchStatus**-Methode verhält sich genauso wie die **ISSAsynchStatus::GetStatus**-Methode, gibt jedoch anstelle von DB_E_CANCELED E_UNEXPECTED zurück, wenn die Initialisierung eines Datenquellenobjekts abgebrochen wird (obwohl [ISSAsynchStatus::WaitForAsynchCompletion](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) DB_E_CANCELED zurückgibt). Dies ist darauf zurückzuführen, dass das Datenquellenobjekt nach einem Abbruchvorgang nicht mehr den gewöhnlichen Zombiestatus aufweist, sodass weitere Initialisierungsvorgänge durchgeführt werden können.  
  
 Wenn das Rowset initialisiert oder asynchron aufgefüllt wird, muss es diese Methode unterstützen.  
  
 Zusätzlich zu den aufgeführten Rückgabewerten kann **ISSAsynchStatus::GetStatus** jeden HRESULT-Wert zurückgeben, der von der Methode zurückgegeben worden wäre, die den asynchronen Vorgang eingeleitet hat, und gibt den Erfolg oder das Fehlschlagen eines Vorgangs an.  
  
 Einige asynchrone Vorgänge können möglicherweise nur den Status „beendet“ und „nicht beendet“ zurückgeben. Sie sollten *pulProgressMax* auf den Wert 1 festlegen und so die Alles-oder-Nichts-Granularität ihrer Schätzung angeben. Ihre Antworten wären dann entweder 0/1 oder 1/1.  
  
 Ein Anbieter kann *pulProgressMax* in aufeinander folgenden Aufrufen ändern und sogar ein kleineres Verhältnis zurückgeben als vorher, wenn dies eine verbesserte Schätzung, bis zu welchem Grad der Task abgeschlossen ist, widerspiegelt.  
  
 Der Anbieter ist nicht verpflichtet, mehr Genauigkeit zu garantieren, wird dazu jedoch in Fällen angehalten, in denen sinnvolle Schätzungen für den Abschluss möglich sind. Derartige Bemühungen verbessern die Benutzer-Schnittstellen-Qualität, da die Haupteinsatzmöglichkeit dieser Funktion vermutlich darin besteht, dem Benutzer Feedback zum Status zu geben. Die Benutzerzufriedenheit nimmt mit der Qualität des Feedbacks für einen nicht sichtbaren Task mit langer Laufzeit zu.  
  
 Durch Aufrufen von **ISSAsynchStatus::GetStatus** für ein initialisiertes Datenquellobjekt oder ein aufgefülltes Rowset oder durch Übergeben eines Werts für *eOperation* außer DBASYNCHOP_OPEN wird S_OK zurückgegeben, wobei *pulProgress* und *pulProgressMax* auf den gleichen Wert festgelegt sind. Wenn die **ISSAsynchStatus::GetStatus**-Methode für ein Objekt aufgerufen wird, das durch Ausführung eines Befehls zum Aktualisieren, Löschen oder Einfügen von Zeilen erstellt wurde, gibt sowohl *pulProgress* als auch *pulProgressMax* die Gesamtzahl der Zeilen an, die von dem Befehl betroffen sind.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausführen asynchroner Vorgänge](../../oledb/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE-DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
