---
title: Ejemplo de la propiedad StayInSync (VC ++) | Microsoft Docs
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
- StayInSync property [ADO], VC++ example
ms.assetid: 3a5db5f0-094b-46e1-939b-d9fa9417a406
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b5df87b29a0fc73a83d8b6dde568a7c173876cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930754"
---
# <a name="stayinsync-property-example-vc"></a>Ejemplo de la propiedad StayInSync (VC ++)
Este ejemplo se muestra cómo el [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) propiedad facilita el acceso a las filas en una jerárquica [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 El bucle externo muestra el nombre y apellido de cada autor, estado e identificación. Anexa **Recordset** para cada fila se recupera de la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección y asignada automáticamente a **rstTitleAuthor** por el **StayInSync**  propiedad cada vez que el elemento primario **Recordset** se mueve a una nueva fila. El bucle interno muestra cuatro campos de cada fila del conjunto de registros anexados.  
  
```  
// BeginStayInSyncCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void StayInSyncX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1 ;  
  
   StayInSyncX();  
   ::CoUninitialize();  
}  
  
void StayInSyncX() {  
   HRESULT  hr = S_OK;  
  
   // Define string variables.  
   _bstr_t strCnn("Provider='MSDataShape'; Data Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   _RecordsetPtr pRst = NULL;  
   _RecordsetPtr pRstTitleAuthor = NULL;  
  
   try {  
      TESTHR(pRstTitleAuthor.CreateInstance(__uuidof(Recordset)));  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      TESTHR(pRst.CreateInstance(__uuidof(Recordset)));  
  
      // Open connection.  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
      pRst->PutStayInSync(true);  
  
      // Open recordset with names from Author & titleauthor table.  
      pRst->Open("SHAPE  {select * from authors} "   
         "APPEND ({select * from titleauthor}"  
         "RELATE au_id TO au_id) AS chapTitleAuthor",  
         _variant_t((IDispatch*)pConnection, true), adOpenStatic, adLockReadOnly, adCmdText);  
  
      pRstTitleAuthor = pRst->GetFields()->GetItem("chapTitleAuthor")->Value;  
      while (!(pRst->EndOfFile)) {      
         printf("\n%s  %s  %s    %s\n", (LPCSTR)(_bstr_t)pRst->  
            Fields->GetItem("au_fname")->Value,  
            (LPCSTR)(_bstr_t)pRst->Fields->GetItem("au_lname")->Value,  
            (LPCSTR)(_bstr_t)pRst->Fields->GetItem("state")->Value,   
            (LPCSTR)(_bstr_t)pRst->Fields->GetItem("au_id")->Value);  
  
         _variant_t vIndex;  
         while ( !(pRstTitleAuthor->EndOfFile) ) {  
            vIndex = (short) 0;  
            printf("%s    ",(LPCSTR)(_bstr_t)pRstTitleAuthor->Fields->Item[&vIndex]->Value);  
            vIndex = (short) 1;  
            printf("%s    ",(LPCSTR)(_bstr_t)pRstTitleAuthor->Fields->Item[&vIndex]->Value);  
            vIndex = (short) 2;  
            printf("%s    ",(LPCSTR)(_bstr_t)pRstTitleAuthor->Fields->Item[&vIndex]->Value);  
            vIndex = (short) 3;  
            printf("%s\n",(LPCSTR)(_bstr_t)pRstTitleAuthor->Fields->Item[&vIndex]->Value);  
  
            pRstTitleAuthor->MoveNext();  
         }  
         pRst->MoveNext();  
      }  
   }  
   catch(_com_error &e) {  
      // Notify user of errors, if any.  Pass connection pointer accessed from the Recordset.  
      PrintProviderError(pConnection);  
      PrintComError(e);     
   }  
  
   // Clean up objects before exit.  
   if (pRst)  
      if (pRst->State == adStateOpen)  
         pRst->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("Error number: %x\t%s\n", pErr->Number, (LPCSTR) pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.    
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Colección de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propiedad StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)
