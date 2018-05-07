---
title: sp_describe_first_result_set (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 12890dc6282f879259730530b3ff8f03fc6de8b9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spdescribefirstresultset-transact-sql"></a>sp_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  返回的元数据的第一个可能的结果集的[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理。 如果批处理没有返回结果，则返回一个空的结果集。 如果发出错误[!INCLUDE[ssDE](../../includes/ssde-md.md)]无法确定将由执行静态分析执行的第一个查询的元数据。 动态管理视图[sys.dm_exec_describe_first_result_set &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)返回相同的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@tsql =** ] **'***Transact-SQL_batch***'**  
 一个或多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 *Transact SQL_batch*可能**nvarchar (***n***)** 或**nvarchar (max)**。  
  
 [  **@params =** ] **N***参数*****  
 @params 为参数提供声明字符串[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理，类似于 sp_executesql。 参数可能**nvarchar （n)** 或**nvarchar (max)**。  
  
 一个字符串，它包含的定义中嵌入的所有参数[!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*。 字符串必须是 Unicode 常量或 Unicode 变量。 每个参数定义由参数名称和数据类型组成。 *n*是一个占位符，表示附加参数定义。 必须在定义语句中指定的每个参数@params。 如果[!INCLUDE[tsql](../../includes/tsql-md.md)]语句中的批处理不包含参数，@params不是必需的。 NULL 是此参数的默认值。  
  
 [ **@browse_information_mode =** ] *tinyint*  
 指定是否返回其他键列和源表信息。 如果设置为 1，则分析每个查询，就好像它在查询中包含 FOR BROWSE 选项一样。 将返回其他键列和源表信息。  
  
-   如果设置为 0，则无信息返回。  
  
-   如果设置为 1，则分析每个查询，就好像它在查询中包含 FOR BROWSE 选项一样。 该参数将返回用作源列信息的基表名称。  
  
-   如果设置为 2，则分析每个查询，就好像它用于准备或执行游标一样。 该参数将返回用作源列信息的视图名称。  
  
## <a name="return-code-values"></a>返回代码值  
 **sp_describe_first_result_set**始终返回状态为成功的零。 如果该过程将引发错误，并且作为 RPC 调用该过程，则返回状态由 sys.dm_exec_describe_first_result_set error_type 列中所述的错误类型的填充。 如果从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中调用此过程，则返回值始终为零，甚至在出现错误时也不例外。  
  
## <a name="result-sets"></a>结果集  
 此公共元数据作为结果集返回，结果元数据中的每列对应于一行。 每一行以下面一节所说明的格式描述列的类型和为 Null 性。 如果对于每个控制路径不存在第一个语句，则返回的结果集不包含任何行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**位 NOT NULL**|指示列是出于浏览信息目的而额外添加的列，该列不会实际显示在结果集中。|  
|**column_ordinal**|**int NOT NULL**|在结果集中包含列的序号位置。 第一列的位置将指定为 1。|  
|**名称**|**sysname NULL**|包含列的名称（如果可以确定名称）。 否则，它将包含 NULL。|  
|**is_nullable**|**位 NOT NULL**|如果列允许 NULL，则包含值 1；如果列不允许 NULL，则包含 0；如果不能确定列是否允许 NULL，则为 1。|  
|**system_type_id**|**int NOT NULL**|包含 sys.types 中指定的列的数据类型的 system_type_id。 对于 CLR 类型，即使 system_type_name 列返回 NULL，该列也会返回值 240。|  
|**system_type_name**|**nvarchar(256) NULL**|包含为列数据类型指定的名称和参数（例如，length、precision、scale）。 如果数据类型是用户定义的别名类型，则会在此处指定基本系统类型。 如果数据类型是 CLR 用户定义类型，则在此列中返回 NULL。|  
|**max_length**|**Smallint 不为 NULL**|列的最大长度（字节）。<br /><br /> 为-1 = 的列数据类型为**varchar （max)**， **nvarchar (max)**， **varbinary （max)**，或**xml**。<br /><br /> 有关**文本**列， **max_length**值将为 16 或设置的值**sp_tableoption 'text in row**。|  
|**精度**|**tinyint 不为 NULL**|如果为基于数值的列，则为该列的精度。 否则，返回 0。|  
|**小数位数**|**tinyint 不为 NULL**|如果基于数值，则为列的小数位数。 否则，返回 0。|  
|**collation_name**|**sysname NULL**|如果列包含的是字符，则为该列的排序规则的名称。 否则返回 NULL。|  
|**user_type_id**|**int NULL**|对于 CLR 和别名类型，包含在 sys.types 中指定的列数据类型的 user_type_id。 否则为 NULL。|  
|**user_type_database**|**sysname NULL**|对于 CLR 和别名类型，包含在其中定义相应类型的数据库的名称。 否则为 NULL。|  
|**user_type_schema**|**sysname NULL**|对于 CLR 和别名类型，包含在其中定义相应类型的架构的名称。 否则为 NULL。|  
|**user_type_name**|**sysname NULL**|对于 CLR 和别名类型，包含类型的名称。 否则为 NULL。|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|对于 CLR 类型，返回定义类型的程序集和类的名称。 否则为 NULL。|  
|**xml_collection_id**|**int NULL**|包含 sys.columns 中指定的列数据类型的 xml_collection_id。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**xml_collection_database**|**sysname NULL**|包含定义与此类型关联的 XML 架构集合的数据库。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**xml_collection_schema**|**sysname NULL**|包含定义与此类型关联的 XML 架构集合的架构。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**xml_collection_name**|**sysname NULL**|包含与此类型关联的 XML 架构集合的名称。 如果返回的类型与 XML 架构集合不关联，则该列将返回 NULL。|  
|**is_xml_document**|**位 NOT NULL**|如果返回的数据类型为 XML，并且保证该类型是完整的 XML 文档（包含根节点，与 XML 片段相对），则返回 1。 否则，返回 0。|  
|**is_case_sensitive**|**位 NOT NULL**|如果列为区分大小写的字符串类型，则返回 1；否则为 0。|  
|**is_fixed_length_clr_type**|**位 NOT NULL**|如果列为固定长度 CLR 类型，则返回 1；否则为 0。|  
|**source_server**|**sysname**|此结果中的此列返回的源服务器的名称（如果结果源自远程服务器）。 在 sys.servers 中所示，未提供名称。 如果列来自本地服务器或无法确定它来自的服务器，则返回 NULL。 仅在请求浏览信息填充。|  
|**source_database**|**sysname**|此结果中的列返回的源数据库的名称。 如果无法确定该数据库，则返回 NULL。 仅在请求浏览信息填充。|  
|**source_schema**|**sysname**|此结果中的列返回的源架构的名称。 如果无法确定该架构，则返回 NULL。 仅在请求浏览信息填充。|  
|**source_table**|**sysname**|此结果中的列返回的源表的名称。 如果无法确定该表，则返回 NULL。 仅在请求浏览信息填充。|  
|**source_column**|**sysname**|结果列返回的源列的名称。 如果无法确定该列，则返回 NULL。 仅在请求浏览信息填充。|  
|**is_identity_column**|**位 NULL**|如果列是标识列，则返回 1；否则，返回 0。 如果无法确定列是否为标识列，则返回 NULL。|  
|**is_part_of_unique_key**|**位 NULL**|如果列是唯一索引的一部分（包括唯一和主要的约束），则返回 1；否则，返回 0。 如果无法确定列是否为唯一索引的一部分，则返回 NULL。 仅在请求浏览信息时填充它。|  
|**is_updateable**|**位 NULL**|如果可以更新列，则返回 1；否则，返回 0。 如果无法确定是否可以更新列，则返回 NULL。|  
|**is_computed_column**|**位 NULL**|如果列是计算列，则返回 1；否则，返回 0。 如果无法确定列是计算的列，返回 NULL。|  
|**is_sparse_column_set**|**位 NULL**|如果列是稀疏列，则返回 1；否则，返回 0。 如果无法确定列是稀疏列集的一部分，则返回 NULL。|  
|**ordinal_in_order_by_list**|**smallint NULL**|此列在 ORDER BY 列表中的位置。 如果 ORDER BY 列表中不显示该列或无法唯一确定 ORDER BY 列表，则返回 NULL。|  
|**order_by_list_length**|**smallint NULL**|ORDER BY 列表的长度。 如果没有 ORDER BY 列表，或者无法唯一确定 ORDER BY 列表，则返回 NULL。 请注意，此值将是相同的返回的所有行**sp_describe_first_result_set。**|  
|**order_by_is_descending**|**smallint NULL**|如果 ordinal_in_order_by_list 不为 NULL， **order_by_is_descending**列报告此列的 ORDER BY 子句的方向。 否则，它报告 NULL。|  
|**tds_type_id**|**int NOT NULL**|供内部使用。|  
|**tds_length**|**int NOT NULL**|供内部使用。|  
|**tds_collation_id**|**int NULL**|供内部使用。|  
|**tds_collation_sort_id**|**tinyint NULL**|供内部使用。|  
  
