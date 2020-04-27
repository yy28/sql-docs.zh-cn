---
title: 支持的 SQL Server 功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 660515f10797e1f11fac22c1baf4ed74e9f67c0c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63157242"
---
# <a name="supported-sql-server-features"></a>支持的 SQL Server 功能
  本主题讨论内存优化表支持或不支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
## <a name="ssnoversion-features-supported-for-in-memory-oltp"></a>内存中 OLTP 支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能  
 具有内存优化对象（包括内存优化文件组）的数据库支持以下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
 有关支持的数据类型的信息，请参阅 [Supported Data Types](supported-data-types-for-in-memory-oltp.md)。  
  
-   内存优化表支持的选项和操作。 有关详细信息，请参阅 [CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql)。  
  
-   本机编译存储过程支持的选项和操作。 有关详细信息，请参阅 [CREATE PROCEDURE (Transact-SQL)](/sql/t-sql/statements/create-procedure-transact-sql)。  
  
-   可使用解释型 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 访问内存优化表。 解释型 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 提供的外围应用等效于访问使用非本机编译存储过程和使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]的非内存优化表。 有关详细信息，请参阅[使用解释型 Transact-SQL 访问内存优化表](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)。  
  
-   多版本控制和积极并发控制。 有关详细信息，请参阅 [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md)。  
  
