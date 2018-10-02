---
title: ALTER EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
author: HeidiSteen
ms.author: heidist
manager: cgronlund
ms.openlocfilehash: 3b6ef1bd5ea4c307ea8e2fc004e2d4dba815ba82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722455"
---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
适用范围：[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

更改一个 Resource Governor 外部池，该池用于指定外部进程可使用的资源。 

+ 对于 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 中的[!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]，外部池控制 `rterm.exe`、`BxlServer.exe` 以及它们生成的其他进程。

+ 对于 SQL Server 2017 中的[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]，外部池控制前一版本中列出的 R 进程以及 `python.exe`、`BxlServer.exe` 及它们生成的其他进程。

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>语法

```sql
ALTER EXTERNAL RESOURCE POOL { pool_name | "default" }
[ WITH (
    [ MAX_CPU_PERCENT = value ]
    [ [ , ] AFFINITY CPU =
            {
                AUTO
              | ( <cpu_range_spec> )
              | NUMANODE = (( <NUMA_node_id> )
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]
    [ [ , ] MAX_PROCESSES = value ]
    )
]
[ ; ]
  
<CPU_range_spec> ::=
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]
```  
  
## <a name="arguments"></a>参数

{ pool_name | "default" }  
现有用户定义外部资源池或安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时创建的默认外部资源池的名称。
与 `ALTER EXTERNAL RESOURCE POOL` 一起使用时，"default" 必须用引号 ("") 引起来或用方括号 ([]) 括起来，以免与系统保留字 `DEFAULT` 冲突。


MAX_CPU_PERCENT =value  
指定在存在 CPU 争用时外部资源池中的所有请求可以接收的最大平均 CPU 带宽。 value 为整数且默认设置为 100。 value 的允许范围是 1 到 100。


AFFINITY {CPU = AUTO | ( \<CPU_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)}  
将外部资源池附加到特定的 CPU。 默认值为 AUTO。

AFFINITY CPU = ( \<CPU_range_spec> ) 将外部资源池映射到给定 CPU_ID 标识的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU。 使用 AFFINITY NUMANODE = ( \<NUMA_node_range_spec> ) 时，外部资源池将关联到与给定 NUMA 节点或一系列节点相对应的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物理 CPU。


MAX_MEMORY_PERCENT =value  
指定此外部资源池中的请求可使用的总服务器内存量。 value 为整数且默认设置为 100。 value 的允许范围是 1 到 100。


MAX_PROCESSES =value  
指定外部资源池允许的最大进程数。 指定 0 以便为池设置无限阈值，此阈值之后仅受计算机资源约束。 默认值为 0。

## <a name="remarks"></a>Remarks

执行 [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) 语句时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]实现资源池。

有关资源池的常规信息，请参阅 [Resource Governor 资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)、[sys.resource_governor_external_resource_pools (Transact-SQL)](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 和 [sys.dm_resource_governor_external_resource_pool_affinity (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)。  

有关使用外部资源池管理机器学习作业的特定信息，请参阅 [SQL Server 中机器学习的资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)。
## <a name="permissions"></a>Permissions

需要 `CONTROL SERVER` 权限。

## <a name="examples"></a>示例

以下语句更改外部池，将 CPU 使用率限制为 50% 并将最大内存限制为计算机可用内存的 25%。
  
```sql
ALTER EXTERNAL RESOURCE POOL ep_1
WITH (
    MAX_CPU_PERCENT = 50
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 25
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>另请参阅

[SQL Server 中机器学习的资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)

[“已启用外部脚本”服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[CREATE EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

[DROP EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)

[ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)

[CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)

[资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

[ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
