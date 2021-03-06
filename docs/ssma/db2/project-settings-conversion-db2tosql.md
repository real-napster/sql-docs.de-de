---
title: Projekteinstellungen (Konvertierung) (DB2ToSQL) | Microsoft-Dokumentation
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a446fd4ce116ee19aa8b38d1ae6d8213e35c16e1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2018
ms.locfileid: "52392474"
---
# <a name="project-settings-conversion-db2tosql"></a>Project Settings (Conversion) (DB2ToSQL)
Die Seite die **Projekteinstellungen** Dialogfeld enthält Einstellungen, die anpassen, wie SSMA für DB2-Syntax, um konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Syntax.  
  
Im Bereich für die Konvertierung finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder:  
  
-   Die Einstellungen für alle SSMA-Projekten auf die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden  **Migration Zielversion** Dropdown-Liste, und klicken Sie dann **allgemeine** am unteren Rand der linken Bereich ein, und klicken Sie dann auf **Konvertierung**.  
  
-   Die Einstellungen für das aktuelle Projekt, auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie dann auf **allgemeine** am unteren Rand im linken Bereich, und klicken Sie dann auf **Konvertierung**.  
  
## <a name="conversion-messages"></a>Konvertierung von Nachrichten  
  
### <a name="generate-messages-about-issues-applied"></a>Generieren von Nachrichten zu Problemen, die angewendet  
Gibt an, ob SSMA generiert von informationsmeldungen während der Konvertierung, sie in den Ausgabebereich zeigt und den konvertierten Code hinzugefügt.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Nein  
  
**Vollmodus:** Nein  
  
## <a name="miscellaneous-options"></a>Sonstige Optionen  
  
### <a name="cast-rownum-expressions-as-integers"></a>ROWNUM Umwandlungsausdrücke als ganze Zahlen  
SSMA ROWNUM Ausdrücke konvertiert wird, konvertiert es den Ausdruck in eine TOP-Klausel, gefolgt von dem Ausdruck. Das folgende Beispiel zeigt die ROWNUM in eine DB2 DELETE-Anweisung:  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
Das folgende Beispiel zeigt die resultierende [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
Im oberen Bereich erfordert, dass es sich bei der TOP-Klauseln-Ausdruck auf eine ganze Zahl ausgewertet wird. Wenn die ganze Zahl negativ ist, erzeugt die Anweisung einen Fehler.  
  
-   Bei Auswahl von **Ja**, SSMA wird den Ausdruck als ganze Zahl umgewandelt.  
  
-   Bei Auswahl von **keine**, SSMA werden alle nicht ganzzahlige Ausdrücke als Fehler im konvertierten Code zu markieren.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/Full-Modus:** Nein  
  
**Vollständige Modus:** Ja  
  
### <a name="default-schema-mapping"></a>Standardmäßige Schemazuordnung  
Diese Einstellung gibt an, wie die DB2-Schemas in SQL Server-Schemas zugeordnet werden. In dieser Einstellung stehen zwei Optionen zur Auswahl:  
  
1.  **Schema in Datenbank:** In diesem Modus DB2-Schema wird standardmäßig "Dbo" SQL Server-Datenbankschemas in SQL Server-Datenbank'sch1' "sch1" zugeordnet.  
  
2.  **Schema zum Schema:** Schema "sch1" wird In diesem Modus DB2 standardmäßig auf "sch1" SQL Server-Datenbankschemas in SQL Server-Standarddatenbank bereitgestellt, die im Verbindungsdialogfeld zugeordnet werden.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Schema für die Datenbank  
  
### <a name="conversion-ways-of-merge-statement"></a>Möglichkeiten der Konvertierung des MERGE-Anweisung  
  
-   Bei Auswahl von **mithilfe von INSERT, UPDATE, DELETE-Anweisung**, SSMA konvertiert Fusion-Anweisung in INSERT-, Update- und Löschen von Anweisungen.  
  
-   Bei Auswahl von **Verwenden von MERGE-Anweisung**, SSMA konvertiert Fusion-Anweisung in der MERGE-Anweisung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!WARNING]  
> Dieses Projekt Festlegen der Option steht nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Verwenden von MERGE-Anweisung  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>Konvertieren Sie Aufrufe von Unterprogramme, mit denen Standardargumente  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Funktionen unterstützen nicht die Auslassung der Parameter im Funktionsaufruf. Darüber hinaus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Funktionen und Prozeduren unterstützen keine Ausdrücke als Parameter Standardwerte.  
  
