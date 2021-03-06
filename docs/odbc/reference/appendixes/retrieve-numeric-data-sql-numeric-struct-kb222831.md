---
title: Abrufen von numerischen Daten mit SQL_NUMERIC_STRUCT | Microsoft-Dokumentation
description: C /C++ mithilfe von ODBC mit SQL_NUMERIC_STRUCT, die im Zusammenhang mit SQL_C_NUMERIC ruft der numerische Datentyp für die SQL Server ab.
editor: ''
ms.prod: sql
ms.technology: ''
ms.devlang: cpp
ms.topic: conceptual
ms.custom: ''
ms.date: 07/13/2017
ms.author: genemi
authors: MightyPen
manager: craigg
ms.openlocfilehash: 256a8f87445dd7bcc581e1bc0e5d55e9b5700ffb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629517"
---
# <a name="retrieve-numeric-data-with-sqlnumericstruct"></a>Abrufen von numerischen Daten mit SQL\_numerischen\_Struktur

In diesem Artikel wird beschrieben, wie numerische Daten aus dem SQL Server-ODBC-Treiber in einer numerischen Struktur abgerufen wird. Es wird beschrieben, wie die richtigen Werte, die mit bestimmten Genauigkeit zu erhalten, und Skalieren die Werte.

Dieser Datentyp ist die Anwendung, numerische Daten direkt zu behandeln. Um das Jahr 2003 eingeführt ODBC 3.0 einen neuen ODBC-C-Datentyp, identifizierte **SQL\_C\_numerischen**. Dieser Datentyp ist seit 2017 weiterhin relevant.

Der C-Puffer, der verwendet wird, ist die Definition des Typs **SQL\_numerischen\_Struktur**. Diese Struktur hat Feldern zum Speichern von der Genauigkeit, Dezimalstellen, Anmeldung und Wert der numerischen Daten. Der Wert selbst wird als eine skalierte ganze Zahl, mit dem niedrigstwertigen Byte Anfang der am weitesten links stehende Position gespeichert. 

Der Artikel [C-Datentypen](c-data-types.md) enthält weitere Informationen über das Format und die Verwendung von SQL\_numerischen\_Struktur. In der Regel die [Anhang D](appendix-d-data-types.md) erläutert, der der ODBC 3.0 Programmer's Reference-Datentypen.


## <a name="sqlnumericstruct-overview"></a>SQL\_numerischen\_Übersicht über die Struktur


Die SQL-Anweisung\_numerischen\_Struktur ist in der Headerdatei sqltypes.h wie folgt definiert:


``` C
#define SQL_MAX_NUMERIC_LEN    16
typedef struct tagSQL_NUMERIC_STRUCT
{
   SQLCHAR    precision;
   SQLSCHAR   scale;
   SQLCHAR    sign;   /* 1 if positive, 0 if negative */
   SQLCHAR    val[SQL_MAX_NUMERIC_LEN];
} SQL_NUMERIC_STRUCT;
```

            
Die Felder für Genauigkeit und Dezimalstellenanzahl der numerischen Struktur werden für die Eingabe aus einer Anwendung nur für die Ausgabe aus dem Treiber für die Anwendung nie verwendet.

Der Treiber verwendet die standardmäßige Genauigkeit von (treiberdefinierten) und den Standardwert (0), wenn Daten an die Anwendung zurückgibt. Wenn die Anwendung die Werte für Genauigkeit und Dezimalstellen angibt, wird der Treiber geht die und verkürzt die Nachkommastellen der numerischen Daten.

## <a name="sqlnumericstruct-code-sample"></a>SQL\_numerischen\_STRUCT-Codebeispiel

In diesem Codebeispiel wird veranschaulicht:

- Legt die Genauigkeit fest.
- Die Skalierungsgruppe.
- Rufen Sie die korrekten Werte. 

> [!Note]
> DIE NUTZUNG DURCH SIE ÜBER DEN CODE IN DIESEM ARTIKEL IST AUF EIGENE GEFAHR. 
>
> Microsoft bietet diese Codebeispiele "wie besehen" ohne Gewährleistung jeglicher Art, ausdrücklich oder konkludent, einschließlich, aber nicht beschränkt auf konkludente Garantien der Marktgängigkeit und/oder der Eignung für einen bestimmten Zweck.

