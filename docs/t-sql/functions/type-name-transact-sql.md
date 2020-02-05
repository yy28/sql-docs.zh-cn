---
title: TYPE_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33f282c79c15a8b9548d799ef86e026fd7357d00
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68098703"
---
# <a name="type_name-transact-sql"></a>TYPE_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回指定类型 ID 的未限定的类型名称。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
TYPE_NAME ( type_id )   
```  
  
## <a name="arguments"></a>参数  
 type_id   
 要使用的类型的 ID。 type_id 的数据类型为 int，它可以引用调用方有权访问的任意架构中的类型   。  
  
## <a name="return-types"></a>返回类型  
 **sysname**  
  
## <a name="exceptions"></a>例外  
 出现错误时或调用方没有查看对象的权限时，将返回 NULL。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，用户只能查看其拥有的安全对象的元数据，或者已对其授予权限的安全对象的元数据。 也就是说，如果用户对该对象没有任何权限，则某些会产生元数据的内置函数（如 TYPE_NAME）可能返回 NULL。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>备注  
 当 type_id 无效或当调用方没有足够权限引用类型时，TYPE_NAME 将返回 NULL  。  
  
 TYPE_NAME 既可用于系统数据类型，也可用于用户定义数据类型。 类型可以包含在任意架构中，但是始终返回一个未限定的类型名称。 这表示名称不具有 schema.   前缀。  
  
 系统函数可以在选择列表、WHERE 子句和任何允许使用表达式的地方使用。 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md) 和 [WHERE (Transact-SQL)](../../t-sql/queries/where-transact-sql.md)。  
  
## <a name="examples"></a>示例  
 以下示例针对 `Vendor` 数据库的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 表中的每列返回对象名称、列名以及类型名称。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例返回具有 `TYPE ID` ID 的数据类型的 `1`。  
  
```  
SELECT TYPE_NAME(36) AS Type36, TYPE_NAME(239) AS Type239;  
GO  
```  
  
 有关类型列表，请查询 sys.types。  
  
```  
SELECT * FROM sys.types;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [TYPE_ID (Transact-SQL)](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPEPROPERTY (Transact-SQL)](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.types (Transact-SQL)](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)  
  
  

