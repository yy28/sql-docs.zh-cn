---
title: DROP SENSITIVITY CLASSIFICATION (Transact-SQL) | Microsoft Docs
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- DROP SENSITIVITY CLASSIFICATION
- DROP_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SENSITIVITY CLASSIFICATION statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5e873944e68a05b29ed865572202e7e2b4438d76
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816893"
---
# <a name="drop-sensitivity-classification-transact-sql"></a>DROP SENSITIVITY CLASSIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

从一个或多个数据库列中删除敏感度分类元数据。

## <a name="syntax"></a>语法

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    <object_name> [, ...n ]

<object_name> ::=
{
    [schema_name.]table_name.column_name
}
```  

## <a name="arguments"></a>参数  

object_name ([schema_name.]table_name.column_name)

是从中删除分类的数据库列的名称。 目前仅支持列分类。
    - schema_name（可选）- 是已分类的列所属架构的名称。
    - table_name（可选）- 是已分类的列所属表的名称。
    - column_name - 是从中删除分类的列的名称。

## <a name="remarks"></a>Remarks  

- 可以使用单个“DROP SENSITIVITY CLASSIFICTION”语句删除多个对象分类。

## <a name="permissions"></a>Permissions  

需要“ALTER ANY SENSITIVITY CLASSIFICATION”权限。 “ALTER ANY SENSITIVITY CLASSIFICATION”由数据库权限“ALTER”或服务器权限“CONTROL SERVER”隐含。


## <a name="examples"></a>示例  


### <a name="a-dropping-classification-from-a-single-column"></a>A. 从单个列中删除分类

以下示例从列 `dbo.sales.price` 中删除分类。  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price
```

### <a name="b-dropping-classification-from-multiple-columns"></a>B. 从多个列中删除分类

以下示例从列 `dbo.sales.price``dbo.sales.discount` 和 `SalesLT.Customer.Phone` 中删除分类。  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price, dbo.sales.discount, SalesLT.Customer.Phone  
```

## <a name="see-also"></a>另请参阅  

[ADD SENSITIVITY CLASSIFICTION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[SQL 信息保护入门](http://aka.ms/sqlip)
