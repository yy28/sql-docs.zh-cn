---
title: CREATE RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE RESOURCE POOL
- RESOURCE POOL
- CREATE_RESOURCE_POOL_TSQL
- RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE RESOURCE POOL
ms.assetid: 82712505-c6f9-4a65-a469-f029b5a2d6cd
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 229aa2bc153efbe7b77e1e0490b6d506df82f598
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="create-resource-pool-transact-sql"></a>CREATE RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建资源调控器资源池。 资源池表示数据库引擎实例的部分物理资源（内存、CPU 和 IO）。 数据库管理员可以使用资源调控器在多个资源池之间分发服务器资源，最多可为 64 个池。 资源调控器并非在每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中都提供。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
CREATE RESOURCE POOL pool_name  
[ WITH  
    (  
        [ MIN_CPU_PERCENT = value ]  
        [ [ , ] MAX_CPU_PERCENT = value ]   
        [ [ , ] CAP_CPU_PERCENT = value ]   
        [ [ , ] AFFINITY {SCHEDULER =  
                  AUTO 
                | ( <scheduler_range_spec> )   
                | NUMANODE = ( <NUMA_node_range_spec> )
                } ]   
        [ [ , ] MIN_MEMORY_PERCENT = value ]  
        [ [ , ] MAX_MEMORY_PERCENT = value ]  
        [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
        [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
    )   
]  
[;]  
  
<scheduler_range_spec> ::=  
{ SCHED_ID | SCHED_ID TO SCHED_ID }[,…n]  
  
<NUMA_node_range_spec> ::=  
{ NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID }[,…n]  
```  
  
## <a name="arguments"></a>参数  
 pool_name  
 资源池的用户定义名称。 pool_name 由字母数字组成，最多可包含 128 个字符，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中必须是唯一的，并且必须符合[标识符](../../relational-databases/databases/database-identifiers.md)规则。  
  
 MIN_CPU_PERCENT = value  
 指定在出现 CPU 争用时资源池中的所有请求保证能接收的平均 CPU 带宽。 value 为整数且默认设置为 0。 value 的允许范围是 0 到 100。  
  
 MAX_CPU_PERCENT = value  
 指定存在 CPU 争用时，资源池中的所有请求将接收的最大平均 CPU 带宽。 value 为整数且默认设置为 100。 value 的允许范围是 1 到 100。  
  
 CAP_CPU_PERCENT = value  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定资源池中的所有请求都将收到的 CPU 带宽硬性上限。 将 CPU 最大带宽级别限制为与指定值相同。 value 为整数且默认设置为 100。 value 的允许范围是 1 到 100。  
  
 AFFINITY {SCHEDULER = AUTO | ( \<scheduler_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)} 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 将资源池附加到特定的计划程序。 默认值为 AUTO。  
  
 AFFINITY SCHEDULER = **(** \< Scheduler_range_spec **)** 将资源池映射到由给定 ID 标识的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划。 这些 ID 映射到 [sys.dm_os_schedulers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md) 的 scheduler_id 列中的值。 
  
 当使用 AFFINITY NUMANODE = (\<NUMA_node_range_spec> ) 时，资源池关联到映射至物理 CPU 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划程序，而这些 CPU 与给定的一个 NUMA 节点或一系列节点相对应。 您可以使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询发现物理 NUMA 配置与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划程序 ID 之间的映射。 
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc   
    ON osn.node_id = sc.parent_node_id   
    AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT = value  
 指定为此资源池保留的、不能与其他资源池共享的最小内存量。 value 为整数，默认设置为 0，value 的允许范围为 0 到 100。  
  
 MAX_MEMORY_PERCENT =value  
 指定此资源池中的请求可使用的总服务器内存量。 value 为整数且默认设置为 100。 value 的允许范围是 1 到 100。  
  
 MIN_IOPS_PER_VOLUME = value  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定为资源池保留的每个磁盘卷每秒的最小 I/O 操作数 (IOPS)。 value 的允许范围是 0 到 2^31-1 (2,147,483,647)。 指定 0 表示池没有最小值阈值。 默认值为 0。  
  
 MAX_IOPS_PER_VOLUME = value  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定可用于该资源池的每个磁盘卷每秒的最大 I/O 操作数 (IOPS)。 value 的允许范围是 0 到 2^31-1 (2,147,483,647)。 指定 0 表示为池设置无限制的阈值。 默认值为 0。  
  
 如果池的 MAX_IOPS_PER_VOLUME 设置为 0，则该池根本不受管控，可以采用系统中的所有 IOPS，即使其他池设置了 MIN_IOPS_PER_VOLUME 也是如此。 对于这种情况，我们建议您在希望管控此池的 IO 时将此池的 MAX_IOPS_PER_VOLUME 值设置为较高的数字（例如，最大值 2^31-1）。  
  
## <a name="remarks"></a>Remarks  
 MIN_IOPS_PER_VOLUME 和 MAX_IOPS_PER_VOLUME 指定每秒的最小和最大的读取或写入数。 这些读取或写入可以是任何大小，并且不指示最小或最大流量。  
  
 MAX_CPU_PERCENT 和 MAX_MEMORY_PERCENT 的值必须分别大于或等于 MIN_CPU_PERCENT 和 MIN_MEMORY_PERCENT 的值。  
  
 CAP_CPU_PERCENT 不同于 MAX_CPU_PERCENT，这是因为与池关联的工作负荷可以使用 MAX_CPU_PERCENT 值之上的 CPU 容量（如果可用），但不能超过 CAP_CPU_PERCENT 的值。  
  
 每个关联组件（计划程序或 NUMA 节点）的总 CPU 百分比不应超过 100%。  
  
## <a name="permissions"></a>权限  
 需要 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何创建名为 `bigPool` 的资源池。 此池使用默认的资源调控器设置。  
  
```  
CREATE RESOURCE POOL bigPool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 以下示例将 `CAP_CPU_PERCENT` 的硬性上限设置为 30%，并将 `AFFINITY SCHEDULER` 的范围设置为 0 到 63、128 到 191。 
  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
     MIN_CPU_PERCENT = 10,  
     MAX_CPU_PERCENT = 20,  
     CAP_CPU_PERCENT = 30,  
     AFFINITY SCHEDULER = (0 TO 63, 128 TO 191),  
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
      );  
  
```  
  
 以下示例设置将 `MIN_IOPS_PER_VOLUME` 设置为 \<某个值>，并将 `MAX_IOPS_PER_VOLUME` 设置为 \<某个值>。 这些值控制可用于资源池的物理 I/O 读取和写入操作。  
  
**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
    MIN_IOPS_PER_VOLUME = 20,  
    MAX_IOPS_PER_VOLUME = 100  
      );  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [创建资源池](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
  