-   Bei Auswahl von **Ja** ein Funktionsaufrufs auslässt, Parameter und SSMA fügt das Schlüsselwort **Standard** in der Funktion und den Aufruf in der richtigen Position. Es wird dann den Aufruf mit einer Warnung markiert.  
  
-   Bei Auswahl von **keine**, SSMA wird die Funktionsaufrufe als Fehler markiert.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-count-function-to-countbig"></a>COUNT-Funktion in COUNT_BIG konvertieren  
Wenn Ihre "COUNT"-Funktion zum Zurückgeben von Werten größer als 2.147.483.647 wahrscheinlich sind, ist 2<sup>31</sup>-1 ist, sollten Sie die Funktionen in COUNT_BIG konvertieren.  
  
-   Bei Auswahl von **Ja**, SSMA konvertiert alle Verwendungen von COUNT, COUNT_BIG.  
  
-   Bei Auswahl von **keine**, als die Anzahl ist die Funktionen bleiben. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gibt einen Fehler zurück, wenn die Funktion einen Wert größer als 2 zurückgibt<sup>31</sup>-1.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/Full-Modus:** Ja  
  
**Vollständige Modus:** Nein  
  
### <a name="convert-forall-statement-to-while-statement"></a>FORALL-Anweisung in WHILE konvertieren Anweisung  
Definiert, wie SSMA FORALL-Schleifen für die Auflistungselemente PL/SQL behandelt wird.  
  
-   Bei Auswahl von **Ja**, SSMA erstellt eine WHILE-Schleife, in denen Auflistungselemente nacheinander abgerufen werden.  
  
-   Bei Auswahl von **keine**, SSMA ein Rowset mithilfe von Knoten ()-Methode aus der Auflistung generiert und als eine einzelne Tabelle verwendet. Dies ist effizienter, aber dadurch wird der Ausgabecode weniger lesbar.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Nein  
  
**Vollmodus:** Ja  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>Konvertieren von foreign key mit SET NULL referenziellen Aktion, für die Spalte, die NULL nicht  
DB2 ermöglicht das Erstellen von foreign Key-Einschränkungen, in denen konnte eine SET NULL-Aktion nicht möglicherweise ausgeführt werden, da NULL-Werte nicht in der referenzierten Spalte zulässig sind. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lässt keine solche foreign Key-Konfiguration.  
  
-   Bei Auswahl von **Ja**, SSMA referenzielle Aktionen, die in DB2 generiert, aber Sie manuelle Änderungen vornehmen, vor dem Laden der Einschränkung müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sie können z. B. keine Aktion statt NULL festgelegt.  
  
-   Bei Auswahl von **keine**, die Einschränkung wird als Fehler gekennzeichnet werden.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Nein  
  
### <a name="convert-function-calls-to-procedure-calls"></a>Konvertieren Sie Funktionsaufrufe Prozeduren  
Einige DB2-Funktionen als autonome Transaktionen definiert sind, oder Anweisungen enthalten, die nicht in gültig wäre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In diesen Fällen erstellt SSMA an eine Prozedur und eine Funktion, die als Wrapper für die Prozedur verwendet wird. Die konvertierte-Funktion ruft die implementierende Prozedur.  
  
SSMA kann Aufrufe von der Wrapperfunktion in Aufrufe an die Prozedur konvertieren. Erstellt die Lesbarkeit des Codes, und kann die Leistung verbessern. Allerdings ist der Kontext immer es können keine; Sie können keine z. B. einen Funktionsaufruf im SELECT-Liste mit einem Prozeduraufruf ersetzen. SSMA verfügt über einige Optionen für die allgemeine Fälle abdecken:  
  
-   Bei Auswahl von **immer**, SSMA versucht wird, ruft der Wrapper-Funktion in Prozeduraufrufen zu konvertieren. Wenn diese Konvertierung durch der aktuelle Kontext nicht möglich ist, wird eine Fehlermeldung erstellt. Auf diese Weise werden keine Funktionsaufrufe im generierten Code beibehalten.  
  
-   Bei Auswahl von **möglichst**, SSMA stellt eine Verschiebung Prozeduraufrufe nur dann, wenn die Funktion Ausgabeparameter besitzt. Wenn das Verschieben nicht möglich ist, wird die Output-Attributs des Parameters entfernt. In allen anderen Fällen bleibt SSMA Funktionsaufrufe.  
  
