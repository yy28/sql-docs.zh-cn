---
title: Analysis Services 跟踪事件 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services], SQL Server Profiler
- events [Analysis Services]
- event classes [Analysis Services], about event classes
- Profiler [SQL Server Profiler], Analysis Services
- event classes [Analysis Services]
ms.assetid: 6fb219cc-f37e-437a-a544-01cec0953571
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 94ed69a366d8e9cc8a622e10176086ba1c32686e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-trace-events"></a>Analysis Services 跟踪事件
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以通过捕获然后分析实例生成的跟踪事件，执行 Microsoft SQL Server Analysis Services (SSAS) 实例的活动。  跟踪事件将会划分为若干组，以便您可以更轻松地找到相关跟踪事件。  每个跟踪事件都包含与该事件相关的一组数据；并不是所有数据片段都与所有事件相关。  
  
 可以使用 **[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]** 启动和捕获跟踪事件（请参阅 [使用 SQL Server Profiler 监视 Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)），也可以通过 XMLA 命令作为 **SQL Server 扩展事件** 启动跟踪事件，并在以后进行分析（请参阅 [使用 SQL Server 扩展事件监视 Analysis Services](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)）。  
  
 下表描述各事件类别以及该类别中的事件。 每个表都包含以下列：  
  
**事件 ID**  
 标识事件类型的整数值。 在您读取转换为表或 XML 文件的跟踪以便筛选事件类型时，该值将很有用。  
  
**事件名称**  
 在 Analysis Services 客户端应用程序中向事件提供的名称。  
  
**事件说明**  
 对事件的简短说明。  
  
 **[“命令事件”事件类别](../../analysis-services/trace-events/command-events-event-category.md)**  
  
 用于命令的事件集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|15|命令开始|命令开始。|  
|16|命令结束|命令结束。|  
  
 **[“发现事件”事件类别](../../analysis-services/trace-events/discover-events-event-category.md)**  
  
 用于发现请求的事件集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|36|发现开始|发现请求的开始。|  
|38|发现结束|发现请求的结束。|  
  
 **[发现服务器状态事件类别](../../analysis-services/trace-events/discover-server-state-event-category.md)**  
  
 用于服务器状态发现的事件集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|33|服务器状态发现开始|服务器状态发现的开始。|  
|34|服务器状态发现数据|服务器状态发现响应的内容。|  
|35|服务器状态发现结束|服务器状态发现的结束。|  
  
 **[错误和警告事件类别](../../analysis-services/trace-events/errors-and-warnings-event-category.md)**  
  
 服务器错误事件的集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|17|错误|服务器错误。|  
  
 **[“文件加载和保存事件”类别](../../analysis-services/trace-events/file-load-and-save-event-category.md)**  
  
 用于文件加载和保存操作报告的事件的集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|90|文件加载开始|文件加载开始。|  
|91|文件加载结束|文件加载结束。|  
|92|文件保存开始|文件保存开始。|  
|93|文件保存结束|文件保存结束|  
|94|PageOut 开始|PageOut 开始。|  
|95|PageOut 结束|PageOut 结束|  
|96|PageIn 开始|PageIn 开始。|  
|97|PageIn 结束|PageIn 结束|  
  
 **[“锁定事件”类别](../../analysis-services/trace-events/lock-events-category.md)**  
  
 与锁相关的事件的集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|50|死锁|元数据锁死锁。|  
|51|锁超时|元数据锁超时。|  
|52|已获取锁|已获取锁|  
|53|已释放锁|已释放锁|  
|54|正在等待的锁|正在等待的锁|  
  
 **[“通知事件”事件类别](../../analysis-services/trace-events/notification-events-event-category.md)**  
  
 通知事件的集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|39|通知|通知事件。|  
|40|用户定义|用户定义事件。|  
  
 **[“进度报告”事件类别](../../analysis-services/trace-events/progress-reports-event-category.md)**  
  
 用于进度报告的事件集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|5|进度报告开始|进度报告开始。|  
|6|进度报告结束|进度报告结束。|  
|7|进度报告当前状态|进度报告正在运行。|  
|8|进度报告错误|进度报告出错。|  
  
 **[查询事件类别](../../analysis-services/trace-events/queries-events-category.md)**  
  
 用于查询的事件集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|9|查询开始|查询开始。|  
|10|查询结束|查询结束。|  
  
 **[查询处理事件类别](../../analysis-services/trace-events/query-processing-events-category.md)**  
  
 查询执行过程中的主要事件的集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|70|查询多维数据集开始|查询多维数据集开始。|  
|71|查询多维数据集结束|查询多维数据集结束。|  
|72|计算非空开始|计算非空开始。|  
|73|计算非空当前|计算非空当前。|  
|74|计算非空结束|计算非空结束。|  
|75|序列化结果开始|序列化结果开始。|  
|76|序列化结果当前|序列化结果当前。|  
|77|序列化结果结束|序列化结果结束。|  
|78|执行 MDX 脚本开始|执行 MDX 脚本开始。|  
|79|执行 MDX 脚本当前|执行 MDX 脚本当前。 不推荐使用。|  
|80|执行 MDX 脚本结束|执行 MDX 脚本结束。|  
|81|查询维度|查询维度。|  
|11|查询子多维数据集|查询子多维数据集，用于基于使用情况的优化。|  
|12|查询子多维数据集详情|查询子多维数据集的详细信息。 此事件在启用时可能会对性能产生负面影响。|  
|60|从聚合获取数据|通过从聚合获取数据答复查询。 此事件在启用时可能会对性能产生负面影响。|  
|61|从缓存获取数据|通过从某个缓存获取数据答复查询。 此事件在启用时可能会对性能产生负面影响。|  
|82|VertiPaq SE 查询开始|VertiPaq SE 查询|  
|83|VertiPaq SE 查询结束|VertiPaq SE 查询|  
|84|资源使用情况|在命令和查询结束后报告读取、写入和 cpu 使用情况。|  
|85|VertiPaq SE 查询缓存匹配|VertiPaq SE 查询缓存使用|  
|98|直接查询开始|直接查询开始。|  
|99|直接查询结束|直接查询结束。|  
  
 **[“安全审核”事件类别](../../analysis-services/trace-events/security-audit-event-category.md)**  
  
 数据库审核事件类的集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|1|审核登录|收集从开始跟踪之后发生的所有新连接事件，如客户端请求与正在运行 SQL Server 实例的服务器进行连接。|  
|2|审核注销|收集从开始跟踪之后发生的所有新断开连接事件，如客户端发出一个断开连接命令即属于一个断开连接事件。|  
|4|审核服务器启动和停止|记录服务关闭、启动和暂停活动。|  
|18|审核对象权限事件|记录对象权限更改。|  
|19|审核管理操作事件|记录服务器备份/还原/同步/附加/分离/图像加载/图像保存。|  
  
 [“会话事件”事件类别](../../analysis-services/trace-events/session-events-event-category.md)  
  
 会话事件的集合。  
  
|**事件 ID**|**事件名称**|**事件说明**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|现有用户连接。|  
|42|现有会话|现有会话。|  
|43|会话初始化|会话初始化。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL Server Profiler 监视 Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
  
