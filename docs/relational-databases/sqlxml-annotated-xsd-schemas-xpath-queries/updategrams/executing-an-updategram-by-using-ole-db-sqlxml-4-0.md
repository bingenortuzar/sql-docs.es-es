---
title: Ejecutar un diagrama de actualización mediante OLE DB (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- ICommandStream interface
- updategrams [SQLXML], OLE DB
- OLE DB, SQLXML
- executing updategrams [SQLXML]
ms.assetid: 4154c590-1541-49d0-8117-4ddf2ce5ccba
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6aa4562f21b33966df3df17f7b486e3cc2935b52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086869"
---
# <a name="executing-an-updategram-by-using-ole-db-sqlxml-40"></a>Ejecutar un diagrama de actualización mediante OLE DB (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se proporciona un ejemplo funcional de usingOLE DB para ejecutar un diagrama de actualización.  
  
## <a name="using-icommandstream-to-set-an-xml-command"></a>Usar ICommandStream para establecer un comando XML  
 La interfaz OLE DB (versión 2.6 o posterior) ICommandStream pasa un comando como un objeto de secuencia, en lugar de como una cadena.  
  
 Esta interfaz permite a un comando estar en cualquier codificación que el analizador XML entienda. Cuando se llama ICommand:: Execute, el texto del comando se lee directamente desde el flujo y se requiere ninguna conversión. Por lo tanto, ejecutar los comandos XML mediante ICommandStream interfaz es más eficaz.  
  
### <a name="setting-xml-as-a-command-using-icommandstream-and-retrieving-the-results-as-an-xml-document"></a>Establecer XML como un comando mediante ICommandStream y recuperar los resultados como un documento XML  
 Se puede usar la interfaz ICommandStream para establecer documentos XML como un comando y se pueden recuperar los resultados como un documento XML.  
  
#### <a name="executing-templates-with-xpath-queries"></a>Ejecutar plantillas con consultas XPath  
 La siguiente plantilla XML, que consta de una consulta XPath se especifica como un comando mediante ICommandStream:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:xpath-query mapping-schema="Schema.xml">Person.Contact</sql:xpath-query>  
</ROOT>  
```  
  
 La consulta XPath de la plantilla se ejecuta en el siguiente esquema de asignación:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data" xmlns:dt="urn:schemas-microsoft-com:datatypes" xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Person.Contact" >  
<AttributeType name="ContactID" />  
<AttributeType name="FirstName" />  
<AttributeType name="LastName" />  
<attribute type="ContactID" />  
<attribute type="FirstName" />  
<attribute type="LastName" />  
</ElementType>  
</Schema>  
```  
  
 La consulta devuelve todos los elementos de empleado. Con la asignación predeterminada, el  **\<Person.Contact >** elemento se asigna a la tabla Person.Contact de la base de datos AdventureWorks.  
  
###### <a name="to-set-xml-as-a-command-and-retrieving-result-as-an-xml-document"></a>Para establecer XML como un comando y recuperar el resultado como un documento XML  
  
1.  Inicialice y establezca una conexión a la base de datos.  
  
2.  Obtener la interfaz ICommandStream en ICommand.  
  
3.  Establezca las propiedades de comando necesarias. En este ejemplo, la propiedad SSPROP_STREAM_BASEPATH específica del proveedor está establecida en el directorio donde están almacenados el esquema de asignación y los archivos de plantilla.  
  
4.  Usar ICommandStream:: SetCommandStream para especificar la secuencia de comandos. En este ejemplo, la plantilla XML que se ejecuta se lee de un archivo. Esto resulta útil si desea ejecutar plantillas XML grandes.  
  
5.  Ejecute el comando XML mediante ICommand:: Execute, que solicita el identificador de interfaz de IID_ISequentialStream.  
  
6.  Procese el resultado. En este ejemplo, el XML que se lee del flujo se muestra en la pantalla.  
  
    ```  
    void InitializeAndEstablishConnection();  
    void SetCommandProperties();  
    void ProcessResultSet();  
  
    #define UNICODE  
    #define _UNICODE  
    #define DBINITCONSTANTS  
    #define INITGUID  
  
    #include <stdio.h>  
    #include <tchar.h>  
    #include <stddef.h>  
    #include <windows.h>  
    #include <iostream.h>  
    #include <oledb.h>  
    #include <SQLOLEDB.h>  
  
    class CSequentialStream : public ISequentialStream  
    {  
       private:     
          ULONG       m_cRef;              // reference count  
          HANDLE      m_hFile;         // handle to the file  
          LPWSTR      m_wszFileName;      // the file name  
  
       public:  
          CSequentialStream( LPWSTR );  
          virtual ~CSequentialStream();  
  
          // IUnknown Methods  
          STDMETHODIMP_(ULONG)    AddRef();  
          STDMETHODIMP_(ULONG)    Release();  
          STDMETHODIMP QueryInterface( REFIID, LPVOID* );  
  
          // ISequentialStream Methods  
          STDMETHODIMP Read(   
                /* [out] */ void __RPC_FAR*,  
                /* [in]  */ ULONG,  
                /* [out] */ ULONG __RPC_FAR* );  
  
          STDMETHODIMP Write(   
                /* [in] */ const void __RPC_FAR*,  
                /* [in] */ ULONG,  
                /* [out]*/ ULONG __RPC_FAR* );  
    };  
  
    IDBInitialize*       pIDBInitialize     = NULL;  
    IDBProperties*       pIDBProperties     = NULL;  
    IDBCreateSession*    pIDBCreateSession  = NULL;  
    IDBCreateCommand*    pIDBCreateCommand  = NULL;  
    ICommand*            pICommand          = NULL;  
    ICommandStream*      pICommandStream    = NULL;  
    ICommandProperties*    pICommandProperties = NULL;  
    IColumnsInfo*        pIColumnsInfo      = NULL;  
    ISequentialStream*    pIXMLOutput      = NULL;  
    DBCOLUMNINFO*        pDBColumnInfo      = NULL;  
    IAccessor*           pIAccessor        =  NULL;  
    DBPROP               InitProperties[4];  
    DBPROPSET            rgInitPropSet[1];  
    ULONG                i, j;  
    HRESULT              hr;  
    LONG                 cNumRows = 0;  
    ULONG                lNumCols;  
    WCHAR*               pStringsBuffer;  
    DBBINDING*           pBindings;  
    ULONG                ConsumerBufColOffset = 0;  
    HACCESSOR            hAccessor;  
    ULONG                lNumRowsRetrieved;  
    HROW                 hRows[10];  
    HROW*                pRows = &hRows[0];  
    BYTE*                pBuffer;  
    CSequentialStream    XMLInput( L"Query.xml" );  
  
    CSequentialStream::CSequentialStream  
    (  
       LPWSTR      wszFileName  
    )  
    :  
       m_cRef( 0 ),  
       m_hFile( NULL ),  
       m_wszFileName( NULL )  
    {  
        // The constructor AddRefs.  
        AddRef();  
  
       // Allocate memory for the file name.  
       m_wszFileName = (LPWSTR) CoTaskMemAlloc( ( wcslen( wszFileName ) + 1 ) * 2 );  
  
       // Copy the file name.  
       wcscpy( m_wszFileName, wszFileName );  
    }  
  
    CSequentialStream::~CSequentialStream  
    (  
    )  
    {  
       // Free any allocated memory.  
       if( m_wszFileName )  
          CoTaskMemFree( m_wszFileName );  
  
       // Close the file.  
       if( m_hFile )  
          CloseHandle( m_hFile );  
    }  
  
    ULONG      
    CSequentialStream::AddRef  
    (  
    )  
    {  
        return ++m_cRef;  
    }  
  
    ULONG  
    CSequentialStream::Release()  
    {  
        if(--m_cRef)  
            return m_cRef;  
  
        delete this;  
        return 0;  
    }  
  
    HRESULT   
    CSequentialStream::QueryInterface  
    (     
       REFIID riid,   
       void** ppv  
    )  
    {  
        *ppv = NULL;  
  
        if (riid == IID_IUnknown)  
            *ppv = this;  
  
        if (riid == IID_ISequentialStream)  
            *ppv = this;  
  
        if(*ppv)  
        {  
            ((IUnknown*)*ppv)->AddRef();  
            return S_OK;  
        }  
  
        return E_NOINTERFACE;  
    }  
  
    HRESULT   
    CSequentialStream::Read  
    (  
       void *pv,   
       ULONG cb,   
       ULONG* pcbRead  
    )  
    {  
       ULONG   cBytesRead = 0;  
  
        // Parameter checking.  
        if(pcbRead)  
            *pcbRead = 0;  
  
        if(!pv)  
            return STG_E_INVALIDPOINTER;  
  
        if(cb == 0)  
            return S_OK;  
  
       // Do we need to open the file?  
       if( m_hFile == NULL )  
       {  
          // Open the file.  
          m_hFile = CreateFile( m_wszFileName, GENERIC_READ, 0, NULL, OPEN_EXISTING, 0, NULL );  
  
          // If the file failed to open, return E_FAIL.  
          if( m_hFile == INVALID_HANDLE_VALUE )  
             return E_FAIL;  
       }  
  
       // Clear the buffer.  
       ZeroMemory( pv, cb );  
  
       // Read cb bytes from the stream.  
       if( !ReadFile( m_hFile, pv, cb, &cBytesRead, NULL ) )  
          return E_FAIL;  
  
       // Inform the user of how many bytes to read.  
       if( NULL != pcbRead )   
          *pcbRead = cBytesRead;  
  
        if(cb != cBytesRead)  
            return S_FALSE;   
  
        return S_OK;  
    }  
  
    HRESULT   
    CSequentialStream::Write  
    (  
       const void *pv,   
       ULONG cb,   
       ULONG* pcbWritten  
    )  
    {  
       // For this example, only a read-only stream is needed.  
       return STG_E_CANTSAVE;  
    }  
  
    void main()   
    {  
       // Call a function to initialize and establish a connection.   
        InitializeAndEstablishConnection();  
  
        // Create a session object.  
        if(FAILED(pIDBInitialize->QueryInterface(  
                                    IID_IDBCreateSession,  
                                    (void**) &pIDBCreateSession)))  
        {  
            cout << "Failed to obtain IDBCreateSession interface.\n";  
        }  
  
        if(FAILED(pIDBCreateSession->CreateSession(  
                                         NULL,   
                                         IID_IDBCreateCommand,   
                                         (IUnknown**) &pIDBCreateCommand)))  
        {  
            cout << "pIDBCreateSession->CreateSession failed.\n";  
        }  
  
        // Access the ICommand interface.  
        if(FAILED(pIDBCreateCommand->CreateCommand(  
                                        NULL,   
                                        IID_ICommand,   
                                        (IUnknown**) &pICommand)))  
        {  
            cout << "Failed to access ICommand interface.\n";  
        }  
  
       // Get an ICommandStream interface.  
       if(FAILED(pICommand->QueryInterface( IID_ICommandStream, (void**) &pICommandStream)))  
       {  
          cout << "Failed to get an ICommandStream interface.\n";  
       }  
  
       // Get an ICommandProperties interface.  
       if(FAILED(pICommand->QueryInterface( IID_ICommandProperties, (void**) &pICommandProperties)))  
       {  
          cout << "Failed to get an ICommandProperties interface.\n";  
       }  
  
       // Set the command properties.  
       SetCommandProperties();  
  
        // Use SetCommandStream() to specify the command stream.  
        if(FAILED(pICommandStream->SetCommandStream(IID_ISequentialStream, DBGUID_DEFAULT, (ISequentialStream*) &XMLInput )))  
        {  
            cout << "Failed to set command stream.\n";  
        }  
  
        // Execute the command.  
        if(FAILED(hr = pICommand->Execute(NULL,   
                                        IID_ISequentialStream,   
                                        NULL,   
                                        &cNumRows,   
                                        (IUnknown **) &pIXMLOutput )))  
        {  
            cout << "Failed to execute command.\n";  
        }  
  
        // Process the result set.  
        ProcessResultSet();   
  
        // Free memory.  
       if( pIXMLOutput )  
          pIXMLOutput->Release();  
       pICommandProperties->Release();  
       pICommandStream->Release();  
        pICommand->Release();  
        pIDBCreateCommand->Release();  
        pIDBCreateSession->Release();  
  
        if(FAILED(pIDBInitialize->Uninitialize()))  
        {  
            /*Uninitialize is not required, but it fails if an interface  
            has not been released. This can be used for debugging.  
            cout << "Problem uninitializing.\n"; */  
        } // endif.  
        pIDBInitialize->Release();  
  
        // Release the COM library.  
        CoUninitialize();  
    };  
  
    //--------------------------------------------------------------------  
    void InitializeAndEstablishConnection()  
    {      
        // Initialize the COM library.  
        CoInitialize(NULL);  
  
        // Obtain access to the SQLOLEDB Provider.  
        hr = CoCreateInstance(CLSID_SQLOLEDB,   
                              NULL,   
                              CLSCTX_INPROC_SERVER,  
                              IID_IDBInitialize,   
                              (void **) &pIDBInitialize);  
        if(FAILED(hr))  
        {  
            printf("Failed to get IDBInitialize interface.\n");  
        } // end if  
  
        /*  
        Initialize the property values needed   
        to establish the connection.  
        */  
        for(i = 0; i < 4; i++)   
            VariantInit(&InitProperties[i].vValue);  
  
        // Server name.  
        InitProperties[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
        InitProperties[0].vValue.vt     = VT_BSTR;  
        InitProperties[0].vValue.bstrVal=   
                                SysAllocString(L"Server");  
        InitProperties[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[0].colid         = DB_NULLID;  
  
    // Database.  
        InitProperties[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
        InitProperties[1].vValue.vt     = VT_BSTR;  
        InitProperties[1].vValue.bstrVal= SysAllocString(L"northwind");  
        InitProperties[1].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[1].colid         = DB_NULLID;  
  
    // Username (login).  
        InitProperties[2].dwPropertyID  = DBPROP_AUTH_USERID;   
        InitProperties[2].vValue.vt     = VT_BSTR;  
        InitProperties[2].vValue.bstrVal= SysAllocString(L"Login");  
        InitProperties[2].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[2].colid         = DB_NULLID;  
  
    // Password.  
    //    InitProperties[3].dwPropertyID  = DBPROP_AUTH_PASSWORD;   
    //    InitProperties[3].vValue.vt     = VT_BSTR;  
    //    InitProperties[3].vValue.bstrVal= SysAllocString(L"Password");  
    //    InitProperties[3].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    //    InitProperties[3].colid         = DB_NULLID;  
  
        /*  
        Now that the properties are set, construct the DBPROPSET structure.  
        (rgInitPropSet). The DBPROPSET structure is used to pass an array   
        of DBPROP structures (InitProperties) to the SetProperties method.  
        */  
        rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
    //  rgInitPropSet[0].cProperties    = 4;  
        rgInitPropSet[0].cProperties    = 3;  
        rgInitPropSet[0].rgProperties   = InitProperties;  
  
        // Set initialization properties.  
        hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                                       (void **)&pIDBProperties);  
        if(FAILED(hr))  
        {  
            cout << "Failed to get IDBProperties interface.\n";  
        }  
  
        hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
        if(FAILED(hr))  
        {  
            cout << "Failed to set initialization properties.\n";  
        } // end if  
  
        pIDBProperties->Release();  
  
        // Establish the connection to the data source.  
        if(FAILED(pIDBInitialize->Initialize()))  
        {  
            cout << "Problem establishing connection to the data source.\n";  
        }  
    } // End of InitializeAndEstablishConnection.  
    void SetCommandProperties()  
    {      
    //    for(i = 0; i < 4; i++)   
            VariantInit(&InitProperties[0].vValue);  
  
        // Server name.  
        InitProperties[0].dwPropertyID  = SSPROP_STREAM_BASEPATH;  
        InitProperties[0].vValue.vt     = VT_BSTR;  
        InitProperties[0].vValue.bstrVal=   
                                SysAllocString(L"C:\\MyDir");  
        InitProperties[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[0].colid         = DB_NULLID;  
  
        /*  
        Now that the properties are set, construct the DBPROPSET structure  
        (rgInitPropSet). The DBPROPSET structure is used to pass an array   
        of DBPROP structures (InitProperties) to the SetProperties method.  
        */  
        rgInitPropSet[0].guidPropertySet = DBPROPSET_SQLSERVERSTREAM;  
        rgInitPropSet[0].cProperties    = 1;  
        rgInitPropSet[0].rgProperties   = InitProperties;  
  
        // Set initialization properties.  
        hr = pICommandProperties->SetProperties(1, rgInitPropSet);   
        if(FAILED(hr))  
        {  
            cout << "Failed to set command properties.\n";  
        } // end if  
    } // End of InitializeAndEstablishConnection.  
  
    //--------------------------------------------------------------------  
    // Retrieve and display data resulting from a query.  
    void ProcessResultSet()  
    {  
       CHAR   szBuf[1000];  
       ULONG   ulNumRead;  
       HRESULT   hr;  
  
       if( pIXMLOutput == NULL )  
          return;  
  
       // Read from the stream.  
       ZeroMemory( szBuf, 1000 );  
       while( ( hr = pIXMLOutput->Read( szBuf, 1000, &ulNumRead ) ) == S_OK )  
       {  
          cout << szBuf;  
       }  
    } // Process resultset.  
    ```  
  
#### <a name="passing-parameters-to-templates"></a>Pasar parámetros a plantillas  
 En este ejemplo se muestra cómo se pueden pasar los valores de parámetro a comandos XML. Esta plantilla XML se especifica como un comando:  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:header><sql:param name='Title'>Mr.</sql:param></sql:header>  
<sql:query>SELECT TOP 20 * FROM Person.Contact  
WHERE Title = @Title  
FOR XML AUTO</sql:query>  
</ROOT>  
```  
  
 La plantilla incluye una consulta SQL. La consulta requiere un valor para el parámetro (@Title). Si no se pasa ningún valor de parámetro, se utiliza el valor predeterminado ("Mr.").  
  
 Al pasar valores de parámetro a una plantilla, se deben especificar tanto el nombre de parámetro como el valor.  
  
 Éste es el código:  
  
```  
#define UNICODE  
#define _UNICODE  
#define DBINITCONSTANTS  
#define INITGUID  
  
#include <stdio.h>  
#include <tchar.h>  
#include <stddef.h>  
#include <windows.h>  
#include <iostream.h>  
#include "oledb.h"  
#include "SQLOLEDB.h"  
  
HRESULT InitializeAndEstablishConnection(IDBInitialize ** ppIDBInitialize);  
HRESULT SetCommandProperties(ICommand * pICommand);  
HRESULT ProcessResultSet(ISequentialStream * pStreamOutput);  
  
//---------------------------------------------------------------------  
// Structure Definition Section  
//---------------------------------------------------------------------  
struct COLUMNDATA  
{  
    DBLENGTH    dwLength;   // The length of the data field  
    DBSTATUS    dwStatus;   // The status value  
    BYTE        bData[1];   // The start of the data field  
};  
  
class CSequentialStream : public ISequentialStream  
{  
    private:      
        ULONG       m_cRef;             // reference count  
        HANDLE      m_hFile;            // handle to the file  
        LPWSTR      m_wszFileName;      // the file name  
  
    public:  
        CSequentialStream( LPWSTR );  
        virtual ~CSequentialStream();  
  
        // IUnknown Methods  
        STDMETHODIMP_(ULONG)    AddRef();  
        STDMETHODIMP_(ULONG)    Release();  
        STDMETHODIMP QueryInterface( REFIID, LPVOID* );  
  
        // ISequentialStream Methods  
        STDMETHODIMP Read(   
                /* [out] */ void __RPC_FAR*,  
                /* [in]  */ ULONG,  
                /* [out] */ ULONG __RPC_FAR* );  
  
        STDMETHODIMP Write(   
                /* [in] */ const void __RPC_FAR*,  
                /* [in] */ ULONG,  
                /* [out]*/ ULONG __RPC_FAR* );  
};  
  
CSequentialStream::CSequentialStream  
(  
    LPWSTR      wszFileName  
)  
:  
    m_cRef( 0 ),  
    m_hFile( NULL ),  
    m_wszFileName( NULL )  
{  
    // The constructor AddRefs.  
    AddRef();  
  
    // Allocate memory for the file name.  
    m_wszFileName = (LPWSTR) CoTaskMemAlloc( ( wcslen( wszFileName ) + 1 ) * 2 );  
  
    // Copy the file name  
    wcscpy( m_wszFileName, wszFileName );  
}  
  
CSequentialStream::~CSequentialStream  
(  
)  
{  
    // Free any allocated memory.  
    if( m_wszFileName )  
        CoTaskMemFree( m_wszFileName );  
  
    // Close the file.  
    if( m_hFile )  
        CloseHandle( m_hFile );  
}  
  
ULONG      
CSequentialStream::AddRef  
(  
)  
{  
    return ++m_cRef;  
}  
ULONG CSequentialStream::Release()  
{  
    if(--m_cRef)  
        return m_cRef;  
  
    delete this;  
    return 0;  
}  
  
HRESULT CSequentialStream::QueryInterface  
(     
    REFIID riid,   
    void** ppv  
)  
{  
    *ppv = NULL;  
  
    if (riid == IID_IUnknown)  
        *ppv = this;  
  
    if (riid == IID_ISequentialStream)  
        *ppv = this;  
  
    if(*ppv)  
    {  
        ((IUnknown*)*ppv)->AddRef();  
        return S_OK;  
    }  
  
    return E_NOINTERFACE;  
}  
  
HRESULT CSequentialStream::Read  
(  
    void *pv,   
    ULONG cb,   
    ULONG* pcbRead  
)  
{  
    ULONG   cBytesRead = 0;  
  
    // Parameter checking.  
    if(pcbRead)  
        *pcbRead = 0;  
  
    if(!pv)  
        return STG_E_INVALIDPOINTER;  
  
    if(cb == 0)  
        return S_OK;  
  
    // Do we need to open the file?  
    if( m_hFile == NULL )  
    {  
        // Open the file.  
        m_hFile = CreateFile( m_wszFileName, GENERIC_READ, 0, NULL, OPEN_EXISTING, 0, NULL );  
  
        // If we failed to open the file, return E_FAIL.  
        if( m_hFile == INVALID_HANDLE_VALUE )  
            return E_FAIL;  
    }  
  
    // Clear the buffer.  
    ZeroMemory( pv, cb );  
  
    // Read cb bytes from the stream.  
    if( !ReadFile( m_hFile, pv, cb, &cBytesRead, NULL ) )  
        return E_FAIL;  
  
    // Inform the user how many bytes were read.  
    if( NULL != pcbRead )   
        *pcbRead = cBytesRead;  
  
    if(cb != cBytesRead)  
        return S_FALSE;   
  
    return S_OK;  
}  
  
HRESULT CSequentialStream::Write  
(  
    const void *pv,   
    ULONG cb,   
    ULONG* pcbWritten  
)  
{  
    // For purposes of this example, only a read-only stream is needed.  
    return STG_E_CANTSAVE;  
}  
void main()   
{  
    HRESULT                 hr = S_OK;  
    IDBInitialize         * pIDBInitialize          = NULL;  
    IDBCreateSession      * pIDBCreateSession       = NULL;  
    IDBCreateCommand      * pIDBCreateCommand       = NULL;  
    ICommand              * pICommand               = NULL;  
    ICommandStream        * pICommandStream         = NULL;  
    ICommandWithParameters* pICommandWithParameters = NULL;  
    ICommandText          * pICommandText           = NULL;  
    IAccessor             * pIAccessor              = NULL;  
    const ULONG             nParams = 1;  
    DBPARAMS              * pParams                 = NULL;  
    DBPARAMS                params;  
    DBBINDING               acDBBinding[nParams];  
    DBBINDSTATUS            acDBBindStatus[nParams];  
    DBORDINAL               rgParamOrdinals[1];  
    DBPARAMBINDINFO         rgParamBindInfo[1];  
    const WCHAR           * wszParamName =      L"@CategoryName";  
    const WCHAR           * wszDataSourceType = L"DBTYPE_WCHAR";  
    BYTE                    sprocparams[1000];  
    COLUMNDATA            * pCol = (COLUMNDATA *) sprocparams;  
    ISequentialStream     * pStreamOutput       = NULL;  
    DBCOLUMNINFO          * pDBColumnInfo       = NULL;  
    HACCESSOR               hAccessor;  
    CSequentialStream       XMLInput( L"TemplateFile.xml" );  
  
    typedef struct tagSPROCPARAMS  
    {  
        WCHAR CategoryName[25];  
    } SPROCPARAMS;  
  
    CoInitialize(0);  
  
    // Call a function to initialize and establish connection.   
    if (FAILED(hr = InitializeAndEstablishConnection(&pIDBInitialize)))  
        goto Cleanup;  
  
    //Create a session object.  
    if(FAILED(hr = pIDBInitialize->QueryInterface(  
                                IID_IDBCreateSession,  
                                (void**) &pIDBCreateSession)))  
    {  
        cout << "Failed to obtain IDBCreateSession interface.\n";  
        goto Cleanup;  
    }  
  
    if(FAILED(hr = pIDBCreateSession->CreateSession(  
                                     NULL,   
                                     IID_IDBCreateCommand,   
                                     (IUnknown**) &pIDBCreateCommand)))  
    {  
        cout << "pIDBCreateSession->CreateSession failed.\n";  
        goto Cleanup;  
    }  
  
    //Access the ICommand interface.  
    if(FAILED(hr = pIDBCreateCommand->CreateCommand(  
                                    NULL,   
                                    IID_ICommand,   
                                    (IUnknown**) &pICommand)))  
    {  
        cout << "Failed to access ICommand interface.\n";  
        goto Cleanup;  
    }  
  
    // Get an ICommandStream interface  
    if(FAILED(pICommand->QueryInterface( IID_ICommandStream, (void**) &pICommandStream)))  
    {  
        cout << "Failed to get an ICommandStream interface.\n";  
        goto Cleanup;  
    }  
  
    //Use SetCommandStream() to specify the command stream.  
    if(FAILED(hr = pICommandStream->SetCommandStream(IID_ISequentialStream, DBGUID_DEFAULT, (ISequentialStream*) &XMLInput )))  
    {  
        cout << "Failed to set command stream.\n";  
        goto Cleanup;  
    }  
  
    // Set the command properties.  
    if (FAILED(hr = SetCommandProperties(pICommand)))  
        goto Cleanup;  
  
    //***************************************  
    pCol->dwStatus = DBSTATUS_S_OK;  
    wcscpy( (LPWSTR) pCol->bData, L"Condiments" );  
    pCol->dwLength = wcslen( (LPWSTR) pCol->bData) * sizeof(WCHAR);  
  
    /*Describe the consumer buffer by filling in the array.   
    of DBBINDING structures.  Each binding associates  
    a single parameter to the consumer's buffer.*/  
    acDBBinding[0].iOrdinal     = 1;  
    acDBBinding[0].obLength     = offsetof( COLUMNDATA, dwLength );  
    acDBBinding[0].obStatus     = offsetof( COLUMNDATA, dwStatus );  
    acDBBinding[0].pTypeInfo    = NULL;  
    acDBBinding[0].pObject      = NULL;  
    acDBBinding[0].pBindExt     = NULL;  
    acDBBinding[0].dwPart       = DBPART_VALUE | DBPART_STATUS | DBPART_LENGTH;  
    acDBBinding[0].dwMemOwner   = DBMEMOWNER_CLIENTOWNED;  
    acDBBinding[0].dwFlags      = 0;  
    acDBBinding[0].bScale       = 0;  
    acDBBinding[0].obValue      = offsetof( COLUMNDATA, bData );  
    acDBBinding[0].eParamIO     = DBPARAMIO_INPUT;  
    acDBBinding[0].cbMaxLen     = 50;   
    acDBBinding[0].wType        = DBTYPE_WSTR;  
    acDBBinding[0].bPrecision   = 0;  
  
    rgParamOrdinals[0]              = 1;  
    rgParamBindInfo[0].bPrecision   = 0;  
    rgParamBindInfo[0].bScale       = 0;  
    rgParamBindInfo[0].dwFlags      = DBPARAMFLAGS_ISINPUT;  
    rgParamBindInfo[0].pwszDataSourceType = (WCHAR *)wszDataSourceType;  
    rgParamBindInfo[0].pwszName     = (WCHAR *)wszParamName;  
    rgParamBindInfo[0].ulParamSize  = 35;  
  
    if (FAILED(hr = pICommandStream->QueryInterface(  
                        IID_ICommandWithParameters,  
                        (LPVOID *)&pICommandWithParameters)))  
    {  
        cout << "Error.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pICommandWithParameters->SetParameterInfo(  
                        nParams,  
                        rgParamOrdinals,  
                        rgParamBindInfo)))  
    {  
        cout << "Error.\n";  
        goto Cleanup;  
    }  
  
    //Create an accessor from the above set of bindings.  
    if (FAILED(hr = pICommandStream->QueryInterface(  
                                    IID_IAccessor,   
                                    (void**)&pIAccessor)))  
    {  
        cout << "Failed to get IAccessor interface.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pIAccessor->CreateAccessor(  
                            DBACCESSOR_PARAMETERDATA,  
                            nParams,   
                            acDBBinding,   
                            sizeof(SPROCPARAMS),   
                            &hAccessor,  
                            acDBBindStatus)))  
    {  
        cout << "Failed to create accessor for the defined parameters.\n";  
        goto Cleanup;  
    }  
    /*  
    Fill in DBPARAMS structure for the command execution. This structure  
    specifies the parameter values in the command and is then passed   
    to Execute.  
    */  
    params.pData = sprocparams; //pCol->bData; //sprocparams;  
    params.cParamSets = 1;  
    params.hAccessor = hAccessor;  
  
    pParams = &params;  
  
    //***************************************  
    //Execute the command.  
    if(FAILED(hr = pICommand->Execute(NULL,   
                                    IID_ISequentialStream,   
                                    pParams,   
                                    NULL,   
                                    (IUnknown **) &pStreamOutput )))  
    {  
        cout << "Failed to execute command.\n";  
        goto Cleanup;  
    }  
  
    //Process the result set.  
    if (FAILED(hr = ProcessResultSet(pStreamOutput)))  
    {  
        goto Cleanup;  
    }  
  