-   Bei Auswahl von **nie**, SSMA hinterlässt alle Funktionsaufrufe als Funktionsaufrufe. Diese Option kann in einigen Fällen aus Gründen der Leistung nicht akzeptabel sein.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Wenn möglich  
  
### <a name="convert-lock-table-statements"></a>LOCK-TABLE-Anweisungen konvertieren  
SSMA kann viele SPERREN TABLE-Anweisungen in Tabellenhinweise konvertieren. SSMA kann nicht konvertiert werden alle SPERREN TABLE-Anweisungen, die PARTITION, SUBPARTITION, enthalten @dblink, und NOWAIT-Klauseln, und kennzeichnet diese Anweisungen mit Fehlermeldungen für die Konvertierung.  
  
-   Bei Auswahl von **Ja**, SSMA konvertiert unterstützten SPERRE TABLE-Anweisungen in Tabellenhinweise.  
  
-   Bei Auswahl von **keine**, SSMA werden alle SPERREN TABLE-Anweisungen mit Fehlermeldungen für die Konvertierung zu markieren.  
  
Die folgende Tabelle zeigt, wie SSMA für DB2-Sperrmodi konvertiert:  
  
|||  
|-|-|  
|DB2-Sperrmodus|SQL Server-Tabellenhinweis|  
|FREIGABE DER ZEILE|ROWLOCK, HOLDLOCK|  
|EXKLUSIVE ZEILE|ROWLOCK, XLOCK, HOLDLOCK|  
|FREIGABE UPDATE = ZEILE FREIGABE|ROWLOCK, HOLDLOCK|  
|FREIGEBEN|TABLOCK, HOLDLOCK|  
|FREIGABE-ZEILE, DIE EXKLUSIVE|TABLOCK, XLOCK, HOLDLOCK|  
|EXKLUSIVE|TABLOCKX, HOLDLOCK|  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>Konvertieren von OPEN-FOR-Anweisungen für den REF CURSOR-OUT-Parameter  
In DB2 kann OPEN-FOR-Anweisung verwendet werden, um ein Resultset an den OUT-Parameter vom Typ REF CURSOR ein Unterprogramm zurückzugeben. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gespeicherte Prozeduren direkt zurückgeben, die Ergebnisse der SELECT-Anweisungen.  
  
SSMA kann viele OPEN-FOR-Anweisungen in SELECT-Anweisungen konvertieren.  
  
-   Bei Auswahl von **Ja**, SSMA konvertiert OPEN-FOR-Anweisung in einer SELECT-Anweisung, die das Resultset an den Client zurückgibt.  
  
-   Bei Auswahl von **keine**, SSMA wird eine Fehlermeldung generiert, in der konvertierten Code und dem Ausgabebereich angezeigt.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>Konvertieren von Datensatz als eine Liste von trennt-Variablen  
SSMA kann DB2-Datensätze in trennt Variablen und in XML-Variablen mit bestimmten Struktur konvertieren.  
  
-   Bei Auswahl von **Ja**, SSMA konvertiert den Datensatz in einer Liste von Variablen trennt, wenn möglich.  
  
-   Bei Auswahl von **keine**, SSMA des Datensatzes in XML-Variablen mit bestimmten Struktur konvertiert.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>SUBSTR-Funktionsaufrufe von SUBSTRING-Funktionsaufrufe konvertieren  
SSMA kann DB2 SUBSTR-Funktionsaufrufe in konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Teilzeichenfolge** Funktionsaufrufe, abhängig von der Anzahl von Parametern. Wenn SSMA einen SUBSTR-Funktionsaufruf kann nicht konvertiert werden, oder die Anzahl der Parameter wird nicht unterstützt, werden die SSMA SUBSTR-Funktionsaufruf in einem benutzerdefinierten SSMA-Funktionsaufruf konvertiert.  
  
-   Bei Auswahl von **Ja**, SSMA konvertiert SUBSTR-Funktionsaufrufe, die drei Parameter in verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Teilzeichenfolge**. Andere SUBSTR-Funktionen werden zum Aufrufen der benutzerdefinierten SSMA-Funktion konvertiert werden.  
  
-   Bei Auswahl von **keine**, SSMA konvertiert die SUBSTR-Funktionsaufruf in einem benutzerdefinierten SSMA-Funktionsaufruf.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Ja  
  
**Vollmodus:** Nein  
  
