---
title: Ejemplo de la propiedad (VC ++) de origen | Microsoft Docs
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
- Source property [ADO], VC++ example
ms.assetid: e10d33da-ea30-4138-ae40-e9f6aa9d17d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da0bfacc4ab64929bcd37051efa9d36944871253
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930883"
---
# <a name="source-property-example-vc"></a>Ejemplo de la propiedad Source (VC ++)
Este ejemplo se muestra el [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) propiedad abriendo tres [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos basados en orígenes de datos diferentes.  
  
```  
// Source_Property_Sample.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void SourceX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   SourceX();  
   ::CoUninitialize();  
}  
  
void SourceX() {  
   // Define string variables.  
   _bstr_t strCmdSQL("Select title ,type, pubdate FROM titles ORDER BY title");    
   _bstr_t strSQL("SELECT title_ID AS TitleID, title AS Title, "   
      "publishers.pub_id AS PubID, pub_name AS PubName "  
      "FROM publishers INNER JOIN titles "   
      "ON publishers.pub_id = titles.pub_id "   
      "ORDER BY Title");  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB:: namespace.  
   _ConnectionPtr pConnection = NULL;  
   _RecordsetPtr pRstTitles = NULL;  
   _RecordsetPtr pRstPublishers = NULL;  
   _RecordsetPtr pRstPublishersDirect = NULL;  
   _RecordsetPtr pRstTitlesPublishers = NULL;  
   _CommandPtr pCmdSQL = NULL;  
  
   try {  
      // Open a connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      // Open a recordset based on a command object.  
      TESTHR(pCmdSQL.CreateInstance(__uuidof(Command)));  
      pCmdSQL->ActiveConnection = pConnection;  
      pCmdSQL->CommandText = strCmdSQL;  
      pRstTitles = pCmdSQL->Execute(NULL, NULL, adCmdText);  
  
      // Open a recordset based on a table  
      TESTHR(pRstPublishers.CreateInstance(__uuidof(Recordset)));  
      pRstPublishers->Open ("publishers", _variant_t((IDispatch *) pConnection, true),  
         adOpenForwardOnly, adLockReadOnly, adCmdTable);  
  
      // Open a recordset based on a table  
      TESTHR(pRstPublishersDirect.CreateInstance(__uuidof(Recordset)));  
      pRstPublishersDirect->Open ("publishers", _variant_t((IDispatch *) pConnection, true),  
         adOpenForwardOnly, adLockReadOnly, adCmdTableDirect);  
  
      // Open a recordset based on a SQL string.  
      TESTHR(pRstTitlesPublishers.CreateInstance(__uuidof(Recordset)));  
      pRstTitlesPublishers->Open(strSQL, _variant_t((IDispatch *) pConnection, true),  
         adOpenForwardOnly, adLockReadOnly, adCmdText);  
  
      // Use the Source property to display the source of each recordset.  
      printf("rstTitles source: \n%s\n\n",  
         (LPCSTR)(_bstr_t) pRstTitles->GetSource().bstrVal);  
  
      printf("rstPublishers source: \n%s\n\n",  
         (LPCSTR)(_bstr_t) pRstPublishers->GetSource().bstrVal);  
  
      printf("rstPublishersDirect source: \n%s\n\n",  
         (LPCSTR)(_bstr_t) pRstPublishersDirect->GetSource().bstrVal);  
  
      printf("rstTitlesPublishers source: \n%s\n\n",  
         (LPCSTR)(_bstr_t) pRstTitlesPublishers->GetSource().bstrVal);  
   }  
   catch (_com_error &e) {  
      // Notify the user of errors if any.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen)  
         pRstTitles->Close();  
   if (pRstPublishers)  
      if (pRstPublishers->State == adStateOpen)  
         pRstPublishers->Close();  
   if (pRstPublishersDirect)  
      if (pRstPublishersDirect->State == adStateOpen)  
         pRstPublishersDirect->Close();  
   if (pRstTitlesPublishers)  
      if (pRstTitlesPublishers->State == adStateOpen)  
         pRstTitlesPublishers->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
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
 [Propiedad Source (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
