---
title: Ejemplo del método (VC ++) Supports | Microsoft Docs
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
- Supports method [ADO], VC++ example
ms.assetid: 6e174179-9d95-41b9-b72b-6cdbdca6e255
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8eb0aa12a31337340854f941237d673abd1c601c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936714"
---
# <a name="supports-method-example-vc"></a>Ejemplo del método Supports (VC ++)
Este ejemplo se usa el [admite](../../../ado/reference/ado-api/supports-method.md) método para mostrar las opciones admitidas por un conjunto de registros abierto con diferentes tipos de cursor. La función DisplaySupport es necesaria para ejecutar este ejemplo.  
  
```  
// SupportsMethodExample.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <stdio.h>  
#include <ole2.h>  
#include <conio.h>  
  
// Function Declarations.  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
  
void SupportsX();  
void DisplaySupport(_RecordsetPtr pRstTemp);  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
   SupportsX();  
   ::CoUninitialize();  
}  
  
void SupportsX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _RecordsetPtr pRstTitles = NULL;  
  
   // Assign connection string to a variable  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open a recordset from Titles table  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
  
      // Fill array with CursorType constants.  
      int aintCursorType[4];  
      aintCursorType[0] = adOpenForwardOnly;  
      aintCursorType[1] = adOpenKeyset;  
      aintCursorType[2] = adOpenDynamic;  
      aintCursorType[3] = adOpenStatic;  
  
      // Open recordset using each CursorType and optimistic locking.  
      // Then call the DisplaySupport procedure to display the supported options.  
      for (int intIndex=0 ; intIndex <= 3 ; intIndex++) {  
         pRstTitles->CursorType = (enum CursorTypeEnum)aintCursorType[intIndex];  
         pRstTitles->LockType = adLockOptimistic;  
  
         // Pass the Cursor type and LockType to the Recordset.  
         pRstTitles->Open ("titles", strCnn,   
            (enum CursorTypeEnum)aintCursorType[intIndex], adLockOptimistic, adCmdTable);  
  
         switch(aintCursorType[intIndex]) {  
         case adOpenForwardOnly:  
            printf("\nForwardOnly cursor supports:\n");  
            break;  
  
         case adOpenKeyset:  
            printf("\nKeyset cursor supports:\n");  
            break;  
  
         case adOpenDynamic:  
            printf("\nDynamic cursor supports:\n");  
            break;  
  
         case adOpenStatic:  
            printf("\nStatic cursor supports:\n");  
            break;  
  
         default :  
            break;  
         }  
  
         DisplaySupport(pRstTitles);  
      }  
   }  
   catch(_com_error &e) {  
      // Display errors, if any. Pass connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstTitles->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         PrintComError(e);  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
  
   // Clean up objects before exit.  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen)  
         pRstTitles->Close();  
}  
  
void DisplaySupport (_RecordsetPtr pRstTemp) {  
   // Fill array with cursor option constants.  
   long  alngConstants[11];  
   alngConstants[0] = adAddNew;  
   alngConstants[1] = adApproxPosition;  
   alngConstants[2] = adBookmark;  
   alngConstants[3] = adDelete;  
   alngConstants[4] = adFind;  
   alngConstants[5] = adHoldRecords;  
   alngConstants[6] = adMovePrevious;  
   alngConstants[7] = adNotify;  
   alngConstants[8] = adResync;  
   alngConstants[9] = adUpdate;  
   alngConstants[10] = adUpdateBatch;  
  
   for ( int intIndex = 0 ; intIndex <= 10 ; intIndex++ ) {  
      VARIANT_BOOL booSupports = pRstTemp->Supports( (enum CursorOptionEnum)alngConstants[intIndex] );  
  
      if (booSupports) {  
         switch(alngConstants[intIndex]) {  
         case adAddNew :  
            printf("\n  AddNew");  
            break;  
  
         case adApproxPosition :  
            printf("\n  AbsolutePosition and AbsolutePage");  
            break;  
  
         case adBookmark :  
            printf("\n  Bookmark");  
            break;  
  
         case adDelete :  
            printf("\n  Delete");  
            break;  
  
         case adFind :  
            printf("\n  Find");  
            break;  
  
         case adHoldRecords :  
            printf("\n  Holding Records");  
            break;  
  
         case adMovePrevious :  
            printf("\n  MovePrevious and Move");  
            break;  
  
         case adNotify :  
            printf("\n  Notifications");  
            break;  
  
         case adResync :  
            printf("\n  Resyncing data");  
            break;  
  
         case adUpdate :  
            printf("\n  Update");  
            break;  
  
         case adUpdateBatch :  
            printf("\n  Batch updating");  
            break;  
  
         default :  
            break;  
         }  
      }  
   }  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
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
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
