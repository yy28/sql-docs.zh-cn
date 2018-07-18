---
title: ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/142018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 811376d76608af8d75ab68649f0eea61bfb8a5c3
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36249809"
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  此语句在单个数据库级别启用多个数据库配置设置。 此语句可用于 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] 以及 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和更高版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这些设置包括：  
  
- 清除过程缓存。  
- 根据最适合特定主数据库的情况，将 MAXDOP 参数设置为该数据库的任意值（1、2、…），为使用的所有辅助数据库（例如，针对报告查询）设置不同的值（例如 0）。  
- 设置独立于数据库兼容级别的查询优化器基数估计模型。  
- 在数据库级别启用或禁用参数探查。
- 在数据库级别启用或禁用查询优化修补程序。
- 在数据库级别启用或禁用标识缓存。
- 在第一次编译批处理时启用或禁用要存储在缓存中的已编译计划存根。  
- 启用或禁用对本机编译的 T-SQL 模块的执行统计信息收集。
- 对支持 ONLINE= 语法的 DDL 语句启用或禁用“默认联机”选项。
- 对支持 RESUMABLE= 语法的 DDL 语句启用或禁用“默认可恢复”选项。 

 ![链接图标](../../database-engine/configure-windows/media/topic-link.gif "链接图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ALTER DATABASE SCOPED CONFIGURATION  
{        
     {  [ FOR SECONDARY] SET <set_options>  }    
}  
| CLEAR PROCEDURE_CACHE  
| SET < set_options >
[;]    
  
< set_options > ::=    
{  
    MAXDOP = { <value> | PRIMARY}    
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}    
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}    
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
    | OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }
    | XTP_PROCEDURE_EXECUTION_STATISTICS = { ON | OFF } 
    | XTP_QUERY_EXECUTION_STATISTICS = { ON | OFF }    
    | ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED } 
    | ELEVATE_RESUMABLE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }  
}  
```  
  
## <a name="arguments"></a>参数  
 
FOR SECONDARY  
 
指定辅助数据库的设置（所有辅助数据库必须具有相同的值）。  
  
MAXDOP **=** {\<value> | PRIMARY }  
**\<value>**  
  
指定应用于该语句的默认 MAXDOP 设置。 0 是默认值，表示将改用服务器配置。 数据库范围的 MAXDOP 会替代（除非设置为 0）通过 sp_configure 在服务器级别设置“max degree of parallelism”。 查询提示仍然可以替代 DB 作用域内 MAXDOP，以调整需要不同设置的特定查询。 所有这些设置都受为工作负荷组设置的 MAXDOP 限制。   

您可以使用 max degree of parallelism 选项来限制并行计划执行时所用的处理器数。 SQL Server 考虑为查询、索引数据定义语言 (DDL) 操作、并行插入、联机更改列、并行统计信息集合以及静态的和由键集驱动的游标填充实施并行执行计划。
 
要在实例级别设置此选项，请参阅[配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 

> [!TIP] 
> 要在查询级别完成此操作，请添加 MAXDOP [查询提示](../../t-sql/queries/hints-transact-sql-query.md)。  
  
PRIMARY  
  
仅可为辅助数据库（该数据库位于主数据库上）设置，表示其配置是为主数据库设置的配置。 如果主数据库的配置更改，辅助数据库上的值也会相应地更改，不需要再显式设置辅助数据库值。 PRIMARY 是辅助数据库的默认设置。  
  
LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY }  

可用于独立于数据库兼容性级别将查询优化器基数估计模型设置为 SQL Server 2012 或更低版本。 默认值为 OFF，可根据数据库兼容性级别设置查询优化器基数估计模型。 将此值设置为 ON 等效于启用[跟踪标志 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 

> [!TIP] 
> 要在查询级别完成此操作，请添加 QUERYTRACEON [查询提示](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 开始，要在查询级别完成此操作，请添加 USE HINT [查询提示](../../t-sql/queries/hints-transact-sql-query.md)，而不是使用跟踪标志。 
  
PRIMARY  
  
此值仅对辅助数据库（该数据库位于主数据库上）有效，指定所有辅助数据库上的查询优化器基数估计模型设置都是为主数据库设置的值。 如果主数据库上查询优化器基数估计模型的配置发生更改，则辅助数据上的值也会相应地更改。 PRIMARY 是辅助数据库的默认设置。  
  
PARAMETER_SNIFFING = { ON | OFF | PRIMARY}  

启用或禁用[参数截取](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)。 默认值为 ON。 这与 [Trace Flag 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)是等效的。   

> [!TIP] 
> 要在查询级别完成此操作，请参阅 OPTIMIZE FOR UNKNOWN [查询提示](../../t-sql/queries/hints-transact-sql-query.md)。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 开始，要在查询级别完成此操作，也可使用 USE HINT [查询提示](../../t-sql/queries/hints-transact-sql-query.md)。 
  
PRIMARY  
  
此值仅对辅助数据库（该数据库位于主数据库上）有效，指定所有辅助数据库上此设置的值都是为主数据库设置的值。 如果主数据库上用于使用[参数截取](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)的配置更改，则辅助数据库上的值也会相应地更改，不需要再显式设置辅助数据库值。 这是辅助数据库的默认设置。  
  
QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY }  

启用或禁用查询优化修补程序，而无论数据库兼容性级别。 默认值为 OFF，可禁用在为特定版本 (post-RTM) 引入可用度最高的兼容性级别后发布的查询优化修补程序。 将此值设置为 ON 等效于启用[跟踪标志 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。   

> [!TIP] 
> 要在查询级别完成此操作，请添加 QUERYTRACEON [查询提示](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 开始，要在查询级别完成此操作，请添加 USE HINT [查询提示](../../t-sql/queries/hints-transact-sql-query.md)，而不是使用跟踪标志。  
  
PRIMARY  
  
此值仅对辅助数据库（该数据库位于主数据库上）有效，指定所有辅助数据库上此设置的值都是为主数据库设置的值。 如果主数据库的配置更改，辅助数据库上的值也会相应地更改，不需要再显式设置辅助数据库值。 这是辅助数据库的默认设置。  
  
CLEAR PROCEDURE_CACHE  

清除数据库的过程（计划）缓存。 可在主数据库和辅助数据库上执行此操作。  

IDENTITY_CACHE = { ON | OFF }  

**适用对象**：[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

在数据库级别启用或禁用标识缓存。 默认值为 ON。 标识缓存用于提高具有标识列的表的 INSERT 性能。 为了避免服务器意外重启或故障转移到辅助服务器时出现标识列值的差值，请禁用 IDENTITY_CACHE 选项。 该选项与现有[跟踪标志 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 类似，但前者可在数据库级别设置，而不只是可在服务器级别设置。   

> [!NOTE] 
> 仅可为 PRIMARY 设置此选项。 有关详细信息，请参阅[标识列](create-table-transact-sql-identity-property.md)。  

OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }  

适用于：[!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] 

第一次编译批处理时，启用或禁用要存储在缓存中的已编译计划存根。 默认为 OFF。 为数据库启用了数据库作用域内配置 OPTIMIZE_FOR_AD_HOC_WORKLOADS 后，已编译计划存根可在第一次编译批处理时存储在缓存中。 与完全编译的计划大小相比，计划存根的内存占用空间更小。  如果编译或再次执行批处理，则会删除已编译计划存根，并将其替换为完全编译的计划。

XTP_PROCEDURE_EXECUTION_STATISTICS  = { ON | OFF }  

适用于：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 

启用或禁用对当前数据库的本机编译的 T-SQL 模块在模块级别的执行统计信息收集。 默认为 OFF。 执行统计信息反映在 [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) 中。

如果该选项为“开”，或通过 [sp_xtp_control_proc_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) 启用了统计信息收集，则收集对本机编译的 T-SQL 模块的模块级别执行统计信息。

XTP_QUERY_EXECUTION_STATISTICS  = { ON | OFF }  

适用于：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

启用或禁用对当前数据库的本机编译的 T-SQL 模块语句级别的执行统计信息收集。 默认为 OFF。 执行统计信息反映在 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 和[查询存储](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)中。

如果该选项为“开”，或通过 [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) 启用了统计信息收集，则收集对本机编译的 T-SQL 模块的语句级别执行统计信息。

有关本机编译的 T-SQL 模块的性能监视的详细信息，请参阅[监视本机编译的存储过程的执行](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)。

ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**适用对象**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]（此功能为公共预览版）

允许你选择选项，使引擎自动将支持的操作提升为联机。 默认值为 OFF，表示除非在语句中指定，否则操作不会提升为联机。 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 反映 ELEVATE_ONLINE 的当前值。 这些选项只适用于通常支持联机的操作。  

FAIL_UNSUPPORTED

此值可将所有支持的 DDL 操作提升为 ONLINE。 不支持联机执行的操作会失败并引发警告。

WHEN_SUPPORTED  

此值可提升支持 ONLINE 的操作。 不支持联机的操作将脱机运行。

> [!NOTE]
> 通过提交指定了 ONLINE 选项的语句，可替代默认设置。 
 
ELEVATE_RESUMABLE= { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**适用对象**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]（此功能为公共预览版）

允许你选择选项，使引擎自动将支持的操作提升为可恢复。 默认值为 OFF，表示除非在语句中指定，否则操作不会提升为可恢复。 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 反映 ELEVATE_RESUMABLE 的当前值。 这些选项只适用于通常支持可恢复的操作。 

FAIL_UNSUPPORTED

此值可将所有支持的 DDL 操作提升为 RESUMABLE。 不支持可恢复执行的操作会失败并引发警告。

WHEN_SUPPORTED  

此值可提升支持 RESUMABLE 的操作。 不支持可恢复的操作以不可恢复的方式运行。  

> [!NOTE]
> 通过提交指定了 RESUMABLE 选项的语句，可替代默认设置。 

##  <a name="Permissions"></a> Permissions  
 需要针对数据库的   
ALTER ANY DATABASE SCOPE CONFIGURATION 权限。 用户若具有针对数据库的 CONTROL 权限，便可授予此权限。  
  
## <a name="general-remarks"></a>一般备注  
 虽然可以为辅助数据库配置不同于主数据库的作用域内配置设置，但所有辅助数据库都使用相同的配置。 无法为各辅助数据库配置不同的设置。  
  
 执行此语句会清除当前数据库中的过程缓存，这意味着需要重新编译所有查询。  
  
 对于 3 部分名称查询，采用查询的当前数据库连接设置，在当前数据库上下文中编译的 SQL 模块（例如过程、函数和触发器）除外，因此应使用其所在的数据库的选项。  
  
 ALTER_DATABASE_SCOPED_CONFIGURATION 事件添加为可用于触发 DDL 触发器的 DDL 事件。 这是 ALTER_DATABASE_EVENTS 触发器组的子级。  
 
 数据库作用域内配置设置随数据库一同转入。 这意味着还原或附加给定数据库时，会保留现有配置设置。
  
## <a name="limitations-and-restrictions"></a>限制和局限  
**MAXDOP**  
  
 精细设置可以替代全局设置，而资源调控器可以限制所有其他 MAXDOP 设置。  MAXDOP 设置的逻辑如下：  
  
-   查询提示可替代 sp_configure 和数据库作用域内设置。 如果为工作负荷组设置了资源组 MAXDOP：  
  
    -   如果查询提示设置为 0，则其会由资源调控器设置替代。  
  
    -   如果查询提示未设置为 0，则其会受资源调控器设置限制。  
  
-   如果不存在受资源调控器设置限制的查询提示，则 DB 作用域内设置（除非为 0）会替代 sp_configure 设置。  
  
-   sp_configure 设置由资源调控器设置替代。  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 QUERYTRACEON 提示用于启用旧版查询优化器或查询优化器修补程序时，会成为查询提示和数据库作用域内配置设置之间的 OR 条件，也就是说，如果启用了两者中任一一个，都会应用这些选项。  
  
**GeoDR**  
  
 可读辅助数据库（Always On 可用性组和 GeoReplication）通过检查数据库状态来使用辅助值。 尽管重新编译不会在故障转移时发生，且从技术上讲，新的主数据库具有使用辅助数据库设置的查询，但是，主数据库和辅助数据库的设置仅在工作负荷不同时才有所相同，因此已缓存查询使用的是最佳设置，而新查询选择适合它们的新设置。  
  
**DacFx**  
  
 由于 ALTER DATABASE SCOPED CONFIGURATION 是 Azure SQL 数据库和 SQL Server 2016 及更高版本的 SQL Server 中的一项新功能，并且会影响数据库架构，因此架构导出（有或没有数据）无法导入到较早版本的 SQL Server，如 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]。 例如，从使用新功能的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 或 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 数据库到 [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) 或 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 的导出无法导入到下级服务器。  

**ELEVATE_ONLINE** 

此选项仅适用于支持 WITH(ONLINE= 语法的 DDL 语句。 不影响 XML 索引 

**ELEVATE_RESUMABLE**

此选项仅适用于支持 WITH(ONLINE= 语法的 DDL 语句。 不影响 XML 索引 

  
## <a name="metadata"></a>元数据  

[sys.database_scoped_configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 系统视图提供有关数据库作用域内配置的信息。 数据库作用域内配置选项仅在 sys.database_scoped_configurations 中显示，因为它们是服务器范围内默认设置的替代项。 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 系统视图仅显示服务器范围内的设置。  
  
## <a name="examples"></a>示例  
以下示例演示 ALTER DATABASE SCOPED CONFIGURATION 的用法  
  
### <a name="a-grant-permission"></a>A. 授予权限  

本示例为用户 [Joe] 授予执行 ALTER DATABASE SCOPED CONFIGURATION 所需的     
权限。  
  
```sql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>B. 设置 MAXDOP  

