---
title: "PARSENAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs:
- TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 63065dcee0d1f7784e7be396273785f741ef44c7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  返回对象名称的指定部分。 可检索的对象部分包括对象名称、所有者名称、数据库名称和服务器名称。  
  
> [!NOTE]  
>  PARSENAME 函数不指示指定名称的对象是否存在。 PARSENAME 仅返回指定对象名称的指定部分。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>参数  
 *object_name*  
 要检索其指定部分的对象的名称。 *object_name*是**sysname**。 此参数是可选的限定对象名称。 如果对象名称的所有部分都是限定的，则此名称可包含四部分：服务器名称、数据库名称、所有者名称以及对象名称。  
  
 *object_piece*  
 要返回的对象部分。 *object_piece*属于类型**int**，并且可能具有这些值：  
  
 1 = 对象名称  
  
 2 = 架构名称  
  
 3 = 数据库名称  
  
 4 = 服务器名称  
  
## <a name="return-types"></a>返回类型  
 **nchar**  
  
## <a name="remarks"></a>注释  
 如果存在下列条件之一，则 PARSENAME 返回 NULL：  
  
-   任一*object_name*或*object_piece*为 NULL。  
  
-   发生语法错误。  
  
 请求的对象部分的长度为 0 和不是有效[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符。 长度为零的对象的名称将使整个限定名称无效。  
  
## <a name="examples"></a>示例  
 以下示例使用 `PARSENAME` 返回有关 `Person` 数据库中 `AdventureWorks2012` 表的信息。  
  
```  
USE AdventureWorks2012;  
SELECT PARSENAME('AdventureWorks2012..Person', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorks2012..Person', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorks2012..Person', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorks2012..Person', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Object Name`  
  
 `------------------------------`  
  
 `Person`  
  
 `(1 row(s) affected)`  
  
 `Schema Name`  
  
 `------------------------------`  
  
 `(null)`  
  
 `(1 row(s) affected)`  
  
 `Database Name`  
  
 `------------------------------`  
  
 `AdventureWorks2012`  
  
 `(1 row(s) affected)`  
  
 `Server Name`  
  
 `------------------------------`  
  
 `(null)`  
  
 `(1 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例使用 `PARSENAME` 返回有关 `Person` 数据库中 `AdventureWorks2012` 表的信息。  
  
```  
-- Uses AdventureWorks  
  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Object Name`  
  
 `------------------------------`  
  
 `DimCustomer`  
  
 `(1 row(s) affected)`  
  
 `Schema Name`  
  
 `------------------------------`  
  
 `dbo`  
  
 `(1 row(s) affected)`  
  
 `Database Name`  
  
 `------------------------------`  
  
 `AdventureWorksPDW2012`  
  
 `(1 row(s) affected)`  
  
 `Server Name`  
  
 `------------------------------`  
  
 `(null)`  
  
 `(1 row(s) affected)`  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [系统函数 &#40;Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  


