---
title: 'ListReportServersInDatabase-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eeb8b39355eac3526fa42aea08df33b32c70472a
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2019
ms.locfileid: "59957986"
---
# <a name="listreportserversindatabase-method-wmi-msreportserverconfigurationsetting"></a>ListReportServersInDatabase-Methode (WMI: MSReportServer_ConfigurationSetting)
  Gibt die Liste von Berichtsserverinstallationen zurück, die in der Berichtsserver-Datenbank vorhanden sind. Dies geschieht unabhängig davon, ob diese Installationen Zugriff auf sichere Informationen haben.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parameter  
 *MachineNames[]*  
 [out] Ein Array, das die Computernamen für die Berichtsserverinstallationen in der Datenbank enthält  
  
 *InstanceNames[]*  
 [aus] Ein Array mit den Instanznamen der einzelnen Berichtsserverinstallationen in der Datenbank.  
  
 *InstallationIDs[]*  
 [out] Ein Array, das die Installations-IDs für jede Berichtsserverinstallation in der Datenbank enthält  
  
 *IsInitialized[]*  
 [out] Ein Array, das den Initialisierungsstatus für jede Berichtsserverinstallation in der Datenbank enthält  
  
 *Länge*  
 [out] Die Länge der von der Methode zurückgegebenen Arrays Alle zurückgegebenen Arrays haben die gleiche Länge.  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
 *ExtendedErrors[]*  
 [out] Ein Zeichenfolgenarray, das zusätzliche Fehler enthält, die durch den Aufruf zurückgegeben werden  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 ListReportServersInDatabase listet die Berichtsserverinstallationen auf, die in der Berichtsserver-Datenbank vorhanden sind. Dies geschieht unabhängig davon, ob diese Installationen Zugriff auf sichere Informationen haben, und es wird ein übereinstimmender Satz von Arrays mit Informationen zu jeder Installation zurückgegeben.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](msreportserver-configurationsetting-members.md)  
  
  
