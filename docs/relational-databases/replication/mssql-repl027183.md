---
title: MSSQL_REPL027183 | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_REPL027183 error
ms.assetid: 52c271ac-1a0e-43d5-85d4-35886d1efd32
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9629f3ae423a161aac65458cf1538d507492693a
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlrepl027183"></a>MSSQL_REPL027183
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|27183|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|合并进程未能使用参数化的行筛选器来枚举项目中的更改。 如果此操作仍失败，请增大该进程的查询超时值，缩短发布的保持期，并改进对已发布表的索引。|  
  
## <a name="explanation"></a>解释  
 在已筛选发布中处理更改时，如果出现合并代理超时，则会引发该错误。 超时可能由下列一种原因引起：  
  
-   没有使用预计算分区优化。  
  
-   用于筛选的列上存在索引碎片。  
  
-   大型合并元数据表，如 **MSmerge_tombstone**、 **MSmerge_contents**和 **MSmerge_genhistory**。  
  
-   未基于唯一键联接的已筛选表和涉及大量表的联接筛选器。  
  
## <a name="user-action"></a>用户操作  
 若要解决此问题：  
  
-   增大合并代理 **-QueryTimeOut** 参数的值，以在解决导致错误的基本问题后，仍可继续进行处理。 代理参数可以在代理配置文件和命令行中指定。 有关详细信息，请参阅：  
  
    -   [处理复制代理配置文件](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [查看和修改复制代理命令提示符参数 (SQL Server Management Studio)](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [复制代理可执行文件概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
-   请尽可能使用预计算分区优化。 如果许多发布要求都得到满足，则默认使用此优化。 有关这些要求的详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。 如果发布不满足这些要求，则请考虑重新设计发布。  
  
-   指定发布保持期可能的最低设置，因为只有在达到保持期时，复制才会清除发布数据库和订阅数据库中的元数据。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
-   在合并复制维护过程中，应不定期检查以下与合并复制相关联的系统表的增长情况： **MSmerge_contents**、 **MSmerge_genhistory**、 **MSmerge_tombstone**、 **MSmerge_current_partition_mappings**、 **MSmerge_past_partition_mappings**。 定期对这些表重建索引。 有关详细信息，请参阅 [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
-   请确保用于筛选的列已建立了适当的索引，并根据需要重新生成这些索引。 有关详细信息，请参阅 [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
-   设置基于唯一列的联接筛选器的 **join_unique_key** 属性。 有关详细信息，请参阅 [Join Filters](../../relational-databases/replication/merge/join-filters.md)。  
  
-   限制联接筛选器层次结构中的表数。 如果要生成五个或更多表的联接筛选器，请考虑其他解决方案：不筛选小表、不会发生更改的表或主要是查找表的表。 仅在必须在订阅中分区的表之间使用联接筛选器。  
  
-   在同步之间的筛选表上进行较少量的更改，或更加频繁地运行合并代理。 有关如何设置同步计划的详细信息，请参阅 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
