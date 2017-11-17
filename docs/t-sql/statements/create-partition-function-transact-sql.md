---
title: "创建分区函数 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION FUNCTION
- PARTITION
- PARTITION FUNCTION
- PARTITION_FUNCTION_TSQL
- PARTITION_TSQL
- CREATE_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RANGE RIGHT partition functions
- RANGE LEFT partition functions
- partitioned indexes [SQL Server], functions
- functions [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], functions
- CREATE PARTITION FUNCTION statement
ms.assetid: 9dfe8b76-721e-42fd-81ae-14e22258c4f2
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a08cf71066a3713d2eb96ff11bafd951795819ff
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-partition-function-transact-sql"></a>CREATE PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在当前数据库中创建一个函数，该函数可根据指定列的值将表或索引的各行映射到分区。 使用 CREATE PARTITION FUNCTION 是创建已分区表或索引的第一步。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，一张表或一个索引最多可以有 15,000 个分区。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE PARTITION FUNCTION partition_function_name ( input_parameter_type )  
AS RANGE [ LEFT | RIGHT ]   
FOR VALUES ( [ boundary_value [ ,...n ] ] )   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *partition_function_name*  
 是分区函数的名称。 分区函数名称必须在数据库中是唯一且符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 *input_parameter_type*  
 是用于分区的列的数据类型。 所有数据类型都可有效用作分区列，除了 **text**、 **ntext**、 **image**、 **xml**、 **timestamp**、 **varchar(max)**、 **nvarchar(max)**、 **varbinary(max)**、别名数据类型或 CLR 用户定义的数据类型。  
  
 实际列（也称为分区列）是在 CREATE TABLE 或 CREATE INDEX 语句中指定的。  
  
 *小于 boundary_value*  
 指定的已分区的表或索引，使用每个分区的边界值*partition_function_name*。 如果*小于 boundary_value*是空的分区函数映射，将整个表或索引使用*partition_function_name*到单个分区。 只能使用 CREATE TABLE 或 CREATE INDEX 语句中指定的一个分区列。  
  
 *小于 boundary_value*是可引用变量的常量表达式。 这包括用户定义类型变量，或函数以及用户定义函数。 它不能引用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 表达式。 *小于 boundary_value*必须匹配或者为隐式转换中提供的数据类型为*input_parameter_type*，并不能截断的方式的大小和比例的值中的隐式转换的过程不匹配，其对应的*input_parameter_type*。  
  
> [!NOTE]  
>  如果*小于 boundary_value*组成**datetime**或**smalldatetime**文本，这些文本计算假定 us_english 是会话语言。 不推荐使用此行为。 要确保分区函数定义对于所有会话语言都具有预期的行为，建议使用对于所有语言设置都以相同方式进行解释的常量，例如 yyyymmdd 格式；或者将文字值显式转换为特定样式。 若要确定服务器的语言会话，请运行 `SELECT @@LANGUAGE`。  
  
 *...n*  
 指定由提供的值的数目*小于 boundary_value*，不能超过 14,999。 创建的分区数是否等于 *n*  + 1。 不必按顺序列出各值。 如果值未按顺序列出，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]将对它们进行排序、创建函数并返回一个警告，说明未按顺序提供值。 数据库引擎将返回错误，如果 *n* 包括所有重复值。  
  
 **左**|右  
 指定到哪一侧的每个边界值间隔、 左侧或右侧，*小于 boundary_value* [ **，***...n* ] 所属，当间隔值进行排序的[!INCLUDE[ssDE](../../includes/ssde-md.md)]升序顺序从左到右。 如果未指定，则默认值为 LEFT。  
  
## <a name="remarks"></a>注释  
 分区函数的作用域被限制为在其中创建该分区函数的数据库。 在数据库中，分区函数驻留在单独的命名空间与其他函数。  
  
 分区列为空值的所有行都放在最左侧分区中，除非将 NULL 指定为边界值并指定了 RIGHT。 在这种情况下，最左侧分区为空分区，NULL 值被放置在后面的分区中。  
  
## <a name="permissions"></a>Permissions  
 可以使用下列任何一种权限执行 CREATE PARTITION FUNCTION：  
  
-   ALTER ANY DATASPACE 权限。 默认情况下，此权限授予 **sysadmin** 固定服务器角色和 **db_owner** 及 **db_ddladmin** 固定数据库角色的成员。  
  
-   在其中创建分区函数的数据库的 CONTROL 或 ALTER 权限。  
  
