---
title: Python-an-SQL-datentypkonvertierungen – SQL Server-Machine Learning
description: Überprüfen Sie die Daten für implizite und explizite Typ Converstions zwischen Python und SQL Server in Data Science und Machine learning-Lösungen.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6a7cb7e8f93489bb52c1457fbf25bf7206026914
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509647"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Geben Sie datentypzuordnungen zwischen Python und SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python-Lösungen, die auf die Funktion für die Python-Integration in SQL Server-Machine Learning-Dienste ausgeführt werden, finden Sie in der Liste der nicht unterstützten Datentypen und datentypkonvertierungen, die möglicherweise implizit durchgeführt werden, wenn Daten zwischen Python und SQL Server übergeben werden.

## <a name="python-version"></a>Python Version

4.2 für SQL Server 2017 Anaconda-Distribution und Python 3.6.

Ein Teil der RevoScaleR-Funktionen (RxLinMod, RxLogit, RxPredict, RxDTrees, RxBTrees, vielleicht einige andere) wird unter Verwendung von Python-APIs, mit der ein neues Python-Paket bereitgestellt **Revoscalepy**. Sie können dieses Paket verwenden, arbeiten mit Daten, die mithilfe von Pandas-Datenrahmen, XDF-Dateien oder SQL Data-Abfragen.

Weitere Informationen finden Sie unter [Revoscalepy-Modul in SQL Server](ref-py-revoscalepy.md) und [Revoscalepy-Funktionsreferenz](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

Python unterstützt eine begrenzte Anzahl von Datentypen im Vergleich zu SQL Server. Wenn Sie Daten aus SQL Server in Python-Skripts verwenden, können daher Daten implizit in einen kompatiblen Datentyp konvertiert. Allerdings häufig eine exakte Konvertierung nicht automatisch durchgeführt werden, und ein Fehler zurückgegeben.

## <a name="python-and-sql-data-types"></a>Python und SQL-Datentypen

Diese Tabelle enthält die impliziten Konvertierungen, die bereitgestellt werden. Andere Datentypen werden nicht unterstützt.

|SQLtype|Python-Typ|
|-------|-----------|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|

## <a name="see-also"></a>Siehe auch

