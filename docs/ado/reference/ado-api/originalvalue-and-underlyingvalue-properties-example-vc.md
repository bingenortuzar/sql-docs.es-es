---
title: Ejemplo OriginalValue y UnderlyingValue propiedades (VC ++) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- UnderlyingValue property [ADO], VC++ example
- OriginalValue property [ADO]
ms.assetid: c5762ad2-f43b-453d-b44a-9c70210eb00f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b4950634f473ca70c26b7b2b2c8159fb9a75fb0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931826"
---
# <a name="originalvalue-and-underlyingvalue-properties-example-vc"></a>Ejemplo OriginalValue y UnderlyingValue propiedades (VC ++)
Este ejemplo se muestra el [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) y [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) propiedades al mostrar un mensaje si los datos subyacentes de un registro ha cambiado durante una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) actualización por lotes.  
  
## <a name="example"></a>Ejemplo  
  
```  
// BeginOriginalValueCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// class extracts title_id and type from titles table  
class CTitleRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CTitleRs)  
  
   // Column title_id is the 1st field in the Recordset  
   ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar, m_szau_Title_id, sizeof(m_szau_Title_id), lau_Title_idStatus, FALSE)  
  
   // Column type is the 3rd field in the Recordset  
   ADO_VARIABLE_LENGTH_ENTRY2(3, adVarChar, m_szau_Type, sizeof(m_szau_Type), lau_TypeStatus, TRUE)  
  
   END_ADO_BINDING()  
  
public:  
   CHAR m_szau_Title_id[7];  
   ULONG lau_Title_idStatus;  
   CHAR m_szau_Type[13];  
   ULONG lau_TypeStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void OriginalValueX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   OriginalValueX();  
   ::CoUninitialize();  
}  
  
void OriginalValueX() {  
   // Define ADO object pointers, initialize pointers on define.  These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   FieldPtr pFldType = NULL;  
   _RecordsetPtr pRstTitles = NULL;  
  
   // Define string variables.  
   _bstr_t strSQLChange("UPDATE Titles SET Type = 'sociology' WHERE Type = 'psychology'");  
   _bstr_t strSQLRestore("UPDATE Titles SET Type = 'psychology' WHERE Type = 'sociology'");  
  
   // Define Other Variables  
   HRESULT hr = S_OK;  
   IADORecordBinding *picRs = NULL;   // Interface Pointer declared  
   CTitleRs titlers;   // C++ Class object  
   char * token1;  
  
   try {  
      _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
      // Open connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      // Open Recordset for batch update.  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
      pRstTitles->PutActiveConnection(_variant_t((IDispatch *)pConnection, true));  
      pRstTitles->CursorType = adOpenKeyset;  
      pRstTitles->LockType = adLockBatchOptimistic;  
  
      // Cast connection pointer to IDispatch type; convert to correct variant type.  
      pRstTitles->Open("Titles", _variant_t((IDispatch *)pConnection,true),  
         adOpenKeyset, adLockBatchOptimistic, adCmdTable);  
  
      // Open IADORecordBinding interface pointer for Binding Recordset to a class.  
      TESTHR(pRstTitles->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ Class here    
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Set field object variable for Type field.  
      pFldType = pRstTitles->Fields->GetItem("type");  
  
      // Change the type of psychology titles.  
      while ( !(pRstTitles->EndOfFile) ) {  
         if (!strcmp(strtok_s((char *)titlers.m_szau_Type, " ", &token1), "psychology"))  
            pFldType->Value = "self_help";  
         pRstTitles->MoveNext();  
      }  
  
      // Simulate a change by another user by updating data using a command string.  
      pConnection->Execute(strSQLChange, NULL, 0);  
  
      // Check for changes.  
      pRstTitles->MoveFirst();  
      while (!(pRstTitles->EndOfFile)) {  
         if (strcmp(pFldType->OriginalValue.pcVal, pFldType->UnderlyingValue.pcVal)) {  
            printf("Data has changed!");  
  
            printf("\nTitle ID: %s", titlers.lau_Title_idStatus ==   
               adFldOK ? titlers.m_szau_Title_id : "<NULL>");  
  
            printf("\nCurrent Value: %s", (LPCSTR) (_bstr_t) pFldType->Value);  
  
            printf("\nOriginal Value: %s", (LPCSTR) (_bstr_t) pFldType->OriginalValue);  
  
            printf("\nUnderlying Value: %s\n\n", (LPCSTR) (_bstr_t) pFldType->UnderlyingValue);  
         }  
         pRstTitles->MoveNext();  
      }  
   }  
   catch (_com_error &e)  {  
      // Notify the user of errors if any.  
      // Pass a connection pointer accessed from the Connection.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   // Clean up objects before exit.  Release the IADORecordset Interface here     
   if (picRs)  
      picRs->Release();  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen) {  
         // Cancel the update because this is a demonstration.  
         pRstTitles->CancelBatch(adAffectAll);  
         pRstTitles->Close();  
      }  
      if (pConnection)  
         if (pConnection->State == adStateOpen) {  
            // Restore Original Values.  
            pConnection->Execute(strSQLRestore, NULL, 0);  
            pConnection->Close();  
         }  
};  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount -1.  
      for (long i = 0 ; i < nCount ; i++) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print COM errors.   
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
 **¡Ha cambiado los datos!**  
**Id. de título: PS1372**  
**Valor actual: self_help**   
**Valor original: psicología**   
**Valor subyacente: sociología**   
**¡Ha cambiado los datos!**  
**Id. de título: PS2091**  
**Valor actual: self_help**   
**Valor original: psicología**   
**Valor subyacente: sociología**   
**¡Ha cambiado los datos!**  
**Id. de título: PS2106**  
**Valor actual: self_help**   
**Valor original: psicología**   
**Valor subyacente: sociología**   
**¡Ha cambiado los datos!**  
**Id. de título: PS3333**  
**Valor actual: self_help**   
**Valor original: psicología**   
**Valor subyacente: sociología**   
**¡Ha cambiado los datos!**  
**Id. de título: PS7777**  
**Valor actual: self_help**   
**Valor original: psicología**   
**Valor subyacente: sociología**    
## <a name="see-also"></a>Vea también  
 [Propiedad OriginalValue (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propiedad UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