### <a name="convert-subtypes"></a>Konvertieren von Untertypen  
SSMA kann PL/SQL-Untertypen auf zwei Arten konvertieren:  
  
-   Bei Auswahl von **Ja**, SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den benutzerdefinierten Typ aus einem Untertyp und verwenden sie für jede Variable dieses Untertyps.  
  
-   Bei Auswahl von **keine**, SSMA wird allen Deklarationen in der Quelle für den Untertyp mit dem zugrunde liegenden Typ ersetzen und konvertieren Sie das Ergebnis wie gewohnt. In diesem Fall werden keine zusätzlichen Typen in erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Nein  
  
### <a name="convert-synonyms"></a>Konvertieren von Synonymen  
Synonyme für die folgenden DB2-Objekte können zu migriert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Tabellen und Objekttabellen  
  
-   Ansichten und Objekt-Ansichten  
  
-   Gespeicherte Prozeduren und Funktionen  
  
-   Materialisierte Sichten  
  
Synonyme für die folgenden DB2-Objekte können durch direkte Verweise auf die Objekte ersetzt werden:  
  
-   Sequenzen  
  
-   Pakete  
  
-   Schemaobjekte für Java-Klasse  
  
-   Benutzerdefinierte Objekttypen  
  
Synonyme können nicht migriert werden. SSMA generiert Fehlermeldungen für das Synonym "und" alle Verweise, die das Synonym zu verwenden.  
  
-   Bei Auswahl von **Ja**, SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Synonyme und direkte Objektverweise gemäß den vorherigen Listen.  
  
-   Bei Auswahl von **keine**, SSMA direkte Objektverweise für alle hier aufgeführten Synonyme erstellt.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-tochardate-format"></a>TO_CHAR (Date, Format) konvertieren  
SSMA kann DB2 TO_CHAR(date, format) in Prozeduren aus der Sysdb Datenbank konvertieren.  
  
-   Bei Auswahl von **TO_CHAR_DATE mithilfe von Funktion**, SSMA konvertiert die TO_CHAR ("Datum", "Format") in TO_CHAR_DATE Funktion mithilfe der englischen Sprache für die Konvertierung.  
  
-   Bei Auswahl von **mithilfe TO_CHAR_DATE_LS-Funktion (NLS Care)**, SSMA konvertiert die TO_CHAR ("Datum", "Format") in TO_CHAR_DATE_LS Funktion mithilfe der sitzungssprache für die Konvertierung  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Verwenden von TO_CHAR_DATE-Funktion  
  
**Vollmodus:** Verwenden von TO_CHAR_DATE_LS-Funktion (NLS Care)  
  
### <a name="convert-transaction-processing-statements"></a>Konvertieren des Transaction Processing-Anweisungen  
SSMA kann DB2 Transaction Processing-Anweisungen konvertieren:  
  
-   Bei Auswahl von **Ja**, SSMA konvertiert DB2 Transaction-Anweisungen auf, die sich in Verarbeitung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anweisungen.  
  
-   Bei Auswahl von **keine**, SSMA markiert die Transaktion, die Verarbeitung von Anweisungen als Fehler bei der Konvertierung.  
  
> [!NOTE]  
> DB2 wird implizit Transaktionen geöffnet. Um dieses Verhalten zu emulieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], müssen Sie BEGIN TRANSACTION-Anweisungen manuell hinzufügen, die Transaktionen gestartet werden soll. Alternativ können Sie den Befehl SET IMPLICIT_TRANSACTIONS ON am Anfang der Sitzungs ausführen. SSMA fügt SET IMPLICIT_TRANSACTIONS ON beim Konvertieren von Unterprogrammen mit autonomen Transaktionen automatisch hinzu.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>Emulieren der DB2-null-Verhalten in der ORDER BY-Klauseln  
NULL-Werte werden anders als in sortiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und DB2:  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]NULL Werte sind die niedrigsten Werte in einer geordneten Liste. In der Liste eine aufsteigende werden NULL-Werte angezeigt.  
  
-   In DB2 sind NULL-Werte für den höchsten Werten in einer geordneten Liste. Standardmäßig werden NULL-Werte in einer Liste mit aufsteigender Reihenfolge zuletzt angezeigt.  
  
-   DB2 wurde zum ersten NULL-Werte und NULL-Werte letzten-Klauseln, können Sie ändern, wie DB2 NULL-Werten sortiert.  
  
