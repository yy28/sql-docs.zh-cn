---
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DB_NAME
- DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database names [SQL Server], DB_NAME
- names [SQL Server], databases
- viewing database names
- displaying database names
- DB_NAME function
ms.assetid: e21fb33a-a3ea-49b0-bb6b-8f789a675a0e
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f16a13c9fb93d17ecb4efaa62b6ba0eb6cd879d
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945636"
---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函数返回指定数据库的名称。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>参数  
database_id  

将返回其名称 `DB_NAME` 的数据库的标识号 (ID)。 如果对 `DB_NAME` 的调用省略 database_id，则 `DB_NAME` 返回当前数据库的名称。
  
## <a name="return-types"></a>返回类型
**nvarchar(128)**
  
## <a name="permissions"></a>权限  

如果 `DB_NAME` 的调用方不具有特定的非 master 或非 tempdb 数据库，则至少需要 `ALTER ANY DATABASE` 或 `VIEW ANY DATABASE` 服务器级权限才能看到相应的 `DB_ID` 行。 对于 master 数据库，`DB_ID` 至少需要 `CREATE DATABASE` 权限。 调用方连接的数据库将始终出现在 sys.databases 中。
  
> [!IMPORTANT]  
>  默认情况下，公共角色具有 `VIEW ANY DATABASE` 权限，允许所有登录名查看数据库信息。 若要防止登录名检测数据库，则需 `REVOKE` 公共登录名的 `VIEW ANY DATABASE` 权限或 `DENY` 个人登录名的 `VIEW ANY DATABASE` 权限。
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-current-database-name"></a>A. 返回当前数据库名称  
此示例返回当前数据库的名称。
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. 返回指定数据库 ID 的数据库名称  
此示例返回数据库 ID `3` 对应的数据库名称。
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. 返回当前数据库名称  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. 使用数据库 ID 返回数据库名称  
此示例返回每个数据库的数据库名称和 database_id。
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>另请参阅
[DB_ID (Transact-SQL)](../../t-sql/functions/db-id-transact-sql.md)  
[元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