## <a name="remarks"></a>注释  
 **sp_describe_first_result_set**保证，如果该过程返回 （一个假想） 的第一个结果集元数据批处理 A 和该批处理 （A） 是否随后执行然后批处理将任一 (1) 引发优化时间错误，(2)引发运行时错误，(3) 返回任何结果集，或者 (4) 返回的第一个结果集所描述的相同元数据与**sp_describe_first_result_set**。  
  
 名称、为 Null 性和数据类型可能不同。 如果**sp_describe_first_result_set**返回空结果集，保证是批处理执行将返回任何结果集。  
  
 此保证假定在服务器上没有相关的架构更改。 服务器上的相关的架构更改不包括创建临时表或表的时间之间的一个批次中的变量， **sp_describe_first_result_set**调用过程中返回结果集的时间执行，包括批处理 B.进行架构更改  
  
 **sp_describe_first_result_set**在任何以下情况下将返回错误。  
  
-   如果输入@tsql不是有效[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理。 通过分析和分析确定有效性[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理。 在查询优化过程中或在执行期间由批处理导致的任何错误时确定不考虑是否[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理无效。  
  
-   如果@params不为 NULL 且包含一个字符串，不是有效语法声明字符串参数，或如果它包含一个字符串，其用于声明任何参数不止一次。  
  
-   如果输入[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理声明具有相同名称的本地变量，如中声明的参数@params。  
  
-   如果该语句将使用某个临时表。  
  
-   查询包括创建随后要查询的永久表。  
  
 如果所有其他检查都获得成功，则将考虑输入批处理内所有可能的控制流路径。 此操作将为帐户所有控件流语句 (GOTO、 IF/ELSE，尽管，和[!INCLUDE[tsql](../../includes/tsql-md.md)]TRY/CATCH 块) 以及任何的过程中，动态[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理或从输入批处理调用 EXEC 语句，使 DDL 语句的触发器DDL 触发器来激发或导致要激发的触发器目标表或修改由于级联操作上的外键约束的表上的 DML 语句。 在很多可能的控制路径的情况下，算法将在某个点停止。  
  
 对于每个控制流路径中，第一个语句 （如果有），返回的结果集由**sp_describe_first_result_set**。  
  
 当在一个批处理中找到多个可能的第一个语句时，其结果可能在列数、列名称、为 Null 性以及数据类型等方面存在不同。 此处详细介绍了如何处理这些差异：  
  
-   如果列数不同，则会引发一个错误，但不返回任何结果。  
  
-   如果列名称不同，则返回的列名称将设置为 NULL。  
  
-   如果为 Null 性不同，则返回的为 Null 性将允许 NULL。  
  
-   如果数据类型不同，则将引发错误而不返回任何结果，但以下情况除外：  
  
    -   **varchar(a)** 到**varchar(a')** 其中 >。  
  
    -   **varchar(a)** 到**varchar （max)**  
  
    -   **nvarchar(a)** 到**nvarchar(a')** 其中 >。  
  
    -   **nvarchar(a)** 到**nvarchar (max)**  
  
    -   **varbinary(a)** 到**varbinary(a')** 其中 >。  
  
    -   **varbinary(a)** 到**varbinary （max)**  
  
 **sp_describe_first_result_set**不支持间接递归。  
  
## <a name="permissions"></a>权限  
 需要有权执行@tsql自变量。  
  
## <a name="examples"></a>示例  
  
### <a name="typical-examples"></a>典型示例  
  
#### <a name="a-simple-example"></a>A. 简单示例  
 下面的示例描述从单个查询中返回的结果集。  
  
```  
sp_describe_first_result_set @tsql = N'SELECT object_id, name, type_desc FROM sys.indexes'  
```  
  
 下面的示例显示了从包含一个参数的单个查询中返回的结果集。  
  
```  
sp_describe_first_result_set @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes   
WHERE object_id = @id1'  
, @params = N'@id1 int'  
```  
  
#### <a name="b-browse-mode-examples"></a>B. 浏览模式示例  
 以下三个示例演示了不同浏览信息模式之间的主要差异。 只有相关的列会包含在查询结果中。  
  
 以下示例使用 0，指示无信息返回。  
  
```sql  
CREATE TABLE dbo.t (a int PRIMARY KEY, b1 int);  
GO  
CREATE VIEW dbo.v AS SELECT b1 AS b2 FROM dbo.t;  
GO  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM dbo.v', null, 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|NULL|NULL|NULL|NULL|  
  
 以下示例使用 1，指示它将返回信息，就好像它在查询中包含 FOR BROWSE 选项一样。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|dbo|t|B1|0|  
|1|2|（英文）。|dbo|t|（英文）。|1|  
  
 以下示例使用 2，指示执行分析，就好像您在准备游标一样。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|B3|dbo|v|B2|0|  
|1|2|ROWSTAT|NULL|NULL|NULL|0|  
  
### <a name="examples-of-problems"></a>问题示例  
 下面的示例对所有示例使用两个表。 请执行以下语句以创建示例表。  
  
```  
CREATE TABLE dbo.t1 (a int NULL, b varchar(10) NULL, c nvarchar(10) NULL);  
CREATE TABLE dbo.t2 (a smallint NOT NULL, d varchar(20) NOT NULL, e int NOT NULL);  
```  
  
#### <a name="error-because-the-number-of-columns-differ"></a>由于列数不同而出错  
 在此示例中，可能的第一个结果集中的列数不同。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a, b FROM t1;  
SELECT * FROM t; -- Ignored, not a possible first result set.'  
  
```  
  
#### <a name="error-because-the-data-types-differ"></a>由于数据类型不同而出错  
 列类型在不同的第一个可能结果集中不同。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a FROM t2;  
```  
  
 结果： 错误，类型不匹配 (**int**与**smallint**)。  
  
#### <a name="column-name-cannot-be-determined"></a>无法确定列名称  
 对于同一个变量长度类型、为 Null 性以及列名称，可能的第一个结果集的列因长度不同而不同：  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d FROM t2; '  
```  
  
 结果：\<未知的列名称 > **varchar （20) NULL**  
  
#### <a name="column-name-forced-to-be-identical-through-aliasing"></a>通过别名强制列名称完全相同  
 与前面的例子相同，但通过列别名，列具有相同名称。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d AS b FROM t2;'  
```  
  
 结果： b **varchar (20) 为 NULL**  
  
#### <a name="error-because-column-types-cannot-be-matched"></a>由于列类型无法匹配而出错  
 列类型与不同，在不同的可能结果集的第一次。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT c FROM t1;'  
```  
  
 结果： 错误，类型不匹配 (**varchar(10)** 与**nvarchar(10)**)。  
  
#### <a name="result-set-can-return-an-error"></a>结果集可以返回一个错误  
 第一次结果集是错误或结果集。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RAISERROR(''Some Error'', 16, 1);  
  
ELSE  
    SELECT a FROM t1;  
SELECT e FROM t2; -- Ignored, not a possible first result set.;'  
```  
  
 结果： **intNULL**  
  
#### <a name="some-code-paths-return-no-results"></a>某些代码路径不返回任何结果  
 第一次结果集是 Null 或结果集。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 结果： **intNULL**  
  
#### <a name="result-from-dynamic-sql"></a>动态 SQL 中的结果  
 第一个结果集是可发现的动态 SQL，因为它是文字字符串。  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 结果： **INT NULL**  
  
#### <a name="result-failure-from-dynamic-sql"></a>动态 SQL 中的结果失败  
 第一个结果集因为动态 SQL 而未定义。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL); '  
```  
  
 结果：错误。 结果由于动态 SQL 而无法发现。  
  
#### <a name="result-set-specified-by-user"></a>用户指定的结果集  
 第一个结果集由用户手动指定。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL)  
    WITH RESULT SETS(  
        (Column1 BIGINT NOT NULL)  
    ); '  
```  
  
 结果： Column1 **bigint 不为 NULL**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>不明确的结果集导致的错误  
 此示例假定名为 user1 的另一个用户具有名为 t1 列具有默认架构 s1 中的表 ( **int NOT NULL**)。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 结果：错误。 t1 可以 dbo.t1 或 s1.t1，每个都有的列数不同。  
  
#### <a name="result-even-with-ambiguous-result-set"></a>在使用不明确的结果集时的结果  
 与前一个示例采用相同的假设。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 结果： **int NULL**由于 dbo.t1.a 和 s1.t1.a 具有类型**int**和不同的可为 null。  
  
## <a name="see-also"></a>另请参阅  
 [sp_describe_undeclared_parameters &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
 
