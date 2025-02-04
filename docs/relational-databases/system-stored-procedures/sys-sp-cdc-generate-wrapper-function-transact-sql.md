---
title: Sys.sp_cdc_generate_wrapper_function (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_generate_wrapper_function_TSQL
- sp_cdc_generate_wrapper_function
- sys.sp_cdc_generate_wrapper_function_TSQL
- sys.sp_cdc_generate_wrapper_function
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_generate_wrapper_function
- sp_cdc_generate_wrapper_function
ms.assetid: 85bc086d-8a4e-4949-a23b-bf53044b925c
author: rothja
ms.author: jroth
ms.openlocfilehash: 074e114f81db6615a04240f10447a3f711a51cf7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083752"
---
# <a name="sysspcdcgeneratewrapperfunction-transact-sql"></a>sys.sp_cdc_generate_wrapper_function (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera scripts para crear funciones de contenedor para las funciones de consulta de captura de datos modificados que están disponibles en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La API que se admite en los contenedores generados permite el intervalo de consulta que se especifican como un intervalo de fecha y hora. Esto hace que la función sea idónea para su uso en muchas aplicaciones de almacenamiento de datos, incluidas las que se desarrollan con diseñadores de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que utilizan la tecnología de captura de datos modificados para determinar la carga incremental.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_generate_wrapper_function  
    [ [ @capture_instance sysname = ] 'capture_instance'  
    [ , [ @closed_high_end_point = ] closed_high_end_pt  
    [ , [ @column_list = ] 'column_list'  
```  
  
```  
  
[ , [ @update_flag_list = ] 'update_flag_list'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @capture_instance=] '*capture_instance*'  
 Es la instancia de captura para la que se van a generar los scripts. *capture_instance* es **sysname** y tiene un valor predeterminado es null. Si se omite un valor o se establece explícitamente en NULL, los scripts de contenedor se generan para todas las instancias de captura  
  
 [ @closed_high_end_point=] *high_end_pt_flag*  
 Es el bit de marca que indica si el procedimiento generado incluirá dentro del intervalo de extracción los cambios que tengan una fecha y hora de confirmación igual al extremo superior. *high_end_pt_flag* es **bit** y tiene un valor predeterminado de 1, que indica que se debe incluir el punto de conexión. El valor 0 indica que todas las fechas y horas de confirmación serán estrictamente menores que el extremo superior.  
  
 [ @column_list=] '*column_list*'  
 Es una lista de las columnas capturadas que se van a incluir en el conjunto de resultados devuelto por la función de contenedor. *column_list* es **nvarchar (max)** y tiene un valor predeterminado es null. Cuando se especifica NULL, se incluyen todas las columnas capturadas.  
  
 [ @update_flag_list=] '*update_flag_list*'  
 Es una lista de las columnas incluidas para las que se incluye una marca de actualización en el conjunto de resultados devuelto por la función de contenedor. *update_flag_list* es **nvarchar (max)** y tiene un valor predeterminado es null. Cuando se especifica NULL, no se incluyen marcas de actualización.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de columna|Descripción|  
|-----------------|-----------------|-----------------|  
|**function_name**|**nvarchar(145)**|Nombre de la función generada.|  
|**create_script**|**nvarchar(max)**|Es el script que crea la función de contenedor de la instancia de captura.|  
  
## <a name="remarks"></a>Comentarios  
 El script que crea la función para contener la consulta de todos los cambios para una instancia de captura siempre se genera. Si la instancia de captura admite consultas de cambios de red, el script para generar un contenedor para esta consulta también se genera.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra cómo se puede utilizar `sys.sp_cdc_generate_wrapper_function` para crear contenedores para todas las funciones de captura de datos modificados.  
  
```  
DECLARE @wrapper_functions TABLE (  
    function_name sysname,  
    create_script nvarchar(max));  
  
INSERT INTO @wrapper_functions  
EXEC sys.sp_cdc_generate_wrapper_function;  
  
DECLARE @create_script nvarchar(max);  
DECLARE #hfunctions CURSOR LOCAL fast_forward  
FOR   
    SELECT create_script FROM @wrapper_functions;  
  
OPEN #hfunctions;  
FETCH #hfunctions INTO @create_script;  
WHILE (@@fetch_status <> -1)  
BEGIN  
    EXEC sp_executesql @create_script  
    FETCH #hfunctions INTO @create_script  
END;  
  
CLOSE #hfunctions;  
DEALLOCATE #hfunctions;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de captura de datos modificados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Captura de datos modificados &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)  
  
  
