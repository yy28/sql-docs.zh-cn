---
title: 工作负荷管理 (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69063b1a-a8f3-453a-83ab-afbe7eb4f463
caps.latest.revision: 11
ms.openlocfilehash: 6dde6c1af7b704e5bd1ed0e03516ad94f191ad9d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="workload-management"></a>工作负荷管理
SQL Server PDW 工作负荷管理功能允许用户和管理员将分配请求用来预设置的内存和并发的配置。 使用工作负荷管理来提高指定工作负荷性能，一致或混合，允许进行合适的资源，不能始终使任何请求的请求。  
  
例如，与 SQL Server PDW 的工作负荷管理技术，你可以：  
  
-   分配大量的资源加载作业。  
  
-   指定用于生成列存储索引的更多资源。  
  
-   解决低性能哈希联接以查看是否需要更多内存，并将它提供更多内存。  
  
## <a name="Basics"></a>工作负荷管理基础知识  
  
### <a name="key-terms"></a>主要术语  
工作负荷管理  
*工作负荷管理*是能够了解和调整系统资源使用状况，以便实现最佳性能的并发请求。  
  
资源类  
在 SQL Server PDW*资源类*是具有预分配的内存和并发限制的内置服务器角色。 SQL Server PDW 将资源分配给根据资源类服务器角色成员资格的提交请求的登录名的请求。  
  
在计算节点上的资源类的实现在 SQL Server 中使用资源调控器功能。 有关资源调控器的详细信息，请参阅[资源调控器](http://msdn.microsoft.com/en-us/library/bb933866(v=sql.11).aspx)MSDN 上。  
  
### <a name="understand-current-resource-utilization"></a>了解当前的资源利用率  
若要了解当前正在运行的请求的系统资源利用率，使用 SQL Server PDW 动态管理视图。 例如，您可以使用 Dmv 来了解运行速度缓慢的大型哈希联接无法方面获益： 有更多内存。  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>调整资源分配  
若要调整资源使用率，请更改正在提交请求的登录名的资源类成员身份。 资源类服务器角色被命名为**mediumrc**， **largerc**，和**xlargerc**。 它们分别表示中型、 大型，和超大型资源分配。  
  
例如，若要分配大量的系统资源的请求，添加提交到请求的登录名**largerc**服务器角色。 下面的 ALTER SERVER ROLE 语句将 Anna 的登录名添加到 largerc 服务器角色。  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>资源类描述  
下表描述的资源类和其系统资源分配。  
  
|资源类|请求重要性|最大内存使用情况 *|并发槽 (最大 = 32)|Description|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|默认值|Medium|400 MB|1|默认情况下，每个登录名被允许的少量内存和其请求的并发资源。<br /><br />当登录名添加到资源类时，新类将优先。 从所有资源类将被删除登录名，该登录名将恢复到默认资源分配。|  
|MediumRC|Medium|1200 MB|3|可能需要的中等规模的资源类的请求的示例：<br /><br />CTAS 操作具有大型哈希联接。<br /><br />选择需要更多内存，以避免缓存到磁盘的操作。<br /><br />数据加载到聚集列存储索引。<br /><br />生成、 重新生成和重新组织较小具有 10-15 列的表的聚集列存储索引。|  
|largerc|High|2.8 GB|7|可能需要较大的资源类的请求的示例：<br /><br />非常大 CTAS 操作具有极大哈希联接，或包含大型聚合，例如大型的 ORDER BY 或 GROUP BY 子句。<br /><br />选择需要的内存量非常大进行操作，如哈希联接或聚合如 ORDER BY 或 GROUP BY 子句的操作<br /><br />数据加载到聚集列存储索引。<br /><br />生成、 重新生成和重新组织较小具有 10-15 列的表的聚集列存储索引。|  
|xlargerc|High|8.4 GB|22|超大型资源类是用于请求可能需要在运行时的额外较大的资源消耗。|  
  
<sup>*</sup>最大内存使用量是近似值。  
  
### <a name="request-importance"></a>请求重要性  
请求重要性映射到在计算节点上运行的 SQL Server 将为请求的 CPU 时间量。  具有较高优先级的请求都收到了更多的 CPU 时间。  
  
### <a name="maximum-memory-usage"></a>最大内存使用量  
最大内存使用量是最大请求可使用在每个处理空间内的可用内存量。 例如 mediumrc 请求可以使用为每个分布内处理的最大为 1200 MB。 仍，务必确保数据不偏离为了避免执行的大部分工作的几个分布区。  
  
### <a name="concurrency-slots"></a>并发槽  
分配 1、 3、 7 和 22 并发槽的目的是允许大型和小型进程运行在同一时间，而不会阻止小过程，在大型过程正在运行。  例如，SQL Server PDW 可以分配最多 32 并发槽在同一时间运行 1 特大型请求 （22 槽）、 1 个大型请求 （7 个插槽） 和 1 个中等规模请求 （3 槽）。  
  
分配对并发请求的最多 32 个并发槽的示例：  
  
-   28 槽 = 4 大型  
  
-   30 槽 = 10 中等  
  
-   32 槽 = 32 的默认值  
  
-   32 槽 = 1 特大 + 1 的大型 + 1 中等  
  
-   32 槽 = 2 大 + 4 中等 + 6 默认  
  
假设 6 大型请求提交到 SQL Server PDW，然后提交 10 个的默认请求。 SQL Server PDW 将处理的请求按优先级顺序，如下所示：  
  
-   分配 28 并发槽开始处理 4 的大型请求内存变得可用，并在队列中保持 2 较大的请求。  
  
-   分配 4 并发槽开始处理 4 默认请求并等待队列中保持 6 默认请求。  
  
在请求完成和并发槽变得可用时，SQL Server PDW 将分配根据可用资源和优先级剩下的请求。 例如，当存在 7 并发槽打开时，等待大型请求将具有的 7 插槽优先级高于处于等待状态中等规模请求。  如果打开 6 个插槽，SQL Server PDW 将分配 6 默认大小的更多请求。 但是，内存和并发槽都必须是可用之前 SQL Server PDW 允许运行的请求。  
  
在每个资源类，请求运行中第一个先进先出 (FIFO) 的顺序。  
  
## <a name="GeneralRemarks"></a>一般备注  
如果登录名是多个资源类的成员，则具有最多的资源的类将优先。  
  
当添加到或从资源类中删除登录名时，用于所有将来的请求; 立即生效的更改当前请求运行或等待不受影响。 该登录名不需要断开连接，然后才能使更改发生在重新连接。  
  
对于每个登录名，资源类设置应用于单个语句和操作，而不适用于会话。  
  
SQL Server PDW 运行语句之前，它将尝试获取请求所需的并发槽。 如果它无法获取足够并发槽，SQL Server PDW 将请求进入执行等待状态。 已分配给请求的所有资源系统都返回到系统中。  
  
大部分的 SQL 语句始终需要默认的资源分配，并因此不由资源类控制。 例如，CREATE LOGIN 仅需要少量的资源，并且即使调用创建登录名的登录名的成员分配的默认资源的资源类。  例如，如果 Anna 是 largerc 资源类的成员，并且她提交 CREATE LOGIN 语句，CREATE LOGIN 语句将运行默认数量的资源。  
  
SQL 语句，并由资源类控制的操作：  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER 表重新生成  
  
-   创建聚集的索引  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   创建 TABLE AS SELECT  
  
-   创建远程 TABLE AS SELECT  
  
-   使用加载数据**dwloader**。  
  
-   INSERT SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   还原到设备，但有更多计算节点还原时的数据库。  
  
-   选择，不包括仅限 DMV 的查询  
  
## <a name="Limits"></a>限制和局限  
资源类控制内存和并发分配。  不控制输入/输出操作。  
  
## <a name="Metadata"></a>元数据  
包含有关资源类和资源类成员信息的 Dmv。  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
包含有关请求和所需的资源的状态信息的 Dmv:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
从 SQL Server Dmv 计算节点上公开相关的系统视图。 请参阅[动态管理视图的 SQL Server](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)有关这些 Dmv MSDN 上的链接。  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>相关的任务  
[工作负荷管理任务](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
