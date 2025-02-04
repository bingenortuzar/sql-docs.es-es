---
title: Configuración del proyecto (asignación de tipo) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 4551181da22af1244f8083f6df5ea00f63e00e69
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266583"
---
# <a name="project-settings-type-mapping-oracletosql"></a>Configuración del proyecto (asignación de tipo) (OracleToSQL)
La página de asignación de tipos de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte tipos de datos de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.  
  
Está disponible en la página de asignación de tipos de la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Para especificar la configuración para todos los proyectos SSMA futuros, en el **herramientas** menú haga clic en **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que la configuración es necesaria para ver o cambiar de **Versión de destino de migración** lista desplegable y, a continuación, haga clic en **Type Mapping** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú haga clic en **configuración del proyecto**y, a continuación, haga clic en **Type Mapping** en la parte inferior del panel izquierdo.  
  
Para especificar la configuración para el objeto actual o la clase de objetos, utilice el **Type Mapping** pestaña en la ventana principal de SSMA.  
  
## <a name="options"></a>Opciones  
La tabla siguiente muestra la **Type Mapping** opciones de la pestaña:  
  
**Tipo de origen**  
El tipo de datos de Oracle asignado.  
  
**Tipo de destino**  
El destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos para el tipo de datos de Oracle especificado.  
  
Consulte las tablas en la sección siguiente para el valor predeterminado SSMA para asignaciones de tipos de Oracle.  
  
**Agregar**  
Haga clic para agregar un tipo de datos a la lista de asignación.  
  
**Editar**  
Haga clic para editar el tipo de datos seleccionado en la lista de asignación.  
  
**Quitar**  
Haga clic para quitar la asignación de tipos de datos seleccionados de la lista de asignación.  
  
**Valores predeterminados**  
Haga clic para restablecer la lista de asignación de tipo para los valores predeterminados SSMA.  
  
## <a name="default-type-mappings"></a>Asignaciones de tipos predeterminadas  
De SSMA para Oracle, puede establecer asignaciones de tipos personalizado para los argumentos, columnas, variables locales y los valores devueltos. La asignación predeterminada para los argumentos y tipos de valor devuelto es casi idéntica.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Tipo de argumento predeterminado y devolver la asignación de tipos de valor  
En la tabla siguiente contiene la asignación de tipo de datos predeterminada para los argumentos y valores devueltos.  
  
|Tipo de datos de Oracle|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_integer|int|  
|blob|varbinary(max)|  
|booleano|bit|  
|char|ntext|  
|char varying|ntext|  
|character|ntext|  
|character varying|ntext|  
|CLOB|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|decimal|float[53]|  
|double precision|float[53]|  
|float|float[53]|  
|int|int|  
|integer|int|  
|long|ntext|  
|long raw|varbinary(max)|  
|long raw [\*... 8000]<sup>*</sup>|varbinary [*]|  
|long raw [8001..\*]<sup>*</sup>|varbinary(max)|  
|carácter nacional|nvarchar(max)|  
|variable de Car. nacional|nvarchar(max)|  
|carácter nacional|nvarchar(max)|  
|national character varying de<sup>**</sup>|nvarchar(max)|  
|national character varying de<sup>*</sup>|nvarchar(max)|  
|nchar|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|número|float[53]|  
|numeric|float[53]|  
|NVARCHAR2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float[53]|  
|ROWID|uniqueidentifier|  
|Signtype|smallint|  
|smallint|smallint|  
|string|ntext|  
|timestamp|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|urowid|uniqueidentifier|  
|varchar|ntext|  
|varchar2|ntext|  
|xmltype|xml|  
  
<sup>*</sup> Se aplica para devolver el valor de tipo asignación solo.  
  
<sup>**</sup> Se aplica al argumento de tipo asignación solo.  
  
### <a name="default-column-type-mapping"></a>Asignación de tipos de columna predeterminados  
En la tabla siguiente contiene la asignación de tipo de valor predeterminado para las columnas.  
  
