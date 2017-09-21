---
title: AbsolutePosition- und CursorLocation Eigenschaften Beispiel (VB) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- AbsolutePosition property [ADO], Visual Basic example
- CursorLocation property [ADO], Visual Basic example
ms.assetid: c4755799-c60a-4b5e-a01f-b85dd0e0a7f9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f5734ca3a76cf3065e3c0f516418cee5ed210cfa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="absoluteposition-and-cursorlocation-properties-example-vb"></a>AbsolutePosition- und CursorLocation Eigenschaften Beispiel (VB)
In diesem Beispiel wird veranschaulicht, wie die [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) Eigenschaft kann den Fortschritt einer Schleife, die alle Datensätze der listet verfolgen eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Er verwendet die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft zum Aktivieren der **AbsolutePosition** Eigenschaft, indem Sie den Cursor auf einen Clientcursor festgelegt.  
  
```  
'BeginAbsolutePositionVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQL As String  
        'record variables  
    Dim strMessage As String  
  
    'Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open Employee recordset with  
    ' Client-side cursor to enable AbsolutePosition property  
    Set rstEmployees = New ADODB.Recordset  
    strSQL = "employee"  
    rstEmployees.Open strSQL, strCnxn, adUseClient, adLockReadOnly, adCmdTable  
  
    ' Enumerate Recordset  
    Do While Not rstEmployees.EOF  
        ' Display current record information  
        strMessage = "Employee: " & rstEmployees!lname & vbCr & _  
            "(record " & rstEmployees.AbsolutePosition & _  
            " of " & rstEmployees.RecordCount & ")"  
        If MsgBox(strMessage, vbOKCancel) = vbCancel Then Exit Do  
        rstEmployees.MoveNext  
    Loop  
  
    ' clean up  
    rstEmployees.Close  
    Cnxn.Close  
    Set rstEmployees = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
   ' clean up  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndAbsolutePositionVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [AbsolutePosition-Eigenschaft (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [CursorLocation-Eigenschaft (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)