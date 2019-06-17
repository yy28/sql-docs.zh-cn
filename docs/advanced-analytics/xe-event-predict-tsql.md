---
title: 用于监视 PREDICT 语句的 SQL Server 机器学习服务的扩展的事件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fa0d9d4ed647a6616c525533e696960784d09290
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63142309"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>用于监视 PREDICT 语句的扩展事件

本指南介绍了扩展的事件，提供 SQL Server 中可用于监视和分析作业使用[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)执行 SQL Server 中的实时评分。

实时评分从机器学习已存储在 SQL Server 的模型生成分数。 PREDICT 函数不需要 R 或 Python，仅使用特定的二进制格式创建的模型等外部运行时。 有关详细信息，请参阅[实时评分](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)。

## <a name="prerequisites"></a>先决条件

有关扩展的事件 （有时称为 XEvents），以及如何在会话中跟踪事件的常规信息，请参阅以下文章：

+ [扩展事件概念和体系结构](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [设置在 SSMS 中的事件捕获](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [管理在对象资源管理器中的事件会话](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>扩展事件表

以下扩展事件是在支持的所有版本的 SQL Server 中可用[T-SQL 的预测](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)语句，包括 Linux 和 Azure SQL 数据库上的 SQL Server。 

在 SQL Server 2017 引入了 T-SQL 的预测语句。 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |事件  |内置执行时间细分|
|predict_model_cache_hit |事件|从 PREDICT 函数模型缓存检索模型时发生。 使用此事件与其他 predict_model_cache_ * 事件来解决由 PREDICT 函数模型缓存引起的问题。|
|predict_model_cache_insert |事件  |   当模型插入 PREDICT 函数模型缓存时发生。 使用此事件与其他 predict_model_cache_ * 事件来解决由 PREDICT 函数模型缓存引起的问题。    |
|predict_model_cache_miss   |事件|在 PREDICT 函数模型缓存中找不到模型时发生。 此事件频繁出现可能指示 SQL Server 需要更多的内存。 使用此事件与其他 predict_model_cache_ * 事件来解决由 PREDICT 函数模型缓存引起的问题。|
|predict_model_cache_remove |事件| 从 PREDICT 函数模型缓存中删除模型时发生。 使用此事件与其他 predict_model_cache_ * 事件来解决由 PREDICT 函数模型缓存引起的问题。|

## <a name="query-for-related-events"></a>查询相关的事件

若要查看这些事件返回的所有列的列表，请在 SQL Server Management Studio 中运行以下查询：

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>示例

若要捕获性能使用预测的评分会话的信息：

1. 创建一个新的扩展事件会话，并且使用 Management Studio 或支持的另一[工具](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)。
2. 添加的事件`predict_function_completed`和`predict_model_cache_hit`到会话。
3. 启动扩展的事件会话。
4. 运行使用预测查询。

在结果中，查看这些列：

+ 值为`predict_function_completed`显示了多少时间花在加载模型和评分的查询。
+ 布尔值，`predict_model_cache_hit`指示查询是否使用缓存的模型。 

### <a name="native-scoring-model-cache"></a>本机评分模型缓存

除了预测特定的事件中，可以使用以下查询以获取有关缓存的模型和缓存使用情况详细信息：

查看本机评分模型缓存：

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

在模型缓存中查看的对象：

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

