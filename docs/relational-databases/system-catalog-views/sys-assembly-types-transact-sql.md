---
title: sys. assembly_types （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a5358b75da914919cb4db567dc7eae6ad8617f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118112"
---
# <a name="sysassembly_types-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  由 CLR 程序集定义的每个用户定义的类型对应一行。 以下 sys.databases 出现在继承列的列表中（在**rule_object_id**后，请参阅[transact-sql&#41;&#40;的 sys.databases ](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) **assembly_types** 。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|从中创建此类型的程序集的 ID。|  
|**assembly_class**|**sysname**|程序集内定义此类型的类的名称。|  
|**is_binary_ordered**|**bit**|对此类型的字节进行排序等同于对该类型使用比较运算符进行排序。|  
|**is_fixed_length**|**bit**|类型的长度始终与 max_length 相同。|  
|**prog_id**|**nvarchar （40）**|向 COM 公开的类型的 ProgID。|  
|**assembly_qualified_name**|**nvarchar(4000)**|程序集限定类型名。 该名称使用适合传递到 Type.GetType() 的格式。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的标量类型目录视图](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
