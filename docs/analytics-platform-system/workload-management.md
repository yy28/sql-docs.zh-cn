---
title: 工作负荷管理
description: 分析平台系统中的工作负荷管理。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d14714cb23a9f6b0d6cc63ddca5049cb6741017c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399447"
---
# <a name="workload-management-in-analytics-platform-system"></a>分析平台系统中的工作负荷管理

SQL Server PDW 的工作负荷管理功能，用户和管理员可以将请求分配给预先设置的内存配置和并发性。 使用工作负荷管理，通过允许请求拥有适当的资源，而无需从而使任何请求，从而提高工作负荷的性能。  
  
例如，通过 SQL Server PDW 中的工作负荷管理技术，可以：  
  
-   向加载作业分配大量资源。  
  
-   指定更多用于生成列存储索引的资源。  
  
-   排查速度较慢的哈希联接的问题，以查看它是否需要更多内存，并为其分配更多内存。  
  
## <a name="Basics"></a>工作负荷管理基础知识  
  
### <a name="key-terms"></a>主要术语  
工作负荷管理  
*工作负荷管理*是了解和调整系统资源利用率以便实现并发请求的最佳性能的能力。  
  
资源类  
在 SQL Server PDW 中，*资源类*是具有预先分配的内存和并发限制的内置服务器角色。 SQL Server PDW 根据提交请求的登录名的资源类服务器角色成员身份，将资源分配给请求。  
  
在计算节点上，资源类的实现使用 SQL Server 中的 Resource Governor 功能。 有关 Resource Governor 的详细信息，请参阅 MSDN 上的[Resource Governor](../relational-databases/resource-governor/resource-governor.md) 。  
  
### <a name="understand-current-resource-utilization"></a>了解当前资源利用率  
若要了解当前正在运行的请求的系统资源使用情况，请使用 SQL Server PDW 动态管理视图。 例如，你可以使用 Dmv 来了解运行速度较慢的大型哈希联接是否可以通过具有更多内存来受益。  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>调整资源分配  
若要调整资源利用率，请更改正在提交请求的登录名的资源类成员身份。 资源类服务器角色命名为**mediumrc**、 **largerc**和**xlargerc**。 它们分别表示中等、大和超大的大型资源分配。  
  
例如，若要将大量系统资源分配给请求，请将提交请求的登录名添加到**largerc**服务器角色。 以下 ALTER SERVER ROLE 语句将 login Anna 添加到 largerc 服务器角色。  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>资源类说明  
下表描述了资源类及其系统资源分配。  
  
|资源类|请求重要性|最大内存使用量 *|并发槽（最大 = 32）|说明|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|default|中型|400 MB|1|默认情况下，每个登录名都允许使用少量的内存和并发资源来处理其请求。<br /><br />将登录名添加到资源类后，新类优先。 从所有资源类中删除某个登录名后，该登录名将恢复为默认的资源分配。|  
|MediumRC|中型|1200 MB|3|可能需要中型资源类的请求示例：<br /><br />具有大型哈希联接的 CTAS 操作。<br /><br />选择需要更多内存以避免缓存到磁盘的操作。<br /><br />将数据加载到聚集列存储索引。<br /><br />为包含10-15 列的较小表生成、重新生成和重新组织聚集列存储索引。|  
|Largerc|高|2.8 GB|7|可能需要大型资源类的请求示例：<br /><br />非常大的 CTAS 操作，这些操作具有巨大的哈希联接，或包含大型聚合，如大的 ORDER BY 或 GROUP BY 子句。<br /><br />选择需要大量内存来执行哈希联接或聚合（如 ORDER BY 或 GROUP BY 子句）的操作<br /><br />将数据加载到聚集列存储索引。<br /><br />为包含10-15 列的较小表生成、重新生成和重新组织聚集列存储索引。|  
|xlargerc|高|8.4 GB|22|特大资源类适用于在运行时可能需要额外大资源消耗的请求。|  
  
<sup>*</sup>最大内存使用率是近似值。  
  
