---
title: sys.masked_columns (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.masked_columns
- masked_columns_tsql
- sys.masked_columns_tsql
- masked_columns
helpviewer_keywords:
- sys.masked_columns catalog view
ms.assetid: 671577e4-d757-4b8d-9aa9-0fc8d51ea9ca
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 432ea847081c8f0060954efdd6e7f2beea1a592d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33179293"
---
# <a name="sysmaskedcolumns-transact-sql"></a>sys.masked_columns (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用**sys.masked_columns**具有动态数据掩码函数应用于它们的表的列的查询视图。 该视图继承自 **sys.columns** 视图。 该视图会返回 **sys.columns** 视图中的所有列，以及 **is_masked** 和 **masking_function** 列，表明该列是否被屏蔽，以及在该列被屏蔽的情况下定义了什么屏蔽函数。 该视图仅显示在其上应用了屏蔽函数的列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|此列所属对象的 ID。|  
|name|**sysname**|列的名称。 在对象中是唯一的。|  
|column_id|**int**|列的 ID。 在对象中是唯一的。<br /><br /> 列 ID 可以不按顺序排列。|  
|**sys.masked_columns**返回继承自的多个列的多**sys.columns**。|各种|请参阅[sys.columns &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)的更多列定义。|  
|is_masked|**bit**|指示是否屏蔽列。 1 表示掩码。|  
|masking_function|**nvarchar(4000)**|列则屏蔽函数。|  
  
## <a name="remarks"></a>注释  
  
## <a name="permissions"></a>权限  
 此视图返回有关表的信息，其中用户对表具有某种形式的权限，或者用户是否拥有 VIEW ANY DEFINITION 权限。  
  
## <a name="example"></a>示例  
 下面的查询联接**sys.masked_columns**到**sys.tables**返回有关所有信息屏蔽列。  
  
```  
SELECT tbl.name as table_name, c.name AS column_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.object_id = tbl.object_id  
WHERE is_masked = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [动态数据屏蔽](../../relational-databases/security/dynamic-data-masking.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
