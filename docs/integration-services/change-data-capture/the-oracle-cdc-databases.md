---
title: Oracle CDC 数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a96486e9-f79b-4b24-bfaf-56203dd0e435
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6cce219b5e5d5d324e5e116bb9f55a931d7caaf8
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2020
ms.locfileid: "78339669"
---
# <a name="the-oracle-cdc-databases"></a>Oracle CDC 数据库

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  一个 Oracle CDC 实例与在目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上具有相同名称的一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库相关联。 此数据库称为 Oracle CDC 数据库（或 CDC 数据库）。  
  
 该 CDC 数据库使用 Oracle CDC 设计器控制台创建和配置并且包含以下元素：  
  
-   通过为 SQL Server CDC 启用数据库创建的 `cdc` 架构。  
  
-   Oracle CDC 实例使用的一组 **cdc.xdbcdc_xxxx** 表。  
  
-   一组空的镜像表，包含元组源 Oracle 数据库中捕获表的定义。  
  
-   一组由 SQL Server CDC 机制生成并且与在非 Oracle 的常规 SQL Server CDC 中使用的完全相同的一组更改表和更改访问函数。  
  
 `cdc` 架构最初只能由 **dbowner** 固定数据库角色的成员访问。 对更改表和更改函数的访问权限由与 SQL Server CDC 相同的安全模式确定。 有关安全模式的详细信息，请参阅 [安全模式](https://go.microsoft.com/fwlink/?LinkId=231151)。  
  
## <a name="creating-the-cdc-database"></a>创建 CDC 数据库  
 在大多数情况下，CDC 数据库是使用 CDC 设计器控制台创建的，但也可以使用通过 CDC 设计器控制台生成的 CDC 部署脚本创建 CDC 数据库。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员可根据需要更改数据库设置（对于用于存储、安全性或可用性之类的项）。  
  
 有关使用 CDC 设计器控制台创建数据库表和所需脚本的详细信息，请参阅 [使用新建实例向导](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)。  
  
## <a name="cdc-database-user-roles"></a>CDC 数据库用户角色  
 为 CDC 创建并启用 CDC 数据库时，将在该 CDC 数据库中创建一个名为 **cdc_service** 的数据库用户，该用户与用其配置 Oracle CDC 服务的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名关联。 该用户将成为 **db_datareader**、 **db_datawriter**和 **db_ddladmin** 数据库角色的成员。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名也与 `dbo` 用户相关联，则不会创建 **cdc_service** 。  
  
 此角色分配允许 Oracle CDC 服务使用捕获的数据和控制信息更新 `cdc` 架构下的表。  
  
 在创建 CDC 数据库和设置 CDC 源 Oracle 表时，CDC 数据库所有者可授予镜像表的 SELECT 权限并且定义 SQL Server CDC 访问控制角色以便控制谁可以访问更改数据。  
  
## <a name="mirror-tables"></a>镜像表  
 对于 Oracle 源数据库中的每个捕获表 \<架构名称>.\<表名称>，都将在 CDC 数据库中使用相同的架构和表名称创建一个类似的空表。 具有架构名称 `cdc` （不区分大小写）的 Oracle 源表无法捕获，因为 `cdc` 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架构是为 SQL Server CDC 保留的。  
  
 镜像表是空的；在其中不存储任何数据。 它们用于启用 Oracle CDC 实例使用的标准 SQL Server CDC 基础结构。 为了防止数据插入或更新到镜像表中，对于 PUBLIC 将拒绝所有 UPDATE、DELETE 和 INSERT 操作。 这将确保不能修改镜像表。  
  
## <a name="access-to-change-data"></a>访问更改数据  
 由于用于获取对与某一捕获实例相关联的更改数据库的访问权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全模式，必须向用户授予对关联镜像表的所有捕获列的 `select` 访问权限（对原始 Oracle 表的访问权限不提供对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中更改表的访问权限）。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全模式的信息，请参阅 [安全模式](https://go.microsoft.com/fwlink/?LinkId=231151)。  
  
 此外，如果在创建捕获实例时指定了访问控制角色，调用者还必须是指定访问控制角色的成员。 所有数据库用户可通过 PUBLIC 角色访问用于访问元数据的其他常规变更数据捕获功能，但返回的元数据访问通常是使用基础源表的选择访问权限以及任何定义的访问控制角色成员身份控制的。  
  
 可通过调用在创建捕获实例时 SQL Server CDC 组件生成的特殊的基于表的函数，读取更改数据。 有关此函数的详细信息，请参阅 [变更数据捕获函数 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152)。  
  
 通过 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CDC 源组件访问 CDC 数据受到相同规则的约束。  
  
## <a name="the-cdc-database-tables"></a>CDC 数据库表  
 本节介绍 CDC 数据库中的以下表。  
  
-   [更改表 (_CT)](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_Change_Tables_CT)  
  
-   [cdc.lsn_time_mapping](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdclsn_time_mapping)  
  
-   [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config)  
  
-   [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state)  
  
-   [cdc.xdbcdc_trace](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_trace)  
  
-   [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions)  
  
###  <a name="BKMK_Change_Tables_CT"></a> 更改表 (_CT)  
 更改表是从镜像表创建的。 它们包含从 Oracle 数据库捕获的更改数据。 根据以下约定命名这些表：  
  
 [cdc].[\<capture-instance>_CT]   
  
 在最初为表 `<schema-name>.<table-name>`启用捕获时，默认捕获实例名称为 `<schema-name>_<table-name>`。 例如，Oracle HR.EMPLOYEES 表的默认捕获实例名称为 HR_EMPLOYEES，而关联的更改表为 [cdc]。 [HR_EMPLOYEES_CT]。  
  
 捕获表由 Oracle CDC 实例写入。 使用在创建捕获实例时由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的特殊表值函数读取捕获表。 例如，`fn_cdc_get_all_changes_HR_EMPLOYEES` 。 有关这些 CDC 函数的详细信息，请参阅 [变更数据捕获函数 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152)。  
  
###  <a name="BKMK_cdclsn_time_mapping"></a> cdc.lsn_time_mapping  
 **[cdc].[lsn_time_mapping]** 表由 SQL Server CDC 组件生成。 它在 Oracle CDC 情况下的用法与其常规用法不同。  
  
 对于 Oracle CDC，在此表中存储的 LSN 值基于与更改相关联的 Oracle 系统更改号 (SCN) 值。 该 LSN 值的前 6 个字节是原始 Oracle SCN 号。  
  
 此外，在使用 Oracle CDC 时，时间列（`tran_begin_time` 和 `tran_end_time`）存储更改的 UTC 时间而非本地时间，就像它对待常规 SQL Server CDC 一样。 这可以确保夏时制时间更改不会影响存储在 lsn_time_mapping 中的数据。  
  
###  <a name="BKMK_cdcxdbcdc_config"></a> cdc.xdbcdc_config  
 此表包含 Oracle CDC 实例的配置数据。 它是使用 CDC 设计器控制台更新的。 该表仅具有一行。  
  
 下表介绍了 **cdc.xdbcdc_config** 表的各列。  
  
|Item|说明|  
|----------|-----------------|  
|版本|它跟踪 CDC 实例配置的版本。 在每次更新表时，以及在每次添加新的捕获实例或删除现有捕获实例时，将更新该项。|  
|connect_string|Oracle 连接字符串。 下面是一个基本示例：<br /><br /> `<server>:<port>/<instance>` （例如 `erp.contoso.com:1521/orcl`）。<br /><br /> 连接字符串还可以指定 Oracle Net 连接描述符，例如 `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`。<br /><br /> 如果使用目录服务器或 tnsnames，则连接字符串可以是连接的名称。<br /><br /> 有关 Oracle 连接字符串的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkId=231153](https://go.microsoft.com/fwlink/?LinkId=231153)，其中介绍了针对 Oracle CDC 服务使用的 Oracle Instant Client 的 Oracle 数据库连接字符串的详细信息。|  
|use_windows_authentication|可以取以下值的布尔值：<br /><br /> **0**：提供 Oracle 用户名和密码进行身份验证（默认值）<br /><br /> **1**：使用 Windows 身份验证连接到 Oracle 数据库。 只有当 Oracle 数据库配置为使用 Windows 身份验证时，才可以使用此选项。|  
|username|日志挖掘 Oracle 数据库用户的名称。 **仅当 use_windows_authentication = 0**时，该值才是必填的。|  
|password|日志挖掘 Oracle 数据库用户的密码。 **仅当 use_windows_authentication = 0**时，该值才是必填的。|  
|transaction_staging_timeout|未提交的 Oracle 事务保留在内存中的时间（秒），超过该时间后，这些事务将写入 **cdc.xdbcdc_staged_transactions** 表。 默认值为 120 秒。|  
|memory_limit|可用于在内存中缓存数据的内存量的限制 (Mb)。 较低的设置将导致更多事务写入 **cdc.xdbcdc_staged_transactions** 表。 默认值为 50 Mb。|  
|选项|name[=value][; ] 形式的选项的列表 - 用于指定辅助选项（例如跟踪、优化）。 有关可用选项的说明，请参阅下表。|  
  
 下表介绍了可用的选项。  
  
|名称|默认|Min|Max|静态|说明|  
|----------|-------------|---------|---------|------------|-----------------|  
|跟踪|False|-|-|False|可用值有：<br /><br /> True<br /><br /> False<br /><br /> on<br /><br /> 关闭|  
|cdc_update_state_interval|10|1|120|False|为某一事务分配的内存块的大小（一个事务可分配多个块）(KB)。 请参阅 [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config) 表中的 memory_limit 列。|  
|target_max_batched_transactions|100|1|1000|True|可在 SQL Server CT 表更新中作为一个事务处理的 Oracle 事务的最大数目。|  
|target_idle_lsn_update_interval|10|0|1|False|用于在捕获表没有任何活动时更新 **lsn_time_mapping** 表的时间间隔（秒）。|  
|trace_retention_period|24|1|24*31|False|时间量（在跟踪表中保存消息的小时数）。|  
|sql_reconnect_interval|2|2|3600|False|在重新连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]前等待的时间量（秒）。 此时间间隔与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端的连接超时一起使用。|  
|sql_reconnect_limit|-1|-1|-1|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新连接的最大数目。 默认值为 -1，表示进程在停止前将一直尝试重新连接。|  
|cdc_restart_limit|6|-1|3600|False|在大多数情况下，CDC 服务将自动重新启动异常结束的 CDC 实例。 此属性定义每小时失败多少次后服务将停止重新启动实例。 值 -1 表示应始终重新启动实例。<br /><br /> 服务将在对配置表的任何更新后返回到重新启动实例。|  
|cdc_memory_report|0|0|1000|False|如果更改了该参数的值，CDC 实例将在跟踪表上打印其内存报告。|  
|target_command_timeout|600|1|3600|False|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时的命令超时。|  
|source_character_set|-|-|-|True|可设置为使用特定的 Oracle 编码，而非使用 Oracle 数据库代码页。 这在所使用的字符数据的实际编码方式不同于 Oracle 数据库代码页所表示的方式时很有用。|  
|source_error_retry_interval|30|1|3600|False|在因若干错误（例如连接错误或在系统表之间暂时丢失同步）而重试之前使用。|  
|source_prefetch_size|100|1|10000|True|预提取批处理的大小。|  
|source_max_tables_in_query|100|1|10000|True|切换到读取 Oracle 日志而不进行表筛选之前 WHERE 子句中的表的最大数目。|  
|source_read_retry_interval|2|1|3600|False|源在尝试再次读取 EOF 上的 Oracle 事务日志之前等待的时间。|  
|source_reconnect_interval|30|1|3600|False|等待多长时间后将尝试重新连接到源数据库（秒）。|  
|source_reconnect_limit|-1|-1||False|源数据库重新连接的最大数目。 默认值为 -1，表示进程在停止前将一直尝试重新连接。|  
|source_command_timeout|30|1|3600|False|使用 Oracle 时的连接超时。|  
|source_connection_timeout|30|1|3600|False|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时的连接超时。|  
|trace_data_errors|True|-|-|False|布尔值。 **True** 指示记录数据转换和截断错误。|  
|CDC_stop_on_breaking_schema_changes|False|-|-|False|布尔值。 **True** 指示当检测到中断的架构更改时停止。<br /><br /> **False** 指示删除镜像表和捕获实例。|  
|source_oracle_home||-|-|False|可设置为 CDC 实例将用于连接到 Oracle 的特定 Oracle 主页路径或 Oracle 主页名称。|  
  
###  <a name="BKMK_cdcxdbcdc_state"></a> cdc.xdbcdc_state  
 此表包含与 Oracle CDC 实例的持久化状态有关的信息。 该捕获状态用于恢复和故障转移情况以及用于运行状况监视。  
  
 下表介绍了 **cdc.xdbcdc_state** 表的各列。  
  
|Item|说明|  
|----------|-----------------|  
|status|用于当前 Oracle CDC 实例的当前状态代码。 该状态描述 CDC 的当前状态。|  
|sub_status|提供有关当前状态的其他信息的第二级状态。|  
|活动|可以取以下值的布尔值：<br /><br /> **0**：Oracle CDC 实例进程处于不活动状态。<br /><br /> **1**：Oracle CDC 实例进程处于活动状态。|  
|error|可以取以下值的布尔值：<br /><br /> **0**：Oracle CDC 实例进程未处于错误状态。<br /><br /> **1**：Oracle CDC 实例处于错误状态。|  
|status_message|提供错误或状态的说明的字符串。|  
|timestamp|具有上次更新捕获状态的时间 (UTC) 的时间戳。|  
|active_capture_node|当前正运行 Oracle CDC 服务和 Oracle CDC 实例（正在处理 Oracle 事务日志）的主机（该主机可以是群集上的节点）的名称。|  
|last_transaction_timestamp|具有事务上次写入更改表的时间 (UTC) 的时间戳。|  
|last_change_timestamp|具有从源 Oracle 事务日志读取最近更改记录的时间 (UTC) 的时间戳。 此时间戳有助于标识 CDC 进程的当前延迟。|  
|transaction_log_head_cn|从 Oracle 事务日志读取的最近更改号 (CN)。|  
|transaction_log_tail_cn|Oracle CDC 实例在重新启动或恢复时重新定位到的 Oracle 事务日志上的更改号 (CN)。|  
|current_cn|源数据库中已知的最新更改号 (CN)。|  
|software_version|Oracle CDC 服务的内部版本。|  
|completed_transactions|自上次重置 CDC 以来处理的事务的数目。|  
|written_changes|写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更改表的更改记录的数目。|  
|read_changes|从源 Oracle 事务日志读取的更改记录的数目。|  
|staged_transactions|**cdc.xdbcdc_staged_transactions** 表中暂存的当前处于活动状态的事务数目。|  
  
###  <a name="BKMK_cdcxdbcdc_trace"></a> cdc.xdbcdc_trace  
 此表包含与 CDC 实例的操作有关的信息。 此表中存储的信息包括错误记录、显著的状态更改和跟踪记录。 错误信息还写入 Windows 事件日志，以便确保在 **cdc.xcbcdc_trace** 表不可用时提供这些信息。  
  
 下表描述 cdc.xdbcdc_trace 表的各列。  
  
|Item|说明|  
|----------|-----------------|  
|timestamp|写入跟踪日志时的准确 UTC 时间戳。|  
|type|包含以下值之一。<br /><br /> ERROR<br /><br /> INFO<br /><br /> TRACE|  
|节点|写入记录的节点的名称。|  
|status|状态表使用的状态代码。|  
|sub_status|状态表使用的子状态代码。|  
|status_message|状态表使用的状态消息。|  
|data|在错误或跟踪记录包含负载（例如，损坏的日志记录）时的附加数据。|  
  
###  <a name="BKMK_cdcxdbcdc_staged_transactions"></a> cdc.xdbcdc_staged_transactions  
 此表存储在捕获事务提交或回滚事件前大型或长时间运行的事务的更改记录。 Oracle CDC 服务首先按事务提交时间、然后按各事务的时间顺序对捕获的日志记录进行排序。 在事务结束前同一事务的日志记录将存储在内存中，然后写入目标更改表或被放弃（在回滚时）。 因为只有有限的可用内存量，所以，大型事务将在事务完成前写入 **cdc.xdbcdc_staged_transactions** 表。 事务还会在长时间运行时写入临时表。 因此，在 Oracle CDC 实例重新启动时，无需从 Oracle 事务日志重新读取旧的更改。  
  
 下表介绍了 **cdc.xdbcdc_staged_transactions** 表的各列。  
  
|Item|说明|  
|----------|-----------------|  
|transaction_id|要暂存的事务的唯一事务标识符。|  
|seq_num|当前事务的 **xcbcdc_staged_transactions** 行的编号（从 0 开始）。|  
|data_start_cn|此行中数据的第一个更改的更改号 (CN)。|  
|data_end_cn|此行中数据的最后一个更改的更改号 (CN)。|  
|data|事务的 BLOB 形式的暂存的更改。|  
  
## <a name="see-also"></a>另请参阅  
 [Change Data Capture Designer for Oracle by Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)  
  
  
