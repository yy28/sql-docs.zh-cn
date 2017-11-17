---
title: "COL_NAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COL_NAME
- COL_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- COL_NAME function
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 214144ab-f2bc-4052-83cf-caf0a85c4cc6
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: c697b619907bb3d80fbbff800b2ac29ef574af8d
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="colname-transact-sql"></a>COL_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

根据指定的对应表标识号和列标识号返回列的名称。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COL_NAME ( table_id , column_id )  
```  
  
## <a name="arguments"></a>参数  
*针对 table_id 所*  
包含列的表的标识号。 *针对 table_id 所*属于类型**int**。
  
*column_id*  
列的标识号。 *column_id*形参属于类型**int**。
  
## <a name="return-types"></a>返回类型
**sysname**
  
## <a name="exceptions"></a>异常  
出现错误时或调用方没有查看对象的权限时，将返回 NULL。
  
用户只能查看符合如下条件的安全对象的元数据：该安全对象为该用户所有，或已授予该用户对该安全对象的权限。 这意味着，如果用户对对象没有任何权限，则元数据生成的内置函数（如 COL_NAME）可能返回 NULL。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>注释  
*针对 table_id 所*和*column_id*参数组合，可生成一个列名称字符串。
  
有关获取表和列标识号的详细信息，请参阅[OBJECT_ID &#40;Transact SQL &#41;](../../t-sql/functions/object-id-transact-sql.md).
  
## <a name="examples"></a>示例  
下面的示例在一个示例中返回的第一列的名称`Employee`表。
  
```sql
-- Uses AdventureWorks  
  
SELECT COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 1) AS FirstColumnName,  
COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 2) AS SecondColumnName;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
ColumnName          
------------   
BusinessEntityID  
```  
  
## <a name="see-also"></a>另请参阅
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
[元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COLUMNPROPERTY (Transact-SQL)](../../t-sql/functions/columnproperty-transact-sql.md)  
[COL_LENGTH &#40;Transact SQL &#41;](../../t-sql/functions/col-length-transact-sql.md)
  
  


