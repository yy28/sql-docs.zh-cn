---
title: Query Store 的数据收集方式 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: cb030bf28132c573774fa393089cf688184c85b3
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540977"
---
# <a name="how-query-store-collects-data"></a>查询存储的数据收集方法
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  查询存储的作用是作为 **数据记录器** 不断地收集与运行和计划相关的编译和运行时信息。 与查询相关的数据将永久保存在内部表中，并通过一组视图向用户显示。  
  
## <a name="views"></a>视图  
 下图显示了查询存储视图及其逻辑关系，以及显示为蓝色实体的编译时间信息：  
  
 ![query-store-process-2views](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
  
 **查看描述**  
  
|“查看”|描述|  
|----------|-----------------|  
|**sys.query_store_query_text**|提供对数据库执行的唯一查询文本。 将忽略查询文本之前和之后的注释和空格。 不忽略文本内部的注释和空格。 批中每个语句都会生成单独的查询文本项。|  
|**sys.query_context_settings**|显示执行查询所依据的影响计划设置的独特组合。 由于 `context_settings_id` 是查询键的一部分，因此不同影响计划设置执行的相同查询文本将在查询存储中生成单独的查询条目。|  
|**sys.query_store_query**|在查询存储中单独进行跟踪和强制执行的查询条目。 如果在不同的上下文设置下执行，或在不同的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 模块（存储过程、触发器等）内外执行，则单个查询文本会产生多个查询条目。|  
|**sys.query_store_plan**|显示具有编译时间统计信息的查询估计计划。 存储计划相当于一个可以通过使用 `SET SHOWPLAN_XML ON`获取的计划。|  
|**sys.query_store_runtime_stats_interval**|查询存储将时间划分为自动生成的时间窗口（间隔），并根据每个执行计划的间隔存储聚合的统计信息。 间隔大小由配置选项“统计信息收集间隔”（位于 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中）或 `INTERVAL_LENGTH_MINUTES` 使用 [ALTER DATABASE SET Options (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md) 进行控制。|  
|**sys.query_store_runtime_stats**|执行计划的聚合运行时统计信息。 所有捕获的度量值以 4 种统计函数形式表示：平均值、最小值、最大值和标准偏差。|  
  
 有关查询存储视图的其他详细信息，请参阅 **使用查询存储来监视性能** 中的 [相关视图、函数和过程](monitoring-performance-by-using-the-query-store.md)部分。  
  
## <a name="query-processing"></a>查询处理  
 查询存储在以下关键点与查询处理管道进行交互：  
  
1.  第一次编译查询时，会将查询文本和初始计划发送到查询存储。  
  
2.  重新编译查询时，将在查询存储中更新该计划。 如果创建新的计划，查询存储将为查询添加新计划条目，将之前的条目与其执行统计信息保存在一起。  
  
3.  执行查询时，将运行时统计信息发送到查询存储。 查询存储为每个在当前活动间隔内执行的计划保存准确的聚合统计信息。  
  
4.  在编译和检查重新编译阶段期间， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 确定查询存储中是否存在某一计划应当应用于当前正在运行的查询。 如果没有强制执行的计划，而且过程缓存中的计划不同于强制计划，重新编译查询，就像计划提示应用于该查询的方式一样有效。 此过程的发生对用户应用程序是透明的。  
  
 下图描绘了上文所述的集成点：  
  
 ![query-store-process-2processor](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor")  
  
 若要最大程度减少 I/O 开销，新的数据是在内存中捕获的。 写入操作排队，并稍后将其刷新到磁盘。 以最低的延迟刷新查询和计划信息（下图中的计划存储）。 运行时统计信息 (Runtime Stats) 会在内存中保留一段时间，该时间用 `SET QUERY_STORE` 语句的 `DATA_FLUSH_INTERVAL_SECONDS` 选项定义。 “SSMS 查询存储”对话框允许输入“数据刷新间隔(分钟)”，它将转换为秒。  
  
 ![query-store-process-3plan](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan")  
  
 发生系统崩溃时，查询存储可能会丢失不超过按照 `DATA_FLUSH_INTERVAL_SECONDS`定义的运行时数据数量。 默认值 900 秒（15 分钟）是查询捕获性能和数据可用性之间的最佳平衡。  
如果出现内存压力，运行时统计信息会在按照 `DATA_FLUSH_INTERVAL_SECONDS`所定义的时间之前刷新到磁盘。  
读取查询存储过程中，内存中数据和磁盘上的数据以透明方式统一。
如果会话终止或客户端应用程序重启/故障，将不会记录查询统计信息。  
  
 ![query-store-process-4planinfo](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

  
## <a name="see-also"></a>另请参阅  
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Query Store 最佳实践](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [查询存储目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
