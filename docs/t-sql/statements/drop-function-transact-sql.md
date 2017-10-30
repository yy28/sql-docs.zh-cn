---
title: "放置函数 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FUNCTION_TSQL
- DROP FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined functions [SQL Server], removing
- removing user-defined functions
- DROP FUNCTION statement
- dropping user-defined functions
- deleting user-defined functions
ms.assetid: ee5ad283-9e44-4109-902f-0ce12669ee11
caps.latest.revision: 49
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b85cb68749cdcf88d62d9d8fbf136a37e845519
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  从当前数据库中删除一个或多个用户定义函数。 用户定义函数通过使用创建[CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md)和可通过修改[ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md)。  
  
 放置函数支持本机编译标量用户定义函数。 有关详细信息，请参阅[内存中 OLTP 的标量用户定义函数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```  
 -- Azure SQL Data Warehouse, Parallel Data Warehouse 

DROP FUNCTION [ schema_name. ] function_name
[;] 
```  
   
  
## <a name="arguments"></a>参数  
 *如果存在*    
 有条件地删除函数，仅当它已存在。 可用开头[!INCLUDE[ssnoversion_md](../../includes/ssnoversion_md.md)]2016年并在[!INCLUDE[sssds_md](../../includes/sssds_md.md)]。
  
 *schema_name*  
 用户定义函数所属的架构的名称。  
  
 *function_name*  
 要删除的用户定义函数的名称。 可以选择是否指定架构名称。 不能指定服务器名称和数据库名称。  
  
## <a name="remarks"></a>注释  
 如果数据库中存在引用 DROP FUNCTION 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数或视图并且这些函数或视图通过使用 SCHEMABINDING 创建，或者存在引用该函数的计算列、CHECK 约束或 DEFAULT 约束，则 DROP FUNCTION 将失败。  
  
 如果存在引用此函数并且已生成索引的计算列，则 DROP FUNCTION 将失败。  
  
## <a name="permissions"></a>Permissions  
 若要执行 DROP FUNCTION，用户至少应对函数所属架构具有 ALTER 权限，或对函数具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-dropping-a-function"></a>A. 删除函数  
 下面的示例删除`fn_SalesByStore`从用户定义函数`Sales`架构中的[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]示例数据库。 若要创建此函数，请参阅中的示例 B [CREATE FUNCTION &#40;Transact SQL &#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
```  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [OBJECT_ID &#40;Transact SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  

