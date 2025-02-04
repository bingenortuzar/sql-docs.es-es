---
title: ISSCommandWithParameters::SetParameterProperties (OLE DB) | Microsoft Docs
description: ISSCommandWithParameters::SetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b9f5a3251b05453d01b2ef984c6a9ea7bde1c115
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015390"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Establece las propiedades de los parámetros por cada parámetro por ordinal o establece las propiedades masivas de los parámetro especificando una matriz de estructuras SSPARAMPROPS.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argumentos  
 *cParams*[in]  
 El número de estructuras SSPARAMPROPS en la matriz *rgParamProperties*. Si este número es cero, **ISSCommandWithParameters::SetParameterProperties** eliminará todas las propiedades que se puedan haber especificado en cualquier parámetro del comando.  
  
 *rgParamProperties*[in]  
 Una matriz de estructuras SSPARAMPROPS que se van a establecer.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El método **ISSCommandWithParameters::SetParameterProperties** devuelve los mismos códigos de error que el método **ICommandProperties::SetProperties** de OLE DB básico.  
  
## <a name="remarks"></a>Notas  
 El establecimiento de propiedades de parámetro con este método se permite por parámetro y por ordinal, o bien mediante una única llamada a **ISSCommandWithParameters::SetParameterProperties** después de generar SSPARAMPROPS desde la matriz de propiedades.  
  
 Se debe llamar al método **SetParameterInfo** antes de llamar al método **ISSCommandWithParameters::SetParameterProperties**. La llamada a `SetParameterProperties(0, NULL)` borra todas las propiedades de parámetro especificadas, en tanto que la llamada a `SetParameterInfo(0,NULL,NULL)` borra toda la información de parámetros, incluidas las propiedades que puedan estar asociadas a un parámetro.  
  
 La llamada a **ISSCommandWithParameters::SetParameterProperties** para especificar propiedades de un parámetro que no es de tipo DBTYPE_XML o DBTYPE_UDT devuelve DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED y marca el campo *dwStatus* de todas las DBPROP incluidas en SSPARAMPROPS para ese parámetro con DBPROPSTATUS_NOTSET. Se debe recorrer la matriz DBPROP de cada DBPROPSET incluido en SSPARAMPROPS para detectar a qué parámetro hace referencia DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED.  
  
 Si se llama a **ISSCommandWithParameters::SetParameterProperties** para especificar las propiedades de parámetros cuya información de parámetro todavía no se ha establecido con **SetParameterInfo**, el proveedor devuelve E_UNEXPECTED con el siguiente mensaje de error:  
  
 No se puede llamar al método SetParameterProperties para los parámetros especificados sin llamar primero al método SetParameterInfo. La información de parámetro debe configurarse antes que las propiedades de parámetro.  
  
 Si la llamada a **ISSCommandWithParameters::SetParameterProperties** contiene algunos parámetros donde se ha establecido la información de parámetro y algunos parámetros donde no se ha establecido, las propiedades dwStatus en DBPROPSET del conjunto de propiedades SSPARAMPROPS devolverán DBSTATUS_NOTSET.  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Mejoras en el motor de base de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] datos a partir de allow ISSCommandWithParameters:: SetParameterProperties para obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por ISSCommandWithParameters:: SetParameterProperties [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]en versiones anteriores de. Para obtener más información, vea [Detección de metadatos](../../oledb/features/metadata-discovery.md).  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET de *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
  
## <a name="see-also"></a>Consulte también  
 [OLE DB &#40;ISSCommandWithParameters&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
