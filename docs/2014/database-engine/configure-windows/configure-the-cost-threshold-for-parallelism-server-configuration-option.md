---
title: 配置“并行的开销阈值”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cost threshold for parallelism option
ms.assetid: dad21bee-fe28-41f6-9d2f-e6ababfaf9db
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6bf9890b05d0334b1a91561ce67e6acde18e1fe6
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639375"
---
# <a name="configure-the-cost-threshold-for-parallelism-server-configuration-option"></a>配置并行的开销阈值服务器配置选项
  本主题说明了如何使用 **或** 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中配置 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] “并行的开销阈值” [!INCLUDE[tsql](../../includes/tsql-md.md)]服务器配置选项。 **cost threshold for parallelism** 选项指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建和运行并行查询计划的阈值。 仅当运行同一查询的串行计划的估计开销高于在“并行的开销阈值”中设置的值时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 才创建和运行该查询的并行计划。 开销指的是在特定硬件配置中运行串行计划估计需要花费的时间（秒）。 **“并行的开销阈值”** 选项可设置为 0 到 32767 之间的任何值。 默认值为 5。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要配置并行的开销阈值选项，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：**[配置 cost threshold for parallelism 选项之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   开销指的是在特定硬件配置中运行串行计划估计需要花费的时间（秒）。 只能为对称多处理器设置 **cost threshold for parallelism** 。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将忽略 **或** 的值：  
  
    -   计算机只有一个逻辑处理器。  
  
    -   由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相关性掩码 **配置选项的原因，只有一个逻辑处理器可供** 使用。  
  
    -   **“最大并行度”** 选项设置为 1。  
  
 逻辑处理器是处理器硬件的基本单元，可让操作系统调度任务或执行线程上下文。 每个逻辑处理器一次只执行一个线程上下文。 处理器内核是提供解码和执行指令的能力的电路。 一个处理器内核可能包含一个或多个逻辑处理器。 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询可用于获取系统的 CPU 信息。  
  
```  
SELECT (cpu_count / hyperthread_ratio) AS PhysicalCPUs,   
cpu_count AS logicalCPUs   
FROM sys.dm_os_sys_info  
```  
  
###  <a name="Recommendations"></a> 建议  
  
-   此选项是一个高级选项，仅应由有经验的数据库管理员或认证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术人员更改。  
  
-   在某些情况下，即使查询的开销计划小于当前 **“并行的开销阈值”** 的值，也有可能选择并行计划。 出现这种情况，是因为使用并行还是串行计划是根据完成完全优化之前所提供的开销估计确定的。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要执行带两个参数的 **sp_configure** 以更改配置选项或运行 RECONFIGURE 语句，则用户必须具备 ALTER SETTINGS 服务器级别的权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-cost-threshold-for-parallelism-option"></a>配置并行的开销阈值选项  
  
1.  在对象资源管理器中，右键单击服务器并选择 **“属性”**。  
  
2.  单击 **“高级”** 节点。  
  
3.  在 **“并行”** 下，将 **“CostThresholdForParallelism”** 选项更改为所需值。 键入或选择一个值（介于 0 到 32767 之间）。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-cost-threshold-for-parallelism-option"></a>配置并行的开销阈值选项  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例说明如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 将 `cost threshold for parallelism` 选项的值设置为 `10`。  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cost threshold for parallelism', 10 ;  
GO  
RECONFIGURE  
GO  
```  
  
 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)版本的组合自动配置的最大工作线程数。  
  
##  <a name="FollowUp"></a> 跟进：配置 cost threshold for parallelism 选项之后  
 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>请参阅  
 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [查询提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-query)   
 [ALTER WORKLOAD GROUP (Transact-SQL)](/sql/t-sql/statements/alter-workload-group-transact-sql)   
 [affinity mask 服务器配置选项](affinity-mask-server-configuration-option.md)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