|Tipo de datos de Oracle|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|blob|varbinary(max)|  
|char|char|  
|char varying [*.. \*]|varchar [*]|  
|Char [*.. \*]|Char [*]|  
|character|char|  
|variable de carácter [*.. \*]|varchar [*]|  
|caracteres [*.. \*]|Char [*]|  
|CLOB|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|DEC [*.. \*]|DEC [*] [0]|  
|DEC [*.. \*][\*.. \*]|DEC [*] [\*]|  
|decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal [*.. \*][\*.. \*]|decimal [*] [\*]|  
|double precision|float[53]|  
|float|float[53]|  
|float [*.. 53]|float [*]|  
|float [54.. *]|float[53]|  
|int|int|  
|integer|int|  
|long|ntext|  
|long raw|varbinary(max)|  
|long raw [*.. 8000]|varbinary [*]|  
|long raw [8001.. *]|varbinary(max)|  
|long varchar|ntext|  
|long[*..8000]|varchar [*]|  
|long[8001..*]|ntext|  
|carácter nacional|nchar|  
|National char varying [*.. \*]|nvarchar [*]|  
|carácter nacional [*.. \*]|nchar [*]|  
|carácter nacional|nchar|  
|national character varying de [*.. \*]|nvarchar [*]|  
|carácter nacional [*.. \*]|nchar [*]|  
|nchar|nchar|  
|nchar [*]|nchar [*]|  
|NCLOB|nvarchar(max)|  
|número|float[53]|  
|número [*.. \*]|numérico [*]|  
|número [*.. \*][\*.. \*]|numérico [*] [\*]|  
|numeric|numeric|  
|numérico [*.. \*]|numérico [*]|  
|numérico [*.. \*][\*.. \*]|numérico [*] [\*]|  
|NVARCHAR2 [*.. \*]|nvarchar [*]|  
|sin formato [*.. \*]|varbinary [*]|  
|real|float[53]|  
|ROWID|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria local [*.. \*]|DateTimeOffset [*]|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|marca de tiempo con la zona horaria [*.. \*]|DateTimeOffset [*]|  
|timestamp[*..\*]|datetime2 [*]|  
|urowid|uniqueidentifier|  
|urowid [*.. \*]|uniqueidentifier|  
|varchar [*.. \*]|varchar [*]|  
|VARCHAR2 [*.. \*]|varchar [*]|  
|tipo XML|xml|  
  
### <a name="default-local-variable-type-mapping"></a>Asignación de tipo de Variable Local predeterminada  
En la tabla siguiente contiene la asignación de tipo de valor predeterminado para las variables locales.  
  
|Tipo de datos de Oracle|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|char varying [*.. 8000]|varchar [*]|  
|char varying [8001.. *]|ntext|  
|char[*..8000]|Char [*]|  
|char[8001..*]|ntext|  
|Carácter|char|  
|variable de carácter [*.. 8000]|varchar [*]|  
|variable de carácter [8001.. *]|ntext|  
|character[*..8000]|Char [*]|  
|caracteres [8001.. *]|ntext|  
|CLOB|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|DEC [*.. \*]|DEC [*] [0]|  
|DEC [*.. \*][\*.. \*]|DEC [*] [\*]|  
|decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal [*.. \*][\*.. \*]|decimal [*] [\*]|  
|double precision|float[53]|  
|Float|float[53]|  
|float [*.. 53]|float [*]|  
|float [54.. *]|float[53]|  
|Int|int|  
|Entero|int|  
|entero [*.. \*]|numérico [*] [0]|  
|long|ntext|  
|long raw|varbinary(max)|  
|long raw [*.. 8000]|varbinary [*]|  
|long raw [8001.. *]|varbinary(max)|  
|carácter nacional|nchar|  
|National char varying [*.. 4000]|nvarchar [*]|  
|National char varying [4001.. *]|nvarchar(max)|  
|carácter nacional [*.. 4000]|nchar [*]|  
|carácter nacional [4001.. *]|nvarchar(max)|  
|carácter nacional|nchar|  
|carácter nacional [*.. 4000]|nvarchar [*]|  
|carácter nacional [4001.. *]|nvarchar(max)|  
|national character varying de [*.. 4000]|nvarchar [*]|  
|national character varying de [4001.. *]|nvarchar(max)|  
|Nchar|nchar|  
|nchar[*..4000]|nchar [*]|  
|nchar[4001..*]|nvarchar(max)|  
|nchar varying [*.. 4000]|nvarchar [*]|  
|nchar varying [4001.. *]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float[53]|  
|número [*.. \*]|numérico [*]|  
|número [*.. \*][\*.. \*]|numérico [*] [\*]|  
|Numeric|numérico [38] [0]|  
|numérico [*.. \*]|numérico [*]|  
|numérico [*.. \*][\*.. \*]|numérico [*] [\*]|  
|nvarchar2[*..4000]|nvarchar [*]|  
|nvarchar2[4001..*]|nvarchar(max)|  
|pls_integer|int|  
|raw[*..8000]|varbinary [*]|  
|sin formato [8001.. *]|varbinary(max)|  
|Real|float[53]|  
|Rowid|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|string[*..8000]|varchar [*]|  
|string[8001..*]|ntext|  
|timestamp|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|marca de tiempo con la zona horaria local [*.. \*]|DateTimeOffset [*]|  
|marca de tiempo con la zona horaria [*.. \*]|DateTimeOffset [*]|  
|timestamp[*..\*]|datetime2 [*]|  
|urowid|uniqueidentifier|  
|urowid [*.. \*]|uniqueidentifier|  
|varchar[*..8000]|varchar [*]|  
|varchar [8001.. *]|ntext|  
|varchar2[*..8000]|varchar [*]|  
|varchar2[8001..*]|varcha(max)|  
|tipo XML|xml|  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
