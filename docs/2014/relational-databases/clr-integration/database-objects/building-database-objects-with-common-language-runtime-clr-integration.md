---
title: 通过公共语言运行时（CLR）集成生成数据库对象 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- database objects [CLR integration], building
- common language runtime [SQL Server], building database objects
- managed code [SQL Server], database objects
- building database objects [CLR integration]
- .NET Framework routines [SQL Server]
ms.assetid: ce34132c-bfa3-447b-9131-b6e17c672efe
author: rothja
ms.author: jroth
ms.openlocfilehash: dd5717b545913bd9e5ee98debe670a1af616fc61
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953573"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>使用公共语言运行时 (CLR) 集成生成数据库对象
  您可以使用生成数据库对象 [!INCLUDE[ssNoVersion](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，称为 "CLR 例程"。 这些例程包括：  
  
-   标量值用户定义函数（标量 UDF）  
  
-   表值用户定义函数 (TVF)  
  
-   用户定义的过程 (UDP)  
  
-   用户定义的触发器  
  
 CLR 例程在托管代码中具有相同的结构。 它们映射为某个类的公共静态（在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET 中共享）方法。 除了例程之外，还可以使用 .NET Framework 定义用户定义类型 (UDT) 和用户定义的聚合函数。 将 UDT 和用户定义聚合映射为整个 .NET Framework 类。  
  
 每种类型的 .NET Framework 例程都具有 [!INCLUDE[tsql](../../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)] 可使用等效的。 例如，标量 UDF 可以用于任意标量表达式中。 TVF 可以用于任意 FROM 子句中。 可以在 EXEC 语句中调用过程或从客户端应用程序调用。  
  
> [!NOTE]  
>  如果查询优化器确定这样做有益处，则在公共语言运行时上执行 CLR 对象（用户定义函数、用户定义类型或触发器）可能在多个线程上发生（并行计划）。 但是，如果用户定义函数访问数据，则会在串行计划上执行。 当在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 之前的服务器版本上执行时，如果某一用户定义函数包含 LOB 参数或返回值，则也必须在串行计划上执行。  
  
 下表列出了本节涵盖的主题。  
  
 [CLR 集成入门](getting-started-with-clr-integration.md)  
 简要概括使用 CLR 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 集成编译对象所需的库和命名空间。 提供一个“Hello World”CLR 存储过程示例。  
  
 [支持的 .NET Framework 库](supported-net-framework-libraries.md)  
 提供有关 CLR 集成支持的 .NET Framework 库的信息。  
  
 [CLR 集成编程模型限制](clr-integration-programming-model-restrictions.md)  
 提供有关 CLR 集成编程模型限制的信息。  
  
 [.NET Framework 中的 SQL Server 数据类型](../../clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型及其 .NET Framework 等效项的概览。  
  
 [CLR 集成自定义属性的概览](../../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)  
 提供有关 CLR 集成自定义属性的信息。  
  
 [CLR 用户定义函数](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 说明如何实现和使用各种类型的 CLR 函数：表值、标量和用户定义的聚合函数。  
  
 [CLR 用户定义类型](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 说明如何实现和使用 CLR 用户定义类型。  
  
 [CLR 存储过程](../../../database-engine/dev-guide/clr-stored-procedures.md)  
 说明如何实现和使用 CLR 存储过程。  
  
 [CLR 触发器](../../../database-engine/dev-guide/clr-triggers.md)  
 说明如何实现和使用 CLR 触发器。  
  
## <a name="see-also"></a>另请参阅  
 [公共语言运行时 &#40;CLR&#41; 集成概述](../common-language-runtime-integration-overview.md)  
  
  
