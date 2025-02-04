---
title: Tipo de conexión Almacenamiento de datos paralelo de SQL Server (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 3925fd3d-2aa1-4768-96ad-cfc2c0ba9283
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b0c8ada8e10ef0f1bc47e1655521acced6f0aa41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106967"
---
# <a name="sql-server-parallel-data-warehouse-connection-type-ssrs"></a>Tipo de conexión Almacenamiento de datos paralelo de SQL Server (SSRS)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] es un dispositivo de almacenamiento de datos escalable que ofrece rendimiento y escalabilidad mediante un procesamiento paralelo masivo. [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] utiliza bases de datos de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] para el procesamiento distribuido y el almacenamiento de datos.  
  
 El dispositivo particiona tablas de base de datos grandes en varios nodos físicos, cada uno de los cuales ejecuta su propia instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Cuando un informe se conecta a [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] para recuperar datos de informes, se conecta al nodo de control que administra el procesamiento de consultas, en la [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] dispositivo. Una vez realizada la conexión, no hay ninguna diferencia entre trabajar con una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que esté o no en un [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] entorno.  
  
 Para incluir en el informe datos de [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] , debe tener un conjunto de datos que se base en un origen de datos de informe del tipo de Almacenamiento de datos paralelo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Este tipo de origen de datos integrado se basa en la extensión de datos de Almacenamiento de datos paralelo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Utilice este tipo de origen de datos para conectarse y recuperar datos de [!INCLUDE[ssDW](../../../includes/ssdw-md.md)].  
  
 Esta extensión de datos admite parámetros de varios valores, agregados del servidor y credenciales administrados con independencia de la cadena de conexión.  
  
 Para obtener más información, vea el sitio web relativo al [Almacenamiento de datos paralelo de SQL Server 2008 R2](https://go.microsoft.com/fwlink/?LinkId=150895).  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones detalladas, consulte [agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 Al conectarse a [!INCLUDE[ssDW](../../../includes/ssdw-md.md)], lo hace a un objeto de base de datos dentro de un dispositivo [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] . Especifique el objeto de base de datos que se va a usar en el diseñador de consultas. Si no especifica una base de datos en la cadena de conexión, puede conectar con la base de datos predeterminada que le asignó el administrador. Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En el siguiente ejemplo de cadena de conexión, se especifica la base de datos de ejemplo, **CustomerSales**, del dispositivo [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] :  
  
```  
HOST=<IP address>; database= CustomerSales; port=<port>  
```  
  
 Además, utilice el cuadro de diálogo **Propiedades de orígenes de datos** para proporcionar credenciales, como el nombre de usuario y la contraseña. Las opciones `User Id` y `Password` se anexan automáticamente a la cadena de conexión; no necesita escribirlos como parte de la cadena de conexión. La interfaz de usuario también proporciona opciones para especificar la dirección IP del nodo de control en el dispositivo [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] y el número de puerto. De forma predeterminada, el puerto es el 17000. El administrador puede configurar el puerto y su cadena de conexión puede utilizar un número de puerto diferente.  
  
 Para más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenciales  
 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] proporciona su propia tecnología de seguridad para implementar y almacenar nombres de usuario y contraseñas. No podrá utilizar la autenticación de Windows. Si intenta conectarse a [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] utilizando la autenticación de Windows, se producirá un error.  
  
 Las credenciales deben ser suficientes para tener acceso a la base de datos. En función de la consulta, podría necesitar otros permisos, como los permisos necesarios para tener acceso a las tablas y a las vistas. El propietario del origen de datos externo debe configurar credenciales que sean suficientes para proporcionar a los usuarios acceso de solo lectura a los objetos de base de datos que necesiten.  
  
 Desde un cliente de creación de informes, están disponibles las siguientes opciones para especificar las credenciales:  
  
-   Utilizar un nombre de usuario y una contraseña almacenados. Para negociar el salto doble que se produce cuando la base de datos que contiene los datos de informe es distinta del servidor de informes, seleccione opciones para utilizar las credenciales como credenciales de Windows. Puede también decidir suplantar al usuario autenticado tras la conexión al origen de datos.  
  
-   No se necesitan credenciales. Para usar esta opción, debe tener la cuenta de ejecución desatendida configurada en el servidor de informes. Para más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) en la [documentación de Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) en msdn.microsoft.com.  
  
 Para obtener más información, consulte [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [especificar credenciales en Generador de informes](../specify-credentials-in-report-builder.md).  

##  <a name="Query"></a> Consultas  
 Una consulta especifica qué datos se van a recuperar para un conjunto de datos de informe.  
  
 Las columnas del conjunto de resultados de una consulta rellenan la colección de campos de un conjunto de datos. Si la consulta devuelve varios conjuntos de resultados, el informe procesa solo el primer conjunto de resultados que una consulta recupera. De forma predeterminada, si crea una nueva consulta o abre una consulta existente que puede ser representada en el diseñador gráfico de consultas, este último está disponible. Puede especificar una consulta de varias maneras:  
  
-   Generar una consulta interactivamente. Utilice el diseñador de consultas relacionales que muestra una vista jerárquica de las tablas, las vistas y otros elementos de base de datos, organizada por esquema de la base de datos. Seleccione columnas de las tablas o de las vistas. Limite el número de filas de datos que se recuperarán especificando criterios de filtro, agrupación y agregados. Personalice el filtro al ejecutarse el informe estableciendo la opción de parámetro.  
  
-   Escriba o pegue una consulta. Use el diseñador de consultas basado en texto para escribir texto [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] directamente, para pegar texto de consulta de otro origen, para especificar consultas complejas que no se pueden generar con el diseñador de consultas relacionales o para escribir expresiones basadas en consultas.  
  
-   Importe una consulta existente de un archivo o informe. Utilice el botón de consulta **Importar** desde cualquier diseñador de consultas para buscar un archivo .sql o .rdl e importar una consulta.  
  
 Para más información, vea [Interfaz de usuario del Diseñador de consultas relacionales &#40;Generador de informes&#41;](relational-query-designer-user-interface-report-builder.md) e [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
 El diseñador de consultas basado en texto admite el modo [Texto](#QueryText) en el que el usuario escribe los comandos de [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] que seleccionan datos del origen de datos.  
  
-   [Texto](#QueryText)  
  
 Utilice [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] con [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] y [!INCLUDE[tsql](../../../includes/tsql-md.md)] con [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Los dos dialectos del lenguaje SQL son muy parecidos. Las consultas escritas para el tipo de conexión a un origen de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se pueden utilizar normalmente para el tipo de conexión a un origen de datos de [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] .  
  
 Una consulta que recupere datos de informe de una base de datos grande, por ejemplo un almacenamiento de datos como [!INCLUDE[ssDW](../../../includes/ssdw-md.md)], podría generar un conjunto de resultados con un número muy grande de filas a menos que se agreguen y resuman los datos para reducir el número de filas que la consulta devuelve. Puede escribir consultas que incluyan agregados y agrupaciones mediante el diseñador gráfico de consultas o el diseñador de consultas basado en texto.  
  
 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] admite la cláusula, la palabra clave y los agregados que el diseñador de consultas proporciona para resumir los datos.  
  
 El diseñador gráfico de consultas usado por [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] proporciona compatibilidad integrada con las agrupaciones y agregados para ayudar a los usuarios a escribir consultas que solo recuperen datos de resumen. Las características de lenguaje de [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] son: la cláusula GROUP BY, la palabra clave DISTINCT y agregados, como SUM y COUNT. El diseñador de consultas basado en texto es totalmente compatible con el lenguaje de [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] , incluidas las agrupaciones y los agregados.  
  
 Para más información sobre [!INCLUDE[tsql](../../../includes/tsql-md.md)], vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference) en los [Libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=141687) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en msdn.microsoft.com.  
  
###  <a name="QueryText"></a> Usar consultas de tipo Texto  
 En el diseñador de consultas basado en texto, escriba comandos de [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] para definir los datos de un conjunto de datos. Las consultas que se utilizan para recuperar datos de [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] son las mismas que las que se utilizan para recuperar datos de las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que no se están ejecutando dentro de una aplicación de [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] . Por ejemplo, la siguiente consulta [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] selecciona todos los nombres de todos los empleados que son asistentes de marketing:  
  
```  
SELECT  
  HumanResources.Employee.BusinessEntityID  
  ,HumanResources.Employee.JobTitle  
  ,Person.Person.FirstName  
  ,Person.Person.LastName  
FROM  
  Person.Person  
  INNER JOIN HumanResources.Employee  
    ON Person.Person.BusinessEntityID = HumanResources.Employee.BusinessEntityID  
WHERE HumanResources.Employee.JobTitle = 'Marketing Assistant'   
```  
  
 Haga clic en el botón **Ejecutar** ( **!** ) de la barra de herramientas para ejecutar la consulta y mostrar un conjunto de resultados.  
  
 Para parametrizar esta consulta, agregue un parámetro de consulta. Por ejemplo, modifique la cláusula WHERE con la siguiente información:  
  
 `WHERE HumanResources.Employee.JobTitle = (@JobTitle)`  
  
 Al ejecutar la consulta, se crean automáticamente parámetros de informe correspondientes a los parámetros de la consulta. Para obtener más información, vea [Parámetros de consulta](#Parameters) , más adelante en este tema.  

##  <a name="Parameters"></a> Parámetros  
 Cuando el texto de consulta contiene variables de consulta o procedimientos almacenados con parámetros de entrada, se generan automáticamente los correspondientes parámetros de consulta y parámetros de informe para el informe. El texto de consulta no debe incluir la instrucción DECLARE para cada variable de consulta.  
  
 Por ejemplo, la siguiente consulta SQL crea un parámetro de informe denominado `EmpID`:  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 De forma predeterminada, cada parámetro de informe tiene el tipo de datos Texto y un conjunto de datos creado automáticamente para proporcionar una lista desplegable de valores disponibles. Una vez creados los parámetros de informe, podría suceder que tenga que cambiar los valores predeterminados. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  

##  <a name="Remarks"></a> Comentarios  
  
###### <a name="platform-and-version-information"></a>Información de plataforma y de versión  
 Para obtener más información sobre la compatibilidad de plataformas y de versiones, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

##  <a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  

##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar elementos de informe relacionados con datos.  
  
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  

## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
