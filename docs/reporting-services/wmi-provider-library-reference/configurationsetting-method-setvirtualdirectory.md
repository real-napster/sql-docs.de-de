---
title: 'SetVirtualDirectory-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec27288ab12d74dd89a34f5c238d77c507913cf1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847718"
---
# <a name="configurationsetting-method---setvirtualdirectory"></a>ConfigurationSetting-Methode: SetVirtualDirectory
  Legt den Namen des virtuellen Verzeichnisses für eine angegebene Anwendung fest.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *Application*  
 Der für das virtuelle Verzeichnis festzulegende Name der Anwendung.  
  
 *VirtualDirectory*  
 Der Name des virtuellen Verzeichnisses  
  
 *lcid*  
 Die Gebietsschema-ID für das virtuelle Verzeichnis  
  
 *Fehler*  
 [out] Die Beschreibung des Fehlers, der aufgetreten ist  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## <a name="remarks"></a>Remarks  
 Eine Anwendung kann nur einen Namen für ein virtuelles Verzeichnis für alle URL-Reservierungen verwenden.  
  
 VirtualDirectory muss den Namenskonventionen für virtuelle Verzeichnisse entsprechen. VirtualDirectory darf keine leere Zeichenfolge sein.  
  
 Aktualisiert den Wert des \Configuration\URLReservations\Application\VirtualDirectory-Elements. Ist erfolgreich, auch wenn noch keine URL-Reservierungen erstellt wurden.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
