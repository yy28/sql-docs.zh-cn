---
title: sys. dm_os_job_object （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 43063bb56607d1b5a21ae04b40ee4c7a17825521
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900137"
---
# <a name="sysdm_os_job_object-azure-sql-database"></a>sys.dm_os_job_object（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

返回单个行，用于描述管理 SQL Server 进程的作业对象的配置，以及作业对象级别的某些资源消耗统计信息。 如果 SQL Server 未在作业对象中运行，则返回空集。 

作业对象是一种在操作系统级别实现 CPU、内存和 IO 资源调控的 Windows 构造。 有关作业对象的详细信息，请参阅[作业对象](/windows/desktop/ProcThread/job-objects)。 
  
|列|数据类型|说明|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|指定在每个计划间隔期间 SQL Server 线程可以使用的处理器周期的部分。 此值在10000循环计划间隔内报告为可用循环的百分比。 例如，值100表示线程可使用 CPU 内核。|
|cpu_affinity_mask|**bigint**|一个位掩码，用于描述 SQL Server 进程可以在处理器组中使用的逻辑处理器。 例如，cpu_affinity_mask 255 （二进制文件 1111 1111）表示可以使用前8个逻辑处理器。|
|cpu_affinity_group|**int**|SQL Server 使用的处理器组的数目。|
|memory_limit_mb|**bigint**|作业对象中所有进程的最大提交内存量（以 MB 为单位），可以累积使用 SQL Server。| 
|process_memory_limit_mb |**bigint**|作业对象中的单个进程（例如 SQL Server）可以使用的最大提交内存量（以 MB 为单位）。|
|workingset_limit_mb |**bigint**|SQL Server 工作集可使用的最大内存量（以 MB 为单位）。|
|non_sos_mem_gap_mb|**bigint**|为线程堆栈、Dll 和其他非 SOS 内存分配留出的内存量（以 MB 为单位）。 SOS 目标内存是与`process_memory_limit_mb` `non_sos_mem_gap_mb`之间的差异。| 
|low_mem_signal_threshold_mb|**bigint**|内存阈值（以 MB 为单位）。 当作业对象的可用内存量低于此阈值时，会将内存不足通知信号发送到 SQL Server 进程。 |
|total_user_time|**bigint**|自作业对象创建以来，作业对象内的线程在用户模式下所用的 100 ns 计时周期总数。 |
|total_kernel_time |**bigint**|自作业对象创建以来，作业对象内的线程在内核模式下所用的总 100 ns 计时周期的总次数。 |
|write_operation_count |**bigint**|自创建作业对象以来 SQL Server 颁发的本地磁盘上的写入 IO 操作总数。 |
|read_operation_count |**bigint**|自创建作业对象之后 SQL Server 颁发的本地磁盘上的读取 IO 操作总数。 |
|peak_process_memory_used_mb|**bigint**|自创建作业对象以来，作业对象中单个进程使用的内存量（以 MB 为单位），例如 SQL Server。| 
|peak_job_memory_used_mb|**bigint**|自创建作业对象以来，作业对象中所有进程已累积使用的内存的最大内存量（以 MB 为单位）。|
  
## <a name="permissions"></a>权限  
在 SQL 数据库托管实例上， `VIEW SERVER STATE`需要权限。 在 SQL 数据库上，需要在数据库中拥有 `VIEW DATABASE STATE` 权限。  
 
## <a name="see-also"></a>另请参阅  

有关托管实例的信息，请参阅[SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。
  
