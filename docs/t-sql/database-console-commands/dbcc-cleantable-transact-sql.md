---
title: DBCC CLEANTABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLEANTABLE_TSQL
- DBCC_CLEANTABLE_TSQL
- DBCC CLEANTABLE
- CLEANTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- disk space [SQL Server], reclaiming
- reclaiming space
- reallocating space
- removing columns
- DBCC CLEANTABLE statement
- space [SQL Server], reclaiming
- deleting columns
- dropping columns
ms.assetid: 0dbbc956-15b1-427b-812c-618a044d07fa
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 01f03593dc5a72c260f44d58da282a67eaa4746b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785478"
---
# <a name="dbcc-cleantable-transact-sql"></a>DBCC CLEANTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
回收表或索引视图中已删除的可变长度列的空间。
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
  
DBCC CLEANTABLE  
(  
    { database_name | database_id | 0 }  
    , { table_name | table_id | view_name | view_id }  
    [ , batch_size ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 database_name | database_id | 0  
 要清除的表所在的数据库。 如果指定 0，则使用当前数据库。 数据库名必须遵循有关[标识符](../../relational-databases/databases/database-identifiers.md)的规则。  
  
 *table_name* | *table_id* | *view_name*| *view_id*  
 要清除的表或索引视图。  
  
 batch_size  
 每个事务处理的行数。 如果未指定，或指定为 0，则该语句将在一个事务中处理整个表。  
  
 WITH NO_INFOMSGS  
 取消显示所有信息性消息。  
  
## <a name="remarks"></a>Remarks  
DBCC CLEANTABLE 用于在删除可变长度列之后回收空间。 可变长度列可以是以下其中一种数据类型：varchar、nvarchar、varchar(max)、nvarchar(max)、varbinary、varbinary(max)、text、ntext、image、sql_variant 和 xml。 该命令不回收删除固定长度列后的空间。
如果删除的列存储在行内，则 DBCC CLEANTABLE 将从表的 IN_ROW_DATA 分配单元回收空间。 如果列存储在行外，则将根据已删除列的数据类型从 ROW_OVERFLOW_DATA 或 LOB_DATA 分配单元回收空间。 如果从 ROW_OVERFLOW_DATA 或 LOB_DATA 页回收空间时产生空页，DBCC CLEANTABLE 将删除该页。
DBCC CLEANTABLE 作为一个或多个事务运行。 如果未指定批大小，则该命令将在一个事务中处理整个表，并在操作过程中以独占方式锁定该表。 对于某些大型表，单个事务的长度和所需的日志空间可能太大。 如果指定批大小，则该命令将在一系列事务中运行，每个事务包括指定的行数。 DBCC CLEANTABLE 不能作为其他事务内的事务运行。
该操作将被完整地记入日志。
不支持对系统表、临时表或表的 xVelocity 内存优化列存储索引部分使用 DBCC CLEANTABLE。
  
## <a name="best-practices"></a>最佳实践  
不应将 DBCC CLEANTABLE 作为日常维护任务来执行。 而应在对表或索引视图中的可变长度列进行重要更改之后并且需要立即回收未使用空间时使用 DBCC CLEANTABLE。 或者，也可以重新生成表或视图的索引；但是，此操作会耗费更多资源。
  
## <a name="result-sets"></a>结果集  
DBCC CLEANTABLE 将返回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
 调用方必须是表或索引视图的所有者，或是 sysadmin 固定服务器角色、db_owner 固定数据库角色或 db_ddladmin 固定数据库角色的成员。  
  
## <a name="examples"></a>示例  
### <a name="a-using-dbcc-cleantable-to-reclaim-space"></a>A. 使用 DBCC CLEANTABLE 回收空间  
以下示例对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库中的 `Production.Document` 表执行 DBCC CLEANTABLE。
  
```sql  
DBCC CLEANTABLE (AdventureWorks2012,'Production.Document', 0)  
WITH NO_INFOMSGS;  
GO  
```  
  
### <a name="b-using-dbcc-cleantable-and-verifying-results"></a>B. 使用 DBCC CLEANTABLE 并验证结果  
以下示例创建一个表并用几个可变长度列填充该表。 然后删除其中两列，并运行 DBCC CLEANTABLE 以回收未使用空间。 在执行 DBCC CLEANTABLE 命令之前和之后，运行查询以验证页计数和已用空间值。
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.CleanTableTest', 'U') IS NOT NULL  
    DROP TABLE dbo.CleanTableTest;  
GO  
CREATE TABLE dbo.CleanTableTest  
    (FileName nvarchar(4000),   
    DocumentSummary nvarchar(max),  
    Document varbinary(max)  
    );  
GO  
-- Populate the table with data from the Production.Document table.  
INSERT INTO dbo.CleanTableTest  
    SELECT REPLICATE(FileName, 1000),   
           DocumentSummary,   
           Document  
    FROM Production.Document;  
GO  
-- Verify the current page counts and average space used in the dbo.CleanTableTest table.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Drop two variable-length columns from the table.  
ALTER TABLE dbo.CleanTableTest  
DROP COLUMN FileName, Document;  
GO  
-- Verify the page counts and average space used in the dbo.CleanTableTest table  
-- Notice that the values have not changed.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Run DBCC CLEANTABLE.  
DBCC CLEANTABLE (AdventureWorks2012,'dbo.CleanTableTest');  
GO  
-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
 [sys.allocation_units (Transact-SQL)](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)  
  
  
