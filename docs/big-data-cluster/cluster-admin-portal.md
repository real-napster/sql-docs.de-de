---
title: Cluster-Verwaltungsportal
titleSuffix: SQL Server big data clusters
description: Erfahren Sie, wie das Verwaltungsportal für den Cluster zum Überwachen von SQL Server-2019 big Data-Clustern (Vorschau) verwenden.
author: yualan
ms.author: alayu
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: fbb43d39e28a8b99e49a4dcaf0b2b4f0fc83e670
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582235"
---
# <a name="how-to-use-the-cluster-administration-portal-to-monitor-a-sql-server-big-data-cluster"></a>Wie Sie das Cluster-Verwaltungsportal verwenden, um eine SQL Server-big Data-Cluster zu überwachen

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Wenn Sie überwachen oder Ihre SQL Server-2019 big Data-Cluster (Vorschauversion) behandeln möchten, verwenden Sie das Verwaltungsportal für den Cluster.

Das Cluster-Verwaltungsportal können Sie:
- Zeigen Sie Anzahl von Pods ausgeführt wird und Probleme schnell an
- Überwachen des Bereitstellungsstatus
- Die dienstverfügbarkeit Endpunkte anzeigen
- Ansichtscontroller und SQL Server-Masterinstanz.
- Durchsuchen Sie Informationen zu Pods, einschließlich Zugriff auf Grafana-Dashboards und Kibana-Protokolle

## <a name="access-the-cluster-administration-portal"></a>Zugriff auf das Verwaltungsportal für cluster

Führen Sie die [schnellstartanleitung aus, um Ihre big Data-Cluster bereitstellen](quickstart-big-data-cluster-deploy.md) bis Sie auf die **Cluster Verwaltungsportal** Abschnitt. Nachdem Sie die big Data-Cluster mit Mssqlctl ausgeführt haben, gehen Sie wie folgt vor:

Sobald der Controller-Pod ausgeführt wird, können Sie das Cluster-Verwaltungsportal, zum Überwachen der Bereitstellung. Sie können den Portalzugriff mithilfe der externen IP-Adresse und den Port für die `endpoint-service-proxy` (z. B.: **https://\<Ip-Adresse\>: 30777/Portal**). Anmeldeinformationen für den Zugriff auf die Administratorportal die Werte sind `CONTROLLER_USERNAME` und `CONTROLLER_PASSWORD` oben angegebenen Umgebungsvariablen.

> [!NOTE]
> Für CTP-Version 2.4 besteht eine sicherheitswarnung angezeigt, wenn die Webseite zugreifen, da sie automatisch generierte SSL-Zertifikate verwendet wird.

## <a name="overview"></a>Übersicht

![Übersicht über die](./media/cluster-admin-portal/portal-overview.png)

Wenn Sie zunächst im Portal eingegeben haben, können Sie schnell die Anzahl von Pods auf anzeigen:
- Controller
- Master-Instanz
- Compute-Pool
- Speicherpool
- Datenpool

Wenn Probleme vorliegen, können Sie einen Link zu bekannten Problemen öffnen. Sie können den linken Navigationsbereich verwenden, um an den bestimmten Pool zu wechseln, wenn ein Problem vorliegt.

## <a name="deployment"></a>Bereitstellung

![Bereitstellung](./media/cluster-admin-portal/portal-deployment.png)

Um Ihrer Bereitstellung überwachen möchten, klicken Sie auf der Registerkarte "Bereitstellung" auf der linken Seite. Sie sehen eine Strukturansicht der Bereitstellung, und wenn Probleme, in der Bereitstellung vorliegen.

## <a name="service-endpoints"></a>Dienstendpunkte

![-Endpunkte](./media/cluster-admin-portal/portal-endpoints.png)

Sie können die verfügbaren Dienstendpunkte anzeigen, indem Sie auf der Registerkarte "Endpunkte" auf den linken Navigationsbereich auf.

Dies schließt Links zu Spark-Endgerät, Grafana-Dashboard und Kibana protokolliert.

## <a name="controller"></a>Controller

![Controller](./media/cluster-admin-portal/portal-controller.png)

Der Controller zeigt alle Pods, die im Zusammenhang mit dem Controller an. Weitere Informationen finden Sie Informationen zu den Controller [hier.](concept-controller.md)

Weitere zusätzliche Informationen zu jedem Pod zu finden, klicken Sie auf **Metriken** Spalte zum Anzeigen von Grafana-Dashboards.

Weitere Informationen zu Protokollen für Pods mit Problemen klicken Sie auf die **Protokolle** Spalte.

## <a name="master-instance"></a>Master-Instanz

![-Endpunkte](./media/cluster-admin-portal/portal-master.png)

Die Master-Instanz zeigt alle Pods, die im Zusammenhang mit der SQL Server-Masterinstanz. Weitere Informationen finden Sie Informationen zu den SQL Server-Masterinstanz [hier.](concept-master-instance.md)

Weitere zusätzliche Informationen zu jedem Pod zu finden, klicken Sie auf **Metriken** Spalte zum Anzeigen von Grafana-Dashboards.

Weitere Informationen zu Protokollen für Pods mit Problemen klicken Sie auf die **Protokolle** Spalte.

## <a name="pool-and-pod-pages"></a>Pools und Pod-Seiten

![Pool](./media/cluster-admin-portal/portal-data-pool.png)

Auf jeder Poolauslagerungsseite (Compute, Speicher und Daten), Sie können einen Drilldown zum jede der Pod Seiten durch Klicken auf **Standard**

![Pod](./media/cluster-admin-portal/portal-data-default-pool.png)

Dadurch wird die Breadcrumb am oberen Rand der Drilldown Pfad.

Weitere zusätzliche Informationen zu jedem Pod zu finden, klicken Sie auf **Metriken** Spalte zum Anzeigen von Grafana-Dashboards.

Weitere Informationen zu Protokollen für Pods mit Problemen klicken Sie auf die **Protokolle** Spalte.

Weitere Informationen zu jedem Pool:
- [Compute-pool](concept-compute-pool.md)
- [Speicherpool](concept-storage-pool.md)
- [Datenpool](concept-data-pool.md)

## <a name="about-page"></a>Zu den Seiten

![Informationen zu](./media/cluster-admin-portal/portal-about.png)

Hier sehen Sie Informationen zu Ihrem Cluster wie die unterschiedliche Versionsnummern, Container und einen Link in der Dokumentation.

## <a name="next-steps"></a>Nächste Schritte

Zusätzlich zu dem Cluster-Verwaltungsportal können Sie auch mehrere hilfreiche Kubernetes-Befehle, um den Status und Integrität Ihres Clusters zu untersuchen ausführen. Weitere Informationen finden Sie unter ["kubectl"-Befehle zur Überwachung und Problembehandlung von SQL Server-big Data-Cluster](cluster-troubleshooting-commands.md).

Weitere Informationen zu SQL Server-2019 big Data-Cluster finden Sie unter [was SQL Server-2019 big Data-Cluster sind?](big-data-cluster-overview.md).
