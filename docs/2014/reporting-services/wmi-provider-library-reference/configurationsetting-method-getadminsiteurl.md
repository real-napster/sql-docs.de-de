---
title: GetAdminSiteUrl-Methode (WMI) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- GetAdminSiteUrl method
ms.assetid: fbc5bf3c-120c-4aec-a4f2-f5391bd415f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f99a269139c6c6be3cb52632481236eaa2ecf0f5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2019
ms.locfileid: "59939886"
---
# <a name="getadminsiteurl-method-wmi"></a>GetAdminSiteUrl-Methode (WMI)
  Ruft die absolute URL für die Zentraladministrationswebsite für die Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]-, [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]-, [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]- oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Farm ab, in die der Berichtsserver integriert ist  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub GetAdminSiteUrl(ByRef AdminSiteUrl as String, _  
ByRef HRESULT as Int32)  
```  
  
```csharp  
public void GetAdminSiteUrl(out string AdminSiteUrl, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *AdminSiteUrl*  
 [out] Eine Zeichenfolge, die die absolute URL für die Zentraladministrationswebsite für die SharePoint-Farm enthält, in die der Berichtsserver integriert ist.  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Methoden](msreportserver-configurationsetting-methods.md)  
  
  
