---
title: 'IRowsetFastLoad:: Commit (OLE DB) | Microsoft Docs'
description: IRowsetFastLoad::Commit (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d76ad5dc881ab4f31808d738d9beacd85929d279
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994409"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Marca el final de un lote de filas insertadas y escribe las filas en la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener ejemplos, consulte [copiar datos masiva con &#40;IRowsetFastLoad&#41; OLE DB](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) y [enviar datos de BLOB a SQL Server mediante IRowsetFastLoad &#40;e&#41;ISEQUENTIALSTREAM OLE DB](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fDone*[in]  
 Si es FALSE, el conjunto de filas mantiene la validez y el consumidor puede usarlo para una inserción de filas adicional. Si es TRUE, el conjunto de filas pierde su validez y el consumidor no puede realizar ninguna inserción más.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ejecutó correctamente y todos los datos insertados se escribieron en la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 E_FAIL  
 Se produjo un error específico del proveedor. Recupere la información de error para el texto de error específico del proveedor.  
  
 E_UNEXPECTED  
 Se ha llamado al método en un conjunto de filas de copia masiva previamente invalidado por el método **IRowsetFastLoad::Commit**.  
  
## <a name="remarks"></a>Notas  
 Un controlador de OLE DB para SQL Server conjunto de filas de copia masiva se comporta como un conjunto de filas del modo de actualización retrasada. A medida que el usuario inserta los datos de fila a través del conjunto de filas, las filas insertadas reciben el mismo trato que las inserciones pendientes en un conjunto de filas que admite **IRowsetUpdate**.  
  
 El consumidor debe llamar al método **Commit** en el conjunto de filas de copia masiva para escribir las filas insertadas en la tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del mismo modo en que se usa el método **IRowsetUpdate::Update** para enviar las filas pendientes a una instancia de SQL Server.  
  
 Si el consumidor libera su referencia en el conjunto de filas de copia masiva sin llamar al método **Commit**, se perderán todas las filas insertadas que no se hayan escrito previamente.  
  
 El consumidor puede procesar por lotes las filas insertadas mediante una llamada al método **Commit** con el argumento *fDone* establecido en FALSE. Cuando *fDone* se establece en TRUE, el conjunto de filas deja de ser válido. Un conjunto de filas de copia masiva que no es válido solo admite la interfaz **ISupportErrorInfo** y el método **IRowsetFastLoad::Release**.  
  
## <a name="see-also"></a>Consulte también  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
