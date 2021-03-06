---
title: Clustered-Eigenschaft – Beispiel (VB) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Clustered property [ADOX], Visual Basic example
ms.assetid: 1cd30769-c8af-43e7-be27-12ed0434daa1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6268c1eb31565a781929b235fd72f4c27091476
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701578"
---
# <a name="clustered-property-example-vb"></a>Clustered-Eigenschaft – Beispiel (VB)
Dieses Beispiel zeigt die [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) Eigenschaft eine [Index](../../../ado/reference/adox-api/index-object-adox.md). Beachten Sie, dass Microsoft Jet-Datenbanken nicht gruppierte Indizes, unterstützen und daher in diesem Beispiel zurückgibt **"false"** für die **Clustered** Eigenschaft aller Indizes in der **Northwind** die Datenbank.  
  
```  
' BeginClusteredVB  
Sub Main()  
    On Error GoTo ClusteredXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblLoop As ADOX.Table  
    Dim idxLoop As ADOX.Index  
    Dim strCnn As String  
  
    strCnn = "Provider='SQLOLEDB';Data Source='MySqlServer';Initial Catalog='pubs';" & _  
        "Integrated Security='SSPI';"  
    ' Connect to the catalog.  
    cnn.Open strCnn  
    cat.ActiveConnection = cnn  
  
    ' Enumerate the tables.  
    For Each tblLoop In cat.Tables  
        'Enumerate the indexes.  
        For Each idxLoop In tblLoop.Indexes  
            Debug.Print tblLoop.Name & " " & _  
                idxLoop.Name & " " & idxLoop.Clustered  
        Next idxLoop  
    Next tblLoop  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ClusteredXError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndClusteredVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogobjekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Clustered-Eigenschaft (ADOX)](../../../ado/reference/adox-api/clustered-property-adox.md)   
 [Index-Objekt (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Table-Objekt (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
