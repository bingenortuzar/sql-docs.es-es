---
title: Copia masiva desde variables de programa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], program variables
- bcp_bind function
- mapping data types [ODBC]
- SQL Server Native Client ODBC driver, bulk copy
- data types [ODBC], bulk copying
- ODBC, bulk copy operations
- program variables [ODBC]
ms.assetid: e4284a1b-7534-4b34-8488-b8d05ed67b8c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b58a6ae57d6a5f6b549a98f4a16871424615ae97
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708034"
---
# <a name="bulk-copying-from-program-variables"></a>Copia masiva de variables de programa
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Es posible realizar la copia masiva directamente desde variables de programa. Después de asignar variables para almacenar los datos de una fila y llamar a [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) para iniciar la copia masiva, llame a [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para que cada columna especifique la ubicación y el formato de la variable de programa que se va a asociar a la columna. Rellene cada variable con datos y, a continuación, llame a [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) para enviar una fila de datos al servidor. Repita el proceso de rellenar las variables y llamar a **bcp_sendrow** hasta que todas las filas se hayan enviado al servidor y, a continuación, llame a [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) para especificar que la operación se ha completado.  
  
 El parámetro_pdata_ de **bcp_bind**contiene la dirección de la variable que se va a enlazar a la columna. Los datos de cada columna pueden almacenarse de una de estas dos formas:  
  
-   Asignando una variable para almacenar los datos.  
  
-   Asignando una variable de indicador inmediatamente seguida de la variable de datos.  
  
 La variable de indicador indica la longitud de los datos para las columnas de longitud variable y también indica los valores NULL, si la columna permite valores NULL. Si solo se usa una variable de datos, la dirección de esta variable se almacena en el parámetro de_pdata_ de **bcp_bind**. Si se usa una variable de indicador, la dirección de la variable de indicador se almacena en el parámetro de_pdata_ de **bcp_bind**. Las funciones de copia masiva calculan la ubicación de la variable de datos mediante la adición de los parámetros de **bcp_bind**_cbIndicator_ y *pdata* .  
  
 **bcp_bind** admite tres métodos para trabajar con datos de longitud variable:  
  
-   Use *cbData* solo con una variable de datos. Coloque la longitud de los datos en *cbData*. Cada vez que cambie la longitud de los datos que se van a copiar de forma masiva, llame a [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)para restablecer *cbData*. Si se usa uno de los otros dos métodos, especifique SQL_VARLEN_DATA para *cbData*. Si todos los valores de datos que se proporcionan para una columna son NULL, especifique SQL_NULL_DATA para *cbData*.  
  
-   Usar variables de indicador. A medida que cada nuevo valor de datos se pase a la variable de datos, almacene la longitud del valor en la variable de indicador. Si se usa uno de los otros dos métodos, especifique 0 para *cbIndicator*.  
  
-   Usar punteros de terminador. Cargue el parámetro_pTerm_ de **bcp_bind**con la dirección del patrón de bits que finaliza los datos. Si se usa uno de los otros dos métodos, especifique NULL para *pTerm*.  
  
 Los tres métodos se pueden usar en la misma llamada de **bcp_bind** , en cuyo caso se usa la especificación que da como resultado la menor cantidad de datos que se van a copiar.  
  
 El parámetro de_tipo_ **bcp_bind**utiliza identificadores de tipo de datos de DB-Library, no identificadores de tipo de datos ODBC. Los identificadores de tipo de datos de DB-Library se definen en SQLNCLI. h para su uso con la función de ODBC **bcp_bind** .  
  
 Las funciones de copia masiva no admiten todos los tipos de datos C de ODBC. Por ejemplo, las funciones de copia masiva no admiten la estructura SQL_C_TYPE_TIMESTAMP de ODBC, por lo que debe usar [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) o [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para convertir los datos SQL_TYPE_TIMESTAMP de ODBC en una variable SQL_C_CHAR. Si después usa **bcp_bind** con un parámetro de *tipo* de SQLCHARACTER para enlazar la variable a una columna de **fecha y hora** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las funciones de copia masiva convierten la cláusula de escape de marca de tiempo de la variable de carácter en el formato de fecha y hora correcto.  
  
 En la tabla siguiente se muestran los tipos de datos que es recomendable usar en la asignación de un tipo de datos SQL de ODBC a un tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tipo de datos SQL de ODBC|Tipo de datos C de ODBC|parámetro de *tipo* bcp_bind|Tipo de datos de SQL Server|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**character**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **variar caracteres**<br /><br /> **char varying**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**texto**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT (con signo)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT (sin signo)|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT (con signo)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_SMALL_INT (sin signo)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER (con signo)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER (sin signo)|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**|  
|SQL_BIGINT (con signo y sin signo)|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binario**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **variables binarias**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**image**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tiene los tipos de datos **tinyint**, **smallint**sin signo o **int** sin signo. Para impedir la pérdida de valores de datos al migrar estos tipos de datos, cree la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el tipo de datos entero inmediatamente superior. Para impedir que los usuarios agreguen después valores que se encuentren fuera del intervalo permitido por el tipo de datos original, aplique una regla a la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para restringir los valores permitidos al intervalo admitido por el tipo de datos de origen inicial:  
  
```  
CREATE TABLE Sample_Ints(STinyIntCol   SMALLINT,  
USmallIntCol INT)  
GO  
CREATE RULE STinyInt_Rule  
AS   
@range >= -128 AND @range <= 127  
GO  
CREATE RULE USmallInt_Rule  
AS   
@range >= 0 AND @range <= 65535  
GO  
sp_bindrule STinyInt_Rule, 'Sample_Ints.STinyIntCol'  
GO  
sp_bindrule USmallInt_Rule, 'Sample_Ints.USmallIntCol'  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite directamente los tipos de datos interval. No obstante, una aplicación puede almacenar secuencias de escape interval como cadenas de caracteres en una columna de caracteres de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La aplicación puede leerlas para usarlas más tarde, pero no pueden usarse en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 Las funciones de copia masiva pueden utilizarse para cargar rápidamente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos leídos de un origen de datos ODBC. Use [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) para enlazar las columnas de un conjunto de resultados a las variables de programa y, a continuación, use **bcp_bind** para enlazar las mismas variables de programa a una operación de copia masiva. Al llamar a [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) o **SQLFetch** , se recupera una fila de datos del origen de datos ODBC en las variables de programa y, al llamar a [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) , se copian de forma masiva los datos de las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Una aplicación puede usar la función [bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) en cualquier momento que necesite cambiar la dirección de la variable de datos especificada originalmente en el parámetro _pdata_ de **bcp_bind** . Una aplicación puede usar la función [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) en cualquier momento que necesite cambiar la longitud de los datos especificados originalmente en el parámetro_cbData_ de **bcp_bind**.  
  
 No es posible leer datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en variables de programa utilizando la copia masiva; no existe una función como "bcp_readrow". Solo pueden enviarse datos de la aplicación al servidor.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones &#40;de copia masiva ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
