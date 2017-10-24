---
title: "使用 SQL Server 事件探查器监视数据挖掘 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 655ac93c-5c5c-4565-914b-915327f7d349
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96b5485ebddba8823f262ba6a2229018d82a72fd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>使用 SQL Server 事件探查器监视数据挖掘（Analysis Services – 数据挖掘）
  如果您具有必要的权限，可以使用 SQL Server Profiler 监视作为请求发送到 SQL Server Analysis Services 实例的数据挖掘活动。 数据挖掘活动可以包括处理模型或结构、预测查询或内容查询或者创建新模型或结构。  
  
 SQL Server Profiler 使用 **跟踪** 监视多个客户端发来的请求，其中包括 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、SQL Server Management Studio、Web 服务或 Excel 数据挖掘外接程序，但前提是这些活动均使用同一 SQL Server Analysis Services 实例。 必须为要监视的每个 SQL Server Analysis Services 实例创建一个单独的跟踪。 有关跟踪的常规信息和如何使用 SQL Server Profiler，请参阅[使用 SQL Server Profiler 监视 Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)。  
  
 有关要捕获的事件类型的具体指南，请参阅[为重播创建探查器跟踪 (Analysis Services)](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)。  
  
## <a name="using-traces-to-monitor-data-mining"></a>使用跟踪监视数据挖掘  
 如果在跟踪中捕获信息，则可以指定是否将该信息保存到 SQL Server 实例中的文件夹或表中。 无论使用什么方法存储该数据，都可以使用 SQL Server Profiler 根据事件查看跟踪和筛选。 下表列出了默认 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 跟踪中影响数据挖掘的一些事件和子类。  
  
|EventClass|EventSubclass|Description|  
|----------------|-------------------|-----------------|  
|**查询开始**<br /><br /> **查询结束**|**0 - MDXQuery**|包含对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 存储过程的所有调用的文本。|  
|**查询开始**<br /><br /> **查询结束**|**1 - DMXQuery**|包含数据挖掘扩展插件 (DMX) 语句的文本和结果。|  
|**进度报告开始**<br /><br /> **进度报告结束**|**34 - DataMiningProgress**|提供有关数据挖掘算法的进度的信息：例如，如果正在生成聚类分析模型，则此进度消息指出正在生成哪一个候选分类。|  
|**查询开始**<br /><br /> **查询结束**|EXECUTESQL|包含正在执行的 Transact-SQL 查询的文本|  
|**查询开始**<br /><br /> **查询结束**|**2- SQLQuery**|包含任意针对以系统表形式存在的架构行集的查询的文本。|  
|**DISCOVER Begin**<br /><br /> **DISCOVER End**|多个|包含封装在 XMLA 中的 DMX 函数调用或 DISCOVER 语句的文本。|  
|**错误**|（无）|包含服务器发送到客户端的错误的文本。<br /><br /> 以“错误(数据挖掘):”或“信息(数据挖掘):”开头的错误消息专门在响应 DMX 请求时生成。 但只查看这些错误消息是不够的。 其他错误（例如由分析器生成的错误）虽然不具有此前缀，但也与数据挖掘有关。|  
  
 通过查看跟踪日志中的命令语句，还可以看到由客户端发送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器的复杂语句（包括对系统存储过程的调用）的语法。 您可以借助该信息进行调试，或者也可以将有效语句用作创建新预测查询或模型的模板。 有关可以通过跟踪捕获的存储过程调用的一些示例，请参阅 [群集模型查询示例](../../analysis-services/data-mining/clustering-model-query-examples.md)。  
  
## <a name="see-also"></a>另请参阅  
 [监视 Analysis Services 实例](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [使用 SQL Server 扩展事件监视 Analysis Services](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  

