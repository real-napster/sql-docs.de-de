---
title: HTTP-Verbindungs-Manager-Editor (Seite) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 730b055542296edad39bd3a8322d1b9110b7a7b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768012"
---
# <a name="http-connection-manager-editor-server-page"></a>HTTP-Verbindungs-Manager-Editor (Seite Server)
  Mithilfe der Registerkarte **Server** des Dialogfelds **HTTP-Verbindungs-Manager-Editor** können Sie den HTTP-Verbindungs-Manager konfigurieren, indem Sie Eigenschaften, z. B. URL und Sicherheitseinstellungen, angeben. Eine HTTP-Verbindung ermöglicht Paketen den Zugriff auf einen Webserver, indem zum Senden und Empfangen von Dateien HTTP verwendet wird. Nach der Konfiguration des HTTP-Verbindungs-Managers können Sie die Verbindung testen.  
  
> [!IMPORTANT]  
>  Der HTTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 Weitere Informationen zum HTTP-Verbindungs-Manager finden Sie unter [HTTP Connection Manager](connection-manager/http-connection-manager.md). Weitere Informationen zu einem allgemeinen Verwendungsszenario für den HTTP-Verbindungs-Manager finden Sie unter [Web Service Task](control-flow/web-service-task.md).  
  
## <a name="options"></a>Optionen  
 **Server-URL**  
 Geben Sie die URL für den Server ein.  
  
 Wenn Sie die Schaltfläche **WSDL herunterladen** auf der Seite **Allgemein** im **Editor für den Task 'Webdienst'** verwenden möchten, um eine WSDL-Datei herunterzuladen, geben Sie die URL für die WSDL-Datei ein. Diese URL endet mit "? wsdl".  
  
 **Anmeldeinformationen verwenden**  
 Geben Sie an, ob der HTTP-Verbindungs-Manager zur Authentifizierung die Sicherheitsanmeldeinformationen des Benutzers verwenden soll.  
  
 **Benutzername**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Kennwort**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Domäne**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Clientzertifikat verwenden**  
 Geben Sie an, ob der HTTP-Verbindungs-Manager zur Authentifizierung ein Clientzertifikat verwenden soll.  
  
 **Zertifikat**  
 Wählen Sie mithilfe des Dialogfelds **Zertifikat auswählen** ein Zertifikat aus der Liste aus. Im Textfeld wird der dem Zertifikat zugeordnete Name angezeigt.  
  
 **Timeout (in Sekunden)**  
 Geben Sie ein Timeout für Verbindungen mit dem Webserver an. Der Standardwert dieser Eigenschaft beträgt 30 Sekunden.  
  
 **Segmentgröße (in KB)**  
 Geben Sie eine Segmentgröße zum Schreiben von Daten an.  
  
 **Verbindung testen**  
 Nachdem die Konfiguration des HTTP-Verbindungs-Managers abgeschlossen ist, bestätigen Sie die Gültigkeit der Verbindung, indem Sie auf **Verbindung testen**klicken.  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [HTTP-Verbindungs-Manager-Editor &#40;Seite „Proxy“&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  
