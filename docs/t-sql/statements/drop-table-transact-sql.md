---
title: "DROP TABLE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_TABLE_TSQL
- DROP TABLE
dev_langs:
- TSQL
helpviewer_keywords:
- removing indexes
- table removal [SQL Server]
- deleting indexes
- dropping data
- deleting tables
- dropping indexes
- removing constraints
- removing permissions
- DROP TABLE statement
- removing tables
- deleting triggers
- removing data
- dropping tables
- deleting permissions
- dropping triggers
- deleting constraints
- removing triggers
- deleting data
- dropping constraints
- dropping permissions
ms.assetid: 0b6f2b6f-3aa3-4767-943f-43df3c3c5cfd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: df9843e4b72c6a8092756725d1d4b3f96eefec74
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="drop-table-transact-sql"></a>DROP TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  删除一个或多个表定义以及这些表的所有数据、索引、触发器、约束和权限规范。 任何视图或引用已删除的表的存储的过程必须显式删除通过使用[DROP VIEW](../../t-sql/statements/drop-view-transact-sql.md)或[DROP PROCEDURE](../../t-sql/statements/drop-procedure-transact-sql.md)。 若要对表中报告的依赖关系，使用[sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP TABLE [ IF EXISTS ] [ database_name . [ schema_name ] . | schema_name . ]  
table_name [ ,...n ]  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name   
[;]  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 要在其中创建表的数据库的名称。  
  
 Windows Azure SQL Database 支持由三部分组成的格式 database_name.[schema_name].object_name，其中 database_name 为当前数据库，database_name 为 tempdb，object_name 以 # 开头。 Windows Azure SQL Database 不支持由四部分组成的名称。  
  
 *如果存在*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 仅当它已存在，则有条件地除去表。  
  
 *schema_name*  
 表所属架构的名称。  
  
 *table_name*  
 要删除的表的名称。  
  
## <a name="remarks"></a>注释  
 不能使用 DROP TABLE 删除被 FOREIGN KEY 约束引用的表。 必须先删除引用 FOREIGN KEY 约束或引用表。 如果要在同一个 DROP TABLE 语句中删除引用表以及包含主键的表，则必须先列出引用表。  
  
 可以在任何数据库中删除多个表。 如果一个要删除的表引用了另一个也要删除的表的主键，则必须先列出包含该外键的引用表，然后再列出包含要引用的主键的表。  
  
 删除表时，表的规则或默认值将被解除绑定，与该表关联的任何约束或触发器将被自动删除。 如果要重新创建表，则必须重新绑定相应的规则和默认值，重新创建某些触发器，并添加所有必需的约束。  
  
 如果你通过使用 DELETE 删除表中的所有行*tablename*或使用 TRUNCATE TABLE 语句，该表存在删除之前。  
  
 删除使用了超过 128 个区的大型表和索引时，需要分两个单独的阶段：逻辑和物理阶段。 在逻辑阶段中，对表使用的现有分配单元进行标记以便释放，并对其进行锁定，直到事务提交为止。 在物理阶段，标记为要释放的 IAM 页被成批地物理删除。  
  
 如果删除的表包含带有 FILESTREAM 属性的 VARBINARY (MAX) 列，则不会删除在文件系统中存储的任何数据。  
  
> [!IMPORTANT]  
>  不应在同一个批处理中对同一个表执行 DROP TABLE 和 CREATE TABLE。 否则，可能出现意外错误。  
  
## <a name="permissions"></a>Permissions  
 需要拥有该表所属架构的 ALTER 权限、该表的 CONTROL 权限或 **db_ddladmin** 固定数据库角色中的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-dropping-a-table-in-the-current-database"></a>A. 删除当前数据库中的表  
 以下示例将从当前数据库中删除 `ProductVendor1` 表及其数据和索引。  
  
```  
DROP TABLE ProductVendor1 ;  
```  
  
### <a name="b-dropping-a-table-in-another-database"></a>B. 删除其他数据库中的表  
 以下示例将删除 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中的 `SalesPerson2` 表。 可以在服务器实例上的任何数据库中执行此示例。  
  
```  
DROP TABLE AdventureWorks2012.dbo.SalesPerson2 ;  
```  
  
### <a name="c-dropping-a-temporary-table"></a>C. 删除临时表  
 以下示例将创建一个临时表，测试该表是否存在，删除该表，然后再次测试该表是否存在。 此示例不使用**IF EXISTS**语法，可以在开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
```  
CREATE TABLE #temptable (col1 int);  
GO  
INSERT INTO #temptable  
VALUES (10);  
GO  
SELECT * FROM #temptable;  
GO  
IF OBJECT_ID(N'tempdb..#temptable', N'U') IS NOT NULL   
DROP TABLE #temptable;  
GO  
--Test the drop.  
SELECT * FROM #temptable;  
  
```  
  
### <a name="d-dropping-a-table-using-if-exists"></a>D. 删除使用 IF EXISTS 表  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 下面的示例创建名为 T1 的表。 然后第二个语句会删除表。 第三个语句不执行任何操作因为此表已删除，但它不会导致错误。  
  
```  
CREATE TABLE T1 (Col1 int);  
GO  
DROP TABLE IF EXISTS T1;  
GO  
DROP TABLE IF EXISTS T1;  
```  
  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_spaceused (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [TRUNCATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [删除视图 &#40;Transact SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [DROP PROCEDURE &#40;Transact SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_expression_dependencies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
