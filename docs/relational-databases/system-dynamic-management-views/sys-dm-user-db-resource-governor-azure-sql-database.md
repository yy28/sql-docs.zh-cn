---
title: sys.dm_user_db_resource_governance (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governance
- sys.resource_governance_TSQL
- resource_governance
- resource_governance_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governance catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: bb4c43fa4193d9254d7f06f24bd903f974739e87
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2019
ms.locfileid: "58567633"
---
# <a name="sysdmuserdbresourcegovernance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

返回资源调控设置 Azure SQL 数据库数据库的配置和容量。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|ssNoversion|在 Azure SQL 数据库服务器中是唯一的数据库的 ID。|
|**logical_database_guid**|UNIQUEIDENTIFIER|用户数据库和用户数据库的生命周期中保持逻辑 guid。  重命名或将数据库设置为另一种 SLO 将不会更改 GUID。 |
|**physical_database_guid**|UNIQUEIDENTIFIER|该对话框保持用户数据库的物理实例的生命周期中的用户数据库的物理 guid。 设置为不同的 SLO 将导致更改此列。|
|**server_name**|NVARCHAR|逻辑服务器名称。|
|**database_name**|NVARCHAR|逻辑数据库名称。|
|**slo_name**|NVARCHAR|服务级别的目标和硬件生成。|
|**dtu_limit**|ssNoversion|数据库 (对于 vCore 为 NULL) 的 DTU 限制。|
|**cpu_limit**|ssNoversion|vCore 的数据库 (为 NULL 的 DTU 数据库) 的限制。|
|**min_cpu**|TINYINT|可由用户工作负荷的最小 CPU 百分比。|
|**max_cpu**|TINYINT|可由用户工作负荷的最大 CPU 百分比。|
|**cap_cpu**|TINYINT|用户工作负荷组的 CPU 百分比的上限。|
|**min_cores**|SMALLINT|使用 SQL 的 Cpu 数。|
|**max_dop**|SMALLINT|最大并行度由用户工作负荷。|
|**min_memory**|ssNoversion|可由用户工作负荷的最小内存百分比。|
|**max_memory**|ssNoversion|可由用户工作负荷的最大内存百分比。|
|**max_sessions**|ssNoversion|用户组的会话数限制。|
|**max_memory_grant**|ssNoversion|最大内存授予的每个查询中用户的工作负荷，以百分比表示。|
|**max_db_memory**|ssNoversion|用户数据库工作负荷的最大缓冲池内存上限|
|**govern_background_io**|bit|指示是否已将后台写入费用计入用户组。|
|**min_db_max_size_in_mb**|BIGINT|最小最大数据库文件大小，以 mb 为单位。|
|**max_db_max_size_in_mb**|BIGINT|最大最大数据库文件，以 mb 为单位。|
|**default_db_max_size_in_mb**|BIGINT|默认最大数据库文件大小，以 mb 为单位。|
|**db_file_growth_in_mb**|BIGINT|默认的 azure 数据库文件，以 mb 为单位的增长。|
|**initial_db_file_size_in_mb**|BIGINT|默认数据库文件大小，以 mb 为单位。|
|**log_size_in_mb**|BIGINT|默认日志文件大小，以 mb 为单位。|
|**instance_cap_cpu**|ssNoversion|在实例级别的 CPU 上限。|
|**instance_max_log_rate**|BIGINT|日志生成速率在实例级别，每秒字节数的上限。|
|**instance_max_worker_threads**|ssNoversion|在实例级别的工作线程限制。|
|**replica_type**|ssNoversion|辅助副本类型，其中 0 是主键和 1。|
|**max_transaction_size**|BIGINT|使用的任何事务，以 kb 为单位的最大日志空间。|
|**checkpoint_rate_mbps**|ssNoversion|检查点带宽 （以 mbps 为单位）。|
|**checkpoint_rate_io**|ssNoversion|检查点 IO 在 IOs 中每秒速率。|
|**last_updated_date_utc**|DATETIME|日期和时间的最后一个设置的更改或重新配置。|
|**primary_group_id**|ssNoversion|主要用户工作负荷组 id。|
|**primary_group_max_workers**|ssNoversion|主要用户的工作负荷组级别的辅助角色限制。|
|**primary_min_log_rate**|BIGINT|主要用户的工作负荷组级别的最小日志速率 （字节数 / 秒）。|
|**primary_max_log_rate**|BIGINT|主要用户的工作负荷组级别的最大日志速率 （字节数 / 秒）。|
|**primary_group_min_io**|ssNoversion|主要用户的工作负荷组级别的最小 IO。|
|**primary_group_max_io**|ssNoversion|主要用户的工作负荷组级别的最大 IO。|
|**primary_group_min_cpu**|FLOAT|最小 CPU 百分比限制在主要用户的工作负荷组级别。|
|**primary_group_max_cpu**|FLOAT|最大 CPU 百分比限制在主要用户的工作负荷组级别。|
|**primary_log_commit_fee**|ssNoversion|主要用户的工作负荷组级别的日志速率调控提交费用。|
|**primary_pool_max_workers**|ssNoversion|在主用户池级别的辅助角色限制。
|**pool_max_io**|ssNoversion|在主用户池级别的最大 IO 限制。|
|**govern_db_memory_in_resource_pool**|bit|指示是否在资源池级别控制的缓冲池的最大大小。 通常设置为弹性池内的数据库。|
|**volume_local_iops**|ssNoversion|每个本地卷 （例如 c:，d:） 的第二个 cap IOs。|
|**volume_managed_xstore_iops**|ssNoversion|每个远程存储帐户的第二个上限的 IOs。|
|**volume_external_xstore_iops**|ssNoversion|每个远程存储帐户由 Azure SQL DB 备份和遥测数据的第二个上限的 IOs。|
|**volume_type_local_iops**|ssNoversion|每个的所有本地卷的第二个上限的 IOs。|
|**volume_type_managed_xstore_iops**|ssNoversion|每个实例使用的所有远程存储帐户的第二个上限的 IOs。|
|**volume_type_external_xstore_iops**|ssNoversion|每个实例使用的 Azure SQL DB 备份和遥测数据的所有远程存储帐户的第二个上限的 IOs。|
|**volume_pfs_iops**|ssNoversion|每个高级文件存储的第二个上限的 IOs。|
|**volume_type_pfs_iops**|ssNoversion|每个实例使用的所有高级文件存储的第二个上限的 IOs。|
|||

## <a name="permissions"></a>权限

此视图需要拥有 VIEW DATABASE STATE 权限。

## <a name="remarks"></a>备注

用户可以访问资源调控配置此动态管理视图和设置 Azure SQL 数据库数据库的容量。 

> [!IMPORTANT]
> 此 dmv 显示的数据的大多数专供内部使用，可能会发生更改。

## <a name="examples"></a>示例

以下示例返回实例最大日志数据的速率按数据库服务器内的单个或共用数据库的数据库名称排序。

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>请参阅

- [事务日志速率调控](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [单一数据库 DTU 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [单个数据库的 vCore 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
