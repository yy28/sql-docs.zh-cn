---
title: 分析平台系统中的工作负荷管理 |Microsoft Docs
description: 分析平台系统中的工作负荷管理。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2281262c086f4d8dcab27debc8bb735ea5e8e1ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157471"
---
# <a name="workload-management-in-analytics-platform-system"></a>分析平台系统中的工作负荷管理

SQL Server PDW 工作负荷管理功能可让用户和管理员可以分配预设置配置的内存和并发的请求。 使用工作负荷管理请求能够相应的资源而无需永久耗尽的任何请求，从而提高工作负荷，一致或混合的性能。  
  
例如，使用 SQL Server PDW 中的工作负荷管理技术，你可以：  
  
-   分配大量的资源添加到加载作业。  
  
-   指定用于生成列存储索引的更多资源。  
  
-   解决遇到缓慢执行哈希联接以查看是否需要更多内存，以及将它提供更多的内存。  
  
## <a name="Basics"></a>工作负荷管理基础知识  
  
### <a name="key-terms"></a>主要术语  
工作负荷管理  
*工作负荷管理*是了解和调整系统资源使用状况，以便实现最佳性能，并发请求的能力。  
  
资源类  
在 SQL Server PDW*资源类*是具有预先分配的内存和并发限制的内置服务器角色。 SQL Server PDW 分配根据资源类服务器角色成员身份的提交请求的登录名的请求的资源。  
  
在计算节点上的资源类的实现在 SQL Server 中使用资源调控器功能。 有关资源调控器的详细信息，请参阅[资源调控器](../relational-databases/resource-governor/resource-governor.md)MSDN 上。  
  
### <a name="understand-current-resource-utilization"></a>了解当前资源利用率  
若要了解当前正在运行的请求的系统资源利用率，使用 SQL Server PDW 的动态管理视图。 例如，您可以使用 Dmv 来了解运行速度缓慢的大型哈希联接可以方面获益： 有更多的内存。  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>调整资源分配  
若要调整资源利用率，更改正在提交请求的登录名的资源类成员。 资源类服务器角色名为**mediumrc**， **largerc**，并**xlargerc**。 它们分别表示中型、 大型和超大型资源分配。  
  
例如，若要分配大量的系统资源的请求，添加提交到请求的登录名**largerc**服务器角色。 下面的 ALTER SERVER ROLE 语句将 Anna 的登录名添加到 largerc 服务器角色。  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>资源类说明  
下表描述了资源类和其系统资源分配。  
  
|资源类|请求重要性|最大内存使用情况 *|并发槽数 (最大 = 32)|Description|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|默认值|Medium|400 MB|1|默认情况下，每个登录名被允许的少量内存和并发为其请求的资源。<br /><br />当一个登录名添加到资源类时，新类将优先。 当所有资源类中删除的登录名时，该登录名会还原为默认资源分配。|  
|MediumRC|Medium|1200 MB|3|可能需要中等资源类的请求的示例：<br /><br />CTAS 操作具有大型的哈希联接。<br /><br />选择需要更多内存来避免缓存到磁盘的操作。<br /><br />将数据加载到聚集列存储索引。<br /><br />生成、 重新生成和重新组织聚集列存储索引的较小的表具有 10-15 列。|  
|Largerc|High|2.8 GB|7|可能需要大型资源类的请求的示例：<br /><br />具有巨大的哈希联接或包含大型的聚合，如大型的 ORDER BY 或 GROUP BY 子句的非常大 CTAS 操作。<br /><br />选择需要的内存量非常大的操作，如哈希联接或 ORDER BY 或 GROUP BY 子句之类的聚合的操作<br /><br />将数据加载到聚集列存储索引。<br /><br />生成、 重新生成和重新组织聚集列存储索引的较小的表具有 10-15 列。|  
|xlargerc|High|8.4 GB|22|特大资源类是对于可能需要在运行时的特大资源消耗的请求。|  
  
<sup>*</sup>最大内存使用情况是一个近似值。  
  
