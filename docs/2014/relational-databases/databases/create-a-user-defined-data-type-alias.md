---
title: Creación de un alias de tipo de datos definido por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.userdefineddatatype.general.f1
- sql12.swb.new.datatype.properties.general.f1
helpviewer_keywords:
- alias data types [SQL Server], creating
ms.assetid: b1dd8413-0cd0-411b-a79b-1bb043ccc62d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b073e6025bc1483db2482a03d525b758d39efea4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917462"
---
# <a name="create-a-user-defined-data-type-alias"></a>Crear un alias de tipo de datos definido por el usuario
  En este tema se describe cómo crear un alias de tipo de datos definido por el usuario en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear un alias de tipo de datos definido por el usuario, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El nombre de un alias de tipo de datos definido por el usuario alias debe cumplir las reglas de los identificadores.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso CREATE TYPE en la base de datos actual y el permiso ALTER en *schema_name*. Si no se especifica *schema_name* , se aplican las reglas de resolución de nombres predeterminadas para determinar el esquema del usuario actual.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-user-defined-data-type"></a>Para crear un tipo de datos definido por el usuario  
  
1.  En el Explorador de objetos, expanda la opción **Bases de datos**, expanda una base de datos, expanda **Programación**y **Tipos**, haga clic con el botón derecho en **Tipos de datos definidos por el usuario**y haga clic en **Nuevo tipo de datos definido por el usuario**.  
  
     **Permitir valores NULL**  
     Especifique si el tipo de datos definido por el usuario puede aceptar valores NULL. La capacidad de admitir valores NULL de un tipo de datos existente definido por el usuario no puede modificarse.  
  
     **Data type**  
     Seleccione el tipo de datos base en el cuadro de lista. En el cuadro de lista se muestran todos los tipos de datos, excepto `geography`, `geometry`, `hierarchyid`, `sysname`, `timestamp` y `xml`. El tipo de un tipo de datos existente definido por el usuario no puede modificarse.  
  
     **Valor de DB-Library**  
     Opcionalmente, seleccione una regla o un valor predeterminado para enlazarlo al alias de tipo de datos definido por el usuario.  
  
     **Longitud/Precisión**  
     Muestra la longitud o la precisión del tipo de datos, según proceda. **Longitud** se aplica a los tipos de datos definidos por el usuario basados en personajes; **Precisión** solo se aplica a los tipos de datos numéricos definidos por el usuario. La etiqueta cambia en función del tipo de datos seleccionado con anterioridad. Este cuadro no puede modificarse si el tipo de datos seleccionado tiene una longitud o precisión fija.  
  
     La longitud no se muestra para los tipos de datos `nvarchar(max)`, `varchar(max)` o `varbinary(max)`.  
  
     **Name**  
     Si va a crear un nuevo alias de tipo de datos definido por el usuario, escriba un nombre único que se usará en la base de datos para representar el tipo de datos definido por el usuario. El número máximo de caracteres debe coincidir con el sistema `sysname` tipo de datos. El nombre de un alias existente de tipo de datos definido por el usuario no puede modificarse.  
  
     **Rule**  
     Opcionalmente, seleccione una regla para enlazarla al alias de tipo de datos definido por el usuario.  
  
     **Escala**  
     Especifique el número máximo de dígitos decimales que se pueden almacenar a la derecha del separador decimal.  
  
     **Esquema**  
     Seleccione un esquema de la lista de esquemas disponibles para el usuario actual. La selección predeterminada es el esquema predeterminado del usuario actual.  
  
     **Storage**  
     Muestra el tamaño de almacenamiento máximo del alias de tipo de datos definido por el usuario. El tamaño de almacenamiento máximo varía en función de la precisión.  
  
    |||  
    |-|-|  
    |1 - 9|5|  
    |10 - 19|9|  
    |20 - 28|13|  
    |29 - 38|17|  
  
     Para `nchar` y `nvarchar` tipos de datos, el valor de almacenamiento siempre es dos veces el valor de **longitud**.  
  
     El almacenamiento no se muestra para los tipos de datos `nvarchar(max)`, `varchar(max)` o `varbinary(max)`.  
  
2.  En el cuadro de diálogo **Nuevo tipo de datos definido por el usuario** , en el cuadro **Esquema** , escriba el esquema al que pertenecerá el alias de tipo de datos o use el botón Examinar para seleccionar el esquema.  
  
3.  En el cuadro **Nombre** , escriba un nombre para el nuevo alias de tipo de datos.  
  
4.  En el cuadro **Tipo de datos** , seleccione el tipo de datos en el que se basará el nuevo alias.  
  
5.  Rellene los cuadros **Longitud**, **Precisión**y **Escala** si corresponde para el tipo de datos que esté creando.  
  
6.  Active la casilla **Permitir valores NULL** si el nuevo alias de tipo de datos puede permitir valores NULL.  
  
7.  En el área **Enlace** , rellene los cuadros **Predeterminado** o **Regla** si desea enlazar un valor predeterminado o una regla al nuevo alias de tipo de datos. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]no pueden crearse valores predeterminados ni reglas. Utilice [!INCLUDE[tsql](../../includes/tsql-md.md)]. El Explorador de plantillas incluye códigos de ejemplo para crear valores predeterminados y reglas.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-user-defined-data-type-alias"></a>Para crear un alias de tipo de datos definido por el usuario  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo siguiente se crea un alias de tipo de datos basado en el tipo de datos `varchar` suministrado por el sistema. El alias de tipo de datos `ssn` se usa para las columnas que almacenan números de la seguridad social de 11 cifras (999-99-9999). La columna no puede ser NULL.  
  
```sql  
CREATE TYPE ssn  
FROM varchar(11) NOT NULL ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Identificadores de base de datos](database-identifiers.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql)  
  
  