SSMA kann DB2 ORDER BY-Verhalten emulieren, durch Prüfen auf NULL-Werte. Es ordnet dann zuerst nach NULL-Werte in der angegebenen Reihenfolge, und klicken Sie dann Aufträge durch andere Werte.  
  
-   Bei Auswahl von **Ja**, SSMA wandelt die DB2-Anweisung auf eine Weise, die DB2-ORDER BY-Verhalten emuliert.  
  
-   Bei Auswahl von **keine**, SSMA DB2 Regeln ignoriert und eine Fehlermeldung generiert, wenn die Klauseln NULL-Werte-vor- und NACHNAMEN NULL-Werte gefunden.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Nein  
  
**Vollmodus:** Ja  
  
### <a name="emulate-row-count-exceptions-in-select"></a>Emulieren Sie die Zeile Anzahl von Ausnahmen in SELECT  
Wenn die SELECT-Anweisung eine INTO-Klausel keine Zeilen zurückgibt, löst DB2 eine NO_DATA_FOUND-Ausnahme aus. Wenn die Anweisung zwei oder mehr Zeilen zurückgibt, wird die TOO_MANY_ROWS-Ausnahme ausgelöst. Die konvertierte-Anweisung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] löst keine Ausnahmen aus, ist die Anzahl der Zeilen aus einer anderen.  
  
-   Bei Auswahl von **Ja**, SSMA fügt Aufruf Sysdb Prozedur Db_error_exact_one_row_check nach jede SELECT-Anweisung. Dieses Verfahren wird die Ausnahmen NO_DATA_FOUND und TOO_MANY_ROWS emuliert. Dies ist die Standardeinstellung, und ermöglicht DB2-Verhalten so nah wie möglich zu reproduzieren. Sie sollten immer auswählen **Ja** Wenn Quellcode Ausnahmehandler verfügt, die diese Fehler zu verarbeiten. Beachten Sie, dass im Falle die SELECT-Anweisung innerhalb einer benutzerdefinierten Funktion dieses Moduls an eine gespeicherte Prozedur, konvertiert werden, wird Da gespeicherte Prozeduren ausführen und Auslösen von Ausnahmen ist nicht kompatibel mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Funktionskontext.  
  
-   Bei Auswahl von **keine**, keine Ausnahmen generiert werden. Das kann nützlich sein, wenn SSMA ein User-defined Function konvertiert, und Sie eine Funktion in bleiben möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="generate-error-for-dbmssqlparse"></a>Fehler für DBMS_SQL generiert. ANALYSIEREN  
  
-   Bei Auswahl von **Fehler**, SSMA Fehler bei der Konvertierung DBMS_SQL zu generieren. ANALYSIERT WERDEN.  
  
-   Bei Auswahl von **Warnung**, SSMA generiert die Warnung auf die Konvertierung DBMS_SQL. ANALYSIERT WERDEN.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Fehler  
  
### <a name="generate-rowid-column"></a>ROWID-Spalte generieren  
Wenn SSMA erstellt Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können sie eine ROWID-Spalte erstellen. Wenn Daten migriert werden, ruft jede Zeile einen neuen UNIQUEIDENTIFIER-Wert, die von der NEWID()-Funktion generiert.  
  
-   Bei Auswahl von **Ja**, die ROWID-Spalte wird für alle Tabellen erstellt und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] GUIDs generiert, wie Sie Werte einfügen. Wählen Sie stets **Ja** Wenn Sie beabsichtigen, mit der SSMA-Tester.  
  
-   Bei Auswahl von **keine**, ROWID-Spalten werden nicht in Tabellen eingefügt.  
  
-   **Fügen Sie die ROWID für Tabellen mit Triggern** ROWID für die Tabellen mit den Trigger hinzufügen.  
  
> [!WARNING]  
> Ist diese Einstellung im Fall von SQL Server 2005, SQL Server 2008 und SQL Server 2012 und 2014 **hinzufügen ROWID für Tabellen mit Triggern**.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Fügen Sie die ROWID für Tabellen mit Triggern  
  
**Vollmodus:** Ja  
  
### <a name="generate-unique-index-on-rowid-column"></a>Generieren von eindeutigen Index für die ROWID-Spalte  
Gibt an, ob es sich bei SSMA eindeutigen Index-Spalte in der Spalte ROWID generiert oder nicht generiert. Eindeutige Index wird generiert, wenn die Option auf "Ja" festgelegt ist, und wenn sie auf "Nein" festgelegt ist, wird eindeutiger Index nicht für die Spalte ROWID generiert.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="local-modules-conversion"></a>Lokale Module-Konvertierung  
Definiert den Typ der Konvertierung von DB2 geschachtelte Unterprogramm (deklariert in eigenständige gespeicherte Prozedur oder Funktion).  
  
