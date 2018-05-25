---
title: sys.dm_os_job_object （Azure SQL 数据库） |Microsoft 文档
ms.custom: ''
ms.date: 04/17/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 8ab408179388ca10821ad79e855e39fd3ec7eb01
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

返回单个行，描述用于管理 SQL Server 进程中，以及在作业对象级别某些资源消耗统计信息的作业对象的配置。 如果未在作业对象中运行 SQL Server，则返回空集。 

作业对象是一种 Windows 结构实现在操作系统级别的 CPU、 内存和 IO 资源调控。 有关作业对象的详细信息，请参阅[作业对象](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)。 

> [!NOTE]
> Sys.dm_os_job_object DMV 当前显示为 sys.dm_job_object 中。 这是临时：`sys.dm_os_job_object`将是此 DMV 的永久名称。 
  
|列|数据类型|Description|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|指定 SQL Server 线程可以使用每个计划的时间间隔内的处理器时钟周期数的部分。 10000 周期的计划间隔内可用的周期百分比报告的值。 例如，线程可以使用 CPU 内核值 100 表示是其完整的容量。|
|cpu_affinity_mask|**bigint**|描述哪些逻辑处理器的位掩码 SQL Server 进程可以使用处理器组中。 例如，cpu_affinity_mask 255 (1111 1111 以二进制形式) 意味着，前八个可以使用逻辑处理器。|
|cpu_affinity_group|**int**|SQL Server 使用的处理器组数。|
|memory_limit_mb|**bigint**|最大提交的内存，以 mb 为单位，在作业对象，包括 SQL Server 中的所有进程都可以都使用累积量。| 
|process_memory_limit_mb |**bigint**|已提交内存，以 mb 为单位，可以使用作业对象，例如 SQL Server 中的单个进程中最大的量。|
|workingset_limit_mb |**bigint**|最大内存，以 mb 为单位，可以使用 SQL Server 工作集量。|
|non_sos_mem_gap_mb|**bigint**|线程堆栈、 Dll、 和其他非 SOS 内存分配的内存，以 mb 为单位，量留出。 SOS 目标内存之间的区别是`process_memory_limit_mb`和`non_sos_mem_gap_mb`。| 
|low_mem_signal_threshold_mb|**bigint**|内存阈值，以 mb 为单位。 当为作业对象的可用内存量低于此阈值时，低内存通知信号是发送到 SQL Server 进程。 |
|total_user_time|**bigint**|在作业对象中的线程所用在用户模式下，自创建作业对象的 100 ns 计时周期的总数。 |
|total_kernel_time |**bigint**|在作业对象中的线程所用在内核模式下，自创建作业对象的 100 ns 计时周期的总数。 |
|write_operation_count |**bigint**|自创建作业对象颁发的 SQL Server 的本地磁盘上的 IO 操作写入的总次数。 |
|read_operation_count |**bigint**|自创建作业对象颁发的 SQL Server 的本地磁盘上的读取 IO 操作总数。 |
|peak_process_memory_used_mb|**bigint**|自创建作业对象以来，已使用的内存，以 mb 为单位，一个作业对象，例如 SQL Server 中处理的高峰量。| 
|peak_job_memory_used_mb|**bigint**|已创建的内存，单位为 MB，因为作业对象累积使用作业对象中的所有进程高峰量。|
  
## <a name="permissions"></a>权限  
在 SQL 数据库托管实例，需要`VIEW SERVER STATE`权限。 在 SQL 数据库上需要`VIEW DATABASE STATE`数据库中的权限。  
 
## <a name="see-also"></a>另请参阅  

托管实例的信息，请参阅[SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。
  
