---
title: Konfigurieren von Parallel Data Warehouse für remotetabellenkopien | Microsoft-Dokumentation
description: Beschreibt das Konfigurieren von Parallel Data Warehouse, um die remotetabellenkopie-Features, die zum Kopieren von Tabellen in SMP-SQL Server-Datenbanken auf nicht zur Appliance gehört Servern verwenden.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fdac0b6ed211e223c3fad7ba15ac79a282c61303
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509522"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>Konfigurieren von Parallel Data Warehouse für remotetabellenkopien
Beschreibt das Konfigurieren von SQL Server PDW, um die remotetabellenkopie-Features, die zum Kopieren von Tabellen in SMP-SQL Server-Datenbanken auf nicht zur Appliance gehört Servern verwenden.  
  
Dieses Thema beschreibt eine Konfigurationsschritte für die Konfiguration von remote-Tabelle kopieren. Eine Liste der alle Konfigurationsschritte, finden Sie unter [Remotetabellenkopie](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Vorbereitungen  
Um SQL Server PDW remotetabellenkopie Verwendung zu konfigurieren, müssen Sie folgende Aktionen ausführen:  
  
-   Haben Sie ein Administratorkonto für Analytics Platform System mit der Möglichkeit, direkt in melden Sie sich die  <strong>*Appliance_domain*-AD01</strong> und  <strong>*Appliance_domain*-AD02</strong> Knoten.  
  
-   Kennen Sie den Hostnamen oder die IP-Name des Zielservers an.  
  
## <a name="HowToPDW"></a>Konfigurieren Sie SQLServer PDW für Remotetabellenkopie an: Aktualisieren von Hostnamen in DNS  
Die **CREATE REMOTE TABLE** remotetabellenkopien, zum-Anweisung gibt den Zielserver mithilfe der IP-Adresse oder der IP-Name des SMP-Windows-Systems. Um die IP-Namen zu verwenden, müssen Sie Einträge für die erfolgreiche namensauflösung der DNS-Server hinzufügen.  
  
Die folgenden Schritte beschreiben, wie Sie den DNS-Server zu aktualisieren.  
  
1.  Melden Sie sich bei dem aktiven Knoten der AD (normalerweise  <strong>*Appliance_domain*-AD01</strong>).  
  
2.  Öffnen Sie den DNS-Manager. Dies befindet sich unter **Verwaltung** in die **starten** Menü.  
  
3.  Verwenden Sie den DNS-Manager, um den Namen der IP-hinzuzufügen.  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Verwenden Sie eine DNS-Weiterleitung nicht zur Appliance gehört DNS-Namen auflösen](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
