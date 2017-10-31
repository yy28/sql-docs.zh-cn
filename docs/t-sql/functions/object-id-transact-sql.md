---
title: "OBJECT_ID (Transact SQL) |Microsoft 文档"
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
- OBJECT_ID
- OBJECT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], IDs
- identification numbers [SQL Server], database objects
- checking object exists
- IDs [SQL Server], database objects
- OBJECT_ID function
- database objects [SQL Server], IDs
- displaying object IDs
- viewing object IDs
- verifying object exists
ms.assetid: f89286db-440f-4218-a828-30881ce3077a
caps.latest.revision: 63
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a612928c3a30b48d3dc8e1dedd4375ca564555d8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="objectid-transact-sql"></a>OBJECT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回架构范围内对象的数据库对象标识号。  
  
> [!IMPORTANT]  
>  使用 OBJECT_ID 不能查询非架构范围内的对象（如 DDL 触发器）。 中找不到的对象[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目录视图，通过查询相应目录视图以获取的对象标识号。 例如，若要返回的 DDL 触发器的对象标识号，请使用`SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
## <a name="arguments"></a>参数  
  *object_name*   
 是要使用的对象。 *object_name*是**varchar**或**nvarchar**。 如果*object_name*是**varchar**，它将隐式转换为**nvarchar**。 可以选择是否指定数据库和架构名称。  
  
  *object_type*   
 架构范围的对象类型。 *object_type*是**varchar**或**nvarchar**。 如果*object_type*是**varchar**，它将隐式转换为**nvarchar**。 对象类型的列表，请参阅**类型**中的列[sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="exceptions"></a>异常  
 对于空间索引，OBJECT_ID 返回 NULL。  
  
 出现错误时，返回 NULL。  
  
 用户只能查看符合如下条件的安全对象的元数据：该安全对象为该用户所有，或已授予该用户对该安全对象的权限。 也就是说，如果用户对该对象没有任何权限，则那些会生成元数据的内置函数（如 OBJECT_ID）可能返回 NULL。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>注释  
 当该参数对系统函数可选时，则采用当前数据库、主机、服务器用户或数据库用户。 内置函数后面必须跟括号。  
  
 除非当前数据库是指定一个临时表名时，数据库名称必须出现在临时表名之前**tempdb**。 例如： `SELECT OBJECT_ID('tempdb..#mytemptable')`。  
  
 在选择列表中，在 WHERE 子句中，可以使用系统函数和允许的表达式的任意位置。 有关详细信息，请参阅[表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)和[其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-object-id-for-a-specified-object"></a>A. 返回指定对象的对象 ID  
 以下示例返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中 `Production.WorkOrder` 表的对象 ID。  
  
```  
USE master;  
GO  
SELECT OBJECT_ID(N'AdventureWorks2012.Production.WorkOrder') AS 'Object ID';  
GO  
```  
  
### <a name="b-verifying-that-an-object-exists"></a>B. 验证对象是否存在  
 以下示例通过验证表是否具有对象 ID 来检查指定表的存在性。 如果该表存在，则将其删除。 如果该表不存在，则不执行 `DROP TABLE` 语句。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'dbo.AWBuildVersion', N'U') IS NOT NULL  
DROP TABLE dbo.AWBuildVersion;  
GO  
```  
  
### <a name="c-using-objectid-to-specify-the-value-of-a-system-function-parameter"></a>C. 使用 OBJECT_ID 指定系统函数的参数值  
 下面的示例返回的所有索引和分区的信息`Person.Address`表中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]通过使用数据库[sys.dm_db_index_operational_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)函数。  
  
> [!IMPORTANT]  
>  在使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数 DB_ID 和 OBJECT_ID 返回参数值时，请始终确保返回有效的 ID。 如果找不到数据库或对象的名称，例如相应名称不存在或拼写不正确，则两个函数都会返回 NULL。 **Sys.dm_db_index_operational_stats**函数将 NULL 解释为指定所有数据库或所有对象的通配符值。 由于这可能是无心之举，所以此部分中的示例说明了确定数据库 ID 和对象 ID 的安全方法。  
  
```  
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
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D： 返回指定对象的对象 ID  
 以下示例返回 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 数据库中 `FactFinance` 表的对象 ID。  
  
```  
SELECT OBJECT_ID(AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>另请参阅  
 [元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION (Transact-SQL)](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_NAME &#40;Transact SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  


