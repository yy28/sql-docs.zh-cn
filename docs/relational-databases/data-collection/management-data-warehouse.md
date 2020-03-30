---
title: 管理数据仓库 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], management data warehouse
- data warehouse
- management data warehouse
ms.assetid: 9874a8b2-7ccd-494a-944c-ad33b30b5499
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8723d9750eb03eda14a7983cba8919ea8e92eb81
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68133622"
---
# <a name="management-data-warehouse"></a>管理数据仓库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  管理数据仓库是一种关系数据库，其中包含从身为数据收集目标的服务器收集来的数据。 此数据用于生成系统数据收集组的报表，而且还可用于创建自定义报表。  
  
 数据收集器基础结构定义了实现保留策略所需的作业和维护计划，而保留策略是由数据库管理员定义的。  
  
> [!IMPORTANT]  
>  对于此版本的数据收集器，将使用简单恢复模式创建管理数据仓库以最小化日志记录。 您应当为自己的组织采取适当的恢复模式。  
  
## <a name="deploying-and-using-the-data-warehouse"></a>部署和使用数据仓库  
 可以将管理数据仓库安装到运行数据收集器的同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上。 但是，如果在所监视的服务器上存在服务器资源或性能问题，则可以在另一台计算机上安装管理数据仓库。  
  
 当您创建管理数据仓库时，将创建预定义系统收集组所需的架构及其对象。 创建的架构包括核心架构和快照架构，当创建用户定义的收集组并且该收集组包含使用一般 T-SQL 查询收集器类型的收集项时，将创建第三个架构 custom_snapshots。  
  
###### <a name="core-schema"></a>核心架构  
 核心架构描述用于组织和标识所收集数据的表、存储过程和视图。 这些表将由为各个收集器类型创建的所有数据表共享。 此架构已锁定，只有管理数据仓库数据库的所有者才可以修改。 此架构中的表的名称均包含前缀“core”。  
  
 下表介绍了核心架构中的数据库表。 这些数据库表使得数据收集器可以跟踪数据来自何处、谁插入的数据以及数据是什么时候上载至数据仓库的。  
  
|表名称|说明|  
|----------------|-----------------|  
|core.performance_counter_report_group_items|存储有关管理数据仓库报表应如何对性能计数器进行分组和聚合的信息。|  
|core.snapshots_internal|标识每个新快照。 只要上载包开始上载一批新数据，此表中即会插入新的一行。|  
|core.snapshot_timetable_internal|存储有关快照时间的信息。 快照时间将存储在单独的表中，因为几乎在同一时间可产生多个快照。|  
|core.source.info_internal|此表存储关于数据源的信息。 只要新收集组开始向数据仓库上载数据，此表即会更新。|  
|core.supported_collector_types_internal|包含可将数据上载到管理数据仓库的已注册收集器类型的 ID。 只有在更新仓库架构以支持新的收集器类型后，此表才会更新。 创建管理数据仓库时，将使用由数据收集器提供的收集器类型 ID 填充此表。|  
|core.wait_categories|包含用于根据 wait_type 特征对等待类型分组的类别。|  
|core.wait_types|包含数据收集器识别的等待类型。|  
|core.purge_info_internal|指示已请求停止从管理数据仓库中删除数据。|  
  
 上述表与收集器类型表一起使用，用于存储信息。 例如，一般 SQL 跟踪收集器类型使用下列表存储跟踪数据：  
  
-   core.source_info_internal  
  
-   core.snapshots_internal  
  
-   snapshots.trace_info  
  
-   snapshots.trace_data  
  
###### <a name="snapshots-schema"></a>快照架构  
 此快照架构描述了存储和维护由所提供的收集器类型收集的数据所需的对象。 此架构中的表已固定，在收集器类型的生存期内无需更改。 如需更改，则此架构仅可由 mdw_admin 角色的成员进行更改。 这些表是为了存储由系统数据收集组收集的数据而创建。  
  
 下表说明了“服务器活动”和“查询统计”收集组所需的管理数据仓库架构部分。  
  
-   系统级资源表  
  
    -   **snapshots.os_wait_stats**  
  
    -   **snapshots.os_latch_stats**  
  
    -   **snapshots.os_schedulers**  
  
    -   **snapshots.os_memory_clerks**  
  
    -   **snapshots.os_memory_nodes**  
  
    -   snapshots.sql_process_and_system_memory  
  
-   系统活动  
  
    -   snapshots.active_sessions_and_requests  
  
-   查询统计信息  
  
    -   snapshots.query_stats  
  
-   I/O 统计信息  
  
    -   **snapshots.io_virtual_file_stats**  
  
-   查询文本和计划  
  
    -   snapshots.notable_query_text  
  
    -   snapshots.notable_query_plan  
  
-   规范化的查询统计信息  
  
    -   snapshots.distinct_queries  
  
    -   snapshots.distinct_query_to_handle  
  
 **Custom_snapshots 架构**  
  
 custom_snapshots 架构描述当标准或第三方收集器类型用于创建用户定义的收集组时所创建的新表和新视图。 所有要求为收集项提供新数据表的收集器类型都可在此架构中创建该表。 在此架构中，可由 mdw_writer 角色的成员添加新表。 对此架构的任何其他更改仅可由 mdw_admin 角色的成员执行。  
  
 通过阅读有关各表相应的数据收集器存储过程的文档，您可获得有关数据库表列的数据类型和内容的详细信息。  
  
### <a name="best-practices"></a>最佳实践  
 使用管理数据仓库时，建议遵循以下最佳做法：  
  
-   除非添加新的收集器类型，否则不要更改管理数据仓库表的元数据。  
  
-   不要直接更改管理数据仓库中的数据。 更改收集的数据将使所收集数据的合法性失效。  
  
-   不要直接使用表，而应使用随数据收集器提供的已记录的存储过程和函数来访问实例和应用程序数据。 表名称和表定义可以更改，在您更新该应用程序时肯定会更改，在未来的版本中也可能更改。  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
|向“核心架构”部分增添了 core.performance_counter_report_group_items 表。|  
|更新了“快照架构”部分中表的列表。 增加了 snapshots.os_memory_clerks、snapshots.sql_process_and_system_memory 和 snapshots.io_virtual_file_stats。 删除了 snapshots.os_process_memory 和 snapshots.distinct_query_stats。|  
  
## <a name="see-also"></a>另请参阅  
 [管理数据仓库存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)   
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [数据收集](../../relational-databases/data-collection/data-collection.md)   
 [查看收集组报表 (SQL Server Management Studio)](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  
