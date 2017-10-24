---
title: "重命名 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/13/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
caps.latest.revision: 15
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d58470957ab58085ddd6a733cf30dbc77ce7439a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="rename-transact-sql"></a>重命名 (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  重命名的用户创建的表中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 重命名的用户创建的表或数据库中的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
> [!NOTE]  
>  若要重命名的数据库中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或[!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用存储的过程[sp_renamedb &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md).  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
-- Rename a table.  
RENAME OBJECT [ :: ]  [ [ database_name .  [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name  
[;]  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- Rename a table  
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name  
[;]  
  
-- Rename a database  
RENAME DATABASE [::] database_name TO new_database_name  
[;]  
```  
  
## <a name="arguments"></a>参数  
 重命名对象 [:]   
          [[*database_name* 。 [ *schema_name* ]。 ] |[ *schema_name* 。 ]]*table_name*收件人*new_table_name*  
 **适用于：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 更改用户定义表的名称。 指定要与一维、 两个或三个部分组成的名称重命名的表。    指定新的表*new_table_name*作为一个部分名称。  
  
 重命名数据库 [:]   
          [ *database_name*收件人*new_database_name*  
 **适用于：**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 更改从用户定义的数据库的名称*database_name*到*new_database_name*。  你无法将数据库重命名为下列任一[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]保留数据库名称：  
  
-   master  
  
-   model  
  
-   msdb  
  
-   tempdb  
  
-   pdwtempdb1  
  
-   pdwtempdb2  
  
-   : DWConfiguration  
  
-   DWDiagnostics  
  
-   DWQueue  
  
## <a name="permissions"></a>Permissions  
 若要运行此命令需要此权限：  
  
-   **ALTER**对表的权限  
   
  
## <a name="limitations-and-restrictions"></a>限制和局限  
  
### <a name="cannot-rename-an-external-table-indexes-or-views"></a>无法重命名外部表、 索引或视图
无法重命名外部表、 索引或视图。 而不是重命名，你可以删除外部表、 索引或视图，然后使用新名称重新创建它。

### <a name="cannot-rename-a-table-in-use"></a>无法重命名的表中使用  
 在使用时，你无法重命名表或数据库。 重命名表需要在表上的排他锁。 如果表中使用，则你可能需要终止使用该表的会话。 若要终止会话可以使用 KILL 命令。 谨慎使用 KILL，因为终止会话时将回滚任何未提交的工作。 SQL 数据仓库中的会话 sid 作为前缀。 你将需要调用 KILL 命令时包括这和会话数。 此示例中查看活动或空闲会话的列表，然后终止会话 SID1234。  
  
### <a name="views-are-not-updated"></a>不会更新视图  
 如果重命名数据库，使用以前的数据库名称的所有视图将都变为无效。 这适用于视图内部和外部数据库。 例如，如果销售数据库已重命名，视图包含`SELECT * FROM Sales.dbo.table1`将变为无效。 若要解决此问题，可以避免在视图中，使用由三部分名称，或更新的视图来引用新的数据库名称。  
  
 时重命名表，视图不会更新，以引用新的表名称。 每个视图中，内部或外部引用以前表名称的数据库将变为无效。 若要解决此问题，可以更新每个视图，以引用新的表名称。  
  
## <a name="locking"></a>锁定  
 重命名表将对数据库对象的共享的锁、 架构对象上的共享的锁和表的排他锁。  
  
## <a name="examples"></a>示例  
  
### <a name="a-rename-a-database"></a>A. 重命名数据库  
 **适用于：** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]仅    
  
 此示例将用户定义的数据库 AdWorks 重命名为 AdWorks2。  
  
```  
-- Rename the user defined database AdWorks  
RENAME DATABASE AdWorks to AdWorks2;  
  
```  
  
 当重命名表，所有对象和与该表关联的属性都更新为引用新的表名称。 例如，表定义、 索引、 约束，并更新权限。 不会更新视图。  
  
### <a name="b-rename-a-table"></a>B. 重命名表  
 **适用于：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 此示例将 Customer 表重命名为 Customer1。  
  
```  
-- Rename the customer table  
RENAME OBJECT Customer TO Customer1;  
  
RENAME OBJECT mydb.dbo.Customer TO Customer1;  
```  
  
 当重命名表，所有对象和与该表关联的属性都更新为引用新的表名称。 例如，表定义、 索引、 约束，并更新权限。 不会更新视图。  
   
  
### <a name="c-move-a-table-to-a-different-schema"></a>C. 将表移动到另一个架构  
 **适用于：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 如果你想要将对象移动到另一个架构，则使用[ALTER SCHEMA &#40;Transact SQL &#41;](../../t-sql/statements/alter-schema-transact-sql.md). 例如，此选项移动表项从产品架构 dbo 架构。  
  
```  
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;  
```  
  
### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. 终止会话之前重命名表  
 **适用于：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 请务必记住，在使用时，不能重命名表。 重命名表需要在表上的排他锁。 如果表中使用，则你可能需要终止使用该表的会话。 若要终止会话可以使用 KILL 命令。 谨慎使用 KILL，因为终止会话时将回滚任何未提交的工作。 SQL 数据仓库中的会话 sid 作为前缀。 你将需要调用 KILL 命令时包括这和会话数。 此示例中查看活动或空闲会话的列表，然后终止会话 SID1234。  
  
```  
-- View a list of the current sessions  
SELECT session_id, login_name, status   
FROM sys.dm_pdw_exec_sessions   
WHERE status='Active' OR status='Idle';  
  
-- Terminate a session using the session_id.  
KILL 'SID1234';  
```  
  
  

