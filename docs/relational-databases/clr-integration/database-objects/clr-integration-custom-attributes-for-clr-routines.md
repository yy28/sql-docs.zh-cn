---
title: CLR 例程的自定义属性 |微软文档
description: 自定义属性可以应用于在 Microsoft SQL Server 中注册的 CLR 例程、用户定义的类型和用户定义的聚合。
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
ms.openlocfilehash: a32a606f73858ede15569d1ade891ad2ce1c69a5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487934"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR 例程的 CLR 集成自定义属性
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  列出的属性可以应用于在 中[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]注册的常见语言运行时 （CLR） 例程、用户定义的类型和用户定义的聚合。 如果未应用此属性，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将采用默认值。 列出的属性在**Microsoft.SqlServer.Server.Server**命名空间中定义。  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUser 定义的聚合属性  
 **SqlUser 定义聚合**属性指示该方法应注册为用户定义的聚合。 必须使用此属性注释每个用户定义聚合。  
  
 有关详细信息，请参阅[SqlUser 定义的聚合属性](https://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 属性  
 **SqlFunction**属性指示该方法应注册为函数，并设置相应的函数属性。  
  
 有关详细信息，请参阅[SqlFunction 属性](https://go.microsoft.com/fwlink/?LinkId=128019)。  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 属性  
 **SqlFacet**属性用于返回有关用户定义类型 （UDT） 表达式的返回类型的信息。  
  
 有关详细信息，请参阅[SqlFacet属性](https://go.microsoft.com/fwlink/?LinkId=128020)。  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 属性  
 **Sql程序**属性指示该方法应注册为存储过程。 此属性仅由 Visual Studio 用于将指定的方法自动注册为存储过程；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不使用此属性。  
  
 有关详细信息，请参阅[Sql程序属性](https://go.microsoft.com/fwlink/?LinkId=128021)。  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 属性  
 **SqlTrigger**属性指示该方法应注册为触发器。  
  
 有关详细信息，请参阅[SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022)和[SqlTrigger属性](https://go.microsoft.com/fwlink/?LinkId=203898)。  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 可将 SqlUserDefinedTypeAttribute 应用于程序集中的类定义。 此属性会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建绑定到具有此自定义属性的类定义的用户定义类型。  
  
 有关详细信息，请参阅[SqlUser 定义类型属性](https://go.microsoft.com/fwlink/?LinkId=128024)。  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 属性  
 **SqlMethod**属性用于指示方法或 UDT 上属性的确定性和数据访问属性。  
  
 有关详细信息，请参阅[SqlMethodattribute](https://go.microsoft.com/fwlink/?LinkId=128025)。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 用户定义的聚合](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 用户定义的函数](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 用户定义类型](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 存储过程](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [CLR 触发器](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
