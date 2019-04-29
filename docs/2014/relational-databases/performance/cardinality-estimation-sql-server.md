---
title: 基数估计 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f7c3f609bd2b25fcb3e3553497ead2baad476f2f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151047"
---
# <a name="cardinality-estimation-sql-server"></a>基数估计 (SQL Server)
  称作基数估计器的基数估计逻辑已在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中重新设计，以便改进查询计划的质量，并因此改进查询性能。 新的基数估计器纳入在新型 OLTP 和数据仓库工作负荷中表现优异的假设和算法。 它基于针对新型工作负荷的深入基数估计研究，以及我们在过去 15 年在改进 SQL Server 基数估计器方面的学习。 客户反馈表明，尽管大多数查询将会从更改或保持不更改中受益，但与以前的基数估计器相比，少数查询可能会显得退步。  
  
> [!NOTE]  
>  基数估计是对查询结果中行数的预测。 查询优化器使用这些估计选择查询执行计划。 查询计划的质量对于改进查询性能有着直接影响。  
  
## <a name="performance-testing-and-tuning-recommendations"></a>性能测试和优化建议  
 对于在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中创建的所有新数据库，将启用新基数估计器。 但是，升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 并不会对现有数据库启用新基数估计器。  
  
 若要确保最佳查询性能，请使用以下建议用新的基数估计器测试您的工作负荷，然后在您的生产系统中启用它。  
  
1.  升级所有现有数据库以便使用新的基数估计器。 若要执行此操作，请使用[ALTER DATABASE 兼容性级别&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)数据库的兼容性级别设置为 120。  
  
2.  使用新基数估计器运行测试工作负荷，然后通过当前用来解决性能问题的相同方式解决任何新性能问题。  
  
3.  在用新的基数估计器（数据库兼容级别 120 (SQL Server 2014)）运行工作负荷并且特定查询已回归后，你可以运行具有跟踪标志 9481 的查询，以便使用在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更早版本中使用的基数估计器版本。 若要运行具有跟踪标志的查询，请参阅知识库文章 [启用可通过特定查询级别上的不同跟踪标志控制的影响计划的 SQL Server 查询优化器行为](https://support.microsoft.com/kb/2801413)。  
  
4.  如果不能更改的所有数据库以便使用新基数估计器，您可以使用之前的基数估计器的所有数据库使用[ALTER DATABASE 兼容性级别&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)到设置数据库兼容性级别为 110。  
  
5.  如果使用数据库兼容级别 110 运行您的工作负荷并且您想要使用新的基数估计器测试或运行特定查询，则可以运行具有跟踪标志 2312 的查询，以便使用 SQL Server 2014 版基数估计器。  若要运行具有跟踪标志的查询，请参阅知识库文章 [启用可通过特定查询级别上的不同跟踪标志控制的影响计划的 SQL Server 查询优化器行为](https://support.microsoft.com/kb/2801413)。  
  
## <a name="new-xevents"></a>新 XEvents  
 有两个新的 query_optimizer_estimate_cardinality XEvents 以便支持新查询计划。  
  
-   *query_optimizer_estimate_cardinality* 在查询优化器对关系表达式上的基数进行评估时发生。  
  
-   *query_optimizer_force_both_cardinality_estimation*_behaviors 在启用跟踪标志 2312 以及 9481 时发生，并且尝试同时强制旧的和新的基数估计行为。  
  
## <a name="examples"></a>示例  
 下面的示例显示新基数估计中的一些更改。 用于估计基数的代码已重新编写。 相关逻辑十分复杂，并且无法提供所有更改的详尽列表。  
  
> [!NOTE]  
>  这些示例作为概念信息提供。 您无需执行操作以便改变您设计数据库和查询的方式。  
  
### <a name="example-a-new-cardinality-estimates-use-an-average-cardinality-for-recently-added-ascending-data"></a>示例 A. 新基数估计使用平均基数用于新添加的升序数据  
 该示例演示对于在最近统计信息更新期间超出表中最大值的升序数据，新的基数估计器是如何改进基数估计的。  
  
```  
SELECT item, category, amount FROM dbo.Sales AS s WHERE Date = '2013-12-19';  
```  
  
 在该示例中，每天都有新行添加到 Sales 表，查询请求在 12/19/2013 发生的销售，并且统计信息上次更新时间是 12/18/2013。 之前的基数估计器假定 12/19/2013 值不存在，因为该日期超出了最大日期并且统计信息没有更新以便包括 12/19/2013 值。 这种情形称作升序键问题，如果在该天您加载数据，然后在更新统计信息前就对数据运行查询，则会发生此问题。  
  
 此行为已更改。 现在，即使对于自上次统计信息更新后添加的最近的升序数据未进行更新，新的基数估计器也假定这些值存在并且对于列中的每个值将平均基数用作基数估计。  
  
### <a name="example-b-new-cardinality-estimates-assume-filtered-predicates-on-the-same-table-have-some-correlation"></a>示例 B. 新的基数估计假定对同一个表的筛选的谓词具有某种关联  
 对于该示例，我们假定表 Cars 是 1000 行，Make 对于“Honda”具有 200 个匹配项，Model 对于“Civic”具有 50 个匹配项，并且所有 Civics 均为 Hondas。 因此，Make 列中 20% 的值是“Honda”，Model 列中 5% 的值是“Civic”，并且 Honda Civics 的实际数目为 50。 以前的基数估计假定 Make 和 Model 列中的值是彼此独立的。 上一查询优化器估计有 10 个 Honda Civics (.05 *.20 \* 1000年行 = 10 行)。  
  
```  
SELECT year, purchase_price FROM dbo.Cars WHERE Make = 'Honda' AND Model = 'Civic';  
```  
  
 此行为已更改。 现在，新基数估计假定 Make 和 Model 列具有“某种”  关联。 查询优化器通过向估计公式添加指数成分，估计更高的基数。 查询优化器现在估计 22.36 行 (.05 * SQRT(.20) \* 1000年行 = 22.36 行) 与谓词相匹配。 对于此方案以及特定的数据分布，22.36 行更接近于该查询将返回的实际 50 行。  
  
 请注意，新的基数估计器逻辑将对谓词选择性进行排序并且增加该指数。 例如，如果谓词选择性为.05、.20 和.25，则基数估计将是 (.05 * SQRT(.20) \* SQRT(SQRT(.25)))。  
  
### <a name="example-c-new-cardinality-estimates-assume-filtered-predicates-on-different-tables-are-independent"></a>示例 C. 新的基数估计假定对不同表的筛选的谓词是独立的  
 对于此示例，以前的基数估计器谓词筛选器 filters s.type 和 r.date 是关联的。 但是，针对新型工作负荷的测试结果表明，针对不同表中列上的谓词筛选器通常是彼此不相关的。  
  
```  
SELECT s.ticket, s.customer, r.store FROM dbo.Sales AS s CROSS JOIN dbo.Returns AS r  
WHERE s.ticket = r.ticket AND s.type = 'toy' AND r.date = '2013-12-19';  
```  
  
 此行为已更改。 现在，新的基数估计器逻辑假定 s.type 与 r.date 不相关。 实际上，假定是每天都会退回玩具，而不是在具体某一天退回。 在此类情形下，与以前的基数估计相比，新的基数估计将是更小的数值。  
  
## <a name="see-also"></a>请参阅  
 [监视和优化性能](monitor-and-tune-for-performance.md)  
  
  
