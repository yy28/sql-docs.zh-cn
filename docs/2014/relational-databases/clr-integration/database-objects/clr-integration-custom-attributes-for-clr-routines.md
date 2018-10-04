---
title: CLR 例程的自定义属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 54e8f172518d9e6513c1072d15debb32b2858d95
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158604"
---
# <a name="custom-attributes-for-clr-routines"></a>CLR 例程的自定义属性
  列出的特性可以应用于公共语言运行时 (CLR) 例程、 用户定义类型和用户定义的聚合中注册的[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]。 如果未应用此属性，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将采用默认值。 列出的属性在 `Microsoft.SqlServer.Server` 命名空间中定义。  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 属性  
 `SqlUserDefinedAggregate` 属性指示方法应注册为用户定义聚合。 必须使用此属性注释每个用户定义聚合。  
  
 有关详细信息，请参阅[SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 属性  
 `SqlFunction` 属性指示方法应注册为包含相应函数属性集的函数。  
  
 有关详细信息，请参阅[SqlFunctionAttribute](http://go.microsoft.com/fwlink/?LinkId=128019)。  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 属性  
 `SqlFacet` 属性用于返回有关用户定义类型 (UDT) 表达式的返回类型的信息。  
  
 有关详细信息，请参阅[SqlFacetAttribute](http://go.microsoft.com/fwlink/?LinkId=128020)。  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 属性  
 `SqlProcedure` 属性指示方法应注册为存储过程。 此属性仅由 Visual Studio 用于将指定的方法自动注册为存储过程；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不使用此属性。  
  
 有关详细信息，请参阅[SqlProcedureAttribute](http://go.microsoft.com/fwlink/?LinkId=128021)。  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 属性  
 `SqlTrigger` 属性指示方法应注册为触发器。  
  
 有关详细信息，请参阅[SqlTriggerContext](http://go.microsoft.com/fwlink/?LinkId=128022)并[SqlTriggerAttribute](http://go.microsoft.com/fwlink/?LinkId=203898)。  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 可将 SqlUserDefinedTypeAttribute 应用于程序集中的类定义。 此属性会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建绑定到具有此自定义属性的类定义的用户定义类型。  
  
 有关详细信息，请参阅[SqlUserDefinedTypeAttribute](http://go.microsoft.com/fwlink/?LinkId=128024)。  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 属性  
 `SqlMethod` 特性用于指示 UDT 的某方法或属性的确定性和数据访问属性。  
  
 有关详细信息，请参阅[SqlMethodAttribute](http://go.microsoft.com/fwlink/?LinkId=128025)。  
  
## <a name="see-also"></a>请参阅  
 [CLR 用户定义聚合](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 用户定义函数](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 用户定义类型](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 存储过程](../../../database-engine/dev-guide/clr-stored-procedures.md)   
 [CLR 触发器](../../../database-engine/dev-guide/clr-triggers.md)  
  
  
