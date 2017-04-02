---
title: "配置 max degree of parallelism 服务器配置选项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "并行查询 [SQL Server]"
  - "处理器 [SQL Server], 并行查询"
  - "用于并行查询的处理器数"
  - "max degree of parallelism 选项"
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 配置 max degree of parallelism 服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中配置 **max degree of parallelism (MAXDOP)** 服务器配置选项。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例在具有多个微处理器或 CPU 的计算机上运行时，它将为每个并行计划的执行检测最佳并行度（即运行一个语句所使用的处理器数）。 您可以使用 **max degree of parallelism** 选项来限制并行计划执行时所用的处理器数。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 考虑为查询、索引数据定义语言 (DDL) 操作、并行插入、联机更改列、并行统计信息集合以及静态的和由键集驱动的游标填充实施并行执行计划。
 

  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果 affinity mask 选项不设置为默认值，则可能会限制可用于对称多处理 (SMP) 系统上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的处理器数。  
  
###  <a name="Recommendations"></a> 建议  
  
-   此选项是一个高级选项，仅应由有经验的数据库管理员或认证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术人员更改。  
  
-   若要使服务器能够确定最大并行度，请将此选项设置为默认值 0。 若将 maximum degree of parallelism 设置为 0， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将能够使用至多 64 个可用的处理器。 若要取消生成并行计划，请将 **max degree of parallelism** 设置为 1。 将该值设置为 1 到 32,767 之间的数值来指定执行单个查询所使用的最大处理器核数。 如果指定的值比可用的处理器数大，则使用实际可用数量的处理器。 如果计算机只有一个处理器，将忽略 **max degree of parallelism** 值。  
  
-   您可以通过在查询语句中指定 MAXDOP 查询提示来覆盖查询中的 max degree of parallelism 值。 有关详细信息，请参阅[查询提示 (Transact-SQL)](../Topic/Query%20Hints%20\(Transact-SQL\).md)。  
  
-   索引操作（如创建或重新生成索引、或删除聚集索引）可能会大量占用资源。 您可以通过在索引语句中指定 MAXDOP 索引选项来覆盖索引操作的 max degree of parallelism 值。 MAXDOP 值在执行时应用于语句，但不存储在索引元数据中。 有关详细信息，请参阅[配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
-   除了查询和索引操作之外，此选项还控制 DBCC CHECKTABLE、DBCC CHECKDB 和 DBCC CHECKFILEGROUP 的并行。 使用跟踪标志 2528，可以禁用为这些语句所做的并行执行计划。 有关详细信息，请参阅[跟踪标志 (Transact-SQL)](../Topic/Trace%20Flags%20\(Transact-SQL\).md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要执行带两个参数的 **sp_configure** 以更改配置选项或运行 RECONFIGURE 语句，则用户必须具备 ALTER SETTINGS 服务器级别的权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 配置 max degree of parallelism 选项  
  
1.  在“对象资源管理器”中，右键单击服务器并选择“属性”。  
  
2.  单击 **“高级”** 节点。  
  
3.  在 **“最大并行度”** 框中，选择执行并行计划时所使用的最大处理器数。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 配置 max degree of parallelism 选项  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此示例说明如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 将 `max degree of parallelism` 选项的值配置为 `8`。  
  
```tsql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 8;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 有关详细信息，请参阅[服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
##  <a name="FollowUp"></a> 跟进：在配置 max degree of parallelism 选项之后  
 该设置将立即生效，无需重新启动服务器。  
  
## 另请参阅  
 [affinity mask 服务器配置选项](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [DBCC CHECKTABLE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [DBCC CHECKDB (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKFILEGROUP (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)   
 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md) 
 [查询提示 (Transact-SQL)](../Topic/Query%20Hints%20\(Transact-SQL\).md)    
 [设置索引选项](../../relational-databases/indexes/set-index-options.md)  
  
  