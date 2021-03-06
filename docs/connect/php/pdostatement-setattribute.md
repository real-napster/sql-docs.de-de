---
title: 'Pdostatement:: SetAttribute | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ec2ed7275c3580554c385940c5cef134244ae35
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744340"
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Legt einen Attributwert fest. Entweder ein vordefiniertes PDO-Attribut oder ein benutzerdefiniertes Treiberattribut.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>Parameter  
$*attribute:* Eine ganze Zahl, eine der Konstanten PDO::ATTR_* oder PDO::SQLSRV_ATTR_\*. Eine Liste der verfügbaren Attribute finden Sie im Abschnitt „Anmerkungen“.  
  
$*value:* Der (gemischte) Wert, der für den angegebenen $*attribute*-Parameter festgelegt werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
„true“ bei Erfolg, andernfalls „false“.  
  
## <a name="remarks"></a>Remarks  
Die folgende Tabelle enthält die Liste mit den verfügbaren Attributen:  
  
|attribute|Werte|und Beschreibung|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 bis zur Grenze des PHP-Speichers.|Konfiguriert die Größe des Puffers, der das Resultset für einen clientseitigen Cursor enthält.<br /><br />Die Standardeinstellung ist 10.240 KB (10 MB).<br /><br />Weitere Informationen zu clientseitigen Cursorn finden Sie unter [Cursortypen &#40;PDO_SQLSRV-Treiber&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|Ganze Zahl zwischen 0 und 4 (inklusiv)|Gibt an, dass die Anzahl der Dezimalstellen, die beim Formatieren von Money-Werte abgerufen.<br /><br />Eine negative ganze Zahl oder Wert größer als 4 werden ignoriert.<br /><br />Diese Option funktioniert nur, wenn PDO::SQLSRV_ATTR_FORMAT_DECIMALS auf "true" festgelegt ist.<br /><br />Diese Option kann auch auf der Verbindungsebene festgelegt werden. Wenn dies der Fall ist, überschreibt diese Option die Option für benutzerverbindungen auf.<br /><br />Weitere Informationen finden Sie unter [Dezimalzeichenfolgen Formatierung und Währungswerten (PDO_SQLSRV-Treiber)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).|
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8 (Standard)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|Legt die Zeichensatzcodierung fest, die vom Treiber verwendet wird, um mit dem Server zu kommunizieren.|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|true oder false|Gibt an, ob zum Abrufen von Datums- und Uhrzeittypen als [PHP-DateTime](http://php.net/manual/en/class.datetime.php) Objekte. Wenn "false", ist das Standardverhalten, um als Zeichenfolgen zurückzugeben.<br /><br />Diese Option kann auch auf der Verbindungsebene festgelegt werden. Wenn dies der Fall ist, überschreibt diese Option die Option für benutzerverbindungen auf.<br /><br />Weitere Informationen finden Sie unter [Vorgehensweise: Abrufen von Datums- und Uhrzeittypen als PHP "DateTime"-Objekte verwenden den PDO_SQLSRV-Treiber](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true oder false|Verarbeitet die numerischen Abrufe aus Spalten mit numerischen SQL-Typen (Bit, Integer, Smallint, Tinyint, Float oder Real).<br /><br />Wenn Optionsflags für die Verbindung ATTR_STRINGIFY_FETCHES aktiviert ist, ist der Rückgabewert eine Zeichenfolge, selbst wenn SQLSRV_ATTR_FETCHES_NUMERIC_TYPE auf.<br /><br />Wenn der zurückgegebene PDO-Typ in Bindung Spalte PDO_PARAM_INT ist, ist der Rückgabewert aus einer Spalte mit ganzen Zahlen eine ganze Zahl an, auch wenn SQLSRV_ATTR_FETCHES_NUMERIC_TYPE deaktiviert ist.|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|true oder false|Gibt an, ob führende Nullen in decimal Zeichenfolgen, die bei Bedarf hinzugefügt werden soll. Wenn diese Option festgelegt die PDO::SQLSRV_ATTR_DECIMAL_PLACES-Option für die Formatierung von Money-Typen ermöglicht. Wenn "false" zu verlassen, wird das Standardverhalten von zurückgeben genaue Genauigkeit und auslassen, führende Nullen für Werte, die kleiner als 1 verwendet.<br /><br />Diese Option kann auch auf der Verbindungsebene festgelegt werden. Wenn dies der Fall ist, überschreibt diese Option die Option für benutzerverbindungen auf.<br /><br />Weitere Informationen finden Sie unter [Dezimalzeichenfolgen Formatierung und Währungswerten (PDO_SQLSRV-Treiber)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|Legt das Abfragetimeout in Sekunden fest.<br /><br />Standardmäßig wartet der Treiber unbegrenzt auf Ergebnisse. Negative Zahlen sind nicht zulässig.<br /><br />„0“ bedeutet „kein Timeout“.|  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>Weitere Informationen  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
