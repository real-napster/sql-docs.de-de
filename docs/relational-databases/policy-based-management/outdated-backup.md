---
title: Veraltete Sicherung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 0891c74cb08e30d497c6207596693e855283d5eb
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512355"
---
# <a name="outdated-backup"></a>Obsolete Sicherung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Diese Regel überprüft, ob aktuelle Sicherungen einer Datenbank existieren. Die Planung regelmäßiger Sicherungen ist wichtig, um die Datenbanken vor Datenverlust aufgrund vieler verschiedener Fehler zu schützen. Die geeignete Häufigkeit der Datensicherung hängt vom Wiederherstellungsmodell der Datenbank und von den Unternehmensrichtlinien hinsichtlich potenziellen Datenverlusts ab sowie davon, wie oft die Datenbank aktualisiert wird. Wird die Datenbank häufig aktualisiert, steigt die Gefahr des Datenverlusts zwischen den Sicherungsvorgängen stark an.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Wir empfehlen, dass Sie Sicherungen häufig genug ausführen, um Datenbanken vor Datenverlust zu schützen.  
  
 Sowohl das einfache als auch das vollständige Wiederherstellungsmodell erfordern Datensicherungen. In beiden Wiederherstellungsmodellen können Sie jede vollständige Sicherung mit differenziellen Sicherungen ergänzen, um das Risiko eines Datenverlusts zu verringern.  
  
 Für Datenbanken, die das vollständige Wiederherstellungsmodell verwenden, empfehlen wir häufige Protokollsicherungen. Von einer Produktionsdatenbank mit sehr wichtigen Daten sollten Protokollsicherungen in der Regel alle 1 bis 15 Minuten erstellt werden.  
  
> [!NOTE]  
>  Die empfohlene Methode zur Planung von Sicherungen ist ein Datenbankwartungsplan.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
 [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
 [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
