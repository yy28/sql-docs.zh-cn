---
title: CLR 用户定义的聚合要求 |微软文档
description: SQL Server CLR 集成允许您在托管代码中创建自定义聚合函数。 它们必须实现所需的聚合协定。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dd27cf3751400d3902ddd4199daee8aeef78b80
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487919"
---
# <a name="clr-user-defined-aggregates---requirements"></a>CLR 用户定义聚合 - 需求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  只要公共语言运行时 (CLR) 程序集中的类型实现了所需的聚合约定，就可以将它作为用户定义聚合函数注册。 此协定由**SqlUser 定义聚合**属性和聚合协定方法组成。 聚合协定包括保存聚合中间状态的机制，以及累积新值的机制，该机制包括四种方法 **：Init、****累积**、**合并**和**终止**。 满足这些要求后，您将能够充分利用 中的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户定义的聚合。 本主题的以下章节提供有关如何创建和使用用户定义聚合的其他详细信息。 例如，请参阅调用[CLR 用户定义的聚合函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)。  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 有关详细信息，请参阅[SqlUser 定义的聚合属性](https://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="aggregation-methods"></a>聚合方法  
 注册为用户定义聚合的类应支持以下实例方法。 这些是查询处理器计算聚合所用的方法。  
  
|方法|语法|说明|  
|------------|------------|-----------------|  
|**Init**|`public void Init();`|查询处理器使用此方法初始化聚合的计算。 对于查询处理器正在聚合的每个组调用此方法一次。 查询处理器可以选择重用聚合类的同一实例来计算多个组的聚合。 **Init**方法应根据需要执行此实例以前使用的任何清理，并使其能够重新启动新的聚合计算。|  
|**积累**|`public void Accumulate ( input-type value[, input-type value, ...]);`|表示该函数的参数的一个或多个参数。 *input_type*应是与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*input_sqltype*在**CREATE**聚合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语句中指定的本机数据类型等效的托管数据类型。 有关详细信息，请参阅映射[CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。<br /><br /> 对于用户定义类型 (UDT)，input-type 与 UDT 类型相同。 查询处理器使用此方法累计聚合值。 对于正在聚合的组中的每个值调用此方法一次。 查询处理器始终仅在在聚合类的给定实例上调用**Init**方法后才调用此方法。 此方法的实现应更新实例的状态以反映正在传递的参数值的累计。|  
|**合并**|`public void Merge( udagg_class value);`|此方法可以将此聚合的另一实例与当前实例合并。 查询处理器使用此方法合并聚合的多个部分计算。|  
|**终止**|`public return_type Terminate();`|此方法完成聚合计算并返回聚合的结果。 *return_type*应为托管[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型，该类型与**CREATE 聚合**语句中指定的*return_sqltype*的托管等效。 *return_type*也可以是用户定义的类型。|  
  
### <a name="table-valued-parameters"></a>表值参数  
 表值参数 (TVP) 即传递到某一过程或函数的用户定义表类型，它提供了一种将多行数据传递到服务器的高效方法。 TVP 提供与参数数组类似的功能，但灵活性更高并且与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成更紧密。 它们还提供提升性能的潜力。 TVP 还有助于减少到服务器的往返次数。 可以将数据作为 TVP 发送到服务器，而不是向服务器发送多个请求（例如，对于标量参数列表）。 用户定义表类型不能作为表值参数传递到在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数，也不能从这些存储过程或函数中返回。 而且，TVP 不能在上下文连接的作用域内使用。 但是，如果在非上下文连接中使用 TVP，则 TVP 可用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数中的 SqlClient。 该连接可以是对执行托管过程或函数的同一服务器的连接。 有关 TVP 的详细信息，请参阅[使用表值参数&#40;数据库引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
|更新了**累积**方法的说明;它现在接受多个参数。|  
  
## <a name="see-also"></a>另请参阅  
 [CLR 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [调用 CLR 用户定义聚合函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
  
  
