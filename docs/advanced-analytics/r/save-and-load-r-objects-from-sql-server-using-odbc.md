---
title: Speichern und Laden von R-Objekten aus SQL Server über ODBC - SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1ed82ffe497af6393371486440e618c162406a01
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513046"
---
# <a name="save-and-load-r-objects-from-sql-server-using-odbc"></a>Speichern und Laden von R-Objekten aus SQL Server über ODBC
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server R Services können serialisierte R-Objekte in einer Tabelle speichern und dann die Objekt nach Bedarf aus der Tabelle laden, ohne den R-Code erneut ausführen oder das Modell erneut trainieren zu müssen. Diese Fähigkeit zum Speichern von R-Objekten in einer Datenbank ist entscheidend für Szenarios wie Trainieren und Speichern eines Modells und dann späteres Verwenden für Bewertungen oder Analysen.

Um die Leistung dieses ausschlaggebenden Schritts zu verbessern, enthält das **RevoScaleR** -Paket jetzt neue Serialisierungs- und Deserialisierungsfunktionen, die die Leistung deutlich steigern und das Objekt kompakter speichern. Dieser Artikel beschreibt diese Funktionen und deren Verwendung.

## <a name="overview"></a>Übersicht

Das **RevoScaleR** -Paket enthält jetzt neue Funktionen, mit denen es einfacher ist, R-Objekte in SQL Server zu speichern und die Objekte dann aus der SQL Server-Tabelle zu lesen. Im Allgemeinen alle Funktionsaufrufe verwendet einen einfachen Schlüssel-Wert-Speicher, in dem der Schlüssel der Name des Objekts ist, und der Wert, der dem Schlüssel zugeordnet ist, das Varbinary-R-Objekt, das in oder aus einer Tabelle verschoben werden.

Um R-Objekte in SQL Server direkt aus einer R-Umgebung zu speichern, müssen Sie folgende Aktionen ausführen:

+ Stellt eine Verbindung mit SQL Server mithilfe der *RxOdbcData* -Datenquelle.
+ Rufen Sie die neuen Funktionen über die ODBC-Verbindung
+ Optional können Sie angeben, dass das Objekt nicht serialisiert werden. Wählen Sie dann einen neuen Komprimierungsalgorithmus anstelle des standardkomprimierungsalgorithmus verwendet.

Standardmäßig wird jedes Objekt, das Sie aus R aufrufen, um es in SQL Server zu verschieben, serialisiert und komprimiert. Umgekehrt wird, wenn Sie ein Objekt aus einer SQL Server-Tabelle laden, um es in Ihrem R-Code zu verwenden, das Objekt deserialisiert und dekomprimiert.

## <a name="list-of-new-functions"></a>Liste neuer Funktionen

- `rxWriteObject` schreibt über die ODBC-Datenquelle ein R-Objekt in SQL Server.

- `rxReadObject` liest über eine ODBC-Datenquelle ein R-Objekt aus einer SQL Server-Datenbank.

- `rxDeleteObject` löscht ein R-Objekt aus der SQL Server-Datenbank, die in der ODBC-Datenquelle angegeben ist. Gibt es mehrere Objekte, die durch die Schlüssel/Version-Kombination gekennzeichnet sind, werden alle gelöscht.

- `rxListKeys` listet alle verfügbaren Objekte als Schlüssel-Wert-Paare auf. Dies erleichtert es Ihnen, die Namen und Versionen der R-Objekte zu ermitteln.

Ausführliche Hilfe zur Syntax jeder Funktion finden Sie in der R-Hilfe. Details sind auch in der [revoscaler](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

## <a name="how-to-store-r-objects-in-sql-server-using-odbc"></a>So speichern Sie R-Objekte über ODBC in SQL Server

In diesem Verfahren wird veranschaulicht, wie Sie die neuen Funktionen verwenden können, um ein Modell zu erstellen und dieses in SQL Server zu speichern.

1. Richten Sie die Verbindungszeichenfolge für die SQL Server-Instanz ein.
   ```R
   conStr <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. Erstellen Sie in R ein *rxOdbcData* -Datenquellenobjekt, für das Sie die Verbindungszeichenfolge verwenden.
   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr)
   ```

3. Löschen Sie die Tabelle, wenn sie bereits vorhanden ist und Sie keine alten Versionen der Objekte nachverfolgen möchten.

   ```R
   if(rxSqlServerTableExists(ds@table, ds@connectionString)) {
       rxSqlServerDropTable(ds@table, ds@connectionString)
       }
   ```
   
4. Definieren Sie eine Tabelle, in der binäre Objekten gespeichert werden können.

   ```R
   ddl <- paste(" CREATE TABLE [", ds@table, "] 
      (","  [id] varchar(200) NOT NULL,
       "," [value] varbinary(max),
       "," CONSTRAINT unique_id UNIQUE (id))", 
       sep = "") 
   ```
5. Öffnen Sie die ODBC-Verbindung, um die Tabelle zu erstellen, und schließen Sie die Verbindung, sobald die DDL-Anweisung abgeschlossen ist.

   ```R
    rxOpen(ds, "w") 
    rxExecuteSQLDDL(ds, ddl) 
    rxClose(ds)
    ```
6. Generieren Sie die R-Objekte, die Sie speichern möchten.

   ```R
   infertLogit <- rxLogit(case ~ age + parity + education + spontaneous + induced, 
     data = infert)
   ```
6. Verwenden Sie das zuvor erstellte *RxOdbcData* -Objekt, um das Modell in der Datenbank zu speichern.

   ```R
   rxWriteObject(ds, "logit.model", infertLogit)
   ```

## <a name="how-to-read-r-objects-from-sql-server-using-odbc"></a>So lesen Sie R-Objekte über ODBC aus SQL Server

In diesem Verfahren wird veranschaulicht, wie Sie die neuen Funktionen verwenden können, um ein Modell aus SQL Server zu laden.

1. Richten Sie die Verbindungszeichenfolge für die SQL Server-Instanz ein.

   ```R
   conStr2 <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. Erstellen Sie in R ein *rxOdbcData* -Datenquellenobjekt, für das Sie die Verbindungszeichenfolge verwenden.

   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr2)
   ```
3. Lesen Sie das Modell aus der Tabelle, indem Sie dessen R-Objektnamen angeben.

   ```R
    infertLogit2 <- rxReadObject(ds, "logit.model")
   ```
