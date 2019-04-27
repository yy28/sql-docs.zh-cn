---
title: Integration Services 容器 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS containers
- containers [Integration Services]
- containers [Integration Services], about containers
- control flow [Integration Services], containers
- SQL Server Integration Services containers
ms.assetid: 1b725922-ec59-4a47-9d55-e079463058f3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 172aa2a77293dd7e9a9ee50bfe0002a71c59cbb9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831255"
---
# <a name="integration-services-containers"></a>Integration Services 容器
  容器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中为包提供结构和为任务提供服务的对象。 它们支持包中的重复控制流，并且将任务和容器分组为有意义的工作单元。 除了任务，容器还可以包含其他容器。  
  
 包将容器用于下列用途：  
  
-   重复执行集合中每个元素的任务，这些元素包括文件夹中的文件、架构或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) 对象等。 例如，包可以运行驻留在多个文件中的 Transact-SQL 语句。  
  
-   重复执行任务，直到指定表达式的求值结果为 `false` 为止。 例如，包可以一周七次，每天一次地发送一封不同的电子邮件。  
  
-   将必须作为一个单元成功或失败的任务和容器分组到一起。 例如，包可以将在数据库表中删除和添加行的任务分组到一起，然后当其中一个任务失败时提交或回滚所有任务。  
  
## <a name="container-types"></a>容器类型  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供四种用于生成包的容器。 下表列出了容器类型。  
  
|容器|Description|  
|---------------|-----------------|  
|[Foreach 循环容器](foreach-loop-container.md)|通过使用枚举器重复运行控制流。|  
|[For 循环容器](for-loop-container.md)|通过测试某个条件重复运行控制流。|  
|[序列容器](sequence-container.md)|将任务和容器分组到那些作为包控制流子集的控制流中。|  
|[任务宿主容器](task-host-container.md)|为单个任务提供服务。|  
  
 包和事件处理程序也是容器类型。 有关详细信息，请参阅 [Integration Services (SSIS) 包](../integration-services-ssis-packages.md)和 [Integration Services (SSIS) 事件处理程序](../integration-services-ssis-event-handlers.md)。  
  
### <a name="summary-of-container-properties"></a>容器属性摘要  
 通常，所有容量类型都有一组属性。 如果使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的图形工具创建包，“属性”窗口将列出 Foreach 循环容器、For 循环容器和序列容器的以下属性。 配置任务宿主容器属性是配置任务宿主容器所封装的任务的一部分。 配置任务时需要设置任务宿主属性。  
  
|属性|Description|  
|--------------|-----------------|  
|`DelayValidation`|指示是否将容器的验证推迟到运行时进行的布尔值。 此属性的默认值为 `False`。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.DelayValidation%2A> 。|  
|`Description`|容器说明。 该属性包含一个字符串，但可以为空。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Description%2A> 。|  
|`Disable`|指示容器是否运行的布尔值。 此属性的默认值为 `False`。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Disable%2A> 。|  
|`DisableEventHandlers`|指示与容器关联的事件处理程序是否运行的布尔值。 此属性的默认值为 `False`。|  
|`FailPackageOnFailure`|指定如果容器中出现错误包是否失败的布尔值。 此属性的默认值为 `False`。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailPackageOnFailure%2A> 。|  
|`FailParentOnFailure`|指定如果容器中出现错误父容器是否失败的布尔值。 此属性的默认值为 `False`。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailParentOnFailure%2A> 。|  
|`ForcedExecutionValue`|如果 `ForceExecutionValue` 设置为 `True`，则为包含容器的可选执行值的对象。 此属性的默认值为 **0**。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForcedExecutionValue%2A> 。|  
|`ForcedExecutionValueType`|`ForcedExecutionValue` 的数据类型。 此属性的默认值为 `Int32`。|  
|`ForceExecutionResult`|指定运行包或容器的强制结果的值。 其值为：`None`、`Success`、`Failure` 和 `Completion`。 此属性的默认值为 `None`。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionResult%2A> 。|  
|`ForceExecutionValue`|指定容器的可选执行值是否应强制包含特定值的布尔值。 此属性的默认值为 `False`。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionValue%2A> 。|  
|`ID`|容器 GUID，该属性是在创建包时分配的。 该属性为只读。<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ID%2A> 的用户。|  
|`IsolationLevel`|容器事务的隔离级别。 其值为：`Unspecified`、`Chaos`、`ReadUncommitted`、`ReadCommitted`、`RepeatableRead`、`Serializable` 和 `Snapshot`。 此属性的默认值为 `Serializable`。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A> 。|  
|`LocaleID`|Microsoft Win32 区域设置。 此属性的默认值为本地计算机上操作系统的区域设置。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LocaleID%2A> 。|  
|`LoggingMode`|指定容器日志记录行为的值。 具体的值为 `Disabled`、`Enabled` 和 `UseParentSetting`。 此属性的默认值为 `UseParentSetting`。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode> 。|  
|`MaximumErrorCount`|容器停止运行前可以出现的最大错误数。 此属性的默认值为 **1**。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.MaximumErrorCount%2A> 。|  
|`Name`|容器的名称。<br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Name%2A> 。|  
|`TransactionOption`|容器的事务参与情况。 其值为：`NotSupported`、`Supported`、`Required`。 此属性的默认值为 `Supported`。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption> 。|  
  
 在以编程方式配置 Foreach 循环容器、For 循环容器、序列容器和任务宿主容器时，若要了解可用于这些容器的所有属性，请参阅以下 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] API 主题：  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForEachLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.Sequence  
  
-   T:Microsoft.SqlServer.Dts.Runtime.TaskHost  
  
## <a name="objects-that-extend-container-functionality"></a>扩展容器功能的对象  
 容器包括由可执行文件和优先约束组成的控制流，并且可能使用事件处理程序和变量。 任务宿主容器是个例外：因为任务宿主容器封装单个任务，所以它不使用优先约束。  
  
### <a name="executables"></a>可执行文件  
 可执行文件指容器级别的任务和该容器内的任意容器。 可执行文件可以是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的任务和容器之一，也可以是自定义任务。 有关详细信息，请参阅[Integration Services Tasks](integration-services-tasks.md)并[Integration Services 容器](integration-services-containers.md)。  
  
### <a name="precedence-constraints"></a>优先约束  
 优先约束将同一父容器中的容器和任务链接到已排序的控制流中。 有关详细信息，请参阅 [优先约束](precedence-constraints.md)。  
  
### <a name="event-handlers"></a>事件处理程序  
 容器级别的事件处理程序对由容器或容器包括的对象所引发的事件做出响应。 有关详细信息，请参阅 [Integration Services (SSIS) 事件处理程序](../integration-services-ssis-event-handlers.md)。  
  
### <a name="variables"></a>变量  
 在容器中使用的变量包括由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的容器级别系统变量和容器使用的用户定义变量。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)。  
  
## <a name="break-points"></a>断点  
 对容器设置断点且中断条件为 **“当容器收到 OnVariableValueChanged 事件时断开”** 时，请在容器范围内定义变量。  
  
## <a name="see-also"></a>请参阅  
 [控制流](control-flow.md)  
  
  
