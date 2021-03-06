---
title: Verwenden von automatisch generierten Schlüssel | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 55a062c7-45ce-40e3-9a6f-4a0f4da4e2a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d50968acff5370bade29886af8d4a52dff3cf016
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757788"
---
# <a name="using-auto-generated-keys"></a>Verwenden von automatisch generierten Schlüsseln

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt die optionalen JDBC 3.0-APIs für das Abrufen automatisch generierter Zeilen-IDs. Der Hauptwert dieser Funktion besteht darin, eine Möglichkeit zu bieten, IDENTITY-Werte einer Anwendung zur Verfügung zu stellen, die eine Datenbanktabelle aktualisiert, ohne dass eine Abfrage und ein zweiter Roundtrip zum Server notwendig sind.

Da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Pseudospalten für IDs unterstützt, müssen Updates, die das Feature für die automatische Generierung von Schlüsseln verwenden müssen, eine Tabelle verwenden, die eine IDENTITY-Spalte enthält. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lässt nur eine einzelne IDENTITY-Spalte pro Tabelle zu. Das von der [getGeneratedKeys](../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)-Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)-Klasse zurückgegebene Resultset enthält nur eine Spalte namens GENERATED_KEYS. Wenn generierte Schlüssel für eine Tabelle ohne IDENTITY-Spalte angefordert werden, gibt der JDBC-Treiber ein leeres Resultset zurück.

Erstellen Sie als Beispiel die folgende Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]-Beispieldatenbank:

```sql
CREATE TABLE TestTable
   (Col1 int IDENTITY,
    Col2 varchar(50),
    Col3 int);  
```

Im folgenden Beispiel wird eine offene Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]-Beispieldatenbank an die Funktion übergeben und eine SQL-Anweisung erstellt. Anschließend werden die Daten der Tabelle hinzugefügt, die Anweisung wird ausgeführt, und der Wert der IDENTITY-Spalte wird angezeigt.

[!code[JDBC#UsingAutoGeneratedKeys1](../../connect/jdbc/codesnippet/Java/using-auto-generated-keys_1.java)]

## <a name="see-also"></a>Weitere Informationen finden Sie unter

[Verwenden von Anweisungen mit dem JDBC-Treiber](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