``` C
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <stdlib.h>
#include <ctype.h>
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

#define MAXDSN       25
#define MAXUID       25
#define MAXAUTHSTR   25
#define MAXBUFLEN   255

SQLHENV     henv   = SQL_NULL_HENV;
SQLHDBC     hdbc1  = SQL_NULL_HDBC;     
SQLHSTMT    hstmt1 = SQL_NULL_HSTMT;
SQLHDESC    hdesc  = NULL;


SQL_NUMERIC_STRUCT NumStr;

int main()
{
   RETCODE retcode;

//Change the values below as appropriate to make a successful connection.
//szDSN: DataSourceName, szUID=userid, szAuthStr: password

UCHAR szDSN[MAXDSN+1] = "sql33",szUID[MAXUID+1]="sa", szAuthStr[MAXAUTHSTR+1] = "";
SQLINTEGER strlen1;
SQLINTEGER a;
int i,sign =1;
long myvalue, divisor;
float final_val;
   
// Allocate the Environment handle. Set the Env attribute, allocate the
//connection handle, connect to the database and allocate the statement //handle.

retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);
retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION,(SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);
retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);
retcode = SQLConnect(hdbc1, szDSN,SQL_NTS,szUID,SQL_NTS,szAuthStr,SQL_NTS);
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);

// Execute the select statement. Here it is assumed that numeric_test
//table is created using the following statements:

// Create table numeric_test (col1 numeric(5,3))
//insert into numeric_test values (25.212)

retcode = SQLExecDirect(hstmt1,(UCHAR *)"select * from numeric_test",SQL_NTS);

// Use SQLBindCol to bind the NumStr to the column that is being retrieved.

retcode = SQLBindCol(hstmt1,1,SQL_C_NUMERIC,&NumStr,19,&strlen1);

// Get the application row descriptor for the statement handle using
//SQLGetStmtAttr.

retcode = SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_ROW_DESC,&hdesc, 0, NULL);

// You can either use SQLSetDescRec or SQLSetDescField when using
// SQLBindCol. However, if you prefer to call SQLGetData, you have to
// call SQLSetDescField instead of SQLSetDescRec. For more information on
// descriptors, please refer to the ODBC 3.0 Programmers reference or
// your Online documentation.

//Used when using SQLSetDescRec
//a=b=sizeof(NumStr);

// Set the datatype, precision and scale fields of the descriptor for the 
//numeric column. Otherwise the default precision (driver defined) and 
//scale (0) are returned.

// In this case, the table contains only one column, hence the second 
//parameter contains one. Zero applies to bookmark columns. Please check 
//the programmers guide for more information.

//retcode=SQLSetDescRec(hdesc,1,SQL_NUMERIC,NULL,sizeof(NumStr),5,3,&NumStr,&a,&b);

retcode = SQLSetDescField (hdesc,1,SQL_DESC_TYPE,(VOID*)SQL_C_NUMERIC,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_PRECISION,(VOID*) 5,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_SCALE,(VOID*) 3,0);
    
// Initialize the val array in the numeric structure.

memset(NumStr.val,0,16);
   
// Call SQLFetch to fetch the first record.

while((retcode =SQLFetch(hstmt1)) != SQL_NO_DATA)
  {
// Notice that the TargetType (3rd Parameter) is SQL_ARD_TYPE, which  
//forces the driver to use the Application Row Descriptor with the 
//specified scale and precision.

   retcode = SQLGetData(hstmt1, 1, SQL_ARD_TYPE, &NumStr, 19, &a); 

// Check for null indicator.

   if ( SQL_NULL_DATA == a )
   {
   printf( "The final value: NULL\n" );
   continue;
   }

// Call to convert the little endian mode data into numeric data.

   myvalue = strtohextoval();

// The returned value in the above code is scaled to the value specified
//in the scale field of the numeric structure. For example 25.212 would
//be returned as 25212. The scale in this case is 3 hence the integer 
//value needs to be divided by 1000.

   divisor = 1;
   if(NumStr.scale > 0)
     {
    for (i=0;i< NumStr.scale; i++)   
         divisor = divisor * 10;
     }
   final_val =  (float) myvalue /(float) divisor;

// Examine the sign value returned in the sign field for the numeric
//structure.
//NOTE: The ODBC 3.0 spec required drivers to return the sign as 
//1 for positive numbers and 2 for negative number. This was changed in the
//ODBC 3.5 spec to return 0 for negative instead of 2.

      if(!NumStr.sign) sign = -1;
      else sign  =1;

   final_val *= sign;
   printf("The final value: %f\n",final_val);
    }

   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA_FOUND);

   /* clean up */ 
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);
   SQLDisconnect(hdbc1);
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
   return(0);
}
```


### <a name="interim-results"></a>Zwischenergebnisse:


```
//  C  ==> 12 * 1    =     12
//  7  ==> 07 * 16   =    112
//  2  ==> 02 * 256  =    512
//  6  ==> 06 * 4096 =  24576
===============================
                 Sum =  25212
```


In der numerischen Struktur ist das Val-Feld ein Array von Zeichen von 16 Elementen. Beispielsweise 25.212 auf 25212 skaliert, und die Skalierung ist 3. Im Hexadezimalformat angegeben wäre diese Zahl 627 C.

Der Treiber gibt Folgendes zurück:

- Das entsprechende Zeichen vom 7C, handelt es sich "|" (über die Pipeline) in das erste Element des Zeichenarrays.
- Die Entsprechung der 62, "b" in das zweite Element handelt.
- Die Reste der Arrayelemente enthalten Nullen (0), damit der Puffer enthält "| b\0".