本示例在异地复制方案中为主数据库设置 MAXDOP = 1，为辅助数据库设置 MAXDOP = 4。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
本示例在异地复制方案中为辅助数据库设置与其主数据库相同的 MAXDOP。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. 设置 LEGACY_CARDINALITY_ESTIMATION  

本示例在异地复制方案中为辅助数据库将 LEGACY_CARDINALITY_ESTIMATION 设置为 ON。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
本示例在异地复制方案中为辅助数据库设置与其主数据库相同的 LEGACY_CARDINALITY_ESTIMATION。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>D. 设置 PARAMETER_SNIFFING  

本示例在异地复制方案中为主数据库将 PARAMETER_SNIFFING 设置为 OFF。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
本示例在异地复制方案中为主数据库将 PARAMETER_SNIFFING 设置为 OFF。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
本示例在异地复制方案中为辅助数据库设置与其主数据库相同的 PARAMETER_SNIFFING。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. 设置 QUERY_OPTIMIZER_HOTFIXES  

在异地复制方案中为主数据库将 QUERY_OPTIMIZER_HOTFIXES 设置为 ON。  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. 清除过程缓存  

本示例清除了过程缓存（仅可用于主数据库）。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. 设置 IDENTITY_CACHE

**适用对象**：[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]（此功能为公共预览版） 

