---
title: "内存中 OLTP 不支持的 SQL Server 功能 | Microsoft Docs"
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
caps.latest.revision: 55
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e1b1d4a26616fe83a241267bc87b9e799d883e26
ms.lasthandoff: 04/11/2017

---
# <a name="unsupported-sql-server-features-for-in-memory-oltp"></a>内存中 OLTP 不支持的 SQL Server 功能
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主题讨论不支持用于内存优化对象的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存中 OLTP 不支持的功能  
 具有内存优化对象（包括内存优化数据文件组）的数据库不支持以下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
|不支持的功能|功能说明|  
|-------------------------|-------------------------|  
|对内存优化表进行数据压缩。|您可以使用数据压缩功能帮助压缩数据库中的数据并帮助减小数据库的大小。 有关详细信息，请参阅 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
|对内存优化表和 HASH 索引以及非聚集索引进行分区。|已分区表和已分区索引的数据划分为分布于一个数据库中多个文件组的单元。 有关详细信息，请参阅 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。|  
|复制|对订阅服务器上内存优化表进行的事务复制之外的其他复制配置与引用内存优化表的表或视图不兼容。 如果存在内存优化文件组，则不支持使用 sync_mode=’database snapshot’ 的复制。 有关详细信息，请参阅 [复制到内存优化表订阅服务器](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)。|  
|镜像|具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持数据库镜像。 有关镜像的详细信息，请参阅[数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。|  
|重新生成日志|具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持通过附加或 ALTER DATABASE 重新生成日志。|  
|链接服务器|不能在与内存优化表相同的查询或事务中访问链接服务器。 有关详细信息，请参阅[链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)。|  
|大容量日志记录|无论数据库处于什么恢复模式，都将始终完整记录针对持久内存优化表的所有操作的日志。|  
|最小日志记录|内存优化表不支持最小日志记录。 有关最小日志记录的详细信息，请参阅[事务日志 (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md) 和[在大容量导入中按最小方式记录日志的前提条件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。|  
|更改跟踪|可在包含内存中 OLTP 对象的数据库上启用更改跟踪。 但是，在内存优化表上的更改不会被跟踪。|  
|DDL 触发器|内存中 OLTP 表和本机编译的模块不支持数据库级别和服务器级别的 DDL 触发器。|  
|变更数据捕获 (CDC)|CDC 不能与具有内存优化表的数据库一起使用，因为它在后台使用 DROP TABLE 的 DDL 触发器。|  
|纤程模式|内存优化表不支持纤程模式：<br /><br /> 如果纤程模式处于活动状态，则不能创建具有内存优化文件组的数据库，也不能向现有数据库添加内存优化文件组。<br /><br /> 如果有包含内存优化文件组的数据库，可以启用纤程模式。 不过，启用纤程模式需要重新启动服务器。 在这种情况下，具有内存优化文件组的数据库将无法恢复，您还会看到一条错误消息，建议您禁用纤程模式以使用具有内存优化文件组的数据库。<br /><br /> 纤程模式启用时，附加和恢复具有内存优化文件组的数据库会失败。 数据库将标记为可疑。<br /><br /> <br /><br /> 有关详细信息，请参阅 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。|  
|Service Broker 的限制|无法访问本机编译存储过程中的队列。<br /><br /> 无法在访问内存优化表的事务中访问远程数据库中的队列。|  
|在订阅服务器上复制|支持对订阅服务器上的内存优化表进行事务复制，不过有一些限制。 有关详细信息，请参阅 [复制到内存优化表订阅服务器](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)|  
  
 除若干例外情况，一般不支持跨数据库事务。 下表介绍支持的情况和相应的限制。 （另请参阅 [跨数据库查询](../../relational-databases/in-memory-oltp/cross-database-queries.md)。）  
  
|“数据库”|Allowed|说明|  
|---------------|-------------|-----------------|  
|用户数据库、模型和 msdb。|是|不支持跨数据库查询和事务。<br /><br /> 访问内存优化表和本机编译存储过程的查询和事务无法访问其他数据库，但系统数据库 master（只读访问）和 tempdb 除外。|  
|资源数据库, tempdb|是|除了单用户数据库外，仅使用资源数据库和 tempdb 的跨数据库事务亦不受限制。|  
|master|只读|如果针对内存中 OLTP 和 master 数据库的跨数据库事务包含针对 master 数据库的任意写入操作，则其将无法提交。 允许仅从 master 读取和仅使用一个用户数据库的跨数据库事务。|  
  
## <a name="scenarios-not-supported"></a>不支持的方案  
  
-   内存中 OLTP 不支持数据库包含（[包含的数据库](../../relational-databases/databases/contained-databases.md)）。 支持 contained database authentication。 但是，在 DMV dm_db_uncontained_entities 中，所有内存中 OLTP 对象都被标记为“breaking containment”。  
  
-   使用上下文连接从 CLR 存储过程内部访问内存优化表。  
  
-   访问内存优化表的查询上的键集和动态游标。 这些游标将降级为静态和只读的。  
  
-   “将 **MERGE INTO***目标*用于*目标*”是内存优化表。 内存优化表支持 **MERGE USING** 源。  
  
-   不支持 ROWVERSION (TIMESTAMP) 数据类型。 有关详细信息，请参阅 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)。  
  
-   具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持自动关闭。  
  
-   具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持数据库快照。  
  
-   事务性 DDL。 用户事务内部不支持内存中 OLTP 对象的 CREATE/ALTER/DROP。  
  
-   事件通知。  
  
-   基于策略的管理 (PBM)。 不支持 PBM 的仅阻止并记录模式。 当服务器上存在此类策略时，可能会使内存中 OLTP DDL 无法成功执行。 支持“按需”和“按计划”模式。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 对内存中 OLTP 的支持](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  

