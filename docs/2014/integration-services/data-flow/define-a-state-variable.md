---
title: 定义状态变量 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45d66152-883a-49a7-a877-2e8ab45f8f79
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca9e4b8dd9c00904b09645e4d0c45673fbb6020f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811629"
---
# <a name="define-a-state-variable"></a>定义状态变量
  本过程介绍如何定义用于存储 CDC 状态的包变量。  
  
 该 CDC 状态变量由 CDC 控制任务加载、初始化和更新，并且由 CDC 源数据流组件用于确定针对更改记录的当前处理范围。 可对 CDC 控制任务和 CDC 源所共有的任何容器定义该 CDC 状态变量。 此操作可在包级别进行，但也可以对循环容器之类的其他容器进行。  
  
 不建议手动修改 CDC 状态变量值，但是，了解其内容可能会很有用。  
  
 下表提供了 CDC 状态变量值的组分的详细说明。  
  
|组件|Description|  
|---------------|-----------------|  
|`<state-name>`|这是当前 CDC 状态的名称。|  
|`CS`|这标记当前处理范围开始点（当前开始）。|  
|`<cs-lsn>`|这是上一次 CDC 运行中处理的最后一个（日志序列号）LSN。|  
|`CE`|这标记当前处理范围结束点（当前结束）。 CDC 状态中的 CE 组分表示 CDC 包当前正在处理或 CDC 包在完全处理其 CDC 处理范围前失败。|  
|`<ce-lsn>`|这是当前运行的 CDC 中要处理的最后一个 LSN。 始终假定要处理的最后一个序列号为最大值 (0xFFF…)。|  
|`IR`|这标记初始处理范围。|  
|`<ir-start>`|这是初始加载开始之前的最后一个更改 LSN。|  
|`<ir-end>`|这是初始加载结束之后的第一个更改 LSN。|  
|`TS`|这标记最后一个 CDC 状态更新的时间戳。|  
|**\<timestamp>**|这是 64 位 System.DateTime.UtcNow 属性的十进制表示法。|  
|`ER`|当最后一个操作失败且包括错误原因的简短说明时显示它。 如果存在该组分，则它始终最后一个显示。|  
|`<short-error-text>`|这是简短的错误说明。|  
  
 LSN 和序列号每个都作为一个十六进制的字符串编码，该字符串最多包含 20 位数字，表示 Binary(10) 的 LSN 值。  
  
 下表对可能的CDC 状态值进行了说明：  
  
|State|Description|  
|-----------|-----------------|  
|(INITIAL)|这是在当前 CDC 组上运行任何包之前的初始状态。 这也是 CDC 状态为空时的状态。|  
|ILSTART（初始加载已开始）|这是初始加载包已开始、`MarkInitialLoadStart` 操作调用 CDC 控制任务后时的状态。|  
|ILEND（初始加载已结束）|这是初始加载包已成功结束、`MarkInitialLoadEnd` 操作调用 CDC 控制任务后时的状态。|  
|ILUPDATE（初始加载更新）|这是在初始加载后仍在处理初始处理范围期间运行滴送更新包时的状态。 这是 `GetProcessingRange` 操作调用 CDC 控制任务后的状态。<br /><br /> 如果使用 _$reprocessing 列，该列设置为 1，指示该包可能在重新处理目标上已存在的行。|  
|TFEND（滴送更新已结束）|这是常规 CDC 运行应该出现的状态。 它指示前一次运行已成功完成，可以开始具有新的处理范围的新一轮运行。|  
|TFSTART|这是在非初始运行滴送更新包时、`GetProcessingRange` 操作调用 CDC 控制任务后的状态。<br /><br /> 这指示已启动常规 CDC 运行，但运行未完成或未完全结束 (`MarkProcessedRange`)。|  
|TFREDO（重新处理滴送更新）|这是在 TFSTART 之后执行 `GetProcessingRange` 时的状态。 这指示上次运行未成功完成。<br /><br /> 如果使用 _$reprocessing 列，该列设置为 1，指示该包可能在重新处理目标上已存在的行。|  
|ERROR|CDC 组处于 ERROR 状态。|  
  
 下面是 CDC 状态变量值的示例。  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   TFEND/CS/0x0000025B000001BC0003/TS/2011-07-17T12:05:58.1001145/  
  
-   TFSTART/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:43.9344900/  
  
-   TFREDO/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:59.5544900/  
  
### <a name="to-define-a-cdc-state-variable"></a>定义 CDC 状态变量  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开具有您需要定义变量的 CDC 流的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
2.  单击 **“包资源管理器”** 选项卡并添加新变量。  
  
3.  为该变量赋予一个可作为状态变量识别的名称。  
  
4.  为该变量赋予 **“字符串”** 数据类型。  
  
 不要向该变量赋予值来作为其定义的一部分。 该值必须由 CDC 控制任务设置。  
  
 如果您计划将该 CDC 控制任务用于 **“自动状态持久化”**，则该 CDC 状态变量将从您指定的数据库状态表中读取并且在其值更改时将更新回该相同的表。 有关状态表的详细信息，请参阅 [CDC Control Task](../control-flow/cdc-control-task.md)和 [CDC Control Task Editor](../cdc-control-task-editor.md)。  
  
 如果您不将该 CDC 控制任务用于“自动状态持久化”，则必须从持久性存储区中加载该变量值，在该持久性存储区中，在上次包运行时保存了该变量值并且在当前处理范围完成后该变量值将写回持久性存储区。  
  
## <a name="see-also"></a>请参阅  
 [CDC Control Task](../control-flow/cdc-control-task.md)   
 [CDC Control Task Editor](../cdc-control-task-editor.md)  
  
  