本示例禁用了标识缓存。

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. 设置 OPTIMIZE_FOR_AD_HOC_WORKLOADS

适用于：[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

本示例可在第一次编译批处理时启用要存储在缓存中的已编译计划存根。

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

### <a name="i--set-elevateonline"></a>I.  设置 ELEVATE_ONLINE 

**适用对象**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]（此功能为公共预览版）
 
此示例将 ELEVATE_ONLINE 设置为 FAIL_UNSUPPORTED。  tsqlCopy 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_ONLINE=FAIL_UNSUPPORTED ;
```  

### <a name="j-set-elevateresumable"></a>J. 设置 ELEVATE_RESUMABLE 

**适用对象**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]（此功能为公共预览版）

此示例将 ELEVEATE_RESUMABLE 设置为 WHEN_SUPPORTED。  tsqlCopy 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_RESUMABLE=WHEN_SUPPORTED ;  
``` 

## <a name="additional-resources"></a>其他资源

### <a name="maxdop-resources"></a>MAXDOP 资源 
* [并行度](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [适用于 SQL Server 中的“max degree of parallelism”配置选项的建议和指南](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>LEGACY_CARDINALITY_ESTIMATION 资源    
* [基数估计 (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [使用 SQL Server 2014 基数估算器优化查询计划](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>PARAMETER_SNIFFING 资源    
* [参数截取](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* ["I smell a parameter!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/)（“我发现一个参数！”）

### <a name="queryoptimizerhotfixes-resources"></a>QUERY_OPTIMIZER_HOTFIXES 资源    
* [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server 查询优化器修补程序跟踪标志 4199 服务模型](https://support.microsoft.com/en-us/kb/974006)

### <a name="elevateonline-resources"></a>ELEVATE_ONLINE 资源 

- [联机索引操作准则](../../relational-databases/indexes/guidelines-for-online-index-operations.md) 

### <a name="elevateresumable-resources"></a>ELEVATE_RESUMABLE 资源 

- [联机索引操作准则](../../relational-databases/indexes/guidelines-for-online-index-operations.md) 
 
## <a name="more-information"></a>详细信息  
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [数据库和文件目录视图](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [服务器配置选项](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
 
