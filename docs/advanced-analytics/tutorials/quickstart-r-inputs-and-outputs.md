---
title: Schnellstart für das Arbeiten mit Eingaben und Ausgaben in R – SQL Server-Machine Learning
description: Erfahren Sie in dieser schnellstartanleitung für R-Skript in SQL Server, wie Sie ein- und Ausgaben für die gespeicherte Systemprozedur Sp_execute_external_script strukturieren.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4df9e266e16e2cc37ce527c19ba7be483e43d50a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582683"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>Schnellstart: Verarbeiten von Eingaben und Ausgaben, die mithilfe von R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Schnellstart wird gezeigt, wie Eingaben verarbeiten und gibt bei Verwendung von R in SQL Server Machine Learning Services oder R Services aus.

Wenn Sie R-Code in SQL Server ausführen möchten, müssen Sie R-Skript in einer gespeicherten Prozedur umschließen. Sie können eine schreiben oder R-Skript übergeben [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Dieses System gespeicherte Prozedur wird verwendet, um die R-Laufzeit im Kontext von SQL Server zu starten, der Daten an R übergeben wird, verwaltet Sitzungen von Benutzern, sicher, und gibt die Ergebnisse an den Client zurück.

In der Standardeinstellung [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) akzeptiert ein einzelnes Eingabe-Dataset, das Sie in der Regel in Form von einer gültigen SQL-Abfrage zu geben. Andere Arten von Eingaben können als SQL-Variablen übergeben werden.

Die gespeicherte Prozedur gibt einen einzelnen R-Datenrahmen als Ausgabe zurück, aber Sie können auch skalare und Modelle als Variablen ausgeben. Sie können z. B. die Ausgabe eines trainierten Modells als binäre Variable und übergeben, um eine T-SQL INSERT-Anweisung, um das Modell in einer Tabelle zu schreiben. Sie können auch Diagramme (im binären Format) oder skalare generieren (einzelne Werte, z. B. Datum und Uhrzeit, die verstrichene Zeit zum Trainieren des Modells und so weiter).

## <a name="prerequisites"></a>Erforderliche Komponenten

Einen vorherigen schnellstartanleitung [R stellen Sie sicher, die in SQL Server vorhanden ist](quickstart-r-verify.md), enthält Informationen und links für das Einrichten der R-Umgebung, die im Rahmen dieser schnellstartanleitung benötigt.

## <a name="create-the-source-data"></a>Erstellen der Quelldaten

Erstellen Sie eine kleine Tabelle mit Testdaten, indem Sie die folgende T-SQL-Anweisung ausführen:

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)
INSERT INTO RTestData VALUES (1);
INSERT INTO RTestData VALUES (10);
INSERT INTO RTestData VALUES (100);
GO
```

Wenn die Tabelle erstellt wurde, verwenden Sie die folgende Anweisung zum Abfragen der Tabelle:
  
```sql
SELECT * FROM RTestData
```

**Ergebnisse**

![Inhalt der RTestData-Tabelle](./media/select-rtestdata.png)

## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben

Sehen wir uns die standardmäßigen Eingabe- und Variablen von Sp_execute_external_script: `InputDataSet` und `OutputDataSet`.

1. Sie können die Daten aus der Tabelle als Eingabe für das R-Skript abrufen. Führen Sie folgende Anweisung ein. Ruft die Daten aus der Tabelle ab, gibt die Werte mit den Namen der Spalte zurück und macht einen Roundtrip über die R-Laufzeit *NewColName*.

    Die von der Abfrage zurückgegebenen Daten werden an die R-Laufzeit übergeben, die die Daten in SQL-Datenbank als dataframe zurückgibt. Die WITH RESULT SETS-Klausel definiert das Schema der zurückgegeben Datentabelle für SQL-Datenbank.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Ergebnisse**

    ![Ausgabe von R-Skript, das Daten aus einer Tabelle zurückgegeben.](./media/r-output-rtestdata.png)

2. Ändern wir den Namen der Eingabe- oder Variablen. Das obige Skript verwendet die Standardeingabe und eingabevariablennamen _"inputdataset"_ und _"outputdataset"_. Definieren Sie die Eingabedaten _InputDatSet_, Sie verwenden die *@input_data_1* Variable.

    In diesem Skript wurde die Namen der Ausgabe- und der Eingabevariablen für die gespeicherte Prozedur zu geändert *SQL_out* und *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Beachten Sie, dass R Groß-/Kleinschreibung beachtet, sodass die Groß-/Kleinschreibung der Eingabe- und Variablen in `@input_data_1_name` und `@output_data_1_name` müssen übereinstimmen, das im R-Code in `@script`. 

    Nur eine Eingabedataset kann als Parameter übergeben werden, und Sie können nur ein Dataset zurückgeben. Allerdings können Sie andere Datasets innerhalb Ihres R-Codes aufrufen und Ausgaben und andere Typen zusätzlich zum Dataset zurückgeben. Sie können auch das Schlüsselwort OUTPUT zu einem beliebigen Parameter hinzufügen, damit es mit den Ergebnissen zurückgegeben wird. 

    Die `WITH RESULT SETS` -Anweisung definiert das Schema für die Daten, die verwendet wird, in SQL Server. Sie müssen SQL-kompatible Datentypen für jede Spalte angeben, die von r zurückgegeben Sie können die Schemadefinition verwenden, um neue Spaltennamen bereitzustellen zu verwenden, da Sie nicht die Spaltennamen aus dem R-Datenrahmen verwenden müssen.

3. Sie können auch Werte, die mit dem R-Skript generieren, und lassen Sie die Zeichenfolge der Eingabeabfrage in _@input_data_1_ leer.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Ergebnisse**

    ![Ergebnisse der Abfrage mit @script als Eingabe](./media/r-data-generated-output.png)

## <a name="next-steps"></a>Nächste Schritte

Überprüfen Sie einige der Probleme, die auftreten können, wenn das Übergeben von Daten zwischen R und SQL Server, z. B. implizite Konvertierungen und Unterschiede bei tabellarischen Daten zwischen R und SQL.

> [!div class="nextstepaction"]
> [Schnellstart: Behandeln von Datentypen und Objekte](quickstart-r-data-types-and-objects.md)