-   Bei Auswahl von **Inline**, die geschachtelte Unterprogramm Aufrufe durch Text ersetzt werden.  
  
-   Bei Auswahl von **gespeicherte Prozeduren**, geschachtelte Unterprogramm wird in einer gespeicherten SQL Server-Prozedur konvertiert und die Aufrufe auf diesen Aufruf einer Prozedur ersetzt werden.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Inline  
  
### <a name="use-isnull-in-string-concatenation"></a>Verwenden von ISNULL in Verketten von Zeichenfolgen  
DB2 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterschiedliche Ergebnisse zurückgeben, wenn zeichenfolgenverkettungen NULL-Werte enthalten. DB2 behandelt, den NULL-Wert, z. B. einen leeren Zeichensatz. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gibt NULL zurück.  
  
-   Bei Auswahl von **Ja**, SSMA ersetzt die DB2-Verkettung Strich (|), durch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verkettung-Zeichen (+). SSMA überprüft auch die Ausdrücke auf beiden Seiten der Verkettung für NULL-Werte.  
  
-   Bei Auswahl von **keine**, SSMA ersetzt die Verkettung Zeichen, aber nicht für NULL-Werte.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
### <a name="use-isnull-in-replace-function-calls"></a>Verwenden von ISNULL in Funktionsaufrufen ersetzen  
ISNULL-Anweisung wird in ersetzen Funktionsaufrufen verwendet, um DB2-Verhalten zu emulieren. Die folgenden Optionen sind für diese Einstellung vorhanden:  
  
-   YES  
  
-   Nein  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Nein  
  
**Vollmodus:** Ja  
  
### <a name="use-isnull-in-concat-function-calls"></a>Verwenden von ISNULL in CONCAT-Funktionsaufrufen  
ISNULL-Anweisung wird in "concat" Funktionsaufrufen verwendet, um DB2-Verhalten zu emulieren. Die folgenden Optionen sind für diese Einstellung vorhanden:  
  
-   YES  
  
-   Nein  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Nein  
  
**Vollmodus:** Ja  
  
### <a name="use-native-convert-function-when-possible"></a>Verwenden von systemeigenen Convert-Funktion, wenn möglich  
  
-   Bei Auswahl von **Ja**, SSMA konvertiert die TO_CHAR ("Datum", "Format") in systemeigene Convert-Funktion, wenn möglich.  
  
-   Bei Auswahl von **keine**, SSMA konvertiert die TO_CHAR ("Datum", "Format") in TO_CHAR_DATE oder TO_CHAR_DATE_LS (die Definition von "konvertieren TO_CHAR(date, format)"-Optionen).  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/vollständigen-Modus:** Ja  
  
**Vollmodus:** Nein  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>Verwenden von SELECT... FÜR XML, die bei der Konvertierung auswählen... INTO für Datensatz-variable  
Gibt an, ob ein XML-Resultset bei der Auswahl in einer Datensatzvariable mit dem generiert werden soll.  
  
-   Bei Auswahl von **Ja**, die SELECT-Anweisung gibt XML zurück.  
  
-   Bei Auswahl von **keine**, die SELECT-Anweisung gibt ein Resultset zurück.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Nein  
  
## <a name="returning-clause-conversion"></a>Zurückgeben der Klausel-Konvertierung  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>Konvertieren Sie RETURNING-Klausel in DELETE-Anweisung in der Ausgabe  
DB2 bietet eine RETURNING-Klausel als eine Möglichkeit, sofort gelöscht. Werte zu erhalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet diese Funktion mit der OUTPUT-Klausel an.  
  
