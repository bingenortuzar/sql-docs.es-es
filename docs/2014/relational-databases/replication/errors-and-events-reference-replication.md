---
title: Referencia de errores y eventos (replicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], errors
- replication [SQL Server], troubleshooting
- errors [SQL Server replication]
- errors and events reference [SQL Server replication]
ms.assetid: e67d1bab-47b6-441d-ab9c-251a2ca499e1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f9323b5d28c0b41b56f4b6fb78c39d8bfacf0ba8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721321"
---
# <a name="errors-and-events-reference-replication"></a>Referencia de errores y eventos (replicación)
  Esta sección de la documentación contiene información sobre la causa y la resolución de una serie de errores relacionados con la replicación.  
  
|Error|de mensaje|  
|-----------|-------------|  
|[MSSQL_ENG002601](mssql-eng002601.md)|No se puede insertar una fila de claves duplicadas en el objeto "%.*ls" con índice único "%.\*ls".|  
|[MSSQL_ENG002627](mssql-eng002627.md)|Infracción de la restricción '%.*ls'. No se puede insertar una clave duplicada en el objeto "%.\*ls".|  
|[MSSQL_ENG003165](mssql-eng003165.md)|La base de datos '%ls' se restauró. Sin embargo, se encontró un error al restaurar o quitar la replicación. Se ha dejado la base de datos sin conexión. Vea el tema MSSQL_ENG003165 en los Libros en pantalla de SQL Server.|  
|[MSSQL_ENG003724](mssql-eng003724.md)|No se puede % S_MSG % S_MSG ' %. * ls' porque se está usando para la replicación.|  
|[MSSQL_ENG004929](mssql-eng004929.md)|No se puede modificar el % S_MSG ' %. * ls' porque se está publicando para replicación.|  
|MSSQL_ENG007395. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|No se puede iniciar una transacción anidada para el proveedor OLE DB "%ls" para el servidor vinculado "%ls". Era necesaria una transacción anidada porque la opción XACT_ABORT estaba establecida en OFF.|  
|[MSSQL_ENG014005](mssql-eng014005.md)|No se pudo quitar la publicación. Hay una suscripción para ella.|  
|[MSSQL_ENG014010](mssql-eng014010.md)|El servidor '%s' no está definido como servidor de suscripción.|  
|[MSSQL_ENG014114](mssql-eng014114.md)|%1!' no está configurado como distribuidor.|  
|[MSSQL_ENG014117](mssql-eng014117.md)|%1!' no está configurado como base de datos de distribución.|  
|[MSSQL_ENG014120](mssql-eng014120.md)|No se pudo quitar la base de datos de distribución '%s'. Esta base de datos está asociada a un publicador.|  
|[MSSQL_ENG014121](mssql-eng014121.md)|No se pudo quitar el distribuidor '%s'. Tiene asociadas bases de datos de distribución.|  
|[MSSQL_ENG014144](mssql-eng014144.md)|No se puede quitar el suscriptor '%s'. Mantiene suscripciones en la base de datos de publicación '%2!'.|  
|[MSSQL_ENG014150](mssql-eng014150.md)|Replicación-%s: el agente %s se ejecutó correctamente. %s|  
|[MSSQL_ENG014151](mssql-eng014151.md)|Replicación-%s: error en el agente %s. %s|  
|[MSSQL_ENG014152](mssql-eng014152.md)|Replicación-%s: el agente %s está programado para reintentar. %s|  
|[MSSQL_ENG014157](mssql-eng014157.md)|La suscripción creada por el suscriptor '%1!s!' a la publicación '%2!s!' expiró y ha sido eliminada.|  
|[MSSQL_ENG014160](mssql-eng014160.md)|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Han expirado una o más suscripciones a esta publicación.|  
|[MSSQL_ENG014161](mssql-eng014161.md)|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Asegúrese de que los agentes de registro del LOG y de distribución se están ejecutando y cumplen con el requisito de latencia.|  
|[MSSQL_ENG014162](mssql-eng014162.md)|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Asegúrese de que el agente de mezcla se está ejecutando y cumple con el requisito esperado.|  
|[MSSQL_ENG014163](mssql-eng014163.md)|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Asegúrese de que el agente de mezcla se está ejecutando y cumple con el requisito esperado.|  
|[MSSQL_ENG014164](mssql-eng014164.md)|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Asegúrese de que el agente de mezcla se está ejecutando y cumple con el requisito esperado.|  
|[MSSQL_ENG014165](mssql-eng014165.md)|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Asegúrese de que el agente de mezcla se está ejecutando y cumple con el requisito esperado.|  
|[MSSQL_ENG018456](mssql-eng018456.md)|Error de inicio de sesión del usuario "%.*ls".%.\*ls|  
|[MSSQL_ENG018752](mssql-eng018752.md)|El Agente de registro del LOG y los procedimientos relacionados con el registro (sp_repldone, sp_replcmds y sp_replshowcmds) solamente pueden conectarse a la base de datos de uno en uno. Si ejecutó un procedimiento relacionado con el registro, quite la conexión mediante la cual se ejecutó el procedimiento o ejecute sp_replflush en esa conexión antes de iniciar el Agente de registro del LOG o de ejecutar otro procedimiento relacionado con el registro.|  
|[MSSQL_ENG020554](mssql-eng020554.md)|El agente de replicación no ha registrado un mensaje de progreso en %ld minutos. Esto podría indicar que un agente no responde o una gran actividad en el sistema. Compruebe que se están replicando los registros en el destino y que las conexiones al suscriptor, publicador y distribuidor están activas.|  
|[MSSQL_ENG020557](mssql-eng020557.md)|Cierre del agente. Para obtener más información, vea el trabajo '%s' en el historial de trabajos del Agente SQL Server.|  
|[MSSQL_ENG020572](mssql-eng020572.md)|Se ha reinicializado la suscripción del suscriptor '%s' al artículo '%s' en la publicación '%s' porque no pasó la validación.|  
|[MSSQL_ENG020574](mssql-eng020574.md)|La suscripción del suscriptor '%s' al artículo '%s' en la publicación '%s' no pasó la validación de datos.|  
|[MSSQL_ENG020575](mssql-eng020575.md)|La suscripción del suscriptor '%s' al artículo '%s' en la publicación '%s' no pasó la validación de datos.|  
|[MSSQL_ENG020596](mssql-eng020596.md)|Solo '%1!' o los miembros de db_owner pueden quitar el agente anónimo.|  
|[MSSQL_ENG020598](mssql-eng020598.md)|No se encontró la fila en el suscriptor al aplicar el comando replicado.|  
|[MSSQL_ENG021075](mssql-eng021075.md)|La instantánea inicial de la publicación '%1!' aún no está disponible.|  
|[MSSQL_ENG021076](mssql-eng021076.md)|La instantánea inicial del artículo '%1!' aún no está disponible.|  
|[MSSQL_ENG021286](mssql-eng021286.md)|La tabla de conflictos '%1!' no existe.|  
|[MSSQL_ENG021330](mssql-eng021330.md)|No se pudo crear un subdirectorio bajo el directorio de trabajo de replicación.(%1!)|  
|[MSSQL_ENG021331](mssql-eng021331.md)|No se pudo copiar el archivo de script de usuario en el distribuidor.(%ls)|  
|[MSSQL_ENG021385](mssql-eng021385.md)|La instantánea no pudo procesar la publicación '%1!'. Puede deberse a un cambio de actividad de esquema activo o a la adición de nuevos artículos.|  
|MSSQL_ENG021617. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|No se pudo ejecutar SQL*PLUS. Compruebe que el código del cliente de Oracle instalado en el distribuidor corresponda a la versión actual.|  
|MSSQL_ENG021620. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|La versión de SQL*PLUS a la que se tiene acceso a través de la variable Path del sistema no es lo suficientemente actual para admitir publicaciones de Oracle. Compruebe que el código del cliente de Oracle instalado en el distribuidor corresponda a la versión actual.|  
|MSSQL_ENG021624. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|No se puede encontrar el proveedor OLEDB de Oracle registrado, OraOLEDB.Oracle, en el distribuidor '%s'. Compruebe que la versión del proveedor OLEDB de Oracle instalada y registrada en el distribuidor sea la actual.|  
|MSSQL_ENG021626. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|No se puede conectar con el servidor de base de datos Oracle '%s' mediante el proveedor OLEDB de Oracle, OraOLEDB.Oracle.|  
|MSSQL_ENG021627. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|No se puede conectar con el servidor de base de datos Oracle '%s' mediante el proveedor OLEDB de Microsoft, MSDAORA.|  
|MSSQL_ENG021628. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|No se puede actualizar el Registro del distribuidor '%s' para que el proveedor OLE DB de Oracle, OraOLEDB.Oracle, pueda ejecutarse con SQL Server. Compruebe que el inicio de sesión actual esté autorizado a modificar las claves del Registro propiedad de SQL Server.|  
|MSSQL_ENG021629. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|La clave del Registro CLSID que indica que el proveedor OLEDB de Oracle, OraOLEDB.Oracle, se ha registrado no está presente en el distribuidor. Compruebe que el proveedor OLEDB de Oracle se haya instalado y registrado en el distribuidor.|  
|MSSQL_ENG021642. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|Los publicadores heterogéneos requieren un servidor vinculado. Ya existe uno con el nombre '%1!s!'. Quítelo o elija otro nombre de publicador.|  
|MSSQL_ENG021663. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|No se encuentra ninguna clave principal válida para la tabla de origen [%s].[%s].|  
|MSSQL_ENG021684. Consulte [Troubleshooting Oracle Publishers](non-sql/troubleshooting-oracle-publishers.md).|Los permisos asociados con el inicio de sesión de administrador del publicador de Oracle '%s' no son suficientes.|  
|[MSSQL_ENG021797](mssql-eng021797.md)|'%s' debe ser un inicio de sesión de Windows válida en el formulario: "MACHINE\Login" o "DOMAIN\Login". Vea la documentación de '%s'.|  
|[MSSQL_ENG021798](mssql-eng021798.md)|Debe agregar el trabajo de agente '%s' a través de '%s' antes de continuar. Vea la documentación de '%s'.|  
|[MSSQL_REPL020011](mssql-repl020011.md)|El proceso no pudo ejecutar '%1' en '%2'.|  
|[MSSQL_REPL027056](mssql-repl027056.md)|El proceso de mezcla no pudo cambiar el historial de generación en '%1'. Para solucionar el problema, reinicie la sincronización con registro de historial detallado y especifique un archivo de salida para escribir en él.|  
|[MSSQL_REPL027183](mssql-repl027183.md)|El proceso de mezcla no pudo enumerar los cambios en los artículos con filtros de fila con parámetros. Si el error persiste, aumente el tiempo de espera de consulta, reduzca el período de retención de la publicación y mejore los índices en las tablas publicadas.|  
  
  
