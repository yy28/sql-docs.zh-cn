---
title: sys.databases _user_db_resource_governance (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
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
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: ea07ba28efc4ac50fdeef04bb1b3643c359ead28
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176253"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys.databases _user_db_resource_governance (Transact-sql)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

返回 Azure SQL 数据库数据库的资源调控配置和容量设置。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|INT|数据库的 ID, 在 Azure SQL 数据库服务器中是唯一的。|
|**logical_database_guid**|UNIQUEIDENTIFIER|用户数据库的逻辑 guid, 一直贯穿用户数据库的使用。  将数据库重命名或设置为其他 SLO 将不会更改 GUID。 |
|**physical_database_guid**|UNIQUEIDENTIFIER|用户数据库的物理 guid, 该 guid 贯穿用户数据库的物理实例。 设置为不同 SLO 将导致此列更改。|
|**server_name**|NVARCHAR|逻辑服务器名称。|
|**database_name**|NVARCHAR|逻辑数据库名称。|
|**slo_name**|NVARCHAR|服务级别目标和硬件生成。|
|**dtu_limit**|INT|数据库的 DTU 限制 (对于 vCore 为 NULL)。|
|**cpu_limit**|INT|数据库的 vCore 限制 (DTU 数据库为 NULL)。|
|**min_cpu**|TINYINT|用户工作负荷可以使用的最小 CPU 百分比。|
|**max_cpu**|TINYINT|用户工作负荷可以使用的最大 CPU 百分比。|
|**cap_cpu**|TINYINT|用户工作负荷组的 CPU 百分比上限。|
|**min_cores**|SMALLINT|SQL 使用的 Cpu 数。|
|**max_dop**|SMALLINT|用户工作负荷使用的最大并行度。|
|**min_memory**|INT|用户工作负荷可以使用的最小内存百分比。|
|**max_memory**|INT|用户工作负荷可以使用的最大内存百分比。|
|**max_sessions**|INT|用户组的会话限制。|
|**max_memory_grant**|INT|用户工作负荷中每个查询的最大内存授予百分比。|
|**max_db_memory**|INT|用户数据库工作负荷的最大缓冲池内存上限|
|**govern_background_io**|bit|指示是否向用户组收取后台写入费用。|
|**min_db_max_size_in_mb**|BIGINT|最小数据库文件大小 (以 MB 为单位)。|
|**max_db_max_size_in_mb**|BIGINT|最大数据库文件大小 (以 MB 为单位)。|
|**default_db_max_size_in_mb**|BIGINT|默认的最大数据库文件大小, 以 MB 为单位。|
|**db_file_growth_in_mb**|BIGINT|Azure 数据库文件的默认增长量 (以 MB 为单位)。|
|**initial_db_file_size_in_mb**|BIGINT|默认数据库文件大小 (以 MB 为单位)。|
|**log_size_in_mb**|BIGINT|默认日志文件大小 (MB)。|
|**instance_cap_cpu**|INT|实例级别的 CPU 上限。|
|**instance_max_log_rate**|BIGINT|实例级别的日志生成速率上限, 以每秒字节数为单位。|
|**instance_max_worker_threads**|INT|实例级别的工作线程限制。|
|**replica_type**|INT|副本类型, 其中0是主要副本, 1 为辅助副本。|
|**max_transaction_size**|BIGINT|任何事务使用的最大日志空间, 以 KB 为单位。|
|**checkpoint_rate_mbps**|INT|检查点带宽 (以 Mbps 为单位)。|
|**checkpoint_rate_io**|INT|每秒 Io 速率 (IO 速率)。|
|**last_updated_date_utc**|DATETIME|上次更改或重新配置设置的日期和时间。|
|**primary_group_id**|INT|主用户工作负荷组 ID。|
|**primary_group_max_workers**|INT|主用户工作负荷组级别的辅助角色限制。|
|**primary_min_log_rate**|BIGINT|主用户工作负荷组级别的最小日志速率 (每秒字节数)。|
|**primary_max_log_rate**|BIGINT|主用户工作负荷组级别的最大日志速率 (每秒字节数)。|
|**primary_group_min_io**|INT|主用户工作负荷组级别的最小 IO。|
|**primary_group_max_io**|INT|主用户工作负荷组级别的最大 IO 数。|
|**primary_group_min_cpu**|浮点数|主用户工作负荷组级别的最小 CPU 百分比限制。|
|**primary_group_max_cpu**|浮点数|主用户工作负荷组级别的最大 CPU 百分比限制。|
|**primary_log_commit_fee**|INT|主用户工作负荷组级别的日志费率调控承诺费。|
|**primary_pool_max_workers**|INT|主用户池级别的辅助角色限制。
|**pool_max_io**|INT|主用户池级别的最大 IO 限制。|
|**govern_db_memory_in_resource_pool**|bit|指示是否在资源池级别控制缓冲池的最大大小。 通常为弹性池中的数据库设置。|
|**volume_local_iops**|INT|本地卷的 IOs 每秒上限 (例如, C:, D:)。|
|**volume_managed_xstore_iops**|INT|远程存储帐户的每秒 Io 上限。|
|**volume_external_xstore_iops**|INT|Azure SQL 数据库备份和遥测使用的远程存储帐户的每秒 Io 上限。|
|**volume_type_local_iops**|INT|所有本地卷的每秒 Io 上限。|
|**volume_type_managed_xstore_iops**|INT|实例使用的所有远程存储帐户的每秒 Io 上限。|
|**volume_type_external_xstore_iops**|INT|针对 Azure SQL 数据库备份和实例的遥测使用的所有远程存储帐户的每秒 Io 上限。|
|**volume_pfs_iops**|INT|高级文件存储的每秒 Io 上限。|
|**volume_type_pfs_iops**|INT|实例使用的所有高级文件存储的每秒 Io 上限。|
|||

## <a name="permissions"></a>权限

此视图需要拥有 VIEW DATABASE STATE 权限。

## <a name="remarks"></a>备注

用户可以访问此动态管理视图, 以获取 Azure SQL 数据库数据库的资源调控配置和容量设置。 

> [!IMPORTANT]
> 此 DMV 提供的大多数数据都适用于内部使用, 并可能会发生更改。

## <a name="examples"></a>示例

下面的示例按数据库服务器在单个或共用数据库中按数据库名称排序的实例最大日志速率数据。

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>请参阅

- [事务日志速率管理](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [单个数据库 DTU 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [单一数据库 vCore 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
