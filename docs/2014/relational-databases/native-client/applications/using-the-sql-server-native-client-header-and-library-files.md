---
title: Verwenden der SQL Server Native Client-Header und Bibliotheksdateien | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header files [SQL Server Native Client]
- SQLNCLI, header files
- OLE DB, header files
- library files [SQL Server Native Client]
- SQL Server Native Client, header files
- data access [SQL Server Native Client], header files
- SQL Server Native Client ODBC driver,header files
- data access [SQL Server Native Client], library files
- SQL Server Native Client, library files
- ODBC applications, header files
- SQLNCLI, library files
ms.assetid: 69889a98-7740-4667-aecd-adfc0b37f6f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 800b3e43129bba36db0836f9a58a3ad1e47b40c1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141180"
---
# <a name="using-the-sql-server-native-client-header-and-library-files"></a>Verwenden der SQL Server Native Client-Header- und Bibliotheksdateien
  Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Header- und Bibliotheksdateien werden mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] installiert. Es ist wichtig, beim Entwickeln von Anwendungen alle für die Entwicklung erforderlichen Dateien in die Entwicklungsumgebung zu kopieren. Weitere Informationen zu Installation und weiterverteilung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client finden Sie unter [Installieren von SQL Server Native Client](installing-sql-server-native-client.md).  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Header- und -Bibliotheksdateien werden am folgenden Speicherort installiert:  
  
 *%Program*\Microsoft SQL Server\110\SDK  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei (sqlncli.h) wird verwendet, um Ihren benutzerdefinierten Anwendungen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Datenzugriffsfunktionalitäten hinzuzufügen. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei enthält alle Definitionen, Attribute, Eigenschaften und Schnittstellen, die Sie mit den neuen, in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] eingeführten Funktionen nutzen können.  
  
 Zusätzlich zu der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei steht die Bibliotheksdatei sqlncli11.lib zur Verfügung. Dabei handelt es sich um die Exportbibliothek für die Massenkopierfunktionalität ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Bulk Copy Program (BCP)) für ODBC.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei ist abwärtskompatibel mit den mit Microsoft Data Access Components (MDAC) verwendeten Headerdateien sqloledb.h und odbcss.h, enthält aber weder die CLSIDs für SQLOLEDB (den in MDAC enthaltenen OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) noch die Symbole für die XML-Funktionalität. Letztere wird nicht von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt.  
  
 ODBC-Anwendungen können nicht im selben Programm auf den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Header (sqlncli.h) und odbcss.h verweisen. Auch wenn Sie keines der neuen, in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] eingeführten Funktionen verwenden, ist die Verwendung der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei anstelle der älteren odbcss.h-Datei möglich.  
  
 OLE DB-Anwendungen, die den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter verwenden, brauchen nur auf sqlncli.h zu verweisen. Wenn eine Anwendung MDAC (SQLOLEDB) und den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter verwendet, kann sowohl auf sqloledb.h als auch auf sqlncli.h verwiesen werden, unter der Voraussetzung, dass sqloledb.h zuerst angegeben wird.  
  
## <a name="using-the-sql-server-native-client-header-file"></a>Verwenden der SQL Server Native Client-Headerdatei  
 Zum Verwenden der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei müssen Sie in Ihrem C-/C++-Programmcode eine `include`-Anweisung angeben. In den folgenden Abschnitten wird beschrieben, wie Sie dies sowohl für OLE DB- als auch für ODBC-Anwendungen durchführen können.  
  
> [!NOTE]  
>  Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Header- und Bibliotheksdateien können nur mithilfe von Visual Studio C++ 2002 oder höher kompiliert werden.  
  
### <a name="ole-db"></a>OLE DB  
 Zum Verwenden der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei in einer OLE DB-Anwendung geben Sie den folgenden Programmiercode ein:  
  
```  
#define _SQLNCLI_OLEDB_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  Die erste der oben stehenden Codezeilen sollte weggelassen werden, wenn sowohl die OLE DB- als auch die ODBC-API von der Anwendung verwendet werden. Wenn die Anwendung außerdem eine `include`-Anweisung für sqloledb.h aufweist, sollte die `include`-Anweisung für sqlncli.h nach der Anweisung für sqloledb.h stehen.  
  
 Verwenden Sie für das Erstellen einer Verbindung mit einer Datenquelle über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client die Zeichenfolge "SQLNCLI11" als Anbietername.  
  
### <a name="odbc"></a>ODBC  
 Zum Verwenden der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei in einer ODBC-Anwendung geben Sie den folgenden Programmiercode ein:  
  
```  
#define _SQLNCLI_ODBC_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  Die erste Zeile des oben stehenden Codezeilen sollte weggelassen werden, wenn OLE DB und ODBC-APIs von der Anwendung verwendet werden. Wenn die Anwendung über eine `#include`-Anweisung für odbcss.h verfügt, sollte diese entfernt werden.  
  
 Verwenden Sie für das Erstellen einer Verbindung mit einer Datenquelle über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client die Zeichenfolge "SQL Server Native Client 11.0" als Treibernamen.  
  
## <a name="component-names-and-properties-by-version"></a>Komponentennamen und Eigenschaften nach Version  
  
|Eigenschaft|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 10.0<br /><br /> SQL Server 2008|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]|MDAC|  
|--------------|--------------------------------------------------|-------------------------------------------------------|---------------------------------------------------------------|----------|  
|ODBC-Treibername|SQL Native Client|SQL Server Native Client 10.0|SQL Server Native Client 11.0|SQL Server|  
|ODBC-Headerdateiname|Sqlncli.h|Sqlncli.h|Sqlncli.h|Odbcss.h|  
|ODBC-Treiber-DLL|Sqlncli.dll|Sqlncl10.dll|Sqlncl11.dll|sqlsrv32.dll|  
|ODBC-Bibliotheksdatei für BCP-APIs|Sqlncli.lib|Sqlncli10.lib|Sqlncli11.lib|Odbcbcp.lib|  
|ODBC-DLL für BCP-APIs|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Odbcbcp.dll|  
|OLE DB PROGID|SQLNCLI|SQLNCLI10|SQLNCLI11|SQLOLEDB|  
|OLE DB-Headerdateiname|Sqlncli.h|Sqlncli.h|Sqlncli.h|Sqloledb.h|  
|OLE DB-Anbieter-DLL|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Sqloledb.dll|  
  
 Die Datei sqlncli.h unterstützt mehrere Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client über das Makro SQLNCLI_VER. Standardmäßig legt SQLNCLI_VER die neueste Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fest. Um eine Anwendung zu erstellen, die sqlncli10.dll anstatt sqlncli11.dll verwendet, legen Sie SQLNCLI_VER auf 10 fest.  
  
## <a name="static-linking-and-bcp-functions"></a>Statische Verknüpfung und BCP-Funktionen  
 Wenn eine Anwendung BCP-Funktionen verwendet, muss in der Verbindungszeichenfolge der Treiber mit derselben Version angegeben werden, die mit der für die Anwendungskompilierung verwendeten Headerdatei und Bibliothek ausgeliefert wurde.  
  
 Wenn Sie beispielsweise eine Anwendung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client und der zugeordneten Bibliotheksdatei (sqlncli11.lib) und Headerdatei (sqlncli.h) aus \Programme\Microsoft SQL Server\110\SDK kompilieren, sollten Sie (als Beispiel wird ODBC verwendet) in der Verbindungszeichenfolge unbedingt "DRIVER={SQL Server Native Client 11.0}" angeben.  
  
 Weitere Informationen finden Sie unter Performing [Durchführen von Massenkopiervorgängen](../features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
