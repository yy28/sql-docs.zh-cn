---
title: "创建列存储索引 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE INDEX
- COLUMNSTORE_INDEX_TSQL
- CREATE CLUSTERED COLUMNSTORE INDEX
- COLUMNSTORE_TSQL
- CREATE NONCLUSTERED COLUMNSTORE INDEX
- CREATE_NONCLUSTERED_COLUMNSTORE_INDEX_TSQL
- CREATE COLUMNSTORE INDEX
- CREATE_CLUSTERED_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE
dev_langs: TSQL
helpviewer_keywords:
- index creation [SQL Server], columnstore indexes
- columnstore index, creating
- CREATE COLUMNSTORE INDEX statement
- CREATE INDEX statement
ms.assetid: 7e1793b3-5383-4e3d-8cef-027c0c8cb5b1
caps.latest.revision: "76"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: fd51d2a902337b232f5bf9497f5ebd0bbcac9199
ms.sourcegitcommit: 0e305dce04dcd1aa83c39328397524b352c96386
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="create-columnstore-index-transact-sql"></a>CREATE COLUMNSTORE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

将一个行存储表转换为聚集列存储索引，或创建一个非聚集列存储索引。 使用列存储索引，以便高效运行对 OLTP 工作负载的实时运行分析，或以提高数据仓库工作负荷的数据压缩和查询性能。  
  
> [!NOTE]  
> 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，你可以将表创建为聚集列存储索引。   不再需要先创建行存储表，然后将其转换为聚集列存储索引。  

> [!TIP]
> 有关索引设计指南的信息，请参阅[SQL Server 索引设计指南](../../relational-databases/sql-server-index-design-guide.md)。