### <a name="request-importance"></a>请求重要性  
请求重要性映射到计算节点上运行的 SQL Server 将为请求提供的 CPU 时间量。  具有较高优先级请求接收更多的 CPU 时间。  
  
### <a name="maximum-memory-usage"></a>最大内存使用情况  
最大内存使用量是最大请求可使用每个处理空间内的可用内存量。 例如 mediumrc 请求可以使用最多为 1200 MB，每个分布区中进行处理。 它是以确保数据不为了避免需要执行的大部分工作的几个分布区倾斜仍然很重要。  
  
### <a name="concurrency-slots"></a>并发槽数  
分配 1、 3、 7 和 22 并发槽的目标是让大型和小型进程运行在同一时间，而不会阻止小进程运行大型的进程时。  例如，SQL Server PDW 可以分配最多 32 个并发槽在同一时间运行 1 个特大规模请求 （22 槽）、 1 个大型请求 （7 个插槽） 和 1 个中型请求 （3 个槽）。  
  
分配对并发请求最多 32 个并发槽的示例：  
  
-   28 槽 = 4 大  
  
-   30 槽 = 10 中  
  
-   32 个槽 = 32 的默认值  
  
-   32 个槽 = 1 特大规模 + 1 的大型 + 1 中  
  
-   32 个槽 = 2 的大 + 4 中等 + 6 的默认值  
  
假设 6 大型请求提交到 SQL Server PDW，然后提交 10 个默认请求。 SQL Server PDW 将处理按优先顺序的请求，如下所示：  
  
-   分配 28 并发槽，以开始处理 4 个大型请求，因为可用内存增多，并在队列中保留 2 个大型请求。  
  
-   分配 4 个并发槽，若要开始处理 4 默认请求并等待队列中保留 6 默认请求。  
  
在请求完成和并发槽可用时，SQL Server PDW 会分配剩余的请求根据可用资源和优先级。 例如，当存在 7 并发槽打开时，等待大型请求将具有 7 槽的优先级高于处于等待状态中的请求。  如果打开了 6 个插槽，SQL Server PDW 将分配 6 默认大小的更多请求。 但是，内存和并发槽所有之前必须可用 SQL Server PDW 允许运行的请求。  
  
在每个资源类中，请求在先进先出 (FIFO) 顺序运行。  
  
## <a name="GeneralRemarks"></a>一般备注  
如果登录名是多个资源类的成员，具有最多的资源类优先。  
  
在添加到或从资源类中删除登录名，更改将立即为所有将来的请求; 生效不会影响正在运行或等待当前请求。 该登录名不需要断开连接并重新连接在发生更改的顺序。  
  
对于每个登录名，资源类设置将应用于各个语句和操作，而不适用于该会话。  
  
SQL Server PDW 运行语句之前，它将尝试获取所需的请求的并发槽。 如果它无法获取足够的并发槽位，SQL Server PDW 会将请求移动到要执行的等待状态。 已分配给请求的所有资源系统都返回给系统中。  
  
大多数 SQL 语句始终需要默认的资源分配，并因此不由资源类控制。 例如，创建登录名仅需要少量的资源，而分配的默认资源，即使调用创建登录名的登录名是资源类的成员。  例如，如果 Anna 是 largerc 资源类的成员，她将提交的 CREATE LOGIN 语句 CREATE LOGIN 语句将用默认数量的资源运行。  
  
SQL 语句和资源类控制的操作：  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER 表重新生成  
  
-   创建聚集的索引  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CREATE REMOTE TABLE AS SELECT  
  
-   使用加载数据**dwloader**。  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   还原时在设备中具有多个计算节点还原的数据库。  
  
-   选择，不包括仅限 DMV 的查询  
  
## <a name="Limits"></a>限制和局限  
资源类控制内存和并发性分配。  不控制输入/输出操作。  
  
## <a name="Metadata"></a>元数据  
包含有关资源类和资源类成员的信息的 Dmv。  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
包含有关请求和所需的资源的状态信息的 Dmv:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
从 SQL Server Dmv 计算节点上公开的相关的系统视图。 请参阅[动态管理视图的 SQL Server](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)有关这些 Dmv MSDN 上的链接。  
  
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
  
