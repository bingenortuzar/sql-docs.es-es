---
title: Atributos personalizados para las rutinas CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
ms.openlocfilehash: f1ff346abc41ee4589a8d0b2193b167fb2cf24e0
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212376"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Atributos personalizados de integración CLR para las rutinas CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Los atributos enumerados se pueden aplicar a rutinas Common Language Runtime (CLR), tipos definidos por el usuario y agregados definidos por el usuario que estén [!INCLUDE[msCoName](../../../includes/msconame-md.md)] registrados en. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Si no se aplica el atributo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asume el valor predeterminado. Los atributos enumerados se definen en el espacio de nombres **Microsoft. SqlServer. Server** .  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Atributo SqlUserDefinedAggregate  
 El atributo **SqlUserDefinedAggregate** indica que el método debe registrarse como un agregado definido por el usuario. Los agregados definidos por el usuario deben anotarse con este atributo.  
  
 Para obtener más información, vea [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Atributo SqlFunction  
 El atributo **SqlFunction** indica que el método debe registrarse como una función, con el conjunto de atributos de función adecuado.  
  
 Para obtener más información, vea [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Atributo SqlFacet  
 El atributo **SqlFacet** se usa para devolver información sobre el tipo de valor devuelto de una expresión de tipo definido por el usuario (UDT).  
  
 Para obtener más información, vea [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Atributo SqlProcedure  
 El atributo **SqlProcedure** indica que el método debe registrarse como un procedimiento almacenado. Solamente Visual Studio usa este atributo para registrar automáticamente el método especificado como un procedimiento almacenado; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no lo usa.  
  
 Para obtener más información, vea [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Atributo SqlTrigger  
 El atributo **SqlTrigger** indica que el método debe registrarse como desencadenador.  
  
 Para obtener más información, vea [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022) y [SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Atributo SqlUserDefinedTypeAttribute  
 Puede aplicar el atributo SqlUserDefinedTypeAttribute a una definición de clase en el ensamblado. Esto hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cree un tipo definido por el usuario que se enlaza a la definición de clase que tiene este atributo personalizado.  
  
 Para obtener más información, vea [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Atributo SqlMethod  
 El atributo **SqlMethod** se usa para indicar el determinismo y las propiedades de acceso a datos de un método o una propiedad en un UDT.  
  
 Para obtener más información, vea [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Vea también  
 [Agregados definidos por el usuario CLR](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR User-Defined Functions](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  (Funciones definidas por el usuario CLR)  
 [Tipos definidos por el usuario CLR](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Procedimientos almacenados CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Desencadenadores CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
