---
title: Ejemplo de la propiedad Status (Recordset) (VB) | Microsoft Docs
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
- Status property [ADO Recordset], Visual Basic example
ms.assetid: e37b4d46-380d-4615-b4bb-e1a7b0851771
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f1f418ed4c8ac74a023203606ebf3934129525a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916793"
---
# <a name="status-property-example-recordset-vb"></a>Ejemplo de la propiedad Status (Recordset) (VB)
Este ejemplo se usa el [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad para mostrar los registros que se han modificado en una operación por lotes antes de que se ha producido una actualización por lotes.  
  
```  
'BeginStatusRecordsetVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    ' connection and recordset variables  
    Dim rstTitles As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' open recordset for batch update  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "Titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenKeyset, adLockBatchOptimistic, adCmdTable  
  
    ' change the type of psychology titles  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "psychology" Then rstTitles!Type = "self_help"  
        rstTitles.MoveNext  
    Loop  
  
    ' display Title ID and status  
    rstTitles.MoveFirst  
    Do Until rstTitles.EOF  
        If rstTitles.Status = adRecModified Then  
            Debug.Print rstTitles!title_id & " - Modified"  
        Else  
            Debug.Print rstTitles!title_id  
        End If  
    rstTitles.MoveNext  
    Loop  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then  
            ' Cancel the update because this is a demonstration  
            rstTitles.CancelBatch  
            rstTitles.Close  
        End If  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndStatusRecordsetVB  
```  
  
## <a name="see-also"></a>Vea también  
 [Propiedad Status (conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