Jetzt ist die Herausforderung der skalierte Ganzzahl aus diesem Zeichenfolgenarray zu erstellen. Jedes Zeichen in der Zeichenfolge entspricht zwei hexadezimale Ziffern, z. B. am wenigsten signifikanten Ziffern (LSD) und die signifikanteste Ziffer (MSD). Die skalierte Ganzzahl-Wert konnte durch Multiplikation der einzelnen Ziffern (LSD & MSD) generiert werden, mit der ein Vielfaches von 16, beginnend mit 1.

Code, der die Konvertierung von little-endian-Modus in die skalierte Ganzzahl implementiert. Es ist, muss der Anwendungsentwickler, um diese Funktionalität zu implementieren. Im folgenden Codebeispiel wird nur eine von den vielen Möglichkeiten.


``` C
long strtohextoval()
{
    long val=0,value=0;
    int i=1,last=1,current;
    int a=0,b=0;

        for(i=0;i<=15;i++)
        {
         current = (int) NumStr.val[i];
         a= current % 16; //Obtain LSD
         b= current / 16; //Obtain MSD
            
         value += last* a;   
         last = last * 16;   
         value += last* b;
         last = last * 16;   
        }
     return value;
}
```


### <a name="applies-to-versions"></a>Gilt für Versionen


Die vorherigen Informationen zu SQL\_numerischen\_Struktur angewendet wird, um die folgenden Versionen:

- Microsoft ODBC-Treiber für Microsoft SQL Server 3.7
- Microsoft Data Access Components 2.1
- Microsoft Data Access Components 2.5
- Microsoft Data Access Components 2.6
- Microsoft Data Access Components 2.7


## <a name="sqlcnumeric-overview"></a>SQL\_C\_numerischen-Übersicht


Das folgende Beispielprogramm veranschaulicht die Verwendung von SQL\_C\_numerischen 123,45 in eine Tabelle eingefügt. In der Tabelle ist die Spalte als einen numerischen Wert oder eine Dezimalzahl, die mit einer Genauigkeit von 5, und mit Skalierung 2 definiert.

Der ODBC-Treiber, die, den Sie verwenden, um dieses Programm ausgeführt werden, muss ODBC 3.0-Funktionalität unterstützen.


``` C
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

void main() {

   SQLHENV    henv  = NULL;
   SQLHDBC    hdbc  = NULL;
   SQLHSTMT   hstmt = NULL;

   SQL_NUMERIC_STRUCT   NumStr;
   SQLINTEGER           cbNumStr = sizeof (NumStr);

   SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);

   /* Set the ODBC behavior version. */ 
   SQLSetEnvAttr(henv,
         SQL_ATTR_ODBC_VERSION,
         (SQLPOINTER) SQL_OV_ODBC3,
         SQL_IS_INTEGER);

   SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);

   /* Substitute your own connection information */ 
   SQLConnect(hdbc,
      (SQLCHAR *) "MyDSN", 5,
      (SQLCHAR *) "UserID", 6,
      (SQLCHAR *) "Password", 8);

   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);

   /*
      Set up the SQL_NUMERIC_STRUCT, NumStr, to hold "123.45".

      First, we need to scale 123.45 to an integer: 12345
      One way to switch the bytes is to convert 12345 to Hex:  0x3039
      Since the least significant byte will be stored starting from the
      leftmost byte, "0x3039" will be stored as "0x3930".

      The precision and scale fields are not used for input to the driver,
      only for output from the driver. The precision and scale will be set
      in the application parameter descriptor later.
   */ 

   NumStr.sign = 1;   /* 1 if positive, 2 if negative */ 

   memset (NumStr.val, 0, 16);
   NumStr.val [0] = 0x39;
   NumStr.val [1] = 0x30;

   /* SQLBindParameter needs to be called before SQLSetDescField */ 
   SQLBindParameter(hstmt,
          1,
          SQL_PARAM_INPUT,
          SQL_C_NUMERIC,
          SQL_NUMERIC,
          5,
          2,
          &NumStr,
          0,
          (SQLINTEGER *) &cbNumStr);

   /* Modify the fields in the implicit application parameter descriptor */ 
   SQLHDESC   hdesc = NULL;

   SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);
   SQLSetDescField(hdesc, 1, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_PRECISION, (SQLPOINTER) 5, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_SCALE, (SQLPOINTER) 2, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_DATA_PTR, (SQLPOINTER) &NumStr, 0);

   SQLExecDirect(hstmt,
         (SQLCHAR *) "INSERT INTO table (numeric_column) VALUES (?)",
         SQL_NTS);

   SQLFreeHandle(SQL_HANDLE_STMT, hstmt);

   SQLDisconnect (hdbc);

   SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
}
```


<!--
GeneMi historical notes, 2017/July/12. Per Jason.C

https://go.microsoft.com/fwlink/?LinkId=147596

https://support.microsoft.com/help/222831

https://web.archive.org/web/20140319133434/http:/support.microsoft.com:80/kb/222831

https://web.archive.org/web/20080505073901/http:/support.microsoft.com:80/kb/181254

https://docs.microsoft.com/sql/odbc/reference/appendixes/c-data-types
-->

