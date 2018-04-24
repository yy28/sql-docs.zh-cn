---
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f9a0898e617c5bc5b4680ce839e3ffa9ef15132
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回数据库名称。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>参数  
database_id  
要返回的数据库的标识号 (ID)。 database_id 的数据类型为 int，无默认值。 如果未指定 ID，则返回当前数据库名称。
  
## <a name="return-types"></a>返回类型
**nvarchar(128)**
  
## <a name="permissions"></a>权限  
如果 DB_NAME 的调用方并非数据库的所有者，并且数据库不是 master 或 tempdb，则查看对应行所需的最低权限为 ALTER ANY DATABASE 或 VIEW ANY DATABASE 服务器级权限，或者为 master 数据库中的 CREATE DATABASE 权限。 始终可以在 **sys.databases**中查看调用方连接的数据库。
  
> [!IMPORTANT]  
>  默认情况下，公共角色具有 VIEW ANY DATABASE 权限，允许所有登录名查看数据库信息。 要阻止登录名检测数据库，请撤销公共 VIEW ANY DATABASE 权限或拒绝单个登录名的 VIEW ANY DATABASE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-current-database-name"></a>A. 返回当前数据库名称  
以下示例返回当前数据库的名称。
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. 返回指定数据库 ID 的数据库名称  
以下示例返回数据库 ID `3` 的数据库名称。
  
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
以下示例返回每个数据库的数据库名称和 database_id。
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>另请参阅
[DB_ID (Transact-SQL)](../../t-sql/functions/db-id-transact-sql.md)  
[元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

