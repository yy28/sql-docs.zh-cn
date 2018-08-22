---
title: sys.dm_os_job_object （Azure SQL 数据库） |Microsoft Docs
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
ms.openlocfilehash: 673f1bffeea908da211cd5ff76bad9d96dabcded
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396057"
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

返回单个行，描述用于管理 SQL Server 进程，以及在作业对象级别某些资源使用情况统计信息的作业对象的配置。 如果未在作业对象中运行 SQL Server，则返回空集。 

作业对象是实现在操作系统级别的 CPU、 内存和 IO 资源调控的 Windows 构造。 有关作业对象的详细信息，请参阅[作业对象](/windows/desktop/ProcThread/job-objects)。 
  
|“列”|数据类型|Description|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|指定 SQL Server 线程可以在每个计划的间隔期间使用的处理器时钟周期数的部分。 报告的值是 10000 周期计划间隔内可用的周期的百分比。 例如，线程可以使用 CPU 内核值 100 表示是其完整的容量。|
|cpu_affinity_mask|**bigint**|SQL Server 进程可以使用处理器组中描述的逻辑处理器的位掩码。 例如，cpu_affinity_mask 255 (1111 二进制文件中) 表示的前八个逻辑处理器可用。|
|cpu_affinity_group|**int**|SQL Server 使用的处理器组数。|
|memory_limit_mb|**bigint**|最大提交内存，单位为 MB，作业对象，包括 SQL Server 中的所有进程可以都使用累积量。| 
|process_memory_limit_mb |**bigint**|最大单位为 MB，可以使用作业对象，如 SQL Server 中的单个进程的已提交内存量。|
|workingset_limit_mb |**bigint**|最大内存，单位为 MB，可以使用 SQL Server 工作集量。|
|non_sos_mem_gap_mb|**bigint**|线程堆栈、 Dll、 和其他非 SOS 内存分配留出的内存，以 mb 为单位量。 SOS 目标内存之间的区别是`process_memory_limit_mb`和`non_sos_mem_gap_mb`。| 
|low_mem_signal_threshold_mb|**bigint**|内存阈值，以 mb 为单位。 当为作业对象的可用内存量低于此阈值时，低内存通知信号发送到 SQL Server 进程。 |
|total_user_time|**bigint**|在该作业对象中的线程所用在用户模式下，由于创建的作业对象的 100 ns 计时周期的总数。 |
|total_kernel_time |**bigint**|在该作业对象中的线程所用在内核模式下，由于创建的作业对象的 100 ns 计时周期的总数。 |
|write_operation_count |**bigint**|写入以来创建的作业对象发出的 SQL Server 的本地磁盘上的 IO 操作总次数。 |
|read_operation_count |**bigint**|创建作业对象以来发出的 SQL Server 的本地磁盘上的读取 IO 操作的总数。 |
|peak_process_memory_used_mb|**bigint**|创建作业对象后，已使用的内存，单位为 MB，一个作业对象，如 SQL Server 中处理的最大资源量。| 
|peak_job_memory_used_mb|**bigint**|已创建的内存，单位为 MB，因为作业对象累积使用作业对象中的所有进程的最大资源量。|
  
## <a name="permissions"></a>Permissions  
在 SQL 数据库托管实例，都需要`VIEW SERVER STATE`权限。 在 SQL 数据库上需要`VIEW DATABASE STATE`数据库中的权限。  
 
## <a name="see-also"></a>请参阅  

有关托管实例的信息，请参阅[SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。
  
