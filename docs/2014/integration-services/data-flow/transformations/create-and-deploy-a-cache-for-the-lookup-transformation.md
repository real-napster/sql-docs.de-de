---
title: Erstellen und Bereitstellen eines Caches für die Transformation für Suche | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- creating cache files for Lookup transformation
- deploying cache files for Lookup transformation
- Lookup transformation cache files
ms.assetid: cedf5cad-2fac-42d0-ad91-9461e117d330
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ef5450bc9598f86909bbb032adcfa4bfc0fc9040
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381068"
---
# <a name="create-and-deploy-a-cache-for-the-lookup-transformation"></a>Erstellen und Bereitstellen eines Cache für die Transformation für Suche
  Sie können eine Cachedatei (.caw) erstellen und für die Transformation zur Suche bereitstellen. Das Verweisdataset wird in der Cachedatei gespeichert.  
  
 Die Transformation für Suche führt Suchvorgänge aus, indem Daten in Eingabespalten aus einer verbundenen Datenquelle mit Spalten in einem Verweisdataset verknüpft werden.  
  
 Sie erstellen eine Cachedatei, indem Sie einen Cacheverbindungs-Manager und eine Transformation für Cachetransformation verwenden. Weitere Informationen finden Sie unter [Cache Connection Manager](../../connection-manager/cache-connection-manager.md) und [Cache Transform](cache-transform.md).  
  
 Weitere Informationen zur Transformation für Suche und zu Cachedateien finden Sie unter [Lookup Transformation](lookup-transformation.md).  
  
### <a name="to-create-a-cache-file"></a>So erstellen Sie eine Cachedatei  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket, und öffnen Sie dann das Paket.  
  
2.  Fügen Sie auf der Registerkarte **Ablaufsteuerung** einen Datenflusstask hinzu.  
  
3.  Fügen Sie auf der Registerkarte **Datenfluss** dem Datenfluss eine Transformation für Cachetransformation hinzu, und verbinden Sie dann die Transformation mit einer Datenquelle.  
  
     Konfigurieren Sie die Datenquelle nach Bedarf.  
  
4.  Doppelklicken Sie auf die Transformation für Cachetransformation, und klicken Sie dann im **Cachetransformations-Editor**auf der Seite **Verbindungs-Manager** auf **Neu** , um einen neuen Cacheverbindungs-Manager zu erstellen.  
  
5.  Konfigurieren Sie den Cacheverbindungs-Manager zum Speichern des Cache im **Editor für Cacheverbindungs-Manager**auf der Registerkarte **Allgemein** , indem Sie die folgenden Optionen auswählen:  
  
    1.  Wählen Sie **Dateicache verwenden**aus.  
  
    2.  Geben Sie den Dateipfad in das Feld **Dateiname**ein.  
  
     Das System erstellt die Datei, wenn Sie das Paket ausführen.  
  
    > [!NOTE]  
    >  Die Schutzebene des Pakets gilt nicht für die Cachedatei. Wenn die Cachedatei vertrauliche Informationen enthält, schränken Sie den Zugriff auf den Speicherort oder Ordner, in dem Sie die Datei speichern, mithilfe einer Zugriffssteuerungsliste ein. Sie sollten nur bestimmten Konten den Zugriff ermöglichen. Weitere Informationen finden Sie unter [Zugriff auf Dateien, die von Paketen verwendet werden](../../access-to-files-used-by-packages.md).  
  
6.  Klicken Sie auf die Registerkarte **Spalten** , und geben Sie dann mit der Option **Indexposition** an, welche Spalten die Indexspalten sind.  
  
     Für Nicht-Index-Spalten ist die Indexposition 0. Für Indexspalten ist die Indexposition eine fortlaufende positive Zahl.  
  
    > [!NOTE]  
    >  Wenn die Transformation für Suche so konfiguriert ist, dass sie einen Cacheverbindungs-Manager verwendet, können nur Indexspalten im Verweisdataset Eingabespalten zugeordnet werden. Auch müssen alle Indexspalten zugeordnet werden.  
  
     Weitere Informationen finden Sie unter [Cache Connection Manager Editor](../../cache-connection-manager-editor.md).  
  
7.  Konfigurieren Sie die Cacheumwandlung nach Bedarf.  
  
     Weitere Informationen finden Sie unter [Cachetransformations-Editor &#40;Seite „Verbindungs-Manager“&#41;](../../cache-transformation-editor-connection-manager-page.md) und [Cachetransformations-Editor &#40;Seite „Zuordnungen“&#41;](../../cache-transformation-editor-mappings-page.md).  
  
8.  Führen Sie das Paket aus.  
  
### <a name="to-deploy-a-cache-file"></a>So stellen Sie eine Cachedatei bereit  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket, und öffnen Sie dann das Paket.  
  
2.  Erstellen Sie optional eine Paketkonfiguration. Weitere Informationen finden Sie unter [Erstellen von Paketkonfigurationen](../../create-package-configurations.md).  
  
3.  Fügen Sie die Cachedatei dem Projekt hinzu, indem Sie wie folgt vorgehen:  
  
    1.  Wählen Sie im Projektmappen-Explorer das Projekt aus, das Sie in Schritt 1 geöffnet haben.  
  
    2.  Klicken Sie im Menü **Projekt** auf **Vorhandenes Element hinzufügen**.  
  
    3.  Wählen Sie die Cachedatei aus, und klicken Sie dann auf **Hinzufügen**.  
  
     Die Datei wird im Projektmappen-Explorer im Ordner **Sonstige** angezeigt.  
  
4.  Konfigurieren Sie das Projekt, um ein Bereitstellungshilfsprogramm zu erstellen, und erstellen Sie anschließend das Projekt. Weitere Informationen finden Sie unter [Create a Deployment Utility](../../create-a-deployment-utility.md).  
  
     Die Manifestdatei „\<*Projektname*>.SSISDeploymentManifest.xml“ wird erstellt. Diese Datei enthält eine Auflistung der verschiedenen Dateien im Projekt, der Pakete und der Paketkonfigurationen.  
  
5.  Stellen Sie das Paket für das Dateisystem bereit. Weitere Informationen finden Sie unter [Deploy Packages by Using the Deployment Utility](../../deploy-packages-by-using-the-deployment-utility.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Bereitstellungs-Hilfsprogramms](../../create-a-deployment-utility.md)  
  
  
