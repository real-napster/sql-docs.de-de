---
title: GetSearchStringEscape-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getSearchStringEscape
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea0f95d0-0238-4dc8-9f26-7ff9b65f30c3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1008cd0fdec7aa60d9d66c62cfb08ad84ca1cd5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getsearchstringescape-method-sqlserverdatabasemetadata"></a>getSearchStringEscape-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die **Zeichenfolge** , die verwendet werden kann, um die Platzhalterzeichen mit Escapezeichen versehen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getSearchStringEscape()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** der Platzhalterzeichenfolge mit Escapezeichen Zeichenfolge enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetSearchStringEscape-Methode wird von der GetSearchStringEscape-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Diese Methode wird nur für Suchen nach Metadatenmustern verwendet. Gibt "\\". Ein **Zeichenfolge** Suchmuster kann Platzhalter ("%" und "_") mit Escapezeichen versehen und durch Voranstellen eines umgekehrten Schrägstrichs als Literale bereitstellen. Dies bedeutet "\\%", "[%]" und "\\\_", "[\_]".  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  