跳过对示例：  
-   [用于将行存储表转换为列存储的示例](../../t-sql/statements/create-columnstore-index-transact-sql.md#convert)  
-   [对于非聚集列存储索引的示例](../../t-sql/statements/create-columnstore-index-transact-sql.md#nonclustered)  
  
请转到方案：  
-   [列存储索引进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
-   [针对数据仓库的列存储索引](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
了解更多信息：  
-   [列存储索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)  
-   [列存储索引功能摘要](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create a clustered columnstore index on disk-based table.  
CREATE CLUSTERED COLUMNSTORE INDEX index_name  
    ON [database_name. [schema_name ] . | schema_name . ] table_name  
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]  
[ ; ]  
  
--Create a non-clustered columnstore index on a disk-based table.  
CREATE [NONCLUSTERED]  COLUMNSTORE INDEX index_name   
    ON [database_name. [schema_name ] . | schema_name . ] table_name   
        ( column  [ ,...n ] )  
    [ WHERE <filter_expression> [ AND <filter_expression> ] ]
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]   
[ ; ]  
  
<with_option> ::=  
      DROP_EXISTING = { ON | OFF } -- default is OFF  
    | MAXDOP = max_degree_of_parallelism 
    | ONLINE = { ON | OFF } 
    | COMPRESSION_DELAY  = { 0 | delay [ Minutes ] }  
    | DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { partition_number_expression | range } [ ,...n ] ) ]  
  
<on_option>::=  
      partition_scheme_name ( column_name )   
    | filegroup_name   
    | "default"   
  
<filter_expression> ::=  
      column_name IN ( constant [ ,...n ]  
    | column_name { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< } constant  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CLUSTERED COLUMNSTORE INDEX index_name   
    ON [ database_name . [ schema_name ] . | schema_name . ] table_name  
    [ WITH ( DROP_EXISTING = { ON | OFF } ) ] --default is OFF  
[;]  
```  
  
## <a name="arguments"></a>参数  
CREATE CLUSTERED COLUMNSTORE INDEX  
创建聚集列存储索引在其中的所有数据是压缩并存储列。 该索引包含表中的所有列，并且存储整个表。 如果现有表是堆或聚集的索引，则会将表转换为聚集列存储索引。 如果表已存储为聚集列存储索引，删除和重新生成现有的索引。  
  
*index_name*  
指定用于新索引的名称。  
  
如果表已具有聚集列存储索引，可以将现有索引，指定相同的名称，或可以使用 DROP EXISTING 选项以指定新名称。  
  
ON [*database_name*。 [*schema_name* ]。 | *schema_name* 。 ] *table_name*  
   指定要作为聚集列存储索引存储的由一部分、两部分或三部分构成的名称。 如果表是堆或聚集的索引表从行存储转换为列存储。 如果该表已为列存储，此语句将重新生成聚集列存储索引。  
  
替换为  
DROP_EXISTING = [关闭] |ON  
   DROP_EXISTING = ON 指定要删除现有的聚集列存储索引，并创建新的列存储索引。  

   默认情况下，DROP_EXISTING = OFF 需要索引名称是与现有名称相同。 出错时指定的索引名称已存在。  
  
MAXDOP = *max_degree_of_parallelism*  
   在索引操作期间覆盖现有的最大并行度服务器配置。 使用 MAXDOP 可以限制在执行并行计划的过程中使用的处理器数量。 最大数量为 64 个处理器。  
  
   *max_degree_of_parallelism*值可以是：  
   - 1 - 取消生成并行计划。  
   - \>1-限制最大指定数目的并行索引操作中使用的处理器数或更少基于当前的系统工作负荷。 例如，当 MAXDOP = 4，使用的处理器数量为 4 或更小。  
   - 0（默认值） - 根据当前系统工作负荷使用实际的处理器数量或更少数量的处理器。  
  
   有关详细信息，请参阅[配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)，和[配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
 
COMPRESSION_DELAY = **0** | *延迟*[分钟]  
   适用于：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。

   对于基于磁盘的表，*延迟*SQL Server 可以将其压缩到压缩行组之前，增量行组中指定的最小必须保持为增量行组处于关闭状态的分钟数。 由于基于磁盘的表不跟踪插入和更新时间在上单个行，SQL Server 应用延迟到处于关闭状态的增量行组。  
   默认值为 0 分钟。  
   有关何时使用 COMPRESSION_DELAY，建议，请参阅[开始使用列存储适进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)。  
  
DATA_COMPRESSION = COLUMNSTORE |COLUMNSTORE_ARCHIVE  
   适用于：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
为指定的表、分区号或分区范围指定数据压缩选项。 选项如下所示：   
COLUMNSTORE  
   列存储是默认设置，并指定使用大多数的高性能列存储压缩进行压缩。 这是典型的选择。  
  
COLUMNSTORE_ARCHIVE  
   进一步 COLUMNSTORE_ARCHIVE 压缩的表或分区到较小的大小。 使用此选项的情况下如存档需要较小的存储大小，可以提供存储和检索有关的更多时间。  
  
   有关压缩的详细信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  

ON  
   使用 ON 选项，您可为数据存储指定选项，例如分区架构、特定的文件组或默认文件组。 如果未指定 ON 选项，则索引使用现有的表设置分区或文件组设置。  
  
   *partition_scheme_name* **(** *column_name* **)**  
   指定表的分区方案。 分区方案必须已在数据库中存在。 若要创建分区方案，请参阅[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)。  
 
   *column_name*指定对其分区已分区的索引的列。 此列必须与匹配的数据类型，长度，并且分区的自变量的精度函数*partition_scheme_name*正在使用。  

   *filegroup_name*  
   指定用于存储聚集列存储索引的文件组。 如果未指定位置并且表未分区，则索引将与基础表或视图使用相同的文件组。 该文件组必须已存在。  

   **"**默认**"**  
   若要在默认文件组上创建索引，请使用"默认值"或 [默认]。  
  
   如果指定了 "default"，则当前会话的 QUOTED_IDENTIFIER 选项必须为 ON。 QUOTED_IDENTIFIER 默认为 ON。 有关详细信息，请参阅 [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
创建 [聚集] 列存储索引  
在行存储表上创建内存中的非聚集列存储索引存储为堆或聚集的索引。 索引可以包含筛选的条件，并不需要包括所有的基础表的列。 列存储索引需要足够的空间来存储数据的副本。 它是可更新，并更改基础表时将更新。 聚集索引的非聚集列存储索引使实时分析。  
  
*index_name*  
   指定索引的名称。 *index_name*必须是唯一在该表中，但不需要在数据库中是唯一。 索引名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 **(** *列*[ **，**...*n* ] **)**  
    指定要存储的列。 非聚集列存储索引被限制为 1024年列。  
   每个列都必须采用列存储索引支持的数据类型。 请参阅[限制和局限](../../t-sql/statements/create-columnstore-index-transact-sql.md#LimitRest)有关支持的数据类型的列表。  

ON [*database_name*。 [*schema_name* ]。 | *schema_name* 。 ] *table_name*  
   指定一个、 两个或三部分包含的索引的表名称。  

使用 DROP_EXISTING = [关闭] |ON  
   DROP_EXISTING = 的 ON 删除和重新生成现有的索引。 指定的索引名称必须与当前的现有索引相同；但可以修改索引定义。 例如，可以指定不同的列或索引选项。
  
   DROP_EXISTING = 的 OFF 的指定的索引名称已存在，则会显示错误。 使用 DROP_EXISTING 不能更改索引类型。 在向后兼容的语法中，WITH DROP_EXISTING 等效于 WITH DROP_EXISTING = ON。  

MAXDOP = *max_degree_of_parallelism*  
   重写[配置 max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)索引操作的持续时间的配置选项。 使用 MAXDOP 可以限制在执行并行计划的过程中使用的处理器数量。 最大数量为 64 个处理器。  
  
   *max_degree_of_parallelism*值可以是：  
   - 1 - 取消生成并行计划。  
   - \>1-限制最大指定数目的并行索引操作中使用的处理器数或更少基于当前的系统工作负荷。 例如，当 MAXDOP = 4，使用的处理器数量为 4 或更小。  
   - 0（默认值） - 根据当前系统工作负荷使用实际的处理器数量或更少数量的处理器。  
  
   有关详细信息，请参阅 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
>  并行索引操作不可用的每个版本[!INCLUDE[msC](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
ONLINE = [ON |关闭]   
   适用于： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]，仅限非聚集列存储索引中。
在指定的非聚集列存储索引保持联机和可用的新副本的索引时正在生成。

   关闭指定的索引不可供使用时正在生成新的副本。 因为这是仅，非聚集索引的基表保持可用性，只有非聚集列存储索引不用于满足查询的新索引直到完成。 

COMPRESSION_DELAY = **0** | \<延迟 > [分钟]  
   适用于：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
   在多长时间行应保留在增量行组之前文件迁移到压缩行组上指定下限。 例如，客户可以说，是否某行是不变时间为 120 分钟，使其适合压缩到列存储格式。 对于基于磁盘的表的列存储索引，我们不能跟踪插入或更新，行的时间时，我们使用增量行组关闭作为代理的行改为。 默认持续时间为 0 分钟。 行迁移到列存储后进行增量行组中累积 100 万行，并它已标记为已关闭。  
  
DATA_COMPRESSION  
   为指定的表、分区号或分区范围指定数据压缩选项。 选项如下所示：  
COLUMNSTORE  
   适用于：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 仅适用于列存储索引，包括非聚集列存储索引和聚集列存储索引。 列存储是默认设置，并指定使用大多数的高性能列存储压缩进行压缩。 这是典型的选择。  
  
COLUMNSTORE_ARCHIVE  
   适用于：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
仅适用于列存储索引，包括非聚集列存储索引和聚集列存储索引。 进一步 COLUMNSTORE_ARCHIVE 压缩的表或分区到较小的大小。 这可用于存档，或者用于要求更小存储大小并且可以付出更多时间来进行存储和检索的其他情形。  
  
 有关压缩的详细信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
其中\<filter_expression > [AND \<filter_expression >] 适用于：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
   这将调用筛选器谓词，指定要包含在索引将哪些行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]筛选索引中的数据行创建筛选的统计信息。  
  
   筛选器谓词使用简单比较逻辑。 比较运算符不允许使用 NULL 文本的比较。 请改用 IS NULL 和 IS NOT NULL 运算符。  
  
   下面是一些 `Production.BillOfMaterials` 表筛选谓词示例：  
   `WHERE StartDate > '20000101' AND EndDate <= '20000630'`    
   `WHERE ComponentID IN (533, 324, 753)`  
   `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
   
   对筛选的索引的指南，请参阅[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。  
  
ON  
   这些选项指定在其创建索引的文件组。  
  
*partition_scheme_name* **(** *column_name* **)**  
   指定定义已分区索引的分区映射到其上的文件组的分区方案。 分区方案必须通过执行数据库中不存在[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)。 
   *column_name*指定对其分区已分区的索引的列。 此列必须与匹配的数据类型，长度，并且分区的自变量的精度函数*partition_scheme_name*正在使用。 *column_name*不限于索引定义中的列。 在对列存储索引进行分区时，如果尚未指定分区依据列，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]会添加分区依据列作为索引列。  
   如果*partition_scheme_name*或*文件组*未指定和表分区、 检索均被放置在相同的分区方案中，使用相同的分区依据列，与基础表。  
   分区表的列存储索引必须实现分区对齐。  
   有关分区索引的详细信息，请参阅[Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  

*filegroup_name*  
   指定要对其创建索引的文件组名称。 如果*filegroup_name*未指定和未分区表、 索引与基础表使用同一文件组。 该文件组必须已存在。  
 
**"**默认**"**  
为默认文件组创建指定索引。  
  
在此上下文中，“default”一词不是关键字。 它是默认文件组的标识符和必须分隔，如下所示 ON **"**默认**"**或亮**[**默认**]**。 如果指定了 "default"，则当前会话的 QUOTED_IDENTIFIER 选项必须为 ON。 这是默认设置。 有关详细信息，请参阅 [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
##  <a name="Permissions"></a> Permissions  
 需要对表的 ALTER 权限。  
  
##  <a name="GenRemarks"></a>一般备注  
 可以在临时表创建列存储索引。 在删除表或结束会话时，也将删除索引。  
 
## <a name="filtered-indexes"></a>筛选索引  
筛选索引是一种经过优化的非聚集索引，适用于从表中选择少数行的查询。 筛选索引使用筛选谓词对表中的部分数据进行索引。 设计良好的筛选索引可以提高查询性能，降低存储成本和维护成本。  
  
### <a name="required-set-options-for-filtered-indexes"></a>筛选索引所需的 SET 选项  
如果下列任何条件成立，则需要“必需的值”列中的 SET 选项：  
- 创建筛选索引。  
- INSERT、UPDATE、DELETE 或 MERGE 操作修改筛选索引中的数据。  
- 查询优化器使用筛选的索引来生成查询计划。  
  
    |SET 选项|必需的值|默认服务器值|，则“默认”<br /><br /> OLE DB 和 ODBC 值|，则“默认”<br /><br /> DB-Library 值|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|   
  
     *当数据库兼容性级别设置为 90 或更高时，如果将 ANSI_WARNINGS 设置为 ON，则将使 ARITHABORT 隐式设置为 ON。 如果数据库兼容性级别设置为 80 或更低，则必须将 ARITHABORT 选项显式设置为 ON。  
  
 如果 SET 选项不正确，则可能会出现以下情况：  
  
-   不会创建筛选索引。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]生成错误并回滚对索引中的数据进行更改的 INSERT、UPDATE、DELETE 或 MERGE 语句。  
  
-   查询优化器不考虑任何 Transact-SQL 语句的执行计划中的索引。  
  
 有关筛选索引的详细信息，请参阅[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。 
  
##  <a name="LimitRest"></a> 限制和局限  

**列存储索引中的每个列必须是以下常见业务数据类型之一：** 
-   datetimeoffset [(  *n*  )]  
-   datetime2 [(  *n*  )]  
-   DATETIME  
-   smalldatetime  
-   日期  
-   时间 [(  *n*  )]  
-   float [(  *n*  )]  
-   实际 [(  *n*  )]  
-   十进制 [(*精度*[ *，缩放*] **)** ]
-   数字 [(*精度*[ *，缩放*] **)** ]    
-   money  
-   SMALLMONEY  
-   BIGINT  
-   ssNoversion  
-   smallint  
-   TINYINT  
-   bit  
-   nvarchar [(  *n*  )] 
-   nvarchar (max) (适用于[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和高级层的 Azure SQL 数据库定价层，仅限聚集列存储索引中)   
-   nchar [(  *n*  )]  
-   varchar [(  *n*  )]  
-   varchar （max) (适用于[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和高级层的 Azure SQL 数据库定价层，仅限聚集列存储索引中)
-   char [(  *n*  )]  
-   varbinary [(  *n*  )] 
-   varbinary (max) (适用于[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和高级层的 Azure SQL 数据库定价层，仅限聚集列存储索引中)
-   二进制 [(  *n*  )]  
-   uniqueidentifier (适用于[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]及更高版本)
  
如果基础表具有列存储索引不支持数据类型的列，则必须省略该列从非聚集列存储索引。  
  
**使用任何以下数据类型的列不能包含列存储索引中：**
-   ntext、text 和 image  
-   nvarchar (max)、 varchar （max） 和 varbinary （max） (适用于[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]和早期版本中，和非聚集列存储索引) 
-   rowversion（和 timestamp）  
-   sql_variant  
-   CLR 类型（hierarchyid 和空间类型）  
-   xml  
-   uniqueidentifier (适用于[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  

**非聚集列存储索引：**
-   包含的列数不能超过 1024。  
-   具有非聚集列存储索引的表可以具有唯一约束、主键约束或外键约束，但这些约束不能包括在非聚集列存储索引中。  
-   不能基于视图或索引视图创建。  
-   不能包含稀疏列。  
-   无法使用更改**ALTER INDEX**语句。 若要更改非聚集索引，必须先删除该列存储索引，然后重新创建它。 你可以使用**ALTER INDEX**禁用和重新生成列存储索引。  
-   不能通过创建**包括**关键字。  
-   不能包括**ASC**或**DESC**排序索引的关键字。 根据压缩算法对列存储索引排序。 排序将抵销许多性能优势。  
-   无法在非聚集列存储索引中包括类型 nvarchar (max)、 varchar （max），和 varbinary （max） 的大型对象 (LOB) 列。 只有聚集列存储索引支持 LOB 类型，从[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]版本和配置在高级定价层的 Azure SQL 数据库。 请注意，之前的版本聚集和非聚集列存储索引中不支持 LOB 类型。


 **列存储索引不能组合具有以下特点：**  
-   计算列。 从 SQL Server 自 2017 年开始，聚集列存储索引可以包含非持久化计算的列。 但是，在 SQL Server 自 2017 年，聚集列存储索引不能包含持久化计算的列，并且你不能对计算列创建非聚集的索引。 
-   页和行压缩和**vardecimal**存储格式 （列存储索引已压缩以不同的格式。）  
-   复制  
-   Filestream

不能在具有聚集列存储索引的表上使用游标或触发器。 此限制不适用于非聚集列存储索引。你可以在具有非聚集列存储索引的表上使用游标和触发器。

**SQL Server 2014 特定限制**  
这些限制仅适用于 SQL Server 2014。 在此版本中，我们引入了可更新聚集列存储索引。 非聚集列存储索引已仍是只读的。  

-   更改跟踪。 不能使用更改跟踪与非聚集列存储索引 (NCCI)，因为它们是只读的。 因此对于聚集列存储索引 (CCI) 工作。  
-   变更数据捕获。 不能使用的更改数据捕获的非聚集列存储索引 (NCCI)，因为它们是只读的。 因此对于聚集列存储索引 (CCI) 工作。  
-   可读辅助副本。 在可读辅助数据库始终 OnReadable 可用性组，无法访问群集的聚集列存储索引 (CCI)。  你可以从可读辅助数据库访问非聚集列存储索引 (NCCI)。  
-   多个活动结果集 (MARS)。 SQL Server 2014 只读连接到具有列存储索引的表使用 MARS。    但是，SQL Server 2014 不支持具有列存储索引的表上的并发数据操作语言 (DML) 操作 MARS。 当发生这种情况时，SQL Server 会终止连接，并中止事务。  
  
 有关的性能优势和限制的列存储索引的信息，请参阅[列存储索引概述](../../relational-databases/indexes/columnstore-indexes-overview.md)。
  
##  <a name="Metadata"></a> 元数据  
 列存储索引中的所有列在元数据中作为包含性列存储。 列存储索引中没有任何键列。 这些系统视图提供有关列存储索引的信息。  
  
-   [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
-   [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
-   [sys.partitions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
-   [sys.column_store_segments (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
-   [sys.column_store_dictionaries (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
-   [sys.column_store_row_groups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  

##  <a name="convert"></a>用于将行存储表转换为列存储的示例  
  
### <a name="a-convert-a-heap-to-a-clustered-columnstore-index"></a>A. 将堆转换为聚集列存储索引  
 此示例将一个表作为堆创建，然后将其转换为名为 cci_Simple 的聚集列存储索引。 这会将整个表的存储从行存储转换为列存储。  
  
```  
CREATE TABLE SimpleTable(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_Simple ON SimpleTable;  
GO  
```  
  
### <a name="b-convert-a-clustered-index-to-a-clustered-columnstore-index-with-the-same-name"></a>B. 将聚集索引转换为具有相同名称的聚集列存储索引。  
 此示例创建一个具有聚集索引的表，然后演示将该聚集索引转换为聚集列存储索引的语法。 这会将整个表的存储从行存储转换为列存储。  
  
```  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cl_simple ON SimpleTable  
WITH (DROP_EXISTING = ON);  
GO  
```  
  
### <a name="c-handle-nonclustered-indexes-when-converting-a-rowstore-table-to-a-columnstore-index"></a>C. 将一个行存储表转换为列存储索引时，请处理非聚集索引。  
 此示例演示如何处理非聚集索引，将一个行存储表转换为列存储索引时。 实际上，开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]采取任何特殊操作是必需的;[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自动定义和重新生成新的聚集列存储索引的非聚集索引。  
  
 如果你想要删除的非聚集索引，使用 DROP INDEX 语句之前创建列存储索引。 DROP EXISTING 选项仅可删除要转换的聚集的索引。 它不删除非聚集索引。  
  
 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，无法在列存储索引上创建非聚集索引。 此示例演示如何在早期版本中你需要在创建列存储索引之前删除的非聚集索引。  
  
```  
  
--Create the table for use with this example.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
  
--Create two nonclustered indexes for use with this example  
CREATE INDEX nc1_simple ON SimpleTable (OrderDateKey);  
CREATE INDEX nc2_simple ON SimpleTable (DueDateKey);   
GO  
  
--SQL Server 2012 and SQL Server 2014: you need to drop the nonclustered indexes  
--in order to create the columnstore index.   
  
DROP INDEX SimpleTable.nc1_simple;  
DROP INDEX SimpleTable.nc2_simple;  
  
--Convert the rowstore table to a columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_simple ON SimpleTable;   
GO  
  
```  
  
### <a name="d-convert-a-large-fact-table-from-rowstore-to-columnstore"></a>D. 将大型事实表从行存储转换为列存储方式  
 此示例说明如何将大型事实表从行存储表转换为列存储表。  
  
 将行存储表转换为列存储表  
  
1.  首先，创建要在此示例中使用的一个较小的表。  
  
    ```  
    --Create a rowstore table with a clustered index and a non-clustered index.  
    CREATE TABLE MyFactTable (  
        ProductKey [int] NOT NULL,  
        OrderDateKey [int] NOT NULL,  
         DueDateKey [int] NOT NULL,  
         ShipDateKey [int] NOT NULL )  
    )  
    WITH (  
        CLUSTERED INDEX ( ProductKey )  
    );  
  
    --Add a non-clustered index.  
    CREATE INDEX my_index ON MyFactTable ( ProductKey, OrderDateKey );  
    ```  
  
2.  从行存储表中删除所有非聚集索引。  
  
    ```  
    --Drop all non-clustered indexes  
    DROP INDEX my_index ON MyFactTable;  
    ```  
  
3.  删除聚集索引。  
  
    -   仅在您要在将它转换为聚集列存储索引时指定索引的新名称的情况下才这样做。 如果不删除聚集的索引，新的聚集列存储索引具有相同的名称。  
  
        > [!NOTE]  
        >  如果您使用自己的名称，索引的名称可能更易于记住。 所有行存储聚集索引都使用该默认名称是 ClusteredIndex_\<GUID >。  
  
    ```  
    --Process for dropping a clustered index.  
    --First, look up the name of the clustered rowstore index.  
    --Clustered rowstore indexes always use the DEFAULT name ‘ClusteredIndex_<GUID>’.  
    SELECT i.name   
    FROM sys.indexes i   
    JOIN sys.tables t  
    ON ( i.type_desc = 'CLUSTERED' ) WHERE t.name = 'MyFactTable';  
  
    --Drop the clustered rowstore index.  
    DROP INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09 ON MyDimTable;  
    ```  
  
4.  将行存储表转换为具有聚集列存储索引的列存储表。  
  
    ```  
    --Option 1: Convert to columnstore and name the new clustered columnstore index MyCCI.  
    CREATE CLUSTERED COLUMNSTORE INDEX MyCCI ON MyFactTable;  
  
    --Option 2: Convert to columnstore and use the rowstore clustered   
    --index name for the columnstore clustered index name.  
    --First, look up the name of the clustered rowstore index.  
    SELECT i.name   
    FROM sys.indexes i  
    JOIN sys.tables t   
    ON ( i.type_desc = 'CLUSTERED' )  
    WHERE t.name = 'MyFactTable';  
  
    --Second, create the clustered columnstore index and   
    --Replace ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    --with the name of your clustered index.  
    CREATE CLUSTERED COLUMNSTORE INDEX   
    ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
     ON MyFactTable  
    WITH DROP_EXISTING = ON;  
    ```  
  
### <a name="e-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>E. 将列存储表转换为具有聚集索引的行存储表  
 要将列存储表转换为具有聚集索引的行存储表，请使用带 DROP_EXISTING 选项的 CREATE INDEX 语句。  
  
```  
CREATE CLUSTERED INDEX ci_MyTable   
ON MyFactTable  
WITH ( DROP EXISTING = ON );  
```  
  
### <a name="f-convert-a-columnstore-table-to-a-rowstore-heap"></a>F. 将列存储表转换为行存储堆  
 要将列存储表转换为行存储堆，只需删除聚集列存储索引即可。  
  
```  
DROP INDEX MyCCI   
ON MyFactTable;  
```  
  

### <a name="g-defragment-by-rebuilding-the-entire-clustered-columnstore-index"></a>G. 重新生成整个聚集列存储索引进行碎片整理  
   适用于： SQL Server 2014  
  
 有两种方法可以重新生成完整的聚集列存储索引。 你可以使用创建聚集列存储索引，或[ALTER INDEX &#40;Transact SQL &#41;](../../t-sql/statements/alter-index-transact-sql.md)和重新生成选项。 这两种方法可以得到相同的结果。  
  
> [!NOTE]  
>  从 SQL Server 2016 开始，使用 ALTER INDEX REORGANIZE 而不是重新生成与在此示例中所述的方法。  
  
```  
--Determine the Clustered Columnstore Index name of MyDimTable.  
SELECT i.object_id, i.name, t.object_id, t.name   
FROM sys.indexes i   
JOIN sys.tables t  
ON (i.type_desc = 'CLUSTERED COLUMNSTORE')  
WHERE t.name = 'RowstoreDimTable';  
  
--Rebuild the entire index by using CREATE CLUSTERED INDEX.  
CREATE CLUSTERED COLUMNSTORE INDEX my_CCI   
ON MyFactTable  
WITH ( DROP_EXISTING = ON );  
  
--Rebuild the entire index by using ALTER INDEX and the REBUILD option.  
ALTER INDEX my_CCI  
ON MyFactTable  
REBUILD PARTITION = ALL  
WITH ( DROP_EXISTING = ON );  
  
```  
  
##  <a name="nonclustered"></a>对于非聚集列存储索引的示例  
  
### <a name="a-create-a-columnstore-index-as-a-secondary-index-on-a-rowstore-table"></a>A. 创建列存储索引作为一个行存储表上的辅助索引  
 此示例在一个行存储表上创建非聚集列存储索引。 在此情况下，可以创建只有一个列存储索引。 列存储索引需要额外存储空间，因为它包含的行存储表中的数据副本。 此示例创建一个简单的表和聚集的索引，然后演示创建非聚集列存储索引的语法。  
  
```  
CREATE TABLE SimpleTable  
(ProductKey [int] NOT NULL,   
OrderDateKey [int] NOT NULL,   
DueDateKey [int] NOT NULL,   
ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey);  
GO  
```  
  
### <a name="b-create-a-simple-nonclustered-columnstore-index-using-all-options"></a>B. 创建简单的非聚集列存储索引使用所有选项  
 下面的示例演示了通过使用所有选项创建非聚集列存储索引的语法。  
  
```  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey)  
WITH (DROP_EXISTING =  ON,   
    MAXDOP = 2)  
ON "default"  
GO  
```  
  
 使用已分区的表的更复杂示例，请参阅[列存储索引概述](../../relational-databases/indexes/columnstore-indexes-overview.md)。  
  
### <a name="c-create-a-nonclustered-columnstore-index-with-a-filtered-predicate"></a>C. 通过筛选谓词创建非聚集列存储索引  
 下面的示例中的 Production.BillOfMaterials 表上创建筛选的非聚集列存储索引[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库。 筛选谓词可包含那些不是筛选索引中的键列的列。 本示例中的谓词将仅选择其中的 EndDate 为非 NULL 的行。  
  
```  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithEndDate'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
  
```  
  
###  <a name="ncDML"></a> D. 更改非聚集列存储索引中的数据  
   适用于：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。
  
 在您在表上创建非聚集列存储索引后，不能直接在该表中修改数据。 具有插入、 更新、 删除或合并的查询将失败并返回一条错误消息。 若要添加或修改表中的数据，可以执行以下操作之一：  
  
-   禁用或删除列存储索引。 然后可以更新表中的数据。 如果禁用列存储索引，则可以在完成数据更新后重新生成列存储索引。 例如，  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   将数据加载到不含列存储索引的临时表中。 在临时表上生成列存储索引。 将临时表切换到主表的一个空分区中。  
  
-   将分区从具有列存储索引的表切换到一个空的临时表中。 如果在临时表上有某个列存储索引，则禁用该列存储索引。 执行任何更新。 生成（或重新生成）列存储索引。 将临时表切换回主表的（现在为空的）分区中。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-change-a-clustered-index-to-a-clustered-columnstore-index"></a>A. 将聚集的索引更改为聚集列存储索引  
 创建聚集列存储索引语句使用 DROP_EXISTING = ON，你可以：  
  
-   将聚集的索引更改为聚集列存储索引。  
  
-   重新生成聚集列存储索引。  
  
 此示例将 xDimProduct 表创建为行存储表具有聚集索引，，，然后使用创建聚集列存储索引的行存储表的表更改为列存储表。  
  
```  
-- Uses AdventureWorks  
  
IF EXISTS (SELECT name FROM sys.tables  
    WHERE name = N'xDimProduct'  
    AND object_id = OBJECT_ID (N'xDimProduct'))  
DROP TABLE xDimProduct;  
  
--Create a distributed table with a clustered index.  
CREATE TABLE xDimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey)  
WITH ( DISTRIBUTION = HASH(ProductKey),  
    CLUSTERED INDEX (ProductKey) )  
AS SELECT ProductKey, ProductAlternateKey, ProductSubcategoryKey FROM DimProduct;  
  
--Change the existing clustered index   
--to a clustered columnstore index with the same name.  
--Look up the name of the index before running this statement.  
CREATE CLUSTERED COLUMNSTORE INDEX <index_name>   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="b-rebuild-a-clustered-columnstore-index"></a>B. 重新生成聚集列存储索引  
 在前面的示例生成，此示例使用创建聚集列存储索引重新生成调用 cci_xDimProduct 现有聚集列存储索引。  
  
```  
--Rebuild the existing clustered columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_xDimProduct   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="c-change-the-name-of-a-clustered-columnstore-index"></a>C. 更改聚集列存储索引的名称  
 若要更改的聚集列存储索引的名称，删除现有的聚集列存储索引，然后重新创建该索引使用新名称。  
  
 我们建议仅此操作而一个小型表或一个空表。 它需要很长的时间，以删除大型聚集列存储索引并重新生成具有不同的名称。  
  
 使用上一示例中的 cci_xDimProduct 聚集列存储索引，此示例将删除 cci_xDimProduct 聚集列存储索引，并与名称 mycci_xDimProduct 聚集列存储索引，然后重新创建。  
  
```  
--For illustration purposes, drop the clustered columnstore index.   
--The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xDimProduct;  
  
--Create a clustered index with a new name, mycci_xDimProduct.  
CREATE CLUSTERED COLUMNSTORE INDEX mycci_xDimProduct  
ON xdimProduct  
WITH ( DROP_EXISTING = OFF );  
```  
  
### <a name="d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>D. 将列存储表转换为具有聚集索引的行存储表  
 可能的情况下，你想要删除聚集列存储索引并创建聚集的索引。 这将表存储在行存储格式。 此示例将列存储表转换为行存储表具有聚集索引具有相同的名称。 所有数据将丢失。 所有数据将都转到行存储表，并列出的列将成为在聚集索引中的键列。  
  
```  
--Drop the clustered columnstore index and create a clustered rowstore index.   
--All of the columns are stored in the rowstore clustered index.   
--The columns listed are the included columns in the index.  
CREATE CLUSTERED INDEX cci_xDimProduct    
ON xdimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey, WeightUnitMeasureCode)  
WITH ( DROP_EXISTING = ON);  
  
```  
  
### <a name="e-convert-a-columnstore-table-back-to-a-rowstore-heap"></a>E. 将列存储表转换回行存储堆  
 使用[DROP INDEX (SQL Server PDW)](http://msdn.microsoft.com/en-us/f59cab43-9f40-41b4-bfdb-d90e80e9bf32)删除聚集列存储索引并将表转换为行存储堆。 此示例将 cci_xDimProduct 表转换为行存储堆。 表会继续分发，但存储为堆。  
  
```  
--Drop the clustered columnstore index. The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xdimProduct;  
```  