### <a name="request-importance"></a>请求重要性  
请求重要性映射到计算节点上运行的 SQL Server CPU 时间，将为请求分配。  优先级较高的请求接收更多的 CPU 时间。  
  
### <a name="maximum-memory-usage"></a>最大内存使用情况  
最大内存使用率是请求可在每个处理空间内使用的最大可用内存量。 例如，mediumrc 请求最多可使用 1200 MB 来处理每个分布。 务必要确保数据不会歪斜，以避免几个分发执行大部分工作。  
  
### <a name="concurrency-slots"></a>并发槽  
分配1、3、7和22并发槽的目标是允许同时运行大型和小型进程，而不会在运行大型进程时阻止小型进程。  例如，SQL Server PDW 可以分配最多32并发槽，以运行1个特大请求（22个槽）、1个大型请求（7个槽）和1个中型请求（3个槽）。  
  
将最多32并发槽分配给并发请求的示例：  
  
-   28个槽 = 4 个大  
  
-   30个槽 = 10 个中等  
  
-   32插槽 = 32 默认值  
  
-   32槽 = 1 个特大 + 1 大 + 1 中型  
  
-   32插槽 = 2 大 + 4 中等 + 6 默认  
  
假设有6个大请求提交到 SQL Server PDW，然后提交10个默认请求。 SQL Server PDW 将按优先级顺序处理请求，如下所示：  
  
-   分配28个并发槽，以便在内存可用时开始处理4个大型请求，并将两个大型请求保存在队列中。  
  
-   分配4个并发槽，开始处理4个默认请求并在等待队列中保留6个默认请求。  
  
当请求完成并且并发槽可用时，SQL Server PDW 会根据可用资源和优先级分配剩余请求。 例如，当打开7个并发槽时，等待大请求的优先级比等待中型请求的优先级高。  如果打开了6个槽，则 SQL Server PDW 将分配其他6个默认大小的请求。 但是，在 SQL Server PDW 允许运行请求之前，内存和并发槽必须全部可用。  
  
在每个资源类中，请求先以先进先出（FIFO）的顺序运行。  
  
## <a name="GeneralRemarks"></a>一般备注  
如果登录名是多个资源类的成员，则具有最多资源的类优先。  
  
当向资源类添加登录名或从中删除登录名时，更改会立即对所有将来的请求生效;当前正在运行或等待的请求不受影响。 登录无需断开连接和重新连接才能发生更改。  
  
对于每个登录名，资源类设置将应用于单个语句和操作，而不是应用于会话。  
  
在 SQL Server PDW 运行某个语句之前，它会尝试获取该请求所需的并发槽。 如果无法获取足够的并发槽，SQL Server PDW 会将请求移到等待执行的状态。 已分配给请求的所有资源系统都将返回到系统。  
  
大多数 SQL 语句始终需要默认资源分配，因此不受资源类控制。 例如，CREATE LOGIN 只需要少量的资源，并且即使登录名调用 CREATE LOGIN 是资源类的成员，也会分配默认资源。  例如，如果 Anna 是 largerc 资源类的成员，而她提交了 CREATE LOGIN 语句，则 CREATE LOGIN 语句将使用默认的资源数来运行。  
  
由资源类控制的 SQL 语句和操作：  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   创建聚集索引  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   创建远程表为 SELECT  
  
-   用**dwloader**加载数据。  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   删除  
  
-   还原到具有更多计算节点的设备时还原数据库。  
  
-   选择，排除仅 DMV 查询  
  
## <a name="Limits"></a>限制和限制  
资源类控制内存和并发分配。  它们不管理输入/输出操作。  
  
## <a name="Metadata"></a>新元  
Dmv，其中包含有关资源类和资源类成员的信息。  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
Dmv，其中包含请求的状态及其所需资源的信息：  
  
-   [sys. dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys. dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
从计算节点上 SQL Server Dmv 公开的相关系统视图。 请参阅 MSDN 上的[SQL Server 动态管理视图](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)以获取这些 dmv 的链接。  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys. dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>Related Tasks  
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
  