Cleanup:  
    //Free up memory.  
    if( pStreamOutput )  
        pStreamOutput->Release();  
    if (pICommandStream)  
        pICommandStream->Release();  
    if (pICommand)  
        pICommand->Release();  
    if (pIDBCreateCommand)  
        pIDBCreateCommand->Release();  
    if (pIDBCreateSession)  
        pIDBCreateSession->Release();  
    if (pIDBInitialize)  
        pIDBInitialize->Release();  
  
    if (hr)  
    {  
        IErrorInfo* pErrorInfo = NULL;  
        BSTR        bstrDesc = NULL;  
        GetErrorInfo(0, &pErrorInfo);  
        if (pErrorInfo)  
        {  
            pErrorInfo->GetDescription(&bstrDesc);  
            printf ("\r\nError: %S\r\n", bstrDesc ? bstrDesc : L"Unknown error");  
            SysFreeString(bstrDesc);  
            pErrorInfo->Release();  
        }  
    }  
  
    //Release the COM library.  
    CoUninitialize();  
};  
  
//--------------------------------------------------------------------  
HRESULT InitializeAndEstablishConnection(IDBInitialize ** ppIDBInitialize)  
{  
    HRESULT         hr = S_OK;  
    IDBInitialize * pIDBInitialize = NULL;  
    IDBProperties * pIDBProperties = NULL;  
    DBPROP          rgIDBProps[4];  
    DBPROPSET       rgIDBPropSet[1];  
    int             ii;  
  
    if (!ppIDBInitialize)  
        return E_INVALIDARG;  
  
    *ppIDBInitialize = NULL;  
  
    /*  
    Initialize the property values needed   
    to establish the connection.  
    */  
    for(ii = 0; ii < 4; ii++)   
        VariantInit(&rgIDBProps[ii].vValue);  
  
    //Obtain access to the SQLOLEDB provider.  
    if(FAILED(hr = CoCreateInstance(CLSID_SQLOLEDB,   
                          NULL,   
                          CLSCTX_INPROC_SERVER,  
                          IID_IDBInitialize,   
                          (void **) &pIDBInitialize)))  
    {  
        printf("Failed to get IDBInitialize interface.\n");  
        goto Cleanup;  
    }  
  
    //Server name.  
    rgIDBProps[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
    rgIDBProps[0].vValue.vt     = VT_BSTR;  
    rgIDBProps[0].vValue.bstrVal= SysAllocString(L"server");  
    rgIDBProps[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[0].colid         = DB_NULLID;  
  
//Database.  
    rgIDBProps[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
    rgIDBProps[1].vValue.vt     = VT_BSTR;  
    rgIDBProps[1].vValue.bstrVal= SysAllocString(L"Northwind");  
    rgIDBProps[1].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[1].colid         = DB_NULLID;  
  
//User name (login).  
    rgIDBProps[2].dwPropertyID  = DBPROP_AUTH_USERID;   
    rgIDBProps[2].vValue.vt     = VT_BSTR;  
    rgIDBProps[2].vValue.bstrVal= SysAllocString(L"sa");  
    rgIDBProps[2].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[2].colid         = DB_NULLID;  
  
//Password.  
//    rgIDBProps[3].dwPropertyID  = DBPROP_AUTH_PASSWORD;   
//    rgIDBProps[3].vValue.vt     = VT_BSTR;  
//    rgIDBProps[3].vValue.bstrVal= SysAllocString(L"password");  
//    rgIDBProps[3].dwOptions     = DBPROPOPTIONS_REQUIRED;  
//    rgIDBProps[3].colid         = DB_NULLID;  
  
    /*  
    Now that the properties are set, construct the DBPROPSET structure  
    (rgInitPropSet). The DBPROPSET structure is used to pass an array   
    of DBPROP structures (rgIDBProps) to the SetProperties method.  
    */  
    rgIDBPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
//  rgInitPropSet[0].cProperties    = 4;  
    rgIDBPropSet[0].cProperties    = 3;  
    rgIDBPropSet[0].rgProperties   = rgIDBProps;  
  
    //Set initialization properties.  
    if (FAILED(hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                                   (void **)&pIDBProperties)))  
    {  
        cout << "Failed to get IDBProperties interface.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pIDBProperties->SetProperties(1, rgIDBPropSet)))  
    {  
        cout << "Failed to set initialization properties.\n";  
        goto Cleanup;  
    } //end if  
  
    //Now establish the connection to the data source.  
    if(FAILED(hr = pIDBInitialize->Initialize()))  
    {  
        cout << "Problem in establishing connection to the data source.\n";  
        goto Cleanup;  
    }  
  
    *ppIDBInitialize = pIDBInitialize;  
  
Cleanup:  
    for(ii = 0; ii < 4; ii++)   
        VariantClear(&rgIDBProps[ii].vValue);  
  
    if (pIDBProperties)  
        pIDBProperties->Release();  
    return hr;  
} //End of InitializeAndEstablishConnection.  
  
HRESULT SetCommandProperties(ICommand * pICommand)  
{  
    HRESULT     hr = S_OK;  
    DBPROP      rgProps[1];  
    DBPROPSET   rgPropSet[1];  
    ICommandProperties* pICommandProperties = NULL;  
  
    VariantInit(&rgProps[0].vValue);  
  
    //Server name.  
    rgProps[0].dwPropertyID  = SSPROP_STREAM_BASEPATH;  
    rgProps[0].vValue.vt     = VT_BSTR;  
    rgProps[0].vValue.bstrVal= SysAllocString(L"D:\\Test");  
    rgProps[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgProps[0].colid         = DB_NULLID;  
  
    /*  
    Now that the properties are set, construct the DBPROPSET structure  
    (rgInitPropSet). The DBPROPSET structure is used to pass an array   
    of DBPROP structures (rgProps) to the SetProperties method.  
    */  
    rgPropSet[0].guidPropertySet = DBPROPSET_SQLSERVERSTREAM;  
    rgPropSet[0].cProperties    = 1;  
    rgPropSet[0].rgProperties   = rgProps;  
  
    // Get an ICommandProperties interface.  
    if(FAILED(pICommand->QueryInterface( IID_ICommandProperties, (void**) &pICommandProperties)))  
    {  
        cout << "Failed to get an ICommandProperties interface.\n";  
        goto Cleanup;  
    }  
  
    //Set initialization properties.  
    if(FAILED(hr = pICommandProperties->SetProperties(1, rgPropSet)))  
    {  
        cout << "Failed to set command properties.\n";  
        goto Cleanup;  
    }  
Cleanup:  
    VariantClear(&rgProps[0].vValue);  
    if (pICommandProperties)  
        pICommandProperties->Release();  
    return hr;  
}  
  
//--------------------------------------------------------------------  
//Retrieve and display data resulting from a query.  
HRESULT ProcessResultSet(ISequentialStream * pStreamOutput)  
{  
    CHAR    szBuf[1000];  
    ULONG   ulNumRead;  
    HRESULT hr;  
  
    if( pStreamOutput == NULL )  
        return E_INVALIDARG;  
  
    // Read from the stream  
    ZeroMemory( szBuf, 1000 );  
    while( ( hr = pStreamOutput->Read( szBuf, 1000, &ulNumRead ) ) == S_OK )  
    {  
        cout << szBuf;  
        cout.flush();  
    }  
    return hr;  
} //ProcessResultSet.  
```  
  
  
