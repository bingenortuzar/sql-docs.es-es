---
title: sys.xml_schema_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 7b9ab66e0a25067440a496c6c5eb04b5d8b61e64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039281"
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por componente de un esquema XML. El par (**collection_id**, **namespace_id**) es una clave externa compuesta para el espacio de nombres contenedor. Para nombre componentes, los valores de **symbol_space**, **nombre**, **scoping_xml_component_id**, **is_qualified**,  **xml_namespace_id**, **xml_collection_id** son únicos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|Id. único del componente del esquema XML en la base de datos.|  
|**xml_collection_id**|**int**|Id. de la colección de esquemas XML que contiene el espacio de nombres de este componente.|  
|**xml_namespace_id**|**int**|Id. del espacio de nombres XML en la colección.|  
|**is_qualified**|**bit**|1 = Este componente tiene un espacio de nombres calificado explícito.<br /><br /> 0 = Es un componente de ámbito local. En este caso, el par de **namespace_id**, **collection_id**, hace referencia a la "ningún espacio de nombres" **targetNamespace**.<br /><br /> Para componentes comodín, este valor será 1.|  
|**name**|**nvarchar**<br /><br /> **(4000)**|Nombre único del componente del esquema XML. Es NULL si el componente no tiene nombre.|  
|**symbol_space**|**char(1)**|Espacio en el que este nombre simbólico es único, en función de **tipo**:<br /><br /> N = Ninguno<br /><br /> T = Tipo<br /><br /> E = Elemento<br /><br /> M = Grupo de modelos<br /><br /> A = Atributo<br /><br /> G = Grupo de atributos|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|Descripción del espacio en el que este nombre simbólico es único, en función de **tipo**:<br /><br /> Ninguno<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**Tipo**|**char(1)**|Tipo del componente del esquema XML.<br /><br /> N = Cualquier tipo (componente intrínseco especial)<br /><br /> Z = Cualquier tipo simple (componente intrínseco especial)<br /><br /> P = Tipo primitivo (tipos intrínsecos)<br /><br /> S = Tipo simple<br /><br /> L = Tipo de lista<br /><br /> U = Tipo de unión<br /><br /> C = Tipo simple complejo (derivado de simple)<br /><br /> K = Tipo complejo<br /><br /> E = Elemento<br /><br /> M = Grupo de modelos<br /><br /> W = Comodín de elementos<br /><br /> A = Atributo<br /><br /> G = Grupo de atributos<br /><br /> V = Comodín de atributos|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|Descripción del tipo de componente del esquema XML.<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**derivation**|**char(1)**|Método de derivación para tipos derivados:<br /><br /> N = Ninguno (no derivado)<br /><br /> X = Extensión<br /><br /> R = Restricción<br /><br /> S = Sustitución|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|Descripción del método de derivación para tipos derivados:<br /><br /> Ninguno<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|Id. del componente del que se deriva este componente. Es NULL si no hay ninguno.|  
|**scoping_xml_component_id**|**int**|Id. único del componente de alcance. Es NULL si no hay ninguno (espacio global).|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Los esquemas XML &#40;sistema de tipo XML&#41; vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
