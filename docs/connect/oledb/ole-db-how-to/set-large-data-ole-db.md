---
title: Establecer datos de gran tamaño (OLE DB) | Microsoft Docs
description: Establecer datos de gran tamaño (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- large data
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 72827ffa7866b624c50a83c0d3695f0f011cfe5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994678"
---
# <a name="set-large-data-ole-db"></a>Establecer datos de gran tamaño (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este ejemplo, se muestra cómo establecer datos BLOB, crear una tabla, agregar un registro de ejemplo, capturar ese registro en el conjunto de filas y, después, establecer el valor del campo BLOB. Este ejemplo no es compatible con IA64.  
  
 Para pasar un puntero a su propio objeto de almacenamiento, el consumidor crea un descriptor de acceso que enlaza el valor de la columna BLOB y, a continuación, llama a los métodos **IRowsetChange::SetData** o **IRowsetChange::InsertRow** .  
  
 Este ejemplo requiere la base de datos de ejemplo AdventureWorks que se puede descargar de la página principal que muestra [ejemplos y proyectos de la comunidad de Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkID=85384) .  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows. Si la autenticación de Windows no está disponible, solicite a los usuarios que escriban sus credenciales en tiempo de ejecución. No guarde las credenciales en un archivo. Si tiene que conservar las credenciales, debería cifrarlas con la [API de criptografía de Win32](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="to-set-blob-data"></a>Para establecer los datos BLOB  
  
1.  Cree una estructura DBOBJECT que describa cómo se debe obtener acceso a la columna BLOB. Establezca el elemento **dwFlag** de la estructura DBOBJECT en STGM_READ y establezca el elemento iid en **IID_ISequentialStream** (la interfaz que se va a exponer).  
  
2.  Establezca las propiedades en el grupo de propiedades DBPROPSET_ROWSET de modo que el conjunto de filas sea actualizable.  
  
3.  Cree un conjunto de enlaces (uno de cada columna) utilizando una matriz de estructuras DBBINDING. Establezca el elemento **wType** de la estructura DBBINDING en DBTYPE_IUNKNOWN y el elemento **pObject** que señale a la estructura DBOBJECT creada.  
  
4.  Cree un descriptor de acceso utilizando la información de enlace de la matriz de estructuras DBBINDINGS.  
  
5.  Llame a **GetNextRows** para capturar las filas siguientes en el conjunto de filas. Llame a **GetData** para leer los datos del conjunto de filas.  
  
6.  Para establecer los datos, cree un objeto de almacenamiento que contiene los datos (y también el indicador de longitud) y, a continuación, llame a **IRowsetChange::SetData** (o a **IRowsetChange::InsertRow**) con el descriptor de acceso que enlaza la columna BLOB.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="description"></a>Descripción  
 Compile con ole32.lib oleaut32.lib y ejecute la siguiente lista de código C++. Esta aplicación se conecta a la instancia predeterminada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del equipo. En algunos sistemas operativos Windows, deberá cambiar (localhost) o (local) al nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para conectarse a una instancia con nombre, cambie la cadena de conexión de L"(local)" a L"(local)\\nombre", donde "nombre" es la instancia con nombre. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Express se instala en una instancia con nombre. Asegúrese de que en la variable de entorno INCLUDE se incluya el directorio que contiene msoledbsql.h.  
  
### <a name="code"></a>código  
  
```  
// compile with: ole32.lib oleaut32.lib  
#define UNICODE  
#define DBINITCONSTANTS  
#define INITGID  
#define OLEDBVER 0x0250  // to include correct interfaces  
  
#include <windows.h>  
#include <stdio.h>  
#include <stddef.h>  
#include <iostream>  
#include <oledb.h>  
#include <oledberr.h>  
#include <msoledbsql.h>  
  
using namespace std;  
  
#define SAFE_RELEASE(pIUnknown) if(pIUnknown) (pIUnknown)->Release();  
HRESULT GetCommandObject(REFIID riid, IUnknown** ppIUnknown);  
HRESULT CreateTable(ICommandText* pICommandText);  
  
class CSeqStream : public ISequentialStream {  
public:  
   // Constructors  
   CSeqStream();  
   virtual ~CSeqStream();  
  
   virtual BOOL Seek(ULONG iPos);  
   virtual BOOL Clear();  
   virtual BOOL CompareData(void* pBuffer);  
   virtual ULONG Length() { return m_cBufSize; };  
  
   virtual operator void* const() { return m_pBuffer; };  
  
   STDMETHODIMP_(ULONG) AddRef(void);  
   STDMETHODIMP_(ULONG) Release(void);  
   STDMETHODIMP QueryInterface(REFIID riid, LPVOID *ppv);  
  
   STDMETHODIMP Read(   
      /* [out] */ void __RPC_FAR *pv,  
      /* [in]  */ ULONG cb,  
      /* [out] */ ULONG __RPC_FAR *pcbRead);  
  
   STDMETHODIMP Write(   
      /* [in] */ const void __RPC_FAR *pv,  
      /* [in] */ ULONG cb,  
      /* [out]*/ ULONG __RPC_FAR *pcbWritten);  
  
private:  
   ULONG m_cRef;   // reference count  
   void* m_pBuffer;   // buffer  
   ULONG m_cBufSize;   // buffer size  
   ULONG m_iPos;   // current index position in the buffer  
};  
  
// class implementation  
CSeqStream::CSeqStream() {  
   m_iPos = 0;  
   m_cRef = 0;  
   m_pBuffer = NULL;  
   m_cBufSize = 0;  
  
   // The constructor AddRef's  
   AddRef();  
}  
  
CSeqStream::~CSeqStream() {  
   // Shouldn't have any references left ASSERT(m_cRef == 0);  
   CoTaskMemFree(m_pBuffer);  
}  
  
ULONG CSeqStream::AddRef() {  
   return ++m_cRef;  
}  
  
ULONG CSeqStream::Release() {  
   // ASSERT(m_cRef);  
   if (--m_cRef)  
      return m_cRef;  
  
   delete this;  
   return 0;  
}  
  
HRESULT CSeqStream::QueryInterface(REFIID riid, void** ppv) {  
   // ASSERT(ppv);  
   *ppv = NULL;  
  
   if (riid == IID_IUnknown)  
      *ppv = this;  
  
   if (riid == IID_ISequentialStream)  
      *ppv = this;  
  
   if(*ppv) {  
      ((IUnknown*)*ppv)->AddRef();  
      return S_OK;  
   }  
  
   return E_NOINTERFACE;  
}  
  
BOOL CSeqStream::Seek(ULONG iPos) {  
   // Make sure the desired position is within the buffer  
   // ASSERT(iPos == 0 || iPos < m_cBufSize);  
  
   // Reset the current buffer position  
   m_iPos = iPos;  
   return TRUE;  
}  
  
BOOL CSeqStream::Clear() {  
   // Frees the buffer  
   m_iPos = 0;  
   m_cBufSize = 0;  
  
   CoTaskMemFree(m_pBuffer);  
   m_pBuffer = NULL;  
  
   return TRUE;  
}  
  
BOOL CSeqStream::CompareData(void* pBuffer) {  
   // ASSERT(pBuffer);  
  
   // Quick and easy way to compare user buffer with the stream  
   return memcmp(pBuffer, m_pBuffer, m_cBufSize) == 0;  
}  
  
HRESULT CSeqStream::Read(void *pv, ULONG cb, ULONG* pcbRead) {  
   // Parameter checking  
   if (pcbRead)  
      *pcbRead = 0;  
  
   if (!pv)  
      return STG_E_INVALIDPOINTER;  
  
   if (cb == 0)  
      return S_OK;  
  
   // Actual code  
   ULONG cBytesLeft = m_cBufSize - m_iPos;  
   ULONG cBytesRead = cb > cBytesLeft ? cBytesLeft : cb;  
  
   // if no more bytes to retrieve return   
   if (cBytesLeft == 0)  
      return S_FALSE;   
  
   // Copy to users buffer the number of bytes requested or remaining  
   memcpy(pv, (void*)((BYTE*)m_pBuffer + m_iPos), cBytesRead);  
   m_iPos += cBytesRead;  
  
   if (pcbRead)  
      *pcbRead = cBytesRead;  
  
   if (cb != cBytesRead)  
      return S_FALSE;   
  
   return S_OK;  
}  
  
HRESULT CSeqStream::Write(const void *pv, ULONG cb, ULONG* pcbWritten) {  
   // Parameter checking  
   if (!pv)  
      return STG_E_INVALIDPOINTER;  
  
   if (pcbWritten)  
      *pcbWritten = 0;  
  
   if (cb == 0)  
      return S_OK;  
  
   // Enlarge the current buffer  
   m_cBufSize += cb;  
  
   // Need to append to the end of the stream  
   m_pBuffer = CoTaskMemRealloc(m_pBuffer, m_cBufSize);  
   memcpy((void*)((BYTE*)m_pBuffer + m_iPos), pv, cb);  
   // m_iPos += cb;  
  
   if (pcbWritten)  
      *pcbWritten = cb;  
  
   return S_OK;  
}  
  
int main() {  
   CoInitialize(NULL);  
  
   DBOBJECT ObjectStruct;  
   ObjectStruct.dwFlags = STGM_READ;  
   ObjectStruct.iid = IID_ISequentialStream;  
  
   struct BLOBDATA {  
      DBSTATUS dwStatus;     
      DBLENGTH dwLength;   
      ISequentialStream* pISeqStream;  
   };  
  
   BLOBDATA BLOBGetData;  
   BLOBDATA BLOBSetData;  
  
   const ULONG cBindings = 1;  
   DBBINDING rgBindings[cBindings];   
   HRESULT hr = S_OK;  
  
   IAccessor* pIAccessor = NULL;  
   ICommandText* pICommandText = NULL;  
   ICommandProperties* pICommandProperties = NULL;  
   IRowsetChange* pIRowsetChange = NULL;  
   IRowset* pIRowset = NULL;  
   CSeqStream* pMySeqStream = NULL;  
  
   DBCOUNTITEM cRowsObtained = 0;  
   HACCESSOR hAccessor = DB_NULL_HACCESSOR;  
   DBBINDSTATUS rgBindStatus[cBindings];  
   HROW* rghRows = NULL;  
  
   const ULONG cPropSets = 1;  
   DBPROPSET rgPropSets[cPropSets];  
   const ULONG cProperties = 1;  
   DBPROP rgProperties[cProperties];  
   const ULONG cBytes = 10;  
  
   BYTE pBuffer[cBytes];  
   ULONG cBytesRead = 0;  
  
   BYTE pReadData[cBytes];   // read BLOB data in this array  
   memset(pReadData, 0xAA, cBytes);  
  
   BYTE pWriteData[cBytes];   // write BLOB data from this array  
   memset(pWriteData, 'D', cBytes);  
  
   // Get Command object  
   hr = GetCommandObject(IID_ICommandText, (IUnknown**)&pICommandText);  
   if (FAILED(hr)) {  
      printf("Failed to get ICommandText interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Create table with image column and index  
   hr = CreateTable(pICommandText);  
   if (FAILED(hr)) {  
      printf("Failed to create table.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Set the DBPROPSET structure.  It is used to pass an array   
   // of DBPROP structures to SetProperties().  
   rgPropSets[0].guidPropertySet = DBPROPSET_ROWSET;  
   rgPropSets[0].cProperties = cProperties;  
   rgPropSets[0].rgProperties = rgProperties;  
  
   // Now set properties in the property group (DBPROPSET_ROWSET)  
   rgPropSets[0].rgProperties[0].dwPropertyID = DBPROP_UPDATABILITY;  
   rgPropSets[0].rgProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgPropSets[0].rgProperties[0].dwStatus = DBPROPSTATUS_OK;  
   rgPropSets[0].rgProperties[0].colid = DB_NULLID;  
   rgPropSets[0].rgProperties[0].vValue.vt = VT_I4;  
   V_I4(&rgPropSets[0].rgProperties[0].vValue) = DBPROPVAL_UP_CHANGE;  
  
   // Set the rowset properties  
   hr = pICommandText->QueryInterface(IID_ICommandProperties,  
      (void **)&pICommandProperties);  
  
   if (FAILED(hr)) {  
      printf("Failed to get ICommandProperties to set rowset properties.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandProperties->SetProperties(cPropSets, rgPropSets);  
  
   if (FAILED(hr)) {  
      printf("Execute failed to set rowset properties.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Execute a command (SELECT * FROM TestISeqStream)  
   hr = pICommandText->SetCommandText(DBGUID_DBSQL, L"SELECT * FROM TestISeqStream");  
  
   if (FAILED(hr)) {  
      printf("Failed to set command text SELECT * FROM.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandText->Execute(NULL,   
      IID_IRowsetChange,   
      NULL,   
      NULL,  
      (IUnknown**)&pIRowsetChange);  
  
   if (FAILED(hr)) {  
      printf("Failed to execute the command SELECT * FROM.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Fill the DBBINDINGS array.  
   rgBindings[0].iOrdinal = 2;   // ordinal position  
   rgBindings[0].obValue = offsetof(BLOBDATA, pISeqStream);  
   rgBindings[0].obLength = offsetof(BLOBDATA, dwLength);  
   rgBindings[0].obStatus = offsetof(BLOBDATA, dwStatus);  
   rgBindings[0].pTypeInfo = NULL;  
   rgBindings[0].pObject = &ObjectStruct;  
   rgBindings[0].pBindExt = NULL;  
   rgBindings[0].dwPart =  DBPART_VALUE | DBPART_STATUS | DBPART_LENGTH;  
   rgBindings[0].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
   rgBindings[0].eParamIO = DBPARAMIO_NOTPARAM;  
   rgBindings[0].cbMaxLen = 0;   
   rgBindings[0].dwFlags = 0;  
   rgBindings[0].wType = DBTYPE_IUNKNOWN;  
   rgBindings[0].bPrecision = 0;  
   rgBindings[0].bScale = 0;  
  
   // Create an accessor using the binding information.  
   hr = pIRowsetChange->QueryInterface(IID_IAccessor, (void**)&pIAccessor);  
   if (FAILED(hr)) {  
      printf("Failed to get IAccessor interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA,  
      cBindings,  
      rgBindings,   
      sizeof(BLOBDATA),  
      &hAccessor,  
      rgBindStatus);  
  
   if (FAILED(hr)) {  
      printf("Failed to create an accessor.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // get the first row.  
   hr = pIRowsetChange->QueryInterface(IID_IRowset, (void **)&pIRowset);  
   if (FAILED(hr)) {  
      printf("Failed to get IRowset interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIRowset->GetNextRows(NULL, 0, 1, &cRowsObtained, &rghRows);  
   hr = pIRowset->GetData(rghRows[0], hAccessor, &BLOBGetData);  
  
   // Verify the retrieved data, only if data is not null.  
   if (BLOBGetData.dwStatus == DBSTATUS_S_ISNULL) {  
      // Process null data  
      printf("Provider returned a null value.\n");  
   }   
   else if(BLOBGetData.dwStatus == DBSTATUS_S_OK) {  
      // Provider returned a nonNULL value  
      BLOBGetData.pISeqStream->Read( pBuffer, cBytes, &cBytesRead);  
  
      if (memcmp(pBuffer, pReadData, cBytes) != 0) {  
         // cleanup   
      }  
  
      SAFE_RELEASE(BLOBGetData.pISeqStream);  
   }  
  
   // Set up data for SetData.  
   pMySeqStream = new CSeqStream();  
  
   // Put data into ISequentialStream object for the provider to write.  
   pMySeqStream->Write(pWriteData, cBytes, NULL);  
  
   BLOBSetData.pISeqStream = (ISequentialStream*)pMySeqStream;  
   BLOBSetData.dwStatus = DBSTATUS_S_OK;  
   BLOBSetData.dwLength = pMySeqStream->Length();  
  
   // Set the data.  
   hr = pIRowsetChange->SetData(rghRows[0], hAccessor, &BLOBSetData);  
   if (FAILED(hr))     {  
      printf("Failed to set data.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIAccessor->ReleaseAccessor(hAccessor, NULL);  
   if (FAILED(hr)) {  
      printf("Failed to release accessor.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIRowset->ReleaseRows(cRowsObtained, rghRows, NULL, NULL, NULL);  
  
   if (FAILED(hr)) {  
      printf("Failed to release rows.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
Exit:  
   // Release all allocated memory and release interface pointers.  
   CoUninitialize();  
}  
  
HRESULT GetCommandObject(REFIID riid, IUnknown** ppIUnknown) {  
   HRESULT hr = S_OK;  
  
   // Local interface pointers, until a connection is made.  
   IDBInitialize* pIDBInitialize = NULL;  
   IDBProperties*  pIDBProperties = NULL;  
   IDBCreateSession* pIDBCreateSession = NULL;  
   IDBCreateCommand* pIDBCreateCommand = NULL;  
  
   const ULONG cPropSets = 1;  
   DBPROPSET rgPropSets[cPropSets];  
  
   const ULONG cProperties = 4;  
   DBPROP rgProperties[cProperties];  
  
   // Initialize property values needed to establish connection.  
   for ( ULONG i = 0 ; i < 4 ; i++ )  
      VariantInit(&rgProperties[i].vValue);  
  
   // Server name.  
   rgProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   rgProperties[0].vValue.vt = VT_BSTR;  
  
   rgProperties[0].vValue.bstrVal = SysAllocString(L"(local)");  
   rgProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgProperties[0].colid = DB_NULLID;  
  
   // Database.  
   rgProperties[1].dwPropertyID = DBPROP_INIT_CATALOG;  
   rgProperties[1].vValue.vt = VT_BSTR;  
   rgProperties[1].vValue.bstrVal = SysAllocString(L"AdventureWorks");  
   rgProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgProperties[1].colid = DB_NULLID;  
  
   rgProperties[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;  
   rgProperties[2].vValue.vt = VT_BSTR;  
   rgProperties[2].vValue.bstrVal = SysAllocString(L"SSPI");  
   rgProperties[2].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgProperties[2].colid = DB_NULLID;  
  
   // Properties are now set.  Next, construct DBPROPSET structure (rgInitPropSet) used to pass an   
   // array of DBPROP structures (InitProperties) to the SetProperties method.  
   rgPropSets[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgPropSets[0].cProperties = cProperties;  
   rgPropSets[0].rgProperties = rgProperties;  
  
   // Get the IDBInitialize interface.  
   hr = CoCreateInstance(CLSID_MSOLEDBSQL,   
      NULL,   
      CLSCTX_INPROC_SERVER,  
      IID_IDBInitialize,   
      (void**)&pIDBInitialize);  
  
   if (FAILED(hr)) {  
      printf("Failed to get IDBInitialize interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);  
   if (FAILED(hr)) {  
      printf("Failed to get IDBProperties interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIDBProperties->SetProperties(cPropSets, rgPropSets);  
   if (FAILED(hr)) {  
      printf("Failed to set properties for DBPROPSET_DBINIT.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIDBInitialize->Initialize();  
   if (FAILED(hr)) {  
      printf("Failed to initialize.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Create a session object.  
   hr = pIDBInitialize->QueryInterface( IID_IDBCreateSession,  
                                        (void **)&pIDBCreateSession);  
  
   if (FAILED(hr)) {  
      printf("Failed to get pIDBCreateSession interface.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pIDBCreateSession->CreateSession( NULL, IID_IDBCreateCommand, (IUnknown**)&pIDBCreateCommand);  
  
   if (FAILED(hr)) {  
      printf("Failed to create session object.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Get CommandText object  
   hr = pIDBCreateCommand->CreateCommand( NULL, riid, (IUnknown**)ppIUnknown);  
  
   if (FAILED(hr)) {  
      printf("Failed to create CommandText object.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   return hr;  
  
Exit:  
   // Free up all allocated memory and release interface pointers.  
   return hr;  
}  
  
HRESULT CreateTable(ICommandText* pICommandText) {  
   HRESULT hr = S_OK;  
  
   // drop the table "TestISeqStream" if the table exists.  
   hr = pICommandText->SetCommandText( DBGUID_DBSQL, L"if object_id('TestISeqStream') is not null drop table TestISeqStream");  
   if (FAILED(hr)) {  
      printf("Failed to set command text DROP TABLE.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandText->Execute(NULL, IID_NULL, NULL, NULL, NULL);  
   if (FAILED(hr)) {  
      printf("Failed to drop the table.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Create a new table.  
   hr = pICommandText->SetCommandText(DBGUID_DBSQL,   
      L"CREATE TABLE TestISeqStream (col1 int,col2 image)");  
  
   if (FAILED(hr)) {  
      printf("Failed to set command text CREATE TABLE.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandText->Execute(NULL, IID_NULL, NULL, NULL, NULL);  
   if (FAILED(hr)) {  
      printf("Failed to create table.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   // Insert one row into table.  
   hr = pICommandText->SetCommandText(DBGUID_DBSQL,  
      L"INSERT INTO TestISeqStream(col1,col2) VALUES (1,0xAAAAAAAAAAAAAAAAA)");  
   if (FAILED(hr)) {  
      printf("Failed to set command text INSERT INTO.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
   hr = pICommandText->Execute(NULL, IID_NULL, NULL, NULL, NULL);  
  
   if (FAILED(hr)) {  
      printf("Failed to insert record in the table.\n");  
      // Release any references and return.  
      goto Exit;  
   }  
  
Exit:  
   // Release all allocated memory and release interface pointers.  
   return hr;  
}  
```  
  
  
