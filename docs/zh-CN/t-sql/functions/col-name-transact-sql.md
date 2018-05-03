---
title: COL_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
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
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 47991654f3d73645737872b0dda53ecc1c5c4052
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="colname-transact-sql"></a>COL_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函数根据表列的表标识号和列标识号值返回该表列的名称。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COL_NAME ( table_id , column_id )  
```  
  
## <a name="arguments"></a>参数  
table_id  
包含该列的表的标识号。 table_id 自变量具有一个 int 数据类型。
  
column_id  
列的标识号。 column_id 自变量具有一个 int 数据类型。
  
## <a name="return-types"></a>返回类型
**sysname**
  
## <a name="exceptions"></a>异常  
出现错误时或调用方没有查看对象的正确权限时将返回 NULL。
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，用户只能查看其所拥有的安全对象的元数据，或者已对其授予权限的安全对象的元数据。 这意味着，如果用户对该对象没有正确的权限，那些发出元数据的内置函数（如 `COL_NAME`）则可能会返回 NULL。 有关详细信息，请参阅[元数据可见性配置](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>Remarks  
table_id 和 column_id 参数共同产生一个列名称字符串。
  
有关获取表和列标识号的详细信息，请参阅 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)。
  
## <a name="examples"></a>示例  
此示例将返回示例 `Employee` 表中首列的名称。
  
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
[元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COLUMNPROPERTY (Transact-SQL)](../../t-sql/functions/columnproperty-transact-sql.md)  
[COL_LENGTH (Transact-SQL)](../../t-sql/functions/col-length-transact-sql.md)
  
  

