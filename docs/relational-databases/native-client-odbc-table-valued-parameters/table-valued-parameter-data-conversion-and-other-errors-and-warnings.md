---
title: Los datos del parámetro con valores de tabla de conversión y otros errores y advertencias | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a4abc28204df04ec77ee6b22e3c7a0c08c832bcd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129147"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>Conversión de datos de parámetros con valores de tabla y otros errores y advertencias
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los valores de columna de parámetro con valores de tabla se pueden convertir entre tipos de cliente y de servidor de la misma manera que otros valores de parámetro y columna. Sin embargo, dado que un parámetro con valores de tabla puede contener varias columnas y filas, es importante poder identificar el valor real donde se produjo el error.  
  
 Cuando se detecta un error o una advertencia en una columna de parámetro con valores de tabla, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera un registro de diagnóstico. El mensaje de error contendrá el número de parámetro del parámetro con valores de tabla, más el ordinal de la columna y el número de fila. Una aplicación también puede utilizar los campos de diagnóstico SQL_DIAG_SS_TABLE_COLUMN_NUMBER y SQL_DIAG_SS_TABLE_ROW_NUMBER dentro de registros de diagnóstico para determinar qué valores están asociados a errores y advertencias. Estos campos de diagnóstico están disponibles en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.  
  
 Los componentes de mensaje y SQLSTATE de registros de diagnóstico cumplen los comportamientos de ODBC existentes en todos los demás aspectos. Es decir, excepto para el parámetro, fila e información de identificación de la columna, los mensajes de error tienen los mismos valores para parámetros con valores de tabla que tendrían para parámetros que no son valores de tabla.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
