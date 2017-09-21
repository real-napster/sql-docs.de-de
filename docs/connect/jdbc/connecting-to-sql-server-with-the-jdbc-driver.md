---
title: Herstellen einer Verbindung mit SQLServer mit der JDBC-Treiber | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ebc9542e5683eb58c198745892916893f284822
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>Verbinden von SQL Server mit dem JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Eine der grundlegenden Aufgaben, die mit der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] , besteht darin, eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Alle Interaktionen mit der Datenbank erfolgt über die [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) -Objekt, da der JDBC-Treiber eine extrem flache Architektur aufweist, nahezu alle wesentlichen Verhalten beziehen sich auf das SQLServerConnection-Objekt.  
  
 Wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ist nur ein IPv6-Port überwacht, legen Sie die java.net.preferIPv6Addresses-System-Eigenschaft, stellen Sie sicher, dass IPv6 statt IPv4 verwendet wird, für die Verbindung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
```  
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 Die Themen in diesem Abschnitt wird beschrieben, wie herstellen und verwalten eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Erstellen der Verbindungs-URL](../../connect/jdbc/building-the-connection-url.md)|Beschreibt, wie Sie eine Verbindungs-URL zu bilden, für die Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Beschreibt außerdem, Herstellen einer Verbindung zu benannten Instanzen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.|  
|[Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md)|Beschreibt die verschiedenen Verbindungseigenschaften und wie sie verwendet werden können, bei der Herstellung einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.|  
|[Festlegen der Datenquelleneigenschaften](../../connect/jdbc/setting-the-data-source-properties.md)|Beschreibt die Verwendung von Datenquellen auf einer Java-Plattform, Enterprise Edition (Java EE).|  
|[Arbeiten mit einer Verbindung](../../connect/jdbc/working-with-a-connection.md)|Beschreibt die verschiedenen Möglichkeiten zum Erstellen einer Instanz einer Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.|  
|[Verbindungspooling](../../connect/jdbc/using-connection-pooling.md)|Beschreibt die Unterstützung von Verbindungspools durch den JDBC-Treiber.|  
|[Verwenden der Datenbankspiegelung &#40; JDBC &#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|Beschreibt die Unterstützung der Datenbankspiegelung durch den JDBC-Treiber.|  
|[JDBC Driver-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|Beschreibt das Entwickeln einer Anwendung, die eine Verbindung mit einer AlwaysOn-Verfügbarkeitsgruppe herstellt.|  
|[Verwenden integrierte Kerberos-Authentifizierung zum Verbinden mit SQLServer](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|Erläutert eine Java-Implementierung für Anwendungen für die Verbindung eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe der integrierten Kerberos-Authentifizierung.|  
|[Herstellen einer Verbindung mit einer Azure SQL-Datenbank](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|Erläutert Verbindungsprobleme für Datenbanken in SQL Azure.|  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  