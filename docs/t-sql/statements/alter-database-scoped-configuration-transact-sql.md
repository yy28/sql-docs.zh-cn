---
title: "ALTER DATABASE SCOPED CONFIGURATION (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "32"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: cc17063b8f74e296562a460677121c5ef1c85016
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  This 语句使多个数据库配置设置在**单个数据库**级别。 此语句可用于[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]和 SQL Server 从开始按[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 这些设置是：  
  
- 清除过程缓存。  
  
- 将 MAXDOP 参数设置为任意值 (1，2，...)，主数据库是基于什么最适合于该特定数据库的设置不同的值 (例如 0) 的所有辅助数据库使用 （例如，用于报表查询）。  
  
- 设置独立于数据库兼容级别的查询优化器基数估计模型。  
  
- 在数据库级别启用或禁用参数探查。
  
- 在数据库级别启用或禁用查询优化修补程序。

- 启用或禁用在数据库级别标识缓存。

- 启用或禁用了编译的计划存根，在首次编译批处理时要存储在缓存中。 
  
 ![链接图标](../../database-engine/configure-windows/media/topic-link.gif "链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
}  
```  
  
## <a name="arguments"></a>参数  
 
辅助数据库  
 
指定 （所有辅助数据库必须具有相同的值） 的辅助数据库的设置。  
  
MAXDOP  **=**  {\<值 > |主}  
**\<值 >**  
  
指定 MAXDOP 设置应用于语句的默认。 0 是默认值，该值指示在将改为使用服务器配置。 （除非它已设置为 0），将重写在数据库范围内 MAXDOP**最大并行度**由 sp_configure 设置在服务器级别。 查询提示仍可以重写数据库范围 MAXDOP，以便优化需要不同的设置的特定查询。 所有这些设置的工作负荷组设置 MAXDOP 受限制。   

您可以使用 max degree of parallelism 选项来限制并行计划执行时所用的处理器数。 SQL Server 将并行执行计划的查询、 索引数据定义语言 (DDL) 操作、 并行插入、 联机更改列、 并行统计信息集合和静态和键集驱动游标填充。
 
若要在实例级别设置此选项，请参阅[配置 max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 

> [!TIP] 
> 若要实现此目的在查询级别，将添加**MAXDOP** [查询提示](../../t-sql/queries/hints-transact-sql-query.md)。  
  
PRIMARY  
  
只能设置为辅助数据库，对主要主机和中的数据库时，表示配置将一组的主站点。 如果主更改，辅助数据库上的值的配置将更改相应地而无需设置辅助副本值显式。 **主**是辅助数据库的默认设置。  
  
LEGACY_CARDINALITY_ESTIMATION  **=**  {ON |**OFF** |主}  

使用此选项可设置为的 SQL Server 2012 和早期版本的查询优化器基数估计模型独立于数据库的兼容性级别。 默认值是**OFF**，查询优化器基数估计模型基于数据库的兼容性级别的设置。 此选项设置为**ON**相当于启用[跟踪标志 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 

> [!TIP] 
> 若要实现此目的在查询级别，将添加**QUERYTRACEON** [查询提示](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加**使用提示**[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用跟踪标志。 
  
PRIMARY  
  
此值才有效时，在主计算机上的数据库中的辅助副本上，指定在所有辅助副本上的查询优化器基数估算模型设置将为主设置的值。 如果主服务器的查询优化器基数估计模型上的配置发生更改，将相应地更改辅助数据库上的值。 **主**是辅助数据库的默认设置。  
  
PARAMETER_SNIFFING  **=**  { **ON** |关闭 |主}  

启用或禁用[参数探查](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)。 默认值为 ON。 这与 [Trace Flag 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)是等效的。   

> [!TIP] 
> 若要实现此目的在查询级别，请参阅**OPTIMIZE FOR UNKNOWN** [查询提示](../../t-sql/queries/hints-transact-sql-query.md)。 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别**使用提示**[查询提示](../../t-sql/queries/hints-transact-sql-query.md)也是可用。 
  
PRIMARY  
  
此值才有效时，在主计算机上的数据库中的辅助副本上，指定在所有辅助副本上的此设置的值将为主设置的值。 如果使用主计算机上的配置[参数探查](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)更改，在辅助副本上的值将更改相应地而无需设置辅助副本值显式。 这是辅助数据库的默认设置。  
  
QUERY_OPTIMIZER_HOTFIXES  **=**  {ON |**OFF** |主}  

启用或禁用查询优化修补程序，而不考虑数据库的兼容性级别。 默认值是**OFF**，它禁用查询优化修补程序已发行后的特定版本引入了最高的可用兼容性级别 (post RTM)。 此选项设置为**ON**相当于启用[Trace Flag 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。   

> [!TIP] 
> 若要实现此目的在查询级别，将添加**QUERYTRACEON** [查询提示](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用跟踪标志。  
  
PRIMARY  
  
此值才有效时，在主计算机上的数据库中的辅助副本上，指定在所有辅助副本上的此设置的值是用于主设置的值。 如果在配置为使主更改，辅助数据库上的值发生更改相应地而无需设置辅助副本值显式。 这是辅助数据库的默认设置。  
  
清除 PROCEDURE_CACHE  

清除该数据库的过程 （计划） 缓存。 这可以同时在主和辅助数据库上执行。  

IDENTITY_CACHE  **=**  { **ON** |关闭}  

**适用于**:[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

启用或禁用在数据库级别的标识缓存。 默认值是**ON**。 标识缓存用于改进对具有标识列的表的插入性能。 若要避免的情况下服务器意外重新启动或故障转移到辅助服务器的位置中的标识列的值方面的差距，禁用 IDENTITY_CACHE 选项。 此选项是类似于现有[跟踪标志 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)，只不过它可以在数据库级别而不是仅在服务器级别设置。   

> [!NOTE] 
> 仅可以为主设置此选项。 有关详细信息，请参阅[标识列](create-table-transact-sql-identity-property.md)。  

OPTIMIZE_FOR_AD_HOC_WORKLOADS  **=**  {ON |**OFF** }  

适用于：[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

启用或禁用了编译的计划存根，在首次编译批处理时要存储在缓存中。 默认为 OFF。 第一次编译后的数据库范围的配置为数据库，编译的计划存根启用 OPTIMIZE_FOR_AD_HOC_WORKLOADS 将存储在缓存时一批。 计划存根 （stub） 具有相比完全编译的计划的大小较小的内存需求量。  如果批处理被编译，或再次执行，则将删除编译的计划存根，并将其替换为完全编译的计划。

##  <a name="Permissions"></a> Permissions  
 需要更改任何数据库作用域配置   
对数据库中。 可以通过具有数据库拥有 CONTROL 权限的用户授予此权限。  
  
## <a name="general-remarks"></a>一般备注  
 虽然您可以配置辅助数据库能够从其主不同的作用域的配置设置，所有辅助数据库将使用相同的配置。 无法为单个辅助数据库配置不同的设置。  
  
 执行此语句清除在当前数据库中，这意味着所有查询都需要重新编译过程缓存。  
  
 对于 3 部分组成的名称查询，查询当前的数据库连接的设置会认可，以外的其他有关当前数据库上下文中进行编译的 SQL 模块 （如过程、 函数和触发器），并因此而使用的选项它们驻留在其中的数据库。  
  
 ALTER_DATABASE_SCOPED_CONFIGURATION 事件被添加为一个可用于激发 DDL 触发器的 DDL 事件。 这是 ALTER_DATABASE_EVENTS 触发器组的子级。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
**MAXDOP**  
  
 精细设置可以重写全局的并且该资源调控器可以制定一个上限的所有其他 MAXDOP 设置。  MAXDOP 设置的逻辑如下所示：  
  
-   查询提示重写 sp_configure 和数据库作用域设置。 如果在资源组的工作负荷组设置 MAXDOP:  
  
    -   如果查询提示设置为 0，它被覆盖的设置的资源调控器。  
  
    -   如果查询提示都是不为 0，它会受设置的资源调控器。  
  
-   数据库作用域设置 （除非它是 0） 将替代 sp_configure 设置，除非查询提示和受设置的资源调控器。  
  
-   Sp_configure 设置被替代设置的资源调控器。  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 当 QUERYTRACEON 提示用于启用旧的查询优化器或查询优化器修补程序时，它将查询提示和数据库范围的配置设置，这意味着如果启用了其中一个应用的选项之间 OR 条件。  
  
**GeoDR**  
  
 可读辅助数据库，例如 Alwayson 可用性组和 GeoReplication，使用通过检查数据库的状态的次数的值。 即使在故障转移时，重新编译不会发生，并且从技术上讲新的主已使用的辅助设置的查询，其理念是，仅当工作负荷是不同，并且因此缓存的查询时，主服务器和辅助数据库之间的设置仅会有所不同使用最佳的设置，而新查询选取新的设置适用于它们。  
  
**DacFx**  
  
 由于 ALTER 数据库范围的配置是架构的 Azure SQL 数据库和 SQL Server 开头，影响数据库架构，导出 （带有或不包含数据） 是架构的不能将其导入 SQL Server 的较旧版本的 SQL Server 2016 中的新增功能例如[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或[!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]。 例如，导出到[DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3)或[BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4)从[!INCLUDE[ssSDS](../../includes/sssds-md.md)]或[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]使用此新功能的数据库将不能导入到的下级服务器。  
  
## <a name="metadata"></a>元数据  

[Sys.database_scoped_configurations &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)系统视图提供有关在数据库中指定了作用域配置的信息。 数据库范围配置选项仅显示在 sys.database_scoped_configurations 因为它们是为服务器级默认设置的替代。 [Sys.configurations &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)系统视图只显示服务器范围的设置。  
  
## <a name="examples"></a>示例  
这些示例演示使用 ALTER DATABASE SCOPED CONFIGURATION  
  
### <a name="a-grant-permission"></a>A. 授予权限  

此示例将执行 ALTER DATABASE SCOPED CONFIGURATION 所需的权限授予     
为用户 [Joe]。  
  
```sql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>B. 设置 MAXDOP  

此示例将 MAXDOP 设置 = 主数据库和 MAXDOP 1 = 4 异地复制方案中的辅助数据库。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
此示例将辅助数据库的 MAXDOP 会相同，因为它已设置为与其在异地复制方案中的主数据库设置。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. 设置 LEGACY_CARDINALITY_ESTIMATION  

此示例会将 LEGACY_CARDINALITY_ESTIMATION 的异地复制方案中的辅助数据库设置为开中。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
此示例将 LEGACY_CARDINALITY_ESTIMATION 设置辅助数据库，因为它是用于在异地复制方案中其主数据库。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>D. 设置 PARAMETER_SNIFFING  

此示例会将 PARAMETER_SNIFFING 的异地复制方案中的主数据库设置为 OFF 中。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
此示例会将 PARAMETER_SNIFFING 的异地复制方案中的主数据库设置为 OFF 中。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
此示例将 PARAMETER_SNIFFING 设置为辅助数据库，因为它是在异地复制方案中的主数据库上。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. 设置 QUERY_OPTIMIZER_HOTFIXES  

异地复制方案中的主数据库上 QUERY_OPTIMIZER_HOTFIXES 设为 ON。  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. 清除过程缓存  

此示例中清除过程缓存 （可能仅对主数据库）。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. 设置 IDENTITY_CACHE

**适用于**:[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]（功能处于公共预览版中） 

此示例将禁用标识缓存。

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. 设置 OPTIMIZE_FOR_AD_HOC_WORKLOADS

适用于：[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

此示例将启用了编译的计划存根，在首次编译批处理时要存储在缓存中。

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

## <a name="additional-resources"></a>其他资源

### <a name="maxdop-resources"></a>MAXDOP 资源 
* [并行度](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [建议和 SQL Server 中的"max degree of parallelism"配置选项的指导原则](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>LEGACY_CARDINALITY_ESTIMATION 资源    
* [基数估计 (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [使用 SQL Server 2014 基数估算器优化查询计划](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>PARAMETER_SNIFFING 资源    
* [参数截取](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* ["我闻参数"！](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/)

### <a name="queryoptimizerhotfixes-resources"></a>QUERY_OPTIMIZER_HOTFIXES 资源    
* [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server 查询优化器修补程序跟踪标志 4199 维护服务模型](https://support.microsoft.com/en-us/kb/974006)

## <a name="more-information"></a>详细信息  
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [数据库和文件目录视图](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [服务器配置选项](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
 
