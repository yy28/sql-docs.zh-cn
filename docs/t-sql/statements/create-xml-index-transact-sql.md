---
title: "创建 XML 索引 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- XML_TSQL
- CREATE_XML_INDEX_TSQL
- XML INDEX
- CREATE_XML_TSQL
- XML
- CREATE XML
- CREATE XML INDEX
- XML_INDEX_TSQL
- FOR_XML_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- CREATE INDEX statement
- index creation [SQL Server], XML indexes
- XML indexes [SQL Server], creating
ms.assetid: c510cfbc-68be-4736-b3cc-dc5b7aa51f14
caps.latest.revision: "38"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7949376e26e184013b9a31258ff757991f4bdd19
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="create-xml-index-transact-sql"></a>CREATE XML INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为指定的表创建 XML 索引。 可在向表中填入数据前创建索引。 可通过指定限定的数据库名称，为另一个数据库中的表创建 XML 索引。  
  
> [!NOTE]  
>  若要创建关系索引，请参阅[CREATE INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-index-transact-sql.md). 有关如何创建空间索引的信息，请参阅[CREATE SPATIAL INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
Create XML Index   
CREATE [ PRIMARY ] XML INDEX index_name   
    ON <object> ( xml_column_name )  
    [ USING XML INDEX xml_index_name   
        [ FOR { VALUE | PATH | PROPERTY } ] ]  
    [ WITH ( <xml_index_option> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_name  
}  
  
<xml_index_option> ::=  
{   
    PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
}  
  
```  
  
## <a name="arguments"></a>参数  
 [PRIMARY] XML  
 创建 XML 索引对指定**xml**列。 指定 PRIMARY 时，会使用由用户表的聚集键形成的聚集键和 XML 节点标识符来创建聚集索引。 每个表最多可具有 249 个 XML 索引。 创建 XML 索引时请注意以下几点：  
  
-   聚集索引必须存在于用户表的主键上。  
  
-   用户表的聚集键被限制为 15 列。  
  
-   每个**xml**表中的列可以具有一个主 XML 索引和多个辅助 XML 索引。  
  
-   在上的一个主 XML 索引**xml**之前可以在列上创建辅助 XML 索引必须存在的列。  
  
-   仅在单个上创建 XML 索引**xml**列。 无法在非上创建 XML 索引**xml**列中，也不能在创建关系索引**xml**列。  
  
-   无法在创建 XML 索引，主或辅助， **xml**上的表值变量的视图中的列**xml**列，或**xml**类型变量。  
  
-   无法对计算创建主 XML 索引**xml**列。  
  
-   SET 选项的设置必须与索引视图或计算列索引所需要的设置相同。 具体而言，选项 ARITHABORT 必须设置为 ON 以及插入、 删除或更新中的值时创建 XML 索引**xml**列。  
  
 有关详细信息，请参阅 [XML 索引 (SQL Server)](../../relational-databases/xml/xml-indexes-sql-server.md)。  
  
 *index_name*  
 索引的名称。 索引名称在表中必须唯一，但在数据库中不必唯一。 索引名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 主 XML 索引名称不能以以下字符开头：  **#** ，  **##** ，  **@** ，或 **@@** .  
  
 *xml_column_name*  
 是**xml**索引所基于的列。 只有一个**xml**列可以指定单个的 XML 索引定义中; 但是，在上创建多个辅助 XML 索引**xml**列。  
  
 USING XML INDEX *xml_index_name*  
 指定创建辅助 XML 索引时要使用的主 XML 索引。  
  
 FOR { VALUE | PATH | PROPERTY }  
 指定辅助 XML 索引的类型。  
  
 Value  
 为主 XML 索引的键列（节点值和路径）所在的列创建辅助 XML 索引。  
  
 PATH  
 为基于主 XML 索引中的路径值和节点值生成的列创建辅助 XML 索引。 在 PATH 辅助索引中，路径值和节点值是用于提高路径搜索效率的键列。  
  
 PROPERTY  
 为 PK 为基表主键的主 XML 索引列（PK、路径值和节点值）创建辅助 XML 索引。  
  
 **\<对象 >:: =**  
  
 要为其建立索引的完全限定对象或非完全限定对象。  
  
 *database_name*  
 数据库的名称。  
  
 *schema_name*  
 表所属架构的名称。  
  
 *table_name*  
 要索引的表的名称。  
  
 **\<xml_index_option >:: =** 
  
 指定创建索引时要使用的选项。  
  
 PAD_INDEX  **=**  {ON |**OFF** }  
 指定索引填充。 默认为 OFF。  
  
 ON  
 通过指定的可用空间的百分比*fillfactor*应用于索引中间级别页。  
  
 关闭或*fillfactor*未指定  
 考虑到中间级页上的键集，将中间级页填充到接近其容量的程度，以留出足够的空间，使之至少能够容纳索引的最大的一行。  
  
 PAD_INDEX 选项只有在指定了 FILLFACTOR 时才有用，因为 PAD_INDEX 使用由 FILLFACTOR 指定的百分比。 如果为 FILLFACTOR 指定的百分比不够大，无法容纳一行，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将在内部覆盖该百分比以允许最小值。 将中间级索引页上的行数为永远不会小于 2，而不考虑如何低值*fillfactor*。  
  
 填充因子 **=** *填充因子*  
 指定一个百分比，指示在[!INCLUDE[ssDE](../../includes/ssde-md.md)]创建或重新生成索引的过程中，应将每个索引页面的叶级填充到什么程度。 *填充因子*必须是介于 1 到 100 的整数值。 默认值为 0。 如果*fillfactor*为 100 或 0，[!INCLUDE[ssDE](../../includes/ssde-md.md)]与完全填充叶级页创建索引。  
  
> [!NOTE]  
>  填充因子的值 0 和 100 在所有方面都是相同的。  
  
 FILLFACTOR 设置仅在创建或重新生成索引时应用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]并不会在页中动态保持指定的可用空间百分比。 若要查看的填充因子设置，请使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目录视图。  
  
> [!IMPORTANT]  
>  使用低于 100 的 FILLFACTOR 值创建聚集索引会影响数据占用的存储空间量，因为[!INCLUDE[ssDE](../../includes/ssde-md.md)]在创建聚集索引时会重新分布数据。  
  
 有关详细信息，请参阅 [为索引指定填充因子](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)。  
  
 SORT_IN_TEMPDB  **=**  {ON |**OFF** }  
 指定是否存储在临时排序结果**tempdb**。 默认为 OFF。  
  
 ON  
 用于生成索引的中间排序结果存储在**tempdb**。 这可能会降低仅当创建索引所需的时间**tempdb**位于不同的与用户数据库的磁盘集。 但是，这会增加索引生成期间所使用的磁盘空间量。  
  
 OFF  
 中间排序结果与索引存储在同一数据库中。  
  
 除了创建索引，在用户数据库中所需的空间**tempdb**必须具有相同数量的额外空间来存储的中间排序结果有关。 有关详细信息，请参阅[SORT_IN_TEMPDB 选项为索引](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)。  
  
 IGNORE_DUP_KEY **= OFF**  
 对 XML 索引不起作用，这是因为此索引类型永远不唯一。 请不要将此选项设置为 ON，否则会引发错误。  
  
 DROP_EXISTING  **=**  {ON |**OFF** }  
 指定删除并重新生成已命名的先前存在的 XML 索引。 默认为 OFF。  
  
 ON  
 删除并重新生成现有索引。 指定的索引名称必须与当前的现有索引相同；但可以修改索引定义。 例如，可以指定不同的列、排序顺序、分区方案或索引选项。  
  
 OFF  
 如果指定的索引名称已存在，则会显示一条错误。  
  
 使用 DROP_EXISTING 不能更改索引类型。 另外，不能将主 XML 索引重新定义为辅助 XML 索引，反之亦然。  
  
 联机**= OFF**  
 指定在索引操作期间基础表和关联的索引不可用于查询和数据修改操作。 在此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，XML 索引不支持联机索引生成操作。 如果针对某个 XML 索引将此选项设置为 ON，则会引发错误。 请省略 ONLINE 选项或将 ONLINE 设为 OFF。  
  
 创建、重新生成或删除 XML 索引的脱机索引操作将获取表的架构修改 (Sch-M) 锁。 这样可以防止所有用户在操作期间访问基础表。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各版本中均不提供联机索引操作。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** |关闭}  
 指定是否允许行锁。 默认值为 ON。  
  
 ON  
 在访问索引时允许使用行锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]确定何时使用行锁。  
  
 OFF  
 不使用行锁。  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** |关闭}  
 指定是否允许使用页锁。 默认值为 ON。  
  
 ON  
 在访问索引时允许使用页锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]确定何时使用页锁。  
  
 OFF  
 不使用页锁。  
  
 MAXDOP  **=**  *max_degree_of_parallelism*  
 重写[配置 max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)索引操作的持续时间的配置选项。 使用 MAXDOP 可以限制在执行并行计划的过程中使用的处理器数量。 最大数量为 64 个处理器。  
  
> [!IMPORTANT]  
>  虽然从语法上讲所有 XML 索引都支持 MAXDOP 选项，但对于主 XML 索引，CREATE XML INDEX 只使用一个处理器。  
  
 *max_degree_of_parallelism*可以是：  
  
 @shouldalert  
 取消生成并行计划。  
  
 \>1  
 基于当前系统工作负荷，将并行索引操作中使用的最大处理器数限制为指定数量或更少。  
  
 0（默认值）  
 根据当前系统工作负荷使用实际的处理器数量或更少数量的处理器。  
  
 有关详细信息，请参阅 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
>  并行索引操作不可用的每个版本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
## <a name="remarks"></a>Remarks  
 从派生的计算列**xml**数据类型可以创建索引作为键或包含非键列，只要计算的列数据类型是允许作为索引键列或非键列。 无法对计算创建主 XML 索引**xml**列。  
  
 若要查看有关 XML 索引的信息，请使用[sys.xml_indexes](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)目录视图。  
  
 有关 XML 索引的详细信息，请参阅[XML 索引 &#40;SQL server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="additional-remarks-on-index-creation"></a>有关创建索引的其他备注  
 有关创建索引的详细信息，请参阅中的"备注"部分[CREATE INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-primary-xml-index"></a>A. 创建主 XML 索引  
 下面的示例为 `CatalogDescription` 表的 `Production.ProductModel` 列创建主 XML 索引。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT * FROM sys.indexes  
            WHERE name = N'PXML_ProductModel_CatalogDescription')  
    DROP INDEX PXML_ProductModel_CatalogDescription   
        ON Production.ProductModel;  
GO  
CREATE PRIMARY XML INDEX PXML_ProductModel_CatalogDescription  
    ON Production.ProductModel (CatalogDescription);  
GO  
```  
  
### <a name="b-creating-a-secondary-xml-index"></a>B. 创建辅助 XML 索引  
 下面的示例为 `CatalogDescription` 表的 `Production.ProductModel` 列创建辅助 XML 索引。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.indexes  
            WHERE name = N'IXML_ProductModel_CatalogDescription_Path')  
    DROP INDEX IXML_ProductModel_CatalogDescription_Path  
        ON Production.ProductModel;  
GO  
CREATE XML INDEX IXML_ProductModel_CatalogDescription_Path   
    ON Production.ProductModel (CatalogDescription)  
    USING XML INDEX PXML_ProductModel_CatalogDescription FOR PATH ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION (Transact-SQL)](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME (Transact-SQL)](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [创建空间索引 &#40;Transact SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;Transact SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [XML 索引 (SQL Server)](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [XML 索引 (SQL Server)](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  

