---
title: sys.databases (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- databases
- databases_TSQL
- sys.databases
- sys.databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.databases catalog view
ms.assetid: 46c288c1-3410-4d68-a027-3bbf33239289
caps.latest.revision: 152
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b9280a340991982831b885416ef8512a127549b5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43073908"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中的每个数据库都包含一行。  
  
 如果数据库没有处于`ONLINE`，或`AUTO_CLOSE`设置为`ON`和数据库已关闭，某些列的值可能为`NULL`。 如果数据库处于`OFFLINE`，对应的行不是低权限的用户可见。 若要查看对应行，如果数据库处于`OFFLINE`，用户必须具有至少`ALTER ANY DATABASE`服务器级权限，或`CREATE DATABASE`中的权限`master`数据库。  
  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|数据库名称，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中或在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 服务器中是唯一的。|  
|**database_id**|**int**|数据库的 ID，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中或在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 服务器中是唯一的。|  
|**source_database_id**|**int**|Non-NULL = 该数据库快照的源数据库 ID。<br /> NULL = 非数据库快照。|  
|**owner_sid**|**varbinary(85)**|注册到服务器的数据库外部所有者的 SID（安全标识符）。 有关谁可以拥有数据库的信息，请参阅**数据库的 ALTER AUTHORIZATION**一部分[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)。|  
|**create_date**|**datetime**|数据库的创建或重命名日期。 有关**tempdb**，每次在服务器重新启动时更改此值。|  
|**compatibility_level**|**tinyint**|对应于兼容行为的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的整数：<br /> **值**:**适用于**<br /> 70:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 80:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 90:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /> 100:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 110:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 120:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 130:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] |  
|**collation_name**|**sysname**|数据库的排序规则。 作为数据库中的默认排序规则。<br /> NULL = 数据库未联机或 AUTO_CLOSE 设置为 ON 并且数据库已关闭。|  
|**user_access**|**tinyint**|用户访问设置：<br /> 0 = 已指定 MULTI_USER<br /> 1 = 已指定 SINGLE_USER<br /> 2 = 已指定 RESTRICTED_USER|  
|**user_access_desc**|**nvarchar(60)**|用户访问设置的说明。|  
|**is_read_only**|**bit**|1 = 数据库为 READ_ONLY<br /> 0 = 数据库为 READ_WRITE|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE 为 ON<br /> 0 = AUTO_CLOSE 为 OFF|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK 为 ON<br /> 0 = AUTO_SHRINK 为 OFF|  
|State|**tinyint**|**值&#124;适用于**<br /> 0 = ONLINE  <br /> 1 = RESTORING <br /> 2 = 正在恢复：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 3 = RECOVERY_PENDING:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 4 = SUSPECT  <br /> 5 = 紧急情况下：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 6 = 脱机：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 7 = 复制： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /> 10 = OFFLINE_SECONDARY: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /><br /> **注意：** 对于 Always On 的数据库，查询`database_state`或`database_state_desc`的列[sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)。|  
|**state_desc**|**nvarchar(60)**|数据库状态的说明。 请参阅状态。|  
|**is_in_standby**|**bit**|对于还原日志而言，数据库是只读的。|  
|**is_cleanly_shutdown**|**bit**|1 = 数据库完全关闭；在启动时不需要恢复<br /> 0 = 数据库并未完全关闭；在启动时需要恢复|  
|**is_supplemental_logging_enabled**|**bit**|1 = SUPPLEMENTAL_LOGGING 为 ON<br /> 0 = SUPPLEMENTAL_LOGGING 为 OFF|  
|**snapshot_isolation_state**|**tinyint**|允许的快照隔离事务状态，如 ALLOW_SNAPSHOT_ISOLATION 选项所设置：<br /> 0 = 快照隔离状态为 OFF（默认值）。 不允许使用快照隔离。<br /> 1 = 快照隔离状态为 ON。 允许使用快照隔离。<br /> 2 = 快照隔离状态正在转换到 OFF 状态。 所有事务都将其修改版本化。 无法使用快照隔离启动新的事务。 数据库仍保持向 OFF 状态转换，直到所有在执行 ALTER DATABASE 时处于活动状态的事务完成。<br /> 3 = 快照隔离状态正在转换到 ON 状态。 新事务都将其修改版本化。 在快照隔离状态变为 1 (ON) 之前，事务无法使用快照隔离。 数据库仍保持向 ON 状态转换，直到所有在执行 ALTER DATABASE 时处于活动状态的更新事务完成。|  
|**snapshot_isolation_state_desc**|**nvarchar(60)**|允许的快照隔离事务状态的说明，它由 ALLOW_SNAPSHOT_ISOLATION 选项设置。|  
|**is_read_committed_snapshot_on**|**bit**|1 = READ_COMMITTED_SNAPSHOT 选项为 ON。 read-committed 隔离级别下的读操作基于快照扫描，没有获取锁。<br /> 0 = READ_COMMITTED_SNAPSHOT 选项为 OFF（默认）。 read-committed 隔离级别下的读操作使用共享锁。|  
|**recovery_model**|**tinyint**|选定的恢复模式：<br /> 1 = FULL<br /> 2 = BULK_LOGGED<br /> 3 = SIMPLE|  
|**recovery_model_desc**|**nvarchar(60)**|选定的恢复模式的说明。|  
|**page_verify_option**|**tinyint**|PAGE_VERIFY 选项的设置：<br /> 0 = NONE<br /> 1 = TORN_PAGE_DETECTION<br /> 2 = CHECKSUM|  
|**page_verify_option_desc**|**nvarchar(60)**|PAGE_VERIFY 选项设置的说明。|  
|**is_auto_create_stats_on**|**bit**|1 = AUTO_CREATE_STATISTICS 为 ON<br /> 0 = AUTO_CREATE_STATISTICS 为 OFF|  
|**is_auto_create_stats_incremental_on**|**bit**|指示自动统计信息的增量选项的默认设置。<br /> 0 = 自动创建统计信息不是增量统计信息<br /> 1 = 如果可能，自动创建统计信息是增量统计信息<br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**is_auto_update_stats_on**|**bit**|1 = AUTO_UPDATE_STATISTICS 为 ON<br /> 0 = AUTO_UPDATE_STATISTICS 为 OFF|  
|**is_auto_update_stats_async_on**|**bit**|1 = AUTO_UPDATE_STATISTICS_ASYNC 为 ON<br /> 0 = AUTO_UPDATE_STATISTICS_ASYNC 为 OFF|  
|**is_ansi_null_default_on**|**bit**|1 = ANSI_NULL_DEFAULT 为 ON<br /> 0 = ANSI_NULL_DEFAULT 为 OFF|  
|**is_ansi_nulls_on**|**bit**|1 = ANSI_NULLS 为 ON<br /> 0 = ANSI_NULLS 为 OFF|  
|**is_ansi_padding_on**|**bit**|1 = ANSI_PADDING 为 ON<br /> 0 = ANSI_PADDING 为 OFF|  
|**is_ansi_warnings_on**|**bit**|1 = ANSI_WARNINGS 为 ON<br /> 0 = ANSI_WARNINGS 为 OFF|  
|**is_arithabort_on**|**bit**|1 = ARITHABORT 为 ON<br /> 0 = ARITHABORT 为 OFF|  
|**is_concat_null_yields_null_on**|**bit**|1 = CONCAT_NULL_YIELDS_NULL 为 ON<br /> 0 = CONCAT_NULL_YIELDS_NULL 为 OFF|  
|**is_numeric_roundabort_on**|**bit**|1 = NUMERIC_ROUNDABORT 为 ON<br /> 0 = NUMERIC_ROUNDABORT 为 OFF|  
|**is_quoted_identifier_on**|**bit**|1 = QUOTED_IDENTIFIER 为 ON<br /> 0 = QUOTED_IDENTIFIER 为 OFF|  
|**is_recursive_triggers_on**|**bit**|1 = RECURSIVE_TRIGGERS 为 ON<br /> 0 = RECURSIVE_TRIGGERS 为 OFF|  
|**is_cursor_close_on_commit_on**|**bit**|1 = CURSOR_CLOSE_ON_COMMIT 为 ON<br /> 0 = CURSOR_CLOSE_ON_COMMIT 为 OFF|  
|**is_local_cursor_default**|**bit**|1 = CURSOR_DEFAULT 为局部默认值<br /> 0 = CURSOR_DEFAULT 为全局默认值|  
|**is_fulltext_enabled**|**bit**|1 = 针对数据库启用全文<br /> 0 = 针对数据库禁用全文|  
|**is_trustworthy_on**|**bit**|1 = 数据库已标记为可信<br /> 0 = 数据库尚未标记为可信|  
|**is_db_chaining_on**|**bit**|1 = 跨数据库所有权链接为 ON<br /> 0 = 跨数据库所有权链接为 OFF|  
|**is_parameterization_forced**|**bit**|1 = 参数化为 FORCED<br /> 0 = 参数化为 SIMPLE|  
|**is_master_key_encrypted_by_server**|**bit**|1 = 数据库具有加密的主密钥<br /> 0 = 数据库没有加密的主密钥|  
|**is_query_store_on**|**bit**|1 = 查询存储是为此数据库启用。 检查[sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)若要查看查询存储状态。<br /> 0 = 查询存储未启用<br /> **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
|**is_published**|**bit**|1 = 数据库为事务复制拓扑或快照复制拓扑中的发布数据库<br /> 0 = 不是发布数据库|  
|**is_subscribed**|**bit**|未使用此列。 它将始终返回 0，而与数据库的订阅服务器状态无关。|  
|**is_merge_published**|**bit**|1 = 数据库为合并复制拓扑中的发布数据库<br /> 0 = 不是合并复制拓扑中的发布数据库|  
|**is_distributor**|**bit**|1 = 数据库为复制拓扑的分发数据库<br /> 0 = 不是复制拓扑的分发数据库|  
|**is_sync_with_backup**|**bit**|1 = 数据库标记为与备份进行复制同步<br /> 0 = 没有标记为与备份进行复制同步|  
|**service_broker_guid**|**uniqueidentifier**|该数据库的服务代理标识符。 用作**broker_instance**的路由表中的目标。|  
|**is_broker_enabled**|**bit**|1 = 该数据库中的代理当前正在发送和接收消息。<br /> 0 = 所有已发送的消息都会停留在传输队列中，已接收的消息不会置于该数据库的队列中。<br /> 默认情况下，还原的数据库或附加的数据库都禁用了代理。 与此相关的例外是数据库镜像，其中 Broker 在故障转移后启用。|  
|**log_reuse_wait**|**tinyint**|事务日志空间重用操作当前正在等待下列各最后一个检查点之一。 (有关更多详细说明这些值，请参阅[事务日志](../../relational-databases/logs/the-transaction-log-sql-server.md)。)<br /> 0 = 无<br />   1 = 检查点（当数据库使用恢复模式并且具有内存优化的数据文件组时，应看到 log_reuse_wait 列指示检查点或 xtp_checkpoint）。**适用于**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  2 = 日志备份**适用范围**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  3 = 活动备份或还原**适用范围**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  4 = 活动事务**适用范围**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  5 = 数据库镜像**适用范围**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  6 = 复制**适用范围**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  7 = 创建数据库快照**适用范围**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  8 = 日志扫描**适用于**<br />  9 = Alwayson 可用性组辅助副本正将此数据库的事务日志记录应用到相应的辅助数据库。 **适用于**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 在 SQL Server 的早期版本中，9 = 其他（暂时）。<br />  10 = 仅供内部使用**适用范围**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  11 = 仅供内部使用**适用范围**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 12 = 仅供内部使用**适用范围**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />13 = 最早的页面**适用范围**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 14 = 其他**适用范围**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  16 = XTP_CHECKPOINT（当数据库使用恢复模式并且具有内存优化的数据文件组时，应看到 log_reuse_wait 列指示检查点或 xtp_checkpoint）。**适用于**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**log_reuse_wait_desc**|**nvarchar(60)**|日志空间的重复使用正在等待最后一个检查点的描述。|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION 为 ON<br /> 0 = DATE_CORRELATION_OPTIMIZATION 为 OFF|  
|**is_cdc_enabled**|**bit**|1 = 对数据库启用变更数据捕获。 有关详细信息，请参阅[sys.sp_cdc_enable_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)。|  
|**is_encrypted**|**bit**|指示数据库是否加密（反映使用 ALTER DATABASE SET ENCRYPTION 子句最后设置的状态）。 可以是下列值之一：<br /> 1 = 已加密<br /> 0 = 未加密<br /> 有关数据库加密的详细信息，请参阅[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。<br /> 如果数据库正在解密过程中**is_encrypted**显示值为 0。 可以使用查看加密过程的状态[sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)动态管理视图。|  
|**is_honor_broker_priority_on**|**bit**|指示数据库是否遵守会话优先级（反映使用 ALTER DATABASE SET HONOR_BROKER_PRIORITY 子句最后设置的状态）。 可以是下列值之一：<br /> 1 = HONOR_BROKER_PRIORITY 为 ON<br /> 0 = HONOR_BROKER_PRIORITY 为 OFF|  
|**replica_id**|**uniqueidentifier**|数据库参与的可用性组（如果有）的本地 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]可用性副本的唯一标识符。<br /> NULL = 数据库不是可用性组中的可用性副本的一部分。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|Always On 可用性组内，如果任何数据库参与数据库的唯一标识符。 **group_database_id**是相同的主副本上以及在其的数据库是否联接到可用性组的每个辅助副本。<br /> NULL = 数据库不是任何可用性组中的可用性副本的一部分。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|映射到此数据库的资源池的 ID。 此资源池控制对该数据库中的内存优化表可用的总内存。<br /> 适用范围：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**default_language_lcid**|**smallint**|指示包含数据库的默认语言的本地 ID (lcid)。<br /> **请注意**充当[配置的默认语言服务器配置选项](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)的**sp_configure**。 此值是**null**非包含数据库。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|指示包含数据库的默认语言。<br /> 此值是**null**非包含数据库。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|指示包含数据库的默认全文语言的本地 ID (lcid)。<br /> **请注意**作为默认值[配置的默认全文语言服务器配置选项](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md)的**sp_configure**。 此值是**null**非包含数据库。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|指示包含数据库的默认全文语言。<br /> 此值是**null**非包含数据库。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|指示包含数据库中是否允许使用嵌套触发器。<br /> 0 = 不允许使用嵌套触发器<br /> 1 = 允许使用嵌套触发器<br /> **请注意**充当[配置 nested 的 triggers 服务器配置选项](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)的**sp_configure**。 此值是**null**非包含数据库。 请参阅[sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)有关的详细信息。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|指示是否应在包含数据库中转换干扰词。<br /> 0 = 不应转换干扰词。<br /> 1 = 应转换干扰词。<br /> **请注意**充当[transform noise words 服务器配置选项](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)的**sp_configure**。 此值是**null**非包含数据库。 请参阅[sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)有关的详细信息。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**two_digit_year_cutoff**|**smallint**|指示 1753 到 9999 之间的数字值，以表示将两位数的年份解释为四位数的年份的截止年份。<br /> **请注意**充当[配置 two digit year cutoff 服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)的**sp_configure**。 此值是**null**非包含数据库。 请参阅[sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)有关的详细信息。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**containment**|**tinyint 不为 null**|指示数据库的包含状态。<br />  0 = 数据库包含状态为 OFF。 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = 数据库处于部分包含状态**适用范围**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**containment_desc**|**nvarchar(60) 不为 null**|指示数据库的包含状态。<br /> NONE = 早期数据库（零包含）<br /> PARTIAL = 部分包含的数据库<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|恢复数据库的估计时间（秒）。 可以为 NULL。<br /> 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|延迟的持久性设置中：<br /> 0 = 已禁用<br /> 1 = 允许<br /> 2 = 强制<br /> 有关详细信息，请参阅[控制事务持续性](../../relational-databases/logs/control-transaction-durability.md)。<br /> **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|  
|**delayed_durability_desc**|**nvarchar(60)**|延迟的持久性设置中：<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> 适用范围：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /> **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**is_memory_optimized_elevate_to_snapshot_on**|**bit**|在会话设置 TRANSACTION ISOLATION LEVEL 设置为较低的隔离级别、READ COMMITTED 或 READ UNCOMMITTED 时，使用 SNAPSHOT 隔离访问内存优化表。<br /> 1 = 最低隔离级别为 SNAPSHOT。<br /> 0 = 隔离级别未进行提升。|  
|**is_federation_member**|**bit**|指示该数据库是否为联合的成员。<br /> 适用于：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|指示数据库是否延伸。<br /> 0 = 数据库不是已启用延伸的。<br /> 1 = 数据库处于已启用延伸的。<br /> 适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 有关详细信息，请参阅[Stretch Database](../../sql-server/stretch-database/stretch-database.md)。|  
|**is_mixed_page_allocation_on**|**bit**|指示是否在数据库中表和索引可以分配初始页从混合区。<br /> 0 = 表和数据库中的索引始终从统一区分配初始页。<br /> 1 = 表和数据库中的索引可以从混合区分配初始页。<br /> 适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 有关详细信息，请参阅的 SET MIXED_PAGE_ALLOCATION 选项[ALTER DATABASE SET 选项&#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。|  
|**is_temporal_retention_enabled**|**bit**|指示是否启用临时保留策略清除任务。<br /> **适用于**: Azure SQL 数据库|
|**catalog_collation_type**|**int**|目录排序规则设置：<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **适用于**: Azure SQL 数据库|
|**catalog_collation_type_desc**|**nvarchar(60)**|目录排序规则设置：<br />COLLATE<br />SQL_Latin_1_General_CP1_CI_AS<br /> **适用于**: Azure SQL 数据库|
  
## <a name="permissions"></a>Permissions  
 如果调用方`sys.databases`不是数据库的所有者，该数据库不是`master`或`tempdb`，查看对应行所需的最小权限`ALTER ANY DATABASE`或`VIEW ANY DATABASE`服务器级别权限，或者`CREATE DATABASE`中的权限`master`数据库。 始终可以在查看调用方连接到的数据库`sys.databases`。  
  
> [!IMPORTANT]  
>  默认情况下，公共角色具有`VIEW ANY DATABASE`权限，允许所有登录名查看数据库信息。 若要阻止登录名检测数据库的能力`REVOKE``VIEW ANY DATABASE`从权限`public`，或`DENY`单个登录名的 VIEW ANY DATABASE 权限。  
  
## <a name="includesssdsincludessssds-mdmd-remarks"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 备注  
 在中[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，此视图位于`master`数据库和用户数据库中。 在中`master`数据库，此视图返回的信息在`master`数据库和服务器上的所有用户数据库。 在用户数据库中，该视图仅返回有关当前数据库及 master 数据库的信息。  
  
 使用正在其中创建新数据库的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的 `master` 数据库中的 `sys.databases` 视图。 数据库复制开始后，可以查询`sys.databases`并`sys.dm_database_copies`视图从`master`要检索与复制进度有关的详细信息的目标服务器的数据库。  
  
## <a name="examples"></a>示例  
  
### <a name="a-query-the-sysdatabases-view"></a>A. 查询 sys.databases 视图  
 下面的示例返回列中提供的一部分`sys.databases`视图。  
  
```  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-includesssdsincludessssds-mdmd"></a>B. 检查 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中的复制状态  
 下面的示例查询`sys.databases`和`sys.dm_database_copies`视图以返回有关数据库的信息复制操作。  
  
**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
  
```  
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```  
### <a name="c-check-the-temporal-retention-policy-status-in-includesssdsincludessssds-mdmd"></a>C. 查看临时保留策略状态 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 下面的示例查询`sys.databases`是否启用了临时保留清理任务返回的信息。 请注意在还原操作之后，临时保留为默认情况下禁用。 使用`ALTER DATABASE`若要显式启用它。
  
适用于：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses (Transact-SQL)](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_recovery_status &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)   
 [数据库和文件目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [sys.dm_database_copies（Azure SQL 数据库）](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
  
  
