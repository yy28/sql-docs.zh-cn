---
title: "基于时间的行筛选器的最佳做法 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: best practices
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 80f52f422d5804a14dc3fbac86ac40a2d3a143ac
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="best-practices-for-time-based-row-filters"></a>基于时间的行筛选器的最佳实践
  应用程序用户通常需要某个表的基于时间的数据子集。 例如，销售人员可能需要上周的订单数据，事件计划人员可能需要下周的事件数据。 在许多情况下，应用程序使用包含 **GETDATE()** 函数的查询来实现此功能。 请考虑以下行筛选器语句：  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 使用此类型的筛选器时，通常假定合并代理运行时始终发生两件事情：满足此筛选器的行复制到订阅服务器中；从订阅服务器中清除不再满足此筛选器的行。 （有关如何使用 **HOST_NAME()** 进行筛选的详细信息，请参阅[参数化行筛选器](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。）但是，合并复制只复制并清除自上次同步以来发生更改的数据，而不考虑如何定义数据的行筛选器。  
  
 要使合并复制处理某一行，该行中的数据必须满足行筛选器，并且该行自上次同步以来必须已发生更改。 对于 **SalesOrderHeader** 表，插入行时将输入 **OrderDate** 。 由于插入是一种数据更改，因此各行将如预期的那样被复制到订阅服务器中。 但是，如果订阅服务器中存在不再满足此筛选器的行（这些行是早于七天前的订单中的行），除非由于某种原因更新这些行，否则不会从订阅服务器中将其删除。  
  
 事件计划人员的情况进一步突显了此类型筛选所存在的问题。 对于 **Events** 表，请考虑以下筛选器：  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 对于包含事件的表，可能在事件日期之前进行插入。 如果在一个月之前插入了要在下周发生的事件，并且由于某种原因未更新行，那么即使该行满足行筛选器，也不会将该行复制到订阅服务器。  
  
 此外，根据发布的配置方式，合并复制可能会在不同时间对筛选器求值：  
  
-   如果发布使用预计算分区（默认设置），将在插入或更新行时对筛选器求值。  
  
-   如果发布不使用预计算分区，则在合并代理运行时对筛选器求值。  
  
 有关预计算分区的详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。 对筛选器求值的时间会影响什么数据满足筛选器。 例如，如果发布使用预计算分区，并且每两天同步一次数据，则销售人员的数据子集可能包括比预期时间早两天的行。  
  
## <a name="recommendations-for-using-time-based-row-filters"></a>使用基于时间的行筛选器时的建议  
 下面的方法提供了基于时间进行筛选的强大而直接的途径：  
  
-   向表中添加数据类型为 **bit**的一列。 此列用来指示是否应复制行。  
  
-   使用引用新列而非基于时间的列的行筛选器。  
  
-   创建一个 SQL Server 代理作业（通过另一种机制计划的作业），该作业在合并代理计划运行之前更新列。  
  
 此方法解决了使用 **GETDATE()** 或其他基于时间的方法时的缺点，并避免了必须确定何时为分区对筛选器求值的问题。 考虑 **Events** 表的以下示例：  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**复制**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|招待会|112|2006-10-04|1|  
|2|宴会|112|2006-10-10|0|  
|3|聚会|112|2006-10-11|0|  
|4|婚礼|112|2006-10-12|0|  
  
 此表的行筛选器将如下所示：  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND Replicate = 1  
```  
  
 SQL Server 代理作业可在每个合并代理运行之前执行类似如下的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句：  
  
```  
UPDATE Events SET Replicate = 0 WHERE Replicate = 1  
GO  
UPDATE Events SET Replicate = 1 WHERE EventDate <= GETDATE()+6  
GO  
```  
  
 第一行将 **Replicate** 列重置为 **0**，第二行对未来七天内发生的事件将该列设置为 **1** 。 如果此 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句在 2006 年 10 月 7 日运行，则该表将更新为：  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**复制**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|招待会|112|2006-10-04|0|  
|2|宴会|112|2006-10-10|1|  
|3|聚会|112|2006-10-11|1|  
|4|婚礼|112|2006-10-12|1|  
  
 现在，下周的事件被标记为正准备进行复制。 当下次为事件协调器 112 使用的订阅运行合并代理时，将把第 2、3 和 4 行下载到订阅服务器中，并从订阅服务器中删除第 1 行。  
  
## <a name="see-also"></a>另请参阅  
 [GETDATE (Transact-SQL)](../../../t-sql/functions/getdate-transact-sql.md)   
 [执行作业](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
