---
title: "更改资源池 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_RESOURCE_POOL_TSQL
- ALTER RESOURCE POOL
dev_langs: TSQL
helpviewer_keywords: ALTER RESOURCE POOL
ms.assetid: 9c1c4cfb-0e3b-4f01-bf57-3fce94c7d1d4
caps.latest.revision: "47"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 357dab163aca094928f5c417c605dcb699c922b1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="alter-resource-pool-transact-sql"></a>ALTER RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中现有资源调控器的资源池配置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
ALTER RESOURCE POOL { pool_name | "default" }  
[WITH  
    ( [ MIN_CPU_PERCENT = value ]  
    [ [ , ] MAX_CPU_PERCENT = value ]   
    [ [ , ] CAP_CPU_PERCENT = value ]   
    [ [ , ] AFFINITY {
                        SCHEDULER = AUTO 
                      | ( <scheduler_range_spec> ) 
                      | NUMANODE = ( <NUMA_node_range_spec> )
                      }]   
    [ [ , ] MIN_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]   
    [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
    [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
)]   
[;]  
  
<scheduler_range_spec> ::=  
{SCHED_ID | SCHED_ID TO SCHED_ID}[,…n]  
  
<NUMA_node_range_spec> ::=  
{NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID}[,…n]  
```  
  
## <a name="arguments"></a>参数  
 { *pool_name* | **"default"** }  
 是现有用户定义资源池或安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时创建的默认资源池的名称。  
  
 与 ALTER RESOURCE POOL 一起使用时，"default" 必须用引号 ("") 引起来或用方括号 ([]) 括起来，以免与系统保留字 DEFAULT 冲突。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。  
  
> [!NOTE]  
>  预定义的工作负荷组和资源池全部使用小写字母的名称，例如"默认"。 对于使用区分大小写排序规则的服务器，应当注意这一点。 使用不区分大小写排序规则的服务器（例如 SQL_Latin1_General_CP1_CI_AS）会将“default”和“Default”视为相同。  
  
 MIN_CPU_PERCENT =*值*  
 指定在出现 CPU 争用时资源池中的所有请求保证能接收的平均 CPU 带宽。 *值*是一个整数，它默认设置为 0。 所允许的范围*值*是从 0 到 100 之间。  
  
 MAX_CPU_PERCENT =*值*  
 指定在存在 CPU 争用时资源池中的所有请求将接收的最大平均 CPU 带宽。 *值*是一个整数，它默认设置为 100。 所允许的范围*值*是从 1 到 100 之间。  
  
 CAP_CPU_PERCENT =*值*  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定资源池中的请求的目标最大 CPU 容量。 *值*是一个整数，它默认设置为 100。 所允许的范围*值*是从 1 到 100 之间。  
  
> [!NOTE]  
>  由于 CPU 监管的统计性质，你可能注意到偶尔峰值超过 CAP_CPU_PERCENT 中指定的值。  
  
 AFFINITY {SCHEDULER = AUTO | (Scheduler_range_spec) | NUMANODE = (NUMA_node_range_spec)}  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 将资源池附加到特定的计划程序。 默认值为 AUTO。  
  
 AFFINITY SCHEDULER = (Scheduler_range_spec) 将资源池映射到由给定 ID 标识的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划。 这些 Id 映射到 scheduler_id 列中的值[sys.dm_os_schedulers &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).  
  
 当您使用 AFFINITY NAMANODE = (NUMA_node_range_spec) 时，资源池关联到映射到物理 CPU 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划程序，而这些 CPU 与给定的一个 NUMA 节点或一系列节点相对应。 您可以使用下面的 Transact-SQL 查询发现物理 NUMA 配置与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划程序 ID 之间的映射。  
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc 
   ON osn.node_id = sc.parent_node_id 
      AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*值*  
 指定为此资源池保留的、不能与其他资源池共享的最小内存量。 *值*是一个整数，它默认设置为 0。 所允许的范围*值*是从 0 到 100 之间。  
  
 MAX_MEMORY_PERCENT =*值*  
 指定此资源池中的请求可使用的总服务器内存量。 *值*是一个整数，它默认设置为 100。 所允许的范围*值*是从 1 到 100 之间。  
  
 MIN_IOPS_PER_VOLUME =*值*  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定为资源池保留的每个磁盘卷每秒的最小 I/O 操作数 (IOPS)。 所允许的范围*值*为 0 到 2 ^31-1 (2,147,483,647)。 指定 0 表示池没有最小值阈值。  
  
 MAX_IOPS_PER_VOLUME =*值*  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定可用于该资源池的每个磁盘卷每秒的最大 I/O 操作数 (IOPS)。 所允许的范围*值*为 0 到 2 ^31-1 (2,147,483,647)。 指定 0 表示为池设置无限制的阈值。 默认值为 0。  
  
 如果池的 MAX_IOPS_PER_VOLUME 设置为 0，则该池根本不受管控，可以采用系统中的所有 IOPS，即使其他池设置了 MIN_IOPS_PER_VOLUME 也是如此。 对于这种情况，我们建议您在希望管控此池的 IO 时将此池的 MAX_IOPS_PER_VOLUME 值设置为较高的数字（例如，最大值 2^31-1）。  
  
## <a name="remarks"></a>注释  
 MAX_CPU_PERCENT 和 MAX_MEMORY_PERCENT 必须分别大于或等于 MIN_CPU_PERCENT 和 MIN_MEMORY_PERCENT。  
  
 如果可用，MAX_CPU_PERCENT 可以使用高于 MAX_CPU_PERCENT 值的 CPU 容量。 虽然可能有上面 CAP_CPU_PERCENT 的周期峰值，但是工作负荷更长时间，即使其他 CPU 容量，则可以应不超过 CAP_CPU_PERCENT。  
  
 每个关联组件（计划程序或 NUMA 节点）的总 CPU 百分比不应超过 100%。  
  
 建议您在熟悉资源调控器状态之后再执行 DDL 语句。 有关详细信息，请参阅[资源调控器](../../relational-databases/resource-governor/resource-governor.md)。  
  
 在执行 DBCC FREEPROCCACHE 后新设置时更改影响设置的计划，只会在以前缓存的计划生效 (*pool_name*)，其中*pool_name*是资源的名称调控器资源池。  
  
-   如果你正从多个计划程序切换地缘，到单个计划程序，执行 DBCC FREEPROCCACHE 不需要因为并行计划可以在串行模式下运行。 但是，它可能不是编译为串行计划的计划与一样有效。  
  
-   如果您要从单个计划程序更改关联，为多个计划程序，则不需要执行 DBCC FREEPROCCACHE。 但是，串行计划不能并行运行，以便清除相应的缓存将可能允许到新计划进行编译，并行度。  
  
> [!CAUTION]  
>  清除缓存的计划，从与多个工作负荷组关联的资源池将影响所有工作负荷组与用户定义的资源池由标识*pool_name*。  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例保留了 `default` 池的所有默认资源池设置，只有 `MAX_CPU_PERCENT` 除外，该设置更改为 `25`。  
  
```  
ALTER RESOURCE POOL "default"  
WITH  
     ( MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 在以下示例中，`CAP_CPU_PERCENT` 将硬性上限设置为 80%，并且 `AFFINITY SCHEDULER` 设置为单个值 8 以及 12 到 16 这个范围。  
  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
ALTER RESOURCE POOL Pool25  
WITH(   
     MIN_CPU_PERCENT = 5,  
     MAX_CPU_PERCENT = 10,       
     CAP_CPU_PERCENT = 80,  
     AFFINITY SCHEDULER = (8, 12 TO 16),   
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
);  
  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
