---
title: Microsoft SQL 数据库中的智能查询处理 | Microsoft Docs
description: 智能查询处理功能，用于提高 SQL Server 和 Azure SQL 数据库中的查询性能。
ms.custom: ''
ms.date: 07/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 3e085237766280d08d22fd0a71c350c26686b6f7
ms.sourcegitcommit: 01fccb8015644e75fd99fc5543d8216a1539f6ca
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2018
ms.locfileid: "40405616"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 数据库中的智能查询处理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

“智能查询处理”功能系列包含有广泛影响的功能，以提升现有工作负载的性能，同时最大限度地减少实现工作量。

![“智能查询处理”功能](./media/1_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>自适应查询处理
“自适应查询处理”功能系列包含查询处理改进，以对应用程序工作负载的运行时状况采用优化策略。 具体改进包括：批处理模式自适应联接、内存授予反馈和多语句表值函数交错执行。

### <a name="batch-mode-adaptive-joins"></a>批处理模式自适应联接
此功能可让你的计划在使用单个缓存计划执行期间动态切换到更好的连接策略。

### <a name="row-and-batch-mode-memory-grant-feedback"></a>行模式和批处理模式内存授予反馈
此功能会重新计算查询所需的实际内存，然后更新缓存计划的授予值，从而减少影响并发的过度内存授予并修复导致磁盘大量溢出的低估内存授予。

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>多语句表值函数 (MSTVF) 交错执行
通过交错执行，函数中的实际行计数可用于做出更明智的下游查询计划决策。 

有关详细信息，请参阅 [SQL 数据库中的自适应查询处理](../../relational-databases/performance/adaptive-query-processing.md)。

## <a name="table-variable-deferred-compilation"></a>表变量延迟编译
“表变量延迟编译”功能提升了计划质量和引用表变量的查询的整体性能。 在优化和初始编译期间，此功能会传播基于实际表变量行计数的基数估计。  这种准确的行计数信息将用于优化下游计划操作。

使用“表变量延迟编译”，引用表变量的语句会延迟编译，直到首次实际执行语句后。 此延迟编译行为等同于临时表行为，这一变化会导致使用实际基数，而不是原始的一行猜测。 若要在 Azure SQL 数据库中启用“表变量延迟编译”的公共预览版，请为执行查询时连接到的数据库启用数据库兼容性级别 150。

有关详细信息，请参阅[表变量延迟编译](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation )。

## <a name="approximate-query-processing"></a>近似查询处理
“近似查询处理”是新功能系列，旨在跨响应速度比绝对精度更为关键的大型数据集进行聚合。  例如，跨 100 亿行计算 COUNT(DISTINCT())，以供显示在仪表板上。  在这种情况下，绝对精度并不重要，关键在于响应速度。 新增的 APPROX_COUNT_DISTINCT 聚合函数返回组中唯一非空值的近似数。

有关详细信息，请参阅 [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)。

## <a name="see-also"></a>另请参阅
[SQL Server 数据库引擎和 Azure SQL 数据库的性能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)    
[Showplan 逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[联接](../../relational-databases/performance/joins.md)    
[演示自适应查询处理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)        
