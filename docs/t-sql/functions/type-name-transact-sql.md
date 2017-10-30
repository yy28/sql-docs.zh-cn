---
title: "类型 _ 名称 (Transact SQL) |Microsoft 文档"
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
- TYPE_NAME_TSQL
- TYPE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- names [SQL Server], data types
- unqualified type names
- type names [SQL Server]
- data types [SQL Server], names
- TYPE_NAME function
ms.assetid: e4075a2e-5f70-440f-986b-9ec8434e07c1
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3d60bec3a21bb5b1127b0f18977d3485979f20b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="typename-transact-sql"></a>TYPE_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回指定类型 ID 的未限定的类型名称。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
TYPE_NAME ( type_id )   
```  
  
## <a name="arguments"></a>参数  
 *type_id*  
 要使用的类型的 ID。 *type_id*是**int**，而且它可以引用调用方有权访问任何架构中的类型。  
  
## <a name="return-types"></a>返回类型  
 **sysname**  
  
## <a name="exceptions"></a>异常  
 出现错误时或调用方没有查看对象的权限时，将返回 NULL。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，用户只能查看其拥有的安全对象的元数据，或者已对其授予权限的安全对象的元数据。 也就是说，如果用户对该对象没有任何权限，则某些会产生元数据的内置函数（如 TYPE_NAME）可能返回 NULL。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>注释  
 类型 _ 名称将返回 NULL 时*type_id*无效或调用方没有足够的权限引用的类型。  
  
 TYPE_NAME 既可用于系统数据类型，也可用于用户定义数据类型。 类型可以包含在任意架构中，但是始终返回一个未限定的类型名称。 这意味着名称没有*架构***。** 前缀。  
  
 在选择列表中，在 WHERE 子句中，可以使用系统函数和允许的表达式的任意位置。 有关详细信息，请参阅[表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)和[其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>示例  
 以下示例针对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的 `Vendor` 表中的每列返回对象名称、列名以及类型名称。  
  
```  
SELECT o.name AS obj_name, c.name AS col_name,  
       TYPE_NAME(c.user_type_id) AS type_name  
FROM sys.objects AS o   
JOIN sys.columns AS c  ON o.object_id = c.object_id  
WHERE o.name = 'Vendor'  
ORDER BY col_name;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
obj_name        col_name                  type_name
--------------- ------------------------ --------------
Vendor          AccountNumber            AccountNumber
Vendor          ActiveFlag               Flag
Vendor          BusinessEntityID         int
Vendor          CreditRating             tinyint
Vendor          ModifiedDate             datetime
Vendor          Name                     Name
Vendor          PreferredVendorStatus    Flag
Vendor          PurchasingWebServiceURL  nvarchar

(8 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例返回`TYPE ID`具有 id 的数据类型`1`。  
  
```  
SELECT TYPE_NAME(36) AS Type36, TYPE_NAME(239) AS Type239;  
GO  
```  
  
 有关类型的列表，查询 sys.types。  
  
```  
SELECT * FROM sys.types;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [TYPE_ID &#40;Transact SQL &#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPEPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.types (Transact-SQL)](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
  
  


