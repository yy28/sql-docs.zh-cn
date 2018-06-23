---
title: CDC 控制任务自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2a073699-79a2-4ea1-a68e-fc17a80b74ba
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4a45fb326b728ae5df24f0ea91124d145d2c1761
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130174"
---
# <a name="cdc-control-task-custom-properties"></a>CDC 控制任务自定义属性
  下表描述了 CDC 控制任务的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|连接|ADO.NET 连接|与 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC 数据库的 ADO.NET 连接，用于访问更改表和 CDC 状态（如果存储于相同数据库中）。<br /><br /> 该连接必须是指向为 CDC 启用的并且所选更改表位于其中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接。|  
|TaskOperation|Integer（枚举）|CDC 控制任务的所选操作。 可能值为 **“标记初始加载开始”**、 **“标记初始加载结束”**、 **“标记 CDC 状态”**、 **“获取正在处理范围”**、 **“标记已处理范围”** 和 **“重置 CDC 状态”**。<br /><br /> 如果在 **CDC（即，不是 Oracle）上工作时选择**MarkCdcStart **、** MarkInitialLoadStart **或** MarkInitialLoadEnd [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则在连接管理器中指定的用户必须是  **db_owner** 或 **sysadmin**。<br /><br /> 有关这些操作的详细信息，请参阅 [CDC Control Task Editor](../cdc-control-task-editor.md) 和 [CDC Control Task](cdc-control-task.md)。|  
|OperationParameter|String|目前用于 **MarkCdcStart** 操作。 此参数允许特定操作所需的附加输入。 例如， **MarkCdcStart** 操作所需的 LSN 编号|  
|StateVariable|String|存储当前 CDC 上下文的 CDC 状态的 SSIS 包变量。 该 CDC 控制任务将状态读取和写入到 **StateVariable** ，并且不会加载它或将它存储到持久性存储区，除非选择了 **AutomaticStatePersistence** 。 请参阅 [定义状态变量](../data-flow/define-a-state-variable.md)。|  
|AutomaticStatePersistence|Boolean|该 CDC 控制任务从 CDC 状态包变量读取 CDC 状态。 执行某一操作后，该 CDC 控制任务将更新 CDC 状态包变量的值。 **AutomaticStatePersistence** 属性向 CDC 控制任务指出谁在两次运行 SSIS 包之间负责持久化 CDC 状态值。<br /><br /> 在此属性为 **true**时，该 CDC 控制任务自动从状态表加载 CDC 状态变量的值。 在该 CDC 控制任务更新 CDC 状态变量的值时，它还在相同的状态 **table.stores**中更新其值、在特殊表中更新该状态并且更新状态变量。 开发人员可以控制哪些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库包含该状态表及其名称。 此状态表的结构是预定义的。<br /><br /> 在为 **false**时，该 CDC 控制任务不持久化其值。 在为 true 时，该 CDC 控制任务在一个特殊的表中存储状态并更新 StateVariable。<br /><br /> 默认值是 **true**，指示会自动更新状态持久化。|  
|StateConnection|ADO.NET 连接|一个 ADO.NET 连接，它指向在使用 **AutomaticStatePersistence**时状态表驻留在其中的数据库。 默认值与 **“连接”** 的默认值相同。|  
|StateName|String|与持久状态关联的名称。 使用相同 CDC 上下文的完整负载和 CDC 包指定一个公共的 CDC 上下文名称。 此名称用于查找状态表中的状态行。<br /><br /> 此属性仅在 **AutomaticStatePersistence** 设置为 **true**时适用。|  
|StateTable|String|指定存储 CDC 上下文状态的表的名称。 使用为此组件配置的连接必须可以访问此表。 此表必须包含名为 **name** 和 **state**的 varchar 列。 （ **状态** 列必须具有至少 256 个字符）。<br /><br /> 此属性仅在 **AutomaticStatePersistence** 设置为 **true**时适用。|  
|CommandTimeout|integer|该值指定在与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库通信时要使用的超时值（秒）。 在来自数据库的响应时间非常慢并且默认值（30 秒）不足够时使用该值。|  
  
## <a name="see-also"></a>请参阅  
 [CDC 控制任务](cdc-control-task.md)   
 [CDC 控制任务编辑器](../cdc-control-task-editor.md)  
  
  