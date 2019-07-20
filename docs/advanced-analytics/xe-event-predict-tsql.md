---
title: 用于监视 PREDICT 语句的扩展事件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1c534681200abf056c8bc7dd3745d8098d59c146
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345662"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>用于监视 PREDICT 语句的扩展事件

本文介绍 SQL Server 中提供的扩展事件, 这些事件可用于监视和分析使用[预测](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)在 SQL Server 中执行实时评分的作业。

实时评分从存储在 SQL Server 中的机器学习模型生成分数。 PREDICT 函数不需要外部运行时, 例如 R 或 Python, 只需要使用特定二进制格式创建的模型。 有关详细信息, 请参阅[实时计分](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)。

## <a name="prerequisites"></a>先决条件

有关扩展事件的一般信息 (有时称为 XEvents), 以及如何在会话中跟踪事件, 请参阅以下文章:

+ [扩展事件的概念和体系结构](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [在 SSMS 中设置事件捕获](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [管理对象资源管理器中的事件会话](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>扩展事件表

以下扩展事件适用于支持[T-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)语句的所有版本 SQL Server, 包括 Linux 上的 SQL Server 和 Azure SQL 数据库。 

T-sql PREDICT 语句是在 SQL Server 2017 中引入的。 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |事件  |内置执行时间细分|
|predict_model_cache_hit |事件|在从 PREDICT 函数模型缓存中检索模型时发生。 将此事件与其他 predict_model_cache_ * 事件一起使用来解决由 PREDICT 函数模型缓存引起的问题。|
|predict_model_cache_insert |事件  |   在将模型插入到 PREDICT 函数模型缓存中时发生。 将此事件与其他 predict_model_cache_ * 事件一起使用来解决由 PREDICT 函数模型缓存引起的问题。    |
|predict_model_cache_miss   |事件|在预测函数模型缓存中找不到模型时发生。 此事件频繁出现可能表明 SQL Server 需要更多内存。 将此事件与其他 predict_model_cache_ * 事件一起使用来解决由 PREDICT 函数模型缓存引起的问题。|
|predict_model_cache_remove |事件| 当从 PREDICT 函数的模型缓存中删除模型时发生。 将此事件与其他 predict_model_cache_ * 事件一起使用来解决由 PREDICT 函数模型缓存引起的问题。|

## <a name="query-for-related-events"></a>查询相关事件

若要查看为这些事件返回的所有列的列表, 请在 SQL Server Management Studio 中运行以下查询:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>示例

使用 PREDICT 捕获有关评分会话性能的信息:

1. 使用 Management Studio 或其他支持的[工具](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)创建新的扩展事件会话。
2. 将事件`predict_function_completed`和`predict_model_cache_hit`添加到会话中。
3. 启动扩展事件会话。
4. 运行使用预测的查询。

在结果中, 查看以下列:

+ 的值`predict_function_completed`显示查询加载模型和评分所花费的时间。
+ 的布尔值`predict_model_cache_hit`指示该查询是否使用了缓存的模型。 

### <a name="native-scoring-model-cache"></a>本机评分模型缓存

除了特定于预测的事件外, 还可以使用以下查询来获取有关缓存模型和缓存使用情况的详细信息:

查看本机评分模型缓存:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

查看模型缓存中的对象:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