-   备份和还原包含内存优化数据文件组的数据库。 有关详细信息，请参阅 [SQL Server 数据库的备份和还原](../backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
-   目录视图、动态管理视图和可支持性扩展事件。 有关详细信息，请参阅[系统视图、存储过程、内存中 OLTP 的 DMV 和等待类型](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象。 有关详细信息，请参阅[对内存中 OLTP 的 SQL Server 管理对象支持](sql-server-management-objects-support-for-in-memory-oltp.md)。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 有关详细信息，请参阅[对内存中 OLTP 的 SQL Server Management Studio 支持](sql-server-management-studio-support-for-in-memory-oltp.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell。 有关详细信息，请参阅 [SQL Server PowerShell 概述](https://msdn.microsoft.com/library/cc281954\(SQL.105\).aspx)。  
  
-   使用 bcp 实用工具导入和导出大容量数据。 有关详细信息，请参阅[使用 bcp 实用工具导入和导出大容量数据 (SQL Server)](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)。  
  
-   崩溃恢复。  
  
-   内存优化数据文件组中有多个容器用于存储内存中 OLTP 对象和缩短恢复时间目标 (RTO)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务日志块计算校验并验证。  
  
-   新的 SNAPSHOT 表提示。 有关详细信息，请参阅[表提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-table)。  
  
-   DB COMPAT 级别。  
  
-   部分包含数据库。 支持 contained database authentication。 但是，在 DMV dm_db_uncontained_entities 中，所有内存中 OLTP 对象都被标记为“breaking containment”。  
  
-   Service broker，存在限制。 无法访问本机编译存储过程中的队列。 无法在访问内存优化表的事务中访问远程数据库中的队列。  
  
-   故障转移群集：作为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alwayson 产品/服务的一部分，Alwayson 故障转移群集实例利用 Windows Server 故障转移群集（WSFC）功能通过冗余在服务器实例级别（故障转移群集实例（FCI））提供本地高可用性。 有关详细信息，请参阅 [AlwaysOn 故障转移群集实例 (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
-   与 AlwaysOn 集成： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了几个为服务器或数据库打造高可用性的可选方案，包括 AlwaysOn。 有关详细信息，请参阅[高可用性解决方案 (SQL Server)](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)。  
  
-   日志传送：使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志传送，你可以自动将“主服务器”实例上“主数据库”内的事务日志备份发送到单独“辅助服务器”实例上的一个或多个“辅助数据库”。 有关详细信息，请参阅[关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
-   支持对订阅服务器上的内存优化表进行事务复制，不过有一些限制。 有关详细信息，请参阅[复制到内存优化表订阅服务器](../replication/replication-to-memory-optimized-table-subscribers.md)。  
  
-   资源调控器： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源调控器是一项可用于管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作负荷和系统资源使用情况的功能。 可以通过 Resource Governor 指定各种限制，对可供传入应用程序请求使用的 CPU、物理 IO 和内存量进行限制。 有关详细信息，请参阅 [Managing Memory for In-Memory OLTP](../../database-engine/managing-memory-for-in-memory-oltp.md) 和 [Resource Governor](../resource-governor/resource-governor.md)。  
  
-   内存中 OLTP 对于内存优化表中的 (var)char 列的支持代码页，以及在索引和本机编译存储过程中使用的支持的排序规则方面存在限制。 有关详细信息，请参阅 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。  
  
-   BACPAC 支持。  
  
## <a name="ssnoversion-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存中 OLTP 不支持的功能  
 具有内存优化对象（包括内存优化数据文件组）的数据库不支持以下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
|不支持的功能|功能说明|  
|-------------------------|-------------------------|  
|对内存优化表进行数据压缩。|您可以使用数据压缩功能帮助压缩数据库中的数据并帮助减小数据库的大小。 有关详细信息，请参阅 [Data Compression](../data-compression/data-compression.md)。|  
|对内存优化表和 HASH 索引进行分区。|已分区表和已分区索引的数据划分为分布于一个数据库中多个文件组的单元。 有关详细信息，请参阅 [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)。|  
|数据库的内存优化数据文件组上的透明数据加密 (TDE)。|“透明数据加密”(TDE) 可对数据和日志文件执行实时 I/O 加密和解密。 有关详细信息，请参阅[透明数据加密 (TDE)](../security/encryption/transparent-data-encryption.md)。<br /><br /> 可在拥有内存中 OLTP 对象的数据库上启用 TDE。 如果启用 TDE，则内存中 OLTP 日志记录会被加密。 即使在数据库上启用了 TDE，也不会对耐久性表的检查点文件加密。|  
|复制|对订阅服务器上内存优化表进行的事务复制之外的其他复制配置与引用内存优化表的表或视图不兼容。 如果存在内存优化的文件组，则不支持使用 sync_mode = ' database snapshot ' 的复制。 有关详细信息，请参阅[复制到内存优化表订阅服务器](../replication/replication-to-memory-optimized-table-subscribers.md)。|  
|多个活动的结果集 (MARS)|内存优化表不支持多个活动结果集 (MARS)。 此错误还可能指示使用了链接服务器。 链接服务器可以使用 MARS。 内存优化表不支持链接服务器。 请直接连接到内存优化的表所在的服务器和数据库。|  
|镜像|“数据库镜像”是一种提高 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库可用性的解决方案。 有关详细信息，请参阅[数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。|  
|重新生成日志|具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持通过附加或 ALTER DATABASE 重新生成日志。|  
|链接服务器|有关详细信息，请参阅 [链接服务器（数据库引擎）](../linked-servers/linked-servers-database-engine.md)。|  
|大容量日志记录|无论数据库处于什么恢复模式，都将始终完整记录针对持久内存优化表的所有操作的日志。|  
|最小日志记录|内存优化表不支持最小日志记录。 有关最小日志记录的详细信息，请参阅[事务日志 (SQL Server)](../logs/the-transaction-log-sql-server.md) 和[在批量导入中按最小方式记录日志的前提条件](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。|  
|更改跟踪|可在包含内存中 OLTP 对象的数据库上启用更改跟踪。 但是，在内存优化表上的更改不会被跟踪。|  
|DDL 触发器|内存中 OLTP 表和本机编译的存储过程不支持数据库级别和服务器级别的 DDL 触发器。|  
|变更数据捕获 (CDC)|不应在包含内存中 OLTP 对象的数据库上启用 CDC，因为它会阻止某些操作，如 DROP。|  
|数据库包含|包含本机编译存储过程和内存优化表的数据库不支持数据库包含。 有关详细信息，请参阅 [Contained Databases](../databases/contained-databases.md)|  
|上下文连接|不支持使用上下文连接从 CLR 存储过程内部访问内存优化表。|  
|游标|访问内存优化表的查询上的键集和动态游标。 这些查询将降级为静态（变成只读）。|  
|TABLESTAMP|不支持 TABLESTAMP。 有关详细信息，请参阅 [FROM (Transact-SQL)](/sql/t-sql/queries/from-transact-sql)。|  
|AUTO_CLOSE|不支持 AUTO_CLOSE。 有关详细信息，请参阅 [Set the AUTO_CLOSE Database Option to OFF](../policy-based-management/set-the-auto-close-database-option-to-off.md)。|  
|数据库快照|不支持数据库快照。 有关详细信息，请参阅[数据库快照 (SQL Server)](../databases/database-snapshots-sql-server.md)。|  
|事务性 DDL|内存中 OLTP 不支持事务性 DDL。|  
|事件通知|不支持事件通知。 有关详细信息，请参阅 [Event Notifications](../service-broker/event-notifications.md)。|  
|纤程模式|内存中 OLTP 不支持纤程模式。|  
|基于策略的管理 (PBM)。|不支持 PBM 的仅阻止并记录模式。 当服务器上存在此类策略时，可能会使内存中 OLTP DDL 无法成功执行。 支持“按需”和“按计划”模式。|  
|DACFX 部署/提取|内存中 OLTP 不支持 DAC Framework 部署/提取。|  
  
 除若干例外情况，一般不支持跨数据库事务。 下表介绍支持的情况和相应的限制。 （另请参阅 [跨数据库查询](cross-database-queries.md)。）  
  
|数据库|允许|说明|  
|---------------|-------------|-----------------|  
|用户数据库、模型和 msdb|否|不支持跨数据库查询和事务。<br /><br /> 访问内存优化表和本机编译存储过程的查询和事务无法访问其他数据库，但系统数据库 master（只读访问）和 tempdb 除外。|  
|资源数据库和 tempdb|是|除了单用户数据库外，仅使用资源数据库和 tempdb 的跨数据库事务亦不受限制。|  
|主|只读|如果针对内存中 OLTP 和 master 数据库的跨数据库事务包含针对 master 数据库的任意写入操作，则其将无法提交。 允许仅从 master 读取和仅使用一个用户数据库的跨数据库事务。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 对内存中 OLTP 的支持](sql-server-support-for-in-memory-oltp.md)  
  
  
