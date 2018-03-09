---
title: "创建外部资源池 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
caps.latest.revision: 
author: jeannt
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb3da0f663ab67238c0eb133f66f465a62dcc970
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="create-external-resource-pool-transact-sql"></a>CREATE EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**适用于：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]和[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

创建用于定义外部进程的资源的外部池。 资源池表示数据库引擎实例的物理资源 （内存和 Cpu） 的一个子集。 数据库管理员可以使用资源调控器在多个资源池之间分发服务器资源，最多可为 64 个池。

+ 有关[!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]中[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]，外部池控制`rterm.exe`， `BxlServer.exe`，与它们生成的其他进程。

+ 有关[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]中[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]，外部池控制为 SQL Server 2016，列出的 R 进程，以及`python.exe`， `BxlServer.exe`，与它们生成的其他进程。

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = ( <NUMA_node_id> )   
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

*pool_name*  
是外部资源池的用户定义名称。 *pool_name*是字母数字，可以是最多为 128 个字符，必须是唯一的实例内[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，且必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  

MAX_CPU_PERCENT =*值*  
指定出现 CPU 争用时，可以接收外部资源池中所有请求的最大平均 CPU 带宽。 *值*是一个整数，它默认设置为 100。 所允许的范围*值*是从 1 到 100 之间。

相关性 {CPU = AUTO |( \<CPU_range_spec >) |NUMANODE = (\<NUMA_node_range_spec >)} 附加到特定的 Cpu 的外部资源池。 默认值为 AUTO。

相关性 CPU = **(** \<CPU_range_spec > **)**映射到外部资源池[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Cpu 由给定 CPU_IDs 标识。

当你使用相关性 NUMANODE = **(** \<NUMA_node_range_spec > **)**，外部资源池关联到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对应于给定的 NUMA 的物理 Cpu节点或节点的范围。 

MAX_MEMORY_PERCENT =*值*  
指定可由该外部资源池中的请求的总服务器内存。 *值*是一个整数，它默认设置为 100。 所允许的范围*值*是从 1 到 100 之间。

MAX_PROCESSES =*值*  
指定的最大允许外部资源池的进程数。 指定 0，则设置池，此后绑定只能由计算机的资源不受限制的阈值。 默认值为 0。

## <a name="remarks"></a>注释

[!INCLUDE[ssDE](../../includes/ssde-md.md)]实现资源池在执行时[ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md)语句。

 有关资源池的常规信息，请参阅[Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)， [sys.resource_governor_external_resource_pools &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)，和[sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).

特定于管理用于机器学习的外部资源池的信息，请参阅[SQL Server 中的机器学习的资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)。 

## <a name="permissions"></a>Permissions

需要 `CONTROL SERVER` 权限。

## <a name="examples"></a>示例

下面的语句定义外部池，将 CPU 使用率限制为 75%和 %到 30%的计算机上的可用内存的最大内存。

```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
  
## <a name="see-also"></a>另请参阅

 [启用了外部脚本的服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [ALTER 外部资源池 &#40;Transact SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [CREATE RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [sys.resource_governor_external_resource_pools (Transact SQL)](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
