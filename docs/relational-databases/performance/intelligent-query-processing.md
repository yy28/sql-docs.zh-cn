---
title: Microsoft SQL 数据库中的智能查询处理 | Microsoft Docs
description: 智能查询处理功能，用于提高 SQL Server 和 Azure SQL 数据库中的查询性能。
ms.custom: ''
ms.date: 05/22/2018
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
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7786fd048f1698c90f379450b31e0bac3457706e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 数据库中的智能查询处理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

“智能查询处理”功能系列包含具有广泛影响的功能，这些功能以最少的实现工作量提高了现有工作负载的性能。   这包括改进已有的构造，并引入适应性方法和功能。  

## <a name="adaptive-query-processing"></a>自适应查询处理
智能查询处理功能系列中包括 SQL Server 2017 和 Azure SQL 数据库中引入的自适应查询处理功能系列，它们添加了全新的查询处理功能，可根据应用程序工作负载的运行时条件调整优化策略：
- **批处理模式自适应联接**。 此功能可让你的计划在使用单个缓存计划执行期间动态切换到更好的连接策略。
- **批处理模式内存授予反馈**。 此功能会重新计算查询所需的实际内存，然后更新缓存计划的授予值，从而减少影响并发的过度内存授予并修复导致磁盘大量溢出的低估内存授予。
- **多语句表值函数的交错执行 (MSTVFs)**。 通过交错执行，我们使用函数中的实际行数来作出更明智的下游查询计划决策。 

有关自适应查询处理的详细信息，请参阅 [SQL 数据库中的自适应查询处理](../../relational-databases/performance/adaptive-query-processing.md)。

## <a name="see-also"></a>另请参阅
[SQL Server 数据库引擎和 Azure SQL 数据库的性能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)    
[Showplan 逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[联接](../../relational-databases/performance/joins.md)    
[演示自适应查询处理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)        
