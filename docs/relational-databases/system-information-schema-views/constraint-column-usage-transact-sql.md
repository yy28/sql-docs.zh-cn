---
title: CONSTRAINT_COLUMN_USAGE （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_COLUMN_USAGE_TSQL
- CONSTRAINT_COLUMN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE view
- CONSTRAINT_COLUMN_USAGE view
ms.assetid: 0f3ae521-6b19-43ad-b2c4-3822adb19591
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e0936e74b3c48a2fe3298215107ae48d0c3b63cc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67950789"
---
# <a name="constraint_column_usage-transact-sql"></a>CONSTRAINT_COLUMN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为当前数据库中定义了约束的每一列返回一行。 该信息架构视图返回当前用户对其拥有权限的对象的相关信息。  
  
 若要从这些视图中检索信息，请指定 INFORMATION_SCHEMA 的完全限定名称 **。**_view_name_。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar （** 128 **）**|表限定符。|  
|**TABLE_SCHEMA**|**nvarchar （** 128 **）**|包含表所有者的架构名。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 不要使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象架构的唯一可靠方法是查询 sys.databases 目录视图。|  
|**TABLE_NAME**|**nvarchar （** 128 **）**|表名。|  
|**COLUMN_NAME**|**nvarchar （** 128 **）**|列名称。|  
|**CONSTRAINT_CATALOG**|**nvarchar （** 128 **）**|约束限定符。|  
|**CONSTRAINT_SCHEMA**|**nvarchar （** 128 **）**|包含该约束的架构的名称。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 不要使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象架构的唯一可靠方法是查询 sys.databases 目录视图。|  
|**CONSTRAINT_NAME**|**nvarchar （** 128 **）**|约束名称。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的系统视图 &#40;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [&#40;Transact-sql&#41;的信息架构视图](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [sys. check_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys. key_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys. foreign_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
