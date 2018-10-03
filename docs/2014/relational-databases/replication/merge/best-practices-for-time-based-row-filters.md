---
title: 基于时间的行筛选器的最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- best practices
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70fb66a1b61dbbdec0fd8443ac150b32c3770818
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48145519"
---
# <a name="best-practices-for-time-based-row-filters"></a>基于时间的行筛选器的最佳实践
  应用程序用户通常需要某个表的基于时间的数据子集。 例如，销售人员可能需要上周的订单数据，事件计划人员可能需要下周的事件数据。 在许多情况下，应用程序使用包含 `GETDATE()` 函数的查询来实现此功能。 请考虑以下行筛选器语句：  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 使用此类型的筛选器时，通常假定合并代理运行时始终发生两件事情：满足此筛选器的行复制到订阅服务器中；从订阅服务器中清除不再满足此筛选器的行。 (有关使用筛选的详细信息`HOST_NAME()`，请参阅[参数化行筛选器](parameterized-filters-parameterized-row-filters.md)。)但是，合并复制只复制并清除自上次同步以来发生更改的数据，而不考虑如何定义数据的行筛选器。  
  
 要使合并复制处理某一行，该行中的数据必须满足行筛选器，并且该行自上次同步以来必须已发生更改。 对于 **SalesOrderHeader** 表，插入行时将输入 **OrderDate** 。 由于插入是一种数据更改，因此各行将如预期的那样被复制到订阅服务器中。 但是，如果订阅服务器中存在不再满足此筛选器的行（这些行是早于七天前的订单中的行），除非由于某种原因更新这些行，否则不会从订阅服务器中将其删除。  
  
 事件计划人员的情况进一步突显了此类型筛选所存在的问题。 对于 **Events** 表，请考虑以下筛选器：  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 对于包含事件的表，可能在事件日期之前进行插入。 如果在一个月之前插入了要在下周发生的事件，并且由于某种原因未更新行，那么即使该行满足行筛选器，也不会将该行复制到订阅服务器。  
  
 此外，根据发布的配置方式，合并复制可能会在不同时间对筛选器求值：  
  
-   如果发布使用预计算分区（默认设置），将在插入或更新行时对筛选器求值。  
  
-   如果发布不使用预计算分区，则在合并代理运行时对筛选器求值。  
  
 有关预计算分区的详细信息，请参阅[使用预计算分区优化参数化筛选器性能](parameterized-filters-optimize-for-precomputed-partitions.md)。 对筛选器求值的时间会影响什么数据满足筛选器。 例如，如果发布使用预计算分区，并且每两天同步一次数据，则销售人员的数据子集可能包括比预期时间早两天的行。  
  
## <a name="recommendations-for-using-time-based-row-filters"></a>使用基于时间的行筛选器时的建议  
 下面的方法提供了基于时间进行筛选的强大而直接的途径：  
  
-   将列添加到数据类型的表`bit`。 此列用来指示是否应复制行。  
  
-   使用引用新列而非基于时间的列的行筛选器。  
  
-   创建一个 SQL Server 代理作业（通过另一种机制计划的作业），该作业在合并代理计划运行之前更新列。  
  
 此方法解决使用的不足之处`GETDATE()`或另一种基于时间的方法并避免了必须确定何时为分区计算筛选器问题。 考虑 **Events** 表的以下示例：  
  
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
  
## <a name="see-also"></a>请参阅  
 [GETDATE (Transact-SQL)](/sql/t-sql/functions/getdate-transact-sql)   
 [执行作业](../../../ssms/agent/implement-jobs.md)   
 [参数化行筛选器](parameterized-filters-parameterized-row-filters.md)  
  
  