-   在其中创建分区函数的数据库所在服务器的 CONTROL SERVER 或 ALTER ANY DATABASE 权限。  
  
##  <a name="BKMK_examples"></a> 示例  
  
### <a name="a-creating-a-range-left-partition-function-on-an-int-column"></a>A. 对 int 列创建 RANGE LEFT 分区函数  
 以下分区函数将表或索引分为四个分区。  
  
```tsql  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
```  
  
 下表显示如何在分区列使用此分区函数的表**col1**划分。  
  
|分区|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**值**|**col1** <= `1`|**col1**  >  `1` AND **col1** <= `100`|**col1**  >  `100` AND **col1** <=`1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-range-right-partition-function-on-an-int-column"></a>B. 对 int 列创建 RANGE RIGHT 分区函数  
 以下分区函数使用的相同值*小于 boundary_value* [ **，***...n* ] 与前面的示例，但它指定 RANGE RIGHT。  
  
```tsql  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE RIGHT FOR VALUES (1, 100, 1000);  
```  
  
 下表显示如何在分区列使用此分区函数的表**col1**划分。  
  
|分区|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**值**|**col1** \<`1`|**col1**  >=  `1` AND **col1** \<`100`|**col1**  >=  `100` AND **col1** \<`1000`|**col1** >= `1000`| 
  
### <a name="c-creating-a-range-right-partition-function-on-a-datetime-column"></a>C. 对 datetime 列创建 RANGE RIGHT 分区函数  
 下面的分区函数分区表或索引为 12 个分区，一个用于每个月内年的中值的有价值**datetime**列。  
  
```tsql  
CREATE PARTITION FUNCTION [myDateRangePF1] (datetime)  
AS RANGE RIGHT FOR VALUES ('20030201', '20030301', '20030401',  
               '20030501', '20030601', '20030701', '20030801',   
               '20030901', '20031001', '20031101', '20031201');  
```  
  
 下表显示如何将表或索引分区列上使用此分区函数**datecol**划分。  
  
|分区|1|2|...|11|12|  
|---------------|-------|-------|---------|--------|--------|  
|**值**|**datecol** \<`February 1, 2003`|**datecol**  >=  `February 1, 2003` AND **datecol** \<`March 1, 2003`||**datecol**  >=  `November 1, 2003` AND **col1** \<`December 1, 2003`|**datecol** >= `December 1, 2003`| 
  
### <a name="d-creating-a-partition-function-on-a-char-column"></a>D. 对 char 列创建分区函数  
 下面的分区函数分区为四个分区的表或索引。  
  
```tsql  
CREATE PARTITION FUNCTION myRangePF3 (char(20))  
AS RANGE RIGHT FOR VALUES ('EX', 'RXE', 'XR');  
```  
  
 下表显示如何在分区列使用此分区函数的表**col1**划分。  
  
|分区|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**值**|**col1** \< `EX`...|**col1**  >=  `EX` AND **col1** \< `RXE`...|**col1**  >=  `RXE` AND **col1** \< `XR`...|**col1** >= `XR`| 
  
### <a name="e-creating-15000-partitions"></a>E. 创建 15,000 个分区  
 以下分区函数将表或索引分为 15,000 个分区。  
  
```tsql  
--Create integer partition function for 15,000 partitions.  
DECLARE @IntegerPartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION IntegerPartitionFunction (int) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i int = 1;  
WHILE @i < 14999  
BEGIN  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N', ';  
SET @i += 1;  
END  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N');';  
EXEC sp_executesql @IntegerPartitionFunction;  
GO  
```  
  
### <a name="f-creating-partitions-for-multiple-years"></a>F. 为多个年度创建分区  
 下面的分区函数分区表或索引为 50 的分区上**datetime2**列。 对于 2007 年 1 月至 2011 年 1 月之间的每个月，都有一个分区。  
  
```tsql  
--Create date partition function with increment by month.  
DECLARE @DatePartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION DatePartitionFunction (datetime2) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i datetime2 = '20070101';  
WHILE @i < '20110101'  
BEGIN  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10)) + '''' + N', ';  
SET @i = DATEADD(MM, 1, @i);  
END  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10))+ '''' + N');';  
EXEC sp_executesql @DatePartitionFunction;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [已分区的表和索引](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [$PARTITION &#40;Transact SQL &#41;](../../t-sql/functions/partition-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;Transact SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [删除分区函数 &#40;Transact SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME (Transact-SQL)](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_functions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  


