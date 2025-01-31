---
title: sp_describe_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor
- sp_describe_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor
ms.assetid: 0c836c99-1147-441e-998c-f0a30cd05275
author: stevestein
ms.author: sstein
ms.openlocfilehash: f82fc9006012d55902f1b5b3260dc7012fd6640a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053069"
---
# <a name="spdescribecursor-transact-sql"></a>sp_describe_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Notifica los atributos de un cursor de servidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_describe_cursor [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
    , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
    , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cursor_return=] *output_cursor_variable* salida  
 Es el nombre de una variable de cursor declarada que recibirá la salida del cursor. *output_cursor_variable* es **cursor**, no tiene ningún valor predeterminado y debe no ser asociada a ningún cursor en el momento en que se llama a sp_describe_cursor. El cursor devuelto es un cursor desplazable, dinámico y de solo lectura.  
  
 [ @cursor_source=] {N ' | N'global' | N'variable'}  
 Especifica si el cursor del que se informa está especificado con el nombre de un cursor local, un cursor global o una variable de cursor. El parámetro es **nvarchar (30)** .  
  
 [ @cursor_identity=] N'*local_cursor_name*']  
 Es el nombre de un cursor creado por una instrucción DECLARE CURSOR que tiene la palabra clave LOCAL u obtuvo el valor predeterminado LOCAL. *local_cursor_name* es **nvarchar (128)** .  
  
 [ @cursor_identity=] N'*global_cursor_name*']  
 Es el nombre de un cursor creado por una instrucción DECLARE CURSOR que tiene la palabra clave GLOBAL u obtuvo el valor predeterminado GLOBAL. *global_cursor_name* es **nvarchar (128)** .  
  
 *global_cursor_name* también puede ser el nombre de un cursor de servidor API que se abre una aplicación ODBC que, a continuación, se denomina mediante una llamada a SQLSetCursorName.  
  
 [ @cursor_identity=] N'*input_cursor_variable*']  
 Es el nombre de una variable de cursor asociada a un cursor abierto. *input_cursor_variable* es **nvarchar (128)** .  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="cursors-returned"></a>Cursores devueltos  
 sp_describe_cursor encapsula su conjunto de resultados en un [!INCLUDE[tsql](../../includes/tsql-md.md)] **cursor** parámetro de salida. De esta forma, los lotes, los procedimientos almacenados y los desencadenadores de [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden trabajar con la salida de fila en fila. También significa que no se puede llamar al procedimiento directamente desde funciones de una API de base de datos. El **cursor** parámetro de salida debe estar enlazado a una variable de programa, pero la API de base de datos no admiten el enlace **cursor** parámetros o variables.  
  
 En la siguiente tabla se muestra el formato del cursor devuelto por sp_describe_cursor. El formato del cursor es el mismo que el devuelto con sp_cursor_list.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|Nombre que se utiliza para hacer referencia al cursor. Si la referencia al cursor se realizó utilizando el nombre especificado en una instrucción DECLARE CURSOR, el nombre de referencia es el mismo que el nombre del cursor. Si la referencia al cursor se hizo utilizando una variable, el nombre de referencia es el de la variable.|  
|cursor_name|**sysname**|Nombre del cursor desde una instrucción DECLARE CURSOR. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si el cursor se creó estableciendo una variable de cursor como un cursor, cursor_name devuelve el nombre de la variable de cursor. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna de salida devuelve un nombre generado por el sistema.|  
|cursor_scope|**tinyint**|1 = LOCAL<br /><br /> 2 = GLOBAL|  
|status|**int**|Mismos valores que informó la función del sistema CURSOR_STATUS:<br /><br /> 1 = El cursor al que hace referencia el nombre del cursor o ?la variable está abierto. Si se trata de un cursor que no distingue, estático o de conjunto de claves, el conjunto de resultados tiene una fila, como mínimo. Si el cursor es dinámico, el conjunto de resultados tiene cero o más filas.<br /><br /> 0 = El cursor al que hace referencia el nombre del cursor o la variable está abierto pero no tiene filas. Los cursores dinámicos nunca devuelven este valor.<br /><br /> -1 = El cursor al que hace referencia el nombre del cursor o la variable está cerrado.<br /><br /> -2 = Se aplica solo a variables de cursor. No hay ningún cursor asignado a la variable. Posiblemente, un parámetro OUTPUT asignó un cursor a la variable pero el procedimiento almacenado cerró el cursor antes de devolver resultados.<br /><br /> -3 = No existe un cursor o variable de cursor con el nombre especificado, o la variable del cursor no tiene todavía un cursor asignado.|  
|model|**tinyint**|1 = Sin distinción (o estático)<br /><br /> 2 = conjunto de claves<br /><br /> 3 = dinámico<br /><br /> 4 = Avance rápido|  
|concurrency|**tinyint**|1 = solo lectura<br /><br /> 2 = Bloqueos de desplazamiento<br /><br /> 3 = Optimista|  
|scrollable|**tinyint**|0 = Solo avance<br /><br /> 1 = Desplazable|  
|open_status|**tinyint**|0 = Cerrado<br /><br /> 1 = Abierto|  
|cursor_rows|**decimal(10,0)**|Número de filas certificadas en el conjunto de resultados. Para más información, vea [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md).|  
|fetch_status|**smallint**|Estado de la última captura de este cursor. Para más información, vea [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md).<br /><br /> 0 = Captura correcta.<br /><br /> -1 = Error en la captura o se sobrepasaron los límites del cursor<br /><br /> -2 = Falta la fila solicitada.<br /><br /> -9 = No se registró ninguna captura en el cursor.|  
|column_count|**smallint**|Número de columnas del conjunto de resultados del cursor.|  
|row_count|**decimal(10,0)**|Número de filas afectadas por la última operación del cursor. Para más información, vea [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md).|  
|last_operation|**tinyint**|Última operación realizada en el cursor:<br /><br /> 0 = No se realizó ninguna operación en el cursor.<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = INSERCIÓN<br /><br /> 4 = UPDATE<br /><br /> 5 = DELETE<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|Valor único del cursor dentro del ámbito del servidor.|  
  
## <a name="remarks"></a>Comentarios  
 sp_describe_cursor describe los atributos globales de un cursor de servidor, como la posibilidad de desplazarlo y actualizarlo. Utilice sp_describe_cursor_columns para obtener una descripción de los atributos del conjunto de resultados devuelto por el cursor. Utilice sp_describe_cursor_tables para obtener un informe de las tablas base a las que hace referencia el cursor. Para obtener un informe de los cursores de servidor de [!INCLUDE[tsql](../../includes/tsql-md.md)] visibles en la conexión, use sp_cursor_list.  
  
 Una instrucción DECLARE CURSOR puede solicitar un tipo de cursor no compatible con la instrucción SELECT de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dentro de DECLARE CURSOR. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte implícitamente el cursor a un tipo compatible con la instrucción SELECT. Si se especifica TYPE_WARNING en la instrucción DECLARE CURSOR, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envía a la aplicación un mensaje informativo que indica que se ha completado una conversión. a continuación, se puede llamar a sp_describe_cursor para determinar el tipo de cursor que se ha implementado.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se abre un cursor global y se utiliza `sp_describe_cursor` para obtener un informe de los atributos del cursor.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR STATIC FOR  
SELECT LastName  
FROM Person.Person;  
  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor into the cursor variable.  
EXEC master.dbo.sp_describe_cursor @cursor_return = @Report OUTPUT,  
        @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Cursores](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [sp_describe_cursor_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
  
