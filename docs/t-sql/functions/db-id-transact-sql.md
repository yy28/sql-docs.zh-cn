---
title: "DB_ID (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DB_ID_TSQL
- DB_ID
dev_langs:
- TSQL
helpviewer_keywords:
- viewing database ID numbers
- IDs [SQL Server], databases
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
- displaying database ID numbers
- DB_ID function
ms.assetid: 7b3aef89-a6fd-4144-b468-bf87ebf381b8
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 99497c63e037054daf249ac75ef35073f102a498
ms.contentlocale: zh-cn
ms.lasthandoff: 09/06/2017

---
# <a name="dbid-transact-sql"></a>DB_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回数据库标识 (ID) 号。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>参数  
*database_name*  
用于返回对应的数据库 ID 的数据库名称。 *database_name*是**sysname**。 如果*database_name*是省略，则返回当前数据库 ID。
  
## <a name="return-types"></a>返回类型
**int**
  
## <a name="permissions"></a>Permissions  
如果调用方**DB_ID**不是数据库的所有者和该数据库未**master**或**tempdb**，请参阅相应的行所需的最小权限是ALTER ANY DATABASE 或 VIEW ANY DATABASE 服务器级权限，或者在 CREATE DATABASE 权限**master**数据库。 始终可以在 **sys.databases**中查看调用方连接的数据库。
  
> [!IMPORTANT]  
>  默认情况下，公共角色具有 VIEW ANY DATABASE 权限，允许所有登录名，若要查看数据库信息。 若要阻止来自能够检测到数据库的登录名，请撤消从公共的的 VIEW ANY DATABASE 权限或拒绝单个登录名的 VIEW ANY DATABASE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>A. 返回当前数据库的数据库 ID  
以下示例将返回当前数据库的数据库 ID
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. 返回指定数据库的数据库 ID  
下面的示例返回的数据库 ID[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库。
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-dbid-to-specify-the-value-of-a-system-function-parameter"></a>C. 使用 DB_ID 来指定系统函数参数的值  
下面的示例使用`DB`_`ID`要返回的数据库 ID[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]系统函数中的数据库`sys.dm_db` \_ `index` \_ `operational` \_ `stats`. 此函数将数据库 ID 作为第一个参数。
  
```sql
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. 返回当前数据库的 ID  
以下示例将返回当前数据库的数据库 ID
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. 返回指定的数据库的 ID。  
下面的示例返回 AdventureWorksDW2012 数据库的数据库 ID。
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>另请参阅
[DB_NAME &#40;Transact SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)  
[元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  