-   Bei Auswahl von **Ja**, SSMA RETURNING-Klauseln in DELETE-Anweisungen in der OUTPUT-Klauseln konvertiert. Da Trigger für eine Tabelle mit Werten ändern können, der zurückgegebene Wert möglicherweise anders [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als DB2 vorlag.  
  
-   Bei Auswahl von **keine**, SSMA generiert eine SELECT-Anweisung vor der DELETE-Anweisungen, die zurückgegebenen Werte abgerufen.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>Konvertieren Sie RETURNING-Klausel in INSERT-Anweisung in der Ausgabe  
DB2 bietet eine RETURNING-Klausel als eine Möglichkeit, sofort eingefügten Werte zu erhalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet diese Funktion mit der OUTPUT-Klausel an.  
  
-   Bei Auswahl von **Ja**, SSMA konvertiert eine RETURNING-Klausel in einer INSERT-Anweisung in der Ausgabe. Da Trigger für eine Tabelle mit Werten ändern können, der zurückgegebene Wert möglicherweise anders [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als DB2 vorlag.  
  
-   Bei Auswahl von **keine**, SSMA emuliert DB2-Funktionen durch Einfügen, und wählen Sie dann Werte aus einer Verweistabelle.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>Konvertieren Sie RETURNING-Klausel in der UPDATE-Anweisung in der Ausgabe  
DB2 bietet eine RETURNING-Klausel als eine Möglichkeit, sofort die aktualisierten Werte zu erhalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet diese Funktion mit der OUTPUT-Klausel an.  
  
-   Bei Auswahl von **Ja**, SSMA RETURNING-Klauseln in der UPDATE-Anweisungen in der OUTPUT-Klauseln konvertiert. Da Trigger für eine Tabelle mit Werten ändern können, der zurückgegebene Wert möglicherweise anders [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als DB2 vorlag.  
  
-   Bei Auswahl von **keine**, SSMA wird SELECT-Anweisungen generieren, nach dem UPDATE-Anweisung für die Rückgabe von Werten abgerufen werden.  
  
Bei Auswahl einer Konvertierungsmodus, in der **Modus** SSMA Feld gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
## <a name="sequence-conversion"></a>Sequenz-Konvertierung  
  
### <a name="convert-sequence-generator"></a>Konvertieren des Sequenz-Generator  
In DB2 können Sie eine Sequenz verwenden, um eindeutige Bezeichner zu generieren.  
  
SSMA kann Sequenzen in Folgendes konvertieren.  
  
-   Verwenden SQL Server-Sequenz-Generator (diese Option ist nur verfügbar, beim Konvertieren in SQL Server 2012 und SQL Server 2014 wird).  
  
-   Verwenden von SSMA-Sequenz-Generator.  
  
-   Verwenden die Identität der Spalte.  
  
Die Standardoption beim Konvertieren in SQL Server 2012 oder SQL Server 2014 ist die Verwendung von SQL Server-Sequenz-Generator. SQL Server 2012 und SQL Server 2014 unterstützt nicht jedoch erhalten aktuelle Sequenzwert (z. B. mit der DB2 Sequenz Currval-Methode). Finden Sie in der SSMA-Teamblog Anleitungen zum Migrieren von DB2 Sequenz Currval-Methode.  
  
SSMA bietet auch eine Option zum Konvertieren von DB2-Sequenz in SSMA-Sequenz-Emulator. Dies ist die Standardoption beim Konvertieren in SQL Server vor 2012  
  
Schließlich können Sie auch Sequenz zugewiesen an eine Spalte in der Tabelle in SQL Server-Identity-Werte konvertieren. Sie müssen angeben, dass die Zuordnung zwischen den Sequenzen aus, um eine Identitätsspalte in DB2 **Tabelle** Registerkarte  
  
### <a name="convert-currval-outside-triggers"></a>Konvertieren von CURRVAL außerhalb von Triggern  
Sichtbar, wenn Sie den Sequenz-Generator konvertiert festgelegt ist, um nur **mit Spalte Identität**. Da DB2 Sequenzen Objekte, die getrennt von Tabellen sind, verwenden zahlreiche Tabellen enthält, die Sequenzen verwenden eines Triggers zu generieren, und fügen Sie einen neuen Sequenzwert. SSMA Kommentare, die sich diese Anweisungen und kennzeichnet diese als Fehler, wenn Sie die Kommentierung Out zu Fehlern führen würde.  
  
-   Bei Auswahl von **Ja**, SSMA kennzeichnet alle Verweise, um außerhalb der Trigger für den konvertierten CURRVAL mit einer Warnung zu sequenzieren.  
  
-   Bei Auswahl von **keine**, SSMA kennzeichnet alle Verweise, um außerhalb der Trigger für den konvertierten CURRVAL mit einem Fehler zu sequenzieren.  
  
## <a name="see-also"></a>Siehe auch  
[Referenz zur Benutzeroberfläche &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
