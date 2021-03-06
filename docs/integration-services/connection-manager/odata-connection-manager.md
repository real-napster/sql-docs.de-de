---
title: OData-Verbindungs-Manager | Microsoft-Dokumentation
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 20421d29832aab8fdeb9532c335c689a1314ad2e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276204"
---
# <a name="odata-connection-manager"></a>OData-Verbindungs-Manager
 Stellen Sie eine Verbindung mit einer OData-Quelle mit einem OData-Verbindungs-Manager her. Eine OData-Quellkomponente stellt über einen OData-Verbindungs-Manager eine Verbindung mit einer OData-Quelle her und verwendet die Daten des Diensts. Weitere Informationen finden Sie unter [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Hinzufügen eines OData-Verbindungs-Managers zu einem SSIS-Paket  
 Sie können einem SSIS-Paket einen neuen OData-Verbindungs-Manager auf drei Arten hinzufügen:  
  
-   Klicken Sie im **Quellen-Editor für OData** auf die Schaltfläche **Neu...**.  
  
-   Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Ordner **Verbindungs-Manager**, und klicken Sie anschließend auf **Neuer Verbindungs-Manager**. Wählen Sie unter **Typ des Verbindungs-Managers** die Option **ODATA**aus.  
  
-   Klicken Sie unten im Paket-Designer mit der rechten Maustaste auf **Verbindungs-Manager**, und wählen Sie **Neue Verbindung** aus. Wählen Sie unter **Typ des Verbindungs-Managers** die Option **ODATA**aus.  
  
## <a name="connection-manager-authentication"></a>Verbindungs-Manager-Authentifizierung  
 Der OData-Verbindungs-Manager unterstützt fünf Authentifizierungsmodi.  
  
-   Windows-Authentifizierung  
  
-   Standardauthentifizierung (mit Benutzername und Kennwort)  

-   Microsoft Dynamics AX Online (mit Benutzername und Kennwort)
  
-   Microsoft Dynamics CRM Online (mit Benutzername und Kennwort)
  
-   Microsoft Online Services (mit Benutzername und Kennwort)  
  
Für den anonymen Zugriff wählen Sie die Option „Windows-Authentifizierung“ aus.  

Sie können die **Microsoft Online Services**-Authentifizierungsoption nicht verwenden, um mit Microsoft Dynamics AX Online oder Microsoft Dynamics CRM Online eine Verbindung herzustellen. Sie können auch keine Option verwenden, die für Multi-Factor Authentication konfiguriert ist.
  
### <a name="specifying-and-securing-credentials"></a>Festlegen und Sichern von Anmeldeinformationen  
 Wenn der OData-Dienst die Standardauthentifizierung erfordert, können Sie im [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)einen Benutzernamen und ein Kennwort angeben. Die Werte, die Sie in den Editor eingeben, werden im Paket beibehalten. Der Kennwortwert wird gemäß der Schutzebene des Pakets verschlüsselt.  
  
 Es gibt mehrere Möglichkeiten, die Werte für Benutzername und Kennwort zu parametrisieren oder außerhalb des Pakets gespeichert. Beispielsweise können Sie Parameter verwenden oder die Eigenschaften des Verbindungs-Managers beim Ausführen des Pakets aus SQL Server Management Studio direkt festlegen.  
  
## <a name="odata-connection-manager-properties"></a>Eigenschaften des OData-Verbindungs-Managers  
 In der folgenden Liste werden die Eigenschaften des OData-Verbindungs-Managers beschrieben.  
  
|||  
|-|-|  
|Eigenschaft|und Beschreibung|  
|URL|Die URL zum Dienstdokument.|  
|UserName|Benutzername für die Authentifizierung, falls erforderlich.|  
|Kennwort|Kennwort für die Authentifizierung, falls erforderlich.|  
|ConnectionString|Enthält weitere Eigenschaften des Verbindungs-Managers.|  
  
## <a name="odata-connection-manager-editor"></a>OData-Verbindungs-Manager-Editor
  Verwenden Sie das Dialogfeld **OData-Verbindungs-Manager-Editor**, um eine Verbindung hinzufügen oder eine vorhandene Verbindung mit einer OData-Datenquelle zu bearbeiten.  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Name des Verbindungs-Managers.  
  
 **Speicherort des Dienstdokuments**  
 URL für den OData-Dienst. Beispiel: https://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Authentifizierung**  
Wählen Sie eine der folgenden Optionen aus:
-   **Windows-Authentifizierung**. Wählen Sie diese Option für den anonymen Zugriff aus.
-   **Standardauthentifizierung** 
-   **Microsoft Dynamics AX Online** für Dynamics AX Online
-   **Microsoft Dynamics CRM Online** für Dynamics CRM Online
-   **Microsoft Online Services** für Microsoft Online Services

Wenn Sie eine andere Option als die Windows-Authentifizierung auswählen, geben Sie **Benutzernamen** und **Kennwort** ein. 

Sie können die **Microsoft Online Services**-Authentifizierungsoption nicht verwenden, um mit Microsoft Dynamics AX Online oder Microsoft Dynamics CRM Online eine Verbindung herzustellen. Sie können auch keine Option verwenden, die für Multi-Factor Authentication konfiguriert ist.

 **Verbindung testen**  
 Klicken Sie auf diese Schaltfläche, um die Verbindung mit der OData-Quelle zu testen.  
