---
title: Anpassen der Datenbankerstellung und -bereitstellung durch Erstellungs- und Bereitstellungs-Contributors | Microsoft-Dokumentation
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: fe2064bb-e01e-4a12-9f12-a99aa9a5203f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 547fb6e8bc880fc98d4cf1f3592e550edfaab735
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666249"
---
# <a name="customize-database-build-and-deployment-by-using-build-and-deployment-contributors"></a>Datenbank-Build und -Bereitstellung anpassen durch Verwendung von Erstellungs- und Bereitstellungs-Contributors
Visual Studio bietet Erweiterungspunkte, mit deren Hilfe Sie das Verhalten der Erstellungs- und Bereitstellungsaktionen für Datenbankprojekte ändern können.  
  
## <a name="available-extensibility-points"></a>Verfügbare Erweiterungspunkte  
Sie können eine Erweiterung für die Erweiterungspunkte erstellen, wie in der folgenden Tabelle zu sehen:  
  
|**Aktion**|**Contributor-Typ**|**Hinweise**|  
|--------------|------------------------|-------------|  
|Erstellen|BuildContributor|Diese Art von Erweiterung wird ausgeführt, wenn das SQL-Projekt nach vollständiger Überprüfung des Projektmodells erstellt wird. Der Erstellungs-Contributor hat Zugriff auf das fertige Modell sowie auf alle Eigenschaften der Erstellungsaufgabe und auf sämtliche benutzerdefinierte Argumente.|  
|Bereitstellen|DeploymentPlanModifier|Diese Art von Erweiterung wird ausgeführt, wenn das SQL-Projekt nach der Generierung (aber noch vor der Ausführung) des Bereitstellungsplans als Teil der Bereitstellungspipeline bereitgestellt wird. Mithilfe eines DeploymentPlanModifier-Elements können Sie dem Bereitstellungsplan Schritte hinzufügen oder Schritte daraus entfernen. Bereitstellungs-Contributors haben Zugriff auf den Bereitstellungsplan, auf die Vergleichsergebnisse sowie auf das Quell- und Zielmodell.|  
|Bereitstellen|DeploymentPlanExecutor|Diese Art von Erweiterung wird bei der Ausführung des Bereitstellungsplans ausgeführt und bietet schreibgeschützten Zugriff auf den Bereitstellungsplan. Die durch das DeploymentPlanExectutor-Element ausgeführten Aktionen basieren auf dem Bereitstellungsplan.|  
  
### <a name="supported-extensibility-scenarios"></a>Unterstützte Erweiterungsszenarien  
Sie können Erstellungs- oder Bereitstellungs-Contributors implementieren, um folgende Beispielszenarien zu ermöglichen:  
  
-   **Generieren einer Schemadokumentation im Rahmen der Projekterstellung**: Für dieses Szenario wird ein Element vom Typ [BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx) implementiert und die OnExecute-Methode überschrieben, um die Schemadokumentation zu generieren. Sie können eine Zieldatei mit Definitionen von Standardargumenten erstellen, die steuern, ob die Erweiterung ausgeführt wird. Außerdem können Sie den Namen der Ausgabedatei angeben.  
  
-   **Generieren eines Unterschiedeberichts beim Bereitstellen eines SQL-Projekts**: Für dieses Szenario wird ein Element vom Typ [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) implementiert, durch das die XML-Datei beim Bereitstellen des SQL-Projekts generiert wird.  
  
-   **Ändern des Bereitstellungsplans, um den Verschiebungszeitpunkt von Daten zu ändern**: Für dieses Szenario wird ein Element vom Typ [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) implementiert und der Bereitstellungsplan durchlaufen. Für jedes im Plan enthaltene Element vom Typ SqlTableMigrationStep wird das Vergleichsergebnis untersucht, um zu ermitteln, ob der Schritt ausgeführt oder übersprungen werden soll.  
  
-   **Kopieren von Dateien in das generierte DACPAC-Paket beim Bereitstellen eines SQL-Projekts**: Für dieses Szenario wird ein Bereitstellungs-Contributor implementiert und die OnEstablishDeploymentConfiguration-Methode überschrieben, um die Dateien anzugeben, die vom Projektsystem als DeploymentExtensionConfiguration markiert wurden. Diese Dateien sollen in den Ausgabeordner kopiert und dem generierten DACPAC-Paket hinzugefügt werden. Sie können den Contributor auch ändern, um mehrere Dateien zu einer neuen Datei zusammenzufassen, die dann in den Ausgabeordner kopiert und dem Bereitstellungsmanifest hinzugefügt wird. Im Rahmen der Bereitstellung können Sie die OnApplyDeploymentConfiguration-Methode implementieren, um die Dateien aus dem DACPAC-Paket zu extrahieren und sie für die Verwendung in der OnExecute-Methode vorbereiten.  
  
Darüber hinaus können Sie angepasste Name/Wert-Argumentpaare aus Ihrem Contributor verfügbar machen, die in die Datenbankprojektdatei geschrieben werden. Mithilfe dieser Argumente können Sie dem Contributor das Extrahieren von Informationen aus MSBuild oder dem Endbenutzer des Contributors das Anpassen des Verhaltens ermöglichen. So können Sie den Benutzern beispielsweise die Angabe des Namens einer Ein- oder Ausgabedatei ermöglichen.  
  
## <a name="common-tasks"></a>Allgemeine Aufgaben  
  
|**Allgemeine Aufgaben**|**Hilfreiche Themen**|  
|--------------------|--------------------------|  
|**Weitere Informationen zu den Erweiterbarkeitspunkten**: Informieren Sie sich über die Basisklassen für die Implementierung von Erstellungs- und Bereitstellungs-Contributors.|[BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx)<br /><br />[DeploymentContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentcontributor.aspx)|  
|**Erstellen von Beispiel-Contributors**: Lernen Sie die erforderlichen Schritte zum Erstellen eines Erstellungs- oder Bereitstellungs-Contributors kennen. In diesen exemplarischen Vorgehensweisen lernen Sie Folgendes:<br /><br />–   Erstellen eines Erstellungs-Contributors zum Generieren eines Berichts mit einer Liste aller im Modell enthaltenen Elemente<br />–   Erstellen eines Bereitstellungs-Contributors zum Ändern des Bereitstellungsplans vor dessen Ausführung<br />–   Erstellen eines Bereitstellungs-Contributors zum Generieren eines Bereitstellungsberichts beim Bereitstellen eines SQL-Projekts<br /><br />Contributors können alle in einer einzelnen Assembly oder in mehreren Assemblys erstellt werden – je nachdem, wie Sie die Contributors auf Ihr Team verteilen möchten.|[Exemplarische Vorgehensweise: Erweitern eines Datenbankprojektbuilds zum Generieren von Modellstatistiken](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)<br /><br />[Exemplarische Vorgehensweise: Erweitern einer Datenbankprojektbereitstellung zum Bearbeiten des Bereitstellungsplans](../ssdt/walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan.md)<br /><br />[Exemplarische Vorgehensweise: Bereitstellung des Datenbankprojekts erweitern, um den Bereitstellungsplan zu analysieren](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Definieren benutzerdefinierter Bedingungen für SQL-Komponententests](https://msdn.microsoft.com/library/jj860449(v=vs.103).aspx)  
  
