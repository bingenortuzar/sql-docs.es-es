---
title: Puesta en modo inactivo de una topología de replicación (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- administering replication, quiescing
- quiesce [SQL Server replication]
- transactional replication, backup and restore
ms.assetid: 7626d575-9994-47be-b772-5b6f1b7ef7ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 59c179c81c1b6b60787603f5953b85e583668c80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63161720"
---
# <a name="quiesce-a-replication-topology-replication-transact-sql-programming"></a>Poner en modo inactivo una topología de replicación (programación de la replicación con Transact-SQL)
  *Detener* un sistema implica detener la actividad de las tablas publicadas en todos los nodos y asegurarse de que cada nodo ha recibido todos los cambios de los demás nodos. Este tema explica cómo detener una topología de replicación, una operación necesaria para varias tareas administrativas, y cómo asegurarse que un nodo ha recibido todos los cambios de otros nodos.  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-read-only-subscriptions"></a>Para detener una topología de replicación transaccional con suscripciones de solo lectura  
  
1.  Detenga la actividad en todas las tablas en el publicador.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_posttracertoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql).  
  
3.  En la base de datos de publicación del publicador, ejecute [sp_helptracertokenhistory](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql).  
  
4.  Asegúrese de que cada suscriptor ha recibido el token de seguimiento.  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-updatable-subscriptions"></a>Para detener una topología de replicación transaccional con suscripciones actualizables  
  
1.  Detenga la actividad en todas las tablas en el publicador y todos los suscriptores.  
  
2.  Si algún suscriptor utiliza suscripciones de actualización en cola:  
  
    1.  Si el Agente de lectura de cola no se está ejecutando de forma continua, ejecútelo. Para obtener más información sobre la ejecución de agentes, vea [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md) o [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    2.  Para comprobar que la cola está vacía, ejecute [sp_replqueuemonitor](/sql/relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql) en cada suscriptor.  
  
3.  En la base de datos de publicación del publicador, ejecute [sp_posttracertoken](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql).  
  
4.  En la base de datos de publicación del publicador, ejecute [sp_helptracertokenhistory](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql).  
  
5.  Asegúrese de que cada suscriptor ha recibido el token de seguimiento.  
  
### <a name="to-quiesce-a-peer-to-peer-transactional-replication-topology"></a>Para detener una topología de replicación transaccional punto a punto  
  
1.  Detenga la actividad en todas las tablas de todos los nodos.  
  
2.  Ejecute [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) en cada base de datos de publicación de la topología.  
  
3.  Si el Agente de registro del LOG o el Agente de distribución no se está ejecutando de forma continua, ejecútelo. El Agente de registro del LOG se debe iniciar antes del Agente de distribución. Para obtener más información sobre la ejecución de agentes, vea [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md) o [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
4.  Ejecute [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql) en cada base de datos de publicación de la topología. Asegúrese de que el conjunto de resultados contiene las respuestas de cada uno de los otros nodos.  
  
### <a name="to-ensure-a-peer-to-peer-node-has-received-all-prior-changes"></a>Para asegurarse de que un nodo punto a punto ha recibido todos los cambios anteriores  
  
1.  Ejecute [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) en la base de datos de publicación del nodo que está comprobando.  
  
2.  Si el Agente de registro del LOG o el Agente de distribución no se está ejecutando de forma continua, ejecútelo. El Agente de registro del LOG se debe iniciar antes del Agente de distribución. Para obtener más información sobre la ejecución de agentes, vea [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md) o [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Ejecute [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql) en la base de datos de publicación del nodo que está comprobando. Asegúrese de que el conjunto de resultados contiene las respuestas de cada uno de los otros nodos.  
  
### <a name="to-quiesce-a-merge-replication-topology"></a>Para detener una topología de replicación de mezcla  
  
1.  Detenga la actividad en todas las tablas en el publicador y en todos los suscriptores.  
  
2.  Ejecute el Agente de mezcla para cada suscripción dos veces: sincronice todas las suscripciones una vez y, a continuación, sincronice cada suscripción una segunda vez. Con esto se asegura de que todos los cambios se han replicado en todos los nodos. Para obtener más información sobre la ejecución de agentes, vea [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md) o [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  Si se producen conflictos durante la sincronización, es posible que los cambios requeridos por la resolución de conflictos no se propaguen a todos los nodos después de ejecutar el Agente de mezcla dos veces.  
  
## <a name="see-also"></a>Vea también  
 [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Medir la latencia y validar las conexiones de la replicación transaccional](../monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
