---
title: Conexión de Close (método), ejemplo de la propiedad de tipo de tabla (VC ++) | Microsoft Docs
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
- Type property [ADOX], VC++ example
- Close method [ADOX], VC++ example
ms.assetid: d0e250aa-fc57-4fd3-9610-d64f50c5507f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ff8cf50279d9be6b3ed334982e2140f0bd41f4d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966695"
---
# <a name="connection-close-method-table-type-property-example-vc"></a>Ejemplo de propiedad tipo de tabla, método connection close (VC++)
Establecer el [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) propiedad **nada** debe "cerrar" el catálogo. Recopilaciones asociadas estará vacías. Los objetos que se crearon a partir de los objetos de esquema en el catálogo se quedarán huérfanos. Las propiedades en los objetos que ya se ha almacenado en caché aún estará disponibles, pero se producirá un error al intentar leer las propiedades que requieren una llamada al proveedor.  
  
```  
// BeginCloseConnectionCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void CloseConnectionByNothingX();  
void CloseConnectionX();  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL) ) )  
      return -1;  
  
   CloseConnectionByNothingX();  
   CloseConnectionX();  
  
   ::CoUninitialize();  
}  
  
void CloseConnectionByNothingX() {  
   HRESULT hr = S_OK;  
  
   // Define and initialize ADOX object pointers, in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Define other variables  
   _variant_t vIndex = (short) 0;  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
  
      m_pCnn->Open("Provider='Microsoft.JET.OLEDB.4.0';Data Source= 'c:\\Northwind.mdb';", "", "", NULL);  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
      m_pTable = m_pCatalog->Tables->GetItem(vIndex);  
  
      // Cache m_pTable.Type info  
      cout << m_pTable->Type << endl;  
  
      _variant_t vCnn;  
      vCnn.vt = VT_DISPATCH;  
      vCnn.pdispVal = NULL;  
      m_pCatalog->PutActiveConnection(vCnn);  
  
      // m_pTable is orphaned, will succeed if this was cached  
      cout << m_pTable->Type << endl;  
  
      cout << m_pTable->Columns->GetItem(vIndex)->DefinedSize << endl;  
      // Previous line will fail if this info has not been cached  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\nError\n\tSource :  %s \n\tdescription : %s \n", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in CloseConnectionByNothingX...." << endl;  
   }  
}  
  
void CloseConnectionX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB  namespace.  
  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Define other variables  
   _variant_t vIndex = (short) 0;  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      m_pCnn->Open("Provider='Microsoft.JET.OLEDB.4.0';Data Source= 'c:\\Northwind.mdb';", "", "", NULL);  
  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
  
      m_pTable = m_pCatalog->Tables->GetItem(vIndex);  
  
      // Cache m_pTable.Type info  
      cout << m_pTable->Type << endl;  
  
      m_pCnn->Close();  
  
      // m_pTable is orphaned, will succeed if this was cached  
      cout << m_pTable->Type << endl;  
  
      cout << m_pTable->Columns->GetItem(vIndex)->DefinedSize << endl;  
      // Previous line will fail if this info has not been cached  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\nError\n\tSource :  %s \n\tdescription : %s \n", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in CloseConnectionX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection (propiedad, ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
