---
title: NumericScale y Precision propiedades (VB) | Microsoft Docs
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
- Precision property [ADOX], Visual Basic example
- NumericScale property [ADOX], Visual Basic example
ms.assetid: ea2ec614-34c8-41b7-8ebd-063798bd56b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 671e7f144ff70bedf1556b506ead6c51d05ebd08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952168"
---
# <a name="adox-code-example-numericscale-and-precision-properties-example-vb"></a>Ejemplos de código ADOX: Ejemplo de las propiedades NumericScale y Precision (VB)
Este ejemplo se muestra el [NumericScale](../../../ado/reference/adox-api/numericscale-property-adox.md) y [precisión](../../../ado/reference/adox-api/precision-property-adox.md) propiedades de la [columna](../../../ado/reference/adox-api/column-object-adox.md) objeto. Este código muestra su valor para el **Order Details** tabla de la *Northwind* base de datos.  
  
```  
' BeginNumericScalePrecVB  
Sub Main()  
    On Error GoTo NumericScalePrecXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblOD As ADOX.Table  
    Dim colLoop As ADOX.Column  
  
    ' Connect the catalog.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "data source='Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
  
    ' Retrieve the Order Details table  
    Set tblOD = cat.Tables("Order Details")  
  
    ' Display numeric scale and precision of  
    ' small integer fields.  
    For Each colLoop In tblOD.Columns  
        If colLoop.Type = adSmallInt Then  
            MsgBox "Column: " & colLoop.Name & vbCr & _  
                "Numeric scale: " & _  
                colLoop.NumericScale & vbCr & _  
                "Precision: " & colLoop.Precision  
        End If  
    Next colLoop  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
NumericScalePrecXError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndNumericScalePrecVB  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [NumericScale (propiedad, ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md)   
 [Precision (propiedad, ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)
